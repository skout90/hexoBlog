---
title: CSS3 새로운 스타일 정리
date: 2017-07-16 00:29:35
categories:
  - CSS
---

<div class="myResize">Junho's Hexo Blog</div>

<style>

.myResize { width: 200px; height: 50px; border: solid black 2px; overflow: auto; resize: both; box-shadow: #ff8080 3px 3px 2px; text-shadow: #ff8080 3px 3px 2px;}

</style>
````html
<div class="myResize">Junho's Hexo Blog</div>

<style>
.myResize {
  width: 300px;
  height: 100px;
  border: solid black 2px;
  overflow: auto;
  resize: both;
  box-shadow: #ff8080 3px 3px 2px;
  text-shadow: #ff8080 3px 3px 2p;
}
</style>
````
#### 1. resize : 크기를 변경할 수 있는 박스 만들기

`resize: both;`

- none : 크기 변경 불가
- horizontal, vertical, both : 수평, 높이, 수평과 폭 높이 둘다 변경 가능, 

#### 2. box-shadow : 박스에 그림자 효과 주기

`box-shadow: #ff8080 3px 3px 2px;`

- 가로위치, 세로 위치, 불투명, 확대 반지름
- 그림자의 색
- inset 지정시 그림자를 박스 안쪽에 표시

#### 3. text-shadow : 문자열에 그림자 효과 주기

`text-shadow: #ff8080 3px 3px 2p;`

- 위치와 크기 : 가로, 세로, 불투명, 확대 반지름
- 색 : 그림자색

<hr>

#### word-wrap : 문자 줄바꿈 처리

- normal : 줄을 바꿀 수 없는 경우, 줄 바꿈하지 않고 표시, 공백과 같이 줄 바꿀 수 있는 경 줄 바꿈
- break-word : 단어 중간에서 줄바꿈.

#### writing-mode: vertical-rl: 세로 쓰기 표시

- horizontal-tb
- vertical-lr : 세로 왼쪽 쓰기
- vertical-rl : 세로 오른쪽 쓰기

