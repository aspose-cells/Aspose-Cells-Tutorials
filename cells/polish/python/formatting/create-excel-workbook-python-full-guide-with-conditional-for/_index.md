---
category: general
date: 2026-07-14
description: Utwórz kod Pythona tworzący skoroszyt Excel, który ustawia kolor tła
  komórek, podświetla komórki na podstawie zakresu dat i zapisuje skoroszyt jako plik
  XLSX w ciągu kilku minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: pl
lastmod: 2026-07-14
og_description: Twórz skoroszyt Excel w Pythonie natychmiast. Dowiedz się, jak ustawić
  kolor tła komórki, podświetlić komórki w zależności od zakresu dat oraz zapisać
  skoroszyt jako XLSX przy użyciu Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Tworzenie skoroszytu Excel w Pythonie – Krok po kroku formatowanie warunkowe
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Tworzenie skoroszytu Excel w Pythonie – Kompletny przewodnik z formatowaniem
  warunkowym
url: /pl/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Pełny przewodnik z formatowaniem warunkowym

Zastanawiałeś się kiedyś, jak **create excel workbook python** skrypty, które wyglądają profesjonalnie, bez ręcznego otwierania Excela? Nie jesteś sam. W wielu projektach opartych na danych musimy generować arkusze kalkulacyjne, kolorować komórki i nawet oznaczać daty mieszczące się w określonym przedziale — wszystko z czystego kodu Pythona.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **creates an Excel workbook python** przy użyciu biblioteki Aspose.Cells, **sets cell background color**, stosuje **conditional formatting based on date** i w końcu **saves workbook as xlsx**. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego potoku automatyzacji.

## Co się nauczysz

- Jak zainicjalizować skoroszyt i pobrać pierwszy arkusz.  
- Funkcja pomocnicza, która dodaje kolekcję formatowania warunkowego dla dowolnego zakresu komórek.  
- Użycie **conditional formatting based on date** do podświetlenia wczorajszych wpisów.  
- Dostosowanie szerokości kolumn dla schludnego układu.  
- Zachowanie wyniku przy użyciu **save workbook as xlsx**.  

Instalacja Excela nie jest wymagana — Aspose.Cells obsługuje wszystko w pamięci.

## Wymagania wstępne

- Zainstalowany Python 3.8+.  
- Pakiet `aspose-cells` (`pip install aspose-cells`).  
- Podstawowa znajomość funkcji Pythona i obiektów datetime.  

Jeśli nigdy nie używałeś Aspose.Cells, potraktuj go jako potężne, czysto‑Pythonowe API, które naśladuje model obiektowy Excela. Jest idealny do generowania po stronie serwera, gdy pakiet Office nie jest dostępny.

## Krok 1: Inicjalizacja skoroszytu (Create Excel Workbook Python)

Na początek: musimy **create excel workbook python** w stylu. Ten krok tworzy pusty obiekt skoroszytu i wskazuje domyślny arkusz.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Dlaczego to ważne:** Klasa `Workbook` jest punktem wejścia dla każdej operacji Excel. Tworząc ją programowo, unikamy ręcznego zarządzania plikami.

## Krok 2: Pomocnik do dodania kolekcji formatowania warunkowego (Set Cell Background Color)

Formatowanie warunkowe znajduje się wewnątrz *kolekcji* dołączonej do zakresu. Owińmy ten szablon w mały pomocnik, który pozwala nam także **set cell background color** dla całego zakresu.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Porada:** Użycie pomocnika utrzymuje główny przepływ czystym i ułatwia ponowne wykorzystanie tej samej logiki dla wielu zakresów.

## Krok 3: Zastosowanie formatowania warunkowego na podstawie daty (Highlight Cells Based on Date Range)

Teraz faktycznie **highlight cells based on date range**. Przykład koncentruje się na „wczoraj”, ale możesz zamienić `TimePeriodType.YESTERDAY` na `TODAY`, `LAST_WEEK` itp.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Co się dzieje?**  
> 1. Najpierw nadajemy całemu zakresowi neutralne zielone tło.  
> 2. Następnie dodajemy warunek `TIME_PERIOD`, który nadpisuje wypełnienie na różowe **tylko** wtedy, gdy data w komórce równa się wczorajszemu dniu.  
> 3. Enum `TimePeriodType` abstrahuje obliczenia daty, więc nie musisz pisać własnej logiki.

