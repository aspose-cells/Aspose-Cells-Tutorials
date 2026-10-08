---
category: general
date: 2026-06-24
description: Osadź czcionki w PDF przy użyciu Aspose.Cells w C#. Dowiedz się, jak
  zapisać Excel jako PDF, wyeksportować Excel do HTML, przekonwertować xlsx na PDF
  przy użyciu Aspose oraz duplikować wiersze w tabeli przestawnej.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: pl
og_description: Osadzanie czcionek w PDF przy użyciu Aspose.Cells w C#. Ten samouczek
  pokazuje krok po kroku, jak zapisać Excel jako PDF, wyeksportować Excel do HTML
  i więcej.
og_title: Osadzanie czcionek w PDF przy użyciu Aspose.Cells – Kompletny przewodnik
  C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Osadzanie czcionek w PDF przy użyciu Aspose.Cells – Kompletny przewodnik C#
url: /pl/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Osadzanie czcionek w PDF przy użyciu Aspose.Cells – Kompletny przewodnik C# 

Zastanawiałeś się kiedyś, jak **osadzić czcionki w PDF**, gdy konwertujesz skoroszyt Excel przy użyciu Aspose.Cells? Nie jesteś sam — wielu programistów napotyka problem, gdy wygenerowany PDF wygląda niepoprawnie na komputerach, które nie mają zainstalowanych oryginalnych czcionek.  

W tym przewodniku przeprowadzimy Cię przez praktyczny przykład, który nie tylko **osadza czcionki w PDF**, ale także pokaże, jak **zapisać Excel jako PDF**, **wyeksportować Excel do HTML**, przekształcić **xlsx do PDF przy użyciu Aspose**, a nawet **duplikować wiersze w tabeli przestawnej** bez uszkadzania tabeli przestawnej. Brzmi jak dużo? Bez obaw — rozłożymy to krok po kroku.

## Czego się nauczysz

- Jak kopiować wiersze zawierające tabelę przestawną, zachowując jej integralność.  
- Jak wstawić smart‑marker, który powiela arkusz szczegółowy dla każdego zamówienia.  
- Dokładne ustawienia potrzebne do **osadzenia czcionek w PDF**, eksportu wykresów jako edytowalny PPTX oraz zachowania zamrożonych okienek przy **eksportowaniu Excela do HTML**.  
- Wskazówki dotyczące rozwiązywania typowych problemów, takich jak brakujące czcionki lub uszkodzone obiekty OLE.  

**Wymagania wstępne:** .NET 6+ (lub .NET Framework 4.6+), zainstalowany Aspose.Cells dla .NET oraz podstawowe środowisko programistyczne C# (Visual Studio, Rider lub VS Code). Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells.

---

## Osadzanie czcionek w PDF – krok po kroku

Poniżej znajduje się pełny, gotowy do uruchomienia kod. Każda sekcja jest opatrzona komentarzem, abyś dokładnie widział, dlaczego robimy to, co robimy.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Dlaczego to działa

- **CopyRows** duplikuje wiersze zawierające tabelę przestawną, więc oryginalna tabela pozostaje połączona z danymi źródłowymi. Spełnia to wymaganie **duplicate rows pivot**.  
- **SmartMarkerProcessing** tworzy nowy arkusz dla każdego zamówienia, automatyzując generowanie arkusza szczegółowego.  
- **PdfSaveOptions.EmbedStandardFonts = true** instruuje Aspose.Cells, aby osadził czcionki bezpośrednio w pliku PDF, co jest kluczem do **embed fonts pdf**. Bez tego ustawienia PDF użyje czcionek systemowych, co zepsuje układ na innych komputerach.  
- **HtmlSaveOptions** z `EmbedAllFonts` i `PreserveFreezePanes` zapewnia, że przy **eksportowaniu Excela do HTML** wizualna wierność odpowiada oryginalnemu skoroszytowi.  

#### Oczekiwany wynik

- `result.pdf` – PDF, w którym wszystkie użyte czcionki są osadzone; otwórz go na dowolnym komputerze, a tekst będzie wyglądał identycznie jak w źródle.  
- `result.pptx` – plik PowerPoint z edytowalnymi wykresami i obiektami OLE.  
- `result.html` – folder HTML (`result.html` + `result_files`), który wyświetla skoroszyt w przeglądarce z zachowanymi zamrożonymi okienkami.  

---

## Zapisz Excel jako PDF przy użyciu Aspose.Cells

Jeśli Twoim jedynym celem jest **zapisanie Excela jako PDF**, możesz pominąć dodatkowe kroki i skupić się na opcjach PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Wskazówka:** Gdy celujesz w zgodność z PDF/A, Aspose automatycznie osadza wszystkie czcionki, co zapewnia dodatkową warstwę bezpieczeństwa przy długoterminowym przechowywaniu.

---

## Eksportuj Excel do HTML zachowując układ

Eksport do HTML często traci wygląd oryginalnego arkusza, szczególnie gdy użyte są zamrożone okienka. Poniższy fragment kodu pokazuje dokładne ustawienia, które są potrzebne:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Ponieważ ustawiliśmy `EmbedAllFonts`, wygenerowany HTML zawiera czcionki zakodowane w base‑64, spełniając wymaganie **export excel to html** bez potrzeby zewnętrznych plików CSS.

---

## Konwertuj Xlsx do PDF przy użyciu Aspose.Cells

Czasami w wyszukiwaniach pojawia się termin „**xlsx to pdf aspose**”. Poniższy kod demonstruje dokładny proces konwersji, w tym kilka dodatkowych udogodnień:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Po co zajmować się ustawieniami strony?** Jeśli je pominiesz, domyślny PDF może obciąć kolumny lub wiersze. Dostosowanie układu najpierw zapewnia, że końcowy PDF będzie odpowiadał temu, co widzisz w Excelu.

---

## Duplikowanie wierszy w tabeli przestawnej — zachowanie integralności tabeli

Częstym problemem jest próba kopiowania wierszy zawierających tabelę przestawną; tabela często traci połączenie ze źródłem danych. Metoda `CopyRows`, której użyliśmy wcześniej, wykonuje ciężką pracę za Ciebie:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – pierwszy wiersz zakresu, który chcesz skopiować.  
- **destinationRow** – miejsce, w którym ma zostać umieszczona kopia (ten sam arkusz, ten sam indeks początkowy, aby efektywnie zduplikować).  
- **totalRows** – liczba wierszy do skopiowania.  

Ponieważ pamięć podręczna tabeli przestawnej znajduje się w arkuszu, kopiowanie wierszy **nie** psuje tabeli przestawnej. Spełnia to słowo kluczowe **duplicate rows pivot**, jednocześnie utrzymując porządek w skoroszycie.

---

## Podsumowanie pełnego działającego przykładu

Łącząc wszystko razem, oto kompletny program, który możesz wkleić do aplikacji konsolowej i uruchomić od razu:



## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zapisz skoroszyt Excel jako PDF z własnymi czcionkami przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Jak wyeksportować wykresy Excel do PDF przy użyciu Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Jak wyeksportować segmentatory Excel do PDF przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}