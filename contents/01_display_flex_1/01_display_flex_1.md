# :art: 01. `display: flex` (1)

<br>

## :one: Intro

- 차세대 CSS 레이아웃으로 불리는 `display: flex;` 속성이 있다.
- 예전의 CSS 방식으로 레이아웃을 구성하려면 `position`, `float` 등을 이용해서 구성해야 했다.
- 하지만 세월이 지날 수록 서비스 이용자들의 디자인 요구 사항과 디자인 수준이 향상됨에 따라 예전의 CSS 기술만으로 구현하기가 까다로워졌다.
- 그래서 W3C에서 최신 CSS 기술 표준을 정의한 CSS3에서 다채롭게 레이아웃을 구성하고 디자인을 할 수 있도록 신기술을 개발했는데 그 중에서 오늘은 display 속성 중 `flex` 에 대해 간단하게 알아보자.

<br>

## :two: Concept

### (1) flex

- `flex` CSS 속성은 한 영역 내에서 요소들을 배치하여 유연하게 차지하고 있는 공간에 맞춰서 레이아웃을 구성하기 위해 사용되는 속성이다.
  - 즉, 자식 요소를 포함하고 있는 부모 요소의 공간에 맞추기 위해 자식 요소들의 크기를 키우거나 줄이는 방법을 설정하는 속성이다.

- 이와 같은 `flex` 속성을 사용하기 위해 해당 부모 요소에 display 속성을 `flex`로 설정해야 한다.

```css
.parent {
  display: flex;
}
```

<br>

### (2) `display: flex;` (예제 파일)

- 기본적으로 `div` 태그와 같은 것들은 `display` 속성이 `block` 이다. 그래서 한 줄에 하나씩만 요소가 배치되는데 example 에서 구현된 예제를 보면서 자세히 살펴보도록 하자.
- 먼저 CSS 속성을 아무것도 설정하지 않고 단순히 사진과 텍스트를 출력했을 때 화면은 아래와 같다.

<img src="https://user-images.githubusercontent.com/52685250/80933239-dfd8ef80-8dfd-11ea-815e-89ebda5bd191.JPG" width="500">

- 사진과 텍스트 모두 한 줄에 하나씩 배치됨을 확인할 수 있다.
- 이 상태에서 `display: flex;` 속성을 이용해 한 줄에 여러 개의 요소가 배치되도록 레이아웃을 구성해보자.
- 우선 각 과일마다 사진과 텍스트를 class명이 `fruit-item`인 `div`태그로 묶어서 총 네 개의 `div`태그를 markup 했다.

```html
<div class="fruits">
  <div class="fruit-item">
    <img src="./images/apple.png" alt="apple">
    <p>Apple</p>
  </div>
  <div class="fruit-item">
    <img src="./images/orange.png" alt="orange">
    <p>Orange</p>
  </div>
  <div class="fruit-item">
    <img src="./images/grape.png" alt="grape">
    <p>Grape</p>
  </div>
  <div class="fruit-item">
    <img src="./images/tomato.png" alt="tomato">
    <p>Tomato</p>
  </div>
</div>
```

- 네 개의 과일을 감싸고 있는 부모 요소인 class명이 fruits인 div 태그에 `display: flex;` 속성을 부여해보자.

