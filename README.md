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
    - [Boolean attr](#html-boolean-attr)
    - [마크업 간소화](#html-simplification)
    - [문서 영역(HTML5 아웃라인)](#html-outline)
    - [실용성 vs 퍼펙트함](#html-pragmatism)
3. [CSS](#css)
    - [CSS]


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


<br>
<br>

## CSS <a id="css" href="#css">#</a>