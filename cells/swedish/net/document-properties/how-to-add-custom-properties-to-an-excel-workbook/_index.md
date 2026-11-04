---
category: general
date: 2026-10-01
description: Lär dig hur du lägger till anpassade egenskaper i en Excel‑arbetsbok
  med Aspose.Cells. Den här guiden visar också hur du lägger till projekt‑ID och läser
  anpassade egenskaper.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: sv
lastmod: 2026-10-01
og_description: Lägg till anpassade egenskaper i en Excel-arbetsbok med Aspose.Cells.
  Följ den här kompletta handledningen för att lägga till ett projekt‑ID, ange granskareinformation
  och läsa anpassade egenskaper programmässigt.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Lägg till anpassade egenskaper i Excel‑arbetsbok – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man lägger till anpassade egenskaper i en Excel‑arbetsbok
url: /sv/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till anpassade egenskaper i en Excel-arbetsbok

Om du behöver **lägga till anpassade egenskaper** i en Excel-arbetsbok, visar den här guiden exakt hur du gör det med Aspose.Cells för .NET. Du kommer också att lära dig hur du lägger till ett projekt‑ID, anger ett granskarnamn och senare **läser anpassade egenskaper** från filen.

Att arbeta med anpassad metadata låter dig bädda in affärsspecifik information direkt i kalkylbladet, vilket gör det enkelt att spåra ägarskap, version eller annan kontext utan att underhålla en separat databas. Stegen nedan täcker hela arbetsflödet från att skapa arbetsboken till att spara de nya egenskaperna.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare installerat  
* En giltig Aspose.Cells för .NET‑licens (eller en gratis provversion)  
* Visual Studio 2022 (eller någon C#‑IDE)  

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Cells`.

## Steg 1: Ställ in projektet och importera namnrymder

Skapa ett nytt konsolprogram och lägg till Aspose.Cells‑referensen:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

`Aspose.Cells`‑namnrymden innehåller klasserna `Workbook`, `Worksheet` och `CustomPropertyCollection` som vi kommer att använda.

## Steg 2: Läs in en befintlig arbetsbok (eller skapa en ny)

Du kan börja med en befintlig `.xlsb`‑fil eller generera en ny arbetsbok. Exemplet nedan läser in en fil med namnet **Data.xlsb** som ligger i en mapp som heter `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Om filen inte finns, ersätt koden med `new Workbook();` för att skapa en tom arbetsbok.

## Steg 3: Lägg till anpassade egenskaper i det första kalkylbladet

Den primära operationen är att **lägga till anpassade egenskaper** i ett kalkylblad. Aspose.Cells lagrar anpassade egenskaper i en samling som beter sig som en ordbok.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Anledningen till att vi använder `CustomProperties.Add` istället för `CustomProperties["Name"] = value` är att `Add`‑metoden skapar posten om den inte finns och garanterar att rätt datatyp lagras. Detta förhindrar oavsiktliga typkonflikter som kan orsaka körfel när värdena läses senare.

## Steg 4: Spara arbetsboken med de nya egenskaperna

Efter att du har injicerat metadata, skriv ändringarna till en ny fil så att originalet förblir orört.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Vid detta tillfälle innehåller Excel‑filen den anpassade metadata du definierade. Du kan verifiera egenskaperna med stegen i nästa avsnitt.

## Steg 5: Läs anpassade egenskaper från en arbetsbok

Att läsa **excel custom properties** följer samma samlingsmönster. Detta kodsnutt demonstrerar hur du hämtar de värden vi just lagrade.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection`‑indexeraren returnerar ett `CustomProperty`‑objekt; genom att komma åt dess `Value`‑egenskap får du den lagrade datan i dess ursprungliga typ. Att kontrollera `null` innan du castar undviker `NullReferenceException` om en egenskap saknas.

### Förväntad konsolutskrift

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Tidsstämpeln kommer att spegla exakt det ögonblick du anropade `Add` i steg 3.

## Proffstips: Uppdatera en befintlig anpassad egenskap

Om du senare behöver **lägga till anpassad** information (t.ex. ändra granskaren), använd `CustomPropertyCollection`‑setter:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Detta mönster säkerställer att egenskapen antingen uppdateras eller skapas, vilket är användbart i iterativa arbetsflöden såsom automatiserad rapportgenerering.

## Steg 6: Verifiera egenskaperna i Excel (valfritt)

Du kan också visa de anpassade egenskaperna direkt i Excel:

1. Öppna den sparade filen `DataWithProps.xlsb` i Microsoft Excel.  
2. Gå till **File → Info → Properties → Advanced Properties**.  
3. Välj fliken **Custom**.  

Du kommer att se posterna `ProjectId`, `Reviewer` och `CreatedOn` listade med sina respektive värden.

## Fullständigt fungerande exempel

Nedan är det kompletta, självständiga programmet som kombinerar alla tidigare kodsnuttar. Kopiera det till `Program.cs` och kör det; konsolen kommer att visa de hämtade värdena.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

När du kör programmet får du konsolutskriften som visades tidigare och skapar `DataWithProps.xlsb` som innehåller den inbäddade metadata.

## Vanliga frågor och edge‑cases

| Question | Answer |
|---|---|
| **Can I store non‑primitive types?** | Aspose.Cells supports `string`, `int`, `double`, `DateTime`, and `bool`. For complex objects, serialize them to JSON or XML first and store the string. |
| **What if the workbook is password‑protected?** | Open the workbook with a password (`new Workbook(path, password)`) before accessing `CustomProperties`. The properties are still accessible after decryption. |
| **Do custom properties survive format conversion?** | When saving to a different format (e.g., `.xlsx`), Aspose.Cells preserves custom properties as long as the target format supports them. |
| **How to delete a custom property?** | Use `worksheet.CustomProperties.Remove("PropertyName");`. This removes the entry from the collection. |

## Nästa steg

Nu när du vet hur du **lägger till anpassade egenskaper**, kan du utforska relaterade ämnen såsom:

* **excel custom properties** för dokumentversionering  
* **read custom properties** från flera kalkylblad i en enda arbetsbok  
* Använda **Aspose.Cells** för att skapa pivottabeller som refererar till anpassad metadata  
* Exportera arbetsboken till PDF samtidigt som anpassade egenskaper bevaras  

Experimentera med olika datatyper, kombinera anpassade egenskaper med cellkommentarer, eller integrera metadata i ett större dokumenthanteringssystem.

---

**Redo att automatisera din Excel‑rapportering?** Lägg till koden ovan i ditt projekt, justera egenskapsnamnen så de matchar dina affärsbehov, så har du ett självbeskrivande kalkylblad redo för vidare bearbetning.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel‑arbetsbok – Lägg till anpassade egenskaper och spara som XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Hur man får åtkomst till anpassade dokumentegenskaper i Excel med Aspose.Cells för .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Behärska Excel‑anpassade egenskaper med Aspose.Cells .NET för förbättrad datamanagement](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}