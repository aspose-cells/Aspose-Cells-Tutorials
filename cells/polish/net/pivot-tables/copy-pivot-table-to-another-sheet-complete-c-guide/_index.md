---
category: general
date: 2026-06-27
description: Skopiuj tabelę przestawną do innego arkusza w C# przy użyciu Aspose.Cells.
  Dowiedz się krok po kroku, jak zachować dane i formatowanie tabeli przestawnej.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: pl
og_description: Skopiuj tabelę przestawną do innego arkusza w C# przy użyciu Aspose.Cells.
  Ten samouczek dokładnie pokazuje, jak zduplikować tabelę przestawną, zachowując
  jej formatowanie.
og_title: Skopiuj tabelę przestawną do innego arkusza – Kompletny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Kopiowanie tabeli przestawnej do innego arkusza – kompletny przewodnik C#
url: /pl/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie tabeli przestawnej do innego arkusza – Kompletny przewodnik C#

Czy kiedykolwiek musiałeś **skopiować tabelę przestawną do innego arkusza**, obawiając się utraty segmentatorów, pól obliczeniowych lub formatowania? Nie jesteś sam. Wielu programistów napotyka ten problem przy automatyzacji raportów Excel, a frustracja jest realna. W tym przewodniku przeprowadzimy Cię przez czyste, kompleksowe rozwiązanie, które **zachowuje tabelę przestawną** dokładnie tak, jak wygląda.

Użyjemy **Aspose.Cells for .NET**, potężnej biblioteki umożliwiającej manipulację plikami Excel bez otwierania samego Excela. Po zakończeniu tego tutorialu będziesz mieć gotowy do uruchomienia fragment C#, który kopiuje tabelę przestawną z jednego arkusza do drugiego, zachowując wszystkie połączenia danych.

## Co obejmuje ten tutorial

- Konfiguracja projektu .NET i dodanie pakietu NuGet Aspose.Cells.  
- Ładowanie istniejącego skoroszytu, który już zawiera tabelę przestawną.  
- Definiowanie zarówno zakresu źródłowego (oryginalna tabela), jak i zakresu docelowego w innym arkuszu.  
- Użycie `CopyOptions`, aby **zachować tabelę przestawną** podczas kopiowania.  
- Zapis wyniku i weryfikacja, że tabela działa w nowej lokalizacji.  

Bez zewnętrznych narzędzi, bez ręcznego kopiowania‑wklejania i bez ukrytej magii — po prostu przejrzysty kod, który możesz wkleić do dowolnej aplikacji konsolowej C# lub usługi.

> **Dlaczego warto:** Automatyzacja duplikacji tabel przestawnych oszczędza godziny ręcznej pracy, szczególnie w nocnych potokach raportowania, gdzie dziesiątki skoroszytów potrzebują identycznych struktur tabel przestawnych w wielu arkuszach.

---

## Krok 1: Konfiguracja projektu i dodanie Aspose.Cells

Na początek. Jeśli jeszcze tego nie zrobiłeś, utwórz nowy projekt konsolowy .NET:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Teraz dodaj pakiet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Użyj najnowszej stabilnej wersji (stan na czerwiec 2026 v23.12). Zawiera poprawki błędów związane z obsługą `CopyPivotTable`.

## Krok 2: Ładowanie skoroszytu i dostęp do arkuszy

