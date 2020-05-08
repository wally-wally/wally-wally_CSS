# :art: 02. `display: grid` - 레이아웃 구성

<br>

## :one: Intro

- 지금까지 나온 CSS 기술들 중 필자가 생각하기에 가장 혁신적이고 신박한 기술이 바로 display 속성의 `grid`가 아닐까 싶다.
- `display: grid;`로 display 속성을 선언한 후 단 몇 줄의 스타일 속성 선언만으로 기본적인 레이아웃을 구성할 수 있다.
- 도대체 얼마나 좋은지 이번 시간에 `grid` 속성의 기본에 대해 알아보자.

<br>

## :two: Concept

### (1) `flex` vs `grid`

- 이전 `01. display: flex` 편을 보고 왔다면 궁금증이 생길 수 있다. `flex`와 `grid`의 차이점은 무엇일가?
- 아주 간단하게 이야기하면 `flex`는 1차원적으로 요소들을 배치하는 속성이고 `grid`는 1차원을 넘어 2차원적으로 요소들을 배치할 수 있는 속성이다.
  - 즉, 한 줄 내에서 여러 개의 아이템을 배치하는 속성을 정의하기 위해서는 `flex`를 한 줄을 넘어 페이지 전체의 전반적인 윤곽을 잡고 아이템들을 여러 줄로 배치하는 속성을 정의할 때 `grid`를 사용한다고 생각하면 쉬울 것 같다.

<br>

### (2) `display: grid;`

- grid 속성을 이용하기 위해서는 해당 영역의 CSS 속성으로 display를 `grid`로 선언하면 된다.

```css
.wrapper {
  display: grid;
}
```

- 사실 grid 속성은 flex보다 더 최신 기술이고 아직도 개발중인 기술이며 grid와 관련된 CSS 속성들이 너무 많아 이 모든 것들을 외워서 사용한다는 것은 사실상 어렵다.
- 그래서 필자가 프로젝트를 하면서 또는 학습을 하면서 배우고 익혔던 내용들 중 나름 중요하다고 생각하는 부분을 골라서 정리를 해보려고 한다.

<br>

### (3) `grid-template-columns` <a href="https://github.com/wally-wally/CSS_Study/tree/master/01_concept/02_display_grid_1/example/01" target="_blank">(예제 파일)</a>

- `grid-template-columns`는 한 줄에 여러 영역들을 배치할 대 각 영역의 너비의 비율을 설정할 수 있는 속성이며 사용법은 아래와 같다.

```css
.wrapper { /* 한 줄에 세 개의 영역을 배치한다고 가정 */
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

- 위의 코드같은 경우는 한 줄에 세 개의 영역을 배치하는데 이 때 너비의 비율을 1 : 2 : 1로 하겠다는 의미이다. 이와 같이 간단한 정수 비율로 설정하기 위해 `fr` 이라는 단위를 사용한다.
- 예제를 통해서 확인하면 아래와 같다.

```html
<div class="wrapper">
  <div class="notice">
    소식1. aaa<br>
    소식2. bbb<br>
    소식3. ccc<br>
  </div>
  <div class="contents">
    환영합니다<br>
    이 곳은 본문 영역입니다.
  </div>
  <div class="ranking">
    1등. AAA<br>
    2등. BBB<br>
    3등. CCC 
  </div>
</div>
```

```css
.wrapper {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}

/* 영역의 너비 비율을 쉽게 보기 위해 각 영역에 배경색을 설정했다. */
.notice {
  background-color: antiquewhite;
}

.contents {
  background-color: coral;
}

