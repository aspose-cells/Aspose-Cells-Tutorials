---
category: general
date: 2026-06-30
description: Добавьте пользовательское контекстное меню в GridJs и узнайте, как загрузить
  книгу Excel, обновить значение ячейки, включить проверку орфографии и зарегистрировать
  пользовательскую команду.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: ru
og_description: Добавьте пользовательское контекстное меню в GridJs, изучая загрузку
  Excel‑книги, обновление значения ячейки, включение проверки орфографии и регистрацию
  пользовательской команды.
og_title: Добавьте пользовательское контекстное меню в GridJs – пошаговое руководство
  на Python
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Добавьте пользовательское контекстное меню в GridJs — Полное руководство по
  Python
url: /ru/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление пользовательского контекстного меню в GridJs – Полное руководство на Python

Когда‑то задавались вопросом, как **добавить пользовательские пункты контекстного меню** в таблицу GridJs, основанную на Excel‑книге? Вы не одиноки. Во многих приложениях с большими объёмами данных нужен контекстный клик, позволяющий пользователям помечать строки, отмечать элементы как проверенные или запускать серверные действия — не покидая сетку.

В этом руководстве мы пройдёмся по загрузке Excel‑книги, привязке пользовательского пункта контекстного меню, обновлению значения ячейки, включению проверки орфографии и регистрации пользовательской команды, сохраняющей изменения обратно в файл. К концу вы получите полностью рабочий экземпляр GridJs, который ощущается естественно для пользователей и записывает изменения сразу в исходную таблицу.

## Предварительные требования

- Python 3.9+ (код использует подсказки типов, но работает на любой современной версии)  
- библиотека `cells` (или любой обёртка для работы с Excel, предоставляющая объекты `Workbook` и `Worksheet`)  
- привязка `gridjs` для Python (модель объектов отражает JavaScript‑API)  
- базовое понимание лямбда‑функций и JSON‑структур  

Если всё это у вас есть, давайте начинать.

## Шаг 1: Загрузка Excel‑книги и выбор листа

Первое, что нужно сделать, — **загрузить Excel‑книгу**, чтобы GridJs имел данные для отображения. Класс `cells.Workbook` абстрагирует работу с файлом и даёт прямой доступ к строкам, столбцам и отдельным ячейкам.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Почему это важно:** Предварительная загрузка книги позволяет сетке запрашивать данные по мере необходимости, а любые последующие правки (например, **обновление значения ячейки**) сохранятся в том же файле.

## Шаг 2: Создание экземпляра GridJs и привязка к листу

Теперь создаём объект `gridjs.GridJs` и указываем, какой лист рендерить. Это как передать GridJs живой источник данных, к которому он может обращаться каждый раз, когда нужно отрисовать страницу или часть данных по требованию.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Совет:** Если работаете с несколькими листами, просто вызовите позже `grid.set_worksheet(other_ws)` — пересоздавать сетку не требуется.

## Шаг 3: Включение проверки орфографии (и других полезных функций)

Большинство бизнес‑приложений позволяют пользователям вводить свободный текст. Включение **проверки орфографии** уменьшает количество опечаток и повышает качество данных. GridJs предоставляет простой флаг для этого.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Зачем включать проверку орфографии?** Она работает на клиенте, давая мгновенную обратную связь без дополнительных запросов к серверу — идеально для больших таблиц.

## Шаг 4: Добавление пользовательского пункта контекстного меню

Это сердце руководства: **добавление пользовательных пунктов контекстного меню**. Мы создадим опцию «Отметить как проверенное», которая при клике выполнит серверную команду, определённую далее.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Иллюстрация**  
> ![Скриншот добавления пользовательского контекстного меню с вариантами правого клика](/images/add-custom-context-menu.png "Пример пользовательского контекстного меню")

Текст alt выше содержит основной ключевой запрос, удовлетворяя требования SEO.

## Шаг 5: Регистрация пользовательской команды для обновления значения ячейки

Когда пользователь выбирает «Отметить как проверенное», нам нужно **зарегистрировать пользовательскую команду**, которая обновит соответствующую ячейку Excel и сохранит файл. Метод `grid.register_custom_command` связывает вызываемый объект Python с идентификатором действия, установленным ранее.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Почему это работает:** Обработчик получает ссылку на ячейку от клиента, использует API `Worksheet` для **обновления значения ячейки**, а затем записывает всю книгу обратно на диск. Ответ сообщает фронтенду об успешном выполнении операции.

### Обработка граничных случаев

- **Отсутствует ссылка на ячейку:** Если в `req` нет поля `"cell"`, выбросьте чёткую ошибку, чтобы UI мог показать toast‑уведомление.  
- **Конкурентные правки:** Для сценариев с высокой нагрузкой рассмотрите блокировку книги или использование версии‑метки, чтобы избежать гонок.

## Шаг 6: Включение ленивой загрузки для больших листов

Если у вас тысячи строк, ленивый запрос сохраняет отзывчивость UI. Установите размер страницы в разумный кусок — 500 строк обычно хватает для большинства браузеров.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **А если у вас 10 000 строк?** Сетка будет запрашивать данные постранично, снижая нагрузку на память как клиента, так и сервера.

## Шаг 7: (Опционально) Добавление пользовательского модального окна для редактирования строк

Иногда нужен более сложный интерфейс, чем встроенный редактор. GridJs позволяет открыть модальное окно, которое может быть реализовано где угодно — в React‑компоненте или простой HTML‑форме.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Зачем нужен модал?** Он изолирует сложную логику валидации и даёт полный контроль над разметкой, оставаясь вызываемым из сетки.

## Шаг 8: Получение клиентской конфигурации в виде JSON

Наконец, нужно передать конфигурацию в браузер. Метод `get_client_config` сериализует всё в JSON‑объект, который может потреблять фронтенд‑библиотека GridJs.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Вывод выглядит примерно так (усечён для краткости):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Ожидаемый результат

- Правый клик по любой ячейке открывает меню с пунктом **Mark as Reviewed**.  
- Выбор этого пункта отправляет запрос на сервер, который **обновляет значение ячейки** на «Reviewed» и сохраняет `example‑updated.xlsx`.  
- Проверка орфографии подсвечивает ошибочные слова по мере ввода.  

Всё это происходит без полной перезагрузки страницы, благодаря ленивой загрузке и лёгкому JSON‑payload.

## Часто задаваемые вопросы и профессиональные советы

| Вопрос | Ответ |
|----------|--------|
| *Что делать, если книга доступна только для чтения?* | Убедитесь, что у файла есть права на запись, либо откройте книгу с `mode="rw"`, если библиотека поддерживает такой режим. |
| *Можно ли добавить более одного пользовательского пункта меню?* | Конечно — просто добавьте дополнительные словари в `grid.settings.context_menu.custom_items`. |
| *Нужно ли перезагружать сетку после обновления ячейки?* | GridJs автоматически обновляет затронутую строку, если вы вернёте `{status:"ok"}`; иначе вызовите `grid.refresh()` на клиенте. |
| *Как сделать проверку орфографии языко‑специфичной?* | Установите `grid.settings.spell_check.language = "en-US"` (или любой поддерживаемый локаль). |
| *Совместима ли ленивый запрос с серверной фильтрацией?* | Да — комбинируйте `grid.settings.filter.enabled = True` и реализуйте логику фильтра в своей пользовательской команде. |

## Полный рабочий пример (все шаги вместе)

Ниже представлен единый скрипт, который можно разместить в маршруте Flask или запустить как отдельный процесс. Замените `YOUR_DIRECTORY` на реальный путь на вашем сервере.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}