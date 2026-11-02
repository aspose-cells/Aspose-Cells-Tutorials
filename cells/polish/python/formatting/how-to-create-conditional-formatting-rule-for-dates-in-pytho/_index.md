---
category: general
date: 2026-08-24
description: Utwórz regułę formatowania warunkowego w Pythonie przy użyciu Aspose.Cells,
  aby podświetlić daty, z automatycznym dopasowaniem szerokości kolumny i formatowaniem
  koloru tła.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: pl
lastmod: 2026-08-24
og_description: Utwórz regułę formatowania warunkowego w Pythonie z Aspose.Cells.
  Dowiedz się, jak podświetlać daty, ustawiać kolory tła i automatycznie dopasowywać
  szerokość kolumn w kilku linijkach kodu.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Utwórz regułę formatowania warunkowego dla dat w Pythonie – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Jak utworzyć regułę formatowania warunkowego dla dat w Pythonie
url: /pl/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć regułę formatowania warunkowego dla dat w Pythonie

Jeśli potrzebujesz **utworzyć regułę formatowania warunkowego**, która reaguje na daty, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells for Python. Niezależnie od tego, czy tworzysz pulpit nawigacyjny raportów, czy zautomatyzowany arkusz kalkulacyjny, zobaczysz, jak podświetlić wczorajsze daty, zastosować niestandardowy kolor tła oraz **automatycznie dopasować szerokość kolumn**, aby wynik wyglądał profesjonalnie.

W tym tutorialu omówimy **formatowanie warunkowe według daty**, pokażemy **formatowanie warunkowe z kolorem tła** i zakończymy zapisem skoroszytu jako plik XLSX. Po zakończeniu będziesz mieć pomocniczą funkcję, którą możesz dostosować do dowolnego **formatowania warunkowego opartego na dacie**, którego potrzebujesz.

## Czego się nauczysz

* Skonfigurować skoroszyt i arkusz przy użyciu Aspose.Cells.  
* Napisać funkcję pomocniczą, która dodaje **formatowanie warunkowe oparte na dacie** do dowolnego zakresu komórek.  
* Wypełnić komórki przykładowymi datami, aby reguła mogła zostać oceniona.  
* Zastosować **automatyczne dopasowanie kolumn**, aby zawartość była czytelna.  
* Zapisać skoroszyt i zweryfikować podświetlone komórki.

Jedynym wymogiem wstępnym jest działające środowisko Pythona z zainstalowanym pakietem `aspose-cells`.

## Wymagania wstępne

| Wymaganie | Szczegóły |
|-----------|-----------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Podstawowa znajomość koncepcji Excela | arkusze, komórki, formatowanie |
| Opcjonalnie: IDE (VS Code, PyCharm, itp.) | dowolny edytor, który potrafi uruchamiać skrypty Pythona |

## Krok 1: Utwórz skoroszyt i pobierz pierwszy arkusz

Pierwszym krokiem jest **utworzenie obiektów gotowych do reguły formatowania warunkowego**: `Workbook` i jego domyślnego `Worksheet`. Te obiekty są punktem wejścia dla wszystkich kolejnych operacji.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Dlaczego to ważne:* `Workbook` przechowuje cały plik Excel, natomiast `Worksheet` jest miejscem, w którym stosujesz komórki, style i **formatowanie warunkowe według daty**. Bez tych obiektów dalszy kod nie ma gdzie działać.

## Krok 2: Zbuduj pomocniczą funkcję dodającą format TIME_PERIOD

