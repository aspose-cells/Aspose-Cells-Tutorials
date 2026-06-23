---
category: general
date: 2026-06-08
description: Eksportuj zakres Excela jako obraz przy użyciu C# i Aspose.Cells. Dowiedz
  się, jak zapisać arkusz Excela jako obraz w kilku prostych krokach.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: pl
og_description: Eksportuj zakres Excela jako obraz w C#. Ten poradnik pokazuje, jak
  szybko i niezawodnie zapisać arkusz Excela jako obraz.
og_title: Eksportuj zakres Excela jako obraz – Kompletny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Eksport zakresu Excela jako obrazu – Kompletny przewodnik C#
url: /pl/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport zakresu Excel jako obrazu – Kompletny przewodnik C#

Kiedykolwiek potrzebowałeś **export Excel range as image**, ale nie byłeś pewien, którego wywołania API użyć? Nie jesteś sam. Niezależnie od tego, czy tworzysz pulpit nawigacyjny raportowy, czy potrzebujesz migawki tabeli przestawnej do slajdu PowerPoint, przekształcenie bloku komórek w PNG to przydatny trik.

W tym przewodniku przeprowadzimy Cię przez samodzielny przykład, który nie tylko **export excel range as image**, ale także pokaże, jak **save excel worksheet as image** dla całego arkusza. Bez zewnętrznych skryptów, tylko czysty C# i Aspose.Cells, więc możesz skopiować‑wkleić kod i od razu zobaczyć działanie.

## Co się nauczysz

- Załadujesz istniejący skoroszyt i znajdziesz określony zakres (tabela przestawna lub dowolny blok komórek).  
- Skonfigurujesz opcje eksportu obrazu, takie jak format, rozdzielczość i skalowanie.  
- Wyeksportujesz pojedynczy zakres do PNG, JPEG lub BMP.  
- Rozszerzysz tę samą logikę, aby **save excel worksheet as image** w jednym wierszu.  
- Otrzymasz wskazówki dotyczące obsługi wielu tabel przestawnych, dużych zakresów i typowych pułapek.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+).  
- Aspose.Cells for .NET ≥ 23.9 (możesz pobrać darmową wersję próbną ze strony Aspose).  
- Podstawowa znajomość C# i operacji I/O na plikach.  

Jeśli masz to wszystko, zanurzmy się.

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Najpierw utwórz nową aplikację konsolową (lub wstaw kod do istniejącego projektu). Dodaj pakiet NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

Następnie zaimportuj wymagane przestrzenie nazw:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro tip:** Trzymaj instrukcje `using` na początku pliku; ułatwia to przeglądanie kodu — szczególnie gdy później dodasz kolejne funkcje Aspose.

## Krok 2: Załaduj skoroszyt zawierający docelowy zakres

Potrzebujesz pliku skoroszytu na dysku. Zamień `YOUR_DIRECTORY/input.xlsx` na rzeczywistą ścieżkę do swojego pliku.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Dlaczego ten krok jest ważny: obiekt `Workbook` jest punktem wejścia dla każdej operacji Aspose.Cells. Bez niego nie możesz odwołać się do arkuszy, zakresów ani tabel przestawnych.

## Krok 3: Zidentyfikuj zakres do eksportu

Masz dwa typowe scenariusze:

1. **Konkretna tabela przestawna** – kod, który podałeś, używa `PivotTables[0].PivotTableRange`.  
2. **Dowolny blok komórek** – możesz użyć `worksheet.Cells.CreateRange("B2:D10")`.

Poniżej obsługujemy oba przypadki, pozwalając Ci wybrać ten, który pasuje do Twojej sytuacji.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Dlaczego najpierw sprawdzamy tabele przestawne:** Wiele plików raportowych opiera się na dynamicznych danych przestawnych. Jeśli ich nie ma, rozwiązanie awaryjne zapewnia, że tutorial nadal działa.

## Krok 4: Skonfiguruj opcje eksportu obrazu

Aspose.Cells daje precyzyjną kontrolę nad wyjściowym obrazem. Najczęstsze ustawienia to format, rozdzielczość (DPI) oraz czy uwzględnić linie siatki.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Możesz przełączyć na `ImageFormat.Jpeg` lub `ImageFormat.Bmp`, jeśli Twój system docelowy preferuje te typy. Ustawienie DPI ma znaczenie, gdy osadzasz obraz w wysokiej rozdzielczości PDF‑ach lub prezentacjach.

## Krok 5: Eksportuj zakres (lub cały arkusz) jako obraz

Teraz dzieje się magia. Metoda `ToImage` zapisuje wizualną reprezentację zakresu bezpośrednio na dysk.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Co robi kod

- `exportRange.ToImage` przechwytuje tylko komórki znajdujące się w określonym zakresie (tabela przestawna lub własny blok).  
- `worksheet.ToImage` przechwytuje *cały* widoczny obszar arkusza, efektywnie **save excel worksheet as image**.  

Oba wywołania respektują wcześniej ustawione opcje — więc otrzymasz pliki PNG z rozdzielczością 300 DPI.

## Obsługa przypadków brzegowych i typowe pytania

### Wiele tabel przestawnych

Jeśli Twój skoroszyt zawiera więcej niż jedną tabelę przestawną, możesz przejść przez nie w pętli:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Bardzo duże zakresy

Eksportowanie ogromnego zakresu (np. tysięcy wierszy) może zużywać dużo pamięci. Zminimalizuj to,:

- Redukując `HorizontalResolution` / `VerticalResolution`.  
- Eksportując w sekcjach (dzieląc zakres na mniejsze bloki).  

### Przezroczyste tło

Jeśli potrzebujesz przezroczystego tła (przydatne przy nakładaniu na strony internetowe), ustaw kolor tła na `Color.Transparent` przed eksportem:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Uprawnienia do plików

Upewnij się, że docelowy katalog istnieje i Twój proces ma uprawnienia do zapisu. W przeciwnym razie `ToImage` zgłosi `IOException`.

## Pełny działający przykład

Łącząc wszystko razem, oto gotowy do uruchomienia program konsolowy:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Oczekiwany wynik** (konsola):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Otwórz wygenerowane pliki PNG, a zobaczysz idealną migawkę wybranego zakresu oraz pełnego arkusza.

## Zakończenie

Właśnie omówiliśmy wszystko, co potrzebne, aby **export excel range as image** oraz jak **save excel worksheet as image** przy użyciu Aspose.Cells i C#. Od ładowania skoroszytu, przez precyzyjne ustawienia obrazu, po obsługę wielu tabel przestawnych — kroki są proste i w pełni powtarzalne.

Następnie możesz:

- Eksperymentować z różnymi wartościami `ImageFormat` (JPEG, BMP).  
- Połączyć obraz z PDF‑em przy użyciu klasy `Document` w celu generowania raportów.  
- Zautomatyzować proces dla partii plików w folderze.

Śmiało dostosuj fragment kodu do własnego przepływu pracy — niezależnie od tego, czy dostarczasz obrazy do API webowego, osadzasz je w e‑mailach, czy tworzysz drukowalne raporty. Szczęśliwego kodowania i niech obrazy mówią za Twoje dane w Excelu!

## Co warto się nauczyć dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny, działający kod wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkryć alternatywne podejścia w własnych projektach.

- [Eksport komórek Excel do obrazu przy użyciu Aspose.Cells .NET: Przewodnik krok po kroku](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}