---
category: general
date: 2026-11-16
description: Utwórz formatowanie warunkowe w Excelu przy użyciu Pythona. Dowiedz się,
  jak dodać zakres formatowania warunkowego, podświetlać daty i programowo tworzyć
  skoroszyt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: pl
lastmod: 2026-11-16
og_description: Utwórz formatowanie warunkowe w Excelu przy użyciu Pythona. Ten tutorial
  pokazuje, jak dodać zakres formatowania warunkowego, podświetlić daty i wygenerować
  skoroszyt.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Tworzenie formatowania warunkowego w Excelu przy użyciu Pythona – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Jak stworzyć formatowanie warunkowe w Excelu przy użyciu Pythona
url: /pl/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak tworzyć formatowanie warunkowe w Excelu przy użyciu Pythona

Jeśli potrzebujesz **tworzyć formatowanie warunkowe** w pliku Excel podczas pracy w Pythonie, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się **tworzyć skoroszyt Excel w stylu python**, określić zakres formatowania oraz podświetlać daty bez wychodzenia z IDE.

Formatowanie warunkowe pozwala wizualnie oznaczyć komórki spełniające określone kryteria — idealne do pulpitów, raportów lub arkuszy weryfikacji danych. Po zakończeniu tego tutorialu będziesz mieć w pełni funkcjonalny skoroszyt, który koloruje komórki z datą „Yesterday” na różowo, a pozostałą część zakresu pozostawia zieloną.

## Co osiągniesz

* Zbudujesz nowy skoroszyt od podstaw.  
* Dodasz kolekcję formatowania warunkowego dla określonego bloku komórek.  
* Zastosujesz regułę **TIME_PERIOD**, która podświetla daty (scenariusz „jak podświetlić daty”).  
* Zapiszesz plik jako skoroszyt XLSX gotowy do dalszego przetwarzania.

**Wymagania wstępne**  
* Python 3.8+  
* Pakiet `aspose-cells` dla Pythona (`pip install aspose-cells`)  
* Podstawowa znajomość modułu `datetime` w Pythonie  

---

## Jak tworzyć formatowanie warunkowe w Pythonie

Pierwszym krokiem jest skonfigurowanie skoroszytu i arkusza, które będą hostować reguły formatowania.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Dlaczego to ważne** – `Workbook` jest punktem wejścia dla wszystkich operacji na Excelu. Tworzenie skoroszytu programowo zastępuje ręczny krok „Plik → Nowy”, umożliwiając automatyzację pipeline’ów raportowych.

---

## Przygotowanie kolekcji formatowania warunkowego – dodanie zakresu formatowania

Następnie definiujemy blok komórek, który otrzyma regułę. W tym przykładzie zakres to **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Wyjaśnienie** – `conditional_formattings.add` rejestruje nową kolekcję powiązaną z ciągiem adresu. Pierwszy warunek (`conds[0]`) działa jako styl „domyślny”; późniejsza reguła nadpisze go, gdy spełnione zostaną jej kryteria.

---

## Dodanie warunku TIME_PERIOD – jak podświetlić daty

Teraz dodajemy właściwą logikę, która identyfikuje daty „Yesterday” i maluje je na różowo.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Dlaczego używać TIME_PERIOD?** – Aspose.Cells udostępnia wbudowane wyliczenia takie jak `YESTERDAY`, `TODAY` i `LAST_WEEK`. Porównują one wartość daty w komórce z bieżącą datą systemową, eliminując potrzebę własnych formuł.

---

## Wstawianie przykładowych danych – demonstracja reguły

Aby zobaczyć formatowanie w działaniu, wstawiamy datę spełniającą regułę oraz inną, która jej nie spełnia.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Uwaga o przypadkach brzegowych** – Reguła `TIME_PERIOD` działa wyłącznie na *rzeczywistych* datach. Jeśli komórka zawiera tekst (np. „N/A”), reguła jest pomijana, co zapobiega nieoczekiwanym zmianom koloru.

---

## Zapis skoroszytu – add conditional formatting python

Na koniec zapisujemy skoroszyt na dysku. Plik można otworzyć w dowolnym programie arkuszy kalkulacyjnych, aby zweryfikować kolory.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Oczekiwany wynik**  

| I19 (zielony → różowy) | J19 (zielony) | K19 (zielony) |
|------------------------|---------------|---------------|
| 30/07/2008 (wczoraj)   | –             | –             |
| **I20**: etykieta „Yesterday” | –   | –             |
| I21‑K21 (zielony)      | –             | –             |

Komórka **I19** ma różowe tło, ponieważ jej data pasuje do okresu „Yesterday”, podczas gdy **K20** pozostaje zielona.

---

## Częste pytania i praktyczne wskazówki

* **Czy mogę użyć własnego zakresu dat zamiast wbudowanego okresu?**  
  Tak. Zamień `condition.time_period` na `condition.formula1 = "TODAY()-1"` i ustaw `condition.type = FormatConditionType.FORMULA`.

* **Co zrobić, jeśli mój skoroszyt już zawiera dane?**  
  Użyj `worksheet.cells.import_data`, aby masowo załadować dane przed dodaniem kolekcji formatowania warunkowego.

* **Wydajność przy dużych arkuszach?**  
  Dodawanie wielu warunków może spowolnić renderowanie. Grupuj komórki o tej samej regule w jeden zakres (np. „A1:C1000”), aby ograniczyć liczbę warunków.

* **Kompatybilność wieloplatformowa?**  
  Wygenerowany plik XLSX spełnia standard Office Open XML, więc działa w aplikacjach na Windows, macOS i Linux.

---

## Podsumowanie

Teraz wiesz, jak **tworzyć formatowanie warunkowe** w skoroszycie Excel przy użyciu Pythona. Tutorial obejmował tworzenie skoroszytu, definiowanie **add conditional formatting range**, zastosowanie reguły **how to highlight dates** oraz zapis pliku — wszystko przy użyciu podejścia **add conditional formatting python** dostarczonego przez Aspose.Cells.

Od tego momentu możesz:

* Rozszerzyć zestaw reguł o inne wartości `TimePeriodType` (np. `TODAY`, `LAST_MONTH`).  
* Połączyć wiele warunków w tym samym zakresie, aby uzyskać bogatsze wskazówki wizualne.  
* Zintegrować ten workflow z automatycznymi pipeline’ami raportowymi lub usługami webowymi.

Miłego kodowania i zachęcamy do eksperymentowania z różnymi kolorami, zakresami i logiką dat, aby dopasować je do swoich potrzeb raportowych!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny, działający kod oraz szczegółowe wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}