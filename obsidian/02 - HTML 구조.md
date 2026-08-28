---
title: HTML 구조
tags: [obsidian, html]
created: 2026-08-28
source: index.html
---

# 02 - HTML 구조

`index.html` 은 화면의 뼈대입니다. 전체가 18줄로 짧습니다.

## 주요 요소

| 요소 | id / class | 역할 |
| --- | --- | --- |
| `<button>` | `theme-toggle` | 라이트/다크 테마 전환 버튼 (우측 상단 고정) |
| `<div>` | `container` | 앱 전체를 감싸는 카드 |
| `<h1>` | — | 제목 "Lotto Number Generator" |
| `<button>` | `generate-btn` | 번호 생성 버튼 |
| `<div>` | `lotto-numbers` | 생성된 공이 들어갈 빈 컨테이너 |

## 코드 뜯어보기

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lotto Number Generator</title>
    <link rel="stylesheet" href="style.css">   <!-- CSS 연결 -->
</head>
<body>
    <button id="theme-toggle">Dark Mode</button>  <!-- JS 가 텍스트를 바꿔줌 -->
    <div class="container">
        <h1>Lotto Number Generator</h1>
        <button id="generate-btn">Generate Numbers</button>
        <div id="lotto-numbers"></div>            <!-- 비어 있음: JS 가 채움 -->
    </div>
    <script src="main.js"></script>               <!-- body 끝에서 로드 -->
</body>
```

## 짚어둘 점

- `#lotto-numbers` 는 처음에 **비어 있습니다.** 버튼을 눌러야 [[04 - JavaScript 로직#displayLottoNumbers]] 가 공을 채워 넣습니다.
- `theme-toggle` 버튼의 텍스트("Dark Mode")는 로드 시 JS가 이모지 포함 텍스트로 교체합니다. → [[04 - JavaScript 로직#테마 토글]]
- `viewport` 메타 태그가 있어야 모바일 반응형이 제대로 동작합니다. → [[03 - CSS 스타일링#반응형]]
- `id` 는 JS가 요소를 찾는 열쇠(`getElementById`)이고, `class` 는 CSS 스타일을 붙이는 열쇠입니다.

#html