.ranking {
  background-color: cornflowerblue;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80940875-e7a78c80-8e1b-11ea-8891-9da9977eec12.JPG" width="800">

- 위 사진과 같이 너비의 비율이 1 : 2 : 1임을 알 수 있다.

- 그렇다고 해서 무조건 `fr` 단위로 비율만 설정할 수 있는 것이 아니고 `px` 단위를 이용해서 고정 너비를 설정할 수도 있다.
- 그리고 한 줄에 여러 개의 영역을 같은 너비의 비율로 배치한다고 하면 아래와 같이 코드를 작성할 수 있다.

```css
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}
```

- 무려 5개를 배치하게 되면 `1fr` 5번씩이나 적어야 한다. 그래서 이러한 번거로움을 줄이기 위해 `repeat()` 함수를 이용해서 `repeat(5, 1fr)`와 같이 작성할 수 있다.
  - `5`는 반복 횟수, `1fr`은 반복할 값(`1fr`와 같은 상대 단위 대신에 `px`도 사용 가능)

---

:heavy_check_mark: <b>실제 프로젝트에서 적용한 사례</b>

- 최근에 도서 추천 서비스 프로젝트를 진행하면서 메인 페이지의 컨텐츠 영역에 grid 속성을 이용해서 레이아웃을 구성했던 적이 있다.

<img src="https://user-images.githubusercontent.com/52685250/80941237-e460d080-8e1c-11ea-8298-a2a99b306e46.JPG" width="800">

- 좌측의 이 주의 작가(AUTHOR OF THE WEEK)와 도서랭킹(BOOKSRANKING)이 하나의 영역이고 우측의 도서 리스트(BOOK LIST)가 또 하나의 영역이다.
- 이 두 영역을 `display: grid;`를 이용해서 1행 2열 레이아웃을 구성했다.

```vue
<template>
  <div class="main-wrapper">
    <ImageSlider />
    <div class="my-6 main-contents">
      <div class="main-sidebar">
        <WeeklyAuthor />
        <BooksRanking />
      </div>
      <div class="main-book-section">
        <BooksHeader />
        <BooksList />
      </div>
    </div>
  </div>
</template>

<script>
// 중략
</script>

<style scoped>
.main-wrapper {
  width: 90%;
  margin: 0 auto;
  box-sizing: border-box;
}

.main-contents {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 4fr;
  gap: 0.75em;
}

.main-contents .main-sidebar {
  min-width: 250px;
}

@media (max-width: 800px) {
  .main-contents {
    display: block;
  }
}
</style>
```

- vue.js를 이용해서 구성한 코드인데 `style` 태그에서 `.main-contents` 부분을 살펴보자.
- `grid-template-columns: 1fr 4fr;` : 작가 및 도서랭킹 부분(`.main-sidebar`)과 도서리스트 부분(`main-book-section`)의 너비 비율을 1 : 4로 구성하여 레이아웃을 구성했다.
  - 이 때 안정적인 레이아웃을 위해 각 영역 사이에 `gap` 을 설정(`gap: 0.75em;`)하여 여백을 두었다.
- 그리고 화면의 너비를 줄였을 때 비율에 맞게 줄어들기 때문에 왼쪽의 영역이 한 없이 계속 작아지게 되는데 이를 방지 하기 위해 좌측 영역에 `min-width` 값을 부여하여 좌측 영역의 너비가 `250px` 이하로 떨어지지 않도록 추가로 설정했다.

---

<br>

### (4) `minmax()` 함수

- `minmax()` 함수는 최솟값과 최댓값을 지정할 수 있는 함수이다.

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(4, minmax(50px, auto));
}
```

- 위 코드에서 `minmax()` 함수가 쓰였는데 한 줄에 네 개의 영역으로 나누되 한 영역의 최소 너비는 50px이고 최댓값은 따로 지정하지 않고 자동으로 늘어나게 하라는 의미이다.
- 참고로 위에서 <b>실제 프로젝트에서 적용한 사례</b>에서 `min-width`를 이용해서 최소 너비를 설정했는데 `minmax()` 함수를 사용하면 더 간단하게 코드를 작성할 수 있다.

<br>

### (5) auto-fill, auto-fit <a href="https://github.com/wally-wally/CSS_Study/tree/master/01_concept/02_display_grid_1/example/02" target="_blank">(예제 파일)</a>

- `auto-fill`과 `auto-fit`은 요소를 배치하다가 남는 공간이 생길 때 어떻게 처리할 지 설정하는 속성이다.
- 우선 `auto-fill`은 남는 공간이 생기면 남은 공간을 채우지 않고 그대로 내버려두는 속성이다.

```html
<div class="wrapper">
  <img src="./images/orange.png" alt="orange1">
  <img src="./images/orange.png" alt="orange2">
  <img src="./images/orange.png" alt="orange3">
</div>
```

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(25%, auto));
  background-color: antiquewhite;
  width: 800px;
}

img {
  width: 200px;
}
```

- 이미지를 담는 가장 바깥 영역(`.wrapper`)의 너비를 800px로 고정시키고 사진의 너비를 200px로 고정시켰다.

- `grid-template-columns: repeat(auto-fill, 25%);` : 하나의 요소의 너비를 한 줄의 전체 너비의 25%만큼 차지하도록 배치하고 `auto-fill`로 설정했기 때문에 `minmax()` 함수에서 최댓값을 `auto`로 설정했다하더라도 뒤에 남는 공간이 생겨도 채우지 않고 빈 상태 그대로 내버려둔다.

<img src="https://user-images.githubusercontent.com/52685250/80942520-f85a0180-8e1f-11ea-9a15-bf401866f34d.JPG" width="800">

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(25%, auto));
  background-color: antiquewhite;
  width: 800px;
}

img {
  width: 200px;
}
```

- 이와 반대로 `auto-fit`은 뒤에 남는 공간이 생기면 남는 공간을 채워서 균일하게 배치되도록 하는 속성이다.

<img src="https://user-images.githubusercontent.com/52685250/80942522-f98b2e80-8e1f-11ea-886d-1a05e68af86d.JPG" width="800">

<br>

## :three: Review

- `display: grid;` 속성을 처음 접하면 생소한 개념들이 많아서 다소 헷갈릴수는 있지만 몇 번 사용하다보면 레이아웃을 구성하는데 매우 간편하다는 것을 느낄 수 있다.
- 이번 시간에는 `grid` 속성을 이용해서 기본적인 레이아웃 구성하는 방법을 알아보았고 다음 `grid` 시간에는 실제로 필자가 프로젝트에서  `grid`를 이용해서 간단한 반응형 웹을 제작한 사례를 소개하고자 한다.