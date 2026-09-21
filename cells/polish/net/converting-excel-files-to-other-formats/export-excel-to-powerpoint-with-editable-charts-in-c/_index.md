---
category: general
date: 2026-09-21
description: Eksportuj Excel do PowerPointa z edytowalnymi wykresami przy użyciu Aspose.Cells.
  Postępuj zgodnie z tym przewodnikiem krok po kroku, aby przekonwertować arkusz kalkulacyjny
  na PPTX, zachowując edytowalność wykresów.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: pl
lastmod: 2026-09-21
og_description: Eksportuj Excel do PowerPointa z edytowalnymi wykresami przy użyciu
  Aspose.Cells. Dowiedz się, jak przekonwertować arkusz kalkulacyjny na PPTX, zachowując
  pełną edytowalność wykresów.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Eksportuj Excel do PowerPointa z edytowalnymi wykresami – samouczek C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Eksportuj Excel do PowerPointa z edytowalnymi wykresami w C#
url: /pl/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportuj Excel do PowerPoint z edytowalnymi wykresami w C#

Eksportowanie Excela do PowerPointa z edytowalnymi wykresami jest powszechnym wymaganiem, gdy potrzebujesz ponownie wykorzystać wizualizacje arkusza kalkulacyjnego w prezentacjach. Ten przewodnik pokazuje, jak **eksportować Excel do PowerPoint** zachowując możliwość edycji wykresów, używając Aspose.Cells dla .NET.

Dowiesz się jak:

* Załadować istniejący skoroszyt zawierający wykresy i pola tekstowe.  
* Skonfigurować opcje eksportu PPTX, aby wykresy i kształty pozostały edytowalne.  
* Przekonwertować konkretny arkusz na plik PowerPoint, który można otworzyć i edytować w Microsoft PowerPoint.

Tutorial zakłada, że masz podstawową znajomość C# oraz aktualną wersję .NET (≥ .NET 6). Wcześniejsze doświadczenie z Aspose.Cells nie jest wymagane.

---

## Eksport Excel do PowerPoint – przegląd

Główna idea stojąca za **eksportem Excel do PowerPoint** polega na traktowaniu każdego arkusza jako źródła obrazu, które może zostać wyrenderowane na slajdzie PPTX. Przełączając flagi `ExportChartAsEditableText` i `ExportShapeAsEditableText`, Aspose.Cells zapisuje podstawowe dane wykresu jako obiekty rysunkowe PowerPoint zamiast płaskiego bitmapy. Dzięki temu powstały slajd jest w pełni edytowalny — tak jak wykres utworzony bezpośrednio w PowerPoint.

> **Dlaczego używać edytowalnych wykresów?**  
> Edytowalne wykresy pozwalają prezenterom dostosować dane, kolory lub etykiety bez powrotu do oryginalnego pliku Excel, przyspieszając zmiany w ostatniej chwili i utrzymując płynny przebieg pracy nad prezentacją.

---

## Konwersja arkusza do PowerPoint (worksheet to PowerPoint)

Poniżej znajduje się kompletny, gotowy do uruchomienia przykład, który demonstruje konwersję **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Wyjaśnienie każdego kroku

| Krok | Co robi kod | Dlaczego ma znaczenie dla **export excel chart pptx** |
|------|-------------|------------------------------------------------------|
| 1️⃣   | Ładuje `input.xlsx` do obiektu `Aspose.Cells.Workbook`. | Skoroszyt zapewnia dostęp do wykresów, które chcesz wyeksportować. |
| 2️⃣   | Ustawia `ExportType` na `Pptx` i włącza `ExportChartAsEditableText` oraz `ExportShapeAsEditableText`. | Te flagi są kluczem do **editable charts pptx** – informują bibliotekę, aby zapisywała geometrię wykresu jako obiekty rysunkowe PowerPoint zamiast obrazów rastrowych. |
| 3️⃣   | Wywołuje `ConvertToImage` na pierwszym arkuszu, tworząc `Worksheet.pptx`. | Metoda wykonuje operację **export excel to powerpoint** i zapisuje plik PPTX, który można otworzyć bezpośrednio w PowerPoint. |

> **Wskazówka:** Jeśli potrzebujesz wyeksportować *wiele* arkuszy, iteruj po `workbook.Worksheets` i wywołuj `ConvertToImage` dla każdego, opcjonalnie nazywając pliki wyjściowe `Sheet1.pptx`, `Sheet2.pptx` itd.