Otwórz skoroszyt, który zawiera źródłową tabelę przestawną. W większości rzeczywistych scenariuszy plik znajduje się na udostępnionym dysku, ale w tym demo przyjmujemy, że jest w lokalnym folderze o nazwie `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Tutaj tworzymy nowy arkusz o nazwie **CopyDestination**, w którym zostanie umieszczona tabela. Jeśli już masz docelowy arkusz, po prostu pobierz go po indeksie lub nazwie.

## Krok 3: Definiowanie zakresów źródłowego i docelowego

Tabela przestawna znajduje się wewnątrz prostokątnego bloku komórek. Musisz powiedzieć Aspose.Cells, który blok skopiować. W tym przykładzie tabela zajmuje wiersze 0‑20 i kolumny 0‑10 (indeksowanie zerowe).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Zauważ, że obliczamy końcowy wiersz i kolumnę dynamicznie. Dzięki temu, nawet jeśli później zmienisz rozmiar zakresu źródłowego, docelowy automatycznie się dostosuje.

## Krok 4: Kopiowanie z zachowaniem tabeli przestawnej

Teraz następuje magia. Przekazując obiekt `CopyOptions` z `CopyPivotTable = true`, Aspose.Cells wie, że ma zachować definicję tabeli przestawnej.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

W tle Aspose.Cells odtwarza pamięć podręczną tabeli przestawnej, odświeża odwołanie do źródła danych i ponownie stosuje formatowanie. To jest **duplikacja tabeli przestawnej w Excelu**, której szukałeś.

## Krok 5: Zapis i weryfikacja wyniku

Na koniec zapisujemy skoroszyt na dysku. Możesz pozostawić oryginalny plik nietknięty, zapisując pod nową nazwą.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Otwórz powstały plik `copy-pivot.xlsx`, a zobaczysz tabelę przestawną idealnie odtworzoną w arkuszu **CopyDestination**, wraz z segmentatorami, polami obliczeniowymi i formatowaniem. Źródło danych nadal wskazuje na oryginalną tabelę, więc odświeżanie działa dokładnie tak samo.

> **Co zrobić, gdy źródłowa tabela przestawna obejmuje zakres dynamiczny?**  
> Użyj `Worksheet.PivotTables[0].CacheDefinition.SourceData`, aby pobrać rzeczywiste granice, a następnie zbuduj `sourceRange` na podstawie tych informacji. To obsługuje przypadki, w których wiersze lub kolumny mogą się z czasem rozszerzać.

## Bonus: Zachowanie formatowania tabeli przy kopiowaniu

Czasami domyślne kopiowanie traci formatowanie warunkowe lub niestandardowe formaty liczb. Aby temu zapobiec, rozbuduj `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Włączenie `CopyFormatting` zapewnia spełnienie wymogu **zachowania formatowania tabeli przestawnej**, dając Ci idealną kopię piksel po pikselu.

## Oczekiwany wynik

Po uruchomieniu programu konsola zakończy się cicho (chyba że dodasz logowanie). Otwierając `copy-pivot.xlsx`, powinieneś zobaczyć:

- Arkusz 1: Oryginalne dane i tabela przestawna niezmienione.  
- **CopyDestination**: Dokładna replika tabeli, zaczynająca się od wiersza 31 (ponieważ w interfejsie Excela wiersze są numerowane od 1).  
- Wszystkie segmentatory i filtry działają; kliknięcie „Refresh” aktualizuje oba przestawne jednocześnie.

---

## Zakończenie

Właśnie pokazaliśmy, jak **skopiować tabelę przestawną do innego arkusza** przy użyciu Aspose.Cells w C#. Kroki — konfiguracja projektu, ładowanie skoroszytu, definiowanie zakresów, kopiowanie z `CopyPivotTable = true` i zapis — tworzą niezawodny wzorzec, który możesz ponownie wykorzystać w dowolnym potoku automatyzacji.  

Jeśli chcesz iść dalej, rozważ:

- **Duplikację tabel przestawnych** w wielu skoroszytach (pętla po plikach).  
- Użycie opcji **Aspose.Cells copy range with pivot** do przenoszenia tabel między różnymi skoroszytami.  
- Automatyzację odświeżania za pomocą `PivotTable.RefreshData()` po skopiowaniu.

Śmiało eksperymentuj z różnymi zakresami źródłowymi lub połącz tę technikę z generowaniem wykresów, aby uzyskać w pełni zautomatyzowane pulpity raportowe. Masz pytania? zostaw komentarz i powodzenia w kodowaniu!

---

![Zrzut ekranu pokazujący skopiowaną tabelę przestawną w nowym arkuszu](copy-pivot-screenshot.png "przykład kopiowania tabeli przestawnej do innego arkusza")


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak zmienić źródło danych tabeli przestawnej przy użyciu Aspose.Cells for .NET | Przewodnik analizy danych](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Mistrzowskie formatowanie tabel przestawnych w .NET przy użyciu Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Dostęp do zewnętrznych źródeł danych tabeli przestawnej w .NET przy użyciu Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}