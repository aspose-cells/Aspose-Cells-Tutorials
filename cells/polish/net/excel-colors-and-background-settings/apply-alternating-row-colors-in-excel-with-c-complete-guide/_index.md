---
category: general
date: 2026-07-03
description: Zastosuj naprzemienne kolory wierszy podczas importowania tabeli danych
  do Excela przy użyciu C#. Dowiedz się, jak wyeksportować tabelę danych C# do Excela,
  zapisać stylizowany arkusz Excel i zachować formatowanie skoroszytu.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: pl
og_description: Zastosuj naprzemienne kolory wierszy w Excelu przy użyciu C#. Ten
  tutorial pokazuje, jak zaimportować DataTable do Excela, wyeksportować DataTable
  z C# do Excela oraz zapisać skoroszyt z formatowaniem.
og_title: Zastosuj naprzemienne kolory wierszy w Excelu przy użyciu C# – Kompletny
  przewodnik
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Zastosuj naprzemienne kolory wierszy w Excelu przy użyciu C# – Kompletny przewodnik
url: /pl/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosuj naprzemienne kolory wierszy w Excelu przy użyciu C# – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **zastosować naprzemienne kolory wierszy** przy eksporcie `DataTable` z C# do Excela? Nie jesteś jedyny — programiści stale pytają, jak sprawić, by arkusze wyglądały profesjonalnie, bez ręcznego formatowania w Excelu po fakcie. Dobra wiadomość? Możesz to zrobić programowo w zaledwie kilku linijkach kodu.

W tym tutorialu przejdziemy przez **import datatable to excel**, pokażemy, jak **export c# datatable to excel** z sformatowaną tabelą, a na koniec **save styled table excel** zachowując formatowanie. Po zakończeniu będziesz w stanie **save workbook with formatting**, które wygląda gotowe na spotkanie z klientem.

## Prerequisites

- .NET 6.0 lub nowszy (przykład używa .NET 6, ale działa z każdą aktualną wersją)
- Aspose.Cells for .NET (wersja trial lub licencjonowana) – ta biblioteka upraszcza stylizowanie
- Źródło `DataTable` (może pochodzić z bazy danych, CSV lub kolekcji w pamięci)

> **Pro tip:** Jeśli jeszcze nie masz Aspose.Cells, możesz go pobrać z NuGet przy pomocy `dotnet add package Aspose.Cells`.

## Step 1: Set Up the Project and Load Your Data

Najpierw utwórz aplikację konsolową (lub dowolny projekt C#) i dodaj niezbędne dyrektywy `using`. Następnie wczytaj dane do `DataTable`. Dla ilustracji wygenerujemy prostą tabelę w locie.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Dlaczego to ważne:** Mając gotowy `DataTable`, możesz **import datatable to excel** jednym wywołaniem, eliminując potrzebę ręcznego wstawiania komórek po kolei.

## Step 2: Create a Workbook and Define the Alternating Row Styles

Teraz utworzymy nowy `Workbook`. Sztuczka, aby **apply alternating row colors**, polega na użyciu `ImportTableOptions.StyleArray`. Skorzystamy z dwóch wbudowanych stylów (zwykle biały i jasnoszary), które później możesz dostosować.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Wyjaśnienie:** `ImportTableOptions` informuje Aspose.Cells, jak traktować każdy wiersz podczas importu. Dostarczając `StyleArray` z dwoma pozycjami, biblioteka automatycznie pomaluje każdy nieparzysty wiersz pierwszym stylem, a każdy parzysty drugim — dokładnie to, czego potrzebujesz, aby **apply alternating row colors**.

## Step 3: Pull the DataTable Into the Worksheet (Including Headers)

Mając już workbook i style, **import datatable to excel**. Metoda `ImportDataTable` wykonuje ciężką pracę: zapisuje nagłówki kolumn, respektuje tablicę stylów i umieszcza dane zaczynając od komórki A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Dlaczego podajemy `true` jako drugi argument:** Dzięki temu metoda zapisuje nazwy kolumn w pierwszym wierszu, co jest niezbędne dla profesjonalnie wyglądającego raportu.

## Step 4: Fine‑Tune the Table (Optional but Handy)

Jeśli chcesz, aby kolumny automatycznie dopasowywały szerokość lub dodać wiersz filtrów, kilka dodatkowych linii sprawi, że tabela będzie błyszczeć.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Te drobne poprawki nie wpływają na naprzemienne kolory, ale podnoszą ogólne wrażenia z pliku **save styled table excel**.

## Step 5: Save the Workbook While Keeping All Formatting

Na koniec zapisujemy plik na dysku. Metoda `Save` zachowuje wszystkie ustawione style, zapewniając, że naprzemienne wiersze pozostaną nienaruszone.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Po otwarciu `StyledEmployees.xlsx` zobaczysz czystą tabelę, w której wiersze naprzemiennie mają biały i jasnoszary kolor tła — dokładnie taki wizualny sygnał, na którym wielu użytkowników polega przy czytelności.

### Expected Output

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Wiersz 1, 3 … → biały tło  
- Wiersz 2, 4 … → jasnoszary tło  

To cały proces **save workbook with formatting**.

## Common Questions & Edge Cases

### What if my DataTable has thousands of rows?

Metoda `ImportDataTable` strumieniuje dane efektywnie, ale przy bardzo dużych tabelach możesz napotkać limity pamięci. W takich przypadkach rozważ podzielenie eksportu na kilka arkuszy lub użycie przeciążenia `ImportDataTable`, które pozwala określić wiersz i kolumnę początkową.

### Can I use custom colors instead of the built‑in ones?

Oczywiście. Wystarczy zamienić przypisania `ForegroundColor` w `styleWhite` i `styleGray` na dowolny `System.Drawing.Color`, który preferujesz — np. pastelowe niebieskie lub kolory firmowe.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### How do I ensure the alternating style works when the user adds rows later?

Jeśli użytkownicy edytują plik ręcznie, oryginalna tablica stylów nie rozciągnie się automatycznie. Szybkim obejściem jest przekształcenie zakresu w tabelę Excela (`ListObject`) po imporcie; Excel wtedy powiela wzorzec dla nowych wierszy.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Teraz każdy nowy wiersz odziedziczy naprzemienne kolory.

## Full Working Example (All Steps in One Place)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Uruchom program, otwórz wygenerowany plik i od razu zobaczysz zastosowane naprzemienne kolory — bez ręcznego formatowania.

## Conclusion

Właśnie pokazaliśmy, jak **apply alternating row colors** przy **import datatable to excel** używając C#. Proces obejmuje wszystko, co potrzebne do **export c# datatable to excel**, **save styled table excel** oraz **save workbook with formatting**, które wygląda profesjonalnie od razu po wygenerowaniu.

Co dalej? Spróbuj zamienić dwa style na własny motyw lub przekształcić zakres w tabelę Excela, aby użytkownicy mogli sortować i filtrować, zachowując jednocześnie wzorzec kolorów. Możesz także zbadać formatowanie warunkowe za pomocą `ConditionalFormattingCollection` dla bardziej dynamicznych wskazówek wizualnych.

Gotowy na kolejny krok?

## What Should You Learn Next?

Poniższe tutoriale obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}