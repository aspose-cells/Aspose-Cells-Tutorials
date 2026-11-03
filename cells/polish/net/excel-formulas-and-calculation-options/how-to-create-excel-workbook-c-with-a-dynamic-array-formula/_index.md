---
category: general
date: 2026-10-01
description: Szybko utwórz skoroszyt Excel w C# i poznaj przykład formuły dynamicznej
  tablicy, aby zapisać formułę Excel w C# przy użyciu Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: pl
lastmod: 2026-10-01
og_description: Szybko utwórz skoroszyt Excel w C# i zobacz przykład formuły tablicowej
  dynamicznej, który pokazuje, jak pisać formuły Excel w C# przy użyciu Aspose.Cells.
  Postępuj zgodnie z instrukcją krok po kroku, aby wygenerować, obliczyć i zapisać
  plik.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Utwórz skoroszyt Excel w C# z dynamiczną formułą tablicową
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak utworzyć skoroszyt Excel w C# z dynamiczną formułą tablicową
url: /pl/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt Excel w C# z dynamiczną formułą tablicową

Jeśli potrzebujesz **create Excel workbook C#** programowo, ten przewodnik pokazuje dokładnie, jak to zrobić przy użyciu Aspose.Cells. Otrzymasz także **dynamic array formula example**, który demonstruje najlepszy sposób **write Excel formula C#** dla nowoczesnych funkcji Excela, takich jak `SORT`.

Tworzenie pliku Excel z C# wymagało wcześniej użycia COM interop lub ręcznego generowania XML, co było kruche i trudne w utrzymaniu. Po zakończeniu tego samouczka będziesz mieć w pełni funkcjonalny skoroszyt, który automatycznie oblicza dynamiczną tablicę, i zrozumiesz, dlaczego takie podejście jest niezawodne w automatyzacji klasy produkcyjnej.

## Wymagania wstępne

