---
category: general
date: 2026-11-16
description: Dowiedz się, jak rozszerzyć tablicę w Excelu przy użyciu Aspose.Cells,
  funkcji dynamicznych tablic oraz reduktora lambda, a następnie zapisać plik Excel
  z C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: pl
lastmod: 2026-11-16
og_description: Jak rozszerzyć tablicę w Excelu przy użyciu Aspose.Cells, dynamicznych
  funkcji tablicowych i reduktora lambda. Zapoznaj się z pełnym przykładem w C#, aby
  zapisać plik Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Jak rozszerzyć tablicę w Excelu przy użyciu Aspose.Cells – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak rozszerzyć tablicę w Excelu przy użyciu Aspose.Cells
url: /pl/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak rozszerzyć tablicę w Excelu przy użyciu Aspose.Cells

Jeśli potrzebujesz **jak rozszerzyć tablicę** w arkuszu Excel z C#, ten samouczek pokazuje dokładne kroki. Utworzysz skoroszyt Excel, użyjesz dynamicznych funkcji tablicowych takich jak `EXPAND` i `REDUCE`, zastosujesz akumulator **lambda**, a na koniec **zapiszesz plik Excel** na dysku. Podejście działa z Aspose.Cells 23.10 lub nowszym i nie wymaga ręcznej instalacji Excela.

Po zakończeniu tego przewodnika będziesz mieć w pełni funkcjonalny plik `ExpandReduceDemo.xlsx`, który demonstruje moc dynamicznych formuł tablicowych w kontekście programistycznym.

## Czego będziesz potrzebować

- .NET 6.0 (lub dowolna wersja .NET obsługiwana przez Aspose.Cells)
- Pakiet Aspose.Cells dla .NET (`dotnet add package Aspose.Cells`)
- Edytor kodu lub IDE (Visual Studio, VS Code, Rider itp.)

Nie jest wymagana dodatkowa interakcja COM ani instalacja Office, ponieważ Aspose.Cells obsługuje format pliku wewnętrznie.

## Krok 1: Utwórz skoroszyt Excel

Pierwszym zadaniem jest **utworzenie skoroszytu Excel** w pamięci. Aspose.Cells udostępnia klasę `Workbook`, która reprezentuje cały plik XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Dlaczego to ważne:** Utworzenie obiektu `Workbook` daje czyste płótno. Domyślny arkusz jest już przygotowany, więc nie musisz dodawać go ręcznie, chyba że potrzebujesz wielu arkuszy.

## Krok 2: Wstaw stałą tablicę pionową

Silnik dynamicznych tablic w Excelu może pracować z dosłownymi stałymi tablicowymi. Umieścimy pionową tablicę `{1;2;3;4;5}` w komórce **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Wskazówka:** średnik (`;`) oddziela wiersze w stałej, podczas gdy przecinek (`,`) oddziela kolumny. To odzwierciedla składnię Excela.

## Krok 3: Rozszerz tablicę do macierzy

Teraz odpowiadamy na kluczowe pytanie – **jak rozszerzyć tablicę** – używając funkcji `EXPAND`. Formuła rozszerza jednowierszową (jednokolumnową) tablicę do macierzy 5‑wierszy × 2‑kolumn, zaczynając od **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Dlaczego EXPAND?** `EXPAND(source, rows, cols)` wymusza, aby zakres źródłowy zajmował określony rozmiar, wypełniając pustymi komórkami w razie potrzeby. To najbardziej czytelny sposób generowania większej macierzy z jednej tablicy.

## Krok 4: Zredukuj macierz przy użyciu akumulatora lambda

Funkcja `REDUCE` iteruje po zakresie i agreguje wartości przy użyciu wyrażenia **lambda**. Tutaj sumujemy wartości każdej kolumny do jednej kolumny, umieszczając wynik w **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Jak używać lambda:** `LAMBDA(acc, val, acc+val)` otrzymuje bieżący akumulator (`acc`) oraz następną wartość komórki (`val`). Zwraca nowy akumulator, efektywnie wykonując sumę bieżącą. To pokazuje **jak używać lambda** w formułach Excel z kodu.

