# avatars

float, flex 속성을 사용한 정렬 [바로가기](../avatars/avatars.html)

## markup 구조

아바타들이 나열된 형태이기 때문에, 순서가 없는 목록 태그인 `ul` 태그 안에 이미지 태그, 아바타들의 상태 텍스트를 가진 `li`가 반복되도록 마크업 하였습니다.

```html
<ul class="avatars-list" aria-label="아바타 목록" aria-live="polite">
  <!-- 반복 시작 -->
  <li class="avatar-item">
    <picture>
      <source srcset="../assets/images/avatars_01.webp 1x, ../assets/images/avatars_01_2x.webp 2x" />
      <img src="../assets/images/png/avatars_01.png" alt="avatar 1" aria-label="avatar 1" />
    </picture>
    <span class="avatar-state" aria-label="아바타 상태">오프라인</span>
  </li>
  <!-- 반복 끝 -->
</ul>
```

### 접근성에 대한 고민🤔

- `ul` 태그를 사용하여 목록인 것을 알 수 있기때문에 `role` 속성은 넣어 주지 않는 대신 어떤 목록인지를 알려주기 위해 `aria-label` 속성을 사용하여 읽어줄 수 있도록 했습니다.
- 아바타들의 상태는 변하는 정보이기 때문에 사용자에게 정보가 변했음을 알려줄 수 있는 aria state 속성에 대해서 찾아 보았습니다.

#### aria-live

> 글로벌 `aria-live`속성은 요소가 업데이트될 것임을 나타내며, 사용자 에이전트, 보조 기술, 사용자가 라이브 영역에서 기대할 수 있는 업데이트 유형을 설명합니다.

> 초기 로드 후 콘텐츠가 변경되면 보조 기술(AT) 사용자는 변경 사항을 "볼" 수 없습니다.
> 일부 변경 사항은 중요합니다. 다른 변경 사항은 중요하지 않습니다. 이 aria-live속성을 사용하면 개발자가 사용자에게 업데이트를 알리고 중요도와 긴급성에 따라 AT 사용자에게 콘텐츠 변경 사항을 즉시, 적극적으로 또는 수동적으로 알릴지 선택할 수 있습니다.

| aria-live values | 설명                                                                                                                             |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `assertive`      | 해당 지역의 업데이트가 가장 높은 우선순위를 가지며 사용자에게 즉시 제공되어야 함을 나타냅니다.                                   |
| `off (default)`  | 사용자가 현재 해당 지역에 집중하고 있지 않으면 해당 지역의 업데이트가 사용자에게 표시되지 않음을 나타냅니다.                     |
| `polite`         | 현재 문장을 말하는 것이 끝날 때나 사용자가 입력을 멈출 때 등 다음 적절한 기회에 해당 지역의 업데이트를 표시해야 함을 나타냅니다. |

출처 - [MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-live)

#### ❓궁금증

assertive, polite 값 사용 시 포커스가 현재 위치에서 업데이트 된 정보로 이동하는 것인지, 변화한 정보를 읽은 후 다시 원래의 포커스로 이동하는 지 궁금합니다. 혹은 포커스의 이동 없이 변화한 정보를 읽어주는지요.

## 이미지 성능 최적화

`picture` 태그를 사용하여 `webp`로 변환한 1배수, 2배수를 설정하여 모니터의 사양에 맞게 로드 되도록 하였고, `webp` 이미지를 지원하지 않는 경우에는 png 이미지가 보여질 수 있도록 하였습니다.

### png이미지와 webp이미지의 용량 차이 비교

| 이미지 종류 |                                                      avatar 1                                                      |                                                      avatar 2                                                      |                                                      avatar 3                                                      |                                                      avatar 4                                                      |                                                      avatar 5                                                      |                                                      avatar 6                                                      |                                                      avatar 7                                                      |                                                      avatar 8                                                      |
| ----------- | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: |
| webp        |  ![avatar 1](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_01.webp)   |  ![avatar 2](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_02.webp)   |  ![avatar 3](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_03.webp)   |  ![avatar 4](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_04.webp)   |  ![avatar 5](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_05.webp)   |  ![avatar 6](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_06.webp)   |  ![avatar 7](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_07.webp)   |  ![avatar 8](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/avatars_08.webp)   |
| 용량        |                                                       1.5KB                                                        |                                                       1.5KB                                                        |                                                       1.5KB                                                        |                                                       1.6KB                                                        |                                                       1.4KB                                                        |                                                       1.6KB                                                        |                                                       1.9KB                                                        |                                                        2KB                                                         |
| png         | ![avatar 1](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_01.png) | ![avatar 2](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_02.png) | ![avatar 3](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_03.png) | ![avatar 4](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_04.png) | ![avatar 5](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_05.png) | ![avatar 6](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_06.png) | ![avatar 7](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_07.png) | ![avatar 8](https://raw.githubusercontent.com/bohyemian/homework/refs/heads/main/assets/images/png/avatars_08.png) |
| 용량        |                                                       8.5KB                                                        |                                                       8.9KB                                                        |                                                       8.4KB                                                        |                                                       9.3KB                                                        |                                                       8.2KB                                                        |                                                       8.3KB                                                        |                                                       9.4KB                                                        |                                                       9.4KB                                                        |

### 마치며

보기에는 단순해 보이는 화면 구성이지만 접근성과 최적화를 고민하며 만드느라 생각보다 많은 시간이 걸렸습니다.

아직 aria의 사용이 익숙하지 않아서 맞게 사용한 것인지 의구심도 들고,
aria state는 변할 수 있기 때문에 속성을 넣는 것 만으로 끝나지 않고 값이 바뀔 때마다 바꿔주어야 해서 추가적인 작업이 더 필요할텐데 그런 처리를 놓치는 경우 오히려 사용자에게 정보의 혼선을 줄 수 있을 것 같다는 생각이 들었습니다.
