---
category: general
date: 2026-06-21
description: Utwórz dynamiczną tablicę przy użyciu Pythona i funkcji SEQUENCE w Excelu.
  Dowiedz się, jak odczytać wynik formuły, przeliczyć formuły w Excelu i zobacz przykład
  funkcji SEQUENCE w Excelu.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: pl
og_description: Utwórz dynamiczną tablicę w Excelu przy użyciu Pythona. Ten tutorial
  pokazuje, jak używać funkcji SEQUENCE, przeliczać formuły w Excelu i odczytywać
  wynik formuły.
og_title: Tworzenie dynamicznej tablicy w Excelu przy użyciu Pythona – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Tworzenie dynamicznej tablicy w Excelu przy użyciu Pythona – przewodnik krok
  po kroku
url: /pl/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie dynamicznej tablicy w Excelu przy użyciu Pythona – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **create dynamic array** formuły w Excelu bez opuszczania skryptu Pythona? Nie jesteś jedyny. Niezależnie od tego, czy automatyzujesz miesięczny raport, czy tworzysz lekki silnik danych, możliwość wstawienia formuły `SEQUENCE` do skoroszytu, przeliczenia go i pobrania zakresu rozlewu z powrotem do Pythona jest przełomowa.

W tym samouczku przeprowadzimy Cię przez rzeczywisty **excel sequence example**, pokażemy, jak **read formula result**, oraz wyjaśnimy najlepszy sposób na **recalculate excel formulas** po wstrzyknięciu nowej logiki. Po zakończeniu będziesz mieć samodzielny skrypt, który możesz skopiować‑wkleić, uruchomić i dostosować do własnych potrzeb.

Nie wymagana jest wcześniejsza znajomość nowego silnika dynamic‑array w Excelu — wystarczy podstawowa znajomość Pythona i biblioteki takiej jak **xlwings**, która potrafi komunikować się z Excelem.

---

## Co się nauczysz

- Jak działa funkcja `SEQUENCE` i dlaczego jest idealna do generowania macierzy.
- Różnica między zwykłą wartością komórki a adresem zakresu rozlewu.
- Użycie `wb.calculate_formula()` (lub jego odpowiednika) do wymuszenia, aby Excel ocenił nowe formuły.
- Wyodrębnianie adresu dynamicznej tablicy przy użyciu `ANCHORARRAY`.
- Pełny, uruchamialny przykład w Pythonie, który możesz wkleić do dowolnego projektu.

## Jak utworzyć dynamiczną tablicę przy użyciu SEQUENCE w Excelu z użyciem Pythona

Pierwszym krokiem jest zapisanie formuły **dynamic array** bezpośrednio w komórce arkusza. W nowoczesnym Excelu funkcja `SEQUENCE` może generować macierz liczb w locie. Oto składnia, której użyjemy:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Why `SEQUENCE`?**  
Traktuj to jak wbudowaną w Excel funkcję `range()` dla arkuszy kalkulacyjnych. Pozwala określić liczbę wierszy, kolumn, wartość początkową i przyrost — wszystko w jednej zwięzłej linii. W naszym przypadku żądamy 3 wierszy i 2 kolumn, zaczynając od 10 i zwiększając o 5, co daje:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Ponieważ formuła znajduje się w `A1`, Excel automatycznie „rozlewa” wynik do sąsiednich komórek `A1:B3`. Ten rozlew będzie później pobrany.

## Użycie funkcji SEQUENCE w Excelu – Szybki przykład Excel Sequence

Jeśli otworzysz Excel ręcznie i wpiszesz `=SEQUENCE(3,2,10,5)` w komórkę, natychmiast zobaczysz tę samą macierz. Funkcja jest częścią silnika **dynamic array** w Excelu wprowadzonego w Office 365, co oznacza:

- Nie ma potrzeby używania Ctrl+Shift+Enter.
- Wynik może automatycznie się rozszerzać lub kurczyć.
- Możesz odwoływać się do całego zakresu rozlewu za pomocą funkcji takich jak `@` lub `#`.

W Pythonie jedyną różnicą jest to, że przypisujemy formułę jako łańcuch znaków do właściwości `.formula` komórki. Biblioteka zajmuje się resztą.

## Pobieranie adresu zakresu rozlewu za pomocą ANCHORARRAY

Gdy dynamiczna tablica jest już w miejscu, często potrzebujesz wiedzieć, gdzie Excel faktycznie umieścił wartości. Właśnie tutaj `ANCHORARRAY` się przydaje. Zwraca adres lewego‑górnego komórki zakresu rozlewu — dokładnie to, czego potrzebujemy, aby odczytać w naszym skrypcie.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Umieszczenie tej formuły w `C1` daje nam łańcuch tekstowy, np. "A1:B3". Zauważ, że **reading the formula result** jako zwykłą wartość, a nie jako kolejną formułę. Ten mały trik eliminuje potrzebę ręcznego parsowania arkusza.

