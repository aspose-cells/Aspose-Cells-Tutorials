---
category: general
date: 2026-02-15
description: Utwórz skoroszyt w C# i wyeksportuj DataTable do Excela z formatowaniem
  wierszy, ustaw tło wiersza oraz automatyzuj zadania w Excelu w ciągu kilku minut.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: pl
og_description: Szybko twórz skoroszyt w C#, stosuj style wierszy i automatyzuj eksport
  do Excela z pełnymi przykładami kodu oraz wskazówkami najlepszych praktyk.
og_title: Tworzenie skoroszytu C# – Eksport DataTable do Excela z formatowaniem
tags:
- C#
- Excel
- DataExport
title: Utwórz skoroszyt C# – Eksportuj DataTable do Excela z formatowaniem
url: /pl/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt C# – Eksportuj DataTable do Excela z formatowaniem

Czy kiedykolwiek potrzebowałeś **create workbook C#** i wyeksportować `DataTable` do Excela z własnym formatowaniem? Nie jesteś sam. W wielu aplikacjach biznesowych wymagana jest generacja ładnie sformatowanego arkusza kalkulacyjnego, który nie‑techniczny użytkownik może otworzyć i od razu zrozumieć.  

W tym przewodniku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które pokazuje **how to create workbook C#**, zastosowanie **excel export formatting**, ustawienie **row background** oraz wykorzystanie **excel automation c#**, aby stworzyć dopracowany plik. Bez niejasnych „zobacz dokumentację” skrótów — tylko pełny kod, wyjaśnienia, dlaczego każda linia ma znaczenie, oraz wskazówki, które naprawdę wykorzystasz jutro.

---

## Wymagania wstępne

- .NET 6 (lub .NET Framework 4.6+).  
- Visual Studio 2022 lub dowolne IDE kompatybilne z C#.  
- Pakiet NuGet **Aspose.Cells for .NET** (lub dowolna biblioteka udostępniająca `Workbook`, `Worksheet`, `Style`).  
- Podstawowa znajomość `DataTable`.  

Jeśli jeszcze nie masz Aspose.Cells, uruchom:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Bezpłatna wersja próbna działa w większości scenariuszy deweloperskich; pamiętaj tylko, aby przed wydaniem zamienić klucz licencyjny.

![Przykład create workbook C# pokazujący stylowane wiersze w Excelu]( "Przykład create workbook C# z kolorami tła wierszy")

---

## Krok 1: Zainicjalizuj Workbook i Worksheet (Create Workbook C#)

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji `Workbook`. Traktuj to jak otwarcie zupełnie nowego pliku Excela w pamięci.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Dlaczego?**  
`Workbook` przechowuje cały dokument Excel, natomiast `Worksheet` reprezentuje pojedynczą zakładkę. Rozpoczęcie od czystego workbooka zapewnia kontrolę nad każdym aspektem wyjścia — żadne ukryte domyślne style nie wkradną się.

---

## Krok 2: Przygotuj przykładowy DataTable (Export DataTable Excel)

W rzeczywistym projekcie pobrałbyś dane z bazy danych, ale na potrzeby ilustracji zbudujemy mały `DataTable` w locie.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Dlaczego to ważne:**  
Eksportowanie `DataTable` jest najczęstszym sposobem przenoszenia danych tabelarycznych z aplikacji do Excela. Powyższa metoda jest w pełni samodzielna, więc możesz ją skopiować i wkleić do dowolnego projektu i będzie działać.

---

## Krok 3: Utwórz styl dla każdego wiersza (Excel Export Formatting)

Aby nadać każdemu wierszowi własny kolor tła, generujemy obiekt `Style` dla każdego wiersza w `DataTable`. To właśnie tutaj **excel export formatting** błyszczy.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Dlaczego stylowanie per‑wiersz?**  
Jeśli musisz wyróżnić konkretne rekordy (np. zaległe faktury), możesz zastąpić prostą rotację kolorów logiką warunkową — po prostu ustaw `style.ForegroundColor` w zależności od danych w wierszu.

---

## Krok 4: Importuj DataTable ze stylami wierszy (Set Row Background)

Teraz łączymy wszystko: dane, workbook i style.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Co zobaczysz:**  
Otwierając `EmployeesReport.xlsx` zobaczysz wiersz nagłówka w domyślnym formatowaniu, a następnie cztery wiersze danych, każdy pomalowany delikatnym kolorem tła. Efekt wygląda jak ręcznie przygotowany raport, a nie nijaki zrzut danych.

---

## Krok 5: Zaawansowane wskazówki Excel Automation C# (Excel Automation C#)

Poniżej znajduje się kilka szybkich trików, które możesz dodać do podstawowego przykładu:

| Wskazówka | Fragment kodu | Kiedy używać |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Po zaimportowaniu danych, aby uniknąć obciętego tekstu. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Gdy tabela może przewijać się poza ekran. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Podświetl wynagrodzenia powyżej określonego progu. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Gdy potrzebujesz raportów tylko do odczytu. |

Te fragmenty pokazują zakres możliwości **excel automation c#** — możesz dalej rozwijać skoroszyt bez przepisywania podstawowej logiki importu.

---

## Częste pytania i przypadki brzegowe

**Co jeśli DataTable ma tysiące wierszy?**  
Aspose.Cells strumieniuje dane efektywnie, ale możesz chcieć wyłączyć tworzenie stylu dla każdego wiersza, aby zaoszczędzić pamięć. Zamiast tego zastosuj pojedynczy styl do zakresu:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Czy mogę wyeksportować do .csv zamiast .xlsx?**  
Oczywiście — po prostu zmień format zapisu:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Stylizacja zostanie utracona (CSV nie obsługuje stylów), ale eksport danych pozostanie taki sam.

**Czy to działa na .NET Core?**  
Tak. Aspose.Cells obsługuje .NET Standard 2.0 i nowsze, więc ten sam kod działa na .NET 6, .NET 7 lub .NET Framework.

---

## Pełny działający przykład (Gotowy do kopiowania‑wklejania)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}