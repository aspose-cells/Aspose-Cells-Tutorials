---
category: general
date: 2026-02-15
description: Maak een werkmap in C# en exporteer een DataTable naar Excel met rijopmaak,
  stel de achtergrondkleur van rijen in en automatiseer Excel‑taken in enkele minuten.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: nl
og_description: Maak snel een C#‑werkmap, pas rijstijlen toe en automatiseer Excel‑export
  met volledige codevoorbeelden en best‑practice‑tips.
og_title: Werkmap maken C# – DataTable exporteren naar Excel met opmaak
tags:
- C#
- Excel
- DataExport
title: Werkmap maken C# – DataTable exporteren naar Excel met opmaak
url: /nl/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkmap maken C# – DataTable exporteren naar Excel met opmaak

Heb je ooit **create workbook C#** moeten gebruiken en een `DataTable` naar Excel dumpen met aangepaste opmaak? Je bent niet de enige. In veel line‑of‑business‑applicaties is de eis om een mooi opgemaakte spreadsheet te genereren die een niet‑technische gebruiker direct kan openen en begrijpen.  

In deze gids lopen we stap voor stap door een complete, kant‑klaar oplossing die je **hoe je create workbook C#** laat zien, **excel export formatting** toepast, een **row background** instelt, en **excel automation c#** benut om een gepolijst bestand te produceren. Geen vage “zie de docs” shortcuts—alleen de volledige code, uitleg waarom elke regel belangrijk is, en tips die je morgen echt kunt gebruiken.

---

## Vereisten

- .NET 6 (of .NET Framework 4.6+).  
- Visual Studio 2022 of een C#‑compatibele IDE.  
- Het **Aspose.Cells for .NET** NuGet‑pakket (of een bibliotheek die `Workbook`, `Worksheet`, `Style` blootlegt).  
- Basiskennis van `DataTable`.  

Als je Aspose.Cells nog niet hebt, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** De gratis proefversie werkt voor de meeste ontwikkelingsscenario's; vergeet alleen niet de licentiesleutel te vervangen voordat je de applicatie uitbrengt.

![Voorbeeld van create workbook C# met gestileerde rijen in Excel]( "Voorbeeld van create workbook C# met rijachtergrondkleuren")

---

## Stap 1: Initialiseer de Workbook en Worksheet (Create Workbook C#)

Het eerste wat je moet doen is een `Workbook` instantieren. Beschouw het als het openen van een gloednieuwe Excel‑bestand in het geheugen.

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

**Waarom?**  
`Workbook` bevat het volledige Excel‑document, terwijl `Worksheet` een enkel tabblad vertegenwoordigt. Beginnen met een lege workbook zorgt ervoor dat je volledige controle hebt over elk aspect van de output—geen verborgen standaardstijlen die zich ongemerkt toevoegen.

---

## Stap 2: Een voorbeeld‑DataTable voorbereiden (Export DataTable Excel)

In een echt project haal je gegevens uit een database, maar voor illustratie bouwen we een kleine `DataTable` direct in de code.

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

**Waarom dit belangrijk is:**  
Een `DataTable` exporteren is de meest voorkomende manier om tabelgegevens van een applicatie naar Excel te verplaatsen. De bovenstaande methode is volledig zelfstandig, zodat je het kunt kopiëren‑plakken in elk project en het zal werken.

---

## Stap 3: Een stijl per rij maken (Excel Export Formatting)

Om elke rij een eigen achtergrondkleur te geven, genereren we een `Style`‑object voor elke rij in de `DataTable`. Hier komt **excel export formatting** goed van pas.

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

**Waarom per‑rij styling?**  
Als je specifieke records wilt markeren (bijv. achterstallige facturen) kun je de eenvoudige kleurcyclus vervangen door conditionele logica—stel gewoon `style.ForegroundColor` in op basis van de gegevens van de rij.

---

## Stap 4: De DataTable importeren met rij‑stijlen (Set Row Background)

Nu brengen we alles samen: de gegevens, de workbook en de stijlen.

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

**Wat je zult zien:**  
Het openen van `EmployeesReport.xlsx` toont een koprij in standaardopmaak, gevolgd door vier gegevensrijen, elk voorzien van een lichte achtergrondkleur. Het resultaat ziet eruit als een handgemaakte rapportage, niet als een saaie dump.

---

## Stap 5: Geavanceerde Excel Automation C# Tips (Excel Automation C#)

Hieronder staan een paar snelle trucjes die je bovenop het basisvoorbeeld kunt toepassen:

| Tip | Codefragment | Wanneer te gebruiken |
|-----|--------------|----------------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Na het importeren van gegevens om afgekapt tekst te voorkomen. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Wanneer de tabel verder kan scrollen dan het scherm. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Salarissen boven een drempel markeren. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Wanneer je alleen‑lezen rapporten nodig hebt. |

---

## Veelgestelde vragen & randgevallen

**Wat als de DataTable duizenden rijen bevat?**  
Aspose.Cells streamt gegevens efficiënt, maar je wilt misschien het aanmaken van stijlen voor elke rij uitschakelen om geheugen te besparen. Pas in plaats daarvan één stijl toe op een bereik:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Kan ik exporteren naar .csv in plaats van .xlsx?**  
Zeker—verander gewoon het opslagformaat:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

De opmaak gaat verloren (CSV heeft geen opmaak), maar de gegevensexport blijft hetzelfde.

**Werkt dit op .NET Core?**  
Ja. Aspose.Cells ondersteunt .NET Standard 2.0 en later, dus dezelfde code draait op .NET 6, .NET 7 of .NET Framework.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

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