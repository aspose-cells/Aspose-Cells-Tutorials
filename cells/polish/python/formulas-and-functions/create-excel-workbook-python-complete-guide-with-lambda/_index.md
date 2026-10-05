---
category: general
date: 2026-06-08
description: Utwórz przykład skoroszytu Excel w Pythonie, który pokazuje, jak używać
  funkcji lambda w Excelu, sumować wiersze za pomocą BYROW i automatyzować obliczenia
  w kilku krokach.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: pl
og_description: Utwórz skoroszyt Excela w Pythonie i dowiedz się, jak używać funkcji
  lambda w Excelu do efektywnego sumowania wierszy za pomocą formuł BYROW.
og_title: Tworzenie skoroszytu Excel w Pythonie – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Tworzenie skoroszytu Excel w Pythonie – Kompletny przewodnik z Lambda
url: /pl/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel w Pythonie – Kompletny przewodnik z Lambda

Zastanawiałeś się kiedyś, jak **create Excel workbook Python** skrypty automatyzujące nudne przetwarzanie liczb? Nie jesteś sam — wielu programistów napotyka problem, gdy muszą wygenerować arkusz, wstawić formułę i odczytać wyniki z powrotem w swoim kodzie.  

W tym samouczku pokażemy również **how to use lambda** w Excelu, wyjaśnimy **how to sum rows** przy użyciu nowoczesnej funkcji `BYROW` i damy Ci schludny, kompletny przykład, który możesz skopiować‑wkleić i uruchomić już dziś.

## Co się nauczysz

- Utwórz nowy skoroszyt z Pythona bez ręcznego otwierania Excela.  
- Wypełnij zakres macierzą liczb 3 × 3.  
- Wstaw formułę `BYROW`, która wykorzystuje składnię **use lambda excel** do sumowania każdego wiersza.  
- Przelicz arkusz, aby formuła się obliczyła, a następnie odczytaj wyniki z powrotem w Pythonie.  

Pod koniec tego przewodnika będziesz mieć samodzielny skrypt, który możesz dostosować do faktur, kart wyników lub każdej sytuacji, w której potrzebujesz **sum rows** w locie.

### Wymagania wstępne

- Zainstalowany Python 3.8+.  
- Biblioteka `openpyxl` (lub `xlwings`, jeśli wolisz podejście oparte na COM). Użyjemy `openpyxl`, ponieważ jest czystym Pythonem i działa na wszystkich platformach.  
- Najnowsza wersja Microsoft Excel (365 lub 2021), która obsługuje funkcję `BYROW` i formuły Lambda.  

Install the library with:

```bash
pip install openpyxl
```

> **Pro tip:** Jeśli napotkasz problemy z uprawnieniami w Windows, użyj `python -m pip install --user openpyxl`.

## Tworzenie skoroszytu Excel w Pythonie – Inicjalizacja skoroszytu

Pierwszą rzeczą, której potrzebujemy, jest zupełnie nowy obiekt skoroszytu, który istnieje wyłącznie w pamięci. W `openpyxl` to jednowierszowy kod:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Dlaczego używamy `wb.active` zamiast indeksowania `Worksheets[0]`? `openpyxl` udostępnia aktywny arkusz bezpośrednio, co jest czytelniejsze i unika dodatkowego przeszukiwania listy. Jeśli kiedykolwiek będziesz potrzebować pracować z wieloma arkuszami, zawsze możesz dodać je za pomocą `wb.create_sheet(title="MySheet")`.

## Wypełnianie arkusza danymi – Prosta macierz 3×3

Następnie wypełniamy arkusz małą macierzą. Odzwierciedla to klasyczny przykład „sumuj każdy wiersz” i utrzymuje kod zwięzły.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Możesz się zastanawiać, dlaczego pętlujemy ręcznie zamiast używać `ws.append()` lub `ws.values`. Jawne pętle dają nam pełną kontrolę nad komórką początkową i ułatwiają późniejsze dostosowanie offsetów — przydatne, gdy chcesz pozostawić pusty wiersz lub kolumnę nagłówka.

