---
category: general
date: 2026-07-13
description: Jak używać WRAPCOLS w C# do konwersji tablicy na kolumny, zastosowania
  formuły tablicowej w Excelu i programowego tworzenia skoroszytu Excel — wszystko
  w jasnych krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: pl
lastmod: 2026-07-13
og_description: Jak używać WRAPCOLS w C# pozwala szybko przekształcić tablicę w kolumny,
  zastosować formułę tablicową w stylu Excela i ocenić wynik programowo.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Jak używać WRAPCOLS w C# – szybkie tworzenie skoroszytu Excel
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak używać WRAPCOLS – Kompletny przewodnik po automatyzacji Excel w C#
url: /pl/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać WRAPCOLS – Kompletny przewodnik po automatyzacji Excel w C#

Zastanawiałeś się kiedyś **jak używać WRAPCOLS**, gdy potrzebujesz przekształcić płaską listę w schludną tabelę w pliku Excel generowanym z C#? Nie jesteś jedyny. Niezależnie od tego, czy budujesz silnik raportowania, eksportujesz wyniki ankiet, czy po prostu bawisz się danymi, funkcja WRAPCOLS może natychmiast przekształcić tablicę w określoną liczbę kolumn.  

W tym samouczku przeprowadzimy Cię przez cały proces: od **tworzenia skoroszytu Excel programowo** po **zastosowanie formuły tablicowej w stylu Excel**, a na końcu **ewaluację formuły w C#**. Po zakończeniu będziesz w stanie **convert array to columns** w jednej linii kodu, bez ręcznych operacji na poszczególnych komórkach.

> **Co otrzymasz:** działający przykład kodu, wyjaśnienie każdego kroku, wskazówki dotyczące typowych pułapek oraz sugestie rozszerzenia rozwiązania.

---

## Wymagania wstępne

Before we dive in, make sure you have:

- .NET 6.0+ (lub dowolny aktualny runtime .NET)
- IDE C# (Visual Studio, Rider lub VS Code)
- Bibliotekę **Aspose.Cells for .NET** (bezpłatna wersja próbna działa dobrze) – to najłatwiejszy sposób na manipulację plikami Excel bez konieczności instalacji Excela.
- Podstawową znajomość składni C# i formuł Excel.

If you prefer a different library (e.g., EPPlus or ClosedXML), the core ideas stay the same—just swap the API calls.

## Krok 1: Skonfiguruj projekt i dodaj bibliotekę Excel

Na początek, utwórz nową aplikację konsolową i pobierz Aspose.Cells przez NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Wskazówka:** Użyj flagi `--version`, aby zablokować znaną stabilną wersję, np. `Aspose.Cells 24.9`.

Teraz otwórz `Program.cs`. Zacznijmy od dodania wymaganych przestrzeni nazw:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Posiadanie odwołania do biblioteki zapewnia, że możemy **tworzyć skoroszyt Excel programowo** i pracować z formułami.

## Krok 2: Utwórz nowy skoroszyt i docelową komórkę

Następnie utwórz nowy skoroszyt i wybierz komórkę, w której będzie znajdować się formuła WRAPCOLS. W terminologii Excela, komórka **A1** to wiersz 0, kolumna 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Dlaczego to robimy? Obiekt `Workbook` jest kontenerem dla wszystkich arkuszy, stylów i obliczeń. Poprzez wyraźne odwołanie do komórki, utrzymujemy kod czytelny i unikamy „magicznych liczb” w dalszej części.

## Krok 3: Wstaw formułę tablicową WRAPCOLS

Teraz przychodzi serce samouczka — **jak używać WRAPCOLS**. Funkcja przyjmuje tablicę i liczbę kolumn, a następnie zwraca dwuwymiarowy zakres. W składni Excela wygląda to tak:

```
=WRAPCOLS({1,2,3,4}, 2)
```

