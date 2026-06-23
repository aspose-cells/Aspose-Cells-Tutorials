---
category: general
date: 2026-06-05
description: Skapa Excel‑arbetsbok i C# snabbt och lär dig hur du ställer in cellens
  talformat, exporterar Excel‑cell och konverterar cellvärdet till en sträng med två
  decimalers precision.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: sv
og_description: Skapa en Excel-arbetsbok i C# och behärska att ställa in cellens talformat,
  exportera en Excel-cell som en sträng och formatera tal med två decimaler.
og_title: Skapa Excel‑arbetsbok i C# – Fullständig steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Skapa Excel-arbetsbok i C# – Komplett programmeringsguide
url: /sv/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i C# – Komplett programmeringsguide

Har du någonsin funderat på hur man **create Excel workbook** i C# utan att kämpa med COM-interoperabilitet eller röriga CSV‑trick? Du är inte ensam. Många utvecklare behöver ett rent, .NET‑native sätt att skapa en .xlsx‑fil, stoppa in ett tal i en cell och sedan exportera det värdet som en snyggt formaterad sträng.  

I den här handledningen går vi igenom precis det—vi börjar med en tom arbetsbok, ställer in cellens talformat, formaterar talet med två decimaler och lär oss slutligen **how to export Excel cell** data som en sträng. I slutet kommer du också att se hur man **convert cell value to string** utan att förlora precision.

> **Pro tip:** Metoden nedan använder **Aspose.Cells for .NET**‑biblioteket, som är ett beprövat, kommersiellt API. Om du söker ett gratisalternativ fungerar EPPlus eller ClosedXML på liknande sätt, men kodsnuttarna kommer att skilja sig något.

## Förutsättningar

- .NET 6.0 SDK (eller någon nyare .NET‑version) installerad.
- Visual Studio 2022 eller VS Code med C#‑tillägget.
- NuGet‑paketet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Inga andra beroenden krävs—allt annat finns i biblioteket.

## Steg 1: Installera Aspose.Cells och konfigurera projektet

Öppna din terminal (eller Package Manager Console) och kör:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Detta skapar en ny konsolapp med namnet `ExcelDemo` och hämtar `Aspose.Cells`‑assemblyn.  

Varför detta steg är viktigt: utan biblioteket kan du inte **create Excel workbook**‑objekt eller manipulera celler på ett typ‑säkert sätt.

## Steg 2: Skapa arbetsboken och hämta det första kalkylbladet

Öppna nu `Program.cs` och ersätt standardkoden med kodsnutten nedan. Den visar det allra första du gör när du **create Excel workbook**—instansierar `Workbook`‑klassen och får en referens till standardbladet.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Varför?** `Workbook`‑objektet är den minnesbaserade representationen av en Excel‑fil. Som standard innehåller det ett kalkylblad, som vi får åtkomst till via indexet som börjar på noll.

## Steg 3: Sätt ett numeriskt värde i en specifik cell

Låt oss rikta in oss på rad 5, kolumn 2 (indexering från noll) och infoga ett decimaltal. Detta demonstrerar **format number with two decimals** senare.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

`PutValue`‑metoden lagrar det råa double‑värdet. Vid detta tillfälle skulle Excel visa hela precisionen om vi inte applicerar ett format.

## Steg 4: Ställ in cellens talformat (två decimaler)

Här är där vi **set cell number format**. Vi använder `Style`‑objektet för att definiera ett anpassat talformat `"0.00"`—exakt två decimaler.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Varför använda en stil istället för strängkonvertering? Att behålla cellen som en numerisk typ bevarar dess beräkningsbara natur (du kan fortfarande summera, medelvärdesberäkna osv.) samtidigt som du visar exakt det du behöver.

## Steg 5: Exportera cellvärdet som en formaterad sträng

Ibland behöver du **how to export excel cell**‑värdet som ren text—kanske för att skriva in det i en loggfil eller skicka det via ett webb‑API. Aspose.Cells låter dig bifoga exportalternativ till en cell, vilket instruerar biblioteket att rendera värdet som en sträng med samma talformat.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## Steg 6: Hämta den formaterade strängen (Convert Cell Value to String)

Låt oss faktiskt utföra exporten och se resultatet. `ExportString`‑metoden returnerar cellens innehåll som en sträng, med tillämpning av eventuella `ExportTableOptions` som vi bifogade.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

När du kör programmet skriver konsolen ut:

```
Formatted cell value: 12345.68
```

Observera avrundningen från `12345.6789` till `12345.68`—det är effekten av **format number with two decimals**.

## Steg 7: (Valfritt) Spara arbetsboken på disk

Om du också vill se resultatet i en faktisk `.xlsx`‑fil, anropa bara `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

När du öppnar `DemoWorkbook.xlsx` visas samma tal i cell **C6**, formaterat med två decimaler.

## Kantfall & Vanliga frågor

### Vad händer om cellen redan har en stil?

`GetStyle`‑metoden returnerar en kopia av den befintliga stilen, så tidigare formatering (teckensnitt, färg osv.) behålls. Du skriver bara över `Custom`‑egenskapen, medan allt annat lämnas orört.

### Hur påverkar kultur decimalavgränsaren?

Aspose.Cells respekterar trådens `CultureInfo`. Om du behöver ett kommatecken istället för en punkt, ställ in:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Samma `"0.00"`‑format kommer nu att rendera `12 345,68`.

### Kan jag exportera ett cellområde på en gång?

Ja—använd `Worksheet.ExportDataTable` eller `Worksheet.ExportString` med ett område‑adress. `ExportTableOptions` som du definierade för en enskild cell kan återanvändas för hela området.

### Vad händer om jag inte vill att värdet avrundas utan trunkeras?

Ändra det anpassade formatet till `"0.00"` med en avrundningsmetod, eller trunkera manuellt innan du sätter värdet:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Fullständigt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Förväntad konsolutskrift**

```
Formatted cell value: 12345.68
```

Öppna `DemoWorkbook.xlsx` → gå till cell **C6** → du kommer att se samma tal med två decimaler.

## Slutsats

Vi har precis gått igenom allt du behöver för att **create Excel workbook** i C#, **set cell number format**, **format number with two decimals**, förstå **how to export Excel cell**‑data, och **convert cell value to string** för vidare bearbetning.  

De viktigaste slutsatserna är:

1. Använd `Workbook` och `Worksheet` för att skapa en Excel‑fil i minnet.  
2. Applicera en anpassad stil (`"0.00"`) för att tvinga två‑decimalers visning.  
3. Bifoga `ExportTableOptions` till en cell när du behöver en strängrepresentation som respekterar samma format.  

Härifrån kan du experimentera—lägga till fler celler, använda villkorsstyrd formatering eller till och med generera diagram. Om du är nyfiken på att formatera teckensnitt eller lägga till formler, kolla in Aspose.Cells‑dokumentationen om **cell styling** och **formula evaluation**.

Har du fler frågor om Excel‑automatisering i C#? Lämna en kommentar, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska arbetsboksoperationer i Aspose.Cells .NET: Ladda Excel‑filer och spåra cell‑föregångare effektivt](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Behärska Excel‑cellformatering och arbetsbokshantering med Aspose.Cells för .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Behärska Aspose.Cells för .NET: Avancerad Excel‑arbetsbok och cellhantering](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}