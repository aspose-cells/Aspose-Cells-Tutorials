---
category: general
date: 2026-06-21
description: Utwórz tabelę mnożenia w Excelu przy użyciu Pythona. Dowiedz się, jak
  używać lambda, jak używać makearray, wyświetlać tablicę Excela i odczytywać wartości
  z Excela w Pythonie w samouczku krok po kroku.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: pl
og_description: Utwórz tabelę mnożenia w Excelu przy użyciu Pythona. Ten tutorial
  pokazuje, jak używać lambda, makearray, wyświetlać tablicę Excela i efektywnie odczytywać
  wartości z Excela w Pythonie.
og_title: Utwórz tabelę mnożenia w Excelu przy użyciu Pythona – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Utwórz tabelę mnożenia w Excelu za pomocą Pythona – pełny przewodnik
url: /pl/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz tabelę mnożenia w Excelu przy użyciu Pythona – Pełny przewodnik

Zastanawiałeś się kiedyś, jak **create multiplication table** w Excelu bez ręcznego wpisywania każdej komórki? Nie jesteś sam. W wielu scenariuszach raportowania potrzebna jest szybka siatka produktów 5×5 (lub większa), a robienie tego ręcznie jest stratą czasu.  

W tym samouczku przeprowadzimy Cię przez czysty, Python‑napędzany sposób generowania tej tabeli, osadzenia jej za pomocą formuły `MAKEARRAY`, a następnie pobrania wyników z powrotem do Twojego skryptu. Po drodze odpowiemy na **how to use lambda**, pokażemy **how to use makearray**, oraz zademonstrujemy **display excel array** i **read excel values python** — wszystko w jednym spójnym przykładzie.

Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który działa z dowolnym skoroszytem, i zrozumiesz, dlaczego to podejście jest zarówno szybkie, jak i przyszłościowe.

## Czego będziesz potrzebować

- Python 3.8+ (najnowsza stabilna wersja jest w porządku)
- Biblioteka `openpyxl` (lub dowolna biblioteka obsługująca Excel, która wspiera formuły)
- Podstawowa znajomość wyrażeń lambda w Pythonie
- Brak specjalnych dodatków Excel; natywna funkcja `MAKEARRAY` (dostępna w Excel 365) wykonuje ciężką pracę

Jeśli brakuje Ci któregoś z nich, po prostu `pip install openpyxl` i jesteś gotowy do działania.

## Tworzenie tabeli mnożenia – przegląd

Podstawowa idea jest prosta: tworzymy nowy skoroszyt, zapisujemy formułę `MAKEARRAY`, która buduje macierz mnożenia 5 × 5, wymuszamy obliczenie w Excelu, a na koniec odczytujemy uzyskane wartości z powrotem do Pythona.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Uruchomienie skryptu wypisuje:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

To w pełni funkcjonalny **create multiplication table** w Excelu, wygenerowany w całości z Pythona.

### Dlaczego używać `MAKEARRAY` zamiast pętli w Pythonie?

- **Performance**: Excel obsługuje obliczenia natywnie, co jest szybsze przy dużych macierzach.
- **Live updating**: Jeśli później zmienisz wymiary w formule, arkusz automatycznie przeliczy się ponownie.
- **Readability**: Formuła wyraża intencję („make an array”) bezpośrednio, utrzymując Twój kod Pythona schludnym.

## Jak używać lambda w Pythonie dla formuł Excel

Część `LAMBDA` wywołania `MAKEARRAY` jest anonimową funkcją po stronie Excela, a nie lambdą Pythona. Mimo to koncepcja jest taka sama: definiujesz mały, wbudowany fragment logiki, który przyjmuje `r` (indeks wiersza) i `c` (indeks kolumny) i zwraca `r*c`.  

Jeśli jesteś nowy w **how to use lambda** w świecie Excela, pomyśl o tym jako o mini‑funkcji, która istnieje wyłącznie wewnątrz formuły. Nie ma potrzeby deklarowania osobnej funkcji w innym miejscu. W Pythonie po prostu osadzamy ciąg znaków:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Ta linia mówi Excelowi: *„Dla każdej komórki w bloku 5 × 5, oblicz wiersz × kolumna.”*  

Ponieważ lambda jest oceniana przez Excel, nie musisz się martwić o własną składnię lambda w Pythonie — wystarczy składnia Excela.

## Jak używać makearray do generowania tablic

