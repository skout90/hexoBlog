---
title: HTML5 태그 정리
date: 2017-07-14 19:44:25
categories:
    - Frontend
---

#### 문서형 정의

| HTML 5                 | HTML4.01                                 |
| ---------------------- | ---------------------------------------- |
| `<!DOCTYPE html>`        | <!DOCTYPE HTML PUBLIC "-//W3C//DTD//HTML4.01//EN"> |
| `<style></style>`        | `<style type="text/css"></style>`          |
| `<script></script>`      | `<script type="text/javascript"></script>` |
| `<meta charset="UTF-8">` | `<meta http-equiv="Content-Type" content="text/html"; EUC-KR">` |

#### 문서 구성

텍스트를 의미적으로 구분, 시작적 변화 없음. HTML 문서 안에서 텍스트가 어떤 위치에 있는지 나타내기 위한 태그.

![section article에 대한 이미지 검색결과](http://www.cellbiol.com/bioinformatics_web_development/wp-content/uploads/2017/01/html5_tags.png)

| 태그           | 기능                             |
| ------------ | ------------------------------ |
| `<section>`    | 소단락, 제목을 붙여도 좋을 만한 문장의 모음      |
| `<article>`    | 컨텐츠, 뉴스기사/블로그/게시판 컨텐츠          |
| `<header>`     | 헤더가 되는 컨텐츠, 섹션이나 아티클의 제목을 표현   |
| `<footer>`     | 푸터, 저작관 관련 정보, 페이지 링크          |
| `<nav>`        | 웹페이지 내비게이션 콘텐츠, 페이지 목차, 항목 리스트 |
| `<aside>`      | 보충 컨텐츠, 메인 컨텐츠와는 관계가 약한 컨텐츠    |
| `<time>`       | 텍스트가 날짜나 그와 관련된 것이라는 것을 나타냄    |
| `<figure>`     | 도표를 나타내는데 사용                   |
| `<figcaption>` | 도표의 제목, figure 요소 안에서 사용       |

#### 기능 태그

| 태그         | 기능                                       |
| ---------- | ---------------------------------------- |
| `<mark>`     | 하이라이트 표시                                 |
| <meter></meter>`<meter>`    | 지정 값을 막대그래프로 나타냄, min/max, low/high/optimum 속성 사용 |
| <progress></progress>`<progress>` | 프로그레스 바, max 속성으로 최대값 지정                 |
| `<output>`   | 폼안에서 계산 결과를 나타냄                          |
| `<details>`  | 접혀있지만, 조작에 따라 상세 정보를 나타냄. open 속성을 지정하면 열린 상태로 작성 |
| `<summary>`  | details 요소에서 지정한 내용의 모음을 나타냄. 접혀있을 때는 이 부분만 표시 |

- output, details 예제

````html
<form oninput="r.value = v1.valueAsNumber + v2.valueAsNumber">
  <input type="number" name="v1" value=0>
  +<input type="number" name="v1" value=0>
  = <output name="r"></output>
</form>

<details open>
  <summary>
  	옵션
  </summary>
  확인 메일을 보낸다.
</details>
````

#### input type 속성

| 태그       | 기능                                   |
| -------- | ------------------------------------ |
| search   | 검색 키워드                               |
| tel      | 전화번호 입력                              |
| url      | URL 입력                               |
| email    | 메일 주소 입력                             |
| month    | 연월 입력                                |
| week     | 주 입력                                 |
| date     | 날짜 입력                                |
| time     | 시각 입력                                |
| datetime | UTD(협정 세계시) 입력                       |
| number   | 수치 입력                                |
| range    | 지정 범위의 수치 입력, min 속성 최소값, max 속성 최대값 |
| color    | 색 입력                                 |

## Reference

HTML5가 보이는 그림책 - ANK Co., Ltd 저, 이영란 역