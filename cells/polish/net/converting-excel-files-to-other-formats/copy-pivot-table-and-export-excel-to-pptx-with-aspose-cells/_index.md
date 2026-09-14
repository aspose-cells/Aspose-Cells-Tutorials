---
category: general
date: 2026-09-11
description: Skopiuj tabelę przestawną i wyeksportuj Excel do PPTX przy użyciu Aspose.Cells.
  Dowiedz się, jak generować edytowalny plik PPTX i zapisać skoroszyt jako PPTX w
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: pl
lastmod: 2026-09-11
og_description: Skopiuj tabelę przestawną i wyeksportuj Excel do PPTX w C# przy użyciu
  Aspose.Cells. Generuj edytowalny plik PPTX i zapisz skoroszyt jako PPTX w kilku
  linijkach kodu.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Kopiowanie tabeli przestawnej i eksportowanie Excela do PPTX – kompletny
  przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Kopiowanie tabeli przestawnej i eksportowanie Excela do PPTX przy użyciu Aspose.Cells
url: /pl/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skopiuj tabelę przestawną i wyeksportuj Excel do PPTX przy użyciu Aspose.Cells

Jeśli potrzebujesz skopiować tabelę przestawną z jednego arkusza do drugiego, a następnie wyeksportować plik Excel do prezentacji PowerPoint, ten przewodnik pokaże Ci, jak to zrobić. Korzystając z Aspose.Cells możesz wygenerować edytowalny plik PPTX i zapisać skoroszyt jako PPTX w zaledwie kilku linijkach kodu C#.

Poradnik obejmuje każdy krok niezbędny do przeniesienia tabeli przestawnej, zachowania jej funkcjonalności oraz stworzenia pliku PPTX, w którym wykres i kształty pozostają edytowalne. Nie są potrzebne żadne zewnętrzne narzędzia — jedynie biblioteka Aspose.Cells i środowisko programistyczne .NET.

## Co osiągniesz

* **Copy pivot table** z arkusza źródłowego do arkusza docelowego, zachowując wszystkie połączenia danych.  
* **Export Excel to PPTX** tak, aby otrzymany slajd można było edytować w PowerPoint.  
* **Generate editable PPTX** w którym wykresy, tabele i kształty nie są spłaszczane do obrazów.  
* **Save workbook as PPTX** przy użyciu tego samego wywołania API Aspose.Cells.  

### Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+).  
* Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`).  
* Podstawowa znajomość aplikacji konsolowych C#.  

> **Wskazówka:** Zainstaluj pakiet NuGet za pomocą CLI, aby mieć pewność, że masz najnowszą wersję:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Jak skopiować tabelę przestawną między arkuszami

Pierwszą operacją jest przeniesienie tabeli przestawnej przy zachowaniu jej definicji. Aspose.Cells udostępnia metodę `CopyRange` z obiektem `CopyOptions`, który zawiera flagę `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Dlaczego to działa:**  
`CopyRange` kopiuje dane komórek, formatowanie oraz, gdy `CopyPivotTable` jest ustawione na true, pamięć podręczną i metadane tabeli przestawnej. Zakres docelowy zaczyna się od komórki `A1` (wiersz 0, kolumna 0), ale możesz zmienić offsety, aby umieścić tabelę przestawną w innym miejscu.

**Typowy przypadek brzegowy:** Jeśli arkusz docelowy już zawiera tabelę przestawną o tej samej nazwie, Aspose.Cells automatycznie zmieni nazwę wprowadzanej tabeli, zapobiegając konfliktowi nazw.

## Eksportuj Excel do PPTX i generuj edytowalny PPTX

Po umieszczeniu tabeli przestawnej możesz wyeksportować cały skoroszyt do pliku PPTX. Klasa `ImageOrPrintOptions` pozwala określić `ExportImageFormat = ImageFormat.Pptx`, co instruuje Aspose.Cells, aby traktował wynik jako prezentację PowerPoint, a nie jako obraz rastrowy.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Dlaczego to działa:**  
Gdy `ExportImageFormat` jest ustawione na `Pptx`, Aspose.Cells przetwarza każdy arkusz na slajd. Kształty, wykresy i tabele przestawne są zapisywane jako natywne obiekty PowerPoint, dzięki czemu możesz dwukrotnie kliknąć je w PowerPoint i edytować leżące pod spodem dane.

**Wskazówka dla dużych skoroszytów:** Jeśli potrzebujesz tylko podzbioru arkuszy, wywołaj `workbook.Worksheets.RemoveAt(index)` dla arkuszy, które nie mają być eksportowane, przed wywołaniem `Save`. To zmniejszy rozmiar pliku PPTX.

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który łączy poprzednie kroki. Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką na swoim komputerze.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Gdy otworzysz `output.pptx` w Microsoft PowerPoint, zobaczysz slajd zawierający skopiowaną tabelę przestawną jako edytowalny wykres. Dwukrotne kliknięcie wykresu otwiera edytor wykresów PowerPoint, umożliwiając modyfikację serii, osi i etykiet danych bez powrotu do Excela.

## Radzenie sobie z typowymi problemami

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| Tabela przestawna pojawia się jako statyczny obraz | pominięto flagę `CopyPivotTable` lub `ExportImageFormat` ustawiono na `Png` | Upewnij się, że `CopyPivotTable = true` oraz `ExportImageFormat = ImageFormat.Pptx`. |
| Arkusz docelowy pokazuje puste komórki | zakres źródłowy nie obejmuje całego obszaru tabeli przestawnej | Rozszerz zakres (np. `"A1:H30"`), aby uwzględnić wszystkie pola przestawne. |
| Wyeksportowany PPTX jest bardzo duży | Dołączono niepotrzebne arkusze | Usuń niechciane arkusze przed wywołaniem `Save`. |
| PowerPoint nie może edytować wykresu | używana starsza wersja Aspose.Cells, która nie obsługuje PPTX | Zaktualizuj do najnowszej wersji Aspose.Cells (sprawdź notatki wydania). |

## Kolejne kroki i powiązane tematy

* **Export Excel sheet to PPTX with custom slide layouts** – zapoznaj się z `WorksheetToPdfConverter`, aby uzyskać większą kontrolę nad wyglądem slajdów.  
* **Export Excel to PDF** – zamień `ImageFormat.Pptx` na `ImageFormat.Pdf`, aby wygenerować plik PDF.  
* **Programmatically modify PPTX after export** – użyj biblioteki `Aspose.Slides`, aby dodać animacje lub notatki prelegenta.  

Opanowując **copy pivot table**, **export excel to pptx** i **generate editable pptx**, możesz zbudować kompleksowe pipeline’y raportowe, które przenoszą dane z arkuszy kalkulacyjnych bezpośrednio do prezentacji, nie tracąc możliwości edycji.

---

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować tabelę przestawną w C# – konwertuj Excel do PPTX, kopiuj zakres i twórz pola tekstowe](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Utwórz nowy skoroszyt Excel – kopiuj i duplikuj tabelę przestawną](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Utwórz tabelę przestawną w Excelu przy użyciu Aspose.Cells dla .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}