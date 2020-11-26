---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 커밋 메시지 # 제목
excerpt             : AngularJS commit message conventions # 썸네일 한줄 요약
last_modified_at    : 2020-11-25 # 2020-11-22 # 작성일 또는 마지막 수정일
categories          : course # java dataStructure algorithm git liquid math course / workout journal
tags                : convention
toc                 : # 목차 사용 default: true
toc_label           : # 목차 제목 default: "목차"
# 알림박스 = {: .notice--info}
---
---

[앵귤러JS 커밋 메시지 컨벤션](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)을 요약해보자  
출처 : [https://gist.github.com/stephenparish/9941e89d80e2bc58a153](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)

---

# 요약

 * 커밋의 내용
 * 중요하지 않은 커밋은 생략
 * 유의미한 정보들로 히스토리를 채운다

---

## 커밋의 내용

커밋에는 세 가지 정보를 담는다.
 * 새 기능 `Features`
 * 버그 픽스 `Bug fix`
 * 주요 변경 사항 `Breaking changes`

---

## 쓸데없는 커밋 무시하기

로직을 변경하지 않은 커밋은 git bisect으로 무시하자

```
git bisect skip $(git rev-list --grep irrelevant <good place> HEAD)
```

---

## 커밋 메시지 포맷

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

---
---

## `<subject>`
첫줄은 `<type>(<scope>): <subject>` 구성으로 전체의 요약이다.

---

`<type>` 커밋 개요 (종류)
 * feat (feature)
 * fix (bug fix)
 * docs (documentation)
 * style (formatting, missing semi colons, …)
 * refactor
 * test (when adding missing tests)
 * chore (maintain) 생산적이지 않은 커밋

---

`<scope>` 수정 대상  
$location, $browser, $compile, $rootScope,  
ngHref, ngClick, ngView 등등..

---

`<subject>` 행동
 * 'changed'`<x>` 과거형
 * 'changes'`<x>` 뒤에s
 * `'change'<o> 아주 좋음`
 * 'Change'`<x>` 첫자 대문자
 * 'change.'`<x>` 마침표

---
---

## `<body>`

구체적인 상세`수정 대상`과 `행동`이 간략하게 `요약`해서 들어간다.  

---
---

## `<footer>`

`주요 변경 사항`(Breaking changes)으로 `무엇을 왜 고쳤는지 상세히` 기재한다.  
justification and migration notes 등등  
어떤 `의미`를 가졌는지나 `바뀐 부분`을 `구체적`으로 기재해도 좋다.  

아래는 예시이다.

```
BREAKING CHANGE: isolate scope bindings definition has changed and
    the inject option for the directive controller injection was removed.
    
    To migrate the code follow the example below:
    
    Before:
    
    scope: {
      myAttr: 'attribute',
      myBind: 'bind',
      myExpression: 'expression',
      myEval: 'evaluate',
      myAccessor: 'accessor'
    }
    
    After:
    
    scope: {
      myAttr: '@',
      myBind: '@',
      myExpression: '&',
      // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
      myAccessor: '=' // in directive's template change myAccessor() to myAccessor
    }
    
    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

---
---

## 이슈 번호

해결된 버그들은 별도의 라인에  
"Closes"로 시작해 기재한다.

```
Closes #234
```

여러 개를 넣어도 된다

```
Closes #123, #245, #992
```

---
---

## 예시

아래는 예시들이다.

```
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```

```
feat(directive): ng:disabled, ng:checked, ng:multiple, ng:readonly, ng:selected

New directives for proper binding these attributes in older browsers (IE).
Added coresponding description, live examples and e2e tests.

Closes #351
```

```
style($location): add couple of missing semi colons
```

```
docs(guide): updated fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

```
feat($compile): simplify isolate scope bindings

Changed the isolate scope binding options to:
  - @attr - attribute binding (including interpolation)
  - =model - by-directional model binding
  - &expr - expression execution binding

This change simplifies the terminology as well as
number of choices available to the developer. It
also supports local name aliasing from the parent.

BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate the code follow the example below:

Before:

scope: {
  myAttr: 'attribute',
  myBind: 'bind',
  myExpression: 'expression',
  myEval: 'evaluate',
  myAccessor: 'accessor'
}

After:

scope: {
  myAttr: '@',
  myBind: '@',
  myExpression: '&',
  // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
  myAccessor: '=' // in directive's template change myAccessor() to myAccessor
}

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

---
