---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 파이썬 기초 # 제목
excerpt             : Python Basic # 썸네일 한줄 요약
last_modified_at    : 2021-04-03 # 마지막 수정일
categories          : etc
tags                : Python Basic
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---


## Python naming conventions

파이썬 명명법

약어는 대문자로 Http(x), HTTP(o)

모듈  
lower\_case, 짧게  
가독성을 위해서라면 ‘\_’ 사용 가능  

패키지  
lowercase, 짧게  
‘\_’ 사용 지양  

클래스  
CapsWords(CamelCase)  
인터페이스가 문서화되고, 주로 callable로 사용한다면 함수명명법처럼 명명해도 무관  

타입변수  
CapsWords(CamelCase), 짧게  

예외  
CapsWords(CamelCase)  
에러라면 “Error” 어미 추가  

함수와 변수  
lower\_case  
가독성을 위해서라면 ‘\_’ 사용 가능  
protected 접근제한자 접두사 ‘\_’  
private 접근제한자 접두사 ‘\_\_’  
스페셜 속성인 경우 접두사, 접미사 모두 ‘\_\_’  
l, O, I 사용금지. 대신 L, o, i 사용 권장  

상수  
UPPER\_CASE  
가독성을 위해서라면 ‘\_’ 사용 가능  

---


## 형변환

파이썬은 자동 형변환이 지원되므로 아래와 같이 사용하면 된다

int(값), float(값), str(값), chr(값), bool(값)

---



## eval() 

문자열로 수식을 받아 실행하고 반환값이 있는 경우 반환한다

eval(“max([1,2,3,4])”)의 경우 리스트 내 최대값인 4가 반환됨

그러나 “\_\_import\_\_(‘os’).system(‘ls/’)”을 인자로 넘겨줄 경우

실제로 os를 임포트 받아 시스템에서 ls 명령어를 실행해버린다

편리하면서도 굉장히 위험한 함수이므로 사용에 각별한 유의가 필요하다

---

## 복합대입연산자

자바에서 쓰던 +=, -=, *= 같은 연산자가 파이썬에서도 사용 가능하다

ex) a += b  =>  a = a + b

---


## 표현식, 함수호출 기반 문자열 조합

타입  
%s: 문자열  
%d: 정수형  
%f: 실수형  
등등  

### 표현식 기반
타입을 순차적으로 미리 지정해 의도하지 않은 값을 막을 수 있다  
ex) “%s\_\_%d\_\_” % (문자열 변수, 정수형 변수)  
%s로 지정해두고 실수나 정수형을 넣어도 자동 형변환이 된다  
ex) “%s\_\_%d\_\_” % (정수형 변수, 정수형 변수)  
딕셔너리를 사용하면 순서와 상관없이 지정해서 출력이 가능하다  
ex) ”%(a)s\_\_%(b)d\_\_” % (‘b’: 33, ‘a’: “abc”)  


### 함수호출 기반
.format() 함수를 통해 {}와 변수를 치환한다, 타입 무관  
ex) “{}\_\_{}\_\_”.format(변수1, 변수2) => 변수1\_\_변수2  
{} 안에 인덱스 지정 가능, 특정 인덱스의 변수 반복 사용 가능  
ex) “{1}{0}{1}”.format(변수1, 변수2) => 변수2변수1변수2  
{인덱스:정렬기준, 옵션, 길이, 구분자, 타입}의 방식으로 설정 가능  
ex) "{1:<+6b}{0}".format(1, 13) => "+1101 1”  
< 좌 > 우 ^가운데 정렬  
\+ 부호 추가  
b 2진수, o 8진수, x 소문자16진수, X 대16, e 지수형식  
구분자는 3번째 자리마다 배치됨 (‘,’ or ‘\_’)


---


## 정규식 regex

```
import re
```

### 사용법

```
p = re.compile(정규식) 또는 re.compile(정규식, re.옵션)

p.메소드(목표 대상)
```

re.옵션  
- DOTALL 또는 S: ‘.’이 줄바꿈 문자까지 매치되게 한다  
- IGNORECASE 또는 I: 대소문자 구분안함  
- MULTILINE 또는 M: 줄 바꿈이 포함된 문자열에서 매 줄마다 매칭하게 한다  
- VERBOSE 또는 X: 정규식을 줄 단위로 나눠서 입력이 가능하게 함  

