# 📚 마크다운(Markdown)

## 🔍 마크다운(Markdown) 이란?

- 웹상에서 글을 쓰는 모든 사람들을 위한 글쓰기 도구(서식, 포맷, 양식)
- 마크다운(Markdown)으로 작성한 문서는 HTML 형식으로 변환시켜 표시
- 쉽게 작성하고 쉽게 읽히도록 간소한 서식



## 마크다운 장/단점

### 👍 마크다운 장점
1. 문법이 쉽다.
2. 관기라 쉽다.
3. 지원 가능한 플랫폼과 프로그램이 다양하다.

### 👎 마크다운 단점
1. 표준이 없어 사용자마다 문법이 상이할 수 있다.
2. 모든 HTML 마크업을 대신하지는 못한다.



## 📝 마크다운 핵심문법(syntax)

### **<u>제목(Header)</u>**

HTML 태그 `<h1>` 부터 `<h6>` 까지 제목을 표현할 수 있다.

**CODE 💻**
```md
# 제목1 h1
## 제목2 h2
### 제목3 h3
#### 제목4 h4
##### 제목5 h5
###### 제목6 h6
```

**VIEW 👓**
# 제목1 h1
## 제목2 h2
### 제목3 h3
#### 제목4 h4
##### 제목5 h5
###### 제목6 h6  

**PLUS ➕**
```md
<!--제목1(h1)과 제목2(h2)는 다음과 같이 표현할 수 있다.-->
제목1
===

제목2
---
```

### **<u>강조(Emphasis)</u>**

HTML 태그 `<em>`, `<strong>`, `<del>` 태그로 변환

**CODE 💻**  
```md
이텔릭체 : *별표* 혹은 _언더바_ 를 사용  
두껍게 : **별표** 혹은 __언더바__ 를 사용  
최소선 : ~~물결표시~~를 사용  
```

**VIEW 👓**  
이텔릭체 : *별표* 혹은 _언더바_ 를 사용  
두껍게 : **별표** 혹은 __언더바__ 를 사용  
최소선 : ~~물결표시~~를 사용

**PLUS ➕**
```md
<u>밑줄</u> : <u></u>를 사용
```

**VIEW 👓**

<u>밑줄</u> : u 를 사용



### **<u>목록(List)</u>**
HTML 태그 `<ol>`, `<ul>` 목록 태그로 변환

**CODE 💻**
```md
1. 순서가 필요한 목록
1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록(서브)
    - 순서가 필요하지 않은 목록(서브)
1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록(서브)
    - 순서가 필요하지 않은 목록(서브)
1. 순서가 필요한 목록
```

**VIEW 👓**  
1. 순서가 필요한 목록
1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록(서브)
    - 순서가 필요하지 않은 목록(서브)
1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록(서브)
    - 순서가 필요하지 않은 목록(서브)
1. 순서가 필요한 목록


**PLUS ➕**
```md
- 순서가 필요하지 않은 목록에 사용 가능한 기호
    - 대쉬
    * 별표
    + 더하기
```

**VIEW 👓**  
- 순서가 필요하지 않은 목록에 사용 가능한 기호
    - 대쉬
    * 별표
    + 더하기



### **<u>링크(Links)</u>**

HTML코드 `<a>`로 변환

**CODE 💻**
```md
기본구조 : [링크타이틀](URL "링크설명")
일반 URL이나 꺾쇠 괄호('<>')안의 URL은 자동으로 링크를 사용

구글 : [Google] (https://google.com "구글링크")  
상대적 참조 : [TIL](../README.md)

구글 URL : https://google.com  
네이버 URL : https://naver.com
```

