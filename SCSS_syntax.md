# SCSS
***
> ### History
>  본래 SASS 전처리기는 Ruby 개발자에 설계하고 개발한 Haml 이라는 전처리기의 일부였습니다. 그래서 Ruby의 문법인 중괄호와 세미콜론의 생략과 엄격한 들여쓰기가 제공되는 CSS 전처리기이지만 CSS 문법과는 다소 다르다는 개발자들의 의견이 많아 CSS 문법과 유사하게 만든 CSS가 SCSS입니다.
>  ***
> ### Variables
> CSS와는 다르게 변수 개념이 존재하여 변수에 값을 대입하여 색깔, 폰트와 같은 CSS 값을 설정할 수 있습니다. 다른 언어의 변수의 개념과 동일하여 지역변수와 전역변수가 있으며, 전역변수를 쓰기 위해서는 !global를 사용해야 합니다.
> ```
> $font-stack:    Helvetica, sans-serif;
> $primary-color: #333;
>
> body {
>  font: 100% $font-stack;
>  color: $primary-color;
> }
> ```
> ***
> ### Nesting
> 기존 CSS에서는 특정한 선택자 안의 선택자를 스타일링하기 위해서는 별도로 선언해서 사용해야 했지만 SCSS 문법에서는 곂쳐서 사용하는 것이 가능합니다. 이를 통해 CSS 유지보수를 쉽게 할 수 있습니다. 부모 선택자를 리퍼런스하려면 & 기호를 사용해야 하고 형제 클래스가 특정 클래스 밖에서도 사용될 경우에는 @at-root 지시자를 사용하면 됩니다.
> ```
> nav {
>  ul {
>    margin: 0;
>    padding: 0;
>    list-style: none;
>  }
>
>  li { display: inline-block; }
>
>  a {
>    display: block;
>    padding: 6px 12px;
>    text-decoration: none;
>  }
> }
> ```
> ***
> ### Partials
> 만약 .sass 파일이나 .scss 파일에서 _로 시작하면 css 파일이 따로 컴파일되지 않습니다. 이를 이용해서 CSS를 모듈화하고 유지 관리를 쉽게 만듭니다. 예로 html에서 해당 css 파일을 불러올 일이 없고 import만 되는 경우 이 기능을 사용하면 됩니다.
> ***
> ### Import
> @import 지시자를 통해 특정 .scss 파일을 불러올 수 있습니다.
> ```
> // _reset.scss
>
> html,
> body,
> ul,
> ol {
>   margin: 0;
>   padding: 0;
> }
> ```
> ```
> // base.scss
>
> @import 'reset';
>
> body {
>  font: 100% Helvetica, sans-serif;
>  background-color: #efefef;
> }
> ```
> ***
> ### Inheritance
> SCSS는 객체 지향의 언어처럼 @extend 지시자를 통해 같은 스타일을 그대로 상속받아 쓸 수 있습니다.
> ```
> .box {
>   border: 1px solid gray;
>   padding: 10px;
>   display: inline-block;
> }
>
> .success-box {
>   @extend .box;
>   border: 1px solid green;
> }
> ```
> ***
> ### Mixins
> Mixins은 @extend 지시자와 매우 비슷하지만 인자들을 받을 수 있는 지시자입니다. @Mixin 지시자를 통해 함수처럼 만들고 @include를 통해 값을 반환할 수 있습니다.
> ```
> @mixin border-radius($radius) {
>  -webkit-border-radius: $radius;
>     -moz-border-radius: $radius;
>      -ms-border-radius: $radius;
>          border-radius: $radius;
> }
>
> .box { @include border-radius(10px); }
> ```
> ***
> ### Operators
> SCSS에서 수학 연산자(+, -, *, /, %, ==, !==)를 사용할 수 있습니다. 다만 +, - 기호를 사용할 때에는 단위를 맞춰서 사용해야만 합니다.
> ```
> .container { width: 100%; }
>
>
> article[role="main"] {
>  float: left;
>  width: 600px / 960px * 100%;
> }
>
> aside[role="complementary"] {
>  float: right;
>  width: 300px / 960px * 100%;
> }
> ```
