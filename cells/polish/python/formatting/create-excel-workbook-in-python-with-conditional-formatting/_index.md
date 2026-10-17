---
category: general
date: 2026-09-05
description: Utwórz skoroszyt Excel w Pythonie i dodaj formatowanie warunkowe, aby
  podświetlić komórki z wczorajszą datą. Poznaj pełny kod i dowiedz się, dlaczego
  każdy krok ma znaczenie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: pl
lastmod: 2026-09-05
og_description: Utwórz skoroszyt Excel w Pythonie i dodaj formatowanie warunkowe,
  aby podświetlić komórki z wczorajszą datą. Postępuj zgodnie z tym przewodnikiem
  krok po kroku, aby uzyskać pełne rozwiązanie.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Utwórz skoroszyt Excel w Pythonie – dodaj formatowanie warunkowe
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym
url: /pl/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym

Jeśli potrzebujesz **utworzyć skoroszyt Excel w Pythonie** do zadania raportowego, ten przewodnik pokazuje, jak wygenerować skoroszyt i zastosować regułę formatowania warunkowego, która podświetla wczorajsze daty. Zobaczysz dokładny kod, dlaczego każda linia istnieje oraz jak dostosować rozwiązanie do innych zakresów dat.

Formatowanie warunkowe to potężny sposób na zwrócenie uwagi na dane spełniające określony warunek. W tym samouczku używamy biblioteki Aspose.Cells dla Pythona przez .NET, która zapewnia pełne wsparcie funkcji Excela bez konieczności posiadania Microsoft Office. Po zakończeniu przewodnika będziesz mieć plik, w którym komórki w zakresie *I19:K20* stają się różowe, gdy zawierają wczorajszą datę.

## Wymagania wstępne

* Python 3.9+ zainstalowany
* `aspose-cells` pakiet (zainstaluj za pomocą `pip install aspose-cells`)
* Podstawowa znajomość składni Pythona
* Uprawnienia zapisu do katalogu, w którym zostanie zapisany skoroszyt

Kod działa na Windows, macOS i Linux, o ile dostępny jest środowisko uruchomieniowe .NET.

## Utwórz skoroszyt Excel w Pythonie

Pierwszym krokiem jest utworzenie obiektu `Workbook` i pobranie domyślnego arkusza. Ten obiekt reprezentuje cały plik Excel w pamięci.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Dlaczego to jest ważne*: `Workbook()` tworzy pusty skoroszyt z jednym arkuszem. Dostęp do `worksheets[0]` daje możliwość dodawania danych, stylów i formatowania później.

## Dodaj zakres formatowania warunkowego

Następnie definiujemy obszar, który będzie oceniany przez regułę warunkową. Zakres `I19:K20` obejmuje sześć komórek w dwóch wierszach.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Dlaczego to jest ważne*: Dodanie kolekcji formatowania warunkowego do określonego zakresu izoluje regułę, zapobiegając wpływowi na niepowiązane komórki. Spełnia to wymóg **add conditional formatting range**.

## Zdefiniuj regułę: podświetl komórki na podstawie daty

Teraz tworzymy warunek typu `TIME_PERIOD`. Powoduje to, że Excel porównuje wartość każdej komórki z określonym oknem czasowym.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Dlaczego to jest ważne*: `TIME_PERIOD` jest jedynym wbudowanym typem, który bezpośrednio obsługuje „Yesterday”, „Today”, „Last Week” itp. Ustawiając `condition.time_period` na `YESTERDAY`, reguła automatycznie ocenia wartość daty w każdej komórce względem dnia poprzedzającego bieżącą datę.

## Stylizuj komórki spełniające warunek

Formatowanie warunkowe wymaga także stylu wizualnego. Tutaj wybieramy różowe jednolite wypełnienie, aby wyróżnić pasujące komórki.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Dlaczego to jest ważne*: Obiekt stylu definiuje, jak Excel wyświetli komórki spełniające warunek. Użycie jednolitego różowego wypełnienia spełnia wymóg **highlight cells based on date** i ułatwia weryfikację wyniku.

## Wstaw przykładowe daty do oceny

Aby zobaczyć regułę w działaniu, wstawiamy dwie daty — jedną, która przypada na wczoraj, i drugą, która nie. Format `number` `30` odpowiada wbudowanemu formatowi daty `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Dlaczego to jest ważne*: Dostarczenie zarówno pasującej, jak i niepasującej daty pozwala zweryfikować, że formatowanie warunkowe działa poprawnie. Dostosuj daty do bieżącego miesiąca podczas uruchamiania skryptu lub zamień je na wartości dynamiczne.

## Zapisz skoroszyt

Na koniec zapisujemy plik na dysku. Stała `SaveFormat.XLSX` zapewnia, że wynikowy plik jest nowoczesnym plikiem Excel.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Dlaczego to jest ważne*: Zachowanie skoroszytu pozwala otworzyć go w Excelu, LibreOffice lub dowolnym przeglądarce obsługującej XLSX. Wydrukowana ścieżka potwierdza, gdzie plik został zapisany.

## Pełny skrypt

Łącząc wszystkie elementy, kompletny, gotowy do uruchomienia skrypt wygląda następująco:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Oczekiwany wynik

Po otwarciu `TimePeriodExample.xlsx`:

* Komórka **I19** ma różowe tło, ponieważ jej wartość odpowiada wczorajszemu dniu.
* Komórka **K20** zachowuje domyślne tło, ponieważ jej data jest poza okresem.
* Etykieta **„Yesterday”** znajduje się w komórce I20 dla przejrzystości.

## Typowe warianty i przypadki brzegowe

| Situation | Adjustment |
|-----------|------------|
| **Podświetl dzisiaj zamiast wczoraj** | Zmien `condition.time_period = TimePeriodType.TODAY`. |
| **Zastosuj regułę do większego obszaru** | Zaktualizuj ciąg zakresu w `add(\"I19:K20\")` na coś w stylu `\"A1:Z100\"`. |
| **Użyj innego koloru wypełnienia** | Zastąp `DrawingColor.pink` dowolnym innym `DrawingColor` (np. `DrawingColor.light_green`). |
| **Pracuj z datami dynamicznymi** | Oblicz `datetime.now() - timedelta(days=1)` dla wczoraj i zapisz tę wartość w komórkach przed zastosowaniem reguły. |

**Pro tip:** Gdy generujesz skoroszyt programowo dla wielu użytkowników, trzymaj definicję formatowania warunkowego oddzielnie od wstawiania danych. Dzięki temu możesz ponownie używać tego samego stylu w wielu arkuszach bez duplikowania kodu.

## Zweryfikuj wynik programowo (opcjonalnie)

Jeśli chcesz potwierdzić formatowanie bez otwierania Excela, możesz sprawdzić styl komórki po zapisaniu:



## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Automatyzacja Excel: Utwórz skoroszyt i dodaj ListBox przy użyciu Aspose.Cells dla .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Utwórz skoroszyt Excel i dodaj etykiety przy użyciu Aspose.Cells dla Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Automatyzacja Excel: Utwórz skoroszyt, dodaj ListBox przy użyciu Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}