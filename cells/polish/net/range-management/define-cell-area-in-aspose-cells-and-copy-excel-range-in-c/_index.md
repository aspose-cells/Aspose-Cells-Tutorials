---
category: general
date: 2026-08-04
description: Zdefiniuj obszar komórek w Aspose.Cells i dowiedz się, jak kopiować tabele
  przestawne, kopiować zakres w Excelu w C# oraz kopiować zakres w tym samym arkuszu
  efektywnie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: pl
lastmod: 2026-08-04
og_description: Zdefiniuj obszar komórek w Aspose.Cells i skopiuj zakres Excela w
  C#, zachowując tabele przestawne. Postępuj zgodnie z tym przewodnikiem krok po kroku,
  aby uzyskać niezawodne wyniki.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Zdefiniuj obszar komórek w Aspose.Cells – skopiuj zakres Excel w C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Zdefiniuj obszar komórek w Aspose.Cells i skopiuj zakres Excela w C#
url: /pl/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zdefiniuj obszar komórek w Aspose.Cells i skopiuj zakres Excel w C#

Jeśli potrzebujesz **zdefiniować obszar komórek** dla zakresu i następnie skopiować ten zakres na tym samym arkuszu, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells dla .NET. Niezależnie od tego, czy przenosisz raport oparty na tabeli przestawnej, czy duplikujesz blok danych, poznasz kompletny proces w kilku prostych krokach.

Odkryjesz także **how to copy pivot** tabele bez utraty ich połączeń oraz zobaczysz czysty przykład **copy excel range c#**, który działa w scenariuszu **copy range same sheet**. Nie są wymagane żadne zewnętrzne narzędzia — tylko Aspose.Cells i kilka linii C#.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
- Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`)
- Plik Excel (`input.xlsx`) zawierający tabelę przestawną w zakresie A1:J50
- Środowisko programistyczne, np. Visual Studio 2022

## Krok 1: Zdefiniuj obszar komórek dla zakresu źródłowego

Pierwszym zadaniem jest **zdefiniować obszar komórek**, który reprezentuje blok, który chcesz skopiować. Aspose.Cells używa struktury `CellArea`, która przechowuje indeksy wierszy i kolumn zaczynające się od zera.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Dlaczego to ważne:** `CellArea` informuje Aspose.Cells dokładnie, które komórki mają być przetwarzane. Używanie indeksów zerowych eliminuje typowe błędy o jeden (off‑by‑one), które występują przy konwersji notacji A1 z Excela na kod.

## Krok 2: Zdefiniuj docelowy obszar komórek na tym samym arkuszu

Aby **copy range same sheet**, musisz również określić, gdzie dane mają zostać umieszczone. Cel może zaczynać się w dowolnym wierszu; tutaj zaczynamy od wiersza 61 (indeks zerowy 60), aby zostawić pusty bufor.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Dlaczego to ważne:** Dzięki odzwierciedleniu wymiarów źródła zapewniasz, że skopiowany blok pasuje idealnie, bez obcięcia.

## Krok 3: Skopiuj zakres zachowując tabele przestawne

Teraz możesz **how to copy pivot** bezpiecznie. Klasa `CopyOptions` zawiera flagę `CopyPivotTables`, która zachowuje definicję tabeli przestawnej, źródło danych i formatowanie.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Dlaczego to ważne:** Bez ustawienia `CopyPivotTables = true` tabela przestawna stanie się statycznym migawką, tracąc interaktywność. Ta opcja kopiuje podstawową pamięć podręczną i połączenia, dzięki czemu nowa tabela przestawna zachowuje się dokładnie tak jak oryginalna.

## Krok 4: Zapisz skoroszyt

Na koniec zapisz zmiany na dysk. Plik wyjściowy pokazuje, że tabela przestawna została zduplikowana na tym samym arkuszu.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Wskazówka:** Użyj `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)`, jeśli musisz wymusić konkretny format, szczególnie przy pracy ze starszymi wersjami Excela.

## Krok 5: Zweryfikuj skopiowaną tabelę przestawną

Otwórz `CopyWithPivot.xlsx` w Excelu i sprawdź następujące elementy:

1. Zakres A61:J110 zawiera kopię oryginalnych danych.
2. Nowa tabela przestawna pojawia się na górze skopiowanego zakresu.
3. Odświeżenie tabeli przestawnej odzwierciedla zmiany w danych źródłowych, potwierdzając, że **how to copy pivot** zakończyło się sukcesem.

Jeśli tabela przestawna nie odświeża się, upewnij się, że zakres danych źródłowych w definicji tabeli przestawnej nadal wskazuje na oryginalny obszar skoroszytu. Aspose.Cells automatycznie aktualizuje odwołanie źródłowe, gdy `CopyPivotTables` jest ustawione na true.

## Przypadki brzegowe i warianty

| Situation | What to change |
|-----------|----------------|
| **Kopiowanie do innego arkusza** | Zastąp `srcWorkbook.Worksheets[0]` indeksem lub nazwą docelowego arkusza i odpowiednio dostosuj `destinationRange`. |
| **Kopiowanie połączonego bloku komórek** | Ustaw `CopyOptions.PasteType = PasteType.All`, aby zachować połączone komórki i formatowanie. |
| **Kopiowanie tylko wartości, bez formuł** | Użyj `CopyOptions.PasteType = PasteType.Values`, aby uniknąć przenoszenia formuł odwołujących się do oryginalnego arkusza. |
| **Duże zakresy ( > 10 000 wierszy )** | Rozważ użycie `Workbook.Copy` dla całych arkuszy w celu zwiększenia wydajności, a następnie usuń niepotrzebne wiersze. |

Te warianty pokazują, że ta sama logika **aspose.cells copy range** może być dostosowana do wielu rzeczywistych scenariuszy.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką folderu na swoim komputerze.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Oczekiwany wynik:** Po uruchomieniu programu, `CopyWithPivot.xlsx` zawiera oryginalne dane oraz identyczny blok zaczynający się od wiersza 61, wraz z działającą tabelą przestawną.

## Zakończenie

Teraz wiesz, jak **define cell area** w Aspose.Cells, **copy excel range c#** oraz **copy range same sheet**, zachowując pełną funkcjonalność tabel przestawnych. Ta technika eliminuje błędy ręcznego kopiowania i wklejania oraz skaluje się do dużych skoroszytów.

Następnie, zapoznaj się z powiązanymi tematami, takimi jak **how to copy pivot** między wieloma arkuszami, lub użyj **aspose.cells copy range**, aby zduplikować całe arkusze wraz z formatowaniem. Eksperymentuj z różnymi ustawieniami `CopyOptions`, aby dostosować zachowanie kopiowania do potrzeb Twojego projektu.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Excel Aspose Cells Dotnet Kopiowanie Danych Zakresu](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Kopiowanie Danych Zakresu](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Kopiowanie Danych Zakresu](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}