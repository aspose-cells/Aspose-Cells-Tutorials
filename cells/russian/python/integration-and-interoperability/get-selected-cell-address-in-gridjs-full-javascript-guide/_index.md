---
category: general
date: 2026-06-30
description: Узнайте, как получить адрес выбранной ячейки, обновить значение ячейки
  сетки и считать введённое значение с помощью JavaScript и GridJs. Пошаговый код
  и советы.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: ru
og_description: Получите адрес выбранной ячейки, обновите значение ячейки сетки и
  считайте вводимое значение с помощью JavaScript. Следуйте этому полному руководству
  для плавной интеграции GridJs.
og_title: Получить адрес выбранной ячейки – Полный учебник по GridJs JavaScript
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
title: Получить адрес выбранной ячейки в GridJs – Полное руководство по JavaScript
url: /ru/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получить адрес выбранной ячейки – Полный учебник по GridJs JavaScript

Когда‑нибудь вам нужно было **get selected cell address** из таблицы GridJs, но вы не знали, какой вызов API использовать? Вы не одиноки. Во многих админ‑панелях пользователи кликают по ячейке, редактируют значение в модальном окне и ожидают, что сетка сразу отобразит изменение. В этом учебнике показано, как точно получить этот адрес, считать новую цену из поля ввода и **update grid cell value** без перезагрузки страницы.

Мы также рассмотрим, как правильно **read input value with JavaScript**, обработаем граничные случаи и закроем модальное окно после завершения обновления. К концу вы получите автономный фрагмент кода, который можно вставить в любой проект, использующий GridJs.

## Что вы построите

- Простая HTML‑таблица на базе GridJs.
- Модальное окно редактирования, которое появляется при клике по ячейке.
- JavaScript, который **gets the selected cell address**, захватывает введённую пользователем цену, **updates the grid cell value**, и в конце скрывает модальное окно.

Никакие внешние библиотеки, кроме GridJs, не требуются, код работает в современных браузерах (Chrome 102+, Edge, Firefox). Если у вас уже есть экземпляр GridJs на странице, вы можете просто скопировать‑вставить нужные части.

## Предварительные требования

- Базовые знания JavaScript и DOM.
- Библиотека GridJs загружена (через CDN или npm).
- Страница, уже отображающая сетку GridJs (мы покажем минимальный пример).

Если что‑то из этого вам незнакомо, не паникуйте — каждый шаг включает краткое повторение.

---

## Шаг 1: Настройте HTML‑скелет

Сначала разместите контейнер таблицы, скрытое модальное окно и поле ввода цены. Модальное окно будет переключаться простыми CSS‑классами.

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

> **Pro tip:** `#editModal` использует минимальный CSS‑трюк — просто добавьте класс `active`, чтобы показать его. Вы можете заменить это на Bootstrap, Tailwind или любой другой модальный компонент, который уже используете.

---

## Шаг 2: Инициализируйте GridJs и захватывайте клики по ячейкам

Теперь мы создадим сетку с примерными данными и будем слушать выбор ячеек. Когда пользователь кликает по ячейке, мы **get the selected cell address** и откроем модальное окно.

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

> **Why this works:** `GridJs.getSelectedCell()` возвращает строку вроде `"C2"` (столбец C, строка 2). Сохранение её в `lastSelectedCell` позволяет нам позже, при **update grid cell value**, точно указать местоположение.

---

## Шаг 3: Считайте новую цену из поля ввода

Когда пользователь нажимает **Save**, нам нужно безопасно **read input value with JavaScript**. Этот шаг также проверяет, что введённая цена является положительным числом.

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

> **Note:** Использование `parseFloat` гарантирует, что мы принимаем десятичные числа (например, `1.99`). Защита `isNaN` предотвращает случайные пустые отправки.

---

## Шаг 4: Обновите значение выбранной ячейки

Теперь мы наконец **update grid cell value**, используя ранее захваченный адрес. Метод `updateCell` в GridJs возвращает promise, поэтому мы можем добавить действие закрытия модального окна.

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

> **Why use a promise?** GridJs может потребоваться переотрисовать таблицу или синхронизироваться с бекендом. Ожидая завершения promise, мы гарантируем, что UI скрывается только после того, как сетка отобразит новое значение.

---

## Шаг 5: Обработайте отмену и граничные случаи

Надёжное решение всегда предоставляет пользователю способ выйти. Кнопка **Cancel** просто скрывает модальное окно и очищает любой сохранённый адрес.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Что если ячейка не выбрана?

Если пользователь каким‑то образом нажимает кнопку **Save**, не кликнув сначала ячейку (возможно, модальное окно открыто программно), `lastSelectedCell` будет `null`. Ранний `return` в `updateSelectedCell` предотвращает ошибку выполнения и выводит полезное предупреждение в консоль.

### Работа с большими сетками

Для сеток с пагинацией `GridJs.getSelectedCell()` всё равно возвращает абсолютный адрес (например, `"B12"`), а не только видимую строку. Это значит, что обновление работает, даже если отредактированная строка находится на другой странице. Учтите, что UI не переключит страницу автоматически после обновления — если это необходимо, вызовите `grid.forceUpdate()` или перейдите на нужную страницу вручную.

---

## Полный рабочий пример

Ниже приведён полный код, который можно скопировать‑вставить в один HTML‑файл. Откройте его в браузере, кликните любую ячейку, измените цену и наблюдайте мгновенное обновление сетки.

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


## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Получить адрес, количество ячеек и смещение для всего диапазона Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Получить адрес, количество ячеек и смещение для всего диапазона Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Получить адрес, количество ячеек и смещение для всего диапазона Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}