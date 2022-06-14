---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 프로토타입 패턴 # 제목
excerpt             : Creational Prototype Pattern # 썸네일 한줄 요약
categories          : DesignPattern Creational
tags                : DesignPattern GoF Creational Prototype
---

출처: [Springframework Guru - Prototype pattern](https://springframework.guru/gang-of-four-design-patterns/prototype-pattern/), [Refactoring Guru - Prototype pattern](https://refactoring.guru/design-patterns/prototype)  
🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

## Prototype Pattern<br>(프로토타입 패턴)

생성 패턴(Object Creational)

객체를 간단하게 복제하는 기능에 대한 패턴이다.  
여기서의 복제는 그 목적에 따라 [깊은 복사와 얕은 복사](../../../basic/shallow_copy_and_deep_copy/)로,  
요구되는 스펙에 맞게 선택해 구현한다.  

구현에 요구되는 클래스는 아래와 같다.  

- Prototype: 복제를 허용하는 객체의 인터페이스 또는 추상 클래스
- ConcretePrototype: 복제 기능을 제공하는 클래스
- PrototypeManager: 프로토타입들을 생성하고 관리하는 클래스(생략 가능)
- Client: PrototypeManager에게 Prototype 복제본을 요청하는 요청자

## Class diagram

<img src="/assets/images/posts/2022-06-10-prototype/diagram.png" alt="클래스_다이어그램">

## 예시

```java
// Prototype - 복제를 허용하는 객체의 인터페이스 또는 추상 클래스
public abstract class PrototypeCapableDoc implements Cloneable {
    private String data;

    public String getData() { return data; }

    public void setData(String data) { this.data = data; }

    // 복제 기능의 추상메소드
    public abstract PrototypeCapableDoc cloneDoc() throws CloneNotSupportedException;
}
```

```java
// ConcretePrototype - 복제 기능을 제공하는 클래스(얕은 복사 예시)
public class ShallowCopyDoc extends PrototypeCapableDoc {
    @Override
    public PrototypeCapableDoc cloneDoc() {
        // 다른 참조 필드가 없기 때문에 얕은 복사로도 충분하다.
        try {
            return (ShallowCopyDoc) super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

```java
// 바로 밑의 DeepCopyDoc 클래스의 참조타입 필드가 되는 클래스.
// 깊은 복사의 과정을 보여주기 위한 예시
public class InnerObj implements Cloneable {
    private String name;
    
    public String getName() { return name; }
    
    public void setName(String name) { this.name = name; }
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

```java
// ConcretePrototype - 복제 기능을 제공하는 클래스(깊은 복사)
public class DeepCopyDoc extends PrototypeCapableDoc {
    private InnerObj innerObj; // 참조타입 필드
    
    public InnerObj getInnerObj() { return innerObj; }

    public void setInnerObj(InnerObj innerObj) { this.innerObj = innerObj; }

    @Override
    public PrototypeCapableDoc cloneDoc() throws CloneNotSupportedException {
        // 깊은 복사 추상메소드 구현
        DeepCopyDoc dcDoc = (DeepCopyDoc) super.clone();
        // 참조타입 필드의 데이터도 확실하게 복제해야한다.
        InnerObj clonedInnerObj = (InnerObj) dcDoc.getInnerObj().clone();
        dcDoc.setInnerObj(clonedInnerObj);
        return dcDoc;
    }

}
```

```java
// PrototypeManager - 프로토타입들을 생성하고 관리하는 클래스(생략 가능)
// 관리자를 따로 분리함으로써 프로토타입의 오염을 방지한다
public class DocPrototypeMgr {
    private static Map<String, PrototypeCapableDoc> prototypes = new HashMap<String, PrototypeCapableDoc>();
    static {
        // 원본이 되는 프로토타입들을 생성, 키워드로 저장
        ShallowCopyDoc scDoc = new ShallowCopyDoc();
        scDoc.setData("ShallowCopyDoc data...");
        prototypes.put("SCDoc", scDoc);

        InnerObj innerObj = new InnerObj();
        innerObj.setName("InnerObj name...");

        DeepCopyDoc dcDoc = new DeepCopyDoc();
        dcDoc.setData("DeepCopyDoc data...");
        dcDoc.setInnerObj(innerObj);
        prototypes.put("DCDoc", dcDoc);
    }

    // 요청시, 프로토타입들의 복제본을 반환
    public static PrototypeCapableDoc getClonedDoc(final String type) {
        try {
            PrototypeCapableDoc doc = prototypes.get(type);
            return doc.cloneDoc();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

## 테스트

```java
PrototypeCapableDoc clonedSCDoc1 = DocPrototypeMgr.getClonedDoc("SCDoc");
PrototypeCapableDoc clonedSCDoc2 = DocPrototypeMgr.getClonedDoc("SCDoc");
// clonedSCDoc1.getData(): "ShallowCopyDoc data..."
// clonedSCDoc2.getData(): "ShallowCopyDoc data..."
clonedSCDoc2.setData("Some data 2");
// clonedSCDoc1.getData(): "ShallowCopyDoc data..."
// clonedSCDoc2.getData(): "Some data 2"

PrototypeCapableDoc clonedDCDoc1 = DocPrototypeMgr.getClonedDoc("DCDoc");
PrototypeCapableDoc clonedDCDoc2 = DocPrototypeMgr.getClonedDoc("DCDoc");
// clonedDCDoc1.getInnerObj().getName(): "InnerObj name..."
// clonedDCDoc2.getInnerObj().getName(): "InnerObj name..."
dcDoc2 = (DeepCopyDoc) clonedDCDoc2;
dcDoc2.getInnerObj().setNata("Some name 2");
// clonedDCDoc1.getInnerObj().getName(): "InnerObj name..."
// clonedDCDoc2.getInnerObj().getName(): "Some name 2"
```

## 장점

- 구현 클래스와의 연결점이 없어도 복제가 가능
  - Object clonedObj = cloneableObj.clone();
- 이미 완성된 프로토타입과 중복되는 초기화 코드 삭제 가능
- 복잡한 객체를 간편하게 생성 가능
- 상속 관계 발생을 줄여준다
  - 복제 후 변경해서 사용하는 것이 서브 클래싱의 대안이 될 수 있다
- 런타임에서 객체의 추가 또는 삭제가 가능하다

## 단점

- 순환참조되는 복잡한 객체의 경우 굉장히 번거로워질 수 있다
- 원시 타입을 제외한 내부 필드의 클래스들도 모두 복제 추상메소드를 구현해야 한다
- 기존의 클래스에 복제 기능을 추가하는것은 번거로워질 수 있다
