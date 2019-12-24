---
title: SCSS 실사용팁 rem 함수 처리, 색상 변수, ellipsis 확장
categories:
  - CSS
date: 2019-10-15 18:43:13
---

css 단위로 `rem`을 사용한다.


  - _variables.scss

    ```scss
    $browser-context: 20; // 브라우저의 기본 폰트
    
    @function rem($pixels, $context: $browser-context) {
      @return #{$pixels/$context}rem;
    }
    
    $primary-color: #FF6D70;
    
    @mixin pad-h ($left, $right) {
      padding-left: $left !important;
      padding-right: $right !important;
    }
    
    %ellipsis {
      word-break: break-all;
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }
    
    // 사용시
    @import "./variables";
    
    .page {
      &__icon-container {
        margin-top: rem(100);
        @include pad-h(rem(40), rem(40));
        color: $primary-color;
        @extend %ellipsis;
      }
    }
    ```

    `@mixin`을 이용한 `@include`의 경우는 정의된 CSS를 각각 선언해주며 `@extend` 공통 CSS를 만들고 추가해주는 차이가 있다.

  - _reset.scss

    ```scss
    html {
      height: auto;
      // 브라우저에서 사용자가 디폴트 폰트 사이즈를 변경할 수 있으므로 %로 설정한다.
      // default 16px, 환산 20px, browswer-context와 맞춰줌
      font-size: 125% !important;
    }
    
    @media screen and (max-width: 700px) {
      html {
        font-size: 81.3% !important; // 환산 13px;
      }
      body {
        line-height: 1.34;
      }
    }
    
    @media screen and (max-width: 467px) {
      html {
        font-size: 62.5% !important; // 환산 10px;
      }
      body {
        line-height: 1.34;
      }
    }
    ```


## Refenrece

 [css에서의 em과 %] : https://aboooks.tistory.com/142