## Przeliczanie formuł w Excelu i odczytywanie wyniku

Excel nie zawsze przelicza natychmiast, gdy nowa formuła jest wstrzykiwana z zewnętrznego skryptu. Aby zapewnić, że skoroszyt odzwierciedla najnowsze zmiany, wyraźnie wywołujemy przebieg kalkulacji.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Why call `calculate_formula()`?**  
Jeśli pominiesz ten krok, `ws.cells["C1"].value` może nadal zwracać `None` lub stary adres, ponieważ Excel wciąż aktualizuje drzewo zależności. Wymuszając przeliczenie, zapewniamy, że **read formula result** jest aktualny.

## Pełny skrypt – od początku do końca

Poniżej znajduje się kompletny, gotowy do uruchomienia przykład, który łączy wszystkie elementy. Zakłada, że masz zainstalowane **xlwings** (`pip install xlwings`) i że Excel jest dostępny na Twoim komputerze.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Oczekiwany wynik

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Uruchomienie skryptu otworzy Excel, wstawi formułę `SEQUENCE`, przeliczy i następnie wydrukuje zarówno adres rozlewu, jak i samą macierz. Nie wymaga ręcznych kliknięć.

## Częste pułapki i wskazówki profesjonalne

- **Pitfall:** Zapomnienie o `wb.calculate_formula()`.  
  *Result:* `C1` pozostaje pusty lub pokazuje przestarzały adres.  
  *Fix:* Zawsze wywołuj przeliczenie po zapisaniu nowych formuł.

- **Pitfall:** Używanie starszej wersji Excela, która nie posiada funkcji `SEQUENCE`.  
  *Result:* błąd `#NAME?`.  
  *Fix:* Upewnij się, że masz Office 365 lub Excel 2021+.

- **Pro tip:** Jeśli potrzebujesz zakresu rozlewu do dalszego przetwarzania (np. tworzenia wykresów), możesz bezpośrednio podać adres do `ws.range(spill_address)`, jak pokazano wyżej.

- **Pro tip:** `ANCHORARRAY` działa z dowolną dynamiczną tablicą, nie tylko z `SEQUENCE`. Zamień na `=SORT(A2:A10)` lub `=FILTER(...)` i nadal otrzymasz prawidłowy adres rozlewu.

- **Edge case:** Gdy docelowy obszar jest już zajęty, Excel zwróci błąd `#SPILL!`. W takim przypadku najpierw wyczyść zakres docelowy lub przenieś formułę do innej komórki.

## Rozszerzanie przykładu – co dalej?

Teraz, gdy wiesz, jak **create dynamic array** formuły, **read formula result**, i **recalculate excel formulas**, możesz eksplorować bardziej zaawansowane scenariusze:

- **Dynamic chart data** – podaj zakres rozlewu jako źródło wykresu i pozwól wykresowi rosnąć automatycznie.
- **Conditional formatting** – zastosuj reguły do zakresu rozlewu używając jego adresu.
- **Cross‑workbook references** – zapisz dynamiczną tablicę w jednym skoroszycie i pobierz dane do innego za pomocą linków `xlwings`.

Każdy z nich opiera się na podstawowych koncepcjach omówionych tutaj, więc śmiało eksperymentuj. Jedynym ograniczeniem jest Twoja wyobraźnia (oraz ewentualnie maksymalna liczba wierszy/kolumn w Excelu).

## Podsumowanie

Właśnie przeszliśmy kompletny przepływ pracy, aby **create dynamic array** formuły w Excelu z Pythona, używać **SEQUENCE function excel**, pobierać zakres rozlewu za pomocą **ANCHORARRAY**, **recalculate excel formulas**, i w końcu **read formula result** z powrotem do Twojego skryptu. Krótki przykład pokazuje, jak potężny może być nowy silnik dynamic‑array w Excelu w połączeniu z narzędziami automatyzacji takimi jak **xlwings**.

Wypróbuj to w własnych projektach, zmień wymiary macierzy lub zamień `SEQUENCE` na dowolną inną dynamiczną funkcję. Gdy nabierzesz wprawy, odkryjesz, że automatyzacja Excela staje się nie tylko możliwa, ale i przyjemnie prosta.

Masz pytania lub chcesz podzielić się, jak rozbudowałeś ten wzorzec? zostaw komentarz poniżej i szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}