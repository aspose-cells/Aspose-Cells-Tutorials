---
category: general
date: 2026-07-13
description: Formatuj kolumnę daty w Excelu podczas eksportowania DataTable z C#.
  Naucz się eksportować DataTable do Excela w C# i importować DataTable do Excela
  ze stylizacją w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: pl
lastmod: 2026-07-13
og_description: Formatuj kolumnę daty w Excelu bez wysiłku. Ten przewodnik pokazuje,
  jak wyeksportować DataTable w C# do Excela oraz zaimportować DataTable do Excela
  z niestandardowymi stylami.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: 'Formatowanie kolumny dat w Excel – krok po kroku: tutorial eksportu w C#'
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Formatowanie kolumny dat w Excelu – Kompletny przewodnik C# po eksporcie DataTable
url: /pl/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatowanie kolumny dat w Excel – Kompletny przewodnik C# po eksportie DataTable

Czy kiedykolwiek potrzebowałeś **format date column Excel**, pobierając dane z bazy, ale komórki wyświetlały surowe znaczniki czasu? Nie jesteś sam. W wielu aplikacjach biznesowych domyślny eksport zapisuje wartość `DateTime` taką jak `2024‑03‑15 00:00:00`, a nikt nie chce takiego bałaganu.  

Dobre wiadomości są takie, że możesz kontrolować dokładny wygląd każdej kolumny bezpośrednio z C#. W tym samouczku przeprowadzimy Cię przez kompleksowe rozwiązanie, które **excel export datatable c#**, stosuje styl daty do pierwszej kolumny, styl waluty do drugiej i w końcu **import datatable to excel** bezproblemowo.

Na koniec będziesz mieć metodę, którą możesz wstawić do dowolnego projektu .NET, niezależnie od tego, czy używasz .NET 6, .NET Framework 4.8, czy nowszej wersji.

---

## Czego będziesz potrzebował

- **Aspose.Cells for .NET** (lub dowolna biblioteka oferująca `CreateStyle` i `ImportDataTable`). Fragmenty kodu używają Aspose, ponieważ jego API jest czyste i szeroko stosowane.
- **DataTable**, którą już wypełniasz z SQL, CSV lub innego źródła.
- Visual Studio (lub Twoje ulubione IDE).  
- Środowisko uruchomieniowe .NET 5.0+ (przykład celuje w .NET 6, ale starsze frameworki działają tak samo).

Jeśli jeszcze nie masz Aspose.Cells, pobierz darmową wersję próbną ze strony oficjalnej — bez wymogu podania karty kredytowej.

---

## Krok 1: Pobierz dane źródłowe jako DataTable

Na początek potrzebujesz `DataTable`. W rzeczywistych scenariuszach zazwyczaj pochodzi ona z `SqlDataAdapter.Fill`, ale dla przejrzystości zamockujemy prostą tabelę:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tip:** Gdy pobierasz dane bezpośrednio z procedury składowanej, upewnij się, że typy kolumn odpowiadają zamierzonym formatom w Excelu. Kolumna `datetime` będzie później celem naszego stylu **format date column excel**.

---

## Krok 2: Utwórz skoroszyt Excel i zdefiniuj style kolumn

Teraz tworzymy nowy skoroszyt. Sztuczka do **format date column excel** polega na utworzeniu obiektu `Style`, ustawieniu jego właściwości `Number` na wbudowany format daty Excela (kod 14) i przypisaniu tego stylu do odpowiedniego indeksu kolumny.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Dlaczego `Number = 14`? Excel przechowuje daty jako liczby seryjne; format 14 instruuje program, aby wyświetlał te liczby przy użyciu krótkiego wzorca daty ustawionego w lokalizacji. Jeśli potrzebujesz własnego wzorca (np. `dd‑MMM‑yyyy`), możesz zamiast tego ustawić `columnStyles[0].Custom = "dd-MMM-yyyy"`.

---

## Krok 3: Importuj DataTable do arkusza z stylami

