---
category: general
date: 2026-06-21
description: Создайте интерактивную таблицу данных с помощью Grid.js и научитесь отображать
  таблицу JSON с сортировкой, пагинацией и поиском. Идеально подходит для веб‑дашбордов.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: ru
og_description: Создайте интерактивную таблицу данных за считанные минуты. Узнайте,
  как использовать Grid.js для отображения JSON‑таблицы с пагинацией, сортировкой
  и поиском.
og_title: Создайте интерактивную таблицу данных с Grid.js – полный учебник
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
title: Создайте интерактивную таблицу данных с Grid.js — полное пошаговое руководство
url: /ru/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание интерактивной таблицы данных с Grid.js – Полное пошаговое руководство

Когда‑нибудь задумывались, как **создать интерактивную таблицу данных**, позволяющую пользователям сортировать, искать и листать строки без написания бэкенда? Вы не одиноки. Во многих дашбордах самая большая боль — превратить статический дамп JSON в гладкую, удобную таблицу, похожую на электронную таблицу, но работающую полностью в браузере.

В этом руководстве мы пройдемся по **использованию Grid.js** для **отображения JSON‑таблицы** на обычной HTML‑странице. К концу вы получите рабочий пример, который можно вставить в любой проект, а также советы по настройке панели инструментов, работе с большими наборами данных и избежанию распространённых ошибок.

## Что вы узнаете

- Как получить JSON‑файл, определяющий столбцы и строки.
- Как инициализировать **Grid.js** с пагинацией, сортировкой, поиском и пользовательской панелью инструментов.
- Как отрисовать сетку в целевом контейнере.
- Дополнительные настройки: пользовательское форматирование ячеек, переключение тем и обработка ошибок.
- Полный готовый к копированию пример кода.

### Предварительные требования

Прежде чем приступить, убедитесь, что у вас есть:

1. Современный браузер (Chrome, Edge или Firefox) — Grid.js использует возможности ES6.
2. Локальная или удалённая папка, содержащая файл `grid_data.json` (формат будет показан ниже).
3. Базовые знания HTML и JavaScript — ничего сложного, только возможность открыть файл `.html` в браузере.

Никаких сборочных инструментов, npm‑установок, серверного кода. В этом и прелесть **создания интерактивной таблицы данных** с Grid.js: всё работает напрямую из CDN.

---

## Шаг 1: Подготовьте JSON, определяющий вашу таблицу

Первое, что нужно — это JSON‑payload, который сообщает Grid.js, какие столбцы существуют и какие строки показывать. По сути это чертёж для вашей **отображаемой JSON‑таблицы**. Ниже минимальный пример, который можно сохранить как `grid_data.json` в той же директории, что и ваш HTML‑файл:

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

*Почему именно такой формат?* Grid.js ожидает, что `columns` будет массивом строк (или объектов для продвинутой конфигурации), а `rows` — массивом массивов, где каждый вложенный массив соответствует порядку столбцов. При желании можно добавить больше столбцов или вложенные объекты — Grid.js отобразит их, пока формы совпадают.

> **Pro tip:** Если вы получаете данные из API, просто замените статический `fetch('grid_data.json')` на URL вашего эндпоинта. Остальная часть кода остаётся той же.

---

## Шаг 2: Инициализируйте Grid.js — ядро **как использовать gridjs**

Теперь, когда источник данных готов, нам нужно подключить Grid.js к странице и задать его поведение. Здесь мы действительно **создаём интерактивную таблицу данных**, добавляя пагинацию, сортировку и удобную кнопку панели инструментов.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN предоставляет последнюю стабильную версию, а тема Mermaid добавляет чистый современный вид «из коробки». При желании можно заменить её на `gridjs.min.css`, если вам больше нравится стиль по умолчанию.

Далее, внутри тега `<script>`, получаем JSON и инициализируем сетку:

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

### Разбор параметров

| Опция | Что делает | Почему важно |
|--------|--------------|----------------|
| `pagination` | Делит строки на страницы (по умолчанию 10 на страницу) | Делает большие таблицы удобными, не перегружая интерфейс. |
| `sort` | Щелчок по заголовку столбца переключает порядок возрастания/убывания | Пользователи быстро находят строки с наибольшими значениями. |
| `search` | Добавляет текстовое поле, фильтрующее строки «на лету» | Отлично подходит для быстрых поисков без перезагрузки данных. |
| `toolbar` | Добавляет пользовательские кнопки или выпадающие списки над таблицей | Идеально для действий «Помощь», «Экспорт» или «Обновить». |
| `formatter` | Позволяет возвращать чистый HTML для ячейки | Здесь мы превращаем строки email в кликабельные ссылки mailto. |

> **Почему такой подход?** Декларативная конфигурация сетки позволяет легко менять поведение, не трогая основную логику рендеринга. Это рекомендованный способ **как использовать Grid.js** в большинстве проектов.

---

## Шаг 3: Отрисуйте сетку на странице

Последняя строка скрипта — `grid.render(document.getElementById('grid-container'))` — вставляет полностью функционирующую таблицу в `<div>`, который вы разместили где‑нибудь в теле HTML:

```html
<div id="grid-container"></div>
```

И всё. При загрузке страницы браузер получает JSON, создаёт экземпляр Grid.js и выводит интерактивную таблицу на экран. Без обновлений, без серверных запросов после начальной загрузки.

---

## Необязательно: Настройка стилей и тем

Если тема Mermaid вам не по вкусу, её можно заменить любой из встроенных тем (`gridjs.min.css`) или написать собственный CSS. Например, чтобы задать заголовку мягкий серый фон:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Добавьте фрагмент в тег `<style>` или во внешний файл стилей. Grid.js уважает стандартные CSS‑селекторы, так что у вас полный контроль над шрифтами, цветами и отступами.

---

## Распространённые ошибки и как их избежать

| Ошибка | Симптом | Решение |
|---------|---------|-----|
| **CORS‑ошибки** при получении JSON с другого домена | В консоли браузера появляется «Blocked by CORS policy» | Размещайте JSON на том же источнике или включите CORS на сервере. |
| **Большие наборы данных вызывают задержки** | Прокрутка становится «тормозной», пагинация медленная | Используйте серверную пагинацию (`pagination: { server: { url: (prev, page, limit) => … } }`) или ленивую загрузку строк. |
| **Кнопка панели инструментов не появляется** | Кнопка не видна, хотя `toolbar.enabled: true` | Убедитесь, что используете Grid.js версии 2.0+; в более старых версиях API панели был другим. |
| **Ссылки‑email не кликабельны** | Форматтер возвращает обычный текст | Возвращайте `gridjs.html(...)` вместо простой строки, как показано в примере. |

Раннее решение этих вопросов сэкономит часы отладки.

---

## Полный рабочий пример (готовый к копированию)

Ниже полностью готовый HTML‑файл, который можно сохранить как `index.html`. Откройте его в браузере, и вы увидите полностью функционирующий **демонстрационный пример создания интерактивной таблицы данных**, который **отображает JSON‑таблицу** с сортировкой, поиском и кнопкой помощи.



## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Как создать список проверки данных Excel с Aspose.Cells для Java: пошаговое руководство](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Как создать флажки в Excel с помощью Aspose.Cells для .NET | Руководство по проверке данных](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Создание и импорт XML‑данных в Excel с помощью Aspose.Cells для Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}