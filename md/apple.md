# apple 제품 카드 [바로가기](../apple/apple.html)🍎

🏷️ **개요**
1. [구조](#구조)
   * [card 컴포넌트](#card-컴포넌트)
   * [레이아웃](#레이아웃)
2. [CSS 스타일링](#스타일링)
3. [결과화면]()
4. [마치며](#마치며)

## 구조

### card 컴포넌트
```html
<div class="card iPad-pro">
  <strong class="card__title">iPad Pro</strong>
  <p class="card__sub-title">
    <span class="card__sub-title-txt">놀라우리만치 얇다.</span>
    <span class="card__sub-title-txt">엄청나게 강력하다.</span>
  </p>
  <p class="card__description">출시일 추후 공개</p>
  <div class="card__btns">
    <a href="#" class="btn bg-type">더 알아보기</a>
    <a href="#" class="btn line-type">가격보기</a>
  </div>
</div>
```
`card` 컨테이너 안에 타이틀, 서브타이틀, 디스크립션, 버튼을 1열로 배치했습니다.

서브타이틀은 모바일에서 줄바꿈 되었다가(모바일 퍼스트) width 1024px 이상부터 한 줄로 바뀌도록  
각각 span태그로 감싸 `display: block` 이었다가 `inline-block` 속성으로 바꿔 주었습니다.

클래스명은 BEM 방식으로 지었고, 버튼은 카드 컴포넌트 아닌 곳에서도 재사용하도록 `card__`를 붙이지 않았습니다.

상품별로 배경이미지를 주기 위해 card에 상품명 클래스를 추가하여 분기했습니다.

### 레이아웃
`card` 컴포넌트를 `grid-cards`로 감싸고 `display: grid` 그리드 컨테이너로 만들어 주었습니다.
```css
.grid-cards {
  grid-template-columns: [cell-span-start cell-odd-start] 1fr [cell-odd-end cell-even-start] 1fr [cell-even-end cell-span-end];

  .card {
    @media (width >= 1024px) {
      &.grid-item-odd {
        grid-column: cell-odd;
      }

      &.grid-item-even {
        grid-column: cell-even;
      }
    }
  }
}
```
2열을 차지하는 `card`에는 `grid-column: cell-span` 속성을 주고  
`grid-item-odd`, `grid-item-even` 클래스로 각각 1열, 2열을 분기하여 color와 버튼의 스타일을 바꿔 주었습니다.


## 스타일링
### 픽셀의 밀도에 따른 이미지 분기
`picture` tag의 `srcset` 속성으로 밀도에 따라 리소스 이미지를 셋팅 했었던 것을 background로 구현하는 조건이는데,
밀도에 따라 분기 해야 겠다는 생각에 미디어쿼리 중에 밀도에 따라 분기할 수 있는 조건이 있는지 찾아 보았습니다.

처음에는 [-webkit-device-pixel-ratio](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/-webkit-device-pixel-ratio) 를 찾게 되었는데 문서를 읽어보니 [`resolution`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/resolution)를 대신 사용하라고 나와 있었습니다.
>참고: 가능하다면 resolution표준 미디어 기능인 미디어 기능 쿼리를 대신 사용하세요.

## 결과화면
<video src="https://github.com/user-attachments/assets/db8bf02d-b40e-4438-bcbf-ab71e7ec7ed9" width="680" height="340" controls="false"></video>

## 마치며
picture로 넣을 때에는 다른 확장자의 이미지도 추가적으로 셋팅할 수 있었는데 미디어 쿼리로 작성하게 되면  
'미디어 쿼리 내에서 `@supports`로 다시 분기를 해야 하나' 갸웃 하면서도 추가적으로 더 찾아보지 않았습니다.

뒤늦게 다른 방법이 있다는 것을 알게 되었는데, 구글링하는 것도 개인의 능력치라고 생각해서 조금 더 여러 방법을 찾아 보면 좋았겠다는 생각이 들었습니다. 🥲

수업 중에도 각자 구현하는 시간에 다른 방법을 고민하지 않고 익숙하게 하던 방식을 고수하는 것을 느꼈는데
새로 배운 것들, 아직 모르는 새로운 것들이 있는지 찾아보는 습관을 들여야겠다고 생각했습니다.


마지막 과제이고 뭐든 만들 수 있는 재료를 다 모았다고 생각되어 *배웠던 것을 총망라 해보자!* 라는 마음으로 시작했는데,  
놓친게 분명 있을텐데도 막상 뭘 더 할 수 있을까 떠오르지 않아서 복습이 많이 필요할 것 같고 아쉬움도 남는 과제였습니다.