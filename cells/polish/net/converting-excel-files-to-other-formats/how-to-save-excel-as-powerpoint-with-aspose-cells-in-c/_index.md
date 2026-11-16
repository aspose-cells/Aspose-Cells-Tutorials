---
category: general
date: 2026-11-16
description: Dowiedz się, jak zapisać plik Excel jako PowerPoint i programowo konwertować
  Excel na PowerPoint. Ten przewodnik krok po kroku obejmuje także eksportowanie Excela
  do PPTX oraz zapisywanie skoroszytu jako PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: pl
lastmod: 2026-11-16
og_description: Zapisz plik Excel jako PowerPoint przy użyciu Aspose.Cells. Skorzystaj
  z tego przewodnika, aby przekonwertować Excel na PowerPoint, wyeksportować Excel
  do PPTX i zapisać skoroszyt jako PPTX w kilka minut.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Zapisz Excel jako PowerPoint – Kompletny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Jak zapisać Excel jako PowerPoint przy użyciu Aspose.Cells w C#
url: /pl/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać Excel jako PowerPoint przy użyciu Aspose.Cells w C#

Jeśli potrzebujesz **zapisać Excel jako PowerPoint** programowo, ten tutorial dostarcza kompletną, gotową do uruchomienia rozwiązanie. Niezależnie od tego, czy tworzysz silnik raportowania, czy automatyczny generator slajdów, poniższe kroki pozwolą Ci przekonwertować arkusz Excel na edytowalny slajd PPTX w zaledwie kilku linijkach kodu.