To instruuje Excel, aby ułożył liczby 1‑4 w **2 kolumny**, co daje wynik:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Aby osadzić tę formułę w C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Zauważ, że używamy **ciągu znaków**, który odzwierciedla to, co wpisałbyś w pasek formuły Excela. To jest krok **apply array formula excel**, a Aspose.Cells automatycznie traktuje go jako formułę tablicową, ponieważ WRAPCOLS zwraca zakres.

## Krok 4: Wymuś obliczenie, aby formuła została wyliczona

Excel zazwyczaj przelicza leniwie — tylko przy otwarciu pliku. Ponieważ chcemy odczytać wynik od razu, musimy wywołać przeliczenie:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Wywołanie `Calculate()` to akcja **evaluate excel formula c#**, która zmusza silnik do obliczenia każdej formuły, w tym naszej tablicowej WRAPCOLS. Bez tego wywołania, `targetCell.Value` nadal byłoby `null`.

## Krok 5: Pobierz i zweryfikuj wynik

Teraz, gdy skoroszyt został przeliczony, możemy pobrać wartość(i) z komórek zajętych przez tablicę. Górna‑lewa komórka (A1) zawiera pierwszy element, a sąsiednie komórki resztę. Odczytajmy cały blok 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Po uruchomieniu programu, konsola powinna wyświetlić:

```
1   3
2   4
```

Ten wynik potwierdza, że pomyślnie **convert array to columns** przy użyciu WRAPCOLS.

## Krok 6: Zapisz skoroszyt (opcjonalnie, ale przydatne)

Jeśli chcesz otworzyć plik w Excelu i zobaczyć formułę na żywo, po prostu zapisz go:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Otwarcie pliku pokaże formułę WRAPCOLS w A1 oraz wypełniony zakres 2‑kolumnowy pod nią. Ten krok jest przydatny do debugowania lub udostępniania pliku końcowym użytkownikom.

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję więcej niż dwóch kolumn?

Po prostu zmień drugi argument WRAPCOLS. Na przykład, `=WRAPCOLS({1,2,3,4,5,6},3)` wygeneruje trzy kolumny:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Zaktualizuj odpowiednio linię w C#:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Czy mogę podać dynamiczny zakres zamiast sztywno zakodowanej tablicy?

Oczywiście. Możesz zbudować ciąg tablicowy programowo:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

W ten sposób możesz **apply array formula excel** w locie, co jest idealne dla raportów o zmiennych rozmiarach danych.

### Co z obsługą błędów?

Jeśli formuła jest niepoprawna, `Calculate()` rzuci `CellsException`. Umieść obliczenia w bloku try/catch i zaloguj błąd:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Czy to działa w starszych wersjach Excela?

WRAPCOLS został wprowadzony w Excel 365/2021. Gdy zapiszesz plik w starszym formacie `.xls`, formuła może zostać utracona. Trzymaj się formatu `.xlsx`, jeśli potrzebujesz, aby funkcja przetrwała poza silnikiem C#.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do skopiowania program:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Uruchom `dotnet run`, a zobaczysz wydrukowaną macierz, a następnie potwierdzenie, że plik `.xlsx` istnieje.

## Podsumowanie i kolejne kroki

Omówiliśmy **how to use WRAPCOLS**, aby **convert array to columns**, przedstawiliśmy technikę **apply array formula excel** z C#, wymusiliśmy obliczenie, aby **evaluate excel formula c#**, oraz zapisaliśmy wynik do dalszego wykorzystania.  

Jeśli masz ochotę na więcej:

- **Dynamic column counts:** niech liczba kolumn będzie zmienną wprowadzoną przez użytkownika.
- **Styling the output:** zastosuj czcionki, obramowania lub formatowanie warunkowe za pomocą Aspose.Cells po obliczeniu.
- **Combining with other functions:** zagnieźdź WRAPCOLS wewnątrz `LET` lub `FILTER`

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Aspose.Cells .NET&#58; How to Create & Style Excel Workbooks Programmatically](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}