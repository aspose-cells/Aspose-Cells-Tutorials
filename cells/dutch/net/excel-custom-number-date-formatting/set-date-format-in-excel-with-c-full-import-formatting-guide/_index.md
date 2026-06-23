---
category: general
date: 2026-06-17
description: Stel datumformaat in Excel in met C# en stel ook de celachtergrond in,
  pas de voorgrondkleur toe en kleur de Excel‑kolom tijdens het importeren. Leer stap
  voor stap.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: nl
og_description: Datumformaat instellen in Excel met C# terwijl je de celachtergrond
  instelt, de voorgrondkleur toepast en de Excel‑kolom kleurt tijdens het importeren.
  Volledige tutorial.
og_title: Datumformaat instellen in Excel met C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Datumformaat instellen in Excel met C# – Volledige gids voor importopmaak
url: /nl/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datumopmaak instellen in Excel met C# – Complete Gids voor Importopmaak

Heb je ooit **datumopmaak** moeten **instellen** in een Excel‑blad dat vanuit C#‑code wordt gegenereerd, maar ook de kolom een aangepaste achtergrond‑ of tekstkleur wilt geven? Je bent niet de enige. In veel rapportagescenario’s haal je een `DataTable` uit een database, zet die in een werkblad, en scramble je vervolgens om de datums er goed uit te laten zien en de kolommen te laten opvallen met de juiste kleuren.  

In deze tutorial lopen we een nette, end‑to‑end‑oplossing door die **datumopmaak instelt**, **celachtergrond zet**, **voorgrondkleur toepast**, en zelfs **een Excel‑kolom kleurt** tijdens het importeren van data. Aan het einde heb je een herbruikbaar patroon dat **excel import formatting** afhandelt zonder de gebruikelijke trial‑and‑error.

> **Wat je nodig hebt**  
> * .NET 6+ (of .NET Framework 4.7+)  
> * Aspose.Cells for .NET (gratis proefversie werkt voor testen)  
> * Een `DataTable`‑bron – elke ADO.NET‑query volstaat  
> * Visual Studio of je favoriete IDE  

Laten we beginnen.

---

## Overzicht van de Oplossing

We splitsen het probleem op in drie logische delen:

1. **Haal de brondata op** – een `DataTable` met de rijen die je wilt exporteren.  
2. **Maak kolomspecifieke stijlen** – één stijl voor de datumkolom, een andere voor een tekstkolom, plus eventuele extra opmaak die je wilt.  
3. **Importeer de tabel met stijlen** – gebruik `Worksheet.Cells.ImportDataTable` zodat elke kolom de stijl erft die je hebt voorbereid.

Waarom deze aanpak? Omdat Aspose.Cells je toestaat een `Style`‑array direct aan de `ImportDataTable`‑aanroep te koppelen, waardoor je geen tweede stap nodig hebt om de opmaak opnieuw toe te passen. Het is sneller, minder foutgevoelig en houdt je code netjes.

---

## Stap 1: Haal de Data op die je wilt Exporteren

Allereerst – je hebt een `DataTable` nodig. In een echt project roep je waarschijnlijk een stored procedure aan of gebruik je Entity Framework om deze te vullen, maar voor illustratie maken we een eenvoudige tabel met een datum‑ en een tekstkolom.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** Als je bron nullable datums gebruikt, zorg er dan voor dat het kolomtype `typeof(DateTime?)` is – Aspose respecteert later nog steeds het formaat dat je toewijst.

---

## Stap 2: Bereid een Array van Stijlen voor – Eén per Kolom

Nu maken we een `Style[]` waarvan de lengte overeenkomt met het aantal kolommen in de `DataTable`. Elke entry bevat de opmaak voor de respectieve kolom.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Datumopmaak instellen voor de eerste kolom

De eerste kolom (`OrderDate`) moet worden weergegeven als “MM/dd/yyyy”. Aspose gebruikt de ingebouwde getalopmaak‑index 14 voor de korte datum, maar je kunt ook een aangepaste opmaak‑string opgeven als je dat liever hebt.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Waarom dit belangrijk is:** Excel slaat datums op als seriële getallen. Door een getalopmaak toe te wijzen, vertel je Excel die seriële waarden weer te geven als mens‑leesbare datums in plaats van ruwe cijfers.