```
# VERBOSE 옵션 예시
charref = re.compile(r'&[#](0[0-7]+|[0-9]+|x[0-9a-fA-F]+);')
# 위의 복잡한 수식을 아래처럼 나눠서 볼 수 있게 함

charref = re.compile(r"""
 &[#]                # Start of a numeric entity reference
 (
     0[0-7]+         # Octal form
   | [0-9]+          # Decimal form
   | x[0-9a-fA-F]+   # Hexadecimal form
 )
 ;                   # Trailing semicolon
""", re.VERBOSE)
```

메소드
- match: 맨 앞부터 확인하며, 대상의 부합여부에 따라 match 객체 / None을 반환
- search: 전체를 검사하며, 대상이 포함하는지에 따라 match 객체 / None을 반환
- findall: 입력 정규식에 해당하는 객체들을 리스트로 반환
- finditer: iterator 오브젝트가 맞는지 확인한다

match 객체의 메소드
- group: 매치된 문자열
- start: 시작 인덱스
- end: 끝 인덱스 + 1
- span: 튜플(시작, 끝 + 1) 반환

---


## range() 사용법

range(시작, 끝 + 1, 증감량)  
시작부터 끝까지 증감량만큼 증감하는 원소들을 가진 range 클래스 객체 반환  

list(값), set(값), tuple(값) 등으로 변환하거나 반복문으로 사용가능

---

## default parameter

```
def func(a = 1, b = 2, c = 3):
…
func(c = 1, a = 3)
```
인자에 기본값과 이름을 지정할 수 있어  
특정 인자에 원하는 값을 명시적으로 입력하거나  
생략하더라도 기본값으로 전달이 된다  

---


## module

```
import 모듈 경로

from 모듈명 import 대상
from 모듈명 import 대상 as A
…
대상.함수() == A.함수()
```

디렉토리 안에 “\_\_init\_\_.py” 파일을 생성하면 패키지로 인식된다

---


## 예외 Exception

try와 except가 최소 구성이며, 나머지는 선택이다

```
try:
	...오류유발 로직...
except 예상오류1:
	...대응...
except 예상오류2 as M:
	print(M)  # M == 에러 메시지
else:  # 오류가 안난 경우
	raise 오류  # 오류를 발생 시킴 (Java의 throw)
finally:
	...결과와 무관하게 마지막에 실행할 로직…
```

### 사용자 정의 예외 생성

```
class 예외이름(Exception):    # Exception을 상속
    def \_\_init\_\_(self):
        super().\_\_init\_\_(에러메시지)
```

---


## 참조수 reference count

객체가 얼마나 많이 참조되고 있는지 그 수를 조회할 수 있다

```
import sys

sys.getrefcount(대상 객체)
```

대상 객체가 참조되고 있는 수 + 1(getrefcount() 함수가 실행되며 참조하게 된다)를 반환한다

만약 참조되고 있는 수가 0이 되면 해당 객체는 가비지 컬렉션이 수행되어 삭제된다

---


## Comprehension

다중 반복문, 조건문을 이용해 원하는 형태로 반환하는 방식

### 작성법

[] 안에 작성하면 List 형태로, {}는 Set의 형태로 반환
```
X = [1, 2, 3, 4, 5]
Y = {1, 2, 3, 4, 5}
Z = (1, 2, 3, 4, 5)

list = [(x, y, z)  # List로 반환
	x for X if x < 5
	y for Y if y % 2 = 0
	z for Z if z > 2
		if z % 2 = 1]
```

{} 내부를 key: value의 반복으로 채우면 Set이 아닌 Dictionary 형태로 반환한다
```
A = [‘a’, ‘b’, ‘c’]
dictionary= {a: 0 for a in A}
# => {'a': 0, 'b': 0, 'c': 0}

# 조건에 따라 값을 변경하기도 편리하다
other = {k: 1 if k == 'c' else v for k, v in dictionary.items()}
# => {'a': 0, 'b': 0, 'c': 1}
```

() 안에 작성하면 Tuple이 아닌 Generator 형태로 반환한다.
```
generator = (a for a in A)
```

