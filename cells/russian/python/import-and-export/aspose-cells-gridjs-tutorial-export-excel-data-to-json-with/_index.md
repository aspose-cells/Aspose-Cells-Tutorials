---
category: general
date: 2026-07-03
description: Учебник Aspose Cells GridJs, показывающий, как экспортировать данные
  Excel в JSON и экспортировать лист в JSON эффективно с использованием ленивой загрузки.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: ru
og_description: Учебник Aspose Cells GridJs объясняет, как экспортировать данные Excel
  в JSON и экспортировать лист в JSON с отложенной загрузкой для больших электронных
  таблиц.
og_title: Учебник Aspose Cells GridJs – Экспорт данных Excel в JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Учебник Aspose Cells GridJs – Экспорт данных Excel в JSON с ленивой загрузкой
url: /ru/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs tutorial – Экспорт данных Excel в JSON с отложенной загрузкой

Задумывались ли вы когда‑нибудь, как **export Excel data JSON** из огромной таблицы, не перегружая браузер? В этом руководстве Aspose Cells GridJs мы пройдем полный, готовый к запуску пример, который позволяет **export worksheet to JSON** с использованием отложенной загрузки, так что запрашиваются только необходимые строки.

Если вы боретесь с огромными файлами `.xlsx`, и клиентская часть постоянно зависает, вы не одиноки. Хорошая новость? Подход, который мы рассматриваем здесь, лёгок и масштабируем, и вы можете внедрить его в любой проект на Python, уже использующий библиотеку Aspose.Cells.

## Что будет рассмотрено в этом руководстве

За несколько минут вы узнаете, как:

1. Загрузить большую книгу (workbook) с помощью Aspose.Cells.
2. Включить отложенную загрузку GridJs, чтобы сервер передавал строки порциями.
3. Экспортировать конфигурацию GridJs в JSON‑файл, который может использовать фронтенд.
4. Настроить размер порции (chunk size) для оптимальной производительности.
5. Проверить результат и интегрировать его с простой HTML‑страницей.

Никаких внешних сервисов, никакой скрытой магии — только чистый Python и API Aspose.Cells. К концу вы получите **complete export worksheet to JSON** конвейер, который можно адаптировать под дашборды, инструменты отчётности или любой компонент data‑grid.

### Требования

- Python 3.8+ установлен локально.
- `asposecells` пакет (можно установить командой `pip install aspose-cells`).
- Большой Excel‑файл (например, `large-data.xlsx`), размещённый в известной директории.
- Базовые знания Python и концепций веб‑разработки.

Если что‑то из этого вам незнакомо, не паникуйте — каждый шаг включает короткое объяснение «почему», чтобы вы понимали логику кода.

---

## Шаг 1: Установить и импортировать Aspose.Cells

Прежде всего, нам нужна библиотека Aspose.Cells. Это коммерческий продукт, но бесплатная пробная версия подходит для разработки.

```bash
pip install aspose-cells
```

Теперь импортируйте необходимые классы в ваш скрипт.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Почему это важно:** Импорт `Workbook` даёт доступ к высокопроизводительному движку, который читает Excel‑файлы напрямую в память, обходя более медленный подход `openpyxl`.

## Шаг 2: Загрузить книгу, содержащую большой набор данных

Когда библиотека готова, укажите ей ваш Excel‑файл. Путь может быть абсолютным или относительным; просто убедитесь, что файл существует.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Совет:** Если ваша книга превышает несколько сотен мегабайт, рассмотрите возможность увеличения лимита памяти процесса Python или используйте 64‑битный интерпретатор, чтобы избежать `MemoryError`.

## Шаг 3: Включить отложенную загрузку GridJs

GridJs — это JavaScript‑компонент сетки от Aspose. Отложенная загрузка заставляет сервер отправлять только подмножество строк — идеально для огромных листов.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Почему отложенная загрузка?** Без неё весь лист будет сериализован в JSON за один раз, что легко превысит ограничения памяти браузера. Установив `LazyLoadingChunkSize` в 500, каждый запрос будет передавать управляемый объём данных.