**VIEW 👓**   
구글 : [Google](https://google.com "구글링크")  
상대적 참조 : [TIL](../README.md)  

구글 URL : https://google.com  
네이버 URL : https://naver.com


**PLUS ➕**  
```md
문서 안에서 참조 링크를 그대로 사용할 수 있다.

[GitHub][1]
[Naver][참조 링크]

<!-- 참조링크 -->
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"

```

**VIEW 👓**  
[GitHub][1]  
[Naver][참조 링크]

<!-- 참조링크 -->
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"



### **<u>이미지(Images)</u>**
HTML 태그 `<img>`로 변환  
링크와 비슷하지만 앞에 '!'가 붙는다

**CODE 💻**  
```md
기본구조 : [대체 텍스트](URL "링크설명")

![Nature](https://image.shutterstock.com/image-photo/bright-spring-view-cameo-island-600w-1048185397.jpg "무료 이미지")

```

**VIEW 👓**  
![Nature](https://image.shutterstock.com/image-photo/bright-spring-view-cameo-island-600w-1048185397.jpg "무료 이미지")


**PLUS ➕**  
```md
마크다운 이미지 코드를 링크 코드로 묶어서 사용 가능
[![Naver](https://t1.daumcdn.net/cfile/tistory/99117C3F5D04CEE519 "네이버 로고")](https://naver.com "image Link")

<!-- 이미지 크기를 작게 하기 위해서는 HTML img태그를 사용해야함 -->
<img src = "https://t1.daumcdn.net/cfile/tistory/99117C3F5D04CEE519" width="200px">
```

**VIEW 👓**  
[![Naver](https://t1.daumcdn.net/cfile/tistory/99117C3F5D04CEE519 "네이버 로고")](https://naver.com "image Link")

[<img src = "https://t1.daumcdn.net/cfile/tistory/99117C3F5D04CEE519" width="200px">](https://naver.com "image Link")



### **<u>코드(Code)</u>**
HTML 태그 `<pre>`, `<code>`로 변환  
숫자 1번 왼쪽의 `(Grave)를 입력

**CODE 💻**  
```md
인라인 코드
`<em>`, `<strong>` 등과 같은 코드를 나타낼때 사용

블록 코드
'''javascript
function sum(a, b) {
    return a+b;
}
'''
위와 같이 여러줄의 코드를 나타낼때 사용
```

**VIEW 👓**  
**인라인 코드**   
`<em>`, `<strong>` 등과 같은 코드를 나타낼때 사용  

**블록 코드**  
```javascript
function sum(a, b) {
    return a+b;
}
```  
위와 같이 여러줄의 코드를 나타낼때 사용



### **<u>표(Table)</u>**
HTML태그 `<table>`로 변환

**CODE 💻**  
```md
- 헤더와 셀을 구분할 때 3개의 이상의 -(hyphen/dash)기호 필요
- 헤더 셀을 구분하면서 :(colons) 기호로 셀 안에 내용 정렬
- |(vertical bar)기호로 셀 구분, 가장 좌측과 우측 기호는 생략가능

|이름|전화번호|비고|
|---|:---:|---|
|아이언맨|010-1234-1234|지각|
|캡틴아메리카|010-1234-1234|
|스파이더맨|010-1234-1234|

이름|전화번호|비고
---|:---:|---
아이언맨|010-1234-1234|지각
캡틴아메리카|010-1234-1234|
스파이더맨|010-1234-1234|
```

**VIEW 👓**  
|이름|전화번호|비고
|---|:---:|---|
|아이언맨|010-1234-1234|지각|
|캡틴아메리카|010-1234-1234||
|스파이더맨|010-1234-1234||  



### **<u>인용문(BlockQuote)</u>**
HTML `<blockquote>` 태그로 변환

**CODE 💻**  
```md
> 남의 말이나 글에서 직접 또는 간접으로 따온 문장


>인용문
>>중첩 인용문
>>>중중첩 인용문
```

**VIEW 👓**  
> 남의 말이나 글에서 직접 또는 간접으로 따온 문장

빈칸으로 인용문 블록 구분(Enter 2번 또는 끝 띄어쓰기 2번으로 개행)

>인용문
>>중첩 인용문
>>>중중첩 인용문1  
>>>중중첩 인용문2  
>>>중중첩 인용문3