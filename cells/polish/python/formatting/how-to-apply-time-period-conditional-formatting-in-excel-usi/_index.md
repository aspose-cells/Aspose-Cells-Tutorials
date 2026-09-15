---
category: general
date: 2026-09-15
description: Dowiedz się, jak zastosować formatowanie warunkowe dla przedziału czasu
  i zapisać skoroszyt jako XLSX przy użyciu Aspose.Cells w Pythonie. Zawiera kod krok
  po kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: pl
lastmod: 2026-09-15
og_description: Zastosuj formatowanie warunkowe okresu czasu w Excelu przy użyciu
  Pythona i zapisz skoroszyt jako XLSX. Przejrzyj ten kompletny przewodnik dla Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Zastosuj formatowanie warunkowe okresu czasu w Excelu przy użyciu Pythona
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Jak zastosować formatowanie warunkowe okresu czasu w Excelu przy użyciu Pythona
url: /pl/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zastosować formatowanie warunkowe oparte na przedziale czasowym w Excelu przy użyciu Pythona

Jeśli potrzebujesz **formatowania warunkowego opartego na przedziale czasowym** w pliku Excel, ten samouczek pokaże Ci dokładnie, jak to zrobić w Pythonie. Zobaczysz kompletny, gotowy do uruchomienia przykład, który tworzy skoroszyt, podświetla wczorajsze daty i **zapisuje skoroszyt jako XLSX** w zaledwie kilku linijkach kodu.

Formatowanie warunkowe to potężny sposób na zwrócenie uwagi na dane spełniające określoną regułę. W tym przewodniku koncentrujemy się na przedziale czasowym „Yesterday”, ale ten sam schemat działa dla innych wbudowanych okresów, takich jak Today, LastWeek i NextMonth. Po zakończeniu samouczka będziesz w stanie tworzyć skrypty w stylu **how to create excel workbook python**, gotowe do produkcji.

## Wymagania wstępne

- Python 3.8+ zainstalowany  
- pakiety `aspose-cells` i `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Podstawowa znajomość składni Pythona  

Nie jest wymagana dodatkowa instalacja Office, ponieważ Aspose.Cells obsługuje generowanie plików wewnętrznie.

## Formatowanie warunkowe oparte na przedziale czasowym przy użyciu Aspose.Cells w Pythonie

Ta sekcja przechodzi przez każdą linię kodu potrzebną do wykonania podstawowego zadania. Poniższy blok kodu to pełny skrypt; komentarze wyjaśniają cel każdego kroku.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Dlaczego każdy krok ma znaczenie

1. **Creating the workbook** daje Ci plik Excel w pamięci, który możesz modyfikować bez otwierania Excela.  
2. **Defining the range** (`I19:K20`) informuje Aspose.Cells, gdzie ma zastosowanie reguła, utrzymując logikę odizolowaną.  
3. **Adding a TIME_PERIOD condition** używa wbudowanej enumeracji Aspose `TimePeriodType.YESTERDAY`. To eliminuje ręczne obliczenia dat i automatycznie aktualizuje się, gdy plik zostanie otwarty w innym dniu.  
4. **Setting the style** (`background_color` i `pattern`) określa, jak wyglądają podświetlone komórki. Użycie `Color.pink` sprawia, że reguła jest łatwa do zauważenia.  
5. **Writing sample dates** z formatem liczbowym 30 zapewnia, że Excel wyświetla je jako krótkie daty, a nie jako liczby seryjne.  
6. **Auto‑fitting the column** poprawia czytelność dla każdego, kto otworzy plik później.  
7. **Saving as XLSX** tworzy szeroko kompatybilny plik, który może być otwarty w Excelu, Google Sheets lub dowolnym nowoczesnym programie arkuszy kalkulacyjnych.

## Jak tworzyć skoroszyt Excel w stylu Python przy użyciu Aspose.Cells

Powyższy skrypt już demonstruje minimalne kroki do **how to create excel workbook python**. W praktyce możesz chcieć:

- Dodać wiele arkuszy (`workbook.worksheets.add("Report")`).  
- Wypełnić duże tabele danych przy użyciu pętli lub pandas DataFrames (`worksheet.cells.import_data_table`).  
- Zastosować dodatkowe formatowanie (czcionki, obramowania) używając `cell.get_style()`.

Wszystkie te działania podążają tym samym schematem: uzyskać obiekt, zmodyfikować jego właściwości i wywołać `set_style` lub `save`.

## Dodawanie formatowania warunkowego w Python – inne przydatne wzorce

Poza przykładem „Yesterday”, Aspose.Cells obsługuje kilka typów formatowania warunkowego:

| FormatConditionType | Typowy przypadek użycia |
|---------------------|--------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Niestandardowe formuły (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Proste porównania (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Skale kolorów gradientowych |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Wizualizacja pasków w komórce |

Aby **add conditional formatting python** dla progowego wartości numerycznej, należy zamienić `FormatConditionType.TIME_PERIOD` na `FormatConditionType.CELL_VALUE` oraz ustawić `condition.operator_type` i `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Zapisz skoroszyt jako XLSX – najlepsze praktyki