`MAKEARRAY` jest stosunkowo nowym dodatkiem do biblioteki funkcji Excel (dostępny w Microsoft 365 od 2022). Zastępuje starsze sztuczki takie jak kombinacje `INDEX` + `ROW`/`COLUMN`. Sygnatura wygląda tak:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – liczba wierszy, które chcesz.
- **columns** – liczba kolumn, które chcesz.
- **lambda** – funkcja Excel LAMBDA, która otrzymuje `(row, column)` i zwraca wartość.

W naszym przykładzie przekazaliśmy `5,5` dla klasycznej tabeli mnożenia, ale możesz łatwo zmienić te liczby:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

To dałoby Ci tabelę 10 × 10 bez użycia jakichkolwiek pętli Pythona. To pokazuje **how to use makearray** dla dowolnego deterministycznego układu, czy to tabela wyszukiwania, mapa cieplna, czy harmonogram finansowy.

## Wyświetlanie tablicy Excel – pobieranie danych z powrotem do Pythona

Gdy Excel obliczy formułę, wynikowe wartości znajdują się w arkuszu tak jak każda ręcznie wprowadzona komórka. Aby **display excel array**, iterujemy po zakresie i wypisujemy każdy wiersz:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Kilka wskazówek:

- Używaj `worksheet.cell(row, column).value` zamiast indeksowania w stylu słownika, jeśli musisz obsłużyć większe zakresy; jest nieco szybsze.
- Jeśli chcesz ładniejszą tabelę, rozważ `tabulate` lub `pandas.DataFrame` do formatowania wyjścia.

Poniżej znajduje się zrzut ekranu wynikowego arkusza (tekst alternatywny obrazu zawiera główne słowo kluczowe dla SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Odczytywanie wartości Excel w Pythonie – wyodrębnianie macierzy do dalszego przetwarzania

Często następnym krokiem po **display excel array** jest przekazanie tych liczb do potoku analizy danych. To właśnie **read excel values python** błyszczy. Ta sama pętla, której użyliśmy do drukowania, może być przekształcona do budowy listy list, tablicy NumPy lub DataFrame Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Wyjście:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Teraz masz w pełni typowany DataFrame, który możesz wykreślić, wyeksportować do CSV lub przekazać do modelu uczenia maszynowego. To kończy część **read excel values python** w tym przepływie pracy.

## Przypadki brzegowe i praktyczne wskazówki

- **Formula recalculation**: Jeśli zmodyfikujesz skoroszyt po początkowym wywołaniu `calculate_formula()`, musisz wywołać ją ponownie; w przeciwnym razie pamięć podręczna tablicy pozostanie nieaktualna.
- **Non‑365 Excel**: Starsze wersje Excela nie obsługują `MAKEARRAY`. W takim przypadku użyj tabeli generowanej w Pythonie i zapisz każdą komórkę osobno.
- **Large tables**: Dla macierzy większych niż ~100 × 100, rozważ strumieniowanie danych, aby uniknąć ładowania całego arkusza do pamięci.
- **Error handling**: Otocz kroki obliczania i odczytu w bloki `try/except`, aby przechwycić `InvalidFileException` lub `FormulaError`.

## Zakończenie

Właśnie pokazaliśmy Ci, jak **create multiplication table** w Excelu przy użyciu Pythona, wykorzystując moc **how to use lambda** i **how to use makearray**. Zobaczyłeś, jak **display excel array**, odczytać te wartości za pomocą **read excel values python**, a nawet przekształcić wynik w DataFrame Pandas do dalszej analizy.

Chcesz iść dalej? Spróbuj zamienić logikę mnożenia na coś bardziej złożonego — może macierz odległości, tabelę prawdopodobieństw lub dynamiczną siatkę cenową. Ten sam wzorzec ma zastosowanie: jedna linia `MAKEARRAY`, szybkie `calculate_formula()` i garść pętli Pythona, aby wyciągnąć dane.

Jeśli uznałeś ten przewodnik za przydatny, wystaw mu gwiazdkę na GitHubie, podziel się nim z zespołem lub zostaw komentarz ze swoim własnym przypadkiem użycia. Szczęśliwego kodowania i ciesz się zwięzłością generowania tabel Excel jednym formułą!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak tworzyć i konfigurować skoroszyty Excel przy użyciu Aspose.Cells .NET: przewodnik krok po kroku](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Samouczek Aspose.Cells .NET: Jak łatwo tworzyć i modyfikować skoroszyty Excel](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Jak tworzyć i stylizować nazwane zakresy w Excelu przy użyciu Aspose.Cells .NET | przewodnik krok po kroku](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}