## Krok 4: Wypełnienie przykładowymi datami (So the Rule Can Be Evaluated)

Aby zobaczyć regułę w działaniu, wstawimy kilka dat do arkusza. Jedna mieści się w oknie „wczoraj”, druga nie.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Uwaga dotycząca przypadków brzegowych:** Jeśli Twój skoroszyt będzie otwierany w różnych ustawieniach regionalnych, rozważ użycie `date_style.custom = "dd‑mm‑yyyy"`, aby wymusić spójny format wyświetlania.

## Krok 5: Porządkowanie układu (Auto‑Fit Columns)

Zaciskany arkusz wygląda nieprofesjonalnie. Zróbmy **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Dlaczego auto‑fit?** Zapewnia, że wszystkie długie etykiety lub daty są w pełni widoczne, co jest szczególnie ważne, gdy udostępniasz plik osobom nietechnicznym.

## Krok 6: Zapisz skoroszyt (Save Workbook As XLSX)

Na koniec **save workbook as xlsx** w wybranej lokalizacji. Stała `SaveFormat.XLSX` informuje Aspose.Cells, aby zapisał w nowoczesnym formacie OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Wynik, który powinieneś zobaczyć:**  
> - Komórki I19 i K20 zawierają daty.  
> - I19 (wczoraj) jest podświetlona na różowo, podczas gdy K20 pozostaje zielona.  
> - Kolumna L automatycznie rozszerza się, aby pomieścić etykietę „Yesterday”.  

Jeśli otworzysz `TimePeriodDemo.xlsx` w Excelu, formatowanie warunkowe będzie już zastosowane — nie są potrzebne dodatkowe kroki.

![Arkusz Excel z podświetloną datą wczorajszą](https://example.com/images/excel-demo.png "Zrzut ekranu wygenerowanego pliku Excel z podświetlonymi komórkami")

*Powyższy obraz ilustruje końcowy skoroszyt; zauważ różowe podświetlenie komórki zawierającej wczorajszą datę.*

## Podsumowanie: Co osiągnęliśmy

- **Created an Excel workbook python** od podstaw przy użyciu Aspose.Cells.  
- **Set cell background color** dla całego zakresu, aby dać arkuszowi wizualną wskazówkę.  
- Zastosowano **conditional formatting based on date**, aby automatycznie oznaczyć wczorajsze wpisy.  
- **Saved workbook as xlsx**, gotowy do dystrybucji lub dalszego przetwarzania.  

Wszystko to zostało zrobione w mniej niż 60 liniach Pythona, a kod działa na każdej platformie obsługującej środowisko Aspose.Cells.

## Kolejne kroki i powiązane tematy

Jeśli uznałeś to za przydatne, możesz również chcieć zbadać:

- **set cell background color** dla całych wierszy w zależności od wartości statusu (np. „Completed”, „Pending”).  
- Używanie **highlight cells based on date range** do tworzenia okien przesuwnych (ostatnie 7 dni, bieżący miesiąc).  
- Eksportowanie do innych formatów, takich jak **CSV** lub **PDF**, przy użyciu `SaveFormat.CSV` lub `SaveFormat.PDF`.  
- Dodawanie **charts** programowo w celu wizualizacji danych, które właśnie sformatowano.  

Śmiało modyfikuj logikę dat, zmieniaj paletę kolorów lub rozszerz zakres, aby objąć całe kolumny. Wzorzec pozostaje ten sam: utwórz skoroszyt, dołącz kolekcję formatowania warunkowego, zdefiniuj regułę i zapisz.

Masz pytania dotyczące konkretnego przypadku użycia? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Automatyzacja Excel przy użyciu Aspose.Cells .NET: Tworzenie skoroszytu i ustawianie linków zewnętrznych](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Utwórz i zapisz skoroszyt Excel Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Utwórz i zapisz skoroszyt Excel Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}