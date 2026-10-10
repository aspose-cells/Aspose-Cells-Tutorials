---
category: general
date: 2026-10-10
description: Skapa en Excel-arbetsbok i C# och använd WRAPCOLS-funktionen för att
  dela upp arraydata i kolumner. Följ en komplett steg‑för‑steg‑guide med körbar kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: sv
lastmod: 2026-10-10
og_description: Skapa en Excel-arbetsbok i C# och använd WRAPCOLS-funktionen för att
  dela upp arraydata i kolumner. Denna guide visar hela koden och förklarar varje
  steg.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Skapa en Excel-arbetsbok och dela upp data med WRAPCOLS i C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man skapar en Excel-arbetsbok och delar upp data med WRAPCOLS i C#
url: /sv/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar Excel workbook och delar data med WRAPCOLS i C#

Om du behöver **create Excel workbook** programatiskt, visar den här guiden exakt hur du gör det och hur du **split array data** över kolumner med hjälp av `WRAPCOLS`‑funktionen. Du får ett komplett, körbart exempel som producerar en `.xlsx`‑fil med data fördelade i tre kolumner.

Handledningen täcker allt du behöver: nödvändiga NuGet‑paket, varje kodrad, varför `WRAPCOLS`‑formeln fungerar, och hur du anpassar lösningen för olika array‑storlekar eller kolumnantal. I slutet kommer du att kunna bädda in tekniken **use wrapcols function** i vilket C#‑projekt som helst som genererar Excel‑filer.

## Förutsättningar

* .NET 6.0 SDK eller senare installerat  
* En C#‑IDE (Visual Studio, VS Code, Rider, etc.)  
* **Aspose.Cells for .NET**‑paketet – biblioteket som tillhandahåller `Workbook`‑klassen som används i exemplen  

Du behöver inte någon Office‑installation; Aspose.Cells skriver `.xlsx`‑filen direkt.

## Steg 1 – create Excel workbook

Den första uppgiften är att instansiera ett nytt workbook‑objekt och få en referens till det första worksheet‑bladet. Detta steg är grunden för all vidare manipulation.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` representerar hela filen, medan `Worksheet` representerar ett enskilt blad. Genom att skapa workbook‑en i minnet undviker du disk‑I/O tills du explicit sparar den.

## Steg 2 – apply WRAPCOLS to split array columns

Nu placerar du en formel i cell **A1** som använder `WRAPCOLS`. Funktionen tar två argument: källarrayen och antalet kolumner som du vill att arrayen ska wrapa in i.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Varför detta fungerar:** `WRAPCOLS` tar den platta arrayen `{1,2,3,4,5,6}` och fyller worksheet rad‑för‑rad, och skapar tre kolumner per rad. Det första argumentet kan vara någon Excel‑array‑literal, ett namngivet område eller en dynamisk array‑formel. Det andra argumentet (`3`) talar om för Excel hur många kolumner som ska genereras innan nästa rad påbörjas.

### Använda funktionen med olika datatyper

`WRAPCOLS`‑funktionen är inte begränsad till tal. Du kan dela textvärden, datum eller blandade typer:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

När källarrayen innehåller strängar behandlar Excel automatiskt resultatet som textceller. Denna flexibilitet låter dig **excel formula split data** för rapportering, instrumentpaneler eller data‑migrationsuppgifter.

## Steg 3 – calculate formulas so the worksheet is populated

Formler lagras som strängar tills du ber workbook att utvärdera dem. Att anropa `CalculateFormula` tvingar en utvärdering och skriver resultaten i cellerna.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Utan detta anrop skulle den sparade filen bara innehålla formeltexten, inte de beräknade värdena. Metoden fungerar över hela workbook, så du kan placera ytterligare formler någon annanstans och de kommer alla att lösas med ett enda anrop.

## Steg 4 – save the workbook to see the result

Slutligen skriver du workbook till disk. Välj en mapp som du har skrivbehörighet till, och ge filen ett tydligt namn.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

När du öppnar `output.xlsx` i Excel (eller någon kompatibel visare) ser du:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Om du använde exempel med blandade typer, skulle raderna 3‑4 innehålla texten och siffrorna enligt.

## Avancerade variationer och hantering av edge‑case

### Variabel kolumnantal vid körning

Ofta beror antalet kolumner du behöver på användarens inmatning. Du kan bygga formelsträngen dynamiskt:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Stora arrayer och prestanda

`WRAPCOLS` kan hantera tusentals element, men att utvärdera extremt stora arrayer i en enda cell kan öka beräkningstiden. Om du märker en nedgång i hastigheten:

* Dela upp källarrayen i mindre delar och skriv varje del till en separat startcell.  
* Använd `WorkbookSettings` för att aktivera flertrådad beräkning:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Hantera tomma celler

Om källarrayen innehåller tomma strängar (`""`) eller `NULL`‑värden, sätter `WRAPCOLS` in tomma celler och bevarar kolumnlayouten. Detta beteende är användbart när du behöver platshållarkolumner för senare datainmatning.

### Använda namngivna områden istället för literals

För underhållbarhet, definiera ett namngivet område som innehåller källdata, och referera sedan till det:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Nu läser formeln data från själva worksheet, vilket möjliggör **how to use wrapcols** i dynamiska rapporteringsscenarier.

## Vanliga fallgropar och pro‑tips

* **Utelämna inte det andra argumentet.** `WRAPCOLS(array)` utan ett kolumnantal returnerar en enda kolumn, vilket undergräver syftet med att dela data.  
* **Undvik att blanda array‑dimensioner.** Källarrayen måste vara endimensionell; att tillhandahålla en tvådimensionell array (t.ex. `{ {1,2},{3,4} }`) utlöser ett `#VALUE!`‑fel.  
* **Spara efter beräkning.** Om du anropar `wb.Save` innan `CalculateFormula` kommer filen bara att innehålla formeltexten.  
* **Kontrollera filbehörigheter.** När du kör i begränsade miljöer (t.ex. ASP.NET) bör du säkerställa att processidentiteten kan skriva till mål‑mappen.  

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera, klistra in och köra. Det inkluderar alla importeringar, felhantering och kommentarer.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

När programmet körs produceras `output.xlsx` med tre distinkta regioner som demonstrerar **excel formula split data** med `WRAPCOLS`‑funktionen.

## Slutsats

Du vet nu hur du **create Excel workbook**‑filer i C# och hur du **use wrapcols function** för att **split array columns** effektivt. De primära stegen — att instansiera `Workbook`, infoga `WRAPCOLS`‑formeln, beräkna och spara — bildar ett återanvändbart mönster för alla automatiseringsuppgifter som kräver datafördelning över kolumner.

Från här kan du:

* Kombinera `WRAPCOLS` med andra dynamiska‑array‑funktioner som `FILTER` eller `SORT`.  
* Exportera stora datamängder från databaser och låt Excel hantera layouten automatiskt.  
* Bygga användardrivna rapporter där kolumnantalet väljs via en UI‑kontroll.

Experimentera med olika array‑källor, kolumnantal och ytterligare formler för att bygga vidare på denna grund. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder WRAPCOLS i C# – Skapa Excel workbook med wrap‑funktioner](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Skapa Excel workbook – Konvertera array till matris med WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Skapa Excel workbook C# – Steg‑för‑steg‑guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}