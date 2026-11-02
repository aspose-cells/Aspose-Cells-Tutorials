---
category: general
date: 2026-10-07
description: Utwórz skoroszyt Excel w Pythonie, ustaw kolor tła komórki, automatycznie
  dopasuj szerokość kolumn i wypełnij daty w Excelu przy użyciu zwięzłego przykładu
  kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: pl
lastmod: 2026-10-07
og_description: Utwórz skoroszyt Excel w Pythonie, następnie ustaw kolor tła komórek,
  automatycznie dopasuj szerokość kolumn i wypełnij daty w Excelu. Postępuj zgodnie
  z tym przewodnikiem krok po kroku, aby wygenerować plik TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Utwórz skoroszyt Excel w Pythonie – ustaw tło i automatyczne dopasowanie
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Utwórz skoroszyt Excela w Pythonie i ustaw tło komórki
url: /pl/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w Pythonie i ustaw tło komórki

Utwórz skoroszyt Excel w Pythonie i zastosuj formatowanie warunkowe przy użyciu zaledwie kilku linii kodu. Ten samouczek pokazuje **jak tworzyć excel** programowo, ustawia kolor tła komórki, automatycznie dopasowuje szerokość kolumn w Excelu oraz wstawia daty w Excelu przy użyciu biblioteki Aspose.Cells.

Nauczysz się:
* Zainicjalizować skoroszyt i uzyskać pierwszy arkusz.  
* Zdefiniować format warunkowy, który podświetla daty „Wczoraj”.  
* Wstawić przykładowe daty do określonych komórek.  
* Automatycznie dopasować kolumny, aby dane były wyraźnie widoczne.  
* Zapisać skoroszyt w wybranym folderze.

Jedynym wymogiem wstępnym jest działające środowisko Python 3 z zainstalowanymi pakietami `aspose-cells` i `aspose-pydrawing`:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Utwórz skoroszyt Excel w Pythonie – krok po kroku

Poniższe sekcje dzielą proces na łatwe do zarządzania kroki. Każdy krok zawiera wymaganą część kodu, wyjaśnienie **dlaczego** jest to istotne oraz wskazówkę, jak uniknąć typowych pułapek.

### Krok 1: Importuj wymagane przestrzenie nazw i zdefiniuj funkcję pomocniczą

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: Importowanie właściwych klas daje dostęp do tworzenia skoroszytu, formatowania warunkowego i obsługi kolorów.  
**Pro tip**: Trzymaj importy na początku pliku; ułatwia to czytanie skryptu i zapobiega błędom cyklicznych importów.

### Krok 2: Utwórz skoroszyt i pobierz pierwszy arkusz

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Konstruktor `Workbook()` tworzy pusty skoroszyt Excel w pamięci.  
**Why**: Rozpoczęcie od nowego skoroszytu zapewnia brak pozostałego formatowania z poprzednich uruchomień.

### Krok 3: Ustaw kolor tła komórki przy użyciu formatu warunkowego

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Why*: Użycie warunku **time period** automatycznie podświetla każdą komórkę zawierającą datę wczorajszą, eliminując ręczne sprawdzanie dat.  
**Tip**: `Color.pink` to tylko przykład; możesz użyć dowolnego obiektu `Color` (`Color.yellow`, `Color.light_green` itp.).

### Krok 4: Wstaw daty w Excelu

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Tutaj **wstawiamy daty w Excelu** w komórki `I19` i `K20`. Pierwsza data uruchomi formatowanie warunkowe, natomiast druga nie.  
**Why this matters**: Pokazanie zarówno dopasowanych, jak i nie‑dopasowanych wartości pomaga zweryfikować, że reguła działa zgodnie z oczekiwaniami.

### Krok 5: Automatycznie dopasuj kolumny w Excelu dla lepszej widoczności

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` dostosowuje szerokość kolumny na podstawie najdłuższej wartości w komórce.  
**Tip**: Wywołaj to po zapisaniu wszystkich danych; w przeciwnym razie szerokość może być obliczona na podstawie niekompletnej zawartości.

### Krok 6: Zapisz skoroszyt

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Zapisanie pliku zapisuje skoroszyt z pamięci na dysk w nowoczesnym formacie XLSX.  

### Pełny skrypt – połączenie wszystkiego razem

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Otwórz wygenerowany plik w Excelu – komórki `I19:K20` będą miały różowe tło dla daty przypadającej na „Wczoraj”, a kolumna L będzie wystarczająco szeroka, aby wyświetlić etykietę bez obcinania.

---

## Dlaczego to podejście działa najlepiej

* **Single‑pass workflow** – Wszystkie operacje odbywają się na tej samej instancji `Workbook`, co eliminuje niepotrzebny I/O.  
* **Conditional formatting** – Użycie `FormatConditionType.TIME_PERIOD` pozwala Excelowi obsługiwać logikę dat, co jest bardziej niezawodne niż pisanie własnych sprawdzeń dat w Pythonie.  
* **Explicit styling** – Ustawienie `background_color` i `pattern` zapewnia spójny wygląd we wszystkich wersjach Excela.  
* **Auto‑fit po danych** –  

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel w Pythonie – Pełny przewodnik](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Utwórz skoroszyt Excel w Pythonie – Kompletny przewodnik krok po kroku](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Utwórz skoroszyt Excel w Pythonie – Kompletny przewodnik z Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}