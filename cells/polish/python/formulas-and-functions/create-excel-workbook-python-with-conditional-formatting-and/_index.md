---
category: general
date: 2026-10-04
description: Utwórz skoroszyt Excel w Pythonie przy użyciu Aspose.Cells. Poznaj formatowanie
  warunkowe w Excelu w Pythonie, ustawianie koloru tła komórek w Pythonie oraz formatowanie
  dat w komórkach w Pythonie w pełnym przykładzie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: pl
lastmod: 2026-10-04
og_description: Utwórz skoroszyt Excel w Pythonie przy użyciu Aspose.Cells. Ten poradnik
  pokazuje warunkowe formatowanie w Excelu w Pythonie, kolor tła komórki w Pythonie
  oraz formatowanie dat w komórkach w Pythonie krok po kroku.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Tworzenie skoroszytu Excel w Pythonie – pełny przewodnik z formatowaniem
  warunkowym
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym i kolorem tła
  komórek
url: /pl/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w Pythonie z formatowaniem warunkowym i kolorem tła komórki

Jeśli potrzebujesz szybko **create Excel workbook python**, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz kompletny, gotowy do uruchomienia przykład, który dodaje **excel conditional formatting python**, zmienia **cell background color python** i **format cells date python** dla podświetlenia „Yesterday”.

W wielu scenariuszach raportowania wizualna wskazówka w postaci kolorowej komórki sprawia, że dane są od razu zrozumiałe. Ten tutorial przeprowadzi Cię przez każdy wiersz kodu, wyjaśni, dlaczego każdy krok ma znaczenie, i dostarczy gotowy do uruchomienia skrypt, który możesz dostosować do własnych projektów.

## Co osiągniesz

1. **create Excel workbook python** przy użyciu biblioteki Aspose.Cells.  
2. Zastosować **excel conditional formatting python**, które automatycznie podświetla daty przypadające na „Yesterday”.  
3. Ustawić **cell background color python** na różowy (lub dowolny inny kolor, który preferujesz).  
4. **format cells date python**, aby daty wyświetlały się w standardowym stylu daty Excela.  

Nie wymagana jest wcześniejsza znajomość Aspose.Cells — wystarczy działające środowisko Python 3 i dostęp do pip.

## Wymagania wstępne

- Zainstalowany Python 3.8 lub nowszy.  
- Pakiety `aspose-cells` i `aspose-pydrawing` zainstalowane poleceniem `pip install aspose-cells aspose-pydrawing`.  
- Podstawowa znajomość składni Pythona oraz pojęć związanych z Excelem (skoroszyty, arkusze, komórki).  

> **Pro tip:** Jeśli uruchomisz skrypt w wirtualnym środowisku, unikniesz konfliktów wersji z innymi projektami.

## Krok 1: Przygotuj projekt i zaimportuj wymagane klasy

Pierwszy krok, gdy **create Excel workbook python**, to zaimportowanie klas Aspose.Cells, które będą potrzebne. Te klasy dają bezpośredni dostęp do tworzenia skoroszytu, formatowania warunkowego i stylizacji.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Dlaczego to ważne:* Importowanie tylko niezbędnych symboli utrzymuje przestrzeń nazw w porządku i ułatwia czytanie skryptu. `Workbook` jest punktem wejścia dla **create Excel workbook python**, natomiast `FormatConditionType` i `TimePeriodType` są kluczowe dla **excel conditional formatting python**.

## Krok 2: Utwórz nowy skoroszyt i uzyskaj pierwszy arkusz

Teraz faktycznie **create Excel workbook python**. Konstruktor `Workbook()` tworzy pusty plik Excel z domyślnym arkuszem.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Wyjaśnienie:* Każdy plik Excel zaczyna się przynajmniej od jednego arkusza. Domyślnie Aspose.Cells nazywa go „Sheet1”. Możesz dodać więcej arkuszy później, ale w tym przykładzie jeden arkusz utrzymuje fokus demonstracji.

## Krok 3: Zdefiniuj docelowy zakres dla formatowania warunkowego

