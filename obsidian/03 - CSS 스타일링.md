---
title: CSS 스타일링
tags: [obsidian, css, 디자인]
created: 2026-08-28
source: style.css
---

# 03 - CSS 스타일링

`style.css` 는 디자인, 테마 전환, 애니메이션, 반응형을 담당합니다.

## CSS 변수(커스텀 프로퍼티)로 테마 만들기

핵심 아이디어: **색상 값을 변수로 뽑아** 두고, 테마가 바뀌면 변수만 갈아끼웁니다.

```css
:root {
    --bg-gradient: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    --text-color: #2c3e50;
    --btn-bg: #4CAF50;
    /* ... */
}

[data-theme="dark"] {
    --bg-gradient: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
    --text-color: #ecf0f1;
    --btn-bg: #2ecc71;
    /* ... */
}
```

- `:root` = 기본(라이트) 테마 변수
- `[data-theme="dark"]` = `<html>` 에 `data-theme="dark"` 가 붙었을 때 덮어쓰는 값
- 이 속성을 켜고 끄는 일은 JS가 합니다. → [[04 - JavaScript 로직#테마 토글]]

## 로또 공 스타일

```css
.lotto-ball {
    width: 55px; height: 55px;
    border-radius: 50%;          /* 원형 */
    display: flex;                /* 숫자 가운데 정렬 */
    justify-content: center;
    align-items: center;
    animation: popIn 0.5s ... forwards;   /* 등장 애니메이션 */
}
```

공의 **배경색은 CSS가 아니라 JS**가 인라인으로 지정합니다(숫자 구간별 색).
→ [[04 - JavaScript 로직#getLottoColor]]

## 등장 애니메이션

```css
@keyframes popIn {
    0%   { transform: scale(0.5) translateY(20px); opacity: 0; }
    100% { transform: scale(1)   translateY(0);    opacity: 1; }
}
```

작게 + 아래에서 시작해 → 제자리로 튀어오르며 나타납니다.

## 반응형

```css
@media (max-width: 480px) {
    .container { padding: 2rem; }
    h1 { font-size: 1.8rem; }
    .lotto-ball { width: 45px; height: 45px; font-size: 16px; }
}
```

화면 폭이 480px 이하이면 여백·글씨·공 크기를 줄여 모바일에 맞춥니다.

## 관련 노트

- 테마 동작 로직 → [[04 - JavaScript 로직]]
- CSS 변수 개념 → [[05 - 핵심 개념 정리#CSS 변수]]
- 용어 → [[99 - 용어집]]

#css #디자인
