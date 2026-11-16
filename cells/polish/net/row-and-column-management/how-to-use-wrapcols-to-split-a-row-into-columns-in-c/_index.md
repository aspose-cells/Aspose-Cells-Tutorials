---
category: general
date: 2026-11-16
description: Dowiedz się, jak używać WRAPCOLS w C#, aby podzielić wiersz na kolumny,
  zautomatyzować skoroszyt Excela, obliczyć formuły i zapisać plik Excela.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: pl
lastmod: 2026-11-16
og_description: Jak używać WRAPCOLS w C#, aby podzielić wiersz na kolumny, zautomatyzować
  skoroszyt Excel, wykonać obliczenia formuł i zapisać plik Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Jak używać WRAPCOLS w C# – dziel wiersze, obliczaj formuły i zapisuj pliki
  Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Jak używać WRAPCOLS, aby podzielić wiersz na kolumny w C#
url: /pl/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać WRAPCOLS do podziału wiersza na kolumny w C#

Jeśli potrzebujesz **jak używać WRAPCOLS** w projekcie C#, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak podzielić wiersz na kolumny, zautomatyzować skoroszyt Excel, wywołać obliczenia formuł Excel i w końcu zapisać plik Excel w stylu C#.

Praca z Excelem programowo często oznacza obsługę dużych zestawów danych, a funkcja `WRAPCOLS` pozwala przekształcić pojedynczy wiersz w macierz bez ręcznego iterowania. Poniższe kroki obejmują wszystko, czego potrzebujesz – od tworzenia skoroszytu po ostateczne zapisanie pliku – abyś mógł włączyć tę technikę do dowolnej aplikacji .NET.

## Co obejmuje ten tutorial

* Tworzenie nowego skoroszytu i dostęp do jego pierwszego arkusza.  
* Wypełnianie wiersza wartościami kolejno od 1‑20.  
* Zastosowanie formuły Excel `WRAPCOLS` do podziału wiersza na bloki po 5 kolumn.  
* Uruchomienie **excel formula calculation**, aby wynik stał się częścią arkusza.  
* Użycie **save excel file c#** do zapisania skoroszytu na dysku.  

Nie wymaga żadnej zewnętrznej konfiguracji poza biblioteką Aspose.Cells for .NET (lub dowolnym kompatybilnym API obsługującym `WRAPCOLS`). Po zakończeniu przewodnika będziesz mieć plik o nazwie `WrapColsDemo.xlsx`, zawierający cztery wiersze po pięć kolumn każdy, pochodzące z pierwotnych danych w jednym wierszu.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Core 3.1 i .NET Framework 4.7+).  
* Odwołanie do **Aspose.Cells** (dostępne przez NuGet: `Install-Package Aspose.Cells`).  
* Podstawowa znajomość składni C# oraz formuł Excel.  

> **Pro tip:** Jeśli wolisz darmową alternatywę, otwarto‑źródłowa biblioteka EPPlus również obsługuje własne formuły, ale `WRAPCOLS` jest wbudowane wyłącznie w biblioteki implementujące pełny silnik obliczeniowy Excel, takie jak Aspose.Cells.

## Krok 1: Utwórz nowy skoroszyt i pobierz pierwszy arkusz

Pierwszą operacją jest zainicjowanie obiektu `Workbook` i pobranie jego domyślnego arkusza. Ten obiekt reprezentuje cały plik Excel w pamięci.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Tworzenie skoroszytu programowo jest podstawą zadań **automate excel workbook**. Odwołanie `Worksheet` pozwala na bezpośrednią manipulację komórkami.

## Krok 2: Wypełnij pierwszy wiersz wartościami 1‑20

Następnie wypełnij komórki od `A1` do `T1` liczbami od 1 do 20. Prosta pętla `for` zapisuje każdą wartość w odpowiednim indeksie kolumny.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Dlaczego warto wpisywać wartości programowo? Gwarantuje to, że demo zadziała na każdej maszynie bez ręcznego wprowadzania danych, co jest kluczowe przy **automate excel workbook** w procesach wsadowych.

## Krok 3: Zastosuj funkcję WRAPCOLS, aby podzielić wiersz na bloki po 5 kolumn

Teraz używamy formuły Excel `WRAPCOLS`. Przyjmuje ona zakres źródłowy i liczbę kolumn, a następnie zwraca dwuwymiarową tablicę, która „owija” dane źródłowe do określonej liczby kolumn.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Umieszczenie formuły w komórce `A2` mówi Excelowi, aby rozpoczął wyjście od drugiego wiersza. Wynikiem będzie macierz 4 × 5, ponieważ 20 elementów podzielonych na 5 kolumn daje cztery wiersze.

### Jak działa WRAPCOLS

* **Source range** – `A1:T1` zawiera pierwotne 20 wartości.  
* **Column count** – `5` nakazuje Excelowi utworzyć pięć kolumn w każdym wierszu.  
* **Result** – Excel automatycznie wypełnia komórki `A2:E5` opakowanymi danymi.  

