---
category: general
date: 2026-05-23
description: Dowiedz się, jak wyeksportować tabelę przestawną jako obraz i zapisać
  ją jako zdjęcie przy użyciu Aspose.Cells w C#. Krok po kroku kod i wskazówki.
draft: false
keywords:
- export pivot table as image
- save pivot table as picture
language: pl
og_description: Eksportuj tabelę przestawną jako obraz i zapisz tabelę przestawną
  jako zdjęcie przy użyciu Aspose.Cells. Pełny kod, wyjaśnienie i najlepsze praktyki.
og_title: Eksportowanie tabeli przestawnej jako obrazu w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  headline: Export Pivot Table as Image with C# – Complete Guide
  type: TechArticle
- description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  name: Export Pivot Table as Image with C# – Complete Guide
  steps:
  - name: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
    text: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
  - name: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
    text: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
  - name: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
    text: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
  - name: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
    text: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
  - name: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
    text: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
  - name: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
    text: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
  - name: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
    text: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel automation
- PivotTable
- Image export
title: Eksportowanie tabeli przestawnej jako obrazu w C# – Kompletny przewodnik
url: /pl/net/pivot-tables/export-pivot-table-as-image-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport tabeli przestawnej jako obrazu w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **wyeksportować tabelę przestawną jako obraz** bezpośrednio z skoroszytu Excel, pomijając zrzut ekranu? Nie jesteś sam. W wielu scenariuszach raportowania — myśl o automatycznych pulpitach nawigacyjnych lub załącznikach e‑mail — posiadanie wyraźnego obrazu tabeli przestawnej jest znacznie wygodniejsze niż surowy plik `.xlsx`.  

W tym tutorialu przejdziemy krok po kroku przez proces **eksportu tabeli przestawnej jako obrazu** oraz omówimy subtelną sztukę **zapisania tabeli przestawnej jako obraz** przy użyciu potężnej biblioteki Aspose.Cells. Po zakończeniu będziesz mieć samodzielny, gotowy do uruchomienia program w C#, który zapisze plik PNG dokładnie tam, gdzie potrzebujesz.

## Co obejmuje ten przewodnik

- Konfiguracja projektu .NET z Aspose.Cells  
- Ładowanie istniejącego skoroszytu i odnalezienie żądanej tabeli przestawnej  
- Ustawianie opcji eksportu obrazu (rozdzielczość, format itp.)  
- Faktyczny eksport tabeli przestawnej jako pliku PNG  
- Typowe pułapki — np. ukryte arkusze lub wiele tabel przestawnych — i jak ich unikać  

Bez zewnętrznych skryptów, bez ręcznego kombinowania, po prostu czysty kod, który możesz skopiować‑wkleić i uruchomić.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

1. **.NET 6+** (lub .NET Framework 4.6+, jeśli wolisz klasyczny) zainstalowany.  
2. **Licencję** na Aspose.Cells — wersja ewaluacyjna działa w testach, ale licencja usuwa znak wodny ewaluacji.  
3. Plik Excel (`Sample.xlsx`) zawierający przynajmniej jedną tabelę przestawną w arkuszu o nazwie *Sheet1* (możesz zmienić nazwę później).  

Jeśli czegoś brakuje, pobierz najnowszy pakiet NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

Teraz, gdy wszystko jest gotowe, zabierzmy się do pracy.

## Krok 1: Załaduj skoroszyt i pobierz arkusz

Na początek musimy otworzyć skoroszyt i wskazać arkusz, w którym znajduje się tabela przestawna. Ten krok jest podstawą **eksportu tabeli przestawnej jako obrazu**, ponieważ bez prawidłowego obiektu `Worksheet` biblioteka nie może znaleźć tabeli.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // Path to the Excel file containing the pivot table
        string workbookPath = @"C:\Data\Sample.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(workbookPath);

        // Obtain the worksheet that contains the pivot table
        // Replace "Sheet1" with your actual sheet name if different
        Worksheet ws = workbook.Worksheets["Sheet1"];
```

> **Dlaczego to ważne:** Aspose.Cells wczytuje cały skoroszyt do pamięci, więc każdy błąd w nazwie arkusza skutkuje `ArgumentException`. Zawsze sprawdzaj, czy arkusz istnieje przed kontynuacją.

## Krok 2: Uzyskaj dostęp do żądanej tabeli przestawnej

Skoroszyt może zawierać wiele tabel przestawnych, ale w prostych scenariuszach zazwyczaj potrzebujemy pierwszej. Jeśli masz ich kilka, możesz iterować po `ws.PivotTables` i wybrać po nazwie.

```csharp
        // Access the first pivot table in the worksheet
        // If you know the pivot's name, you can use ws.PivotTables["MyPivot"]
        PivotTable pivot = ws.PivotTables[0];
```

> **Pro tip:** Gdy masz więcej niż jedną tabelę, użyj `ws.PivotTables["PivotName"]`, aby nie wyeksportować przypadkowo niewłaściwej tabeli.

## Krok 3: Skonfiguruj opcje eksportu obrazu

Aspose.Cells daje precyzyjną kontrolę nad wyjściem obrazu. Tutaj ustawimy format na PNG, ale możesz przełączyć się na JPEG lub BMP, zmieniając `ImageFormat`. Można także dostosować DPI, skalowanie i czy mają być widoczne linie siatki.

```csharp
        // Set up image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: increase resolution for sharper output
            // HorizontalResolution = 300,
            // VerticalResolution = 300,
            // Transparent = true   // if you need a transparent background
        };