## Jak używać Lambda w formułach Excel

Funkcja **use lambda excel** w Excelu pozwala pisać anonimowe funkcje bezpośrednio w komórce. Pomyśl o niej jak o `lambda` w Pythonie, ale działającej w silniku arkusza. Składnia to:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

W połączeniu z `BYROW` możesz zastosować tę lambdę do każdego wiersza zakresu, generując kolumnę wyników. To jest sedno naszego triku **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

Co się dzieje pod maską?

- `A1:C3` to zakres źródłowy (nasza macierz).  
- `LAMBDA(r, SUM(r))` definiuje tymczasową funkcję, która otrzymuje pojedynczy wiersz (`r`) i zwraca jego sumę.  
- `BYROW` uruchamia tę lambdę dla **każdego wiersza** i rozlewa wyniki do kolumny D, zaczynając od `D1`.  

Ponieważ `BYROW` jest funkcją *dynamic array*, Excel automatycznie wypełnia `D1:D3` trzema sumami.

> **Note:** `BYROW` i formuły Lambda są dostępne tylko w Excel 365/2021 i nowszych. Jeśli używasz starszej wersji, musisz wrócić do tradycyjnych formuł `SUM` lub VBA.

## Jak sumować wiersze przy użyciu BYROW i Lambda

Teraz, gdy formuła znajduje się w arkuszu, musimy nakazać Excelowi jej obliczenie. `openpyxl` sam nie oblicza formuł; tylko je odczytuje/zapisuje. Aby wywołać obliczenie, możemy:

1. Zapisz skoroszyt i otwórz go w Excelu (ręcznie).  
2. Użyj silnika COM `xlwings`, aby wymusić przeliczenie (wymaga zainstalowanego Excela).  

Dla rozwiązania czysto‑Pythonowego użyjemy `xlwings` tylko do kroku przeliczenia — nic więcej.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Dlaczego nie wywołać `wb.calculate()`? `openpyxl` nie posiada własnego silnika, więc polegamy na samym Excelu poprzez `xlwings`. Narzut jest minimalny dla małych arkuszy i daje nam dokładny wynik, jaki wyświetliłby Excel.

## Przelicz i pobierz wyniki – odczytaj sumy z powrotem w Pythonie

Na koniec odczytujemy rozlane wyniki z kolumny D. `openpyxl` ułatwia to:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Jeśli wolisz pozostać w `openpyxl`, możesz odczytać komórki po przeliczeniu w Excelu:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Oba podejścia dają tę samą listę `[6, 15, 24]`, potwierdzając, że **how to sum rows** z `BYROW` + Lambda działa zgodnie z opisem.

## Przypadki brzegowe i typowe pułapki

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Wersja Excela starsza niż 365 | `BYROW` i `LAMBDA` pojawiają się jako `#NAME?` | Użyj klasycznej formuły `=SUM(A1:C1)` skopiowanej ręcznie w dół lub zaktualizuj Excela. |
| Duże macierze (10 k+ wierszy) | Przeliczenie może stać się wolne | Wywołaj `book.api.CalculateFullRebuild()` tylko raz lub podziel skoroszyt. |
| Uruchamianie na serwerze bez interfejsu graficznego bez Excela | `xlwings` nie może uruchomić Excela | Przejdź na czystą bibliotekę Pythona, taką jak `pandas` + `numpy` do obliczeń, a następnie zapisz wyniki. |
| Problemy regionalne (przecinek vs. średnik) | Formuła może zostać odrzucona | Użyj `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` dla ustawień regionalnych używających `;`. |

## Pełny działający przykład (gotowy do kopiowania‑wklejania)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook with Aspose.Cells Java - Complete Guide](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Create Excel Workbook & Automate Reports with Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}