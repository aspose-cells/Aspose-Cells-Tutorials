---
category: general
date: 2026-10-01
description: Lär dig hur du skapar en Excel‑arbetsbok i C# och tillämpar anpassat
  talformat, ställer in cellernas decimaler och sparar arbetsboken som XLSX i en komplett
  steg‑för‑steg‑guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: sv
lastmod: 2026-10-01
og_description: Skapa en Excel‑arbetsbok i C# med anpassat talformat, ställ in cellens
  decimaler och spara arbetsboken som XLSX. Följ den här kompletta guiden för exakt
  numerisk utskrift.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Skapa Excel‑arbetsbok C# – anpassat talformat och XLSX‑export
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man skapar en Excel‑arbetsbok i C# med anpassad talformatering
url: /sv/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar Excel-arbetsbok C# med anpassad talformattering

Om du behöver **create excel workbook c#** som visar siffror exakt som du vill, visar den här guiden hur du gör det i några tydliga steg. Du kommer att lära dig att tillämpa ett anpassat talformat, ange cellers decimalplatser och slutligen **save workbook as xlsx** för vidare användning.

Att arbeta med numerisk data innebär ofta en avvägning mellan precision och läsbarhet. I slutet av den här handledningen har du ett återanvändbart mönster som begränsar visade siffror till ett specifikt antal signifikanta siffror samtidigt som det ursprungliga värdet bevaras i filen. Inga externa skript krävs – bara C# och Aspose.Cells‑biblioteket.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon C#‑IDE)  
* **Aspose.Cells for .NET** NuGet‑paketet (`Install-Package Aspose.Cells`) – detta bibliotek tillhandahåller klasserna `Workbook`, `Worksheet` och `ExportTableOptions` som används i exemplen.  

Dessa krav är minimala; samma kod fungerar i .NET Core, .NET Framework och även i Azure Functions.

## Steg 1: Skapa Excel-arbetsbok C# – initiera filen

Den första operationen är att instansiera ett nytt `Workbook`‑objekt. Detta objekt representerar hela Excel‑filen i minnet och innehåller automatiskt ett standard‑worksheet.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Varför detta är viktigt:**  
Att skapa arbetsboken i förväg ger dig en ren canvas. Standard‑worksheetet (`Worksheets[0]`) är redo för datainmatning, så du behöver inte lägga till ett nytt blad om ditt scenario inte kräver flera flikar.

## Steg 2: Skriv ett numeriskt värde till en cell

Sätt nu in ett exempelnummer i cell **A1**. Värdet vi använder (`123.456789`) innehåller fler decimaler än vi så småningom vill visa, vilket låter oss demonstrera avrundning senare.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tips:** `PutValue` upptäcker automatiskt datatypen, så du behöver inte konvertera talet till en sträng.

## Steg 3: Tillämpa anpassat talformat – begränsa synliga decimaler

För att styra hur Excel visar talet skapar vi ett `Style` med ett **custom number format**. Mönstret `"0.######"` säger åt Excel att visa upp till sex decimaler men utelämna efterföljande nollor.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Hur detta fungerar:**  
Formatsträngen följer Excels anpassade format‑syntax. `0` tvingar en siffra, medan `#` visar en siffra endast om den är signifikant. Genom att kombinera dem får du en flexibel visning som fortfarande respekterar den ursprungliga precisionen.

## Steg 4: Ange cellers decimalplatser – med ExportTableOptions

Om du behöver **set cell decimal places** för exporterad data (t.ex. vid konvertering till en DataTable) låter Aspose.Cells dig specificera antalet **significant digits**. Detta steg säkerställer att den exporterade CSV‑ eller DataTable‑filen följer samma avrundningsregler som du använde i arbetsboken.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Varför använda `SignificantDigits`?**  
Till skillnad från ett fast antal decimaler bevarar signifikanta siffror talets storleksordning samtidigt som precisionen begränsas, vilket ofta är vad analytiker förväntar sig när de sammanfattar data.

## Steg 5: Exportera worksheet‑data och **save workbook as xlsx**

Till sist exporterar du data (om du behöver en DataTable) och sparar arbetsboken på disk. Anropet `ExportDataTable` respekterar de `ExportTableOptions` vi konfigurerat, och `workbook.Save` skriver en standard‑XLSX‑fil.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Förväntat resultat:**  
När du öppnar *SigDigits.xlsx* i Excel visar cell **A1** `123.5`. Det underliggande värdet förblir `123.456789`, men det visade talet följer regeln med 4 signifikanta siffror. Om du exporterar bladet till en DataTable kommer värdet i tabellen också att avrundas till `123.5`.

---

## Tillämpa anpassat talformat på ytterligare celler

Om du behöver formatera ett område snarare än en enskild cell, återanvänd `Style`‑objektet:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Proffstips:** Återanvändning av ett stil‑objekt minskar minnesbelastningen och garanterar konsekvent formatering över hela bladet.

## Hur man formaterar tal i Excel med C# – vanliga variationer

| Scenario | Formatsträng | Resultat |
|----------|--------------|----------|
| Fast två decimaler | `"0.00"` | `123.46` |
| Valuta (US) | `"$#,##0.00"` | `$123.46` |
| Procent med en decimal | `"0.0%"` | `12,346.0%` |
| Vetenskaplig notation | `"0.00E+00"` | `1.23E+02` |

Välj det mönster som matchar dina rapporteringskrav. Alla mönster är kompatibla med `Style.Custom`‑egenskapen som demonstrerades tidigare.

## Ange cellers decimalplatser dynamiskt baserat på användarinmatning

Ibland är den erforderliga precisionen inte känd vid kompileringstid. Du kan bygga formatsträngen vid körning:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Särskilt fall:** Om `decimals` är noll blir formatet `"0"` (heltal). Validera alltid användarinmatningen för att undvika felaktiga formatsträngar.

## Spara arbetsbok som XLSX – bästa praxis

* **Använd absoluta sökvägar** när du skriver till en känd katalog (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** `Workbook` om du omsluter den i ett `using`‑statement för att snabbt frigöra ohanterade resurser:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Versionskompatibilitet:** Aspose.Cells skriver filer som är kompatibla med Excel 2010‑2023, så downstream‑användare stöter inte på formatproblem.

---

## Fullständigt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera, klistra in och köra omedelbart. Det inkluderar alla nödvändiga `using`‑direktiv, kommentarer och felhantering.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verifieringssteg**

1. Kör programmet (`dotnet run`).  
2. Öppna `SigDigits.xlsx`.  
3. Bekräfta att **A1** visar `123.5`.  
4. Om du öppnar filens XML (`.xlsx` är ett zip‑arkiv) ser du det anpassade formatet `"0.######"` lagrat i `<c>`‑elementets `s`‑attribut.

---

## Slutsats

I den här handledningen har du lärt dig hur du **create excel workbook c#**, **apply custom number format**, **set cell decimal places** och **save workbook as xlsx** med Aspose.Cells. Lösningen demonstrerar både visuell formatering i Excel och data‑exportavrundning via `ExportTableOptions`.  

Härifrån kan du:

* Utöka tillvägagångssättet till hela områden eller tabeller.  
* Kombinera flera stilar (typsnitt, kanter) med `StyleFlag`.  
* Automatisera rapportgenerering genom att loopa över datakällor och applicera samma formateringslogik.  

Känn dig fri att experimentera med olika formatsträngar, decimalantal eller exportalternativ för att matcha dina specifika rapporteringsbehov. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}