## Krok 5: Oblicz formuły, aby wyniki się pojawiły

Aspose.Cells nie ocenia automatycznie formuł po ich ustawieniu. Wywołanie `CalculateFormula` zmusza silnik do obliczenia każdej formuły w skoroszycie.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Uwaga:** Jeśli otworzysz wygenerowany plik w Excelu, wartości będą już widoczne, ponieważ zostały wstępnie obliczone.

## Krok 6: Zapisz plik Excel na dysku

Na koniec, **zapisz plik Excel** używając metody `Save`. Wybierz folder, w którym masz uprawnienia do zapisu.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Oczekiwany rezultat

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Kolumna B** i **C** zawierają macierz 5 × 2 wygenerowaną przez `EXPAND`.
- **Komórka D1** pokazuje `15`, sumę wszystkich liczb, obliczoną przez formułę `REDUCE` + **lambda**.

## Częste pytania i przypadki brzegowe

- **Czy mogę rozszerzyć do większej liczby kolumn niż dostarcza źródło?**  
  Tak. `EXPAND` wypełnia brakujące kolumny pustymi komórkami. To samo działa dla wierszy.

- **Co jeśli źródłowa tablica jest pozioma (`{1,2,3,4,5}`)?**  
  `EXPAND` potraktuje źródło jako pojedynczy wiersz; nadal możesz określić liczbę wierszy i kolumn, aby przekształcić ją.

- **Czy `REDUCE` działa z danymi nienumerycznymi?**  
  Lambda musi zwracać wartość zgodną z typem akumulatora. Dla konkatenacji tekstu możesz użyć `LAMBDA(acc, val, acc & val)`.

- **Czy muszę wywoływać `CalculateFormula` przy każdej zmianie?**  
  Tylko wtedy, gdy potrzebujesz obliczonych wartości przed zapisem. Excel przeliczy przy otwarciu, jeśli to pominiesz.

## Porady profesjonalne

- **Wydajność:** Dla dużych skoroszytów wywołaj `workbook.CalculateFormula` raz po ustawieniu wszystkich formuł, zamiast po każdej komórce.
- **Bezpieczeństwo wersji:** `EXPAND` i `REDUCE` są dostępne w Excel 365 i nowszych. Aspose.Cells implementuje je niezależnie od docelowej wersji Excela, ponieważ silnik obliczeniowy jest wbudowany.
- **Debugowanie formuł:** Użyj `sheet.Cells["B1"].Formula`, aby odczytać dokładny ciąg, który ustawiłeś; pomaga to przy dynamicznym budowaniu formuł.

## Zakończenie

Teraz wiesz **jak rozszerzyć tablicę** w Excelu przy użyciu Aspose.Cells, wykorzystujesz **dynamiczne funkcje tablicowe**, stosujesz **lambda** z `REDUCE` oraz **zapisujesz plik Excel** z C#. Ten kompleksowy przykład można dostosować do bardziej złożonych przekształceń danych, takich jak transpozycja macierzy, sumy skumulowane czy własne agregacje.

---

*Next steps:*  
- Zbadaj inne dynamiczne funkcje, takie jak `FILTER`, `SORT` i `UNIQUE`.  
- Połącz wiele wyrażeń `LAMBDA`, aby tworzyć wielokrotnego użytku funkcje definiowane przez użytkownika.  
- Zintegruj generowanie skoroszytu z API ASP.NET Core w celu tworzenia raportów w locie.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak utworzyć skoroszyt Excel w C# z dynamiczną formułą tablicową](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Jak rozszerzyć tablicę w Excelu i wypełnić szablon](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Jak rozszerzyć tablicę w C# przy użyciu Aspose.Cells – przewodnik krok po kroku](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}