Formatowanie warunkowe działa na prostokątnym zakresie. Tutaj wybieramy zakres `I19:K20`, który daje trzy kolumny i dwa wiersze do pracy.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Dlaczego to robimy:* Metoda `get` zwraca obiekt `ConditionalFormatting` powiązany z określonym zakresem. Jeśli zakres nie ma jeszcze żadnego formatowania, Aspose.Cells automatycznie tworzy nową kolekcję.

## Krok 4: Dodaj warunek TIME_PERIOD i ustaw kolor tła

To jest sedno **excel conditional formatting python**. Dodajemy regułę `TIME_PERIOD`, która podświetla komórki zawierające daty przypadające na „Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Głębsze omówienie:*  
- `FormatConditionType.TIME_PERIOD` instruuje Excel, aby ocenił daty względem bieżącej daty.  
- `TimePeriodType.YESTERDAY` to wbudowane wyliczenie, które automatycznie aktualizuje się każdego dnia, więc skoroszyt zawsze podświetla najnowsze „Yesterday”.  
- Ustawiając `background_color` na `Color.pink` i wzorzec na `SOLID`, uzyskujemy efekt **cell background color python** bez dodatkowego kodu VBA.

## Krok 5: Wypełnij zakres przykładowymi datami i zastosuj formatowanie dat

Aby zobaczyć formatowanie warunkowe w działaniu, potrzebujemy rzeczywistych wartości dat. Musimy także **format cells date python**, aby Excel traktował je jako daty, a nie zwykłe liczby.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Wyjaśnienie:*  
- Linia `style.number = 30` to krok **format cells date python**. Kod formatu 30 odpowiada krótkiej dacie (`m/d/yy`).  
- Użycie funkcji pomocniczej utrzymuje kod w stylu DRY (Don’t Repeat Yourself) i ułatwia późniejsze dodawanie kolejnych dat.

## Krok 6: Dodaj opisową etykietę

Mała etykieta pomaga każdemu, kto otworzy skoroszyt, zrozumieć, dlaczego komórki są kolorowane.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Krok 7: Zapisz skoroszyt na dysku

Na koniec **create Excel workbook python** na dysku, wywołując `save`. Stała `SaveFormat.XLSX` zapewnia, że plik jest w nowoczesnym formacie Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Gdy otworzysz `TimePeriodDemo.xlsx` w Excelu, zobaczysz:

- Komórki `I19` i `K20` zawierają daty.  
- Komórka, która odpowiada „Yesterday” (w tym statycznym przykładzie, `I19`) jest podświetlona na różowo.  
- Etykieta „Yesterday” pojawia się w `I20`.  

> **Tip:** Jeśli uruchomisz skrypt w innym dniu, formatowanie warunkowe nadal podświetli komórkę, której data jest dokładnie jeden dzień przed bieżącą datą systemową — bez konieczności zmiany kodu.

## Pełny skrypt – gotowy do skopiowania i uruchomienia

Poniżej znajduje się kompletny, samodzielny program, który zawiera wszystkie powyższe kroki. Skopiuj go do pliku o nazwie `conditional_format_demo.py`, dostosuj `YOUR_DIRECTORY` i uruchom poleceniem `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Oczekiwany wynik

Uruchomienie skryptu wypisuje wiersz potwierdzający:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Otwarcie wygenerowanego pliku pokazuje różowe tło w komórce, która spełnia regułę „Yesterday”, potwierdzając, że **excel conditional formatting python** i **cell background color python** działają razem.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak dostosować kod |
|-----------|-----------------------|
| **Inny kolor podświetlenia** | Zmien `Color.pink` na dowolną inną stałą `Color`, np. `Color.light_green`. |
| **Podświetlenie „Today” zamiast „Yesterday”** | Ustaw `condition.time_period = TimePeriodType.TODAY`. |
| **Zastosowanie formatowania do całej kolumny** | Użyj zakresu takiego jak `"A:A"` i odpowiednio dostosuj zmienną `target_range`. |
| **Użycie własnego formatu daty** | Zamień `style.number = 30` na `style.custom = "dd-mmm-yyyy"` dla bardziej czytelnego formatu. |
| **Wiele warunków w tym samym zakresie** |  |

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz skoroszyt Excel w Pythonie – Kompletny przewodnik z lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Utwórz i zapisz skoroszyt Excel jako PDF w ASP.NET przy użyciu Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Jak utworzyć i zapisać skoroszyt Excel jako ODS przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}