---
category: general
date: 2026-03-18
description: Samouczek konwersji arkusza Excel na PNG, pokazujący, jak wyeksportować
  tabelę przestawną, ustawić obszar wydruku tabeli przestawnej i wyeksportować obraz
  zakresu w Excelu przy użyciu Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: pl
og_description: samouczek konwertowania arkusza Excel na PNG, który krok po kroku
  pokazuje, jak eksportować tabele przestawne, ustawiać obszar wydruku w tabeli przestawnej
  oraz eksportować obraz zakresu Excel przy użyciu C#.
og_title: Arkusz Excel do PNG – Kompletny przewodnik po eksportowaniu tabel przestawnych
tags:
- Aspose.Cells
- C#
- Excel automation
title: Arkusz Excel do PNG – Eksportuj tabelę przestawną jako PNG w C#
url: /pl/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Export a Pivot Table as PNG in C#

Czy kiedykolwiek potrzebowałeś zamienić **excel sheet to png**, ale nie wiedziałeś, jak uchwycić tylko tabelę przestawną? Nie jesteś sam. W wielu procesach raportowania wizualizacja tabeli przestawnej jest gwiazdą, a eksportowanie jej jako PNG pozwala osadzić ją w e‑mailach, dashboardach lub dokumentacji bez konieczności dołączania całego skoroszytu.

W tym przewodniku pokażemy, **jak wyeksportować pivot**, **set print area pivot**, oraz w końcu **export excel range image**, aby uzyskać czysty plik **export worksheet to image**. Bez tajemniczych odnośników do zewnętrznych dokumentów – tylko kompletny, gotowy do uruchomienia fragment kodu i wyjaśnienie każdego wiersza.

## What You’ll Need

- **Aspose.Cells for .NET** (pakiet NuGet `Aspose.Cells` – wersja 23.12 lub nowsza).  
- Środowisko programistyczne .NET (Visual Studio, Rider lub `dotnet` CLI).  
- Plik Excel (`input.xlsx`) zawierający przynajmniej jedną tabelę przestawną.

To wszystko. Jeśli masz te elementy, zanurzmy się.

## Step 1 – Load the Workbook and Grab the First Worksheet

Zanim będziemy mogli dotknąć tabeli przestawnej, musimy wczytać skoroszyt do pamięci.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Dlaczego to ważne:* Ładowanie pliku daje dostęp do wszystkich obiektów (tabele, wykresy, pivoty). Użycie pierwszego arkusza to prosty domyślny wybór; możesz zamienić `0` na rzeczywisty indeks lub nazwę arkusza, jeśli potrzebujesz.

## Step 2 – Retrieve the Pivot Table Range

Tabela przestawna znajduje się wewnątrz bloku komórek. Potrzebujemy tego bloku, aby poinstruować Excel, co ma drukować.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Dlaczego to robimy:* `PivotTableRange` podaje dokładny początkowy i końcowy wiersz/kolumnę. Bez tego eksport obejmowałby cały arkusz, co podważa sens **set print area pivot**.

## Step 3 – Define the Print Area So Only the Pivot Is Rendered

Silnik drukowania Excela respektuje właściwość `PrintArea`. Ograniczając ją do pivotu, unikamy niechcianych danych lub pustych komórek.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Wskazówka:* Jeśli masz wiele pivotów na tym samym arkuszu, możesz połączyć ich zakresy, używając listy oddzielonej przecinkami (`"0,0:10,5,12,0:22,5"`). To technika **export excel range image** dla kilku bloków.

## Step 4 – Set Up Image Export Options (PNG Format)

Aspose.Cells pozwala precyzyjnie dostosować wyjście. PNG jest bezstratny, idealny dla wyraźnych wizualizacji pivotów.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Dlaczego PNG?* W przeciwieństwie do JPEG, PNG zachowuje ostrość tekstu i przezroczyste tło, co czyni go domyślnym wyborem w scenariuszach **excel sheet to png**.

## Step 5 – Export the Worksheet (Pivot Area) to a PNG File

Teraz dzieje się magia – renderujemy zdefiniowany obszar drukowania do obrazu.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Co zobaczysz:* Plik `pivot.png` zawierający wyłącznie tabelę przestawną, bez dodatkowych wierszy czy kolumn. Otwórz go w dowolnym przeglądarce obrazów i będziesz mieć gotową do udostępnienia wizualizację.

---

## Frequently Asked Questions & Edge Cases

### What if the workbook has **multiple pivot tables**?

Pobierz `PivotTableRange` każdego pivotu, połącz zakresy i przypisz połączony ciąg do `PrintArea`. Przykład:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Can I export to **other image formats**?

Oczywiście. Zmien `imgOptions.ImageFormat = ImageFormat.Jpeg;` (lub `Bmp`, `Gif`, `Tiff`). Pamiętaj, że JPEG wprowadza artefakty kompresji – zazwyczaj nie jest idealny dla pivotów z dużą ilością tekstu.

### How do I handle **large pivots** that span many pages?

Ustaw `imgOptions.OnePagePerSheet = false;`, aby zezwolić na renderowanie wielostronicowe, a następnie iteruj po stronach:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### What about **hidden rows/columns**?

Aspose respektuje ustawienia widoczności arkusza. Jeśli musisz pominąć ukryte elementy, tymczasowo je odsłoń przed eksportem lub ręcznie dostosuj `PrintArea`.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Uruchom program, a znajdziesz `pivot.png` dokładnie tam, gdzie wskazałeś. Otwórz plik – powinieneś zobaczyć wyraźny rendering samej tabeli przestawnej, nic więcej.

---

## Conclusion

Masz teraz **kompletne, end‑to‑end rozwiązanie** do zamiany **excel sheet to png**, które koncentruje się wyłącznie na tabeli przestawnej. Dzięki **setting the print area pivot**, konfiguracji **image export options** oraz metodzie `ToImage` z Aspose.Cells możesz automatyzować generowanie raportów, osadzać wizualizacje w stronach internetowych lub po prostu archiwizować migawki analiz.

Co dalej? Spróbuj zamienić PNG na wysokiej rozdzielczości PDF (`ImageFormat.Pdf`), eksperymentuj z wieloma pivotami na jednym arkuszu lub połącz to podejście z eksportem wykresów, aby uzyskać pełnoprawny pipeline eksportu dashboardu.

Masz własny pomysł, którym chcesz się podzielić? zostaw komentarz lub przygotuj się na kolejny tutorial, w którym przyjrzymy się **export worksheet to image** dla pełnych migawków arkusza, w tym wykresów i formatowania warunkowego. Szczęśliwego kodowania!  

<img src="pivot.png" alt="przykład eksportu tabeli przestawnej z arkusza Excel do PNG">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}