Jeśli kiedykolwiek będziesz musiał **split row into columns** z innym rozmiarem bloku, po prostu zmień drugi argument. Na przykład `WRAPCOLS(A1:T1,4)` wygeneruje pięć wierszy po cztery kolumny każdy.

## Krok 4: Oblicz formuły, aby wynik WRAPCOLS został materializowany

Nowo dodana formuła pozostaje nieobliczona, dopóki nie uruchomi się silnik obliczeniowy. Wywołując `CalculateFormula()`, zapewniasz, że krok **excel formula calculation** zapisze rzeczywiste wartości w arkuszu.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Obliczenie jest kluczowe przed **save excel file c#**, ponieważ zapisywany plik musi zawierać wyliczone wartości, a nie sam tekst formuły. Bez tego kroku wynikowy skoroszyt pokazałby `#N/A` lub surową formułę zamiast oczekiwanych liczb.

## Krok 5: Zapisz skoroszyt na dysku

Na koniec utrwal skoroszyt metodą `Save`. Możesz podać dowolną prawidłową ścieżkę; w przykładzie użyto katalogu zastępczego, który powinieneś zamienić na własny.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Wywołanie `Save` demonstruje **save excel file c#** w najprostszej formie. Aspose.Cells automatycznie wybiera format XLSX na podstawie rozszerzenia pliku. Jeśli potrzebujesz starszego pliku `.xls`, zmień odpowiednio rozszerzenie.

### Oczekiwany wynik

Otwórz `WrapColsDemo.xlsx` i zobaczysz:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Pierwotny pojedynczy wiersz został **split row into columns** na cztery wiersze, z pięcioma kolumnami w każdym.

## Pełny kod źródłowy

Połączenie wszystkich kroków daje kompaktowy, samodzielny program:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Skopiuj kod do nowego projektu konsolowego, przywróć pakiet NuGet Aspose.Cells i uruchom. Program utworzy plik Excel na pulpicie w kilka sekund.

## Typowe warianty i przypadki brzegowe

| Situation | Adjustment |
|-----------|------------|
| **Different block size** | Zmień `WRAPCOLS(A1:T1,5)` na `WRAPCOLS(A1:T1, n)`, gdzie `n` to żądana liczba kolumn. |
| **Multiple source rows** | Użyj `WRAPCOLS(A1:A10,5)` aby opakować pionowy zakres w macierz 5‑kolumnową. |
| **Dynamic source range** | Zbuduj ciąg adresu w C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) przed przypisaniem formuły. |
| **Large worksheets** | Wywołaj `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, aby pominąć komórki powodujące błędy i zwiększyć wydajność. |
| **Saving as CSV** | Zamień `workbook.Save(outputPath)` na `workbook.Save(outputPath, SaveFormat.Csv)`. |

Te warianty pokazują, że ten sam **how to use wrapcols** można dostosować do wielu scenariuszy przekształcania danych.

## Wskazówki rozwiązywania problemów

* **Formula not evaluated** – Upewnij się, że wywołujesz `workbook.CalculateFormula()` *po* ustawieniu formuły. Pominięcie tego kroku pozostawi komórkę z surowym tekstem `WRAPCOLS`.  
* **File access denied** – Sprawdź, czy docelowy katalog istnieje i czy proces ma uprawnienia do zapisu. Użycie `Environment.SpecialFolder.Desktop` eliminuje większość problemów z uprawnieniami.  
* **Incorrect number of rows** – Podwójnie sprawdź drugi argument `WRAPCOLS`. Określa on liczbę kolumn, a nie wierszy; wiersze są wyliczane jako całkowita liczba komórek źródłowych podzielona przez tę liczbę kolumn.

## Podsumowanie

Teraz wiesz, **jak używać WRAPCOLS** w C# do **split row into columns**, w pełni **automate excel workbook**, uruchomić **excel formula calculation** i **save excel file c#** przy użyciu jednego, przejrzystego kodu. Technika eliminuje ręczne kopiowanie‑wklejanie i skaluje się bez problemu w dużych potokach przetwarzania danych.

### Kolejne kroki

* Poznaj inne dynamiczne funkcje tablicowe, takie jak `SEQUENCE`, `FILTER` i `UNIQUE`, aby wzbogacić swój zestaw narzędzi automatyzacji Excel.  
* Połącz `WRAPCOLS` z API generującymi wykresy, aby tworzyć gotowe do publikacji raporty.  
* Zintegruj kod z usługą w tle, która przetwarza przesyłane pliki CSV i generuje przekształcone pliki Excel dla dalszej analizy.

Śmiało eksperymentuj z różnymi zakresami źródłowymi i liczbami kolumn – zmień formułę, uruchom ponownie obliczenia i obserwuj natychmiastową aktualizację skoroszytu. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}