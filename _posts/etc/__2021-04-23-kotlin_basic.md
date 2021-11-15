---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Kotlin App Basic # 제목
excerpt             : 코틀린 앱개발 기초 # 썸네일 한줄 요약
last_modified_at    : 2021-04-23 # 마지막 수정일
categories          : ETC
tags                : Kotlin Android App
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [tutorialEU](https://www.youtube.com/watch?v=4GXflIdrlus)

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

❗️ 학습/교육용이 아닌 복습용이므로 작성자가 이미 알던 내용은 생략되었습니다.


사용 언어 코틀린

---

## Binding

이전 방식들
```kt
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // val myTV = findViewById<TextView>(R.id.myTV)
        // myTV.text = "Hello Students"
    }
}
```

권장되는 새로운 방식
```
# build.gradle

android {
...
    buildFeatures {
        viewBinding true
    }
}
```

```kt
// MainActivity.kt

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding   // added

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)   // added
        setContentView(binding.root)    // changed :: R.layout.activity_main -> binding.root

        binding.myTV.text = "Hello Students"    // using
        
        // set on-click listener
        binding.btnClickMe.setOnClickListener {
            binding.myTV.text = "changed"
            Toast.makeText(this@MainActivity, "You clicked me.", Toast.LENGTH_SHORT).show()
        }
    }
}
```

### 문자열 대입

```kt
var name = "Baek"
var hello = "Hello! $name"

var money = 1000
var paid = 200
var wallet = "I got ${money - paid} now"

fun func(name: String, num: Int): String {
    return "${name}'s ${num}th try"
}

var str = "func #${num}. result : ${func(name, num)}"

```

### 코틀린의 when, 자바의 switch

```kt
var condition = 5
var result = ""

when(condition) {
    1 -> result = "1st" // case
    2 -> result = "2nd"
    // 다양한 범위 지정 방식
    in 3..5 -> result = "${condition}th"
    6, 7, 8 -> result = "${condition}th"
    in 11 downTo 9 -> result = "${condition}th"
    12 -> result = "12번째 - 끝"
    // Default
    else -> result = condition.toString()
}
println(result)
```

자료형의 확인도 가능하다
```kt
var x : Any = 13.37
userInputTypeName = when(x) {
    is Boolean -> "$x is an Boolean"
    is Int -> "$x is an Int"
    is Float -> "$x is an Float"
    is Double -> "$x is an Double"
    is String -> "$x is an String"
    else -> "$x is not primary type"
}
```

### for 반복문의 범위

```kt
for (i in 1..10){}   // 1부터 10까지
for (i in 1 until 10){}
for (i in 1 until 10 step 2){}   // 1부터 2씩 9까지
for (i in 10 downTo 1 step 2){}  // 10부터 -2씩 2까지
```

### nullable

코틀린에서 변수가 null값을 가질수 있게 허용하려면 ? 연산자를 붙이면 된다
```kt
var nullableName : String? = "Baek"

// let
println(nullableName?.toLowerCase())                // this is same
nullableName?.let { println(it.toLowerCase()) }     // with this
if (nullableName != null) {                         // and this
    println(nullableName.toLowerCase())
}

// ?: Elvis operator
var name = nullableName ?: "Default Name"

// !! non-null assertion operator
// throw null pointer exception if the value is null
name = nullableName!!
```


### class
```kt
class Person public constructor(firstName: String = "Seungho", lastName: String = "Baek") {}
// "Seungho" and "Baek" are default values

// creations ex>
var samsung = Person("sung", "sam")
var me = Person()
var theMaster = Person(firstName = "Jong-1")

...

// constructor is ommitable
class Person(firstName: String = "Seungho", lastName: String = "Baek") {

    // Member Variables - Properties
    var age : Int? = 0
        set(value) {
            field = if (value > 0) value else throw IllegalArgumentException("age can not be lowr or same with 0")
        }


    lateinit var job : String   // means will initialize later, not now
    // if try to access this before initialize, raise an exception
    val brand : String = "The Bon"
        get() {
            return field.toLowerCase()
        }


    // Initializer
    init {
        this.firstName = firstName
        this.lastName = lastName
        println("a Person created")
    }

    // Member secondary Constructor
    constructor(firstName: String, lastName: String, age: Int)
        : this(firstName, lastName) {
            this.age = age
        }

    // Member functions - Methods
    fun sayHi() {
        println("Hi, this is $firstName")
    }
}
```

### data class

```kt
data class User(val id: Long, val name: String)

fun main() {
    val user1 = User(1, "Baek")
    val user2 = User(1, "Baek")

    println(user1 == user2) // true
    println("User Details : $user1")
    // User Details : User(id=1, name=Baek)

    val updatedUser = user1.copy(name="Tony")
    println("$updatedUser")
    // User(id=1, name=Tony)

    println(user1.component1())     // 1
    println(user1.component1())     // Baek

    val (id, name) = user1
    println("id=$id, name=$name")   // id=1, name=Baek
}

```

### 상속

```kt
// 코틀린 클래스들은 전부 Any 클래스를 상속 받는다
// 코틀린 클래스는 final이 디폴트 값이기 때문에 상속을 받으려면 부모 클래스에 open을 붙여줘야한다

open class Car(val name: String, val brand: String) {
    open var range: Double = 0.0
    // open for override

    open fun drive(distance: Double) {
        println("Drove for $distance km")
    }
}

class ElectricCar(val name: String, val brand: String, batteryLife: Double) : Car(name, brand) {
    override var range = batteryLife * 6

    override fun drive(distance: Double) {
        range -= distance
        if (range < 0) {
            println("Can not drive anymore, need charge")
        } else {
            println("Drove for $distance km on electricity / $range left")
        }
    }
}
```