```

> **Dlaczego wybieramy PNG:** PNG zachowuje ostrość tekstu i obsługuje przezroczystość, co czyni go idealnym do wstawiania w raporty lub strony internetowe.

## Krok 4: Wyeksportuj tabelę przestawną jako plik obrazu

Teraz dzieje się magia. Metoda `ToImage` zapisuje tabelę przestawną na dysku w skonfigurowanym formacie. To sedno **zapisu tabeli przestawnej jako obrazu**.

```csharp
        // Define the output path – make sure the directory exists
        string outputPath = @"C:\Exports\pivot.png";

        // Export the pivot table as an image file
        pivot.ToImage(outputPath, imageOptions);

        System.Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

> **Przypadek brzegowy:** Jeśli docelowy katalog nie istnieje, `ToImage` zgłosi `DirectoryNotFoundException`. Utwórz folder wcześniej lub użyj `Directory.CreateDirectory(Path.GetDirectoryName(outputPath))`.

## Krok 5: Zweryfikuj wynik

Uruchom program (F5 w Visual Studio lub `dotnet run` w wierszu poleceń). Przejdź do `C:\Exports\pivot.png` i powinieneś zobaczyć wyraźny zrzut swojej tabeli przestawnej, identyczny z tym, co widzisz w Excelu.

![przykład eksportu tabeli przestawnej jako obrazu](https://example.com/images/pivot-export.png "przykład eksportu tabeli przestawnej jako obrazu")

*Tekst alternatywny obrazu: przykład eksportu tabeli przestawnej jako obrazu*

Jeśli obraz jest przycięty, dostosuj właściwości `ImageOrPrintOptions` takie jak `HorizontalResolution`, `VerticalResolution` lub `OnePagePerSheet`. Te drobne zmiany pozwalają **zapisac tabelę przestawną jako obraz** w dokładnie takich wymiarach, jakich potrzebujesz.

## Często zadawane pytania i pułapki

| Pytanie | Odpowiedź |
|----------|-----------|
| **Czy mogę wyeksportować wiele tabel jednocześnie?** | Przejdź pętlą po `ws.PivotTables` i wywołaj `ToImage` dla każdej, zmieniając nazwę pliku wyjściowego przy każdym przebiegu. |
| **Co jeśli tabela zawiera wykresy?** | Wykresy nie są częścią regionu danych tabeli przestawnej, więc nie pojawią się. Eksportuj wykres osobno przy użyciu `Chart.ToImage`. |
| **Czy to działa z chronionymi hasłem skoroszytami?** | Tak — załaduj skoroszyt przy pomocy `Workbook(workbookPath, new LoadOptions { Password = "secret" })`. |
| **Jak zmienić kolor tła?** | Ustaw `imageOptions.BackgroundColor = Color.White;` (lub dowolny `System.Drawing.Color`). |
| **Czy istnieje możliwość eksportu do JPEG w celu zmniejszenia rozmiaru pliku?** | Zmien `ImageFormat = ImageFormat.Jpeg` i opcjonalnie ustaw `imageOptions.JpegQuality = 80`. |

## Profesjonalne wskazówki dla produkcyjnego eksportu

1. **Zwalnianie zasobów:** Umieść `Workbook` w bloku `using` lub wywołaj `workbook.Dispose()`, aby zwolnić pamięć, szczególnie przy dużych plikach.  
2. **Bezpieczeństwo wątków:** Każdy wątek powinien mieć własną instancję `Workbook`; obiekty Aspose.Cells nie są bezpieczne wątkowo.  
3. **Logowanie:** Loguj ścieżkę eksportu oraz ewentualne wyjątki w centralnym pliku logów, aby ułatwić diagnostykę.  
4. **Przetwarzanie wsadowe:** Jeśli musisz generować obrazy dla dziesiątek skoroszytów, rozważ system kolejkowy (np. Azure Queue), aby rozłożyć obciążenie.  

## Kompletny działający przykład

Oto pełny program, gotowy do skopiowania‑wklejenia:

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;
using System.IO;

class ExportPivotImage
{
    static void Main()
    {
        // 1️⃣ Load workbook
        string workbookPath = @"C:\Data\Sample.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // 2️⃣ Get worksheet containing the pivot
        Worksheet ws = workbook.Worksheets["Sheet1"]; // adjust if needed

        // 3️⃣ Grab the first pivot table
        if (ws.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found on the sheet.");
            return;
        }
        PivotTable pivot = ws.PivotTables[0];

        // 4️⃣ Set image export options (PNG is default)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Uncomment to increase DPI for sharper images
            // HorizontalResolution = 300,
            // VerticalResolution = 300
        };

        // 5️⃣ Ensure output directory exists
        string outputDir = @"C:\Exports";
        Directory.CreateDirectory(outputDir);
        string outputPath = Path.Combine(outputDir, "pivot.png");

        // 6️⃣ Export pivot table as image
        pivot.ToImage(outputPath, imageOptions);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

Uruchomienie tego kodu wygeneruje plik PNG o nazwie `pivot.png` w `C:\Exports`. Otwórz go dowolnym przeglądarką obrazów, a zobaczysz dokładną wizualną replikę tabeli przestawnej — idealną do raportów, e‑maili lub stron internetowych.

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **wyeksportować tabelę przestawną jako obraz** i **zapisac tabelę przestawną jako obraz** przy użyciu C# i Aspose.Cells. Od ładowania skoroszytu po precyzyjne dopasowanie opcji obrazu, proces jest prosty i w pełni skryptowalny.  

Co dalej? Wypróbuj inne formaty (JPEG, BMP), zwiększ DPI dla grafiki drukarskiej lub przetwarzaj wsadowo folder skoroszytów. Możesz także rozważyć eksport całego arkusza jako obrazu, jeśli potrzebny jest szerszy kontekst.  

Masz więcej pytań lub trudny scenariusz? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Powiązane tutoriale

- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Master Pivot Table Formatting in .NET Using Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}