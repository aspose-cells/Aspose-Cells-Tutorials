---
category: general
date: 2026-09-21
description: Dowiedz się, jak utworzyć skoroszyt Excel w Pythonie, ustawić kolor tła
  komórki oraz zastosować formatowanie warunkowe oparte na dacie przy użyciu Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: pl
lastmod: 2026-09-21
og_description: Utwórz skoroszyt Excel w Pythonie, ustaw kolor tła komórki i zastosuj
  formatowanie warunkowe oparte na dacie przy użyciu Aspose.Cells. Postępuj zgodnie
  z przewodnikiem krok po kroku.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Utwórz skoroszyt Excel w Pythonie przy użyciu formatowania warunkowego
url: /pl/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel w Pythonie z formatowaniem warunkowym

Jeśli potrzebujesz **create Excel workbook python** skryptów, które automatycznie podświetlają daty, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz, jak **ustawić kolor tła komórki**, dodać regułę „Wczoraj” i zapisać plik — wszystko przy użyciu Aspose.Cells for Python.

Praca z plikami Excel programowo często oznacza powtarzanie tej samej logiki formatowania w wielu arkuszach. Po zakończeniu tego tutorialu będziesz mieć wielokrotnego użytku wzorzec dla **excel conditional formatting python**, który możesz wstawić do dowolnego projektu.

## Prerequisites

- Python 3.8+ zainstalowany  
- pakiet `aspose-cells` (`pip install aspose-cells`)  
- Podstawowa znajomość funkcji Pythona oraz modułu datetime  

Nie są wymagane dodatkowe biblioteki; Aspose.Cells obsługuje wszystkie operacje na Excelu.

## Step 1: Create the workbook and access the first worksheet

Pierwszy krok to **create excel workbook python** obiekty i pobranie domyślnego arkusza. Daje to czyste płótno do dalszego stylizowania.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Dlaczego to ważne:* `Workbook()` tworzy plik Excel w pamięci. Dostęp do `worksheets[0]` unika twardego kodowania nazw arkuszy i działa nawet, gdy domyślna nazwa się zmieni.

## Step 2: Helper to add a TIME_PERIOD conditional format

Aby kod był schludny, opakowujemy tworzenie formatowania warunkowego w pomocniczą funkcję. Przyjmuje ona zakres komórek, kolor tła oraz żądaną regułę okresu czasu.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Dlaczego to ważne:* Pomocnik abstrahuje powtarzalne kroki tworzenia formatowania warunkowego, co ułatwia ponowne użycie dla innych reguł opartych na dacie, takich jak „Dziś” czy „Ostatni tydzień”.

## Step 3: Apply the “Yesterday” rule to a range

Teraz używamy pomocnika, aby podświetlić komórki zawierające wczorajszą datę. Zakres `I19:K20` przyjmie **medium sea green**, gdy warunek zostanie spełniony.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Dlaczego to ważne:* `TimePeriodType.YESTERDAY` jest częścią wbudowanej enumeracji Aspose.Cells, więc nie musisz ręcznie obliczać dat. Biblioteka ocenia regułę przy każdym otwarciu skoroszytu.

## Step 4: Populate the range with sample dates

Aby zobaczyć regułę w działaniu, wpisujemy dwie daty — jedną pasującą do „Wczoraj”, a drugą nie. Styl liczbowy `30` odpowiada wbudowanemu formatowi daty.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Dlaczego to ważne:* Wstawiając konkretne daty, możesz zweryfikować, że formatowanie warunkowe działa, nie musząc otwierać pliku w konkretnym dniu.

## Step 5: Add a descriptive label and auto‑fit the column

Mała etykieta wyjaśnia przeznaczenie formatowanego zakresu, a `auto_fit_column` sprawia, że arkusz jest czytelny.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Step 6: Save the workbook

Na koniec zapisujemy skoroszyt na dysku. Wywołanie `os.makedirs` zapewnia, że docelowy folder istnieje.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Po otwarciu *TimePeriodDemo.xlsx* zobaczysz:

- Komórka **I19** jest zacieniona **medium sea green**, ponieważ jej wartość spełnia regułę „Wczoraj”.  
- Komórka **K20** zachowuje domyślne tło, ponieważ jej data nie spełnia warunku.  

To demonstruje **format cells by date** przy użyciu jednej linii kodu w Pythonie.

## Full, runnable example

Łącząc wszystkie elementy, oto kompletny skrypt, który możesz skopiować i uruchomić:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Uruchom skrypt, otwórz wygenerowany plik i zobacz formatowanie warunkowe w akcji.

## Common variations and edge cases

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY` | Real‑time dashboards |
| **Multiple ranges** | Call `add_time_period` for each range, passing different colors | Complex reports |
| **Dynamic date range** | Use `TimePeriodType.LAST_7_DAYS` or `TimePeriodType.NEXT_MONTH` | Rolling reports |
| **Custom color** | Use `Color.from_argb(255, r, g, b)` to create any shade | Brand‑consistent styling |

**Pro tip:** Always set `condition.style.pattern = BackgroundType.SOLID` when you want a solid fill; otherwise Excel may display a gradient that looks inconsistent across versions.

## Conclusion

Teraz wiesz, jak **create Excel workbook python** skrypty, które **set cell background color**, stosują **excel conditional formatting python**, oraz **format cells by date** przy użyciu Aspose.Cells. Przykład obejmuje scenariusz **date based conditional formatting**, ale ten sam wzorzec działa dla dowolnej reguły okresu czasu.

Następnie możesz zbadać:

- Dodawanie pasków danych lub zestawów ikon (`FormatConditionType.DATA_BAR`)  
- Łączenie wielu reguł warunkowych w tym samym zakresie  
- Eksportowanie skoroszytu do PDF (`SaveFormat.PDF`) w celu raportowania  

Śmiało eksperymentuj z różnymi kolorami, zakresami i typami okresów czasu, aby dopasować je do swoich potrzeb raportowych. Szczęśliwego kodowania!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}