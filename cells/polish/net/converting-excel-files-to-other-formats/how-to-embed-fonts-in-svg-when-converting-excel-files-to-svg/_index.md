---
category: general
date: 2026-09-15
description: Dowiedz się, jak osadzać czcionki w SVG i eksportować wykresy z Excela
  do PowerPointa, obejmując konwersję XLSX do SVG oraz konwersję XLSX do PPTX wraz
  z pełnymi przykładami kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: pl
lastmod: 2026-09-15
og_description: Osadź czcionki w SVG i wyeksportuj wykres Excel do PowerPointa za
  pomocą krok po kroku kodu C#. Szybko i niezawodnie konwertuj XLSX na SVG oraz XLSX
  na PPTX.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Osadzanie czcionek w SVG i eksport wykresu z Excela do PowerPointa – kompletny
  przewodnik
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak osadzić czcionki w SVG przy konwertowaniu plików Excel do SVG i PowerPointa
url: /pl/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak osadzić czcionki w SVG podczas konwertowania plików Excel do SVG i PowerPoint  

Jeśli potrzebujesz **osadzić czcionki w SVG** podczas konwertowania skoroszytu Excel, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Dowiesz się także, jak **wyeksportować wykres Excel do PowerPoint**, oraz jak **konwertować XLSX do SVG** i **konwertować XLSX do PPTX** z edytowalnymi wykresami.  

Praca z danymi Excel programowo często oznacza konieczność przenoszenia tej samej treści wizualnej między różnymi formatami plików. Ręczne odtwarzanie wykresu w PowerPoint lub ponowne stosowanie czcionek w SVG jest podatne na błędy i czasochłonne. Po zakończeniu tego samouczka będziesz mieć pojedynczy, wielokrotnego użytku fragment kodu C#, który:

* Zapisuje skoroszyt jako plik SVG z osadzonymi czcionkami i selektorami wariacji czcionek.  
* Eksportuje ten sam skoroszyt do pliku PPTX, w którym wykres pozostaje edytowalny.  

Jedynym wymogiem wstępnym jest aktualna wersja **Aspose.Cells for .NET** (2024‑x lub nowsza) oraz środowisko programistyczne .NET, takie jak Visual Studio 2022.

---

## Czego będziesz potrzebować  

* .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.8).  
* Pakiet NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Plik Excel (`input.xlsx`) zawierający przynajmniej jeden wykres.  
* Uprawnienia zapisu do katalogu wyjściowego.  

---

## Osadzanie czcionek w SVG podczas konwertowania XLSX do SVG  

Osadzanie czcionek zapewnia, że SVG renderuje się poprawnie na każdym urządzeniu, nawet jeśli docelowy system nie posiada oryginalnych krojów pisma. Klasa `SvgSaveOptions` udostępnia dwa flagi umożliwiające to: `EmbedFonts` i `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Dlaczego to działa:**  
* `EmbedFonts = true` kopiuje pliki czcionek do sekcji `<defs>` SVG, eliminując zależności zewnętrzne.  
* `FontVariationSelectors = true` dodaje niezbędne selektory dla czcionek obsługujących funkcje OpenType, zachowując wariacje glifów, takie jak ligatury.  

**Oczekiwany rezultat:** Otwórz `WithFonts.svg` w dowolnej nowoczesnej przeglądarce; tekst wewnątrz wykresu lub komórek wyświetla się dokładnie taką czcionką, jaka była użyta w Excelu, nawet na maszynach, które nie mają tej czcionki zainstalowanej.

---

## Eksport wykresu Excel do PowerPoint z edytowalnymi wykresami  

Jeśli musisz osadzić wykres na slajdzie PowerPoint, ale jednocześnie umożliwić odbiorcy edycję danych wykresu, `PptxSaveOptions` z Aspose.Cells oferuje flagę `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Dlaczego to ważne:**  
Ustawienie `ExportEditableChart` na `true` zapisuje wykres jako obiekt wykresu Office Open XML, a nie jako statyczny obraz. Po otwarciu `EditableChart.pptx` w PowerPoint możesz kliknąć prawym przyciskiem myszy wykres → **Edit Data** i modyfikować serie tak, jak w natywnym wykresie PowerPoint.

**Kroki weryfikacji:**  

1. Otwórz `EditableChart.pptx` w PowerPoint.  
2. Znajdź slajd zawierający wykres.  
3. Wybierz **Chart Tools → Design → Edit Data**.  
4. Potwierdź, że pojawia się siatka danych w stylu Excel i że możesz zmieniać wartości.

