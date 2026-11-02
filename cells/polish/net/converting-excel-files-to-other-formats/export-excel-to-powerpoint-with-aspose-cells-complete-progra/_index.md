---
category: general
date: 2026-08-14
description: Eksportuj Excel do PowerPoint przy użyciu Aspose.Cells i dowiedz się,
  jak obliczać formuły Excela w kodzie. Przykład krok po kroku w C# z pełnym kodem
  źródłowym.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: pl
lastmod: 2026-08-14
og_description: Eksportuj Excel do PowerPoint przy użyciu Aspose.Cells i obliczaj
  formuły Excela w kodzie. Skorzystaj z tego kompletnego przewodnika, aby generować
  edytowalne pliki PPTX ze skoroszytów.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Eksportowanie Excela do PowerPointa z Aspose.Cells – pełny samouczek C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Eksportowanie Excela do PowerPointa przy użyciu Aspose.Cells – kompletny przewodnik
  programistyczny
url: /pl/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportuj Excel do PowerPoint przy użyciu Aspose.Cells – kompletny przewodnik programistyczny

Jeśli potrzebujesz **eksportować Excel do PowerPoint** programowo, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells dla .NET. Dowiesz się także, jak **obliczać formuły Excel w kodzie**, kopiować tabele przestawne bez utraty definicji oraz korzystać z nowej funkcji Office‑365 EXPAND dla dynamicznych tablic.

W kolejnych sekcjach przeprowadzimy Cię przez rzeczywisty przykład w C#, wyjaśnimy, dlaczego każda linia ma znaczenie, oraz omówimy typowe pułapki, abyś mógł dostosować rozwiązanie do własnych projektów.

## Co obejmuje ten tutorial

* Ładowanie istniejącego skoroszytu (`input.xlsx`)  
* Kopiowanie zakresu zawierającego tabelę przestawną przy zachowaniu jej definicji  
* Eksportowanie skoroszytu do pliku PowerPoint (`.pptx`) z edytowalnymi polami tekstowymi i kształtami  
* Eksportowanie zakresu komórek jako ciągi znaków przy użyciu własnej logiki  
* Obliczanie formuł Excel w kodzie, w tym funkcji Office‑365 EXPAND  
* Zapisywanie ostatecznego skoroszytu ze wszystkimi zastosowanymi zmianami  

**Prerequisites**  
* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7.2+)  
* Aspose.Cells dla .NET v25.11 lub nowszy (opcja `CopyPivotTable` została wprowadzona w wersji v25.11)  
* Podstawowa znajomość C# oraz koncepcji Excela, takich jak zakresy, tabele przestawne i formuły  

> **Pro tip:** Zainstaluj Aspose.Cells przez NuGet (`Install-Package Aspose.Cells`), aby Twój projekt był aktualny z najnowszymi funkcjami.

## Eksport Excel do PowerPoint przy użyciu Aspose.Cells

Pierwszym głównym zadaniem jest konwersja skoroszytu do prezentacji PowerPoint przy zachowaniu wszystkich elementów wizualnych jako edytowalne. Jest to niezbędne, gdy chcesz automatycznie generować zestawy slajdów z raportów finansowych lub pulpitów nawigacyjnych.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Dlaczego to działa

* **`Workbook`** ładuje cały plik Excel do pamięci, dając pełny dostęp do API.  
* **`CopyRange`** z `CopyPivotTable = true` zapewnia, że źródło danych, pamięć podręczna i układ tabeli przestawnej są dokładnie powielone — czego starsze wersje Aspose.Cells nie mogły zrobić.  
* Dodanie nowego arkusza (`Copy`) pozwala zachować oryginalny arkusz nietknięty, co jest przydatne w ścieżkach audytu.

## Eksportuj skoroszyt do PowerPoint z edytowalnymi obiektami

Teraz przekształcamy skoroszyt w plik PowerPoint. Włączając `ExportEditableObjects`, każdy wykres, kształt lub pole tekstowe staje się natywnym obiektem PowerPoint, który użytkownicy mogą edytować bezpośrednio po eksporcie.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Wyjaśnienie

* **`WorkbookDesigner`** to wysokopoziomowy pomocnik, który przygotowuje skoroszyt do eksportu, obsługując Smart Markers, nazwane zakresy i korekty układu.  
* Ustawienie `ExportEditableObjects = true` instruuje Aspose.Cells, aby przetłumaczył rysunki Excel na kształty PowerPoint, zamiast spłaszczać je do obrazów. To daje **w pełni edytowalną** prezentację.  

> **Edge case:** Jeśli Twój skoroszyt zawiera złożone wykresy zbudowane na podstawie zewnętrznych połączeń danych, upewnij się, że te połączenia są rozwiązane przed wywołaniem `ExportToPptx`, w przeciwnym razie wykres może być pusty.

## Eksportuj zakres jako ciągi znaków przy użyciu własnej logiki

