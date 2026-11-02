---
category: general
date: 2026-09-27
description: Dowiedz się, jak skopiować tabelę przestawną w C# przy użyciu Aspose.Cells.
  Zawiera kopiowanie wierszy z formatowaniem, kopiowanie tabeli przestawnej do innego
  arkusza oraz eksport tabeli przestawnej do nowego skoroszytu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: pl
lastmod: 2026-09-27
og_description: Jak skopiować tabelę przestawną w C# przy użyciu Aspose.Cells. Postępuj
  zgodnie z przewodnikiem krok po kroku, aby skopiować wiersze z formatowaniem, przenieść
  tabelę przestawną na inny arkusz i wyeksportować ją do nowego skoroszytu.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Jak skopiować tabelę przestawną w C# – pełny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Jak skopiować tabelę przestawną w C# przy użyciu Aspose.Cells
url: /pl/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w C# z Aspose.Cells

Jeśli potrzebujesz **skopiować tabelę przestawną** z jednego arkusza do drugiego, poznanie **sposobu kopiowania tabeli przestawnej** w C# z Aspose.Cells może zaoszczędzić Ci godziny ręcznej pracy. Podejście pozwala także **skopiować wiersze z formatowaniem**, zachować niezmieniony cache przestawny oraz nawet **wyeksportować tabelę przestawną do nowego skoroszytu**, gdy potrzebny jest oddzielny plik.

Ten tutorial przeprowadzi Cię przez cały proces:

* utworzenie skoroszytu,  
* skopiowanie zakresu tabeli przestawnej z zachowaniem formatowania,  
* umieszczenie skopiowanych danych w nowym arkuszu oraz  
* zapis wyniku jako osobnego pliku.

Zobaczysz, dlaczego wbudowana metoda `CopyRows` jest najpewniejszym sposobem na **skopiowanie tabeli przestawnej do innego arkusza**, oraz otrzymasz wskazówki dotyczące obsługi przypadków brzegowych, takich jak ukryte wiersze czy zewnętrzne źródła danych.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

