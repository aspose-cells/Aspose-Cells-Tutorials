---
category: general
date: 2026-06-21
description: Grid.js를 사용하여 인터랙티브 데이터 그리드를 만들고, 정렬·페이지네이션·검색 기능이 포함된 JSON 데이터 테이블을
  표시하는 방법을 배워보세요. 웹 대시보드에 최적입니다.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: ko
og_description: 몇 분 안에 인터랙티브한 데이터 그리드를 만들 수 있습니다. Grid.js를 사용하여 페이지네이션, 정렬 및 검색이 가능한
  JSON 데이터 테이블을 표시하는 방법을 배워보세요.
og_title: Grid.js로 인터랙티브 데이터 그리드 만들기 – 완전 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Grid.js로 인터랙티브 데이터 그리드 만들기 – 전체 단계별 가이드
url: /ko/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide

정적 JSON 덤프를 스프레드시트처럼 부드럽고 검색 가능한 테이블로 바꾸는 것이 가장 큰 고민이신가요? 백엔드를 작성하지 않고도 사용자가 정렬, 검색, 페이지 이동을 할 수 있는 **인터랙티브 데이터 그리드**를 만들고 싶다면, 당신만 그런 것이 아닙니다. 많은 대시보드에서 가장 큰 고통은 바로 이 작업입니다.

이 튜토리얼에서는 **Grid.js**를 사용해 **JSON 데이터 테이블**을 일반 HTML 페이지에 표시하는 방법을 단계별로 안내합니다. 튜토리얼을 마치면 어떤 프로젝트에도 바로 넣을 수 있는 동작 예제를 얻을 수 있으며, 툴바 커스터마이징, 대용량 데이터 처리, 흔히 발생하는 문제 회피 팁도 함께 제공합니다.

## What You’ll Learn

- 컬럼과 행을 정의한 JSON 파일을 가져오는 방법
- 페이지네이션, 정렬, 검색, 커스텀 툴바를 포함한 **Grid.js** 초기화 방법
- 그리드를 목표 컨테이너에 렌더링하는 방법
- 선택 사항: 셀 포맷팅 커스터마이징, 테마 전환, 오류 처리
- 복사‑붙여넣기만 하면 되는 완전한 코드 샘플

### Prerequisites

시작하기 전에 아래 항목을 준비하세요:

1. 최신 브라우저(Chrome, Edge, Firefox) – Grid.js는 ES6 기능에 의존합니다.
2. `grid_data.json` 파일이 들어 있는 로컬 또는 원격 폴더(포맷은 아래 예시 참고)
3. HTML과 JavaScript에 대한 기본 지식 – 별다른 빌드 도구 없이 `.html` 파일을 브라우저에서 열 수 있으면 충분합니다.

빌드 도구도, npm 설치도, 서버‑사이드 코드도 필요 없습니다. 바로 CDN에서 로드해 **인터랙티브 데이터 그리드**를 만들 수 있는 것이 Grid.js의 장점입니다.

---

## Step 1: Prepare the JSON That Defines Your Table

그리드에 어떤 컬럼이 존재하고 어떤 행을 표시할지 알려주는 JSON 페이로드가 먼저 필요합니다. 이것을 **JSON 데이터 테이블을 표시**하기 위한 설계도라고 생각하면 됩니다. 아래 예시는 `grid_data.json`이라는 파일명으로 HTML 파일과 같은 디렉터리에 저장할 수 있는 최소 예시입니다:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Why this format?* Grid.js expects `columns` to be an array of strings (or objects for advanced configuration) and `rows` to be an array of arrays where each inner array matches the column order. You can, of course, add more columns or nested objects – Grid.js will render them as long as the shapes line up.

> **Pro tip:** If you’re pulling data from an API, just replace the static `fetch('grid_data.json')` with your endpoint URL. The rest of the code stays the same.

---

## Step 2: Initialise Grid.js – The Heart of **how to use gridjs**