Nauczysz się, jak **konwertować Excel na PowerPoint**, wyeksportować arkusz do pliku PPTX i zachować edytowalność pól tekstowych oraz kształtów – wszystko bez opuszczania środowiska .NET.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7.2+)
* Ważna licencja Aspose.Cells (bezpłatna wersja próbna działa w celach ewaluacyjnych)
* Visual Studio 2022 (lub dowolne IDE C#)
* skoroszyt Excel zawierający dane i kształty, które chcesz wyeksportować

## Krok 1: Zainstaluj Aspose.Cells

Dodaj pakiet NuGet Aspose.Cells do swojego projektu:

```bash
dotnet add package Aspose.Cells
```

> **Wskazówka:** Użyj flagi `-v`, aby wskazać konkretną wersję, np. `Aspose.Cells.24.5`.

## Krok 2: Załaduj skoroszyt, który chcesz wyeksportować

Pierwszą operacją w przepływie **zapisywania Excel jako PowerPoint** jest załadowanie źródłowego skoroszytu.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Dlaczego to ważne:* Załadowanie skoroszytu daje dostęp do jego arkuszy, ustawień strony oraz obiektów rysunkowych, które staną się edytowalnymi kształtami w PowerPoint.

## Krok 3: Skonfiguruj opcje eksportu dla edytowalnego slajdu PPTX

Aby **konwertować Excel na PowerPoint** zachowując możliwość edycji, musisz ustawić kilka właściwości w obiekcie `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Wyjaśnienie:*  
* `SaveFormat = SaveFormat.Pptx` informuje Aspose.Cells, że ma wygenerować plik PowerPoint.  
* `ExportEditableText` oraz `ExportEditableShapes` zapewniają, że powstały slajd zachowuje się jak natywny slajd PowerPoint – możesz kliknąć pole tekstowe lub kształt i edytować je bezpośrednio w PowerPoint.

## Krok 4: Zdefiniuj obszar eksportu i dopasuj go do jednego slajdu

Gdy **eksportujesz Excel do PPTX**, zazwyczaj chcesz, aby określony zakres pojawił się na slajdzie. Ustawienie obszaru drukowania i opcji dopasowania zapewnia czysty wynik w postaci jednego slajdu.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Dlaczego to ważne:* `PrintArea` ogranicza eksport do komórek od A1 do G30, natomiast `FitToPagesTall` i `FitToPagesWide` kompresują wszystko do jednego slajdu, zapobiegając niechcianym dodatkowym stronom.

## Krok 5: Zapisz arkusz jako edytowalny plik PPTX

Teraz możesz w końcu **zapisać skoroszyt jako PPTX** i zakończyć proces **zapisywania Excel jako PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Po uruchomieniu programu otwórz `EditableShapes.pptx` w Microsoft PowerPoint. Zobaczysz slajd odzwierciedlający wybrany zakres Excel, a wszystkie pola tekstowe i kształty będą w pełni edytowalne.

### Oczekiwany wynik

* Plik o nazwie `EditableShapes.pptx` znajdujący się w `C:\Output\`.
* Jeden slajd PowerPoint zawierający zakres A1:G30.
* Pola tekstowe, wykresy i kształty, które możesz dwukrotnie kliknąć i edytować bezpośrednio w PowerPoint.

## Pełny kod źródłowy (gotowy do skopiowania)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Częste pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|--------|
| **Co zrobić, jeśli mam wiele arkuszy?** | Przejdź pętlą przez `workbook.Worksheets` i powtórz kroki 3‑5 dla każdego arkusza, zmieniając nazwę pliku wyjściowego (np. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Czy mogę wyeksportować cały skoroszyt do jednej prezentacji PowerPoint?** | Tak. Ustaw `ExportAllSheets = true` w `ImageOrPrintOptions`. Każdy arkusz stanie się osobnym slajdem. |
| **Moje kształty pojawiają się jako obrazy, a nie edytowalne obiekty.** | Upewnij się, że `ExportEditableShapes = true` oraz że używasz Aspose.Cells 24.5+ (wcześniejsze wersje nie mają tej funkcji). |
| **Wygenerowany plik PPTX jest zbyt duży.** | Zmniejsz obszar drukowania lub obniż rozdzielczość obrazu za pomocą `exportOptions.ImageResolution`. |
| **Czy potrzebna jest licencja do użytku produkcyjnego?** | Płatna licencja usuwa znak wodny wersji ewaluacyjnej i odblokowuje pełną wydajność. Bezpłatna wersja próbna działa w celach testowych. |

## Wskazówki dla solidnego kodu produkcyjnego

* **Waliduj ścieżki plików** przed wywołaniem `Workbook` lub `Save`, aby uniknąć `FileNotFoundException`.  
* **Umieść eksport w bloku try/catch**, aby obsłużyć błędy licencjonowania (`Aspose.Cells.LicenseException`).  
* **Zwolnij zasoby skoroszytu** (`workbook.Dispose()`) po zakończeniu, aby uwolnić niezarządzane zasoby.  
* **Używaj asynchronicznego I/O** (`FileStream` z `await`), jeśli eksportujesz wiele dużych arkuszy w usłudze webowej.

## Kolejne kroki

Teraz, gdy wiesz, jak **zapisać Excel jako PowerPoint**, możesz zgłębiać powiązane tematy:

* **Eksportuj Excel do PPTX z niestandardowymi układami slajdów** – dostosuj `SlideSize` i dodaj slajd główny.  
* **Konwertuj slajd Excel na PDF** – użyj `SaveFormat.Pdf` dla wersji do druku.  
* **Masowa konwersja folderu ze skoroszytami** – połącz pętlę przedstawioną powyżej z `Directory.GetFiles`.  

Eksperymentuj z różnymi obszarami drukowania, opcjami skalowania i motywami PowerPoint, aby dostosować wynik do identyfikacji wizualnej Twojej organizacji.

---

*Miłego kodowania! Jeśli ten przewodnik pomógł Ci **konwertować Excel na PowerPoint**, podziel się nim z zespołem lub otwórz zgłoszenie w repozytorium Aspose.Cells na GitHubie, aby uzyskać dalszą pomoc.*

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapisać Excel jako PowerPoint przy użyciu C# i Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Jak zapisać PPTX z Excela – Kompletny przewodnik po eksporcie arkusza Excel do PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Konwertuj Excel na PowerPoint – Pełny przewodnik krok po kroku](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}