## Шаг 4: Экспортировать конфигурацию GridJs в JSON

Теперь мы просим Aspose создать JSON, который ожидает фронтенд‑компонент GridJs. Это ядро операции **export excel data json**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Метод `ExportGridJsJson` возвращает объект `bytes`, содержащий JSON‑представление листа, готовый к сохранению или потоковой передаче.

## Шаг 5: Записать JSON в файл (или передать в поток)

Для быстрой проверки запишите JSON на диск. В продакшн‑API вы бы возвращали его напрямую из эндпоинта Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Что вы увидите:** Открыв `lazygrid.json`, вы увидите структуру с `columns`, `rows` и метаданными пагинации. Массив `rows` будет изначально пустым; GridJs запросит первую порцию при загрузке страницы.

## Шаг 6: Подключить JSON к простой HTML‑странице (опционально)

Если хотите увидеть сетку в действии, создайте небольшую HTML‑страницу, которая загружает GridJs из CDN и указывает на сгенерированный JSON.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Зачем это нужно?** Это демонстрирует полный цикл: Python создаёт JSON, браузер получает его, а GridJs отрисовывает данные порциями. Теперь вы можете экспериментировать с различными значениями `LazyLoadingChunkSize`, чтобы найти оптимальный вариант для вашей сети.

## Шаг 7: Проверка и устранение неполадок

Запустите Python‑скрипт:

```bash
python export_lazy_grid.py
```

Вы должны увидеть сообщение об успехе и файл `lazygrid.json`. Откройте HTML‑файл в браузере; сетка должна сразу отобразить первые 500 строк, с элементами управления пагинацией для загрузки остальных.

Если сетка появляется пустой:

- **Проверьте размер JSON‑файла** — файл нулевого размера обычно означает, что путь к книге указан неверно.
- **Убедитесь, что отложенная загрузка включена** — флаг `LazyLoading` должен быть `True`.
- **Проверьте консоль браузера** — любые ошибки CORS или 404 указывают, что JSON не обслуживается корректно.

---

## Распространённые варианты и граничные случаи

### Экспорт конкретного листа

В примере выше всегда используется первый лист (`Worksheets[0]`). Чтобы экспортировать другой лист, просто измените индекс или используйте имя листа:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Изменение размера порции для массивных файлов

Для файлов с миллионами строк размер порции 500 может быть всё ещё слишком мал, вызывая множество запросов. Вы можете увеличить его до 2000 и более, но помните, что большие порции потребляют больше пропускной способности за запрос.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Экспорт в поток вместо файла

Если ваш API возвращает JSON напрямую, запись на диск не требуется:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Обработка формул и форматирования

По умолчанию `ExportGridJsJson` включает вычисленные значения формул. Если нужны сырые формулы, установите:

```python
grid_options.ExportFormulas = True
```

---

## Заключение

В этом **Aspose Cells GridJs tutorial** мы рассмотрели всё, что нужно для **export Excel data JSON** и **export worksheet to JSON** с отложенной загрузкой. От установки Aspose.Cells, включения отложенной загрузки, генерации JSON до подключения его к простой HTML‑странице — теперь у вас есть полно‑стековый шаблон, который элегантно масштабируется с массивными таблицами.

Попробуйте — измените размер порции, укажите другие листы или интегрируйте эндпоинт в приложение Flask или Django. Возможности безграничны, а прирост производительности мгновенный.

Готовы к следующему шагу? Попробуйте добавить сортировку столбцов, пользовательские рендереры ячеек или даже серверную фильтрацию, чтобы сделать вашу сетку GridJs действительно интерактивной. Если возникнут проблемы, оставьте комментарий ниже; счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Импорт JSON‑данных в Excel с помощью Aspose.Cells Java: Полное руководство](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Загрузка CSV и экспорт в JSON с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Экспорт данных Excel с помощью Aspose.Cells .NET: Полное руководство для бесшовного экспорта данных](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}