데이터 소스가 준비되었으니 이제 Grid.js를 페이지에 불러오고 동작 방식을 지정해야 합니다. 여기서 실제로 **인터랙티브 데이터 그리드** 기능인 페이지네이션, 정렬, 툴바 버튼 등을 설정합니다.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN을 통해 최신 안정 버전을 가져오며, Mermaid 테마는 기본적으로 깔끔하고 현대적인 모습을 제공합니다. 기본 스타일링을 원한다면 `gridjs.min.css`로 교체하면 됩니다.

다음으로 `<script>` 태그 안에서 JSON을 가져와 그리드를 초기화합니다:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Breaking Down the Options

| Option | What It Does | Why It Matters |
|--------|--------------|----------------|
| `pagination` | Splits rows into pages (default 10 per page) | Keeps large tables usable without overwhelming the UI. |
| `sort` | Clickable column headers toggle ascending/descending order | Users can quickly find the highest‑value rows. |
| `search` | Adds a text input that filters rows on the fly | Great for ad‑hoc lookups without reloading data. |
| `toolbar` | Adds custom buttons or dropdowns above the grid | Perfect for “Help”, “Export”, or “Refresh” actions. |
| `formatter` | Lets you return raw HTML for a cell | Here we turn email strings into clickable mailto links. |

> **Why this approach?** By keeping the grid configuration declarative, you can easily tweak behaviour without touching the core rendering logic. This is the recommended way to **how to use Grid.js** for most projects.

---

## Step 3: Render the Grid Into Your Page

스크립트 마지막 줄인 `grid.render(document.getElementById('grid-container'))`는 완전한 테이블을 HTML 본문 어딘가에 배치한 `<div>`에 삽입합니다:

```html
<div id="grid-container"></div>
```

이것으로 끝입니다. 페이지가 로드되면 브라우저가 JSON을 가져와 Grid.js 인스턴스를 만들고, 인터랙티브 테이블을 화면에 그립니다. 초기 로드 이후에는 새로 고침이나 서버 호출이 필요 없습니다.

---

## Optional: Styling and Theme Tweaks

기본 Mermaid 테마가 마음에 들지 않으면 내장 테마(`gridjs.min.css`) 중 하나로 교체하거나 직접 CSS를 작성할 수 있습니다. 예를 들어 헤더 배경을 부드러운 회색으로 바꾸려면:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

위 코드를 `<style>` 태그 안이나 외부 스타일시트에 추가하세요. Grid.js는 표준 CSS 선택자를 그대로 따르므로 폰트, 색상, 간격 등을 자유롭게 제어할 수 있습니다.

---

## Common Pitfalls & How to Avoid Them

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| **CORS errors** when fetching JSON from another domain | Browser console shows “Blocked by CORS policy” | Host the JSON on the same origin or enable CORS on the server. |
| **Large data sets cause lag** | Scrolling becomes choppy, pagination slow | Use `server` pagination (`pagination: { server: { url: (prev, page, limit) => … } }`) or lazy‑load rows. |
| **Toolbar button doesn’t appear** | No button visible despite `toolbar.enabled: true` | Ensure you’re using Grid.js version 2.0+; older versions had a different toolbar API. |
| **Email links not clickable** | Formatter returns plain text | Return `gridjs.html(...)` instead of a plain string, as shown in the example. |

초기에 이러한 문제를 해결하면 나중에 디버깅에 소요되는 시간을 크게 절감할 수 있습니다.

---

## Full Working Example (Copy‑Paste Ready)

아래는 `index.html`로 저장해 바로 실행할 수 있는 완전한 HTML 파일입니다. 브라우저에서 열면 **인터랙티브 데이터 그리드** 데모가 표시되며, **JSON 데이터 테이블**을 정렬, 검색, 도움말 버튼과 함께 확인할 수 있습니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 배운 기술을 확장하고, 추가 API 기능을 마스터하거나 다른 구현 방식을 탐구하는 데 도움이 됩니다.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}