Czasami potrzebujesz surowych wartości tekstowych do dalszego przetwarzania (np. podania ich parserowi CSV). Klasa `ExportTableOptions` pozwala kontrolować, jak każda komórka jest konwertowana.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Dlaczego możesz tego używać

* **Jednolity typ danych:** Eksportowanie jako ciągi znaków unika błędów niezgodności typów, gdy odbiorca oczekuje tekstu.  
* **Niestandardowe formatowanie:** Zastąp `value.ToString()` dowolnym własnym formatowaniem (np. `value.ToString("yyyy-MM-dd")` dla dat).  

## Obliczaj formuły Excel w kodzie

Częstym wymaganiem jest **obliczanie formuł Excel w kodzie** bez otwierania Excela. Aspose.Cells udostępnia wbudowany silnik obliczeniowy, który działa offline i obsługuje najnowsze funkcje Office‑365, w tym `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Jak działa silnik obliczeniowy

* Właściwość `Formula` przechowuje wyrażenie dokładnie tak, jak wpisujesz je w Excelu.  
* `CalculateFormula()` uruchamia pełne przeliczenie skoroszytu, uwzględniając zależności między komórkami.  
* Funkcja `EXPAND` (dostępna w Excel 365) zwraca zakres rozlewu oparty na komórce źródłowej (`B1`) oraz określonych wierszach (`5`) i kolumnach (`3`).  

> **Tip:** Jeśli potrzebujesz obliczyć tylko podzbiór skoroszytu, użyj `Worksheet.CalculateFormula()`, aby ograniczyć zakres i poprawić wydajność.

## Zapisz skoroszyt ze wszystkimi zastosowanymi zmianami

Na koniec zapisz zmodyfikowany skoroszyt z powrotem na dysk. Możesz zapisać w dowolnym obsługiwanym formacie (`.xlsx`, `.xls`, `.csv` itp.) zmieniając rozszerzenie pliku.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Co należy zweryfikować

* Otwórz `result.xlsx` w Excelu, aby potwierdzić kopiowanie tabeli przestawnej, wynik formuły `EXPAND` oraz wszelkie niestandardowo wyeksportowane ciągi.  
* Otwórz `output.pptx` w PowerPoint; powinieneś zobaczyć slajd odzwierciedlający układ Excela, a wszystkie wykresy/pola tekstowe powinny być edytowalne.

## Częste pytania i rozwiązywanie problemów

| Pytanie | Odpowiedź |
|----------|-----------|
| **Czy potrzebuję licencji, aby używać Aspose.Cells?** | Tak. Wersja próbna działa do oceny, ale pełna licencja usuwa znaki wodne oceny i odblokowuje funkcję `CopyPivotTable`. |
| **Co zrobić, gdy wyeksportowany PPTX pokazuje puste kształty?** | Sprawdź, czy obiekty rysunkowe w skoroszycie nie są ukryte (`Visible = true`) oraz czy wszystkie zewnętrzne linki do obrazów są osadzone przed eksportem. |
| **Czy mogę wyeksportować wiele arkuszy do osobnych slajdów PPTX?** | Użyj `WorkbookDesigner.ExportToPptx` w pętli, określając różne `ExportOptions` dla każdego arkusza, lub połącz je w jedną prezentację, dodając slajdy ręcznie przy pomocy Aspose.Slides. |
| **Czy `CalculateFormula` jest bezpieczne wątkowo?** | Nie. Przeprowadzaj obliczenia w jednym wątku lub klonuj skoroszyt dla każdego wątku, aby uniknąć warunków wyścigu. |

## Podsumowanie

Masz teraz **kompletne, kompleksowe rozwiązanie do eksportu Excel do PowerPoint** przy użyciu Aspose.Cells i rozumiesz, jak **obliczać formuły Excel w kodzie** — w tym nowoczesną funkcję `EXPAND`. Tutorial obejmował ładowanie skoroszytu, kopiowanie tabel przestawnych, eksport do edytowalnego PowerPoint, niestandardowy eksport ciągów, obliczanie formuł oraz ostateczne zapisywanie.

Z tego miejsca możesz:

* Rozszerz eksport, aby obejmował wiele slajdów na arkusz (drugorzędne słowo kluczowe: *calculate Excel formulas in code* może być ponownie użyte przy generowaniu danych wykresu).  
* Zintegruj Aspose.Slides, aby dodać animacje lub układy slajdów głównych.  
* Zastąp prosty delegat `CustomExport` formatowaniem zależnym od lokalizacji dla projektów międzynarodowych.  

Śmiało eksperymentuj z różnymi zakresami, odkrywaj inne funkcje Office‑365 (np. `FILTER`, `SORT`) i łącz ten przepływ pracy z automatycznym dostarczaniem e‑maili, aby uzyskać w pełni zautomatyzowane pipeline’y raportowania.

---


## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Automatyzuj eksport danych Excel przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Jak wyeksportować wykresy Excel do PDF przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Eksportuj komórki Excel do obrazu przy użyciu Aspose.Cells .NET: Przewodnik krok po kroku](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}