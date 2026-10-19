---
category: general
date: 2026-09-24
description: Skapa en Excel‑arbetsbok programatiskt och lär dig hur du skapar flera
  detaljblad, för att sedan spara arbetsboken som en xlsx‑fil med ett tydligt C#‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: sv
lastmod: 2026-09-24
og_description: Skapa Excel-arbetsbok programatiskt, se hur du skapar flera detaljblad
  och sparar arbetsboken som en xlsx-fil i ett enda körbart exempel.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Skapa Excel‑arbetsbok programatiskt – fullständig C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Skapa Excel-arbetsbok programatiskt med Smart Markers
url: /sv/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel‑arbetsbok programatiskt med Smart Markers

Om du behöver **skapa Excel‑arbetsbok programatiskt**, visar den här guiden exakt hur du gör det med Aspose.Cells .NET. Du får också reda på **hur du skapar flera detaljblad** från en enda datakälla och slutligen **sparar arbetsboken som xlsx‑fil** utan några manuella steg.  

Lösningen är självständig: vi går igenom varje kodrad, förklarar varför varje inställning är viktig och tar upp vanliga fallgropar som duplicerade bladnamn. När du är klar har du en färdig konsolapplikation som producerar en arbetsbok med ett huvudblad och en uppsättning detaljblad.

## Vad du behöver

| Förutsättning | Orsak |
|--------------|--------|
| .NET 6.0 SDK eller senare | Tillhandahåller runtime för C#‑konsolappen |
| Aspose.Cells för .NET (NuGet‑paket `Aspose.Cells`) | Levererar klasserna `Workbook`, `SmartMarkerProcessor` och `SmartMarkerOptions` |
| En enkel datakälla (t.ex. `DataTable` eller en lista med objekt) | Tillhandahåller värdena som Smart Markers ska expandera |
| Visual Studio 2022 eller någon editor som stödjer .NET | Gör det enkelt att kompilera och köra koden |

> **Proffstips:** Installera Aspose.Cells‑paketet via CLI innan du börjar:  
> `dotnet add package Aspose.Cells`

## Steg 1: Skapa projektet och importera namnrymder

Skapa ett nytt konsolprojekt och ta in de nödvändiga namnrymderna.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Varför detta är viktigt*: `Aspose.Cells` hanterar arbetsbokens livscykel, medan `Aspose.Cells.SmartMarkers` ger dig den kraftfulla Smart Marker‑motorn som kan generera många blad från en enda mall.

## Steg 2: Skapa Excel‑arbetsboken programatiskt

Den första konkreta handlingen är att instansiera ett `Workbook`. Detta objekt representerar hela Excel‑filen i minnet.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Om du föredrar att börja från en mall som redan innehåller rubrikrader eller formatering, ersätt `new Workbook()` med `new Workbook("Template.xlsx")`. Resten av processen fungerar identiskt.

## Steg 3: Förbered en Smart Marker‑mall

Smart Markers arbetar på cellinnehåll som innehåller platshållare som `&=Employees.Name`. För den här tutorialen lägger vi till en enkel mall direkt via kod, men du kan också redigera bladet manuellt i Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Varför detta är viktigt*: Platshållaren `&=Employees.Name` talar om för Smart Marker‑processorn att iterera över samlingen `Employees`. Varje iteration kommer att skapa ett nytt kalkylblad eftersom vi konfigurerar processorn att skapa ett **detaljblad** för varje rad.

## Steg 4: Bygg en datakälla som innehåller flera rader

Vi använder en `DataTable` som ett snabbt sätt att simulera en samling med anställdas poster.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Du kan ersätta detta med vilken `IEnumerable` som helst (t.ex. `List<Employee>`) – Smart Markers accepterar alla datakällor som implementerar `IEnumerable`.

## Steg 5: Konfigurera Smart Marker‑alternativ – hur du skapar flera detaljblad

