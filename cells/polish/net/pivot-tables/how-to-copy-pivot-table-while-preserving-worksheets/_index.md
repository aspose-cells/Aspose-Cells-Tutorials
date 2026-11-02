---
category: general
date: 2026-09-15
description: Dowiedz się, jak skopiować tabelę przestawną, skopiować arkusz z tabelą
  przestawną oraz zapisać skoroszyt jako pptx przy użyciu Aspose.Cells w C#. Kompletny
  przewodnik krok po kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: pl
lastmod: 2026-09-15
og_description: Jak skopiować tabelę przestawną, skopiować arkusz z tabelą przestawną
  oraz zapisać skoroszyt jako plik pptx przy użyciu Aspose.Cells. Zapoznaj się z kompletnymi,
  gotowymi do uruchomienia przykładami w C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Jak skopiować tabelę przestawną i wyeksportować arkusze – pełny przewodnik
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak skopiować tabelę przestawną, zachowując arkusze
url: /pl/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną zachowując arkusze

Jeśli potrzebujesz **how to copy pivot table** z jednego skoroszytu do drugiego bez utraty podstawowego cache tabeli przestawnej, ten przewodnik zapewnia gotowe rozwiązanie. Zobaczysz także, jak **copy worksheet with pivot** oraz jak **save workbook as pptx** zachowując edytowalne pola tekstowe. Wszystkie przykłady używają najnowszego Aspose.Cells for .NET, więc możesz wkleić kod do dowolnego projektu C# i od razu zobaczyć wyniki.

Praca z plikami Excel programowo często wiąże się z przenoszeniem danych między skoroszytami, eksportowaniem do prezentacji lub wstawianiem złożonych Smart Markerów. Poniższe trzy fragmenty kodu obejmują te typowe scenariusze i wyjaśniają, dlaczego każdy krok ma znaczenie.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany  
* Aspose.Cells for .NET (wersja 25.11 lub nowsza) odwołany w projekcie  
* Folder o nazwie `YOUR_DIRECTORY`, w którym będą odczytywane i zapisywane pliki przykładowe  

Nie są wymagane dodatkowe pakiety NuGet.

---

## Jak skopiować tabelę przestawną przy użyciu Aspose.Cells

Kopiowanie zakresu zawierającego tabelę przestawną przy zachowaniu cache tabeli przestawnej jest częstym wymaganiem. Poniższe kroki pokazują dokładną sekwencję, której potrzebujesz.

### Krok 1 – Załaduj źródłowy skoroszyt zawierający tabelę przestawną

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Dlaczego*: Aspose.Cells odczytuje skoroszyt do pamięci, dając dostęp do arkuszy, komórek i tabel przestawnych.

### Krok 2 – Utwórz pusty docelowy skoroszyt

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Dlaczego*: Rozpoczęcie od pustego skoroszytu zapewnia, że żadne ukryte style ani nazwy zakresów nie będą interferować z operacją kopiowania.

### Krok 3 – Skopiuj wiersze zawierające tabelę przestawną

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Dlaczego*: `CopyRows` kopiuje surowe wartości komórek, formaty oraz odwołania do podstawowego cache tabeli przestawnej. Zakres musi obejmować cały obszar tabeli przestawnej.

### Krok 4 – Skopiuj kolumny zawierające tabelę przestawną

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Dlaczego*: Tabele przestawne rozciągają się zarówno na wiersze, jak i kolumny; kopiowanie kolumn zapewnia zachowanie pełnego układu tabeli.

### Krok 5 – Przenieś przygotowany arkusz do docelowego skoroszytu

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Dlaczego*: Metoda `Copy` klonuje arkusz, włącznie z cache tabeli przestawnej, więc docelowy skoroszyt wyświetla identyczną tabelę przestawną.

### Krok 6 – Zapisz wynik – tabela przestawna pozostaje nienaruszona

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Dlaczego*: Zapisanie skoroszytu zapisuje wszystkie wewnętrzne struktury, gwarantując, że tabela przestawna będzie mogła być odświeżona później.

**Wskazówka**: Po skopiowaniu możesz wywołać `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()`, aby zaktualizować dane, jeśli źródłowe dane uległy zmianie.

---

## Kopiowanie arkusza z tabelą przestawną – zwięzła alternatywa

Jeśli po prostu potrzebujesz zduplikować cały arkusz, który już zawiera tabelę przestawną, możesz pominąć kroki kopiowania wierszy/kolumn i użyć metody `Copy` na poziomie arkusza bezpośrednio.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

