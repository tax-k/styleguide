# 마크업 가이드

### Based on
> [Code Guide by @mdo](http://mdo.github.io/code-guide)  
> [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)  
> [Airbnb CSS / Sass Styleguide](https://github.com/airbnb/css)



## 목차 <a id="contents-table" href="#contents-table">#</a>

1. [기본규칙](#basic)
2. [HTML](#html)
    - [HTML - Syntax](#html-syntax)
    - [HTML - Doctype](#html-doctype)
    - [HTML - 언어(lang) 속성](#html-lang)
    - [HTML - IE 호환](#html-ie-compatible)
    - [HTML - 인코딩 설정](#html-charset)
    - [CSS, JavaScript import](#html-type-attr)
    - [태그 속성 순서](#html-tag-attr-order)
    - [Boolean attr](#html-boolean-attr)
    - [마크업 간소화](#html-simplification)
    - [문서 영역(HTML5 아웃라인)](#html-outline)
    - [실용성 vs 퍼펙트함](#html-pragmatism)
3. [CSS](#css)
    - [CSS Reset](#css-reset)
    - [CSS 기본 룰](#css-syntax)
    - [Property 선언 순서](#css-property-order)
    - [미디어 쿼리 위치](#css-media-query)
    - [주석](#css-comment)
    - [선택자](#css-selector)
    - [선택자 우선순위](#css-priority)
4. [네이밍 규칙](#naming-rule)
5. [접근성 가이드라인](#accessibility)



## 기본규칙 <a id="basic" href="#basic">#</a>
많은 길드원이 작성했더라도 한명이 쓴 것처럼 보이는 코드가 좋습니다. 언제든지 길드원들과 논의하여 업데이트할 수 있습니다.

## HTML <a id="html" href="#html">#</a>
### HTML - Syntax <a id="html-syntax" href="#html-syntax">#</a>

>끝나지 않는 전쟁
* 공백 4칸 `VS` 공백 2칸
* tab(하드 탭) `VS` space(소프트 탭)  
*comming soon*
- - -
* 속성(attr)값에는 항상 <b>큰 따옴표(" ")</b>를 사용합니다.
* HTML이 눈감아줘도 단일 태그에는 <b>슬래시(`/`)</b>를 사용하지 않습니다 (ex: `<img />` or `<br />`)
* HTML이 눈감아줘도 닫는게 선택적이라도 생략하지 마세요 (ex: `<li />` or `<body />`)

**bad** 
```html
<img src='images/modu-logo.png' alt='modu-logo'>
```

**good** 
```html
<li>
    <img src="images/modu-logo.png" alt="modu-logo">
</li>
```  


### HTML - doctype <a id="html-doctype" href="#html-doctype">#</a>
모든 HTML 페이지의 시작에 이 문서 타입을 선언함으로써, 표준 모드를 사용하게 합니다.  

```html
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
       ...
    </body>
</html>
```
### HTML - 언어(lang) 속성 <a id="html-lang" href="#html-lang">#</a>
접근성(accessibility) 까지 챙길수 있는 습관
>Authors are encouraged to specify a `lang` attribute on the root `html` element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.
* 영어: `en`
* 한국어: `ko`

```html
<html lang="ko">
</html>
```

### HTML - IE 호환 <a id="html-ie-compatible" href="#html-ie-compatible">#</a>
인터넷 익스플로러도 항상 챙겨줍시다. **절대 따돌리지 않습니다.**   
우리 익스플로러가 최신 버전의 레이아웃 엔진을 사용하여 문서를 렌더링하도록 지정해주세요
```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

### HTML - 인코딩 설정 <a id="html-charset" href="#html-charset">#</a>
문자열 인코딩은 `utf-8`로 명시적으로 선언합니다.
```html
<head>
    <meta charset="UTF-8">
</head>
```
### CSS, JavaScript import <a id="html-type-attr" href="#html-type-attr">#</a>
html5는 `text/css` 과 `text/javascript`가 기본값이에요.  
CSS와 JavaScript를 불러올 때 `type` 속성을 생략합니다.
```html
<!-- 외부 CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- 내부 CSS (최대한 쓰지 않습니다 )-->
<style>
.modu-text-accent {
    color: #ec185e;
}
</style>

<!-- 자바스크립트 -->
<script src="code-guide.js"></script>
```

### 태그 속성 순서 <a id="html-tag-attr-order" href="#html-tag-attr-order">#</a>
HTML 태그 속성들은 코드의 가독성 향상을 위해 특정 순서로 놓는 것이 좋습니다.
1. **`class`**
2. **`id`**, `name`
3. `data-*`
4. **`src`**, `for`, **`type`**, **`href`**, **`value`**
5. **`title`**, **`alt`**
6. `aria-*`, `role`  

`class`는 콤포넌트의 재사용성을 높여주기 때문에 가장 먼저 오게 합니다.  
`id`는 좀 더 구체적이고 제한적으로 쓰이므로 두 번째로 오게 합니다.

```html
<!-- 귿 example -->
<a class="..." id="..." data-modal="toggle" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

### Boolean attr <a id="html-boolean-attr" href="#html-boolean-attr">#</a>
`checked`, `disabled`, `selected`   
이게 Boolean attr 입니다. 생소할 수도 있습니다.  
```html
<!-- 예전엔 요렇게 써줬습니다. 복잡... -->
<label><input type=checkbox checked=checked name=coffee disabled=disabled> Coffee</label>
```
HTML5는 태그 안에 Boolean attr가 있기만 하면 됩니다.
```html
<!-- 우린 요렇게 써줍니다. -->
<input type="text" disabled>
<input type="checkbox" value="1" checked>
<option value="1" selected>1</option>
```
### 마크업 간소화 <a id="html-simplification" href="#html-simplification">#</a>
HTML 마크업 작성시 가능하면 불필요한 부모 엘리먼트들을 피하는게 좋아요
```html
<!-- 낫 밷 -->
<span class="avatar">
    <img src="..." alt="...">
</span>

<!-- 귿 -->
<img class="avatar" src="..." alt="...">
```

### 문서 영역(HTML5 아웃라인) <a id="html-outline" href="#html-outline">#</a>
섹션 요소와 헤딩 요소를 이용하여 문서 개요를 의미적으로 구성해요.  
섹션 요소(`section`, `article`, `nav`, `aside`)에는 헤딩 요소를 사용합니다.  
헤딩 요소는 `h1` 요소를 한 페이지에 한 번 사용합니다.   
헤딩 요소만 보고도 '아 이게 뭐구나' 할 수 있으면 좋습니다.  
단순 `div` 만으로 하는것은 파악이 어려울 수 있으니까요.
```html
<!-- 밷 HTML -->
<body>
    <h1>모두연</h1>
    <div>
        <h1>랩</h1>
        <div>
            <h1>PRML</h1>
        </div>
    </div>
</body>

<!-- 귿 HTML -->
<body>
    <h1>모두연<h1>
    <article>
        <h2>랩<h2>
        <section>
            <h3>PRML<h3>
        </section>
    </article>
</body>
```

### 실용성 vs 퍼펙트함 <a id="html-pragmatism" href="#html-pragmatism">#</a>
실용성을 잃지 않는 선에서 가능한 한 HTML 표준과 시맨틱함을 챙겨야합니다.
너무 '난 다 지킬꺼야'같은 퍼펙트함은 실용성이 떨어질 수 있습니다.
> HTML 은 <b>관대</b>하니까요

<b>[⬆️ 처음으로](#contents-table)</b>

## CSS <a id="css" href="#css">#</a>
### CSS reset <a id="css-reset" href="#css-reset">#</a>
- 브라우저 별 기본 css 가 다릅니다. 이를 맞추기 위해 처음에 초기화 해주세요.  
[참고](http://meyerweb.com/eric/tools/css/reset/)
```css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
    display: block;
}
body {
    line-height: 1;
}
ol, ul {
    list-style: none;
}
blockquote, q {
    quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content: '';
    content: none;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
```
### CSS 기본 룰 <a id="css-syntax" href="#css-syntax">#</a>
> 들여쓰기는 나중에 다시 논하기로 🤔

- 가독성을 높이기 위해서 여는 중괄호 앞에 하나의 공백 문자를 놓습니다.  
- 닫는 중괄호는 다음줄에 작성합니다.  
- 각각의 선언은 한 줄에 하나만 하고 `:` 뒤에는 공백 문자 하나를 포함시킵니다.  
- 마지막줄은 원래 세미콜론(`;`)이 생략 가능 하지만 에러방지를 위해 작성합시다.

```css
/* 귿 CSS */
.selector {
    property: value;
    property: value;
}
```
- 스타일 선언 사이에 의미가 있을때만 빈 줄 바꿈을 합니다.
```css 
/* 귿 CSS */
.selector {}
.selector .selector-secondary{
    property: value;
    property: value;
}

.selector2 { property: value; }
```

- 스타일 속성이 하나 일때는 한줄로 작성합니다.
- 콤마로 나뉜 속성값(ex: `box-shadow`)은 콤마 뒤에 공백을 추가합니다.
```css
/* 굳 CSS */
.selector { box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff; }
```
- `rgb()`, `rgba()` ... 등 색상값을 표현하는 코드는 콤마뒤에 공백 넣지 않습니다.  
- 속성값들과 색상값들에 소숫점이 필요할 경우 `0.#`을 사용하지 않습니다.
```css
/* 굳 CSS */
.selector { background: rgba(255,255,255,.5); }
```
- 가능하다면 축약형 16진수 값으로 사용하고 소문자로 표현합니다.  
```css
/* 밷 CSS */
.selector { color: #FFFFFF; }
/* 굳 CSS */
.selector { color: #fff; }
```
- 여러 선택자에 스타일 매길 때, 한 줄에 하나씩 각각의 선택자를 놓습니다.
```css
/* 밷 CSS */
.selector, .selector-secondary, .selector[type=text] {
    property: value;
    property: value;
}

/* 굳 CSS */
.selector,
.selector-secondary,
.selector[type="text"] {
    property: value;
}
```
- 속성값에는 홑따옴표(`''`)를 사용합니다.
```css
/* 밷 CSS */
[type=text] { ... }
[type="text"] { ... }
.selector { background: url(ex.png); }
.selector { background: url("ex.png"); }

/* 굳 CSS: 속성 선택자 속성값에 홑따옴표 사용 */
[type='text'] { ... }

/* 굳 CSS: CSS 속성값에 홑따옴표 사용 */
.selector { 
    background: url('ex.png');
    font-family: 'open sans', arial, sans-serif;
}
```
- 축약 가능한 값은 축약합니다.
```css
/* 밷 CSS */
.selector {
    border-top-style: none;
    font-family: palatino, georgia, serif;
    font-size: 100%;
    line-height: 1.6;
    padding-bottom: 2em;
    padding-left: 1em;
    padding-right: 1em;
    padding-top: 0;
}
/* 귿 CSS */
.selector {
    border-top: 0;
    font: 100%/1.6 palatino, georgia, serif;
    padding: 0 1em 2em;
}
/* 하지만 무턱대고 줄이는것이 좋은것은 아닙니다. 
ex)margin 같은 경우 위에만 주려고 하는데 축약형을 쓰기엔 또 재정의를 해야합니다. 
border도 위쪽 왼/오 에만 주고 싶은데 굳이 .... 축약은 놉 
너무 남발하지 말고 적절히 섞어서 씁시다 :)
*/
/* 밷 example */
.element {
    margin: 0 0 10px;
    background: red;
    background: url('image.jpg');
    border-radius: 3px 3px 0 0;
}

/* 귿 example */
.element {
    margin-bottom: 10px;
    background-color: red;
    background-image: url('image.jpg');
    border-top-left-radius: 3px;
    border-top-right-radius: 3px;
}
```


### property 선언 순서 <a id="css-property-order" href="#css-property-order">#</a>
**포지션 > 박스모델 > 타이포그라피 > 기타효과** 순으로 선언합니다.
```css
/* 귿 CSS */
.declaration-order {
  /* 포지션: 위치 먼저 잡고 */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* 박스모델: 사이즈 잡고 */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* 타이포그라피: 글자 잡고 */
  font: normal 13px 'Helvetica Neue', sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* 기타 시각효과: 시각요소 잡고 */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```
### 미디어 쿼리 위치 <a id="css-media-query" href="#css-media-query">#</a>
미디어쿼리는 관련 규칙이 있는 자리에 최대한 가까이 모아 놓습니다.
```css
/* 귿 CSS */
.element { ... }
.element-avatar { ... }
.element-selected { ... }
@media (min-width: 640px) {
    .element { ... }
    .element-avatar { ... }
    .element-selected { ... }
}
```
### 주석 <a id="css-comment" href="#css-comment">#</a>
좋은 주석은 그 자체만으로도 맥락과 목적을 충분히 보여줍니다.  
단순히 엘리먼트라든가 클라스 이름들을 주석 처리하는 것으로만 사용하지 마세요.
```css
/* 밷 example */
/* Modal header */
.modal-header {
  ...
}

/* 귿 example */
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
  ...
}
```
### 선택자 <a id="css-selector" href="#css-selector">#</a>
- 아이디(`#selector`) 나 태그(`div`, `img` ... 등)는 사용하지 않습니다. ❌
- 속성 선택자도 사용하지 않습니다. ❌
- [선택자 우선순위(priority)](#css-priority)를 높이는 조합은 자제해주세요.
- 선택자는 최대 세 개 정도로만 선택할 수 있게끔 해주세요. 3️⃣
- 필요하다면 가장 가까운 부모로부터만 속성을 물려 받을 수 있게끔 해주세요.

```css
/* 밷 example */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* 귿 example */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```
### 선택자 우선순위 <a id="css-priority" href="#css-priority">#</a>
아래는 스타일 시트(CSS file)의 우선순위 표입니다. 같은 선택자 레벨이라면 나중에 포함된 파일의 선택자가 더 힘이 셉니다. 

|우선순위 |속성 종류 |부가 설명 |
|----------------|-------------------------------|-----------------------------|
|**1(낮음)**|User Agent          |브라우저의 기본 스타일 시트            |
|**2**          |사용자 (일반)            |사용자의 스타일 시트           |
|**3**          |제작자 (일반)|제작자가 넣은 스타일 시트|
|**4**          |제작자 (중요)|제작자가 넣은 시트 중 중요 표시한 속성|
|**5(높음)**          |사용자 (중요)|사용자가 넣은 스타일 시트 중 중요 표시한 속성|

- 여기서 우리는 만드는 입장이니 `제작자` 입장을 고려합시다.
- (일반) `vs` (중요) 차이는 `!important` 를 뜻합니다.
- <b>`!important`는 우선순위 레벨을 무너뜨리기 때문에 사용을 금합니다. ❌</b>  


다음은 이제 우리가 만드는 `제작자의 CSS file` 내에서의 우선순위를 설명합니다.
단계에는 a, b, c, d 네가지 레벨이 있습니다.

|단계(순위)	| 설명 |
|--|--|
| **a(1)** | CSS의 선택자가 아닌, 요소에 직접 `style 속성`으로 스타일을 줄때 1점 |
|**b(2)**| 아이디 선택자(`#abc`)의 개수만큼 숫자가 올라갑니다. (`#first`이면 1, `#first #second`면 2)|
|**c(3)**| 클래스 선택자(`.abc`), 속성 선택자, 그리고 가상 클래스(`pseudo-class`) 선택자(`a:link`)의 개수|
|**d(4)** | 태그명(p, h1 ...)으로 준 선택자와 가상 요소(pseudo-element) 선택자의 개수|

막 계산해서 하는거 아니니 걱정하지 맙시다 😀

**간단요약**
1. 요소에 style 속성으로 직접 주는 것(inline css)
2. `#id` 같은 아이디 선택자
3. `.class` 같은 클래스 선택자
4.  `div / h1 / p ... etc` 선택자와 :hover같은 상태 선택자  

이 순서로 우선순위가 결정됩니다 😀

<b>[⬆️ 처음으로](#contents-table)</b>
## 네이밍 룰 <a id="naming-rule" href="#naming-rule">#</a>
 
> There are only <b>two hard problems</b> in Computer Science: <b>cache invalidation</b> and <b>naming things</b> — Phil Karlton

### 🤔 네이밍 룰은 너무나도 어려운거 같습니다. 😱
- 네이밍 룰은 [BEM(Block Element Modifier)](http://getbem.com/naming/)스타일을 따릅니다.
- BEM 은 **Block**, **Element**, **Modifier** 을 이용하는 방법론입니다.
<br>  

**Block**: 단독으로도 의미를 가지고있는 요소입니다. ex) `header`, `container`, `menu` ...  
**Element**: 의미적으로 **Block**과 연결되있는 요소입니다. ex) `header title`, `header logo`...  
**Modifier**: **Block**이나 **Element**의 플래그적 의미를 가지고 있습니다. 상태, 행동, 모양 등을 의미합니다. ex) `highlighted`, `activated` ...  
<br>

### 친절한 설명
**Block**  
1. NAMING   
    - 이름은 **영어 소문자**, **숫자**, <b>대시(`-`)</b>를 이용합니다. ⭕️
    - 영문 <b>카멜케이스(camelCase)</b>는 사용하지 않는걸로 합니다. ❌
2. HTML  
    - DOM 이면 다 **Block**이 될 수 있습니다.
    ```html
    <div class="block">...</div>
    ```
3. CSS  
    - 클래스 선택자(`.selector`)만 사용합니다. ⭕️
    - 태그명(`div`)이나 아이디(`#selector`)는 사용하지 않습니다. ❌
    - 다른 블럭에 의존하는게 없어야 합니다.
    ```css
    .block { color: #042; }
    ```
<br>

**Element**  
1. NAMING   
    - 이름은 **영어 소문자**, **숫자**, <b>대시(`-`)</b>, <b>언더바(`_`)</b>를 이용합니다. ⭕️
    - **Block 이름, 언더바 두개, Element 이름**의 조합(`.block__elem`)을 사용합니다.
2. HTML  
    - **Block**안에 있는 DOM들은 다 **Elements**가 될 수 있습니다.
    ```html
    <div class="block">
	  ...
	  <span class="block__elem"></span>
	</div>
    ```
3. CSS  
    - 클래스 선택자(`.selector`)만 사용합니다. ⭕️
    - 태그명(`div`)이나 아이디(`#selector`)는 사용하지 않습니다. ❌
    - 다른 블럭에 의존하는게 없어야 합니다.
    ```css
    /* 밷 CSS */
    .block .block__elem { color: #042; }
	div.block__elem { color: #042; }

    /* 귿 CSS */
    .block__elem { color: #042; }
    ```
<br>  

**Modifier**  
1. NAMING   
    - 이름은 **영어 소문자**, **숫자**, <b>대시(`-`)</b>, <b>언더바(`_`)</b>를 이용합니다. ⭕️
    - **Block 또는 Element 이름, 대시 두개, Modifier 이름**의 조합(`.block--mod` or `.block__elem--mod` 등)을 사용합니다.
2. HTML  
    - **Modifier**는 **Block**이나 **Elements**의 DOM에 추가되는 클래스 명입니다.
    - 워래 클래스명은 그대로 두고 뒤에 추가하여 상태나 성질을 표현합니다.
    ```html
    <!-- 밷 example -->
    <div class="block--mod">...</div>

    <!-- 귿 example -->
    <div class="block block--mod">...</div>
	<div class="block block--size-big block--shadow-yes">...</div>
    ```
3. CSS  
    - **Modifier**의 선택자를 사용합니다. ⭕️
    ```css
    /* block modifier */
    .block--hidden { }

    /* block modifier > element modifier */
    .block--mod .block__elem { }

    /* element modifier */
    .block__elem--mod { }
    ```
<br>

**BEM Example** 

HTML
```html
<form class="form form--theme-xmas form--simple">
  <input class="form__input" type="text" />
  <input
    class="form__submit form__submit--disabled"
    type="submit" />
</form>
```
CSS
```css
.form { }
.form--theme-xmas { }
.form--simple { }
.form__input { }
.form__submit { }
.form__submit--disabled { }
```

* 짧고 간결하게 작성하되 너무 축약하지 않습니다.  
`.btn`과 같이 쉽게 의미를 유추 할 수 있는 축약은 괜찮지만 `.s`은 의미를 파악하기 어렵습니다.
* 의미, 구조, 목적을 담아 성심성의껏 작명합니다.  

<b>[⬆️ 처음으로](#contents-table)</b>  
## 접근성 가이드 <a id="accessibility" href="#accessibility">#</a>

1. 링크 텍스트가 단독으로 사용될 때도 정확한 의미 파악이 가능하도록 해야합니다
    - `Bad Case`
        - 목적이나 용도를 알기 어려운 링크 텍스트를 제공한 경우
            > 탭이 존재하고 각각의 더보기를 그냥 '더보기'로만 제공할 때  

            **💡각 탭메뉴명 + 더보기 로 `alt` 제공합니다.**
            ```html
            <!-- 귿 case-->
            <img src="/img/read-more.png" alt="공지사항 더보기">
            ```  
            <br>  

        - 한 페이지에 다른 목적지를 가진 동일한 링크 텍스트가 두개 이상 들어간 경우  
            > 페이지에 다른 목적지를 가진 동일한 링크 텍스트인 '더보기' 가 두개 이상 존재할때  

            **💡한 페이지에 다른 목적지를 가진 링크가 동일한 텍스트 링크 텍스트를 갖지 않도록 해야 합니다.**
            ```html
            <!-- 귿 case-->
            <a href="/notice">공지사항 더보기</a>
            <a href="/event">이벤트 더보기</a>
            ```  
            <br> 
    - `Good Case`
        - UI상 정확한 링크 텍스트 제공이 어려워(공간이 협소한 경우 등) 숨김 텍스트 혹은 title로 제공한 경우
             > 공간이 협소하여 숨김 텍스트 혹은 title로 정확한 텍스트를 제공하고 있어 오류가 아닙니댜.  

            **💡숨김 텍스트 혹은 title로 제공하도록 합니다.**
            ```html
            <!-- 귿 case-->
            <a class="link-btn" href="/notice"><span class="link-btn__alt--blind">공지사항</span>더보기</a>
            <a class="link-btn" href="/event" title="이벤트 더보기">더보기</a>
            ``` 