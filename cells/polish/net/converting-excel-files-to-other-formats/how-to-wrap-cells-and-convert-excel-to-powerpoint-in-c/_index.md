---
category: general
date: 2026-09-18
description: Jak zawijać komórki w skoroszycie Excel i zapisać go jako plik PowerPoint.
  Dowiedz się, jak używać WRAPCOLS, tworzyć arkusz skoroszytu i eksportować do PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: pl
lastmod: 2026-09-18
og_description: Jak zawijać komórki w Excelu i eksportować skoroszyt jako edytowalny
  plik PowerPoint przy użyciu C#. Postępuj zgodnie z przewodnikiem krok po kroku,
  aby opanować WRAPCOLS i tworzenie arkuszy skoroszytu.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: Jak zawijać komórki i konwertować Excel na PowerPoint w C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Jak zawijać komórki i konwertować Excel na PowerPoint w C#
url: /pl/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zawijać komórki i konwertować Excel do PowerPoint w C#

Jeśli potrzebujesz **how to wrap cells** w arkuszu Excel i następnie przekształcić ten arkusz w prezentację PowerPoint, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Po przeczytaniu pierwszych dwóch zdań dokładnie będziesz wiedział, które wywołania API wykonują zawijanie i która metoda zapisuje plik jako PPTX.

Użyjemy Aspose.Cells for .NET, biblioteki umożliwiającej manipulację skoroszytami Excel bez zainstalowanego Microsoft Office. Poradnik obejmuje **convert Excel to PowerPoint**, demonstruje **how to use WRAPCOLS** oraz wyjaśnia najlepsze praktyki **create workbook worksheet**. Nie są wymagane żadne zewnętrzne narzędzia — wystarczy środowisko programistyczne .NET.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
- Pakiet NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Podstawowa znajomość C# oraz koncepcji arkuszy
- IDE, takie jak Visual Studio lub VS Code

> **Pro tip:** Używaj darmowej licencji ewaluacyjnej Aspose.Cells podczas eksperymentów; zamień ją na pełną licencję przed wdrożeniem.

## Krok 1: Utwórz skoroszyt i dodaj arkusz

Pierwszą rzeczą, którą musisz **create workbook worksheet**, jest utworzenie obiektu `Workbook`. Domyślnie Aspose.Cells tworzy jeden arkusz (indeks 0), którego użyjemy w demonstracji.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Dlaczego to ważne:** Inicjalizacja skoroszytu daje czyste płótno. Domyślny arkusz jest już częścią kolekcji `Worksheets`, więc nie musisz wywoływać `Add()`, chyba że potrzebujesz dodatkowych arkuszy.

## Krok 2: Wypełnij zakres źródłowy (A2:A10)

Zanim będziemy mogli **how to wrap cells**, potrzebujemy danych do zawinięcia. Ten krok wypełnia komórki od A2 do A10 przykładowym tekstem.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Przypadek brzegowy:** Jeśli zakres źródłowy jest pusty, `WRAPCOLS` zwraca `#VALUE!`. Zawsze upewnij się, że zakres zawiera przynajmniej jedną niepustą komórkę.

## Krok 3: Zastosuj formułę WRAPCOLS

Teraz odpowiadamy na podstawowe pytanie **how to use WRAPCOLS**. Formuła przyjmuje pionowy zakres i rozkłada go na określoną liczbę kolumn. Wpisujemy formułę do komórki `A1`; wynikowa tablica automatycznie rozleje się na sąsiednie komórki.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**Co się dzieje w tle:** `WRAPCOLS` ocenia zakres źródłowy, dzieli elementy równo (lub tak równomiernie, jak to możliwe) pomiędzy docelowe kolumny i zapisuje wartości w prostokątnym bloku. Rozmiar bloku jest dynamiczny, więc nie musisz wstępnie definiować zakresu docelowego.

## Krok 4: Zapisz skoroszyt jako edytowalny plik PowerPoint

Na koniec zajmiemy się **convert Excel to PowerPoint** oraz **save Excel as PowerPoint**. Aspose.Cells może wyeksportować arkusz bezpośrednio do PPTX, zachowując układ jako edytowalny kształt.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Dlaczego PPTX?** Wygenerowany PowerPoint zawiera jedną slajd z zawiniętymi komórkami wyświetlonymi jako tabela. Możesz otworzyć plik w Microsoft PowerPoint, edytować tekst, zmieniać style lub dodawać dodatkowe slajdy — wszystko pozostaje w pełni edytowalne.

### Oczekiwany wynik

- **Strona Excel:** Komórka `A1` pokazuje 3‑kolumnową tablicę oryginalnych długich ciągów, przy czym każda kolumna zawiera mniej‑więcej taką samą liczbę wierszy.
- **Strona PowerPoint:** Otwierając `ChartEditable.pptx` wyświetla się slajd z tabelą odzwierciedlającą zawiniowany układ. Tabelę można zaznaczyć, zmienić jej rozmiar lub edytować tak jak każdy natywny obiekt PowerPoint.

## Typowe warianty i na co zwrócić uwagę

| Scenariusz | Dostosowanie |
|------------|--------------|
| **Zawijaj do większej liczby kolumn** | Zmień drugi argument funkcji `WRAPCOLS`, np. `=WRAPCOLS(A2:A10,5)`. |
| **Zawijaj inny zakres** | Zaktualizuj odwołanie w formule, np. `=WRAPCOLS(B2:B15,2)`. |
| **Eksportuj tylko część arkusza** | Użyj `Worksheet.ExportDataTable`, aby wyodrębnić `DataTable`, a następnie API `Presentation` do tworzenia niestandardowego PPTX. |
| **Duże arkusze ( > 10 000 wierszy )** | Rozważ podzielenie eksportu na wiele slajdów, aby uniknąć wąskich gardeł wydajności. |

> **Uwaga:** Domyślny eksport PPTX renderuje arkusz jako pojedynczy obraz, gdy skoroszyt zawiera wykresy. Użycie `WRAPCOLS` zapewnia, że dane pozostają w formie tabeli, którą można edytować.

## Pełny kod źródłowy do szybkiego kopiowania

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

Zapisz plik jako `Program.cs`, przywróć pakiet NuGet i uruchom:

```bash
dotnet run
```

Powinieneś zobaczyć komunikat w konsoli potwierdzający eksport, a plik PPTX pojawi się w określonym folderze.

## Podsumowanie

Teraz wiesz, **how to wrap cells** w arkuszu Excel, **how to use WRAPCOLS**, oraz dokładne kroki **convert Excel to PowerPoint** poprzez **save excel as powerpoint** przy użyciu Aspose.Cells. Kompletny przykład demonstruje **create workbook worksheet**, stosuje formułę zawijania i generuje edytowalny plik PPTX gotowy do modyfikacji prezentacji.

### Kolejne kroki

- Zbadaj inne funkcje Excela (np. `TRANSPOSE`, `FILTER`) przed eksportem.
- Połącz wiele arkuszy w wieloslajdową prezentację PowerPoint przy użyciu pętli.
- Dodaj własne tytuły slajdów lub branding, integrując Aspose.Slides po eksporcie.

Śmiało eksperymentuj z różną liczbą kolumn, zakresami źródłowymi lub nawet łącz wykresy i tabele w jednym PPTX. Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Wrap Text in Excel Using Aspose.Cells for .NET | Formatting Tutorial](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Export Excel Workbook and Worksheet Properties to HTML Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}