Podczas **save workbook as xlsx**, rozważ:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) aby uniknąć przestarzałych formatów.  
- **Using a deterministic file name** jeśli skrypt działa w pętli (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) w długotrwale działających usługach, aby zwolnić pamięć natywną.  

Przykład już używa `SaveFormat.XLSX`, co tworzy nowoczesny, oparty na zipie skoroszyt, który zachowuje wszystkie reguły formatowania warunkowego.

## Podświetlenie wczoraj w Excelu – kroki weryfikacji

Po uruchomieniu skryptu otwórz `TimePeriodExample.xlsx`:

1. Komórki `I19` i `K20` zawierają daty `30‑07‑2008` i `03‑08‑2008`.  
2. Komórka `I20` wyświetla tekst „Yesterday”.  
3. Jeśli zmienisz datę systemową na **30 lipca 2008** i ponownie otworzysz plik, komórki z pasującymi datami zostaną automatycznie wypełnione różowym kolorem.  
4. Zmiana daty systemowej na inny dzień usuwa różowe wypełnienie, potwierdzając, że reguła reaguje na logikę **time period conditional formatting**.

## Częste pułapki i jak ich unikać

- **Missing `aspose-pydrawing`** – klasa `Color` znajduje się w tym pakiecie; zapomnienie o jej instalacji powoduje `ImportError`.  
- **Incorrect number format** – użycie domyślnego formatu General wyświetla liczby seryjne (np. 39822). Zawsze ustaw `style.number = 30` dla krótkich dat.  
- **Range mismatch** – zakres formatowania warunkowego musi obejmować komórki, które chcesz podświetlić; w przeciwnym razie reguła nie ma efektu.

## Pro tip: ponowne użycie procedury formatowania

Jeśli potrzebujesz tej samej reguły „Yesterday” w wielu skoroszytach, opakuj logikę w funkcję pomocniczą:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Wywołaj `apply_yesterday_highlight(worksheet, "A1:A10")` w dowolnym miejscu, gdzie jest potrzebne.

## Podsumowanie

Ten przewodnik pokazał, jak zaimplementować **time period conditional formatting** w Excelu przy użyciu Pythona, jak **save workbook as XLSX**, oraz jak **highlight yesterday in Excel** przy użyciu jednego, wielokrotnego użycia skryptu. Masz teraz solidne podstawy do **add conditional formatting python** kodu w każdym projekcie automatyzacji, niezależnie od tego, czy generujesz codzienne raporty, tworzysz pulpity nawigacyjne, czy przygotowujesz eksport danych.

**Kolejne kroki**

- Zbadaj inne wartości `TimePeriodType`, takie jak `TODAY` lub `LAST_WEEK`.  
- Połącz wiele reguł warunkowych na tym samym zakresie, aby uzyskać bogatsze wskazówki wizualne.  
- Zintegruj generowanie skoroszytu z usługą webową lub zadaniem cyklicznym.

Miłego kodowania i ciesz się wizualną przejrzystością, jaką formatowanie warunkowe wnosi do Twojej automatyzacji Excela!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Mistrzowskie formatowanie warunkowe w Excelu przy użyciu Aspose.Cells .NET : Kompletny przewodnik](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Mistrz Aspose.Cells .NET : Zastosuj formatowanie warunkowe do alternatywnych wierszy w Excelu](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Mistrz formatowania warunkowego z własnymi czcionkami w Excelu przy użyciu Aspose.Cells dla .NET i C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}