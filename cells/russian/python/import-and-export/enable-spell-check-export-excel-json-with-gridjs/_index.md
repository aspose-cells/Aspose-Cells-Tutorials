---
category: general
date: 2026-06-21
description: Включите проверку орфографии при экспорте Excel в JSON с помощью GridJs.
  Узнайте, как преобразовать xlsx в JSON, настроить ленивую загрузку и эффективно
  загрузить рабочую книгу Excel.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: ru
og_description: Включите проверку орфографии при экспорте Excel JSON с помощью GridJs.
  Это руководство показывает, как преобразовать xlsx в JSON, настроить ленивую загрузку
  и загрузить книгу Excel.
og_title: Включить проверку орфографии и экспортировать Excel JSON с GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Включить проверку орфографии и экспорт Excel JSON с GridJs
url: /ru/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Включить проверку орфографии и экспортировать Excel JSON с помощью GridJs

Когда‑нибудь вам нужно было **включить проверку орфографии** в веб‑интерфейсе таблицы и вы задавались вопросом, как одновременно получить данные в виде JSON? Вы не одиноки. Многие разработчики сталкиваются с тем же, когда пытаются **экспортировать Excel JSON** из рабочей книги, сохраняя такие продвинутые функции, как проверка формул.

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет, как **загрузить Excel workbook**, превратить его в JSON‑payload с помощью GridJs, **настроить отложенную загрузку** и, конечно, **включить проверку орфографии**. К концу вы сможете **конвертировать xlsx в JSON** всего в несколько строк — без загадок и недостающих частей.

> **Что вы получите**  
> * Скрипт на Python, который читает файл `.xlsx`, создает объект сервера GridJs и записывает `grid_data.json`.  
> * Понимание, почему каждый параметр важен (проверка орфографии, проверка формул, отложенная загрузка).  
> * Советы по масштабированию решения для больших рабочих книг.

---

## Предварительные требования

Перед тем как начать, убедитесь, что на вашей машине установлено следующее:

| Требование | Почему это важно |
|-------------|----------------|
| Python 3.9+ | Требуется для пакета `cells`, используемого ниже. |
| `cells` library (`pip install cells`) | Предоставляет классы `Workbook` и `GridJs`. |
| Пример Excel‑файла (`sample.xlsx`) | Это источник, из которого мы будем **загружать Excel workbook**. |
| Права записи в папку вывода | Необходимо для шага `grid.save()`. |

Если что‑то из этого вам незнакомо, сначала установите необходимые компоненты — иначе скрипт выдаст ошибку импорта.

---

## Шаг 1: Загрузить Excel Workbook

Самое первое, что нужно сделать, когда вы хотите **конвертировать xlsx в json**, — открыть рабочую книгу. Представьте это как открытие двери перед тем, как начать обставлять комнату.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tip:** Если ваш файл огромный, рассмотрите возможность использования `cells.Workbook(..., read_only=True)`, чтобы снизить потребление памяти.

---

## Шаг 2: Создать объект сервера GridJs

Теперь, когда рабочая книга находится в памяти, нам нужен объект **GridJs**, который преобразует листы в JSON, пригодный для потребления клиентским UI.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Переменная `grid` по сути является тонкой оболочкой вокруг рабочей книги, умеющей сериализовать ячейки, формулы и даже информацию о стилизации.

---

## Шаг 3: Включить проверку орфографии (и проверку формул)

Здесь ключевое слово проявляет свою силу. Переключив флаг `enableSpellCheck`, вы предоставляете конечным пользователям страховочную сетку от опечаток — так же, как в настольном Excel.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Почему включать оба? Проверка орфографии ловит текстовые ошибки, а проверка формул защищает от сломанных вычислений. Вместе они делают веб‑UI таким же отполированным, как нативный опыт Excel.

---

## Шаг 4: Настроить отложенную загрузку

Если вы работаете с тысячами строк, отправка всего набора данных одним payload‑ом перегрузит браузер. **Настройте отложенную загрузку**, чтобы передавать данные небольшими порциями (по 500 строк за запрос в нашем примере).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Вы можете подкорректировать `pageSize` в зависимости от условий сети. Меньшие страницы означают больше запросов, но более плавный UI; большие страницы уменьшают количество вызовов, но могут вызвать задержки.

