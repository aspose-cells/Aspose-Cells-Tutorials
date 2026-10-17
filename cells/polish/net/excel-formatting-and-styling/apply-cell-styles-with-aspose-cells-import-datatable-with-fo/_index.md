---
category: general
date: 2026-06-05
description: Stosuj style komórek podczas importu przy użyciu Aspose.Cells. Dowiedz
  się, jak importować DataTable z formatowaniem, stylizować wiersze i utrzymywać arkusze
  w porządku.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: pl
og_description: Zastosuj style komórek podczas importowania DataTable do arkusza Aspose.Cells.
  Przewodnik krok po kroku z pełnym kodem i wskazówkami.
og_title: Zastosuj style komórek w Aspose.Cells – importuj DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Zastosuj style komórek w Aspose.Cells – importuj DataTable z formatowaniem
url: /pl/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosuj style komórek w Aspose.Cells – importuj DataTable z formatowaniem

Zastanawiałeś się kiedyś, jak **zastosować style komórek**, gdy wciągasz `DataTable` do arkusza Excel? Nie jesteś jedyny. W wielu scenariuszach raportowania potrzebujesz, aby dane wyglądały dobrze od razu — bez ręcznego formatowania później. Dobrą wiadomością jest to, że Aspose.Cells ułatwia **import z formatowaniem**, więc Twoje wiersze mogą być czerwone lub niebieskie, pogrubione lub cokolwiek chcesz.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokazuje **jak zaimportować datatable** do arkusza **z zastosowanymi stylami komórek**. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową C#, która tworzy skoroszyt, stylizuje pierwsze dwie kolumny i zapisuje plik — wszystko przy użyciu API `aspose cells import`.

## Czego się nauczysz

- Skonfiguruj Aspose.Cells w projekcie .NET  
- Zbuduj przykładowy `DataTable`, który naśladuje rzeczywiste dane  
- Zdefiniuj obiekty `Style` dla czerwonej i niebieskiej czcionki  
- Użyj `Worksheet.Cells.ImportDataTable`, aby **zaimportować arkusz datatable** z jednoczesnym zastosowaniem stylów  
- Zweryfikuj wynik i zapisz skoroszyt  

Bez dodatkowych narzędzi, tylko czysty C# i Aspose.Cells. Zaczynajmy.

## Wymagania wstępne

Zanim zagłębimy się w kod, upewnij się, że masz następujące elementy:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells 23.x jest przeznaczony dla .NET Standard 2.0+, więc .NET 6 zapewnia najnowsze funkcje środowiska uruchomieniowego. |
| Aspose.Cells for .NET (NuGet) | Biblioteka udostępnia potrzebne nam metody `Workbook`, `Worksheet`, `Style` oraz `ImportDataTable`. |
| Basic C# knowledge | Zrozumiesz klasy, tablice i instrukcje `using`. |
| An IDE (Visual Studio, VS Code, Rider) | Każdy edytor się sprawdzi, ale będziesz musiał przywrócić pakiety NuGet. |

Możesz zainstalować pakiet z wiersza poleceń:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Utwórz nowy skoroszyt i uzyskaj dostęp do pierwszego arkusza

Na początek—utwórzmy `Workbook` i pobierzmy pierwszy arkusz. Myśl o skoroszycie jak o pustym notesie; pierwszy arkusz to strona, na której będziemy pisać.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Wskazówka:** Jeśli kiedykolwiek potrzebujesz wielu arkuszy, po prostu dodaj je za pomocą `wb.Worksheets.Add()` i odwołuj się do nich po nazwie lub indeksie.

## Krok 2: Przygotuj przykładowy DataTable (Jak zaimportować DataTable)

Teraz potrzebujemy czegoś do zaimportowania. W rzeczywistych projektach wywołałbyś bazę danych, ale dla przejrzystości zbudujemy `DataTable` w pamięci.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Dlaczego to ważne:** Posiadanie `DataTable` pozwala nam przetestować przepływ **aspose cells import** bez żadnych zewnętrznych zależności.

## Krok 3: Zdefiniuj style do zastosowania w importowanych komórkach

Tutaj dzieje się magia. Utworzymy dwa obiekty `Style`: jeden z czerwoną czcionką, drugi z niebieską czcionką. Zostaną one zastosowane kolumnowo podczas importu.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Uwaga:** Długość `importStyles` musi odpowiadać liczbie kolumn, które importujesz, w przeciwnym razie Aspose zgłosi `ArgumentException`.

## Krok 4: Zaimportuj DataTable do arkusza **z formatowaniem**

Teraz łączymy wszystko. Przeciążenie `ImportDataTable`, którego używamy, przyjmuje tablicę `Style[]`, co pozwala nam **zastosować style komórek** w momencie, gdy dane trafiają do arkusza.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Jak to działa

