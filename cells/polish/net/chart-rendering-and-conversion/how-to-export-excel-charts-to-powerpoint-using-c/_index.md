---
category: general
date: 2026-10-26
description: Dowiedz się, jak eksportować wykresy z Excela do PowerPointa przy użyciu
  C#. Zachowaj możliwość edycji kształtów i zapisz jako PPTX w kilku linijkach kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: pl
lastmod: 2026-10-26
og_description: Eksportuj wykresy z Excela do PowerPointa przy użyciu C#. Ten przewodnik
  pokazuje, jak zachować edytowalne kształty i zapisać jako PPTX przy użyciu Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Eksportuj wykresy Excel do PowerPoint przy użyciu C# – przewodnik krok po
  kroku
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Jak wyeksportować wykresy Excel do PowerPoint przy użyciu C#
url: /pl/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować wykresy Excel do PowerPoint przy użyciu C#

Jeśli potrzebujesz **wyeksportować wykresy Excel do PowerPoint**, ten przewodnik poprowadzi Cię przez kompletną, gotową do uruchomienia rozwiązanie. Niezależnie od tego, czy tworzysz pulpit nawigacyjny raportowy, czy automatyzujesz zestawy slajdów, zobaczysz, jak kilka linii kodu C# utrzymuje kształty wykresów w pełni edytowalne po konwersji.

W tym samouczku nauczysz się, jak:

* Wczytać istniejący skoroszyt Excel zawierający wykresy.  
* (Opcjonalnie) dostosować ustawienia skoroszytu przed konwersją.  
* Zapisać skoroszyt jako plik PowerPoint, zachowując edytowalność kształtów.  

Wszystko to odbywa się przy użyciu **Aspose.Cells for .NET**, biblioteki obsługującej konwersję Excel‑do‑PowerPoint bez wymogu posiadania Microsoft Office na serwerze.

## Czego będziesz potrzebować

| Wymaganie | Powód |
|-------------|--------|
| .NET 6.0 lub nowszy | Nowoczesny runtime z pełnym zestawem funkcji językowych |
| Visual Studio 2022 (lub dowolne IDE) | Wygodny edytor i debugger |
| **Aspose.Cells for .NET** NuGet package | Udostępnia klasę `Workbook` oraz obsługę `SaveFormat.Pptx` |
| Plik Excel (`ChartAndShapes.xlsx`) zawierający przynajmniej jeden wykres | Źródło wykresów, które chcesz wyeksportować |

> **Pro tip:** Użyj darmowej wersji **Aspose.Cells Evaluation**, aby przetestować kod; klucz licencyjny usuwa znak wodny wersji ewaluacyjnej.

```bash
dotnet add package Aspose.Cells
```

## Eksport wykresów Excel do PowerPoint – pełny przepływ pracy

Poniżej znajduje się kompletny kod, który realizuje eksport przy **zachowaniu edytowalności kształtów**. Każdy krok jest szczegółowo wyjaśniony.

### Krok 1: Wczytaj skoroszyt Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Klasa `Workbook` reprezentuje cały plik Excel. Wczytanie pliku odczytuje wszystkie arkusze, wykresy i kształty do pamięci, co jest wymagane do dalszej manipulacji.*

### Krok 2: (Opcjonalnie) Dostosuj ustawienia skoroszytu

W większości przypadków domyślne ustawienia są wystarczające do czystego eksportu. Jednak jeśli musisz zmienić tryb obliczeń, ustawienia strony lub ukryć niektóre arkusze, możesz zrobić to tutaj.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Dlaczego to ważne:** Dostosowanie ustawień przed konwersją zapewnia, że wygenerowane slajdy odzwierciedlają dokładny stan, którego oczekujesz, szczególnie gdy formuły lub ukryte arkusze mogą wpływać na dane wykresu.