---

## Generator

Generator 타입은 iterator에 속하지만 오직 처음부터 순차적으로만 원소들을 조회할 수 있다 
게다가 한번 순환이 끝나면 다시 사용할 수가 없다
```
# generator ex)
(x**2 for x in range(3))
```

내부에 yield로 값을 반환하는 구문이(절대 닿지 않더라도) 있다면 generator 타입이 된다

---

## Iterator의 조건
\_\_iter\_\_(self)와 \_\_next\_\_(self)
- \_\_iter\_\_(self)
  - 인덱스를 순환 시작점으로 초기화하고 자기 자신을 반환
- \_\_next\_\_(self)
  - 인덱스를 순차적으로 순환시키며 끝에 도달했을 때는 예외를 발생시키고,
그렇지 않을 때는 해당 위치의 원소를 반환


```
# iterator ex)

class A:
	def \_\_iter\_\_(self):
		self.idx = 1
return self

def \_\_next\_\_(self):
	x = self.idx
	if x <= 20:
		self.idx += 1
		return x
	else:
		raise StopIteration
```

---


## zip()

다수의 리스트를 인자로 받아 리스트들의 원소들의 튜플로 구성된 리스트를 반환

가능한 만큼만 생성 하므로 전달된 인자 중 가장 짧은 리스트만큼의 길이를 가진다

```
X = range(97, 102)
Y = ['a', 'b', 'c', 'd', 'e',]
Z = range(1, 3)

A = zip(X, Y, Z)
for a in A:
    print(a)

# =>
# (97, 'a', 1)
# (98, 'b', 2)
```

---

## map() 함수

Java Stream의 map과 그 쓰임이 매우 유사하다

대상의 값들을 순회하며 정해진 방식에 따라 모두 변환해준다

사용법은 아래와 같다
```
# result = map(함수, 대상)

X = [1, 2, 3, 4, 5]

def double(x: int):
    return x * 2
    
doubleX = map(double, X)

print(list(doubleX)) # => [2, 4, 6, 8, 10]
```

---

## 익명함수 (람다함수)

람다함수는 이름을 지정하는 대신 그 로직만을 바로 사용한다
```
# 일반 함수
def double(x: int):
    return x * 2

# 람다 함수
lambda x: x*2

# 사용 예시
X = [1, 2, 3, 4, 5]
doubleX = map(lambda x: x*2, X)

print(list(doubleX)) # => [2, 4, 6, 8, 10]
```

---

## Default Dict

```
# import
from collections import defaultdict

# 사용 예시
a = defaultdict(기본값)
```

기본적으로 일반 dict와 그 성질이 같으나,  
없는 키를 호출하면 해당 키를 생성하고 설정했던 기본값을 넣어 반환한다  

일반 dict에서도 .setdefault(키, 값) 함수를 사용하면,  
해당 키가 있을때는 변경 사항이 없지만, 키가 없을 때는 생성하고 값을 넣어 등록한다  

---

## Named Tuple

일반 class 형태로 생성하는것보다 적은 메모리를 사용한다  
튜플과 마찬가지로 immutable 성질을 가져 수정이 불가하다  

```
# 네임드 튜플 이름 = namedtuple(네임드 튜플 이름, 멤버 변수들)

from collections import namedtuple

Samsung = namedtuple('Samsung', ['a', 'b'])
# Samsung = namedtuple('Samsung', ['a, b'])
# Samsung = namedtuple('Samsung', ['a b'])
# Samsung = namedtuple('Samsung', ['a b c d’])
# 모두 가능하다

A = Samsung(5, 6)

print("{}, {}".format(A.a, A.b)) # => 5, 6
```

---

## Ordered Dict
```
from collections import OrderedDict
a = OrderedDict()
```

파이썬 3.6 이후부터는 일반 dict 또한 순서가 보장된다

그러나 일반 dict는 동일한 키, 밸류들만 확인해 일치여부를 반환하는 반면

ordereddict는 키, 밸류들의 순서까지 확인해 일치여부를 반환한다

---

## frozenset

```
a = frozenset([1, 2, 3, 4,])
```

불변성을 가진 set이다

추가, 수정, 삭제 모두 안된다


---

