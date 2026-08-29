---
category: general
date: 2026-06-30
description: Добавьте пользовательское контекстное меню в сетку Excel на Python и
  запишите значение в ячейку Excel при сохранении обновлённого файла. Узнайте, как
  создать меню правой кнопки мыши и обновить значение ячейки в стиле Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: ru
og_description: Добавьте пользовательское контекстное меню в Python, чтобы записать
  значение в ячейку Excel и сохранить обновлённый файл Excel. Это руководство проведёт
  вас через создание меню правой кнопки мыши с помощью GridJs.
og_title: Добавление пользовательского контекстного меню в Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Добавление пользовательского контекстного меню в Python — Полное руководство
url: /ru/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить пользовательское контекстное меню в Python – Полное руководство

Когда‑нибудь задумывались, как **добавить пользовательские пункты контекстного меню** в таблицу, которую вы обслуживаете из Python? Возможно, вам нужна быстрая кнопка «Отметить как проверенное», которая появляется при правом клике по ячейке, записывает значение в ячейку Excel и сохраняет обновлённую книгу — всё без выхода из веб‑интерфейса.  

В этом руководстве мы построим именно это: **пользовательское меню правой кнопки мыши**, работающего на GridJs, серверный обработчик, который **записывает значение в ячейку Excel**, и финальный шаг, который **сохраняет обновлённый файл Excel** на диск. К концу вы получите переиспользуемый шаблон, который можно вставить в любой проект на Flask, FastAPI или Django.

> **Зачем это нужно?**  
> Добавление пользовательского контекстного меню упрощает процессы проверки данных, уменьшает количество ручного копирования‑вставки и даёт конечным пользователям ощущение нативного интерфейса прямо внутри сетки. Плюс вы увидите, как **обновлять значение ячейки в стиле python**, что является базовым навыком любой автоматизации Excel.

## Предварительные требования

- Python 3.9+ (код также работает на 3.10)  
- `openpyxl` для работы с файлами Excel  
- Обёртка `gridjs` для Python (или JS‑библиотека, если предпочитаете фронтенд)  
- Базовый веб‑фреймворк (в примере используется Flask)  
- Файл книги `sample.xlsx` в папке проекта  

Если чего‑то не хватает, выполните:

```bash
pip install openpyxl flask gridjs
```

Теперь погрузимся в детали.

---

## Шаг 1 – Добавить пользовательское контекстное меню: инициализировать GridJs и привязать лист

Первое, что нужно сделать, — создать экземпляр `GridJs` и указать ему лист, с которым вы будете работать. Здесь впервые появляется фраза **add custom context menu** в нашем коде, и она задаёт основу для всего остального.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Что происходит?**  
`grid.set_worksheet(ws)` сообщает GridJs использовать данные из `ws` в качестве источника. С этого момента любые изменения контекстного меню будут автоматически применяться к тому же листу, поддерживая синхронность UI и файла.

> **Совет:** Открывайте книгу в режиме чтения/записи только один раз. Многократное открытие внутри обработчика запросов может вызвать блокировку файла в Windows.

---

## Шаг 2 – Записать значение в ячейку Excel: определить действие для пункта меню

Теперь, когда сетка готова, нам нужно **write value to excel cell**, когда пользователь выбирает нашу пользовательскую команду. Добавим пункт меню «Mark as Reviewed» и зададим ему идентификатор `markReviewed`. Идентификатор — это то, что клиент‑side JavaScript отправит обратно на сервер.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Зачем нужен пользовательский идентификатор?**  
Идентификатор отделяет текст UI от серверной логики, позволяя менять подпись без правки кода бэкенда. Он также делает операцию **create right‑click menu** явной и переиспользуемой.

---

## Шаг 3 – Создать меню правой кнопки: зарегистрировать обработчик на сервере

С пунктом меню на месте, нужно сообщить GridJs, что делать при его нажатии. Здесь реализуется функциональность **create right‑click menu**, которая действительно отправляет запрос обратно в Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Несколько замечаний:

1. **`ws[cell_address] = "Reviewed"`** — самый простой способ **update cell value python**. Под капотом `openpyxl` преобразует адрес в стиле A1 в индексы строки/столбца.  
2. Обработчик возвращает небольшой JSON. GridJs ожидает индикатор статуса; при необходимости можно добавить сообщения об ошибках.

Теперь привязываем идентификатор к обработчику:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Что если ячейка пуста или защищена?**  
- Пустые ячейки обрабатываются без проблем — `openpyxl` создаст их «на лету».  
- Для защищённых листов сначала нужно снять защиту (`ws.protection.sheet = False`) или отловить `PermissionError`.

---

## Шаг 4 – Обновить значение ячейки в Python: зафиксировать изменение, сохранив книгу

Записать значение — это только половина истории; необходимо **save updated excel file**, чтобы изменение сохранилось после завершения сеанса. Здесь мы завершаем цикл от UI к диску.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Зачем отдельная папка?**  
Сохранение в директорию `output/` оставляет оригинальный шаблон нетронутым, что удобно для аудита. Подгоните путь под свою среду развертывания.

> **Внимание:** При обслуживании множества одновременных пользователей рекомендуется использовать потокобезопасный замок (`threading.Lock`) вокруг `wb.save()`, чтобы избежать гонок.

---

## Шаг 5 – Сгенерировать JSON конфигурации клиента и собрать всё вместе

Наконец, нужно сформировать JSON, который будет потреблять фронтенд‑instance GridJs. Этот JSON содержит данные листа **и** определение пользовательского меню.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Когда вы вставите `config_json` в HTML‑страницу, GridJs отобразит сетку с пунктом «Mark as Reviewed», доступным по правому клику на любой ячейке.

### Полный пример на Flask

Ниже минимальное Flask‑приложение, которое собирает все части вместе. Запустите его, откройте `http://localhost:5000` и правой кнопкой мыши кликните любую ячейку, чтобы увидеть пользовательское меню в действии.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Ожидаемый результат:**  
- Правый клик по любой ячейке → появляется «Mark as Reviewed».  
- Клик → содержимое ячейки меняется на «Reviewed».  
- Книга `output/sample-updated.xlsx` теперь содержит новое значение.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что если нужно несколько пользовательских действий?* | Просто добавьте больше объектов в `grid.settings.context_menu.custom_items` и зарегистрируйте каждый с собственным идентификатором. |
| *Можно ли передать дополнительные данные (например, ID строки) в обработчик?* | Да. Добавьте дополнительные ключи в JSON‑payload на клиенте, затем прочитайте их из `request` в `on_custom_command`. |
| *Совместим ли этот подход с асинхронными фреймворками?* | Абсолютно — просто сделайте `on_custom_command` асинхронной функцией и используйте `await wb.save(...)`, если переключаетесь на `aiofiles` или аналог. |
| *Как стилизовать иконку меню?* | Укажите любое имя из Material‑Icons (`"icon": "edit"`). Фронтенд автоматически загрузит шрифт иконок. |
| *Что делать с большими книгами?* | Загружайте только нужный лист и рассматривайте потоковую загрузку строк через `openpyxl.iter_rows()`, чтобы снизить потребление памяти. |

## Что изучать дальше?

Следующие руководства охватывают смежные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}