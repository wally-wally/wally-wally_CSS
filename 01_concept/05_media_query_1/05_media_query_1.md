# :art: 05. media query(1)

<br>

## :one: Intro

- 프로그래밍을 하다 보면 조건에 따라 실행되는 로직을 다르게 해야하는 경우가 생긴다. 주로 if 문이나 switch 문과 같은 조건식 구문이 있는데 CSS에서도 CSS3부터 추가된 `media query`를 이용하면 상황에 따라 스타일을 다르게 적용할 수 있다.
- 이번 시간에는 `media query`의 기본적인 사용법과 필자가 프로젝트를 하면서 주로 사용한 속성들 중심으로 살펴보자.

<br>

## :two: Concept

:heavy_check_mark: <b>기본 마크업</b>

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>media_query</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="wrapper">
    <h1>미디어 쿼리 학습</h1>
    <div class="desktop">
      데스크탑 사이즈
    </div>
    <div class="mobile">
      모바일 사이즈
    </div>
  </div>
</body>
</html>
```

`style.css`

```css
h1 {
  color: crimson;
}

.desktop {
  font-size: 24px;
  color: blue;
}

.mobile {
  font-size: 20px;
  color: green;
}
```

<br>

### (1) `@media` 작성법

- 기본 작성법

```css
@media (조건식) {
  /* 해당 조건식에 만족하는 경우 적용할 CSS 속성 작성*/
}
```

- 두 개 이상의 조건식을 모두 만족해야하는 경우
  - `and`로 조건식들을 연결해준다.

```css
@media (조건식1) and (조건식2) {
  /* 조건식1과 조건식2에 모두 만족하는 경우 적용할 CSS 속성 작성*/
}
```

- 두 개 이상의 조건식 중 하나 이상 만족해야하는 경우
  - `or`가 아닌 comma(`,`)로 조건식들을 연결해준다.

```css
@media (조건식1), (조건식2) {
  /* 조건식1 또는 조건식2에 만족하는 경우 적용할 CSS 속성 작성*/
}
```

<br>

### (2) 일정 너비 이하인 경우 <a href="https://github.com/wally-wally/CSS_Study/tree/master/01_concept/05_media_query_1/example/01" target="_blank">(예제 파일)</a>

```css
@media (max-width: 900px) {
  .desktop {
    font-size: 15px;
    color: black;
  }
}
```

- `@media` 기본 사용법을 익혔으니 지금부터는 상황에 따라 어떻게 사용하는지 살펴보자.
- 위와 같이 작성하면 너비가 900px 이하인 경우 class명이 `desktop`인 영역의 텍스트(`데스크탑 사이즈`) 크기가 24px 에서 15px로 감소하게 된다. 그리고 글자색은 검정색으로 바뀐다.

- 너비가 900px 초과인 경우

  ![캡처01](https://user-images.githubusercontent.com/52685250/82012525-31616400-96b3-11ea-8933-5c76a8bf2b1e.JPG)

- 너비가 900px 이하인 경우

  ![캡처02](https://user-images.githubusercontent.com/52685250/82012532-32929100-96b3-11ea-8758-70e000d7705a.JPG)

- 이를 응용하면 일정 너비 이상인 경우 적용하고 싶을 때에는 `min-width` 속성을 사용하면 되고, 일정 높이 이하 또는 이상인 경우 적용하고 싶을 때에는`max-height`, `min-height` 속성을 각각 사용하면 된다.

---

:heavy_check_mark: <b>[예제] 너비가 500px 이하이고 높이가 900px 이하인 경우 제목(`미디어 쿼리 학습`)을 가운데 정렬 하고 `모바일 사이즈` 텍스트의 굵기를 bold로 변경</b>

```css
@media (max-width: 500px) and (max-height: 900px) {
  h1 {
    text-align: center;
  }
  
  .mobile {
    font-weight: bold;
  }
}
```

- 해당 조건에 만족하지 않는 경우

  ![캡처03](https://user-images.githubusercontent.com/52685250/82012972-222ee600-96b4-11ea-85e0-98f5eadb1df2.JPG)

- 두 조건에 모두 만족하는 경우

  ![캡처04](https://user-images.githubusercontent.com/52685250/82012973-22c77c80-96b4-11ea-9157-511dfe8a0a2a.JPG)

<br>

### (3) 가로화면, 세로화면 감지 <a href="https://github.com/wally-wally/CSS_Study/tree/master/01_concept/05_media_query_1/example/02" target="_blank">(예제 파일)</a>

- 모바일 화면에서 디바이스가 가로 모드인지 세로 모드인지 판단 후 CSS 속성을 다르게 적용할 수 있다.

- 참고로 Javascript를 이용해서도 `orientationchange` 이벤트를 이용해 가로 모드와 세로 모드를 감지할 수 있다.

  ```javascript
  window.addEventListener("orientationchange", () => {
    if(window.orientation == -90 || window.orientation == 90) {
      alert('가로 모드입니다.')
    } else {
      alert('세로 모드입니다.')
    }
  });
  ```

- 하지만 `window.orientation` 속성은 Internet Explorer 뿐만 아니라 Chrome, Firefox 에서도 더 이상 지원되지 않는 속성이여서 위 코드를 사용하기엔 다소 어려움이 있다. <a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/orientation" target="_blank">(참고-MDN 공식 문서)</a>

- 물론 다른 Javascript 속성을 이용해서 구현할 수 있지만 `wally-wally_CSS`인 만큼 이번 시간에는 CSS를 이용해서 구현해보도록 하자.

- 기본 마크업

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>media_query</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="wrapper">
    <h1>모바일 화면 방향 감지</h1>
    <div class="horizontal">
      가로 모드
    </div>
    <div class="vertical">
      세로 모드
    </div>
  </div>
</body>
</html>
```

- `@media` 속성 중 `orientation` 속성이 있는데 이는 화면의 방향을 감지하는 속성이다.
  - `landscape` : 가로 방향 (너비 > 높이)
  - `portrait` : 세로 방향 (너비 < 높이)
- 가로 모드 일 때 `가로 모드` 텍스트만 보이게 하고 세로 모드일 때는 `세로 모드` 텍스트만 보이게 해보자.

```css
@media (orientation: landscape) {
  .horizontal {
    display: block;
  }

  .vertical {
    display: none;
  }
}

@media (orientation: portrait) {
  .horizontal {
    display: none;
  }

  .vertical {
    display: block;
  }
}
```

- 안 보이게 하고 싶을 때는 `display: none;` (또는 `visibility: hidden;`) 을 설정하면 되고 보이게 하고 싶을 때는 display 속성을 `none` 이 아닌 다른 속성(여기서는 `display: block;`)으로 설정하면 된다.

- 세로 모드(너비 < 높이)

  ![캡처05](https://user-images.githubusercontent.com/52685250/82014479-a898f700-96b7-11ea-83c3-79c4233cf610.JPG)

- 가로 모드(너비 > 높이)

  ![캡처06](https://user-images.githubusercontent.com/52685250/82014482-a9ca2400-96b7-11ea-9abf-03347ad608cf.JPG)

<br>

## :three: Review

- 이외에도 `aspect-ratio`(화면 비율), `resolution`(해상도) 등 다양한 `@media` 속성들이 있지만 이번 시간에는 주로 사용되는 속성들과 필자가 프로젝트를 진행하면서 가장 많이 사용했던 속성들과 상황들 위주로 설명해보았다.
- 추후 시간이 된다면 기타 다른 속성들도 설명할 계획이다.
- 다음 시간에는 `media query`를 이용해서 반응협 웹을 어떻게 제작하는지 알아보자.