---

## Włącz edytowalne wykresy w PPTX (export excel chart pptx)

Gdy `ExportChartAsEditableText` jest ustawione na `true`, Aspose.Cells zapisuje każdy wykres jako kolekcję elementów `<a:graphic>` wewnątrz XML‑a PPTX. PowerPoint traktuje te elementy jako natywne obiekty wykresu, które można dwukrotnie kliknąć, aby otworzyć edytor wykresu.

**Typowe pułapki**

* **Brak licencji Aspose.Cells** – Bez licencji biblioteka dodaje znak wodny do wyniku. Zarejestruj licencję wcześnie w programie (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Nieobsługiwane typy wykresów** – Chociaż większość wykresów 2‑D (kolumnowy, liniowy, kołowy) jest w pełni edytowalna, niektóre złożone wykresy 3‑D lub kombinowane mogą zostać zamienione na obrazy. Przetestuj konkretne typy wykresów, jeśli zależy Ci na pełnej edytowalności.  
* **Duże arkusze** – Eksport bardzo dużych arkuszy może zużywać znaczną ilość pamięci. Rozważ użycie `ExportMaxRows` lub `ExportMaxColumns` w `ImageOrPrintOptions`, aby ograniczyć obszar konwertowany.

---

## Wskazówki dotyczące utrzymania wykresów edytowalnych (editable charts pptx)

1. **Zachowaj zakresy danych wykresu** – Upewnij się, że źródło danych wykresu znajduje się w tym samym arkuszu, który eksportujesz. Odwołania do innych arkuszy są konwertowane na wartości statyczne w PPTX.  
2. **Używaj najnowszej wersji Aspose.Cells** – Nowe wydania poprawiają wsparcie dla dodatkowych funkcji wykresów i naprawiają rzadkie błędy związane z eksportem PPTX.  
3. **Zweryfikuj wynik** – Po konwersji otwórz wygenerowany PPTX w PowerPoint i sprawdź, czy możesz edytować tytuł wykresu, serie i etykiety osi. Jeśli którykolwiek element pojawi się jako obraz, sprawdź ponownie, czy `ExportChartAsEditableText` jest włączone i czy typ wykresu jest obsługiwany.  
4. **Przetwarzanie wsadowe** – W scenariuszach automatyzacji (np. generowanie zestawu slajdów z wielu raportów Excel), opakuj logikę konwersji w metodę przyjmującą `Workbook`, `int worksheetIndex` oraz `string outputPath`. To izoluje przepływ pracy **export excel to powerpoint** i czyni go wielokrotnego użytku.

---

## Podsumowanie pełnego działającego przykładu

Łącząc wszystko razem, oto minimalny program, który możesz skopiować i wkleić do nowego projektu konsolowego .NET:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Oczekiwany wynik**

* Plik o nazwie `Worksheet.pptx` pojawia się w `YOUR_DIRECTORY`.  
* Otwierając plik w Microsoft PowerPoint, wyświetla się slajd zawierający oryginalny wykres oraz wszelkie pola tekstowe.  
* Dwukrotne kliknięcie wykresu otwiera edytor wykresów PowerPoint, umożliwiając zmianę wartości serii, kolorów lub tytułów osi — potwierdzając, że funkcja **editable charts pptx** działa zgodnie z zamierzeniami.

---

## Zakończenie

Masz teraz kompletną rozwiązanie do **export Excel to PowerPoint**, które zachowuje edytowalność wykresów. Konfigurując `ImageOrPrintOptions` z `ExportChartAsEditableText` i `ExportShapeAsEditableText`, proces konwersji tworzy natywny plik PPTX, w którym wykresy zachowują się tak, jakby zostały utworzone bezpośrednio w PowerPoint.

Od tego momentu możesz:

* Rozszerzyć kod, aby obsługiwał wiele arkuszy (**worksheet to PowerPoint** dla każdego).  
* Połączyć eksport z innymi funkcjami Aspose.Cells, takimi jak dodawanie tytułów slajdów lub wstawianie obrazów.  
* Zbadać powiązane tematy, takie jak **export Excel chart PPTX** z własnymi motywami lub automatyzacja całego procesu generowania zestawu slajdów.

Śmiało eksperymentuj z różnymi typami wykresów, dodawaj etykiety danych lub integruj ten przepływ pracy w większym systemie raportowania. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak przekonwertować Excel do PowerPoint przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}