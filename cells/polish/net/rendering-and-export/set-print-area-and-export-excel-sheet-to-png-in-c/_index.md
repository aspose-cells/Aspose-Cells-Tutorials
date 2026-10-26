---
category: general
date: 2026-10-26
description: Ustaw obszar wydruku i wyeksportuj arkusz Excela do formatu PNG w C#.
  Poznaj opcje eksportu obrazu, jak wyeksportować PNG oraz uzyskaj obraz gotowy do
  druku ze skoroszytu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: pl
lastmod: 2026-10-26
og_description: Ustaw obszar wydruku i wyeksportuj arkusz Excela do formatu PNG w
  C#. Ten samouczek krok po kroku omawia opcje eksportu obrazu oraz sposób eksportowania
  PNG ze skoroszytu.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Ustaw obszar wydruku i wyeksportuj arkusz Excela do PNG – przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ustaw obszar wydruku i wyeksportuj arkusz Excela do PNG w C#
url: /pl/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw obszar wydruku i wyeksportuj arkusz Excel do PNG w C#

Jeśli potrzebujesz **ustawić obszar wydruku** przed wyeksportowaniem arkusza Excel do PNG, ten przewodnik pokaże Ci, jak to zrobić. Zobaczysz kompletny przykład w C#, który konfiguruje opcje eksportu obrazu, dostosowuje obszar wydruku arkusza i zapisuje wynik jako obraz.

Eksportowanie arkusza Excel do PNG jest częstym wymogiem, gdy chcesz osadzić migawkę arkusza w raporcie, e‑mailu lub na stronie internetowej. Poniższy kod działa z każdym skoroszytem zawierającym tabelę przestawną, ale technika ma zastosowanie także do zwykłych zakresów danych. Nie są potrzebne żadne zewnętrzne narzędzia — wystarczy biblioteka Aspose.Cells for .NET.

## Wymagania wstępne

- .NET 6.0 lub nowszy (przykład jest skierowany na .NET 6, ale działa z każdą nowszą wersją .NET)
- Aspose.Cells for .NET (zainstaluj przez NuGet: `Install-Package Aspose.Cells`)
- Podstawowa znajomość C# oraz koncepcji Excela, takich jak arkusze i obszary wydruku

## Krok 1: Skonfiguruj opcje eksportu obrazu

Pierwszą rzeczą, którą robisz, jest utworzenie instancji `ImageOrPrintOptions`. Ten obiekt informuje Aspose.Cells, jak renderować arkusz jako obraz.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Dlaczego to ważne:** `ImageOrPrintOptions` kontroluje format wyjściowy, rozdzielczość i inne szczegóły renderowania. Użycie PNG zapewnia jakość bezstratną, co jest idealne w raportach wymagających wyraźnego tekstu i grafiki.

## Krok 2: Załaduj skoroszyt i uzyskaj dostęp do docelowego arkusza

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Dlaczego to ważne:** Musisz pracować z konkretnym obiektem `Worksheet`, ponieważ obszar wydruku jest ustawieniem na poziomie arkusza.

## Krok 3: Zidentyfikuj zakres, który chcesz wydrukować

W wielu scenariuszach interesujące Cię dane znajdują się wewnątrz tabeli przestawnej. Poniższy kod wyodrębnia zakres danych pierwszej tabeli przestawnej na arkuszu.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Jeśli Twój arkusz nie zawiera tabeli przestawnej, możesz zamienić `pivotDataRange` na dowolny `CellArea`, który utworzysz ręcznie, np.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Krok 4: **Ustaw obszar wydruku** tak, aby pasował do wybranego zakresu

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Dlaczego to ważne:** Obszar wydruku mówi Excelowi (i Aspose.Cells), które komórki uwzględnić przy renderowaniu arkusza jako obrazu. Dopasowując obszar wydruku do zakresu danych tabeli przestawnej, unikasz pustych marginesów i zapewniasz, że wyeksportowany PNG zawiera wyłącznie istotne dane.

## Krok 5: Wyeksportuj arkusz do obrazu PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Dlaczego to ważne:** `worksheet.ToImage` respektuje wcześniej ustawiony obszar wydruku, więc plik PNG zawiera dokładnie te komórki, które określiłeś. Przypisanie obrazu do kształtu picture umożliwia ponowne osadzenie go w skoroszycie w razie potrzeby, a zapis na dysku daje Ci samodzielny plik.

## Pełny działający przykład

Połączenie wszystkich kroków daje samodzielny program, który możesz uruchomić od razu.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu tworzy `C:\Temp\WorksheetExport.png`. Otwarcie pliku pokazuje wyraźny obraz PNG, który zawiera tylko komórki zdefiniowane przez **ustawiony obszar wydruku** (dane tabeli przestawnej w tym przykładzie). Obraz można wstawiać do dokumentów Word, slajdów PowerPoint czy stron internetowych bez dodatkowych kroków konwersji.

## Obsługa wielu arkuszy lub tabel przestawnych

- **Wiele arkuszy:** Przejdź pętlą po `wb.Worksheets` i powtórz kroki 3‑5 dla każdego arkusza, który chcesz wyeksportować.
- **Wiele tabel przestawnych:** Wybierz odpowiedni `PivotTables[index]` lub iteruj po `worksheet.PivotTables`, aby wyeksportować każdą tabelę osobno.
- **Brak tabeli przestawnej:** Utwórz ręcznie `CellArea` (zobacz komentarz w Kroku 3) i przypisz go do `PrintArea`.

## Praktyczne wskazówki (E‑E‑A‑T)

- **Porada:** Ustaw `HorizontalResolution` i `VerticalResolution` na 300 DPI dla PNG gotowych do druku; niższe wartości zmniejszają rozmiar pliku przy użyciu w sieci.
- **Uważaj na puste kształty obrazu:** Jeśli arkusz nie ma kształtów obrazu, dodaj jeden przed przypisaniem obrazu:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Wydajność:** Ponowne użycie jednej instancji `ImageOrPrintOptions` dla wielu arkuszy unika niepotrzebnych alokacji.
- **Kompatybilność:** Aspose.Cells 23.9+ w pełni wspiera .NET 6 i nowsze; wcześniejsze wersje mogą wymagać dostosowań nazw API.

## Podsumowanie

Teraz wiesz, jak **ustawić obszar wydruku** i wyeksportować Excel

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyeksportować Excel do PNG – pełny przewodnik krok po kroku](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Jak wyeksportować zakres Excela jako obraz przy użyciu C# i Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [Arkusz Excel do PNG – eksport tabeli przestawnej jako PNG w C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}