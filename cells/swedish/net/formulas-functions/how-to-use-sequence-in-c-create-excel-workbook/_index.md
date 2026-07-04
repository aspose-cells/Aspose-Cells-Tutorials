---
category: general
date: 2026-07-03
description: Hur man använder SEQUENCE i C# för att generera inkrementella tal i Excel.
  Lär dig skapa en Excel-arbetsbok i C# och ASP.NET och skapa en Excel-fil med några
  få kodrader.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: sv
og_description: Hur man använder SEQUENCE i C# för att generera inkrementella tal
  i Excel. Steg‑för‑steg‑guide för att skapa Excel‑arbetsbok med C# och ASP.NET för
  att skapa en Excel‑fil.
og_title: Hur man använder SEQUENCE i C# – Skapa Excel-arbetsbok
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Hur man använder SEQUENCE i C# – Skapa en Excel‑arbetsbok
url: /sv/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du SEQUENCE i C# – Skapa Excel-arbetsbok

Har du någonsin undrat **how to use SEQUENCE** för att spåna ut en lista med siffror i ett Excel‑blad från C#? Du är inte ensam. Oavsett om du bygger en rapporteringsdashboard, matar ett data‑grid, eller bara behöver ett snabbt sätt att generera ID:n, så sparar detta knep dig från att trassla med loopar.

I den här handledningen kommer vi att **create an Excel workbook in C#**, lägga in en `SEQUENCE` dynamisk‑array‑formel i cell A1, och sluta med en fin kolumn med inkrementella siffror. Vi kommer också att se hur man levererar den filen från en ASP.NET‑controller—ja, **ASP.NET create Excel file** behandlas också. I slutet kommer du att kunna **generate incremental numbers Excel**‑style med en enda kodrad.

## Vad du behöver

- .NET 6+ (koden fungerar även på .NET Framework 4.6+)  
- **Aspose.Cells for .NET** NuGet‑paketet (eller vilket bibliotek som helst som exponerar `Workbook`/`Worksheet`‑objekt)  
- Ett grundläggande ASP.NET Core‑ eller MVC‑projekt om du vill prova webb‑nedladdningsdelen  

Det är allt. Ingen extra COM‑interop, ingen Office‑installation krävs.

## Så använder du SEQUENCE för att generera inkrementella siffror

Excel‑funktionen `SEQUENCE(rows, [columns], [start], [step])` returnerar ett **spill**‑område. I vårt fall vill vi ha 5 rader, 1 kolumn, starta vid 10, steg 2. Formeln ser ut så här:

```excel
=SEQUENCE(5,1,10,2)
```

När Excel utvärderar den kommer cellerna A1:A5 att innehålla **10, 12, 14, 16, 18**. Det fina är att vi inte behöver skriva några C#‑loopar—formeln gör det tunga arbetet.

Nedan är den kompletta C#‑snutten som skapar en arbetsbok, infogar formeln, tvingar beräkning och sparar filen.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Förväntat resultat** – öppna *DynamicArray.xlsx* så ser du:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Det är hela **how to use sequence**‑historien i C#. Enkelt, eller? Men låt oss gräva lite djupare.

### Varför använda SEQUENCE istället för en loop?

- **Performance** – Excel gör beräkningarna i sin egen motor, som är starkt optimerad.
- **Maintainability** – Formeln är själv‑dokumenterande; vem som helst som öppnar bladet förstår omedelbart avsikten.
- **Dynamic resizing** – Ändra `rows`‑argumentet så expanderar spill‑området automatiskt.

## Skapa Excel‑arbetsbok C# – Steg för steg

Om du är ny på **create excel workbook c#**, så hjälper följande checklista dig att undvika vanliga fallgropar.

1. **Add the Aspose.Cells package**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Du kan också använda ClosedXML eller EPPlus, men det API som visas matchar koden ovan.)

2. **Set a license** (optional for trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instantiate `Workbook`** – detta ger dig en ny, tom arbetsbok.

4. **Reference the worksheet** – `workbook.Worksheets[0]` är standardbladet med namnet *Sheet1*.

5. **Apply the SEQUENCE formula** – som visat tidigare.

6. **Calculate** – `workbook.CalculateFormula()` tvingar spill; annars skulle filen bara innehålla formeln.

7. **Save** – du kan skriva till disk, en `MemoryStream`, eller direkt till ett HTTP‑svar.

### Proffstips

Om du behöver arbetsboken i minnet (t.ex. för att skicka den via ett webb‑API), använd en `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

## ASP.NET skapa Excel‑fil – Strömning till webbläsaren

Nu när vi vet **create excel workbook c#**, låt oss integrera det i en ASP.NET Core‑controller så att användare kan ladda ner filen i farten.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

När en användare går till `/api/excel/download` visar webbläsaren en nedladdningsprompt för *DynamicArray.xlsx*. Filen innehåller redan kolumnen med **generated incremental numbers excel** tack vare `SEQUENCE`‑formeln.

### Vad händer om klienten använder en äldre Excel‑version?

Dynamiska arrayer (inklusive `SEQUENCE`) introducerades i Excel 365/2019. Om du behöver bakåtkompatibilitet, gå tillbaka till en manuell fyllning:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Det där kodsnutten visar den klassiska **generate incremental numbers excel**‑metoden utan att förlita sig på den nya funktionen.

## Vanliga frågor & specialfall

- **Do I need to enable iterative calculation?**  
  Nej. `SEQUENCE` är en icke‑iterativ funktion; ett enkelt anrop av `CalculateFormula()` räcker.

- **What if I want a horizontal spill?**  
  Ändra det andra argumentet: `=SEQUENCE(1,5,10,2)` spillar över B1:F1.

- **Can I combine SEQUENCE with other functions?**  
  Absolut. Till exempel kan `=INDEX(A:A, SEQUENCE(5,1,10,2))` hämta rader från en annan kolumn.

- **Is the workbook size a concern?**  
  Påverkan på filstorleken från en formel är försumbar. Endast när du börjar fylla i miljontals celler manuellt blir storleken ett problem.

## Slutsats

Vi har gått igenom **how to use sequence** i C# för att **create excel workbook c#**, levererat den arbetsboken via **ASP.NET create excel file**, och demonstrerat ett rent sätt att **generate incremental numbers excel** utan att skriva några loopar. Huvudpoängen: låt Excels egna dynamiska‑array‑motor göra räkningen, och låt din .NET‑kod fokusera på orkestreringen.

Känn dig fri att experimentera—byt ut `rows`, `start` eller `step`‑argumenten, spill horisontellt, eller kombinera formeln med `IF` eller `FILTER` för mer avancerade rapporter. När du är redo, prova att kedja flera blad tillsammans eller exportera arbetsboken som CSV för downstream‑system.

Har du ett eget knep du vill dela? Lägg en kommentar nedan, eller kontakta mig på GitHub. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar och konfigurerar Excel‑arbetsböcker med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hur man skapar och sparar Excel‑filer med Aspose.Cells för .NET: En komplett guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Hur man skapar och formaterar Excel‑arbetsböcker med Aspose.Cells för .NET (2023‑guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}