---
category: general
date: 2026-06-30
description: GridJs를 사용하여 JavaScript로 선택한 셀 주소를 가져오고, 그리드 셀 값을 업데이트하며, 입력 값을 읽는 방법을
  배워보세요. 단계별 코드와 팁.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: ko
og_description: 선택한 셀 주소를 가져오고, 그리드 셀 값을 업데이트하며, JavaScript로 입력 값을 읽어보세요. 원활한 GridJs
  통합을 위해 이 완전한 가이드를 따라가세요.
og_title: 선택된 셀 주소 가져오기 – 완전한 GridJs JavaScript 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: GridJs에서 선택된 셀 주소 가져오기 – 전체 JavaScript 가이드
url: /ko/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 선택된 셀 주소 가져오기 – 완전한 GridJs JavaScript 튜토리얼

GridJs 테이블에서 **선택된 셀 주소를 가져와야** 했지만 어떤 API 호출을 사용해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 관리 패널에서 사용자는 셀을 클릭하고 모달에서 값을 편집한 뒤 그리드가 즉시 변경 사항을 반영하기를 기대합니다. 이 튜토리얼에서는 해당 주소를 정확히 어떻게 가져오고, 입력 필드에서 새로운 가격을 읽으며, 페이지를 새로 고치지 않고 **그리드 셀 값을 업데이트**하는 방법을 보여줍니다.

또한 **JavaScript로 입력값 읽기**를 올바르게 수행하는 방법, 엣지 케이스 처리, 업데이트가 완료되면 모달을 닫는 방법까지 다룹니다. 마지막까지 진행하면 GridJs를 사용하는 어떤 프로젝트에도 바로 삽입할 수 있는 독립형 스니펫을 얻게 됩니다.

## 만들게 될 것

- GridJs로 구동되는 간단한 HTML 테이블
- 셀을 클릭하면 나타나는 편집 모달
- **선택된 셀 주소를 가져오고**, 사용자가 입력한 가격을 잡아 **그리드 셀 값을 업데이트**한 뒤 모달을 숨기는 JavaScript

외부 라이브러리는 GridJs 외에 필요 없으며, 코드는 최신 브라우저(Chrome 102+, Edge, Firefox)에서 동작합니다. 이미 페이지에 GridJs 인스턴스가 있다면 관련 부분만 복사‑붙여넣기 하면 됩니다.

## 사전 요구 사항

- JavaScript와 DOM에 대한 기본 지식
- GridJs 라이브러리 로드됨(CDN 또는 npm 사용)
- 이미 GridJs 그리드를 렌더링하고 있는 페이지(간단한 예시를 보여드림)

위 항목이 익숙하지 않다고 해도 걱정 마세요—각 단계마다 간단히 정리해 두었습니다.

---

## 단계 1: HTML 골격 설정

먼저 테이블 컨테이너, 숨겨진 모달, 가격 입력 필드를 배치합니다. 모달은 간단한 CSS 클래스 토글로 표시됩니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** `#editModal`은 최소한의 CSS 트릭을 사용합니다—`active` 클래스를 추가하면 표시됩니다. 이를 Bootstrap, Tailwind 또는 이미 사용 중인 다른 모달 컴포넌트로 교체해도 됩니다.

---

## 단계 2: GridJs 초기화 및 셀 클릭 캡처

이제 샘플 데이터를 사용해 그리드를 만들고 셀 선택을 감지합니다. 사용자가 셀을 클릭하면 **선택된 셀 주소를 가져오고** 모달을 엽니다.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()`은 `"C2"`와 같은 문자열을 반환합니다(열 C, 행 2). 이를 `lastSelectedCell`에 저장하면 나중에 **그리드 셀 값을 업데이트**할 때 정확한 위치를 참조할 수 있습니다.

---

## 단계 3: 입력 필드에서 새로운 가격 읽기

사용자가 **Save** 버튼을 클릭하면 **JavaScript로 입력값 읽기**를 안전하게 수행해야 합니다. 이 단계에서는 입력된 가격이 양수인지도 검증합니다.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** `parseFloat`를 사용하면 소수점(예: `1.99`)도 허용됩니다. `isNaN` 검사는 실수로 빈 값이 제출되는 것을 방지합니다.

---

## 단계 4: 선택된 셀 값 업데이트

이제 앞서 캡처한 주소를 사용해 **그리드 셀 값을 업데이트**합니다. GridJs의 `updateCell` 메서드는 프로미스를 반환하므로, 프로미스 체이닝으로 모달 닫기 동작을 연결할 수 있습니다.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** GridJs는 테이블을 다시 렌더링하거나 백엔드와 동기화해야 할 수 있습니다. 프로미스를 기다림으로써 UI가 그리드가 새로운 값을 반영한 뒤에만 숨겨지도록 보장합니다.

---

## 단계 5: 취소 및 엣지 케이스 처리

견고한 솔루션은 항상 사용자가 빠져나갈 방법을 제공합니다. **Cancel** 버튼은 모달을 숨기고 저장된 주소를 초기화합니다.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### 셀을 선택하지 않은 경우는?

사용자가 셀을 클릭하지 않고 **Save** 버튼을 강제로 눌렀을 경우(`lastSelectedCell`이 `null`), `updateSelectedCell` 내부의 조기 반환이 런타임 오류를 방지하고 유용한 경고를 로그에 남깁니다.

### 대형 그리드 처리

페이지네이션이 있는 그리드에서도 `GridJs.getSelectedCell()`은 절대 주소(예: `"B12"` )를 반환하므로, 편집된 행이 다른 페이지에 있더라도 업데이트가 정상 작동합니다. 다만 업데이트 후 UI가 자동으로 페이지를 전환하지는 않으니, 필요하다면 `grid.forceUpdate()`를 호출하거나 직접 페이지를 이동시켜야 합니다.

---

## 완전한 작동 예제

아래 코드는 하나의 HTML 파일에 복사‑붙여넣기 하면 바로 실행할 수 있는 전체 예시입니다. 브라우저에서 열고 셀을 클릭한 뒤 가격을 바꾸면 그리드가 즉시 업데이트되는 것을 확인해 보세요.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 작동 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [전체 Excel 범위에 대한 주소, 셀 수, 오프셋 가져오기](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [전체 Excel 범위에 대한 주소 셀 수 및 오프셋 가져오기](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [전체 Excel 범위에 대한 주소 셀 수 및 오프셋 가져오기](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}