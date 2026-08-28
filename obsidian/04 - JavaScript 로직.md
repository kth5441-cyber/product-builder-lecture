---
title: JavaScript 로직
tags: [obsidian, javascript, 로직]
created: 2026-08-28
source: main.js
---

# 04 - JavaScript 로직

`main.js` 는 앱의 동작을 담당합니다. 크게 **① 테마 토글** 과 **② 로또 생성** 두 부분입니다.

## DOM 요소 가져오기

```js
const generateBtn    = document.getElementById('generate-btn');
const lottoNumbersDiv = document.getElementById('lotto-numbers');
const themeToggle    = document.getElementById('theme-toggle');
```

각 `id` 는 [[02 - HTML 구조]] 의 요소와 1:1로 대응합니다.

---

## 테마 토글

### initTheme

```js
function initTheme() {
    const savedTheme = localStorage.getItem('theme') || 'light';
    document.documentElement.setAttribute('data-theme', savedTheme);
    updateThemeButtonText(savedTheme);
}
```

- `localStorage` 에 저장된 테마를 읽어 적용 (없으면 `'light'`).
- `<html>` 에 `data-theme` 를 붙이면 [[03 - CSS 스타일링#CSS 변수(커스텀 프로퍼티)로 테마 만들기]] 의 변수가 바뀝니다.
- 페이지 로드 시 마지막 줄에서 한 번 호출됩니다.

### 토글 클릭

```js
themeToggle.addEventListener('click', () => {
    const currentTheme = document.documentElement.getAttribute('data-theme');
    const newTheme = currentTheme === 'light' ? 'dark' : 'light';
    document.documentElement.setAttribute('data-theme', newTheme);
    localStorage.setItem('theme', newTheme);   // 선택 기억
    updateThemeButtonText(newTheme);
});
```

라이트 ↔ 다크를 뒤집고, 선택을 저장하고, 버튼 글씨를 갱신합니다.

---

## 로또 생성

### 버튼 클릭 흐름

```js
generateBtn.addEventListener('click', () => {
    lottoNumbersDiv.innerHTML = '';           // 이전 결과 지우기
    const numbers = generateLottoNumbers();   // 6개 뽑기
    displayLottoNumbers(numbers);             // 화면에 그리기
});
```

### generateLottoNumbers

```js
function generateLottoNumbers() {
    const numbers = new Set();                // 중복 자동 제거
    while (numbers.size < 6) {
        const randomNumber = Math.floor(Math.random() * 45) + 1;  // 1~45
        numbers.add(randomNumber);
    }
    return Array.from(numbers).sort((a, b) => a - b);  // 오름차순
}
```

- `Set` 을 써서 **중복 없는** 6개를 보장합니다. → [[05 - 핵심 개념 정리#Set 으로 중복 제거]]
- `Math.floor(Math.random() * 45) + 1` → 1 이상 45 이하 정수.
- `sort((a,b) => a-b)` 로 숫자 오름차순 정렬(문자열 정렬 아님에 주의).

### displayLottoNumbers

```js
function displayLottoNumbers(numbers) {
    numbers.forEach(number => {
        const lottoBall = document.createElement('div');
        lottoBall.className = 'lotto-ball';
        lottoBall.textContent = number;
        lottoBall.style.backgroundColor = getLottoColor(number);  // 색 지정
        lottoNumbersDiv.appendChild(lottoBall);
    });
}
```

숫자마다 `.lotto-ball` div 를 만들어 색을 칠하고 컨테이너에 붙입니다.

### getLottoColor

```js
function getLottoColor(num) {
    if (num <= 10) return '#fbc400'; // 노랑
    if (num <= 20) return '#69c8f2'; // 파랑
    if (num <= 30) return '#ff7272'; // 빨강
    if (num <= 40) return '#aaa';    // 회색
    return '#b0d840';                // 초록
}
```

실제 로또 공 색 규칙을 흉내 낸 구간별 색상.

| 구간 | 색 | 코드 |
| --- | --- | --- |
| 1–10 | 노랑 | `#fbc400` |
| 11–20 | 파랑 | `#69c8f2` |
| 21–30 | 빨강 | `#ff7272` |
| 31–40 | 회색 | `#aaa` |
| 41–45 | 초록 | `#b0d840` |

## 관련 노트

- 전체 흐름 → [[01 - 파일 구조#로드 순서와 의존 관계]]
- 개념 정리 → [[05 - 핵심 개념 정리]]

#javascript #로직
