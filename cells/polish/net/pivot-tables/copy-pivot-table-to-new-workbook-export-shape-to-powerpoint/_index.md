---
category: general
date: 2026-10-20
description: Skopiuj tabelę przestawną do nowego skoroszytu przy użyciu Aspose.Cells
  i dowiedz się, jak wyeksportować edytowalny kształt do PowerPointa w jednym przewodniku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: pl
lastmod: 2026-10-20
og_description: Skopiuj tabelę przestawną do nowego skoroszytu przy użyciu Aspose.Cells
  i wyeksportuj edytowalny kształt do PowerPointa — krok po kroku kod, który możesz
  uruchomić już dziś.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Skopiuj tabelę przestawną do nowego skoroszytu, wyeksportuj kształt do PowerPointa
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Skopiuj tabelę przestawną do nowego skoroszytu, wyeksportuj kształt do PowerPointa
url: /pl/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skopiuj tabelę przestawną do nowego skoroszytu, wyeksportuj kształt do PowerPointa

Jeśli potrzebujesz **skopiować tabelę przestawną do nowego skoroszytu** zachowując jej funkcjonalność, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells. Zobaczysz także najszybszy sposób na **wyeksportować edytowalny kształt do PowerPointa**, aby pole tekstowe pozostało edytowalne po konwersji.

Wielu programistów zakłada, że kopiowanie zakresu zawierającego tabelę przestawną spowoduje utratę logiki przestawnej, lub że kształty stają się statycznymi obrazami po zapisaniu jako PPTX. Ten tutorial obala te mity i dostarcza niezawodne, gotowe do produkcji rozwiązanie.

W kolejnych sekcjach dowiesz się, jak:

* Załadować skoroszyt źródłowy i skopiować zakres zawierający tabelę przestawną.
* Utworzyć skoroszyt docelowy, który zawiera tę samą tabelę przestawną.
* Dodać kształt pola tekstowego, zmodyfikować jego tekst i zapisać skoroszyt jako prezentację PowerPoint, w której pole tekstowe pozostaje edytowalne.
* Zrozumieć, dlaczego każde wywołanie API jest wymagane i jak unikać typowych pułapek.

**Wymagania wstępne**

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+).
* Aspose.Cells dla .NET zainstalowany (`Install-Package Aspose.Cells`).
* Podstawowa znajomość C# i Visual Studio (lub dowolnego ulubionego IDE).

---

## Skopiuj tabelę przestawną do nowego skoroszytu

Ten sekcja krok po kroku pokazuje, jak skopiować zakres zawierający tabelę przestawną i zachować definicję przestawnej w nowym pliku.

### Krok 1 – Załaduj skoroszyt źródłowy i wybierz pierwszą arkusz

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Dlaczego?*  
`Workbook` jest punktem wejścia do wszelkich operacji na Excelu w Aspose.Cells. Wybranie właściwego arkusza zapewnia, że pracujemy z dokładnym miejscem tabeli przestawnej.

### Krok 2 – Zdefiniuj obszar komórek, który obejmuje tabelę przestawną

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Dlaczego?*  
Tabela przestawna znajduje się w określonym bloku komórek. Określając `CellArea`, który w pełni obejmuje przestawną, Aspose.Cells wie, że ma skopiować również ukryty cache przestawnej.

### Krok 3 – Utwórz skoroszyt docelowy i pobierz jego pierwszy arkusz

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Dlaczego?*  
Nowy skoroszyt gwarantuje brak konfliktujących nazwanych zakresów lub istniejących przestawnych, co sprawia, że operacja kopiowania jest czysta.

### Krok 4 – Skopiuj wiersze z obszaru źródłowego do arkusza docelowego

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Dlaczego?*  
`CopyRows` jest częścią **Aspose.Cells copy rows** API. Kopiuje zarówno wartości komórek, jak i ukryty cache przestawnej, dzięki czemu tabela przestawna pozostaje funkcjonalna po przeniesieniu.

### Krok 5 – Zapisz nowy skoroszyt

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Wynik*  
Otwórz `CopyWithPivot.xlsx` w Excelu. Tabela przestawna pojawia się dokładnie tak, jak w pliku źródłowym i możesz ją odświeżać lub modyfikować w normalny sposób.

---

## Wyeksportuj edytowalny kształt do PowerPointa

Teraz dodamy kształt pola tekstowego, zmienimy jego zawartość i zapiszemy skoroszyt jako plik PPTX. Kształt pozostaje w pełni edytowalny po otwarciu w PowerPoint.

### Krok 1 – Utwórz nowy skoroszyt i uzyskaj dostęp do jego pierwszego arkusza

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Krok 2 – Dodaj kształt pola tekstowego do arkusza

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Dlaczego?*  
`AddTextBox` tworzy **edytowalne pole tekstowe kompatybilne z PowerPoint**. Współrzędne podawane są w punktach; dostosuj je do swojego układu.

### Krok 3 – Pobierz kształt i zmodyfikuj jego tekst

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Dlaczego?*  
Bezpośredni dostęp do obiektu `Shape` pozwala zmieniać właściwości takie jak `Text`, `Font` czy `Fill`. Ten krok demonstruje, jak programowo ustawić początkową treść.

### Krok 4 – Zapisz skoroszyt jako prezentację PowerPoint

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Wynik*  
Otwórz `Presentation.pptx` w Microsoft PowerPoint. Pole tekstowe pojawia się na pierwszym slajdzie i możesz dwukrotnie kliknąć, aby edytować tekst tak, jak w natywnym kształcie PowerPoint.

---

## Oczekiwany wynik

| Plik | Co zobaczysz |
|------|-----------------|
| `CopyWithPivot.xlsx` | Arkusz zawierający oryginalną tabelę przestawną, w pełni funkcjonalną (odświeżanie działa). |
| `Presentation.pptx` | Jeden slajd z edytowalnym polem tekstowym, które zawiera tekst „Change me in PowerPoint”. |

---

## Typowe pułapki i wskazówki najlepszych praktyk

* **Utrata cache przestawnej** – Jeśli kopiujesz tylko wartości komórek (np. używając `CopyRows` z flagą `PasteOptions` ustawioną na `PasteValues`), cache przestawnej jest pomijany i tabela staje się statyczna. Zawsze używaj domyślnego przeciążenia `CopyRows`, jak pokazano.
* **Pozycjonowanie kształtu** – `AddTextBox` używa jednostek punktowych, a nie indeksów komórek Excela. Przetestuj współrzędne na próbce pliku, aby uniknąć umieszczenia poza slajdem.
* **Niezgodność formatu pliku** – Zapis skoroszytu jako PPTX przy użyciu `SaveFormat.Pptx` automatycznie konwertuje wszystkie obsługiwane kształty. Próba zapisu jako `Pdf` spowoduje rasteryzację kształtu, czyniąc go nieedytowalnym.

---

## Podsumowanie

Teraz wiesz, jak **skopiować tabelę przestawną do nowego skoroszytu** oraz jak **wyeksportować edytowalny kształt do PowerPointa** przy użyciu Aspose.Cells dla .NET. Pełne, działające przykłady kodu obejmują wszystkie wymagane wywołania API, wyjaśniają, dlaczego każdy krok ma znaczenie, i pokazują oczekiwane rezultaty.

Następnie możesz zgłębić:

* **Praca z wykresami** – kopiowanie wykresów razem z tabelami przestawnymi (`Aspose.Cells copy rows between worksheets`).

## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}