1. **Nagłówki** – Ponieważ przekazaliśmy `true`, Aspose zapisuje „Name” i „Score” w pierwszym wierszu.  
2. **Wiersze danych** – Każdy kolejny wiersz otrzymuje odpowiedni styl z `importStyles`.  
3. **Wydajność** – Metoda strumieniuje dane bezpośrednio do arkusza, co jest szybsze niż iteracyjne przetwarzanie komórek.

## Krok 5: Zweryfikuj wynik i zapisz skoroszyt

Sprawdźmy kilka pierwszych komórek, aby upewnić się, że style się utrzymały, a następnie zapiszmy plik na dysku.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Gdy otworzysz **StyledImport.xlsx**, zobaczysz:

- Kolumna „Name” w **czerwonym** tekście.  
- Kolumna „Score” w **niebieskim** tekście.  
- Nagłówki kolumn w domyślnym stylu (można je również stylizować, ale to kolejny samouczek).

![Przykład zastosowania stylów komórek](https://example.com/images/apply-cell-styles.png "Zastosowanie stylów komórek w Aspose.Cells")

> **Uwaga:** Powyższy obrazek demonstruje ostateczny wygląd. Atrybut `alt` zawiera główne słowo kluczowe, spełniając wymagania SEO.

## Częste pytania i przypadki brzegowe

### Co jeśli mój DataTable ma więcej kolumn niż stylów?

Aspose zastosuje ostatni styl w tablicy do wszelkich dodatkowych kolumn. Aby uniknąć nieoczekiwanych kolorów, zawsze dopasowuj długość tablicy do liczby kolumn lub przekaż `null` dla kolumn, które nie mają być stylizowane.

### Czy mogę zastosować różne style do konkretnych wierszy?

Oczywiście. Po imporcie możesz przeiterować wiersze i przypisać nowe obiekty `Style` w zależności od warunków (np. podświetlić wyniki > 90 na zielono). Oto szybki fragment kodu:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Czy to działa z dużymi zestawami danych?

Tak. `ImportDataTable` strumieniuje dane wydajnie, a zastosowanie statycznej tablicy stylów dodaje pomijalny narzut. Przy milionach wierszy rozważ użycie `ImportDataTable` w partiach lub wykorzystanie `Cells.ImportDataTable` z `DataReader` dla jeszcze lepszego zarządzania pamięcią.

### Jak zachować istniejące formatowanie w arkuszu?

Jeśli docelowy zakres już ma formatowanie, które chcesz zachować, ustaw parametr `importOptions` przeciążenia `ImportDataTable` (`ImportTableOptions`) i dostosuj `ImportDataTableOptions.PreserveCellFormatting`. Domyślne zachowanie nadpisuje style tymi, które podasz.

## Podsumowanie: Co osiągnęliśmy

- **Zastosowano style komórek** podczas operacji **aspose cells import**.  
- Zademonstrowano **import z formatowaniem** poprzez przekazanie tablicy `Style[]`.  
- Pokażano **jak zaimportować datatable** do arkusza i zapisać wynik.  
- Omówiono przypadki brzegowe, takie jak niezgodna liczba stylów oraz warunkowe stylizowanie wierszy.  

Wszystko to zostało zrealizowane w jednej, samodzielnej aplikacji konsolowej — bez zewnętrznych skryptów, bez ręcznego majsterkowania w Excelu. Masz teraz solidną bazę dla każdej funkcji raportowania lub eksportu danych, która wymaga dopracowanego wyjścia w Excelu.

## Kolejne kroki

Gotowy, aby podnieść poziom? Oto kilka pomysłów, które rozwijają to, czego się właśnie nauczyłeś:

- **Stylizuj wiersz nagłówka** (np. pogrubienie, kolor tła).  
- **Zastosuj formatowanie warunkowe** używając `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Eksportuj do innych formatów** takich jak CSV lub PDF przy użyciu `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Połącz wiele DataTables** w jeden skoroszyt, każdy na osobnym arkuszu, używając tego samego podejścia do stylizacji.  

Jeśli napotkasz problemy, zostaw komentarz lub sprawdź oficjalną dokumentację Aspose dotyczącą `ImportDataTable`. Szczęśliwego kodowania i ciesz się pięknie stylizowanymi plikami Excel!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaimportować DataTable do Excela przy użyciu Aspose.Cells dla .NET (przewodnik krok po kroku)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Jak ustawić style czcionki w Excelu przy użyciu Aspose.Cells dla .NET (przewodnik krok po kroku)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Jak zastosować cień tekstu w Excelu przy użyciu Aspose.Cells .NET: przewodnik krok po kroku](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}