### 2.2 Celachtergrond instellen voor de tweede kolom

Laten we de `CustomerName`‑kolom een lichtblauwe achtergrond geven. Hier komt **set cell background** om de hoek kijken.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Opmerking:** Zonder `Pattern` op `Solid` te zetten, verschijnt de voorgrondkleur niet omdat het standaardpatroon “None” is.

### 2.3 Voorgrond‑ (tekst)kleur toepassen – Optionele Extra

Wil je ook dat de tekst zelf een contrasterende kleur heeft, dan kun je dezelfde stijl aanpassen:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Dat voldoet aan de **apply foreground color**‑vereiste terwijl de achtergrond van de kolom intact blijft.

---

## Stap 3: Importeer de DataTable met de Gedefinieerde Stijlen

Met de stijlen klaar, is de laatste stap één regel code die de data importeert en de stijlen kolom‑voor‑kolom toepast.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Hoe het werkt:** Aspose leest de `columnStyles`‑array en koppelt elke `Style` aan de overeenkomstige kolomindex. De header‑rij erft de standaardstijl tenzij je een aparte stijl voor rij 0 opgeeft.

### 3.1 Werkboek opslaan

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Voer het programma uit, open *FormattedReport.xlsx*, en je zou moeten zien:

- **OrderDate**‑kolom weergegeven als datums (bijv. `06/15/2026`).  
- **CustomerName**‑kolom met een lichtblauwe vulling en donkerblauwe tekst.  

Dat is de volledige **excel import formatting**‑workflow in minder dan 30 regels C#.

---

## Stap‑voor‑Stap Samenvatting (met Waarom)

| Stap | Wat je doet | Waarom het belangrijk is |
|------|-------------|--------------------------|
| **Data ophalen** | Roep `GetData()` aan om een `DataTable` te vullen. | Biedt een gestructureerde bron die Aspose direct kan inlezen. |
| **Stijl‑array maken** | Reserveer `Style[]` met dezelfde kolomtelling. | Maakt per‑kolom styling mogelijk in één import‑aanroep. |
| **Datumopmaak instellen** | `columnStyles[0].Number = 14;` | Zorgt dat datums correct worden weergegeven in Excel. |
| **Achtergrondkleur instellen** | `ForegroundColor = LightBlue; Pattern = Solid;` | Markeert de kolom, voldoet aan **set cell background**. |
| **Voorgrondkleur toepassen** | `Font.Color = DarkBlue;` | Verbetert leesbaarheid en voldoet aan **apply foreground color**. |
| **Importeren met stijlen** | `ImportDataTable(..., columnStyles);` | Eén‑pass import die alle opmaak respecteert. |
| **Werkboek opslaan** | `wb.Save(...);` | Slaat het resultaat op voor downstream gebruikers. |

---

## Edge Cases & Veelgestelde Vragen

### Wat als ik meer dan twee kolommen heb?

Breid gewoon de `columnStyles`‑array uit en wijs een `Style` toe aan elke index die je nodig hebt. Niet‑toegewezen indexen vallen terug op de standaardstijl, wat prima is.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Hoe format ik een kolom als valuta?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Kan ik de header‑rij stijl apart aanpassen?

Ja. Na de import kun je de eerste rij pakken en een aparte stijl toepassen:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Wat als de DataTable null‑datums bevat?

Aspose laat die cellen leeg. Als je liever een placeholder zoals “N/A” wilt, kun je de tabel vooraf verwerken:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Pas daarna de stijl aan om een aangepast formaat te tonen dat “N/A” weergeeft voor de sentinel‑waarde.

---

## Volledig Werkend Voorbeeld

Hieronder staat het complete, kant‑klaar programma. Voer het uit als console‑applicatie en je krijgt een mooi opgemaakt Excel‑bestand.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}