### Krok 3: Zapisz skoroszyt jako plik PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Stała `SaveFormat.Pptx` informuje Aspose.Cells, aby zapisał prezentację PowerPoint. Wewnątrz biblioteka konwertuje każdy wykres Excel na kształt PowerPoint, który pozostaje w pełni edytowalny w Microsoft PowerPoint.*

### Krok 4: Zweryfikuj wynik

Otwórz `Shapes.pptx` w PowerPoint i:

1. Wybierz wykres na dowolnym slajdzie.  
2. Kliknij prawym przyciskiem → **Edit Data**.  
3. Potwierdź, że pojawia się tabela danych wykresu i możesz modyfikować wartości.

Jeśli wykres otwiera panel **Edit Data**, konwersja zakończyła się sukcesem i **edytowalność kształtów** została zachowana.

![Przykład eksportu wykresów Excel do PowerPoint](export-excel-charts-to-powerpoint.png){.img-fluid alt="Przykład eksportu wykresów Excel do PowerPoint"}

## Częste pułapki i jak ich unikać

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| Wykresy pojawiają się jako statyczne obrazy | Użycie starszej wersji Aspose.Cells, która nie obsługuje eksportu PPTX | Uaktualnij do najnowszej wersji Aspose.Cells 23.x lub nowszej |
| Brak danych w wykresie PowerPoint | Skoroszyt nie został w pełni obliczony przed eksportem | Wywołaj `workbook.CalculateFormula()` przed `Save` |
| Kształty nie są edytowalne | Zapisywanie z `SaveFormat.Xlsx` zamiast `SaveFormat.Pptx` | Upewnij się, że przekazujesz `SaveFormat.Pptx` do `Workbook.Save` |
| Wyjątek licencji w czasie wykonywania | Wersja ewaluacyjna bez zarejestrowanej licencji | Zarejestruj licencję przy użyciu `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Przypadek brzegowy: Eksportowanie wielu arkuszy z oddzielnymi wykresami

Jeśli Twój plik Excel zawiera kilka arkuszy, z których każdy ma własny wykres, Aspose.Cells automatycznie tworzy osobny slajd dla każdego wykresu. Kolejność slajdów możesz kontrolować, przestawiając arkusze przed operacją zapisu.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Wskazówka dotycząca wydajności: Strumieniuj wyjście zamiast zapisywać na dysk

Podczas generowania plików PowerPoint w API webowym, unikaj plików tymczasowych, zapisując do `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Pełny, gotowy do uruchomienia przykład

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Oczekiwany wynik:** Konsola wyświetla komunikat potwierdzający, a `Shapes.pptx` otwiera się w PowerPoint, przy czym każdy wykres Excel pojawia się na osobnym slajdzie. Wybranie wykresu pozwala edytować jego dane, potwierdzając, że **edytowalność kształtów** została zachowana.

## Podsumowanie i dalsze kroki

Teraz wiesz, jak **wyeksportować wykresy Excel do PowerPoint** przy użyciu C#, zachowując wykresy w pełni edytowalne. Głównym elementem rozwiązania jest metoda `Workbook.Save` z `SaveFormat.Pptx`, funkcja **Eksportu Aspose.Cells**, która ukrywa złożoną obsługę Open XML.

Od tego momentu możesz zbadać:

* Dodawanie własnych tytułów slajdów lub notatek przy użyciu API **Aspose.Slides**.  
* Konwertowanie innych obiektów Excel (tabele, obrazy) wraz z wykresami.  
* Automatyzację przetwarzania wsadowego wielu skoroszytów w usłudze w tle.

Śmiało eksperymentuj z opcjonalnymi ustawieniami przedstawionymi powyżej i włącz ten wzorzec do swoich pipeline'ów raportowych, aby szybko i niezawodnie generować prezentacje PowerPoint.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Eksport wykresu Excel do PowerPoint przy użyciu C# – kompletny przewodnik Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Jak wyeksportować Excel do PowerPoint przy użyciu C# – kompletny przewodnik](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Jak wyeksportować kształty z Excela do PowerPoint – kompletny przewodnik](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}