Zamiast powtarzać ten sam kod szkieletowy dla każdego zakresu, enkapsulujemy logikę w funkcji pomocniczej. Funkcja ta dołącza **formatowanie warunkowe z kolorem tła**, które koloruje komórki w zależności od `TimePeriodType` (np. Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Dlaczego używamy funkcji pomocniczej:* Izoluje ona logikę **formatowania warunkowego opartego na dacie**, co sprawia, że kod jest łatwiejszy do odczytania, testowania i ponownego użycia w wielu arkuszach lub projektach.

## Krok 3: Zastosuj regułę formatowania warunkowego do konkretnego zakresu

Teraz używamy pomocniczej funkcji, aby podświetlić komórki zawierające „Yesterday”. To jest sedno naszej operacji **utworzenia reguły formatowania warunkowego**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Gdy skoroszyt zostanie otwarty, każda komórka w `I19:K20`, której data równa się wczorajszej, zostanie wyświetlona z różowym wypełnieniem (styl ustawiony w funkcji pomocniczej). Argument `bg_color` pokazuje, jak można dodać domyślne tło za warunkowym kolorem, jeśli jest to potrzebne.

## Krok 4: Wypełnij zakres przykładowymi datami

Reguła warunkowa staje się widoczna dopiero po tym, jak arkusz zawiera dane spełniające warunek. Wstawimy dwie daty: jedną pasującą do „Yesterday” i drugą, która znajduje się poza tym okresem.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Dlaczego to ma znaczenie:* Korzystając z obiektów `datetime`, zapewniamy, że Excel traktuje wartości jako prawdziwe daty, co jest niezbędne do prawidłowego działania **formatowania warunkowego według daty**. Format liczbowy (`30`) gwarantuje, że komórki wyświetlają się jako rozpoznawalne daty.

## Krok 5: Automatycznie dopasuj kolumnę i zapisz skoroszyt

Po wstawieniu danych i formatowania, ostatnim szlifem jest **automatyczne dopasowanie szerokości kolumn**, aby daty były w pełni widoczne. Następnie zapisujemy plik na dysku.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Wywołanie `auto_fit_column` analizuje najdłuższą zawartość w kolumnie 12 (co odpowiada kolumnie **L** w Excelu) i odpowiednio rozszerza jej szerokość. Ten mały krok zapobiega obcięciu dat i sprawia, że **formatowanie warunkowe z kolorem tła** jest wyraźnie widoczne.

### Oczekiwany wynik

Po otwarciu `TimePeriodDemo.out.xlsx`:

| I19 (data) | I20 (etykieta) | K20 (data) |
|------------|----------------|------------|
| 30‑Jul‑2008 (podświetlone różem) | Yesterday | 03‑Aug‑2008 (bez podświetlenia) |

* Komórka z wczorajszą datą ma różowe tło, ponieważ **utworzona reguła formatowania warunkowego** dopasowała się do okresu `YESTERDAY`.  
* Wszystkie pozostałe komórki zachowują domyślne tło (lub opcjonalny `medium_sea_green`, który podałeś).  
* Kolumna L jest automatycznie poszerzona, więc daty są w pełni czytelne.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak dostosować kod |
|----------|--------------------|
| **Podświetlenie „Today” zamiast „Yesterday”** | Zamień `TimePeriodType.YESTERDAY` na `TimePeriodType.TODAY`. |
| **Użycie innego koloru tła** | Zmień `condition.style.background_color = Color.pink` na dowolny inny `Color` (np. `Color.light_sky_blue`). |
| **Zastosowanie reguły do nieciągłego zakresu** | Wywołaj `add_time_period_condition` wielokrotnie z różnymi ciągami `cell_range` (np. `"A1:A10", "C1:C10"`). |
| **Praca z istniejącym skoroszytem** | Załaduj plik przy pomocy `Workbook("myfile.xlsx")` zamiast tworzyć nowy. |
| **Wiele warunków opartych na dacie w tym samym zakresie** | Po pierwszym wywołaniu `add_time_period_condition` dodaj kolejną regułę przy pomocy `conditions.add_condition(FormatConditionType.TIME_PERIOD)` i ustaw inny `time_period`. |

## Podsumowanie

Wiesz już, jak **utworzyć regułę formatowania warunkowego**, która reaguje na daty, jak zastosować **formatowanie warunkowe z kolorem tła** oraz jak **automatycznie dopasować szerokość kolumn** przy użyciu Aspose.Cells for Python. Funkcja pomocnicza abstrahuje logikę, umożliwiając ponowne użycie tego samego wzorca w dowolnym scenariuszu **formatowania warunkowego według daty** — czy to „Yesterday”, „LastWeek”, czy własny zakres.

Następnie możesz zbadać:

* Dodawanie **zestawów ikon** lub **pasek danych** obok reguł datowych.  
* Generowanie dynamicznych raportów pobierających daty z bazy danych.  
* Łączenie wielu **reguł formatowania warunkowego opartych na dacie** w jednym arkuszu.

Śmiało eksperymentuj z różnymi kolorami, okresami i zakresami, aby dopasować je do potrzeb swojego projektu. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Mistrzowskie formatowanie warunkowe w Excelu przy użyciu Aspose.Cells .NET: Kompletny przewodnik](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Jak wyodrębnić kolory formatowania warunkowego przy użyciu Aspose.Cells dla .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Mistrzowskie formatowanie warunkowe z niestandardowymi czcionkami w Excelu przy użyciu Aspose.Cells dla .NET i C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}