```css
.fruits {
  display: flex;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80933493-ed42a980-8dfe-11ea-8a61-46b17c076d05.JPG" width="700">

- 그러면 위 사진과 같이 한 줄에 여러 개의 과일들이 배치됨을 확인할 수 있다.
- 기본적으로 `display: flex;` 속성은 특별한 추가 CSS 속성을 지정하지 않는 이상 자식 요소들을 모두 가로로  한 줄에 배치하게 해준다.

<br>

### (3) `flex-direction` (예제 파일)

- 레이아웃을 구성하다보면 가로 배치가 아닌 세로 배치를 해야하는 경우가 있다.
- `display: flex;`를 사용할 때 배치의 방향을 바꿀 수 있는 속성인 `flex-direction`이 있다.
- `flex-direction`의 기본값은 `row`로서 가로로 배치하게 해주는데 이 값을 `column`으로 바꾸면 세로로 배치할 수 있다.

```css
.fruits {
  display: flex;
  flex-direction: column;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80933622-7bb72b00-8dff-11ea-8f78-f79dcc7b9ef9.JPG" width="300">

<br>

### (4) `justify-content` (예제 파일)

- 다시 가로로 배치하는 상황으로 돌아오자.(`flex-direciton: column;` 속성 제거)
- 기본적으로 `display: flex;` 속성을 지정하면 각 요소 간 공백 없이 한 줄에 여러 개의 요소들이 배치하게 된다.
- 하지만 모든 요소들이 붙어 있으면 안정적인 레이아웃을 가져다주지 못한다. 그래서 좀 더 안정적인 레이아웃을 구성하는데 도움을 주기 위해 `flex`와 관련된 배치 속성들이 몇 가지 존재한다.
- 먼저 `justify-content`는 메인축 방향으로 아이템들을 정렬하는 속성이다.
- 현재 가로로 배치하고 있기 때문에 메인축 방향을 가로 방향임을 우선 잊지 말자!

- `justify-content`의 기본값은 `flex-start`로 시작점을 기준으로 차례대로 배치된다.
  - 현재는 가로로 배치되기 때문에 시작점은 왼쪽이 되고 `flex-directon`이 `column`인 경우 메인축 방향 즉, 배치되는 방향이 세로 이기 때문에 `flex-start`는 맨 위가 된다.
- `justify-content`에서 설정할 수 있는 다양한 값 들 중 주로 사용되는 것들만 골라서 살펴보자.

| 값            | 의미                                                         |
| ------------- | ------------------------------------------------------------ |
| flex-end      | 요소들의 배치 시작점을 끝점으로 변경해준다.                  |
| center        | 아이템들을 가운데로 정렬한다.                                |
| space-between | 아이템들의 부모 요소의 전체 너비 또는 전체 높이에 꽉 차게 자식 요소들이 배치되고 이 때 아이템들의 사이에 균일한 간격을 만들어준다. |

- 글로 읽는 것 보다 직접 CSS 속성들을 사용하면서 눈으로 익히는 것이 중요하다!

```css
.fruits {
  display: flex;
  justify-content: flex-end;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80933972-e452d780-8e00-11ea-881e-9f6b3f5736e6.JPG" width="800">

```css
.fruits {
  display: flex;
  justify-content: justify-content;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80933975-e4eb6e00-8e00-11ea-8ac4-5f0ba48c8cf9.JPG" width="800">

```css
.fruits {
  display: flex;
  justify-content: space-between;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80933976-e5840480-8e00-11ea-872b-3f0db3c257ad.JPG" width="800">

<br>

### (5) `align-items` (예제 파일)

- `align-items`는 `justify-content`와 반대로 메인축에 수직인 방향을 기준으로 요소들을 배치하는 속성이다.

- `align-items`의 기본값은 `stretch`로 아이템들을 수직축 방향으로 끝까지 쭉 늘어난다.(각 자식 요소마다 배경색을 설정하면 수직축 방향으로 끝까지 배경색이 칠해진다.)

- `align-items`에서 설정할 수 있는 다양한 값 들 중 주로 사용되는 것들만 골라서 살펴보자.

| 값         | 의미                                                         |
| ---------- | ------------------------------------------------------------ |
| flex-start | 아이템들을 시작점으로 정렬한다. 즉 `display: flex;`의 배치 방향이 가로(row)인 경우 시작점이 `위`로 세로(column)인 경우 시작점은 `아래`가 된다. |
| flex-end   | `flex-start`와 반대로 아이템들을 끝점을 기준으로 정렬한다.   |
| center     | 아이템들을 가운데로 정렬한다.                                |

- 글로 읽는 것 보다 직접 CSS 속성들을 사용하면서 눈으로 익히는 것이 중요하다!(아래 예시는 `justify-content: center;`로 설정된 상태에서 `align-items` 값만 바꾸면서 확인)
  - 전체 영역을 감싸는 태그 : class명이 `wrapper`인 `div` 태그의 배경색을 회색, 과일들의 내용들을 감싸는 태그 : class명이 `fruits`인 `div` 태그의 배경색을 흰색으로 설정함
  - 흰색 영역 내에서 과일들이 어떻게 배치되는지 살펴보자.

```css
.wrapper {
  height: 1000px;
  background-color: gray;
}

.fruits {
  background-color: white;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: flex-start;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80937740-5e8b5800-8e11-11ea-98a4-324e69552c9f.JPG" width="700">

```css
.wrapper {
  height: 1000px;
  background-color: gray;
}

.fruits {
  background-color: white;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80937742-5fbc8500-8e11-11ea-86aa-ff1836af2b68.JPG" width="700">

```css
.wrapper {
  height: 1000px;
  background-color: gray;
}

.fruits {
  background-color: white;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}
```

<img src="https://user-images.githubusercontent.com/52685250/80937743-60551b80-8e11-11ea-86fc-302412b8431b.JPG" width="700">

<br>

## :three: Review (예제 파일)

- 이번 시간에는 display 속성이 `flex`일 때 주로 사용되는 CSS 속성들 중 주로 요소들의 배치와 관련된 것들을 알아보았다.
- `position` 속성을 이용해서 화면의 정가운데에 요소를 배치하는 방법으로 아래와 같은 방법이 예전부터 내려왔다.

```css
.wrapper {
  /* 아래 네 줄은 화면 정가운데에 요소를 배치하는 기본 공식! */
  position: absolute;
  left: 50%;
  right: 50%;
  transform: translate(-50%, -50%);
  
  /* 위 네 줄을 작성했음에도 불구하고
     원하는대로 디자인이 잘 안 나오는 경우
     상황에 따라서 아래 두 줄을 차례대로 하나씩 추가하면서 CSS 속성을 조절하자. */
  width: 100%;
  text-align: center;
}
```

- 이 방법은 현재 현업에서도 많이 사용되는 방법이다. 하지만 화면의 정가운데에 배치하는데 많은 CSS 속성을 지정해야하기 때문에 다소 어려울 수 있다.
- 그래서 (나름?) 최신 CSS 기술인 `flex` 속성을 이용해서 세 줄로 화면의 정가운데에 배치할 수 있다.

```css
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

- `position` 속성을 이용했을 때보다 훨씬 더 간결하고 `center`라는 키워드를 사용했기 때문에 직관적으로 파악하기가 쉽다.
- 하지만 이러한 방법이 모든 환경에서 적용되는 것은 아니다.

<img src="https://user-images.githubusercontent.com/52685250/80938080-b37b9e00-8e12-11ea-888f-0d88ba1a2748.JPG" width="700">

- 위 사진은 caniuse 라는 사이트로 해당 CSS 속성이 여러 브라우저 환경에서 지원이 되는지 안 되는지 알려주는 사이트이다. <a href="https://caniuse.com/#search=display%3A%20flex" target="_blank">(바로 이동)</a>
- Chrome, Edge, Firefox 등 거의 대부분의 브라우저에서는 `display: flex;` 기술 지원이 구현(초록색)되어 있지만 Internet Explorer에서는 6, 7 버전에서는 아예 지원하지 않고(빨간색) 8~11 버전에서는 부분적으로 지원해주고 있다.(노란색)
- Internet Explorer 환경에서 `flex` 속성을 이용하기 위해서는 `-ms-`와 같은 Vendor Prefix를 붙여야 사용할 수 있다.
- 그래서 내가 만들고자 하는 서비스에서 화면 정가운데에 요소를 배치해야하는 상황이 생길 때 모든 브라우저 환경에서 올바르게 작동해야 하는 상황이라면 즉, 크로스 브라우징 이슈까지 해결해야한다고 하면 `display: flex;` 속성을 이용하려면 제약 조건들을 고려해서 제작해야 한다.
- 만약 최신 기술을 사용해도 되고 Internet Explorer 환경은 고려하지 않는다면 우리의 정신 건강을 위해서 `display: flex;` 속성을 적극적으로 사용하는 것을 추천한다.

- 다음 `display: flex (2)`  시간에는 `flex`와 관련된 또 다른 CSS 속성들을 살펴보도록하자.