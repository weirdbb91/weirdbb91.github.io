---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Spring state machine # 제목
excerpt             : Spring state machine 사용법 정리 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Spring StateMachine
---

출처 모름: 그냥 알던거 정리  

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

일반적인 [State machine](https://en.wikipedia.org/wiki/Finite-state_machine)의 개념을 Spring Project로 그대로 가져온 Framework입니다.

[간단 소개 링크](https://spring.io/projects/spring-statemachine)

## 구성

- State: 관리의 대상이 되는 상태 값

  - Initial State: 초기 상태값  
![image](https://user-images.githubusercontent.com/50126248/210174713-3b1090fc-aef1-4bf3-af4f-00ba00c1465c.png)  
  - End State: 완료 상태값  
![image](https://user-images.githubusercontent.com/50126248/210174731-9c6db5a7-a92b-4d75-86d7-a11c1d541aff.png)  
  - Source State: 변경 이전의 원래 상태  
![image](https://user-images.githubusercontent.com/50126248/210174774-072e9644-2e9f-4281-99bb-fb9d9485c509.png)  
  - Target State: 변경을 목표로 하는 상태  
![image](https://user-images.githubusercontent.com/50126248/210174778-b2cb19f5-0b84-4020-ab31-a0ac79068fbb.png)  
- StateMachine: State의 변경 규칙 명세  
![image](https://user-images.githubusercontent.com/50126248/210174794-c30460c6-a1c0-409d-ad27-dd793123db4a.png)  
- Event: State에 변경이 발생하게 되는 계기  
  ex) 장착, 탈착, 폐기 등

- Transition: State의 변경, 변이, 변화 등  
![image](https://user-images.githubusercontent.com/50126248/210174804-cc09f410-c65a-4992-9d09-562a819caa3f.png)  
- Guard: Event가 발생했을 때, 조건을 검증하는 관문(반환값이 false일 경우, Transition은 일어나지 않는다.)

  - 폐기 Event 발생시의 Guard 예시) Source State == 유휴 && 폐기 승인 목록에 존재

- Action: Transition 발생 후 실행되는 행위

  - 폐기 Event 발생시의 Action 예시) 폐기 완료 알림 전송

## 의존성

Gradle

```java
implementation 'org.springframework.statemachine:spring-statemachine-core:2.1.3.RELEASE'
```

2022년 12월 26일 기준 최신 버전은 3.2.0이나,  
해당 버전에는 기존의 상태 처리 방식들이 Deprecated 처리 되어 있고  
비동기 처리를 강제하고 있어개발 편의상 2.1.3.RELEASE 버전을 사용했습니다.

## 사용 방법 - [2.1.3.RELEASE 문서 Link](https://docs.spring.io/spring-statemachine/docs/2.1.3.RELEASE/reference/#statemachine-getting-started)

1. State 및 Event 정의

    관리할 State와 Event를 Enum 타입으로 정의합니다.  
    String 타입으로도 가능하지만, 유지보수 편의성을 위해 Enum 타입으로 정의하겠습니다.  
    ![image](https://user-images.githubusercontent.com/50126248/210174892-090ba990-427e-4e61-b6fb-ed23be8002cb.png)  
2. State machine 설정

    1. Entity에 필드로 State 추가  
    ![image](https://user-images.githubusercontent.com/50126248/210174906-f482fd5f-7313-460f-b8e3-42183501321c.png)  
    2. Entity Repository 생성  
    ![image](https://user-images.githubusercontent.com/50126248/210174924-60425a10-159a-4d87-83e5-339a41e38ab2.png)  
    ![image](https://user-images.githubusercontent.com/50126248/210174928-dd98a7b0-aea0-400a-b9d0-b64968772ddf.png)  
    ![image](https://user-images.githubusercontent.com/50126248/210174935-500834fd-2248-42cf-86a6-c02ab431522d.png)  
    3. StateMachineConfigurerAdapter를 상속받는 설정 Class를 생성합니다.  
    ![image](https://user-images.githubusercontent.com/50126248/210174949-56cce44d-e936-4da2-b270-22492ff53b60.png)  
    StateMachineFactory를 사용할 수 있도록 @EnableStateMachineFactory을 꼭 추가해줍니다.  
        1. State 등록  
        ![image](https://user-images.githubusercontent.com/50126248/210174982-0b55b25d-f246-4c49-bdc1-0b3791f36396.png)  
        위와 같이 Initial State와 End State, 그리고 사용할 모든 State를 등록해줍니다.

        2. Transition 설정  
        ![image](https://user-images.githubusercontent.com/50126248/210175025-c2d5f49f-3a95-474a-a1b3-8121b5d9a61b.png)  
        위와 같이 어떤 Source state에서 어떤 Event가 발생했을 때 어떤 Target state로 Transition이 발생하고,해당 Transition에 어떤 guard나 action이 있는지 추가해줍니다.

        3. StateMachineListener 등록(선택)  
        ![image](https://user-images.githubusercontent.com/50126248/210175038-85f58c8d-4c75-4947-bef8-df85d49a3b71.png)  
        필요하다면, State의 변경사항을 감지해 특정 로직을 수행하는 Listener를 등록합니다.

3. MediaStateChangeInterceptor  
![image](https://user-images.githubusercontent.com/50126248/210175054-a89e8a22-4292-48ef-9b77-0d99bfffa30e.png)  
위 인터셉터의 목적은 state 변경사항을 Entity에 반영하기 위함입니다.  
그러므로 Entity를 수정하기 위해 Entity Repository를 필드로 가집니다.  
StateMachineInterceptorAdapter<>를 상속받아,  
State가 변경되기 전에 호출되는 preStateChange 메소드를 Override합니다.  
preStateChange 메소드 안에서 메시지의 Header를 통해 Entity의 id를 찾아서  
변경된 state로 Entity를 수정해줍니다.

4. Entity Service에 StateMachineFactory 추가  
![image](https://user-images.githubusercontent.com/50126248/210175080-fa82d2c6-f68b-4f08-814e-93c327e5ed3e.png)  

   - MEDIA_ID_HEADER: 아래에서 다루는 Message의 HeaderName이 될 값

   - MediaStateChangeInterceptor: state 변경사항을 Entity에 반영하는 인터셉터

       Entity Service에 위 두 필드와 함께 StateMachineFactory를 추가합니다.

       1. StateMachine 인스턴스 가져오기  
           ![image](https://user-images.githubusercontent.com/50126248/210175186-8d6154b7-4bc3-45b1-98e8-0edce705658b.png)  
           build(Long mediaId) 메소드에서는 stateMachineFactory의  
           getStateMachine(String machineId) 메소드를 통해  
           StateMachine 인스턴스를 생성해 반환 받습니다.  
           Accessor를 이용해 state 변경사항을 반영하는 인터셉터를 추가하고,  
           마지막으로 Media(Entity)의 state로 StateMachine을 초기화 해 반환합니다.  

       2. Event 생성  
           ![image](https://user-images.githubusercontent.com/50126248/210175199-c8e75109-ea7b-4d0a-b1a3-2245f8f51996.png)  
           sendEvent(Long mediaId, StateMachine<> sm, MediaEvent event) 메소드에서는  
           StateMachine에 Event를 전송합니다.  
           이 때 MEDIA_ID_HEADER를 headerName으로 가지는 Header를 Message에 추가해서  
           Event가 발생한 Media(Entity)의 id를 전달합니다.

       3. 실 사용 예시  
           ![image](https://user-images.githubusercontent.com/50126248/210175222-e304610b-012c-4e76-a5dc-22da92ac39f3.png)  
           위 4.1에서 설명한 build 메소드로 StateMachine 인스턴스를 받아,  
           위 4.2에서 설명한 sendEvent 메소드를 통해 Event를 전송합니다.

5. 실 사용 흐름 정리

   1. Entity의 State로 초기화 된 StateMachine에 Event를 전송합니다.

   2. Guard 검증 - True인 경우만 통과

   3. Action 실행

   4. StateMachineListenerAdapter의 transition Method 실행

   5. 인터셉터에서 State의 변경을 수신해 해당 Entity의 State를 변경

   6. StateMachineListenerAdapter의 stateChanged Method 실행

6. 기타

   1. Guard  
    ![image](https://user-images.githubusercontent.com/50126248/210175356-76b39aa4-abed-478a-ac34-5bcc0a669007.png)  
    위의 Guard 예시는 Event가 발생했을 때 Header로 전달한 Media(Entity)의  
    id를 StateContext에서 가져와 MediaRepository(Entity Repository)를 활용해  
    해당 Media(Entity)를 찾아냅니다.  
    ![image](https://user-images.githubusercontent.com/50126248/210175367-31d87685-3eb9-4304-a8a8-4932aab6ca39.png)  
    그리고 찾아낸 Media(Entity)가 Transition 발생 조건에 부합하는지  
    확인(boolean값 반환)합니다.  
       - 발생 조건을 검증하는데에 Entity가 필요없다면,  
         MediaRepository를 설정 class에 추가할 필요가 없습니다.

   2. Action  
    ![image](https://user-images.githubusercontent.com/50126248/210175377-4183412a-f6d9-4798-bb73-929d6dcdb93b.png)  
    Action 또한 Guard와 마찬가지로 StateContext를 받아  
    Transition이 끝나고 실행할 행동들을 정의합니다.
