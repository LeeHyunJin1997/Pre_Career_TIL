# 웹페이지 디자인 형태

- 고정폭 레이아웃
- 유동적 레이아웃
- 별도 사이트 : 디바이스별 별도의 도메인으로 분리
- 반응형 레이아웃 : 디스플레이 종류에 따라 화면의 크기가 변화



# 미디어 쿼리

```css
@media media-type and (media-feature-rule) {
    /* CSS rules go here */
}
```

- CSS에서 @media 키워드를 활용하여 환경에 따른 CSS를 적용
- media-type
  - all
  - print
  - screen
  - speech
- media-feature-rule
  - `and` 혹은 `,(or)` 로 조건 제어 가능
  - `orientation: landscape` : 가로모드 (너비 > 높이)
  - `orientation: portrait` : 세로모드 (너비 < 높이)
  - `min-width`
  - `max-width`