- .NET 6.0 lub nowszy zainstalowany (kod działa również z .NET Core i .NET Framework)
- Ważna licencja Aspose.Cells lub darmowy klucz ewaluacyjny
- Visual Studio 2022 (lub dowolne IDE obsługujące C#)
- Podstawowa znajomość składni C# i formuł Excel

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Cells`, które możesz dodać przy użyciu:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Skonfiguruj projekt C# i odwołanie do Aspose.Cells

Utwórz nową aplikację konsolową i dodaj odwołanie do Aspose.Cells. Ten krok jest niezbędny, ponieważ biblioteka udostępnia `Workbook`, `Worksheet` oraz silnik obliczeniowy potrzebny do **write Excel formula C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Dlaczego to ważne:** Aspose.Cells abstrahuje szczegóły niskopoziomowego OpenXML, pozwalając skupić się na logice biznesowej, a nie na niuansach formatu pliku.

## Krok 2: Utwórz skoroszyt Excel i uzyskaj pierwszy arkusz

Teraz **create Excel workbook C#** poprzez utworzenie obiektu `Workbook`. Domyślny skoroszyt zawiera pojedynczy arkusz, który pobieramy do dalszych operacji.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Wskazówka:** Jeśli potrzebujesz wielu arkuszy, wywołaj `workbook.Worksheets.Add()` przed ich dostępem.

## Krok 3: Wypełnij dane źródłowe dla dynamicznej tablicy

Funkcje tablicowe dynamiczne, takie jak `SORT`, wymagają zakresu źródłowego. Wypełnijmy komórki *A2:A10* nieposortowanymi liczbami, aby formuła `SORT` mogła pokazać swoje działanie.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Dlaczego to robimy:** Dostarczenie konkretnych danych pozwala zobaczyć **dynamic array formula example** w działaniu, bez potrzeby zewnętrznych plików wejściowych.

## Krok 4: Wpisz dynamiczną formułę tablicową do komórki A1

Oto rdzeń części **write Excel formula C#**. Przypisujemy formułę `SORT` do komórki *A1*. Ponieważ `SORT` jest funkcją dynamicznej tablicy, Excel automatycznie rozleje posortowane wyniki do kolejnych komórek.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Wyjaśnienie:**  
> - `worksheet.Cells[0, 0]` wskazuje komórkę **A1** (wiersz 0, kolumna 0).  
> - Ciąg znaków `=SORT(A2:A10)` jest standardową formułą Excel. Aspose.Cells parsuje ją tak samo jak Excel, zapewniając pełne wsparcie dla nowoczesnych funkcji dynamicznych tablic.

## Krok 5: Przelicz skoroszyt, aby formuła wypełniła się automatycznie

Aspose.Cells nie przelicza formuł automatycznie przy zapisie. Musisz wyraźnie wywołać przeliczenie, aby zobaczyć rozlane wyniki.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

Po tym wywołaniu komórki **A1:A9** będą zawierały posortowaną listę: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Weryfikacja wyniku (oczekiwany wynik)

Możesz wydrukować rozlane wartości w konsoli, aby potwierdzić, że obliczenia zakończyły się sukcesem:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Oczekiwany wynik w konsoli**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Uwaga o przypadkach brzegowych:** Jeśli zakres źródłowy zawiera dane nienumeryczne, `SORT` posortuje je leksykograficznie. Zawsze waliduj typy danych przed zastosowaniem funkcji wyłącznie numerycznych.

## Krok 6: Zapisz skoroszyt na dysku (opcjonalnie)

Zachowanie pliku pozwala otworzyć go w Excelu i zobaczyć dynamiczną tablicę wizualnie. Ten krok nie jest wymagany do samego obliczenia, ale jest przydatny przy debugowaniu i dystrybucji.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Po otwarciu *SortedNumbers.xlsx* w Excel 365 lub nowszym zobaczysz, że posortowana lista automatycznie rozlewa się od **A1** w dół — dokładnie to, co **dynamic array formula example** wygenerował z C#.

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny, gotowy do uruchomienia program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Uruchom program (`dotnet run`), a zobaczysz wydrukowane posortowane liczby, a następnie potwierdzenie, że plik został zapisany.

## Częste pytania i warianty

### Co zrobić, jeśli potrzebuję użyć innej funkcji dynamicznej tablicy?

Zastąp ciąg formuły dowolną inną funkcją dynamicznej tablicy, np. `=FILTER(A2:A10, B2:B10>10)` lub `=UNIQUE(A2:A10)`. Ten sam wzorzec **write Excel formula C#** ma zastosowanie:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Jak obsłużyć formuły odwołujące się do innych arkuszy?

Odwołaj się do innego arkusza, podając jego nazwę:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells automatycznie rozwiązuje odwołania między arkuszami podczas `workbook.Calculate()`.

### Czy mogę wyłączyć automatyczne przeliczanie i przeliczyć później?

Tak. Ustaw tryb przeliczania skoroszytu na ręczny:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Poprawia to wydajność, gdy aktualizujesz tysiące komórek przed ostatecznym przeliczeniem.

## Podsumowanie

Teraz wiesz, jak **create Excel workbook C#** przy użyciu Aspose.Cells, wstawić **dynamic array formula example** i **write Excel formula C#**, które automatycznie rozlewają wyniki. Kompletny zestaw rozwiązań obejmuje konfigurację projektu, przygotowanie danych, wstawianie formuły, wymuszone przeliczanie, weryfikację oraz opcjonalne zapisywanie pliku.

Od tego momentu możesz badać bardziej zaawansowane scenariusze: łączenie wielu funkcji dynamicznych tablic, stosowanie własnych formatów liczbowych lub integrację generowania skoroszytu z API webowym. Pamiętaj, aby zawsze walidować dane wejściowe przed zastosowaniem formuł i korzystać z bogatego silnika obliczeniowego Aspose.Cells do niezawodnego przetwarzania Excel po stronie serwera. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}