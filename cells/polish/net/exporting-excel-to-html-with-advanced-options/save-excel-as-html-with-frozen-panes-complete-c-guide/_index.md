---
category: general
date: 2026-05-04
description: Szybko zapisz plik Excel jako HTML przy użyciu Aspose.Cells dla .NET
  – dowiedz się, jak w kilka minut wyeksportować Excel do HTML z zamrożonymi okienkami.
draft: false
keywords:
- save excel as html
- export excel to html
- convert excel to html
- export excel sheet html
- how to export excel html
language: pl
og_description: Zapisz Excel jako HTML z zamrożonymi okienkami przy użyciu Aspose.Cells.
  Ten przewodnik przeprowadzi Cię przez eksport Excela do HTML, omawiając kod, opcje
  i pułapki.
og_title: Zapisz Excel jako HTML – samouczek C# krok po kroku
tags:
- Aspose.Cells
- C#
- Excel Export
title: Zapisz Excel jako HTML z zamrożonymi okienkami – Kompletny przewodnik C#
url: /pl/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-with-frozen-panes-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz Excel jako HTML – Kompletny przewodnik C#

Kiedykolwiek potrzebowałeś **zapisania Excela jako HTML**, ale obawiałeś się, że zamrożone wiersze lub kolumny znikną? Nie jesteś sam. W tym przewodniku pokażemy, **jak wyeksportować Excel do HTML** zachowując zamrożone okienka, korzystając z popularnej biblioteki Aspose.Cells dla .NET.

Omówimy wszystko – od instalacji pakietu NuGet po dostosowanie `HtmlSaveOptions`, aby wynik wyglądał dokładnie tak jak oryginalny arkusz. Po zakończeniu będziesz mógł **eksportować Excel do HTML**, **konwertować Excel na HTML**, a także odpowiedzieć na pytanie „**jak wyeksportować Excel HTML**?” swoim współpracownikom bez problemu.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- **.NET 6.0** lub nowszy (kod działa również z .NET Framework 4.6+)
- **Visual Studio 2022** (lub dowolne inne IDE)
- **Aspose.Cells for .NET** – zainstaluj przez NuGet (`Install-Package Aspose.Cells`)
- Przykładowy skoroszyt Excel (`sample.xlsx`) zawierający przynajmniej jedno zamrożone okienko

To wszystko – bez dodatkowego COM interop, bez wymogu instalacji Excela. Aspose.Cells obsługuje wszystko w pamięci.

## Krok 1: Utwórz projekt i dodaj Aspose.Cells

Na początek utwórz nowy projekt konsolowy (lub włącz kod do istniejącej aplikacji ASP.NET).

```bash
dotnet new console -n ExcelToHtmlDemo
cd ExcelToHtmlDemo
dotnet add package Aspose.Cells
```

**Dlaczego ten krok jest ważny:** Dodanie pakietu zapewnia dostęp do `Workbook`, `HtmlSaveOptions` oraz flagi `PreserveFreezePanes`, która pozwala zamrożonym wierszom/kolumnom przetrwać konwersję.

## Krok 2: Wczytaj skoroszyt i przygotuj dane (opcjonalnie)

Jeśli już masz plik `.xlsx`, możesz pominąć część generowania danych. W przeciwnym razie, oto szybki sposób na stworzenie arkusza z zamrożonym górnym wierszem i lewą kolumną.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and access the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Report";

        // Populate some data
        for (int row = 0; row < 30; row++)
        {
            for (int col = 0; col < 10; col++)
            {
                ws.Cells[row, col].PutValue($"R{row + 1}C{col + 1}");
            }
        }

        // Freeze the first row and first column (A1 is top‑left corner)
        ws.FreezedRows = 1;   // freeze row 1
        ws.FreezedColumns = 1; // freeze column A

        // Save the workbook to a temporary file for later reuse
        string tempPath = "sample.xlsx";
        wb.Save(tempPath);
        Console.WriteLine($"Workbook created at {tempPath}");
    }
}
```

Uruchomienie tego fragmentu tworzy `sample.xlsx` z zamrożonym okienkiem. Jeśli już posiadasz plik, po prostu wskaż go w następnym kroku.

## Krok 3: Skonfiguruj HtmlSaveOptions, aby zachować zamrożone okienka

Teraz przechodzimy do sedna tutorialu: **eksport Excel do HTML** przy zachowaniu zamrożonego widoku. Klasa `HtmlSaveOptions` daje nam precyzyjną kontrolę.

```csharp
using Aspose.Cells;
using System;