| Wymaganie | Dlaczego jest ważne |
|-----------|----------------------|
| .NET 6.0 lub nowszy | Aspose.Cells obsługuje .NET 6+ i zapewnia najlepszą wydajność. |
| Visual Studio 2022 (lub dowolne IDE C#) | Potrzebujesz edytora, który potrafi przywrócić pakiety NuGet. |
| Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`) | Biblioteka dostarcza API `CopyRows` używane w przykładzie. |
| Plik Excel źródłowy (`source.xlsx`) zawierający tabelę przestawną w zakresie `A1:G20` | Kod kopiuje właśnie ten zakres; dostosuj go, jeśli Twoja tabela przestawna jest większa. |

Zainstaluj bibliotekę przy użyciu NuGet CLI lub Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Załaduj skoroszyt zawierający tabelę przestawną

Pierwsza linia tworzy obiekt `Workbook`, który reprezentuje cały plik Excel. Jednorazowe załadowanie pliku daje dostęp do odczytu i zapisu we wszystkich arkuszach.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Dlaczego ten krok jest ważny** – Bez załadowania skoroszytu żadne z kolejnych wywołań `CopyRows` nie może odwoływać się do danych źródłowych ani cache’u przestawnego.

## Krok 2: Przygotuj arkusze źródłowy i docelowy

Potrzebujesz arkusza docelowego, w którym będzie znajdować się skopiowana tabela przestawna. Poniższy kod pobiera pierwszy arkusz (gdzie znajduje się oryginalna tabela przestawna) i dodaje nowy arkusz o nazwie **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** Jeśli arkusz docelowy już istnieje, najpierw wywołaj `Worksheets.RemoveAt(index)`, aby uniknąć duplikatów nazw.

## Krok 3: Zdefiniuj obszar komórek obejmujący tabelę przestawną

Obiekt `CellArea` opisuje komórki w lewym‑górnym i prawym‑dolnym rogu zakresu, który chcesz przenieść. W tym przykładzie tabela przestawna zajmuje `A1:G20`. Dostosuj współrzędne dla większych tabel.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Krok 4: Skopiuj wiersze z formatowaniem i zachowaj cache przestawny

Metoda `CopyRows` kopiuje **wiersze** z arkusza źródłowego do arkusza docelowego. Przekazując `CopyOptions.CopyAll`, zapewniasz, że wartości, formatowanie, wykresy i osadzone obiekty — wszystkie elementy tabeli przestawnej — zostaną przeniesione.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Dlaczego `CopyRows` działa lepiej niż `Copy` dla tabel przestawnych

* `CopyRows` respektuje wewnętrzny cache przestawny, więc skopiowana tabela przestawna pozostaje w pełni funkcjonalna.  
* Zachowuje **kopiowanie wierszy z formatowaniem** dokładnie tak, jak wyglądają w oryginalnym arkuszu.  
* W przeciwieństwie do prostego `Copy` zakresu, przenosi także ukryte wiersze i powiązane slicery.

## Krok 5: Zapisz skoroszyt ze skopiowaną tabelą przestawną

Na koniec zapisz zmodyfikowany skoroszyt na dysku. Nowy plik zawiera oryginalny arkusz oraz arkusz **Copy**, w którym znajduje się w pełni działająca kopia pierwotnej tabeli przestawnej.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Oczekiwany rezultat

Po otwarciu `pivot_copied.xlsx`:

* Arkusz **Sheet1** nadal zawiera oryginalne dane i tabelę przestawną.  
* Arkusz **Copy** pokazuje identyczną tabelę przestawną z tym samym układem, filtrami i formatowaniem.  
* Wszystkie formuły i połączenia danych pozostają nienaruszone, ponieważ cache przestawny został skopiowany razem z wierszami.

## Jak skopiować tabelę przestawną do innego arkusza w tym samym skoroszycie

Jeśli potrzebujesz tabeli przestawnej w innym istniejącym arkuszu (np. „Report”), zamień krok tworzenia docelowego arkusza na odwołanie do wybranego arkusza:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Ten fragment pokazuje **kopiowanie tabeli przestawnej do innego arkusza** bez tworzenia nowego arkusza.

## Eksport tabeli przestawnej do nowego skoroszytu

Czasami chcesz mieć tabelę przestawną w całkowicie oddzielnym pliku. Po operacji kopiowania możesz usunąć wszystkie arkusze oprócz tego, który zawiera skopiowaną tabelę przestawną, a następnie zapisać:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Teraz `pivot_only.xlsx` zawiera pojedynczy arkusz z duplikowaną tabelą przestawną, spełniając wymaganie **eksportu tabeli przestawnej do nowego skoroszytu**.

## Jak skopiować wiersze Excela bez utraty formatowania

Ta sama metoda `CopyRows` działa dla dowolnego zakresu, nie tylko tabel przestawnych. Jeśli musisz **skopiować wiersze Excela**, które zawierają formatowanie warunkowe, walidację danych lub scalone komórki, użyj tej samej metody:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Ponieważ `CopyOptions.CopyAll` przenosi wszystko, wiersze docelowe wyglądają dokładnie tak jak wiersze źródłowe.

## Typowe pułapki i jak ich unikać

| Pułapka | Objaw | Rozwiązanie |
|---------|-------|--------------|
| Zakres źródłowy nie obejmuje całej tabeli przestawnej | Skopiowana tabela przestawna jest obcięta. | Upewnij się, że `CellArea` obejmuje wszystkie wiersze/kolumny tabeli przestawnej. |
| Arkusz docelowy już zawiera dane | Nadpisane wiersze powodują utratę danych. | Wybierz pusty arkusz lub rozpocznij kopiowanie od wyższego indeksu wiersza. |
| Tabela przestawna korzysta z zewnętrznego źródła danych | Kopia traci połączenie. | Po skopiowaniu wywołaj `pivotTable.RefreshData()`, aby przywrócić połączenie. |
| Ukryte wiersze są pomijane | Niektóre wiersze znikają w kopii. | `CopyRows` automatycznie kopiuje ukryte wiersze; upewnij się, że nie używasz `CopyOptions.CopyValuesOnly`. |

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się samodzielny program, który możesz wkleić do nowego projektu konsolowego. Demonstruje każdy krok omówiony powyżej.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Uruchomienie programu** tworzy `pivot_copied.xlsx` z duplikatem oryginalnej tabeli przestawnej na nowym arkuszu o nazwie **Copy**.

## Podsumowanie

Teraz wiesz **jak skopiować tabelę przestawną** w C# przy użyciu


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}