Gdy tablica stylów jest gotowa, wywołanie importu to jedna linia. To serce **excel export datatable c#**, a także miejsce, w którym **import datatable to excel**, zachowując nasze formatowanie.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Przeciążenie `ImportDataTable`, którego używamy, przyjmuje tablicę stylów, stosując każdy styl do pasującej kolumny w trakcie zapisu danych. Nie ma potrzeby pętli post‑processing — Twoja kolumna dat jest już ładnie sformatowana.

---

## Krok 4: Zapisz skoroszyt (lub przesyłaj go bezpośrednio do przeglądarki)

W zależności od scenariusza możesz zapisać na dysk, do strumienia pamięci lub zwrócić plik jako odpowiedź HTTP. Oto trzy typowe wzorce:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Watch out for:** Jeśli używasz `FileResult` w ASP.NET Core, upewnij się, że ustawiasz `Response.Headers["Cache-Control"] = "no-cache"` gdy plik jest generowany w locie. Zapobiega to serwowaniu przestarzałej wersji przez przeglądarkę.

---

## Krok 5: Zweryfikuj wynik – jak wygląda arkusz Excel

Po uruchomieniu kodu otwórz `ExportedReport.xlsx`. Powinieneś zobaczyć:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Zauważ, że **format date column excel** wyświetla czystą krótką datę, podczas gdy kolumna waluty automatycznie dopasowuje się do Twoich ustawień regionalnych. Nie jest potrzebne ręczne formatowanie komórek.

![format date column excel example](/images/format-date-column-excel.png)

*Tekst alternatywny obrazu: format date column excel – zrzut ekranu arkusza Excel z prawidłowo sformatowaną kolumną dat.*

---

## Często zadawane pytania i przypadki brzegowe

### Co jeśli moja DataTable ma więcej niż trzy kolumny?

Po prostu rozszerz tablicę `columnStyles`. Dla każdej kolumny, której nie stylizujesz explicite, pozostaw wpis `null`; Excel zastosuje domyślny format General.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Jak zastosować własny format daty (np. „dd‑MMM‑yyyy”)?

Zastąp wbudowany numer własnym ciągiem:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Czy mogę użyć tego podejścia z EPPlus lub ClosedXML?

Tak, koncepcja jest identyczna: utwórz obiekt stylu, przypisz go do kolumny, a następnie załaduj `DataTable`. API się różni, ale wzorzec **excel export datatable c#** pozostaje taki sam.

### A co z dużymi zestawami danych (100 k+ wierszy)?

`ImportDataTable` jest zoptymalizowany pod kątem masowych zapisów, ale możesz napotkać limity pamięci. W takim przypadku rozważ strumieniowanie wierszy przy użyciu `Cells.ImportDataTable` w partiach lub użyj `Worksheet.Cells["A1"].PutValue` w pętli, ponownie wykorzystując obiekty stylów.

---

## Pełny działający przykład (wszystkie kroki w jednej metodzie)

Poniżej znajduje się samodzielna metoda, którą możesz skopiować i wkleić do dowolnej aplikacji konsolowej lub kontrolera ASP.NET. Demonstruje ona cały przepływ — od pobrania danych po stylizowany eksport do Excela.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Uruchom program, otwórz `StyledExport.xlsx`, a zobaczysz, że **format date column excel** został zastosowany perfekcyjnie.

---

## Podsumowanie i kolejne kroki

Właśnie omówiliśmy, jak **format date column excel** podczas wykonywania **excel export datatable c#**, oraz jak **import datatable to excel** z formatowaniem per‑kolumna w jednym wywołaniu. Najważniejsze wnioski:

1. Utwórz `Style` dla każdej kolumny, którą chcesz sformatować.  
2. Użyj `Number = 14` dla dat, `Number = 2` dla waluty lub dowolnego własnego formatu, którego potrzebujesz.  
3. Przekaż tablicę stylów do `ImportDataTable` — biblioteka wykona ciężką pracę.

Co możesz zbadać dalej?

- **Conditional formatting** aby podświetlić przeterminowane daty.  
- **

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z instrukcjami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}