class Exporter
{
    static void Main()
    {
        // Load the workbook (replace with your own path if needed)
        string sourcePath = "sample.xlsx";
        Workbook wb = new Workbook(sourcePath);

        // Step 3‑1: Create HtmlSaveOptions and enable frozen pane preservation
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // This flag makes sure the frozen rows/columns stay frozen in the HTML output
            PreserveFreezePanes = true,

            // Optional: embed CSS directly (makes the HTML file self‑contained)
            ExportActiveWorksheetOnly = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // Step 3‑2: Define the output HTML file path
        string htmlPath = "output/sheet.html";

        // Step 3‑3: Save the workbook as HTML
        wb.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Workbook successfully saved as HTML at {htmlPath}");
    }
}
```

**Dlaczego `PreserveFreezePanes = true`?**  
Gdy po prostu wywołasz `wb.Save("file.html")`, otrzymana strona wyświetla wszystkie wiersze i kolumny jako statyczną treść – brak przewijania, brak zamrożonego obszaru. Ustawienie `PreserveFreezePanes` wstrzykuje niezbędny JavaScript i CSS, aby naśladować zachowanie zamrażania w Excelu, dając użytkownikom znane wrażenia.

### Oczekiwany wynik

Otwórz `output/sheet.html` w przeglądarce. Powinieneś zobaczyć:

- Górny wiersz zablokowany podczas przewijania w pionie.
- Najbardziej lewą kolumnę zablokowaną podczas przewijania w poziomie.
- Stylizację odzwierciedlającą oryginalną siatkę Excela (czcionki, obramowania itp.).

Jeśli zamrożone okienka nie pojawią się, sprawdź, czy źródłowy arkusz rzeczywiście ma ustawione `FreezedRows`/`FreezedColumns` oraz czy nie nadpisałeś przypadkowo `PreserveFreezePanes` później w kodzie.

## Krok 4: Obsługa wielu arkuszy (Export Excel Sheet HTML)

Czasami potrzebny jest HTML tylko jednego arkusza, a nie całego skoroszytu. Użyj `HtmlSaveOptions`, aby skierować się do konkretnego arkusza:

```csharp
// Export only the second worksheet (index 1)
htmlOptions.ExportActiveWorksheetOnly = false;
htmlOptions.OnePagePerSheet = false; // combines all sheets into one HTML file
htmlOptions.SelectedSheets = new int[] { 1 }; // export sheet at index 1 only
```

Ten fragment odpowiada na przypadek **export excel sheet html**: możesz wybrać dowolny arkusz po indeksie lub nazwie, a wygenerowany HTML będzie zawierał wyłącznie jego zawartość.

## Krok 5: Dostosowywanie HTML – szybka ściągawka „Convert Excel to HTML”

Poniżej kilka typowych ustawień, które mogą się przydać przy **konwersji Excel na HTML** w projektach webowych:

| Opcja | Cel | Przykład |
|--------|---------|---------|
| `ExportImagesAsBase64` | Osadzenie obrazów bezpośrednio w HTML (bez plików zewnętrznych) | `htmlOptions.ExportImagesAsBase64 = true;` |
| `ExportHiddenWorksheet` | Dołączenie ukrytych arkuszy do wyniku | `htmlOptions.ExportHiddenWorksheet = true;` |
| `CssClassPrefix` | Prefiks klas CSS, aby uniknąć kolizji nazw | `htmlOptions.CssClassPrefix = "myExcel_";` |
| `Encoding` | Ustawienie kodowania znaków (zalecane UTF‑8) | `htmlOptions.Encoding = Encoding.UTF8;` |

Swobodnie łącz te opcje w zależności od wymagań projektu.

## Krok 6: Typowe pułapki i wskazówki

- **Duże pliki mogą generować ogromny HTML** – rozważ włączenie paginacji (`htmlOptions.OnePagePerSheet = true`), aby podzielić wynik.
- **Względne ścieżki do obrazów** – jeśli wyłączysz `ExportImagesAsBase64`, Aspose utworzy folder `images` obok pliku HTML. Upewnij się, że ten folder jest wdrożony razem z aplikacją webową.
- **Konflikty stylów** – generowany CSS używa ogólnych nazw klas, np. `.a0`, `.a1`. Skorzystaj z `CssClassPrefix`, aby je znamespace’ować i uniknąć kolizji ze stylami Twojej witryny.
- **Wydajność** – ładowanie ogromnego skoroszytu tylko po to, by wyeksportować jeden arkusz, marnuje pamięć. Użyj `Workbook.LoadOptions`, aby wczytać jedynie potrzebny arkusz, gdy pracujesz z gigabajtami danych.

## Pełny przykład od początku do końca (Wszystkie kroki w jednym pliku)

```csharp
using Aspose.Cells;
using System;
using System.IO;
using System.Text;

class FullExportDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Prepare workbook (create or load existing)
        // -------------------------------------------------
        string sourcePath = "sample.xlsx";

        // If the file doesn't exist, create a dummy workbook with frozen panes
        if (!File.Exists(sourcePath))
        {
            Workbook createWb = new Workbook();
            Worksheet sheet = createWb.Worksheets[0];
            sheet.Name = "Demo";

            for (int r = 0; r < 20; r++)
                for (int c = 0; c < 5; c++)
                    sheet.Cells[r, c].PutValue($"R{r + 1}C{c + 1}");

            sheet.FreezedRows = 1;
            sheet.FreezedColumns = 1;
            createWb.Save(sourcePath);
        }

        // Load the workbook (this is the part where we **export excel to html**)
        Workbook wb = new Workbook(sourcePath);

        // -------------------------------------------------
        // 2️⃣  Configure HTML export options
        // -------------------------------------------------
        HtmlSaveOptions htmlOpts = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,           // keep frozen rows/columns
            ExportActiveWorksheetOnly = true,     // only the first sheet
            ExportImagesAsBase64 = true,          // embed images
            CssClassPrefix = "excel_",            // avoid CSS clashes
            Encoding = Encoding.UTF8
        };

        // -------------------------------------------------
        // 3️⃣  Define output folder & file
        // -------------------------------------------------
        string outDir = "output";
        Directory.CreateDirectory(outDir);
        string htmlFile = Path.Combine(outDir, "sheet.html");

        // -------------------------------------------------
        // 4️⃣  Save as HTML
        // -------------------------------------------------
        wb.Save(htmlFile, htmlOpts);
        Console.WriteLine($"✅  Excel successfully saved as HTML at: {htmlFile}");
        Console.WriteLine("Open the file in a browser to see frozen panes in action.");
    }
}
```

Uruchom program (`dotnet run`), a otrzymasz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}