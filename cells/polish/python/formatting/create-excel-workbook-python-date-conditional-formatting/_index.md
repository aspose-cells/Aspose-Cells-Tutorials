---
category: general
date: 2026-08-08
description: Utwórz skoroszyt Excel w Pythonie i dodaj formatowanie warunkowe oparte
  na dacie. Przewodnik krok po kroku z użyciem Aspose.Cells, aby podświetlić komórki
  z wczorajszą datą.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: pl
lastmod: 2026-08-08
og_description: Utwórz skoroszyt Excel w Pythonie przy użyciu Aspose.Cells i zastosuj
  formatowanie warunkowe oparte na dacie dla dynamicznych arkuszy kalkulacyjnych.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Tworzenie skoroszytu Excel w Pythonie – formatowanie warunkowe dat
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Utwórz skoroszyt Excel z warunkowym formatowaniem dat w Pythonie
url: /pl/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym daty

Jeśli potrzebujesz **create Excel workbook Python** i automatycznie podświetlać komórki, które pasują do określonej daty, ten tutorial pokaże Ci dokładnie, jak to zrobić. Nauczysz się stosować **conditional formatting based on date**, aby wczorajsze daty świeciły na różowo, używając biblioteki Aspose.Cells.

Poradnik przechodzi przez każdy krok — od instalacji SDK po zapisanie ostatecznego pliku .xlsx — dzięki czemu możesz skopiować‑wkleić działający przykład do własnego projektu. Nie jest wymagana żadna zewnętrzna dokumentacja; cały kod i wyjaśnienia są samodzielne.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* Python 3.8 lub nowszy zainstalowany.
* Pakiet `aspose-cells` (wrapper Pythona dla Aspose.Cells). Zainstaluj go poleceniem:
  ```bash
  pip install aspose-cells
  ```
* Podstawową znajomość Pythona oraz koncepcji Excela, takich jak arkusze i style komórek.

> **Pro tip:** Aspose.Cells działa bez konieczności instalacji Microsoft Excel, co czyni go idealnym do automatyzacji po stronie serwera.

## Step 1: Create the Excel workbook in Python

Pierwszym zadaniem jest utworzenie nowego skoroszytu i pobranie domyślnego arkusza. Ten obiekt reprezentuje cały plik Excel i zapewnia dostęp do wierszy, kolumn oraz API formatowania.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Utworzenie skoroszytu jest podstawą dla wszelkich dalszych manipulacji, niezależnie od tego, czy dodajesz dane, formuły, czy reguły formatowania.

## Step 2: Define a date‑based conditional format

Teraz dodajemy **conditional formatting based on date**. Enum `FormatConditionType.TIME_PERIOD` pozwala określić wbudowane okresy czasu, takie jak Yesterday, Today lub LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Dlaczego ten krok jest ważny: Excel ocenia warunek dla każdej komórki w zakresie. Gdy wartość komórki mieści się w określonym okresie (wczoraj), automatycznie stosowany jest styl, który przypisaliśmy.

## Step 3: Populate the range with sample dates

Aby zobaczyć regułę w działaniu, zapisujemy kilka obiektów `datetime` do docelowych komórek. Jeden z nich jest celowo ustawiony na wczorajszą datę względem wewnętrznego systemu dat w skoroszycie.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Linia `number = 30` mówi Excelowi, aby wyświetlał wartość przy użyciu standardowego krótkiego formatu daty. Możesz zmienić ten indeks na dowolny wbudowany format liczbowy, jeśli wolisz inną prezentację.

## Step 4: Adjust column width for readability

Automatyczne dopasowanie szerokości kolumny zawierającej daty ułatwia odczyt wyniku, szczególnie gdy skoroszyt jest otwierany w Excelu lub przeglądarce.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Step 5: Save the workbook to disk

Na koniec zapisz skoroszyt jako plik .xlsx. Zastąp `"YOUR_DIRECTORY"` rzeczywistą ścieżką na swoim komputerze.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Po otwarciu `TimePeriodDemo.out.xlsx` w Excelu, komórka **I19** będzie miała różowe tło, ponieważ jej wartość spełnia regułę „Yesterday”, natomiast **K20** pozostanie niezmieniona.

### Expected output

| I19 (data) | I20 (etykieta) | J19 | J20 | K19 | K20 (data) |
|------------|----------------|-----|-----|-----|------------|
| *2008‑07‑30* (różowe tło) | Yesterday | – | – | – | *2008‑08‑03* (bez formatowania) |

Różowe cieniowanie potwierdza, że **conditional formatting based on date** działa zgodnie z oczekiwaniami.

## Common variations and edge cases

| Sytuacja | Jak dostosować kod |
|----------|--------------------|
| **Highlight “Today” instead of “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Apply the rule to an entire column** | Use `worksheet.get_range("A:A").format_conditions` |
| **Use a custom date range (e.g., last 7 days)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Different background colors** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Running on Linux without a display** | Aspose.Cells is fully headless; no extra configuration required. |

## Full, runnable example

Poniżej znajduje się kompletny skrypt, który możesz uruchomić od razu (po zaktualizowaniu katalogu wyjściowego). Zawiera wszystkie importy, komentarze i podstawowe obsługi błędów.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Uruchomienie skryptu generuje plik Excel, w którym komórka „Yesterday” jest automatycznie podświetlona, demonstrując **create Excel workbook Python** połączone z **conditional formatting based on date**.

## Conclusion

Teraz wiesz, jak **create Excel workbook Python** tworzyć obiekty, definiować **date‑based conditional formatting**


## What Should You Learn Next?

Poniższe tutoriale obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz skoroszyt Excel przy użyciu Aspose.Cells w Javie: przewodnik krok po kroku](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Utwórz skoroszyt Excel z wykresami przy użyciu Aspose.Cells .NET | przewodnik krok po kroku](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Automatyzacja Excel: Utwórz skoroszyt i dodaj ListBox przy użyciu Aspose.Cells dla .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}