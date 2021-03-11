---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Spring 5 WebClient # 제목
excerpt             : Spring 5 WebClient 요약 # 썸네일 한줄 요약
last_modified_at    : 2021-03-11 # 2020-11-22 # 작성일 또는 마지막 수정일
categories          : etc # java dataStructure algorithm git math course etc/ workout journal
tags                : Etc Spring WebClient
toc                 : # 목차 사용 default: true
toc_label           : # 목차 제목 default: "목차"
# {: .notice--info}
---

---

## 출처 [baeldung](https://www.baeldung.com/spring-5-webclient)

너무 간만이지만 기록하고 싶은게 생겨서 쓰게 됐다  

🚫 아래의 내용은 사실과 다를 수 있다
---


AsyncRestTemplate이 deprecated 됐고, RestTemplate도 곧 된다길래 알아봤더니  
WebClient 사용을 권장하고 있어서 알아봤다



## 의존성 추가
build.gradle
```
compile 'org.springframework.boot:spring-boot-starter-webflux'
```

# 구성
1. `인스턴스 생성`
2. `요청 설정`
3. `응답 처리`

---

## 1. `WebClient 인스턴스 생성`

3가지 방법이 있다  

1. 기본 설정 이용
  ```
  WebClient client = WebClient.create();
  ```
2. Base URI만 지정
  ```
  WebClient client = WebClient.create("http://localhost:8080");
  ```
3. 상세 설정 지정
  ```
  WebClient client = WebClient.builder()
  .baseUrl("http://localhost:8080")
  .defaultCookie("cookieKey", "cookieValue")
  .defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE) 
  .defaultUriVariables(Collections.singletonMap("url", "http://localhost:8080"))
  .build();
  ```

### Timeout 지정  
기본 HTTP 타임아웃은 30초로 너무 길다  
바꿔본다

- ChannelOption.CONNECT_TIMEOUT_MILLIS 옵션으로 바꾼다
- responseTimeout으로 응답 타임아웃 지정 가능
- 읽기/쓰기(ReadTimeoutHandler/WriteTimeoutHandler) 각각 설정 가능

```
HttpClient httpClient = HttpClient.create()
  .option(ChannelOption.CONNECT_TIMEOUT_MILLIS, 5000)
  .responseTimeout(Duration.ofMillis(5000))
  .doOnConnected(conn -> 
    conn.addHandlerLast(new ReadTimeoutHandler(5000, TimeUnit.MILLISECONDS))
      .addHandlerLast(new WriteTimeoutHandler(5000, TimeUnit.MILLISECONDS)));

WebClient client = WebClient.builder()
  .clientConnector(new ReactorClientHttpConnector(httpClient))
  .build();
```
⚠️ `주의` : `클라이언트 요청`에서 설정하는 timeout은  
Mono/Flux 게시자용 signal timeout입니다  
`HTTP 연결, 읽기/쓰기나 응답 timeout이 아닙니다`

---

## 2. `요청 준비`

### 메소드 설정
post, get, delete...
```
UriSpec<RequestBodySpec> uriSpec = client.post();
```

### URL 지정

스트링으로 넘겨줘도 되고
```
RequestBodySpec bodySpec = uriSpec.uri("/resource");
Using a UriBuilder Function:
```

빌더 패턴을 써도 된다
```
RequestBodySpec bodySpec = uriSpec.uri(
  uriBuilder -> uriBuilder.pathSegment("/resource").build());
```

### 바디 정의

여러가지 방법이 있는데  
`bodyValue 메소드로 간단`하게 줘도 되고
```
RequestHeadersSpec<?> headersSpec = bodySpec.bodyValue("data");
```

`어떤 타입`을 보내는건지 알려줄수도 있고 
```
RequestHeadersSpec<?> headersSpec = bodySpec.body(
  Mono.just(new Foo("name")), Foo.class);
```

아래의 BodyInserters 기능들을 이용할 수도 있다

1. fromValue()
```
RequestHeadersSpec<?> headersSpec = bodySpec.body(
  BodyInserters.fromValue("data"));
```

2. fromPublisher()
```
RequestHeadersSpec headersSpec = bodySpec.body(
  BodyInserters.fromPublisher(Mono.just("data")),
  String.class);
```

1. `fromMultipartData()`
```
LinkedMultiValueMap map = new LinkedMultiValueMap();
map.add("key1", "value1");
map.add("key2", "value2");
RequestHeadersSpec<?> headersSpec = bodySpec.body(
  BodyInserters.fromMultipartData(map));
```

### 헤더 정의

바디 정의 이후에 헤더, 쿠키, 허용타입 등을 지정할 수 있는데  
이것들은 WebClient 인스턴스 생성 할 때 설정했던(또는 기본설정)것들에 추가됩니다

“If-None-Match”, “If-Modified-Since”, “Accept”, “Accept-Charset”와 같이 자주 쓰이는 헤더들은 미리 넣어뒀다
사용예시는 아래와 같다

```
ResponseSpec responseSpec = headersSpec.header(
    HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
  .accept(MediaType.APPLICATION_JSON, MediaType.APPLICATION_XML)
  .acceptCharset(StandardCharsets.UTF_8)
  .ifNoneMatch("*")
  .ifModifiedSince(ZonedDateTime.now())
  .retrieve();
```

---

## 3. `응답 처리`

retrieve() 메소드로 아주 짧게 가능하다
```
Mono<String> response = headersSpec.retrieve()
  .bodyToMono(String.class);
```

그러나 응답 `결과에 따라 예외와 같은 다양한 처리`를 원한다면  
`상태, 헤더에 접근 가능`한 `exchangeToMono()/exchangeToFlux()`를 추천한다
```
Mono<String> response = headersSpec.exchangeToMono(response -> {
  if (response.statusCode()
    .equals(HttpStatus.OK)) {
      return response.bodyToMono(String.class);
  } else if (response.statusCode()
    .is4xxClientError()) {
      return Mono.just("Error response");
  } else {
      return response.createException()
        .flatMap(Mono::error);
  }
});
```


---

WebTestClient에 대해서는 다음에 알아보자