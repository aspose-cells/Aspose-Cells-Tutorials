---
category: general
date: 2026-10-10
description: Konwertuj Excel na PowerPoint i ustaw obszar wydruku w C# przy użyciu
  Aspose.Cells – dowiedz się, jak eksportować Excel, ustawiać obszar wydruku i generować
  plik PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: pl
lastmod: 2026-10-10
og_description: Konwertuj Excel na PowerPoint za pomocą Aspose.Cells. Ten samouczek
  pokazuje, jak ustawić obszar wydruku, wyeksportować Excel i utworzyć plik PPTX w
  C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Konwertuj Excel na PowerPoint – pełny przewodnik dla programistów C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Konwertuj Excel na PowerPoint i ustaw obszar wydruku
url: /pl/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj Excel do PowerPoint i ustaw obszar wydruku

Jeśli potrzebujesz **convert Excel to PowerPoint**, ten przewodnik pokazuje dokładnie, jak to zrobić w C#. Definiując najpierw obszar wydruku, kontrolujesz, które komórki pojawią się na każdym slajdzie, a końcowy plik PPTX odpowiada Twoim oczekiwaniom co do układu. Rozwiązanie odpowiada również na pytania „how to export Excel” i „how to set print area”, używając tej samej bazy kodu.

W tym samouczku:

* Wczytasz istniejący skoroszyt.
* Ustawisz obszar wydruku dla arkusza (krok **set print area excel**).
* Skonfigurujesz opcje konwersji dla wyjścia PowerPoint.
* Wygenerujesz plik **convert excel to pptx** w jednym wywołaniu metody.

Wszystkie wymagane kody są dołączone, więc możesz je skopiować, wkleić i uruchomić od razu.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **.NET 6.0 or later** | Próbka celuje w .NET 6+, ale dowolna wersja .NET obsługująca C# 10 działa. |
| **Aspose.Cells for .NET** | Ta biblioteka dostarcza `Workbook`, `ImageOrPrintOptions` i metodę `ConvertToPdf` (używaną dla PPTX). Zainstaluj ją przez NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | Tutorial używa `input.xlsx`. Umieść go w folderze, do którego możesz odwołać się w kodzie. |
| **Write permission to the output folder** | Program zapisuje `output.pptx`. Upewnij się, że katalog istnieje i ma prawa zapisu. |

> **Pro tip:** Jeśli pracujesz z wieloma arkuszami, powtórz krok obszaru wydruku dla każdego arkusza przed konwersją.

## Krok 1: Utwórz nowy projekt konsolowy C#

Otwórz terminal lub okno PowerShell i uruchom:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

To tworzy nowy projekt o nazwie **ExcelToPowerPointDemo** i dodaje pakiet Aspose.Cells, który jest podstawową zależnością dla **how to export Excel** do innych formatów.

## Krok 2: Napisz kod konwersji

Zastąp zawartość pliku `Program.cs` poniższym kompletnym przykładem. Kod demonstruje **convert excel to powerpoint**, pokazuje **how to set print area** i tworzy plik **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Dlaczego każdy element ma znaczenie

* **Loading the workbook** – To jest pierwszy krok w każdym scenariuszu **how to export Excel**. `Workbook` odczytuje plik do pamięci, dając pełny dostęp do arkuszy, komórek i formatowania.
* **Setting the print area** – Przypisując `PageSetup.PrintArea`, informujesz Aspose.Cells, które komórki mają być renderowane. To jest sedno **set print area excel**; bez tego cały arkusz zostałby wyeksportowany, co może skutkować ogromnymi, nieczytelnymi slajdami.
* **Choosing `SaveFormat.Pptx`** – Obiekt `ImageOrPrintOptions` pozwala przełączać formaty wyjściowe. Ustawienie `SaveFormat` na `Pptx` uruchamia pipeline **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Mimo nazwy metody, gdy `SaveFormat` jest ustawiony na `Pptx`, biblioteka generuje plik PowerPoint. To zalecany sposób **convert excel to powerpoint** w jednym wywołaniu.

## Krok 3: Uruchom program

Z folderu projektu wykonaj:

```bash
dotnet run
```

Jeśli wszystko jest poprawnie skonfigurowane, powinieneś zobaczyć wyjście konsoli podobne do:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Otwórz `output.pptx` w Microsoft PowerPoint lub dowolnym kompatybilnym przeglądarce. Każdy slajd odpowiada wydrukowanej stronie arkusza, ograniczonej do zakresu, który zdefiniowałeś.

## Obsługa wielu arkuszy

Jeśli Twój skoroszyt zawiera więcej niż jeden arkusz i chcesz, aby każdy arkusz miał własny zestaw slajdów, przeiteruj kolekcję:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Ten wzorzec pokazuje **how to export Excel** dane arkusz po arkuszu, jednocześnie **setting print area** indywidualnie.

## Przypadki brzegowe i wskazówki najlepszych praktyk

| Sytuacja | Zalecane podejście |
|-----------|----------------------|
| **Very large worksheets** | Zredukuj obszar wydruku lub zwiększ `HorizontalResolution`/`VerticalResolution`, aby utrzymać rozmiar PPTX w rozsądnych granicach. |
| **Different page orientations** | Ustaw `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` przed konwersją. |
| **Custom slide size** | Użyj `conversionOptions.OnePagePerSheet = false;` i dostosuj `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Otocz kod ładowania w blok `try { … } catch (FileNotFoundException)`, aby zapewnić czytelny komunikat o błędzie. |
| **Non‑ASCII characters** | Upewnij się, że skoroszyt jest zapisany w kodowaniu UTF‑8; Aspose.Cells obsługuje Unicode automatycznie. |

## Pełny kod źródłowy do odniesienia

Poniżej znajduje się cały program, włącznie z dyrektywami `using` i komentarzami. Zapisz go jako `Program.cs` w projekcie utworzonym w **Krok 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Oczekiwany wynik

Uruchomienie programu tworzy plik PowerPoint (`output.pptx`), który zawiera:

* Jeden slajd na każdą wydrukowaną stronę arkusza.
* Tylko komórki w zakresie **A1:G30** widoczne na każdym slajdzie.
* Zachowane formatowanie (czcionki, kolory, obramowania) tak jak w Excelu.

Otwórz plik w PowerPoint, aby zweryfikować, że układ odpowiada zdefiniowanemu obszarowi wydruku.

## Zakończenie

Teraz wiesz, jak **convert Excel to PowerPoint** jednocześnie precyzyjnie **set print area excel** przy użyciu Aspose.Cells w C#. Poradnik obejmował **how to export Excel**, pokazał **how to set print area** i przedstawił pełny **convert excel to pptx**.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak ustawić obszar wydruku w Excelu przy użyciu Aspose.Cells dla .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ustaw obszar wydruku w Excelu i eksportuj do PowerPoint – przewodnik krok po kroku](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Ustaw obszar wydruku Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}