Som standard skriver Smart Markers data tillbaka till samma blad. För att generera **flera detaljblad** måste du sätta egenskapen `DetailSheetNewName`. Detta visar också **hur du skapar flera detaljblad** utan namnkonflikter.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Om datakällan innehåller duplicerade namn lägger processorn automatiskt till ett numeriskt suffix (t.ex. `Detail_1`, `Detail_2`). Detta förhindrar körfel och säkerställer att alla detaljblad sparas.

## Steg 6: Bearbeta Smart Markers

Nu anropar vi processorn och skickar med datakällan samt de alternativ vi just definierat.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Varför detta är viktigt*: Processorn läser platshållaren `&=Employees.Name`, itererar över varje rad i `employees`, skapar ett nytt blad kallat “Detail” och skriver radens data till det bladet. Det ursprungliga bladet förblir som en sammanfattning eller huvudblad.

## Steg 7: Spara arbetsboken som xlsx‑fil

Till sist sparar du arbetsboken till disk med **save workbook as xlsx file**‑mönstret.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Enum‑värdet `SaveFormat.Xlsx` garanterar att filen lagras i det moderna Office Open XML‑formatet, vilket är kompatibelt med Excel 2007+ och de flesta molntjänster.

## Fullt, körbart exempel

Kopiera följande kod till `Program.cs` i ett .NET‑konsolprojekt och kör det. Programmet genererar `detail.xlsx` i mappen `output`, med ett huvudblad och tre detaljblad (ett per anställd).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Förväntad output**

- `output/detail.xlsx` innehåller:
  - **Sheet1** – den ursprungliga mallen med rubriken “Employee Report”.
  - **Detail** – första detaljbladet med Alice‑posten.
  - **Detail_1** – andra detaljbladet med Bob‑posten.
  - **Detail_2** – tredje detaljbladet med Carol‑posten.

Öppna filen i Excel så ser du varje anställd på sitt eget blad, vilket bevisar att vi framgångsrikt **skapar flera detaljblad** och **sparar arbetsboken som xlsx‑fil**.

## Vanliga frågor & hantering av kantfall

| Fråga | Svar |
|----------|--------|
| *Vad gör jag om jag behöver ett eget namn för varje detaljblad?* | Sätt `DetailSheetNewName = "Employee_"` och inkludera en kolumn som heter `SheetName` i datakällan. Processorn lägger då till värdet från `SheetName` till basnamnet. |
| *Kan jag behålla det ursprungliga bladet som en sammanfattning av alla detaljer?* | Ja. Huvudbladet förblir orört; du kan lägga till formler som refererar till de genererade detaljbladen. |
| *Vad händer när datakällan är tom?* | Inga detaljblad skapas, men arbetsboken sparas ändå. Överväg att kontrollera `employees.Rows.Count` innan bearbetning om du behöver speciell hantering. |
| *Är det möjligt att använda en befintlig mallfil?* | Ersätt `new Workbook()` med `new Workbook("Template.xlsx")`. All Smart Marker‑logik fungerar på samma sätt. |

## Slutsats

Du vet nu **hur du skapar Excel‑arbetsbok programatiskt**, hur du **skapar flera detaljblad** med Smart Markers, och hur du **sparar arbetsboken som xlsx‑fil** med Aspose.Cells. Det kompletta exemplet kan anpassas för fakturor, rapporter eller vilket scenario som helst där en master‑detail‑Excel‑utmatning krävs.

### Nästa steg

- Utforska andra Smart Marker‑funktioner såsom **group markers** och **conditional formatting**.
- Ersätt `DataTable` med en riktig databasfråga för att generera storskaliga rapporter.
- Använd `Workbook.Save("output.pdf", SaveFormat.Pdf)` för att exportera samma data till PDF för distribution.

Känn dig fri att experimentera med olika namngivningsscheman, styling eller extra kalkylblad – dina nya färdigheter för programmatisk Excel‑generering är redo för produktionsbruk. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}