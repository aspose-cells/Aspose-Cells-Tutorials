---
category: general
date: 2026-08-04
description: Eksportuj wykres Excel do PowerPoint przy użyciu Aspose.Cells w C#. Postępuj
  zgodnie z tym przewodnikiem krok po kroku dotyczącym konwersji z Excela do PowerPoint
  i zachowaj edytowalność kształtów.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: pl
lastmod: 2026-08-04
og_description: Eksportuj wykres z Excela do PowerPointa przy użyciu Aspose.Cells
  w C#. Dowiedz się, jak utworzyć edytowalny plik PPTX, zachować dane wykresu i zautomatyzować
  konwersję z Excela do PowerPointa.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Eksport wykresu Excel do PowerPoint przy użyciu C# – pełny samouczek Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Eksport wykresu Excel do PowerPoint przy użyciu C# – kompletny przewodnik Aspose.Cells
url: /pl/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu Excel do PowerPoint przy użyciu C# – kompletny przewodnik Aspose.Cells

Jeśli potrzebujesz **eksportować wykres Excel do PowerPoint**, ten tutorial pokaże Ci, jak zrobić to za pomocą Aspose.Cells i Aspose.Slides w C#. Otrzymasz w pełni edytowalny plik PPTX, który zachowuje dane wykresu i kształty, co umożliwia dalszą pracę projektową.

Eksportowanie wykresów z Excela do PowerPointa jest powszechnym wymogiem przy tworzeniu zautomatyzowanych potoków raportowania, prezentacji sprzedażowych lub materiałów szkoleniowych. W tym przewodniku nauczysz się dokładnych kroków, aby wykonać **konwersję Excel do PowerPoint**, która zachowuje wszystkie elementy wykresu edytowalne. Nie jest wymagane ręczne kopiowanie‑wklejanie, a kod działa z .NET 6+ oraz klasycznym .NET Framework.

## Wymagania wstępne

- Ważna licencja Aspose.Cells (lub darmowy klucz ewaluacyjny)  
- Aspose.Slides for .NET dodany do projektu (biblioteka obsługuje wyjście PPTX)  
- .NET 6 SDK lub nowszy zainstalowany  
- Plik Excel zawierający przynajmniej jeden wykres (w tym przykładzie używamy `Shapes.xlsx`)  

Możesz zainstalować pakiety NuGet przy użyciu następujących poleceń:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Krok 1: Załaduj skoroszyt Excel

Pierwszą operacją jest otwarcie skoroszytu, który zawiera wykres, który chcesz wyeksportować. Klasa `Workbook` reprezentuje cały plik Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Dlaczego to ważne:** Załadowanie skoroszytu daje dostęp do jego arkuszy, wykresów i formatowania. Aspose.Cells odczytuje plik bez konieczności instalacji Microsoft Office, co utrzymuje rozwiązanie lekkie i przyjazne dla serwera.

## Krok 2: Wybierz arkusz i określ obszar wydruku

Arkusz może zawierać wiele wykresów, ale zazwyczaj eksportujesz określony region. Ustawienie `PrintArea` informuje Aspose.Cells, które komórki (włącznie z wykresami) mają być renderowane.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Dlaczego to ważne:** Ograniczając eksport do zdefiniowanego obszaru wydruku, unikasz niepotrzebnych pustych slajdów i utrzymujesz mały rozmiar pliku PPTX. Obszar można dostosować, aby odpowiadał dokładnemu zakresowi Twojego wykresu.

## Krok 3: Skonfiguruj opcje eksportu dla edytowalnego PPTX

Aspose.Cells używa klasy `ImageOrPrintOptions` do kontrolowania formatu wyjściowego i edytowalności. Ustawienie `ImageFormat` na `ImageFormat.Pptx` tworzy plik PowerPoint, natomiast `ExportEditableShapes = true` zachowuje obiekty wykresu jako edytowalne kształty.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Dlaczego to ważne:** Flaga `ExportEditableShapes` jest kluczem do uzyskania **edytowalnych kształtów w PowerPoint**. Bez niej wykres zostałby zrastrowany jako obraz, tracąc możliwość późniejszej modyfikacji punktów danych lub stylizacji.

## Krok 4: Zapisz arkusz jako prezentację PowerPoint

Na koniec wywołaj metodę `Save` na obiekcie `Workbook`. Enum `SaveFormat.Pptx` informuje Aspose.Cells, aby wygenerował plik PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Po zakończeniu działania kodu otwórz `ShapesExport.pptx` w PowerPoint. Zobaczysz slajd zawierający oryginalny wykres Excel jako natywny obiekt wykresu PowerPoint. Kliknij dwukrotnie wykres, aby edytować dane, zmienić kolory lub dodać animacje — tak, jakbyś stworzył wykres bezpośrednio w PowerPoint.

