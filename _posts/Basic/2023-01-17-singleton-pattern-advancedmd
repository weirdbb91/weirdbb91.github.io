---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : GoF Singleton Pattern Advanced # 제목
excerpt             : 싱글톤 패턴 심화 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java GoF Pattern Singleton
---

출처 : 인프런 백기선님의 강의 "코딩으로 학습하는 GoF의 디자인 패턴" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

GoF 디자인 패턴 중 싱글톤 패턴에 대해 조금 더 심도 있게 알아본다  

## 정의

인스턴스를 오직 한개만 제공하며,  
해당 인스턴스에 대한 글로벌한 접근이 가능한 패턴  

## 구현 방법

1. 기본형(Thread Safe하지 않음)

    ```java
    public class Settings {
        private static Settings instance;

        // 생성자를 private으로 선언해 접근을 막는다
        private Settings() {}

        // 유감스럽게도 Thread Safe하지 않음
        public static Settings getInstance() {
            // 없으면 생성 (Thread 당 최대 한번만 실행 됨)
            if (instance == null) {
                // 위 if 문에 진입하고부터
                // instance에 새 객체를 할당하기 전까지
                // 다른 Thread 또한 if 문에 진입할 수 있음
                instance = new Settings();
            }
            return instance;
        }
    }
    ```

2. sychronized 키워드 사용

    ```java
    // synchronized 키워드를 사용하면 Thread Safe하지만,
    // Lock을 사용하기 때문에 부가적인 성능부하 발생
    public static synchronized Settings getInstance() {
        // 없으면 생성 (단 한번만 실행 됨)
        if (instance == null) {
            instance = new Settings();
        }
        return instance;
    }
    ```

3. 이른 초기화(Eager Initialization)

    ```java
    public class Settings {
        // 먼저 생성해버린다
        // 다만 인스턴스를 생성하는데에 리소스가 많이 들고,
        // 사용하지 않을 수도 있다면 매우 유감
        private static final Settings INSTANCE = new Settings();

        // 생성자를 private으로 선언해 접근을 막는다
        private Settings() {}

        public static Settings getInstance() {
            // 미리 생성해둠
            return INSTANCE;
        }
    }
    ```

4. Double Checked Locking

    ```java
    public class Settings {
        // java 1.5 부터 volatile 키워드를 써줘야  
        // 이 코드 블럭이 동작한다
        private static volatile Settings instance;

        // 생성자를 private으로 선언해 접근을 막는다
        private Settings() {}

        public static Settings getInstance() {
            // 인스턴스가 있으면 바로 통과
            if (instance == null) {
                // Thread가 다수 진입해도 locking
                synchronized (Settings.class) {
                    if (instance == null) {
                        intance = new Settings();
                    }
                }
            }
            return instance;
        }
    }
    ```

5. Static Inner 클래스 사용(권장 1)

    ```java
    // Settings.java

    public class Settings {
        // 생성자를 private으로 선언해 접근을 막는다
        private Settings() {}

        // Multi Thread 환경에서도 안전하고,
        // 아래의 getInstance() 메소드가 호출 될 때
        // 클래스 로딩이 되기 때문에 Lazy Loading이 가능
        private static class SettingsHolder {
            private static final Settings INSTANCE = new Settings();
        }
        
        public static Settings getInstance() {
            return SettingsHolder.INSTANCE;
        }
    }
    ```

    - Static Inner 클래스 파훼법 1 - 리플렉션

        ```java
        // App.java

        public class App {
            public static void main(Stringp[] args) throws Exception {
                Settings settings = Settings.getInstance();

                // 리플렉션을 사용해 private으로 막아두었던
                // 생성자를 강제로 불러 새 객체를 생성
                Constructor<Settings> constructor = Settings.class.getDeclaredConstructor();
                constructor.setAccessible(true);
                Settings otherSettings = constructor.newInstance();

                System.out.println(settings == otherSettings); // false
            }
        }
        ```

    - Static Inner 클래스 파훼법 2 - 직렬화 & 역직렬화

        ```java
        // Settings.java

        // 직렬화를 위해 Serializable 구현
        public class Settings implements Serializable {
        ...
        ```

        ```java
        // App.java

        public class App {
            public static void main(Stringp[] args) throws Exception {
                Settings settings = Settings.getInstance();
                Settings otherSettings = null;

                // 직렬화
                try (ObjectOutput out = new ObjectOutputStream(new FileOutputStream("settings.obj"))) {
                    out.writeObject(settings);
                }
                
                // 역직렬화
                try (ObjectInput in = new ObjectInputStream(new FileInputStream("settings.obj"))) {
                    otherSettings = (Settings) in.readObject();
                }

                System.out.println(settings == otherSettings); // false
            }
        }
        ```

        - 직렬화 & 역직렬화 - 대응방법

            ```java
            // Settings.java

            public class Settings implements Serializable {
                ...
                // Override는 아니지만, 역직렬화시 해당 메소드 호출
                protected Object readResolve() {
                    return getInstance();
                }
                ...
            }
            ```

6. 최고 존엄 Enum(권장 2)

    ```java
    // Settings.java

    @Getter @Setter
    @NoArgsConstructor
    public enum Settings {
        // enum은 리플렉션과 직렬화 & 역직렬화로부터 안전하다
        // IllegalArgumentException : Cannot reflectively create enum objects
        
        INSTANCE;

        private Integer number;

        // 단점으로는 enum은 상속을 받지 못한다
    }
    ```