To podejście jest przydatne, gdy arkusz nie zawiera dodatkowych danych poza obszarem tabeli przestawnej. Operacja **copy worksheet with pivot** automatycznie zachowuje wszystkie formatowania, nazwy zakresów i cache tabel przestawnych.

---

## Zapisz skoroszyt jako PPTX z edytowalnymi polami tekstowymi

Eksportowanie arkusza Excel zawierającego edytowalne pole tekstowe do PowerPoint może być wymagane przy pulpitach raportowych. Poniższy kod pokazuje **save workbook as pptx** przy zachowaniu edytowalności pola tekstowego.

### Krok 1 – Załaduj skoroszyt, który zawiera pole tekstowe

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Krok 2 – Skonfiguruj opcje zapisu PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Dlaczego*: Ustawienie `ExportEditableTextBox` instruuje Aspose.Cells, aby przetłumaczył pole tekstowe z Excela na kształt PowerPoint, który pozostaje edytowalny po eksporcie.

### Krok 3 – Zapisz skoroszyt jako PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Oczekiwany rezultat**: Otwórz `Result.pptx` w PowerPoint, zaznacz pole tekstowe i edytuj jego zawartość tak jak każde natywne kształty.

**Częste pytanie**: *Co zrobić, jeśli muszę zablokować pole tekstowe?*  
Ustaw `pptxOptions.ExportEditableTextBox = false`; kształt zostanie przekształcony w statyczny obraz.

---

## Eksportuj Smart Marker zawierający tablicę JSON jako wartość pojedynczej komórki

Smart Markery pozwalają wypełniać szablony Excel złożonymi strukturami danych. Poniżej pełny przykład, który demonstruje obsługę danych w stylu **how to copy pivot table** przy wstawianiu tablicy JSON do jednej komórki.

### Krok 1 – Przygotuj SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Krok 2 – Wstaw Smart Marker do komórki A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Krok 3 – Zdefiniuj źródło danych z tablicą w stylu JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Krok 4 – Przetwórz skoroszyt

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Krok 5 – Zapisz wynikowy skoroszyt

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Weryfikacja wyniku**: Otwórz `JsonSingleCell.xlsx` i potwierdź, że komórka A1 zawiera `A,B,C`. To pokazuje, jak traktować kolekcję jako wartość pojedynczej komórki, co jest często potrzebne przy eksporcie danych do systemów downstream.

---

## Pełny działający przykład

Poniżej znajduje się pojedynczy program łączący trzy scenariusze. Możesz skopiować kod do aplikacji konsolowej, dostosować ścieżki plików i uruchomić go, aby zobaczyć wszystkie trzy wyniki.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Uruchomienie tego programu generuje:

* `CopyWithPivot.xlsx` – idealna kopia oryginalnej tabeli przestawnej.  
* `Result.pptx` – slajd PowerPoint z edytowalnym polem tekstowym.  
* `JsonSingleCell.xlsx` – arkusz, w którym tablica JSON pojawia się w jednej komórce.

---

## Zakończenie

Teraz wiesz, jak bezpiecznie **how to copy pivot table**, jak **copy worksheet with pivot** w jednym wywołaniu oraz jak **save workbook as pptx** zachowując edytowalne pola tekstowe. Te wzorce obejmują najczęstsze przepływy pracy Excel‑do‑PowerPoint i Excel‑do‑JSON, które napotkasz w projektach automatyzacji przedsiębiorstw.

Następnie rozważ eksplorację:

* Odświeżanie skopiowanych tabel przestawnych programowo (`PivotTable.Refresh()`)  
* Eksportowanie do innych formatów, takich jak PDF lub HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Korzystanie z zaawansowanych opcji Smart Marker, takich jak funkcje niestandardowe lub formatowanie warunkowe  

Śmiało eksperymentuj z różnymi zakresami, wieloma arkuszami lub większymi strukturami JSON. API Aspose.Cells daje precyzyjną kontrolę, więc możesz dostosować te przykłady do dowolnego scenariusza rzeczywistego. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz nowy skoroszyt – Jak skopiować arkusz z tabelą przestawną](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Jak skopiować tabelę przestawną w C# – Konwertuj Excel do PPTX, kopiuj zakres i twórz pole tekstowe](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Kopiowanie arkuszy w obrębie skoroszytu przy użyciu Aspose.Cells for .NET – Przewodnik krok po kroku](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}