### Oczekiwany wynik

| Nazwa pliku                | Zawartość na slajdzie                         |
|----------------------------|-----------------------------------------------|
| `ShapesExport.pptx`        | Wykres z `Shapes.xlsx` wyświetlony jako edytowalny wykres PowerPoint, z etykietami osi, legendą i niezmienionymi seriami danych. |

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i uruchomić. Zawiera wszystkie niezbędne dyrektywy `using`, obsługę błędów i komentarze.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Wyjaśnienie każdego bloku**

| Blok | Cel |
|------|-----|
| `using` dyrektywy | Importuje przestrzenie nazw Aspose.Cells i Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Ładuje plik Excel bez potrzeby instalacji Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Ogranicza eksport do regionu zawierającego wykres. |
| `ImageOrPrintOptions` | Konfiguruje wyjście PPTX i włącza **eksport Aspose.Cells PPTX** z edytowalnymi kształtami. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Zapisuje plik PowerPoint na dysku. |
| `try / catch` | Zapewnia podstawową obsługę błędów dla brakujących plików lub problemów z licencją. |

Uruchomienie tego programu generuje slajd PowerPoint, który możesz otworzyć w Microsoft PowerPoint, Google Slides (po konwersji) lub dowolnym kompatybilnym przeglądarce.

## Wspólne warianty i przypadki brzegowe

### Eksportowanie wielu arkuszy

Jeśli potrzebujesz slajdu dla każdego arkusza, iteruj przez `workbook.Worksheets` i wywołaj `Save` z unikalną nazwą pliku dla każdej iteracji.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Kontrolowanie układu slajdu

Aspose.Slides pozwala dodać niestandardowy układ slajdu po eksporcie. Utwórz nową prezentację, zaimportuj wygenerowany slajd, a następnie zastosuj motyw master.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Obsługa wykresów z zewnętrznymi źródłami danych

Jeśli wykres odwołuje się do zakresu danych poza zdefiniowanym obszarem wydruku, rozszerz `PrintArea`, aby uwzględnić te komórki. W przeciwnym razie wykres może utracić serie danych podczas eksportu.

### Kwestie licencjonowania

Biblioteki Aspose działają w trybie ewaluacyjnym z znakiem wodnym. Aby usunąć znak wodny, ustaw licencję przed jakimkolwiek wywołaniem API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Zrób to samo dla Aspose.Slides, jeśli używasz jego zaawansowanych funkcji.

## Porady profesjonalne

- **Ponowne użycie opcji eksportu:** Utwórz jedną instancję `ImageOrPrintOptions` i przypisz ją do każdego arkusza, aby kod był DRY.  
- **Przetwarzanie wsadowe:** W przypadku raportowania na dużą skalę połącz tę logikę eksportu z workerem w tle lub Azure Function, aby generować pliki PPTX na żądanie.  
- **Wydajność:** Jeśli potrzebujesz tylko obrazu wykresu (nie edytowalnego), ustaw `ExportEditableShapes = false`. To zmniejsza zużycie pamięci i przyspiesza konwersję.  
- **Testowanie:** Zweryfikuj wygenerowany plik PPTX zarówno w instalacjach PowerPoint na Windows, jak i macOS, ponieważ niektóre nieprawidłowości renderowania różnią się między platformami.

## Podsumowanie

Masz teraz kompletną, kompleksową rozwiązanie do **eksportu wykresu Excel do PowerPoint** przy użyciu C#. Tutorial obejmował ładowanie skoroszytu, wybór obszaru wydruku, konfigurowanie **eksportu Aspose.Cells PPTX** z **edytowalnymi kształtami w PowerPoint**, oraz zapisanie wyniku jako w pełni edytowalny plik PPTX.  

Od tego momentu możesz eksplorować dodatkowe scenariusze **konwersji Excel do PowerPoint**, takie jak eksport wsadowy, niestandardowe układy slajdów lub integrację procesu z API webowym. Eksperymentuj z różnymi typami wykresów, dodawaj obrazy lub łącz wiele arkuszy w jedną prezentację, aby dostosować wyjście do potrzeb Twojego biznesu.  

Gotowy, aby zautomatyzować swój przepływ raportowania? Spróbuj zamienić plik źródłowy, dostosować obszar wydruku i zintegrować kod z istniejącymi usługami .NET. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak przekonwertować Excel do PowerPoint przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak wyeksportować wykresy Excel do PDF przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Eksportowanie komórek Excel do obrazu przy użyciu Aspose.Cells .NET: Przewodnik krok po kroku](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}