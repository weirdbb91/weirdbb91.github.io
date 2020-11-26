---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 자바 코드 컨벤션 # 제목
excerpt             : Java Code Conventions # 썸네일 한줄 요약
last_modified_at    : 2020-11-26 # 2020-11-22 # 작성일 또는 마지막 수정일
categories          : course # java dataStructure algorithm git liquid math course / workout journal
tags                : conventions
toc                 : # 목차 사용 default: true
toc_label           : # 목차 제목 default: "목차"
# 알림박스 = {: .notice--info}
---
---

[자바 코드 컨벤션](https://google.github.io/styleguide/javaguide.html#s2.1-file-name)을 읽고 그 일부를 정리해봤다.

출처 : [https://google.github.io/styleguide/javaguide.html#s2.1-file-name](https://google.github.io/styleguide/javaguide.html#s2.1-file-name)

---
---

# 1 용어 참고

 * `클래스(class)`는 일반 클래스, 열거형 클래스, 인터페이스 또는 주석유형(@interface)을 의미합니다.  
 * 클래스의 `멤버(member)`는 중첩 클래스, 필드, 메서드 또는 생성자를 의미합니다.  
      즉, 이니셜 라이저와 주석을 제외한 클래스의 모든 최상위 콘텐츠입니다.  
 * `주석(comment)` 이라는 용어 는 항상 구현 주석을 의미합니다.  
      "문서 주석(documentation comments)"이라는 문구는 사용하지 않습니다.  
      대신 "Javadoc"이라는 일반적인 용어를 사용합니다.  

---
---
# 2 소스 파일 기본

**2.1 파일 이름**

소스 파일의 이름은 최상위 클래스의 이름(정확히 하나만 있음, 대소문자 구분)과 .java확장자로 구성됩니다.

---

**2.3.1 공백 문자**

소스파일에서 사용하는 공백 문자는 오직 ASCII 가로 공백 문자(0x20) 하나 입니다.  
(줄 마침 시퀀스 제외)  

 * 문자열과 코드의 다른 모든 공백문자는 이스케이프 됩니다
 * 탭 문자는 들여쓰기(indent)에 사용 되지 않습니다

---

**2.3.2 특수 이스케이프 시퀀스**

이스케이프 시퀀스 `( \b, \t, \n, \f, \r, \", \', \\ 등)`는 그대로 쓰는것을 권장합니다  
8진수나 (e.g. \012) Unicode (e.g. \u000a) 등으로 대체하지 않습니다

---

**2.3.3 Non-아스키 문자**

나머지 non-ASCII 문자의 경우 실제 유니코드문자 (예 : `∞`) 또는  
동등한 유니코드 이스케이프(예 :`\u221e`)가 사용됩니다.  
코드를 더 쉽게 읽고 이해할 수 있는 방법에 따라 선택이 달라집니다

|예시|평가|
|-|-|
|String unitAbbrev = "μs";|최고 : 주석없이도 깔끔합니다|
|String unitAbbrev = "\u03bcs"; // "μs"|허용 : 그러나 이럴 이유가 없습니다|
|String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"|허용 : 그러나 어색하고 실수하기 쉽습니다|
|String unitAbbrev = "\u03bcs";|나쁨 : 이게 뭔지 아무도 모릅니다.|
|return '\ufeff' + content; // byte order mark|좋음 : 타이핑 할 수 없는 문자는 이스케이프 문자를 사용하고 필요한 경우 주석을 추가합니다.|

---
---
# 소스 파일 구조

소스 파일은 다음의 순서로 작성합니다.
1. 라이센스 또는 저작권 정보(있다면)
2. Package
3. Import
4. 단 하나의 최상위 클래스

각각 사이에 빈 줄 하나씩 넣어서 구역을 구분합니다

---

**3.1 라이센스나 저작권 정보**가 파일에 있다면 작성합니다 

---

**3.2 Package**는 100자가 넘어도 줄을 바꾸지 않습니다

---

**3.3 Import**

---

**3.3.1 와일드 카드(*) 사용금지**

```java
import java.util.*;
```

위 같은 와일드 카드(*)는 쓰지 않습니다

---

**3.3.2 줄바꿈 없음**

import시에 100자가 넘어도 줄을 바꾸지 않습니다

---

**3.3.3 순서와 간격**

static import 먼저하고  
사이에 빈줄 한줄  
non-static import 작성합니다  

중간에 다른 빈줄은 없습니다

---

**3.3.4 static 중첩 클래스 static import 금지**

일반 import입니다

---

**3.4 class 선언**

---

**3.4.1 단 하나의 최상위 클래스 선언**

---
---

## 4 서식

---

**4.1 괄호**

if, else, for, do, while등의 문에 내용이 비어 있어도 {} 중괄호는 쳐줍니다.

---

**4.1.3 빈블록**

내용이 없다면 중괄호를 닫기 전에 개행할 필요가 없습니다  
{} 또는 { } 가능

---

**4.2 블록 들여쓰기**
들여쓰기(indent) 단위는 2칸입니다

---

**4.3 한줄에 한 문만** 작성하도록 합니다

---

**4.4 한줄 제한: 100자**  한줄에 100자 넘기지 않도록 합니다

예외: 불가능할 때, package, import, shell에 붙여 넣을수 있는 주석의 명령줄

---

**4.5 줄 바꿈**

합당하게 한 줄을 차지 할 수 있는 코드를 여러 줄로 나누는 것을 줄 바꿈(Line-wrapping)이라고 합니다

---

**4.5.1 끊는 지점**

더 높은 수준의 구문에서 끊는 것이 주요 원칙입니다
1. 비할당연산자에서 줄이 끊기면 기호 앞에서 끊습니다
   * 다음의 기호들에도 적용됩니다
     + 마침표 `.`
     + 메서드 참조 기호 `::`
     + type bound의 앰퍼센드 ex. <T extends Foo `&` Bar>
     + catch블록의 pipe ex. catch (FooException `|` BarException e)
2. 할당연산자에서 끊기면 보통 기호 뒤에서 끊지만 상관없습니다
   * 이는 foreach문에서 할당연산자 역할을 하는 `:`에도 적용됩니다
3. 메서드 또는 생성자 이름 뒤의`(`는 붙인 상태로 둡니다
4. 쉼표`,` 는 앞의 토큰에 붙인 상태로 둡니다
5. 람다의 본문이 중괄호 없는 단일식일 때는 화살표 바로 뒤에서 줄을 바꿀수도 있습니다
   * 아래의 예제를 확인합니다 
```java
MyLambda<String, Long, Object> lambda =
    (String label, Long value, Object obj) -> {
        ...단일식 아니면 괄호 열고나서 바꾸자...
    };

Predicate<String> predicate = str ->
    longExpressionInvolving(str);
```

---

**4.5.2 줄 바꿈시 최소 4공백**

이어지는 원래의 줄을 기준으로 최소 4개 공백을 더해서 들여쓰기 합니다  
한줄을 여러번 줄 바꿈 할 때는 4개 이상으로 원하는 만큼 들여쓰기 가능합니다  

---

**4.6 공백**

**4.6.1 줄 공백(빈 줄)Vertical Whitespace**

아래의 해당되는 경우에 단 하나의 줄을 통째로 비운다
 1. 연속된 클래스 이니셜라이져 또는 멤버 사이 : 필드, 생성자, 메서드, 중첩 클래스,  
      static 이니셜라이져, 인스턴스 이니셜라이져
      * 예외 : 두 개의 연속된 필드 사이에 다른 코드가 없다면 빈 줄은 선택 사항입니다  
               이러한 빈 줄은 필드 로직의 그룹화를 위해 쓰입니다
      * 예외 : enum 상수 사이 (4.8.1에서 추가로 설명함)
 2. 이 문서에 기재된 내용이 요구시
 3. 가독성을 위해 필요시 : 첫번째 멤버, 이니셜라이져, 클래스의 마지막 멤버 등

---

**4.6.2 분리 공백(띄어쓰기)Horizontal Whitespace**

기타 요구사항과 리터럴, 주석 및 Javadoc을 제외하고 ASCII 공백은 다음의 위치에만 사용합니다
1. 예약어와 여는 괄호 사이 ex. if (, for (, catch ( 등
2. 닫는 중괄호와 else 또는 catch 등의 예약어 사이 ex. } else {, } catch { 등
3. 여는 중괄호 앞, 두 가지 예외
   * 예외 : @Annotation({a, b})
   * 예외 : String[][] x = {{"foo"}}; (아래 8번 항목에 의함)
4. 이항 또는 삼항 연산자의 양쪽과 다음의 연산자 유사 기호에도 적용
   * 접속어 타입 bound의 앰퍼샌드 : <T extends Foo `&` Bar>
   * 다수의 예외를 처리하는 catch 블록의 pipe : catch (FooException `|` BarException e)
   * foreach문에서의 `:`
   * 람다 식의 화살표 : (String str) `->` str.length()<br><br>
     아래의 경우 제외
   * 메소드 참조 `::`는 분리하지 않습니다. Object`::`toString
   * 구분기호 `.`도 분리하지 않습니다. object`.`toString();
5. Cast의 `)` , 구분기호 `,` , 콜론 `:` , 세미콜론 `;` 의 뒷 부분
6. 줄 끝 주석의 `//` 양 옆, 다중 공백이 허용되지만 불필요합니다
7. 선언문의 변수 타입과 변수명 사이 List<String> list
8. 배열 이니셜라이저의 두 중괄호 바로 안쪽(선택)  
   new int[] {5, 6}, new int[] `{` 5, 6 `}` 둘 다 유효
9. type annotation과 [] 사이  

이 규칙은 줄의 시작이나 끝에 추가하는 공백을 요구하거나 금지하지 않습니다.  
줄 내부에 한해서 적용됩니다.  

---

**4.6.3 수평정렬(불필요)**

아래의 수평정렬은 Google 스타일에서 권장하지 않습니다.

```java
private int x; // 좋습니다
private Color color; // 마찬가지

private int   x;      // 허용되지만, 향후 수정에
private Color color;  // 번거로운 요소로 작용합니다
```

수평정렬시 추후 수정하게 됐을 때 "폭발 반경"을 갖습니다.  
이는 최악의 경우 쓸데없는 무의미한 작업을 초래합니다.  
심지어 최선의 경우에도 버전 히스토리 정보를 망가뜨리고  
검토자의 속도를 늦추고 병합 충돌을 심화시킵니다.

네 그냥 하지 말라고 하네요

---

**4.7 그룹화 용도의 괄호 : 권장**

그룹화 용도의 괄호는 작성자와 리뷰어가 아래 사항들에 동의 할 때 생략합니다.
 1. 괄호가 없어도 코드가 오해를 야기하지 않음
 2. 괄호가 가독성에 도움이 안됨
 3. 모든 독자가 자바의 모든 연산자 우선순위를 외우고 있다고  
    가정하는것은 합리적이지 않음

---

**4.8 특정 구조**

---

**4.8.1 Enum 클래스**

열거형 상수(enum constant) 의 쉼표, 뒤에 오는 줄 바꿈은 선택사항입니다  
한다고 해도 한 줄만 합니다  

```java
private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },

  NO,
  MAYBE
}
```

메서드나 다른 documentation이 없으면 배열 초기화하듯 해도 됩니다

```java
private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
```

enum 클래스도 클래스이므로, 다른 클래스들과 마찬가지의 규칙을 적용합니다

---

**4.8.2 변수 선언**

---

**4.8.2.1 한줄에 하나씩만 선언**

```java
int a, b; // 이런거 하지마세요 (for문 header 예외)
```

---

**4.8.2.2 필요할 때 선언**

지역변수들을 습관적으로 구조 첫부분에 선언하지 마세요  
대신, 처음 사용되는 부분에 가깝도록 선언해 범위를 최소화 하세요  
일반적으로 지역변수의 초기화는 선언과 동시에 또는 직후에 합니다  

---

**4.8.3 배열**

---

**4.8.3.1 배열을 초기화 할 때: 블록처럼 해도 됨**

```java
new int[] {           new int[] {
  0, 1, 2, 3            0,
}                       1,
                        2,
new int[] {             3,
  0, 1,               }
  2, 3
}                     new int[]
                          {0, 1, 2, 3}
```

**4.8.3.2 C 스타일 배열 선언 금지**

대괄호는 변수가 아닌 자료형에 붙입니다 

```java
String[] args // 굿
String args[] // 금지 C 스타일 ㄴㄴ
```

---

**4.8.4 Switch 문**

---

**4.8.4.1 들여 쓰기**

다른 블록과 마찬가지로 스위치 블록 또한 2칸 들여쓰기 합니다.

---

**4.8.4.2 fall through : 주석 달기**

switch 내에서 바로 종료(break, continue, return, 예외 발생)되거나  
다음 그룹으로 실행이 이어질 수 있는 case에는 주석을 달아도 됩니다  
(일반적으로 // fall through)  
이 주석은 switch 문의 마지막 case에는 안씁니다.

```java
switch (input) {
  case 1: // 아무것도 없는데 뭐하러 써
  case 2:
    prepareOneOrTwo();
    // fall through       <- 굿
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input); // 아 안써요
}
```

`case 1:` 에는 주석 안씁니다 명령문 case 끝에만 주석을 달도록 합니다 

---

**4.8.4.3 default case가 있어야 됩니다**

switch 문에는 빈 칸이더라도 default는 꼭 넣어줍시다

예외: enum에 대한 switch문이 해당 유형의 모든 값을 커버하면 생략 가능  
근데 하나라도 놓치면 IDE나 다른 분석도구에서 경고가 발생 할 수 있습니다.  

---

**4.8.5 Annotations**

클래스, 메서드, 생성자에 적용되는 Annotations은 documentation​​ 바로 뒤에 붙이고  
각 Annotations은 depth 맞춰서 한 줄에 하나씩 씁니다  

```java
@Override // 이게 Annotation
@Nullable // 얘도 Annotation
public String getNameIfPresent() { ... }
```

예외: 파라미터도 없고 딱 하나만 있는거면 한줄에 같이 써도 됩니다

```java
@Override public int hashCode () { ... }
```

필드에 붙이는 Annotation도 원래 바로 붙이는게 맞는데  
(매개변수화가 가능하면) 여러개를 한줄에 쓰는것 도 허용됨  

```java
@Partial @Mock DataLoader loader;
```

매개변수, 지역변수, 자료형에 대한 Annotation 규칙은 따로 없습니다

---

**4.8.6 주석**

여기서는 구현 주석을 다룹니다. Javadoc은 섹션 7에서 별도로 다루고 있습니다.

---
**4.8.6.1 블록 주석 스타일**

블록 주석은 주변 코드와 동일한 깊이에서 들여쓰기됩니다.

```java
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```

팁: 여러 줄 쓸 때 /* ... */ 이거 쓰면 코드 포맷터가 스타일링 해줌  
한줄용 주석 // 이거는 대부분 그런거 안해줌

---

**4.8.7 수정자(Modifiers)**

클래스 및 멤버의 수정자는 Java 언어에서 권장하는 아래의 순서로 씁니다.

```java
public protected private abstract default static final transient volatile synchronized native strictfp
```

---

**4.8.8 Numeric Literals**

long 타입을 명시할 때는 대문자 `L`을 씁니다(소문자 금지)  
1과의 혼동을 피하기 위함  
```java
 3000000000L /* <- O */ 3000000000l // <- X
```

---
---

## 5 이름 짓기 Naming

---

**5.1 모든 식별자의 공통규칙**

식별자는 `ASCII 문자`와 `숫자`만 사용하며 특별한 경우만 밑줄`_`을 허용합니다  
따라서 각 유효한 식별자 이름은 정규식에 사용될 수 있습니다 `\w+.`

Google 스타일에서는 특별한 접두사 또는 접미사를 안씁니다. 
```java
name_, mName, s_name, kName // 전부 금지
```

---

**5.2.1 패키지 이름**

패키지 이름은 모두 소문자로 단순하게 쭉 이어 씁니다  
```java
package com.example.deepspacenot // 굿
package com.example.deepSpace // 대문자 금지
package com.example.deep_space // 언더바 금지
```

---

**5.2.2 클래스 이름**

클래스 이름은 각 단어 앞글자만 대문자를 쓰는 UpperCamelCase로  
일반적으로 명사 또는 명사구로(ex. Character, ImmutableList 등) 작성.  

인터페이스 이름은 클래스와 마찬가지로(ex. List) 작성하지만  
때로는 형용사 또는 형용사구도(ex. Readable) 가능합니다.

Annotation 이름에 대한 특정 규칙이나 확립된 규칙은 없습니다.

테스트 클래스는 테스트중인 클래스의 이름 뒤에 Test를 붙임  
(ex. HashTest, HashIntegrationTest 등)

---

**5.2.3 메서드 이름**

메소드 이름은 UpperCamelCase에서 맨 앞 첫 자를 소문자를 쓰는  
lowerCamelCase로 작성합니다.

메서드 이름은 일반적으로 동사 또는 동사구(ex. endMessage, stop)

JUnit Test 메서드는 특별히 밑줄`_`로 논리적 구성요소를 구분할 수 있고  
각 구성 요소는 lowerCamelCase로 작성됩니다.  
전형적인 방식 중에 하나로 `<methodUnderTest>_<state>`가 있고  
(ex. pop_emptyStack) 테스트 방법의 이름을 정하는 규정은 없습니다.

---

**5.2.4 상수 이름**

상수는 각 대문자 단어를 밑줄로 구분하는 CONSTANT_CASE 방식이다  

상수는 값이 완전 불변하고 메서드에서 부작용이 없는 static final 필드입니다.  

상수에는 프리미티브, 문자열, 불변 유형, 불변 타입의 불변 컬렉션이 포함됩니다.  
인스턴스의 상태가 변경이 가능하다면 상수가 아닙니다.  
단순히 객체를 변화시킬 의도가 없는것 만으로는 충분하지 않습니다. 

```java
// 상수
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap<String, Integer> AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // Joiner는 불변
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// 상수 아님
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
    ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```