---

## Шаг 5: Экспортировать Excel JSON

Все тяжёлые операции теперь происходят «за кулисами». Финальный акт — **экспортировать excel json** в файл, который ваш фронтенд сможет запросить.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Когда метод `save` завершится, у вас будет аккуратный `grid_data.json`, содержащий:

* Имена листов и их ID  
* Данные строк (значения, формулы и форматирование)  
* Метаданные о включенных функциях (проверка орфографии, отложенная загрузка и т.д.)

Вы можете проверить вывод, открыв файл в текстовом редакторе или загрузив его в консоль браузера:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Это **полное, автономное решение** для преобразования Excel‑файла в JSON‑payload при сохранении проверки орфографии.

---

## Полный скрипт — собрать всё вместе

Ниже представлен весь код программы, который можно скопировать, скорректировать пути и запустить. Никаких скрытых шагов, никаких внешних скриптов — только один файл.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Сохраните его как `export_gridjs.py` и запустите:

```bash
python export_gridjs.py
```

Вы должны увидеть серию сообщений `[✓]`, подтверждающих успешное выполнение каждого шага.

---

## Часто задаваемые вопросы и особые случаи

**Что если моя рабочая книга содержит несколько листов?**  
GridJs автоматически перебирает каждый лист, поэтому результирующий JSON будет содержать массив `sheets`. При необходимости вы можете отфильтровать его на клиенте, если нужен только подмассив.

**Можно ли отключить проверку орфографии для конкретного листа?**  
Словарь `options` применяется глобально. Чтобы переключать её по листу, понадобится создавать отдельные объекты `GridJs` или пост‑обрабатывать полученный JSON.

**Мой файл больше 10 МБ — поможет ли отложенная загрузка?**  
Абсолютно. Отложенная загрузка работает на уровне API; сервер отдает только запрошенную страницу. При низкой задержке сети можно увеличить `pageSize` до 1000.

**Нужно ли беспокоиться о Unicode‑символах?**  
`cells` из коробки поддерживает UTF‑8, поэтому такие символы, как эмодзи или нелатинские скрипты, сохраняются при передаче.

---

## Pro Tips для продакшна

* **Кешировать JSON** — если рабочая книга меняется редко, кешируйте `grid_data.json` в CDN для молниеносной загрузки.  
* **Безопасность** — никогда не раскрывайте исходный файл Excel; отдавайте только сгенерированный JSON.  
* **Версионирование** — включайте номер версии в имя файла JSON (например, `grid_data_v2.json`), чтобы избежать устаревших данных после обновлений.  
* **Тестирование** — напишите небольшой unit‑test, который загружает JSON и проверяет, что `enableSpellCheck` равно `true`. Это позволяет быстро обнаружить регрессии.

---

## Заключение

Теперь у вас есть надёжный, сквозной рецепт, позволяющий **включить проверку орфографии**, пока вы **экспортируете Excel JSON** с помощью GridJs. От **загрузки excel workbook** до **настройки отложенной загрузки** и, наконец, **конвертации xlsx в json** процесс прост и готов к продакшну.

Следующие шаги? Попробуйте подключить сгенерированный `grid_data.json` к простой HTML‑странице, использующей клиентскую библиотеку GridJs, поэкспериментировать с пользовательскими рендерерами ячеек или добавить аутентификацию вокруг JSON‑эндпоинта. Возможности безграничны, когда вы комбинируете проверку орфографии, отложенную загрузку и бесшовную конверсию Excel‑в‑JSON.

Есть дополнительные вопросы или «упрямый» файл, с которым не справляетесь? Оставьте комментарий ниже, и happy coding!  

---

![Enable spell check in GridJs](/images/enable-spell-check-gridjs.png "Screenshot showing spell check enabled in GridJs UI")

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы реализации в ваших проектах.

- [Экспортировать Excel в JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Импортировать JSON‑данные в Excel с помощью Aspose.Cells Java: Полное руководство](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Как эффективно фильтровать данные при загрузке Excel‑рабочих книг с помощью Aspose.Cells в Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}