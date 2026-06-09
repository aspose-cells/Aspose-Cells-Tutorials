---
category: general
date: 2026-06-08
description: Добавьте пользовательское контекстное меню в GridJs и экспортируйте таблицу
  в CSV с загрузкой CSV‑файла в виде Blob. Следуйте этому пошаговому руководству для
  полностью работающего примера.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: ru
og_description: Добавьте пользовательское контекстное меню в GridJs и экспортируйте
  таблицу в CSV с помощью blob‑файла для загрузки. Узнайте полную реализацию за менее
  чем 10 минут.
og_title: Добавьте пользовательское контекстное меню в GridJs – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Добавление пользовательского контекстного меню в GridJs — Полное руководство
url: /ru/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить пользовательское контекстное меню в GridJs – Полное руководство

Хотите **добавить пользовательское контекстное меню** к компоненту GridJs? В этом руководстве мы подробно покажем, как это сделать, и как **экспортировать сетку в CSV** с помощью **download CSV file blob**. Независимо от того, создаёте ли вы быстрый админ‑панель или полноценную аналитическую панель, контекстное меню по правому клику, позволяющее пользователям выгружать данные в CSV, может значительно повысить продуктивность.

Мы охватим всё, что вам понадобится: серверную часть на Python с Flask, JavaScript‑обработчик, создающий Blob, и HTML/JS, который генерирует GridJs. К концу вы получите автономный пример, который можно вставить в любой проект.

---

## Что вам понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **Python 3.9+** и **Flask**, установленные (`pip install flask`).
- Обёртка **gridjs** для Python (или сама JavaScript‑библиотека) — в этом руководстве мы будем использовать лёгкую Python‑обёртку, отражающую JavaScript API.
- Базовое понимание **async JavaScript** (`fetch`, `Promise`) — не переживайте, мы объясним каждую строку.
- Любой удобный редактор (VS Code, PyCharm или даже простой текстовый редактор).

Это всё. Никаких дополнительных инструментов сборки фронтенда, никаких танцев с Node npm. Просто обычный Flask, обслуживающий HTML, генерируемый GridJs.

---

## Добавить пользовательское контекстное меню в GridJs

Первое, что нужно сделать, — сообщить GridJs, что вы хотите собственное меню правого клика. По умолчанию GridJs поставляется с минимальным набором (copy, paste и т.д.), но вы можете полностью заменить его.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Почему это важно:**  
Установка `CustomContextMenu` заменяет список по умолчанию на тот, который вы предоставляете. Строка `"Export CSV"` — это лишь метка; реальная работа происходит, когда пользователь нажимает её, что мы подключим в следующем шаге.

> *Совет:* Держите список коротким. Перегруженное контекстное меню теряет смысл быстрых действий.

---

## Экспортировать сетку в CSV с помощью загрузки Blob

Теперь, когда пункт меню существует, нам нужен JavaScript‑обработчик, который общается с сервером, получает CSV, преобразует его в **Blob** и принудительно инициирует загрузку. Именно здесь появляется фраза **download CSV file blob**.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Разбор обработчика

| Line | What It Does |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Вызывает маршрут Flask (`/export/csv`), передавая имя листа в строке запроса. |
| `.then(r => r.blob())` | Преобразует HTTP‑ответ в **Blob** — по сути бинарный контейнер для данных CSV. |
| `URL.createObjectURL(b)` | Генерирует временный URL, который браузер может воспринимать как файл. |
| `a.download = cell.sheetName + ".csv"` | Устанавливает имя файла, которое пользователь увидит в диалоговом окне загрузки. |
| `a.click()` | Программно кликает по скрытому элементу `<a>`, вызывая загрузку Blob. |

> **Зачем использовать Blob?**  
> Браузеры не могут напрямую загрузить обычный текст, полученный через `fetch`, без преобразования его в объект, похожий на файл. Приём с Blob‑URL — самый надёжный кросс‑браузерный способ инициировать **download CSV file blob** без перезагрузки страницы.

---

## Настройка Flask‑бэкенда

Фронтенд‑обработчик ожидает конечную точку по адресу `/export/csv`. Ниже минимальный Flask‑вью, который принимает имя листа, извлекает данные из рабочей книги и отсылает CSV в потоковом виде.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Ключевые моменты

- **`io.StringIO`** позволяет собрать CSV в памяти, не касаясь файловой системы.  
- **`Content‑Disposition`** сообщает браузеру, что файл является вложением, и предлагает имя файла. Хотя фронтенд тоже задаёт `a.download`, наличие этого заголовка на сервере обеспечивает резервный вариант для клиентов без JavaScript.  
- Маршрут предельно прост; позже вы можете добавить аутентификацию, проверки прав доступа или потоковую передачу для огромных наборов данных.

---

## Рендеринг Grid на клиенте

С готовыми контекстным меню и бэкендом последний шаг — отрисовать компонент GridJs и отправить HTML/JS в браузер.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

В Flask‑вью это обычно выглядит так:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Когда страница загружается, GridJs строит таблицу, внедряет пользовательское контекстное меню, а наш JavaScript‑обработчик готов к работе. Щёлкните правой кнопкой мыши любой ячейке, выберите **Export CSV** и наблюдайте, как браузер скачивает файл с именем, соответствующим листу.

---

## Полный рабочий пример (Все файлы)

Ниже полностью готовый код, который можно скопировать в новую папку. Установите Flask (`pip install flask`) и запустите `python app.py`.

**`app.py`**



## Что вам следует изучить дальше?

Следующие руководства охватывают смежные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}