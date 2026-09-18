---
category: general
date: 2026-09-18
description: Utwórz prezentację PowerPoint z Excela przy użyciu Aspose.Cells – kopiuj
  tabele przestawne, eksportuj zakresy i zapisz jako PPTX w kilku linijkach kodu C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: pl
lastmod: 2026-09-18
og_description: Szybko twórz prezentacje PowerPoint z Excela. Dowiedz się, jak kopiować
  tabele przestawne, eksportować zakresy i zapisywać skoroszyt jako plik PPTX przy
  użyciu Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Utwórz PowerPoint z Excela przy użyciu Aspose.Cells – przewodnik krok po
  kroku
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Jak utworzyć PowerPoint z Excela przy użyciu Aspose.Cells
url: /pl/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć PowerPoint z Excela przy użyciu Aspose.Cells

Jeśli potrzebujesz utworzyć PowerPoint z Excela, ten przewodnik pokaże Ci zwięzłe, kompleksowe rozwiązanie. Zobaczysz, jak skopiować tabelę przestawną, wyeksportować wybrany zakres i zapisać wynik jako plik PPTX przy użyciu kilku linii C#.

Generowanie zestawu slajdów bezpośrednio z danych arkusza kalkulacyjnego eliminuje ręczny krok kopiuj‑wklej, który spowalnia przepływy pracy raportowania. Samouczek obejmuje wszystko, czego potrzebujesz, od konfiguracji projektu po ostateczny plik PPTX, i działa z najnowszą wersją Aspose.Cells dla .NET.

## Wymagania wstępne

* **Aspose.Cells for .NET** (wersja 23.12 lub nowsza). Zainstaluj go za pomocą NuGet: `Install-Package Aspose.Cells`.
* Środowisko programistyczne **.NET 6+** (działa Visual Studio 2022 lub VS Code).
* Skoroszyt Excel (`Source.xlsx`) zawierający dane i tabelę przestawną, którą chcesz ponownie użyć.
* Uprawnienia zapisu do folderu wyjściowego.

Nie są wymagane dodatkowe biblioteki zewnętrzne.

## Utwórz PowerPoint z Excela – krok po kroku

Proces składa się z czterech logicznych kroków, które odpowiadają przykładowemu kodowi, który zobaczysz później.

### Krok 1: Załaduj źródłowy skoroszyt i zdefiniuj zakres

Musisz załadować skoroszyt zawierający dane źródłowe i tabelę przestawną. Wybranie precyzyjnego zakresu zapewnia, że zostaną przeniesione tylko potrzebne komórki, co utrzymuje slajd lekki.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Dlaczego to jest ważne:**  
`CreateRange` tworzy obiekt `Range`, który może być kopiowany w całości. Ograniczając zakres do `A1:G20`, unikasz pobierania niepowiązanych komórek, które w przeciwnym razie mogłyby zwiększyć rozmiar pliku PowerPoint.

### Krok 2: Przygotuj docelowy skoroszyt

Aspose.Cells traktuje slajd PowerPoint jako skoroszyt, gdy zapisujesz go w formacie PPTX. Utworzenie nowego skoroszytu zapewnia czyste płótno dla kopiowanego zakresu.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Wskazówka:**  
Jeśli potrzebujesz wielu slajdów, możesz dodać dodatkowe arkusze i później zapisać każdy jako osobny plik PPTX.

### Krok 3: Skopiuj zakres zachowując tabelę przestawną

Metoda `CopyRange` przyjmuje obiekt `PasteOptions`. Ustawienie `CopyPivotTables = true` informuje Aspose.Cells, aby zachował strukturę tabeli przestawnej w całości, a nie tylko wyrenderowane wartości.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Jak to działa:**  
Gdy `CopyPivotTables` jest ustawione na true, docelowy arkusz otrzymuje zarówno dane źródłowe, jak i pamięć podręczną tabeli przestawnej. Oznacza to, że tabela przestawna pozostaje w pełni funkcjonalna i może być odświeżona później, jeśli dane źródłowe ulegną zmianie.

### Krok 4: Zapisz skoroszyt jako plik PowerPoint

Na koniec wyeksportuj skoroszyt do formatu PPTX. Flaga `SaveFormat.Pptx` informuje Aspose.Cells, aby zapisał arkusz jako slajd PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Wynik:**  
`CopyWithPivot.pptx` otwiera się w Microsoft PowerPoint (lub dowolnym kompatybilnym przeglądarce) z jednym slajdem, który wyświetla skopiowany zakres, w tym aktywną tabelę przestawną, z którą można interaktywnie pracować w PowerPoint.

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego i uruchomić od razu.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Oczekiwany wynik:**  
Uruchomienie programu wypisuje „PowerPoint file created successfully.” i tworzy plik o nazwie `CopyWithPivot.pptx`. Otworzenie pliku w PowerPoint pokazuje pojedynczy slajd, na którym skopiowany zakres z Excela pojawia się dokładnie tak, jak w źródłowym arkuszu, z aktywną tabelą przestawną, którą można odświeżyć bezpośrednio w PowerPoint.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co zmienić |
|-----------|----------------|
| **Wiele tabel przestawnych** | Zdefiniuj osobne obiekty `Range` dla każdej tabeli i wywołaj `CopyRange` dla każdej z nich, lub skopiuj cały arkusz, jeśli korzystają z tego samego źródła danych. |
| **Duże zestawy danych** | Zwiększ zakres (np. `"A1:Z5000"`). Rozważ włączenie `PasteOptions.CompressData = true`, aby zmniejszyć rozmiar PPTX. |
| **Różne układy slajdów** | Po zapisaniu jako PPTX otwórz plik w PowerPoint i zastosuj własny układ lub motyw; dane pozostają edytowalne. |
| **Zapisywanie do strumienia** | Użyj `destinationWorkbook.Save(stream, SaveFormat.Pptx)`, gdy musisz zwrócić PPTX przez interfejs API webowy. |
| **Zachowanie formatowania komórek** | Ustaw `PasteOptions.PasteType = PasteType.All`, aby zachować czcionki, kolory i obramowania. |

**Wskazówka pro:**  
Zawsze sprawdzaj, czy folder docelowy istnieje przed wywołaniem `Save`. Jeśli folder nie istnieje, `Save` zgłasza `DirectoryNotFoundException`.

## Podsumowanie

Teraz wiesz, jak utworzyć PowerPoint z Excela, skopiować tabelę przestawną i wyeksportować wynik jako plik PPTX przy użyciu Aspose.Cells. Kroki — ładowanie źródłowego skoroszytu, definiowanie zakresu, kopiowanie z `CopyPivotTables` oraz zapisywanie jako PPTX — obejmują cały przepływ pracy w niezawodny, gotowy do produkcji sposób.

Następnie zapoznaj się z **jak wyeksportować Excel do PPTX** dla wielu arkuszy lub dowiedz się **jak kopiować zakresy między skoroszytami**, gdy musisz połączyć dane z kilku źródeł przed wygenerowaniem zestawu slajdów. Oba tematy opierają się na tym samym interfejsie API i mogą być połączone w celu automatyzacji złożonych pipeline'ów raportowania.

Miłego kodowania i ciesz się przekształcaniem swoich arkuszy kalkulacyjnych w dopracowane prezentacje!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować tabelę przestawną w C# – konwertuj Excel do PPTX, kopiuj zakres i twórz pole tekstowe](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Utwórz nowy skoroszyt – jak skopiować arkusz z tabelą przestawną](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Jak tworzyć i zapisywać pliki Excel przy użyciu Aspose.Cells dla .NET: kompletny przewodnik](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}