---

## Konwersja XLSX do SVG – podsumowanie pełnego przepływu pracy  

Poniżej znajduje się kompaktowa wersja, która łączy wczytywanie, opcjonalną manipulację danymi i zapisywanie jako SVG. Użyj jej, gdy potrzebujesz jedynie wyjścia SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Wywołaj metodę w następujący sposób:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Wskazówka dotycząca przypadków brzegowych:** Jeśli Twój skoroszyt zawiera niestandardowe czcionki, które nie są zainstalowane na serwerze, osadź je ręcznie przed wywołaniem `Save`. Użyj `FontInfoCollection`, aby dodać pliki czcionek do `SvgSaveOptions` poprzez właściwość `CustomFonts` (dostępna w nowszych wydaniach Aspose.Cells).

---

## Konwersja XLSX do PPTX – zachowanie edytowalności wykresu  

Poniższa metoda pomocnicza demonstruje ścieżkę **convert XLSX to PPTX**, zapewniając jednocześnie, że wykres pozostaje edytowalny.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Użycie:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Częste pytanie:** *Co jeśli mój skoroszyt ma wiele arkuszy z wykresami?*  
**Odpowiedź:** Aspose.Cells domyślnie eksportuje pierwszy arkusz. Aby uwzględnić dodatkowe arkusze, iteruj po `workbook.Worksheets`, kopiuj każdy wykres na nowy slajd i zapisuj każdy slajd osobno przy użyciu obiektów `Presentation` z Aspose.Slides. Ten zaawansowany scenariusz wykracza poza podstawowy przepływ „zapisz skoroszyt jako SVG” i „wyeksportuj wykres Excel do PowerPoint”, ale podstawowe flagi pozostają takie same.

---

## Praktyczne wskazówki i pułapki  

* **Wydajność:** Osadzanie czcionek zwiększa rozmiar pliku SVG. Jeśli rozmiar jest istotny, ustaw `EmbedFonts = false` i korzystaj z czcionek web‑safe.  
* **Licencjonowanie czcionek:** Upewnij się, że masz prawo do osadzania używanych czcionek; niektóre czcionki komercyjne ograniczają osadzanie.  
* **Kompatybilność wykresów:** Edytowalne wykresy są zapisywane jako części `chart.xml` wewnątrz PPTX. Bardzo złożone wykresy (np. 3‑D lub wykresy kombinowane) mogą utracić część stylizacji po edycji w PowerPoint. Przetestuj najczęściej używane typy wykresów.  
* **Niezgodności wersji:** Flaga `ExportEditableChart` wymaga Aspose.Cells 20.10 lub nowszej. Użycie starszej wersji spowoduje ciche przejście na obraz rastrowy.  
* **Bezpieczeństwo wątków:** Obiekty Workbook nie są bezpieczne wątkowo. Twórz nową instancję `Workbook` dla każdego żądania w scenariuszu usługi webowej.  

---

## Pełny przykład end‑to‑end  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Uruchomienie tego programu generuje dwa pliki:

* **WithFonts.svg** – SVG, który renderuje się dokładnie tak jak widok w Excel, z osadzonymi czcionkami.  
* **EditableChart.pptx** – prezentacja PowerPoint, w której wykres można edytować bezpośrednio.

---

## Zakończenie  

Teraz wiesz, jak **osadzić czcionki w SVG** podczas **konwertowania XLSX do SVG**, oraz jak **wyeksportować wykres Excel do PowerPoint**, zachowując edytowalność wykresu. Ten sam kod pokazuje również czysty sposób na **zapisanie skoroszytu jako SVG** i **konwersję XLSX do PPTX** przy minimalnym wysiłku.  

Od tego momentu możesz zgłębiać dalsze tematy, takie jak:

* Dodawanie niestandardowych czcionek programowo (`svgOptions.CustomFonts`).  
* Przetwarzanie wsadowe wielu skoroszytów w usłudze w tle.  
* Użycie Aspose.Slides do tworzenia wieloslajdowych plików PPTX, które łączą kilka wykresów Excel.  

Eksperymentuj z opcjami, dostosuj fragmenty kodu do swojego projektu i ciesz się niezawodnymi konwersjami Excel‑do‑SVG/PPTX bez ręcznego przetwarzania po konwersji. Szczęśliwego kodowania!

## Co powinieneś się nauczyć dalej?

Następujące samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}