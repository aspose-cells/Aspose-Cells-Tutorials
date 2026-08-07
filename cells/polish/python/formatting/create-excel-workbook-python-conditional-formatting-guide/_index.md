---
category: general
date: 2026-07-20
description: Utwórz skoroszyt Excel w Pythonie przy użyciu Aspose.Cells, ustaw kolor
  tła komórki i dodaj formatowanie warunkowe w Pythonie, aby stylizować komórki według
  daty.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: pl
lastmod: 2026-07-20
og_description: Utwórz skoroszyt Excel w Pythonie przy użyciu Aspose.Cells. Dowiedz
  się, jak ustawić kolor tła komórki i dodać formatowanie warunkowe w Pythonie, aby
  formatować komórki według daty.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Utwórz skoroszyt Excel w Pythonie – Dodaj formatowanie warunkowe
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Tworzenie skoroszytu Excel w Pythonie – Przewodnik po formatowaniu warunkowym
url: /pl/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel w Pythonie – Przewodnik po formatowaniu warunkowym

Zastanawiałeś się kiedyś, jak **create Excel workbook Python** od podstaw i sprawić, by wyglądał profesjonalnie bez otwierania interfejsu? Nie jesteś sam. Wielu programistów napotyka trudności, gdy muszą **set cell background color** lub zastosować style oparte na datach programowo.  

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który używa Aspose.Cells do **add conditional formatting python** reguł, formatuje komórki według daty i zapisuje wynik jako nowoczesny plik XLSX. Po zakończeniu będziesz mieć samodzielny skrypt, który możesz wkleić do dowolnego projektu.

## Co się nauczysz

- Jak zainicjować workbook i pobrać pierwszy worksheet.  
- Sposoby na **set cell background color** dla całego zakresu.  
- Użycie **aspose cells conditional formatting** do podświetlenia dat „Yesterday”.  
- Automatyczne dopasowywanie kolumn i zapisywanie pliku na dysku.  

Nie wymagana jest żadna zewnętrzna konfiguracja — wystarczy Python 3 i pakiet Aspose.Cells. Jeśli już zainstalowałeś `aspose-cells`, jesteś gotowy; w przeciwnym razie wystarczy szybkie `pip install aspose-cells`.

## Wymagania wstępne

- Python 3.8+ (kod działa na 3.9, 3.10 i nowszych).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Podstawowa znajomość koncepcji Excela (komórki, zakresy, formatowanie).  

Masz je? Świetnie — zanurzmy się.

## Tworzenie skoroszytu Excel w Pythonie – konfiguracja i arkusz

Na początek potrzebujemy nowego obiektu workbook oraz odwołania do domyślnego worksheet. To jest płótno, na którym będą wykonywane wszystkie późniejsze operacje.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Dlaczego to ważne:** `Workbook()` tworzy plik Excel w pamięci, eliminując potrzebę jakichkolwiek plików tymczasowych. Zmienna `worksheet` jest naszym punktem wejścia do działań na poziomie komórek.

## Ustaw kolor tła komórki

Zanim dodamy jakiekolwiek reguły, warto nadać docelowemu zakresowi podstawowy kolor, aby formatowanie warunkowe się wyróżniało. Poniższy pomocnik zarówno pobiera (lub tworzy) `FormatConditionCollection` dla danego zakresu, jak i maluje komórki jednolitym tłem.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Wskazówka:** Jeśli planujesz ponownie używać tego samego zakresu z wieloma regułami, wywołaj ten pomocnik raz i zachowaj zwróconą kolekcję; oszczędza to kilka wywołań API.

## Dodaj formatowanie warunkowe w Pythonie dla zakresów dat

Teraz najciekawsza część: stworzymy regułę **time‑period conditional formatting**, która podświetli komórki zawierające wczorajszą datę. To pokazuje moc **format cells by date** przy użyciu Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Dlaczego używać `TIME_PERIOD`?** Abstrahuje to potrzebę pisania własnych formuł. Aspose.Cells ocenia datę względem bieżącej daty systemowej, więc reguła zawsze pozostaje aktualna.

### Uruchamianie reguły

```python
apply_yesterday_rule()
```

Po otwarciu wygenerowanego pliku, komórki `I19` będą świecić na różowo (ponieważ to „Yesterday”), podczas gdy `K20` pozostanie w podstawowym zielonym kolorze.

## Automatyczne dopasowanie kolumn i zapis skoroszytu

Porządną tabelę w Excelu wygląda profesjonalnie. Automatyczne dopasowanie zapewnia, że nasze dane nie są ściśnięte.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Przypadek brzegowy:** Jeśli wskażesz katalog, który nie istnieje, `workbook.save` zgłosi błąd. Owiń wywołanie zapisu w blok `try/except`, jeśli potrzebujesz łagodnego obsłużenia.

### Pełny skrypt (gotowy do kopiowania i wklejenia)

Poniżej znajduje się cały skrypt, gotowy do uruchomienia. Wystarczy zamienić `YOUR_DIRECTORY` na prawidłowy folder na Twoim komputerze.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Uruchomienie tego skryptu wygeneruje plik `TimePeriodExample.xlsx` z opisanym formatowaniem warunkowym.

## Częste pytania i wskazówki

- **Czy mogę wybrać inny zakres dat?**  
  Oczywiście. Zmień `"I19:K20"` na dowolny zakres w stylu A1 i odpowiednio dostosuj przykładowe daty.

- **Co zrobić, jeśli potrzebuję własnej formuły zamiast `YESTERDAY`?**  
  Użyj `FormatConditionType.FORMULA` i ustaw `condition.formula1 = "YOUR_FORMULA"` — na przykład `=TODAY()-A1=1`, aby naśladować wczoraj.

- **Jak zastosować wiele reguł do tego samego zakresu?**  
  Wywołaj ponownie `conditions.add_condition` z innym `FormatConditionType`. Kolejność ma znaczenie; późniejsze reguły mogą nadpisać wcześniejsze.

- **Czy istnieje sposób, aby ustawić kolor czcionki razem z tłem?**  
  Tak — zmodyfikuj `condition.style.font.color = Color.white` (lub dowolny inny `Color`).

## Podsumowanie

Teraz wiesz, jak **create Excel workbook Python** przy użyciu Aspose.Cells, **set cell background color**, oraz **add conditional formatting python**, które formatuje komórki według daty. Skrypt jest w pełni funkcjonalny, obsługuje przypadki brzegowe, takie jak brakujące katalogi, i może być rozszerzony do bardziej zaawansowanych scenariuszy, takich jak logika warunkowa z wieloma regułami czy dynamiczne wykrywanie zakresów.

Gotowy na kolejny krok? Spróbuj zamienić regułę „Yesterday” na „Last Week”, poeksperymentuj z wypełnieniami gradientowymi lub wygeneruj pełny raport z dziesiątkami sformatowanych tabel. Wszystkie elementy budulcowe są tutaj, a Ty właśnie opanowałeś podstawy **aspose cells conditional formatting** w Pythonie.

Miłego kodowania i zachęcam do dzielenia się własnymi wariacjami w komentarzach!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}