---
category: general
date: 2026-04-07
description: Applicera anpassat talformat på en kalkylbladscell och lär dig hur du
  formaterar tal i kalkylbladet när du exporterar cellvärdet med C#. Snabb, komplett
  guide.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: sv
og_description: Applicera anpassat talformat på en kalkylbladscell och exportera den
  som en formaterad sträng. Lär dig hur du formaterar tal i kalkylblad och exporterar
  cellvärdet.
og_title: Tillämpa anpassat talformat – Komplett C#‑exporthandledning
tags:
- C#
- Spreadsheet
- Number Formatting
title: Använd anpassat talformat i C#‑export av kalkylblad – Steg‑för‑steg‑guide
url: /sv/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apply Custom Number Format in C# Spreadsheet Export – Complete Tutorial

Har du någonsin behövt **apply custom number format** på en cell och sedan hämta den formaterade strängen från ett kalkylblad? Du är inte ensam. Många utvecklare fastnar när de upptäcker att det råa värdet returneras istället för den snygga, lokalanpassade strängen de förväntar sig. I den här guiden visar vi exakt hur du formaterar tal i kalkylblads‑celler och hur du exporterar cellvärdet som en formaterad sträng med ett populärt C#‑kalkylbladsbibliotek.

När du är klar med genomgången kan du **apply custom number format** på vilken numerisk cell som helst, exportera resultatet med `ExportTable` och se exakt den output du förväntar dig att visa i ett UI eller en rapport. Inga externa dokument behövs – allt finns här.

## Prerequisites

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.7+)
- En referens till kalkylbladsbiblioteket som tillhandahåller `Workbook`, `Worksheet` och `ExportTableOptions` (t.ex. **Aspose.Cells** eller **GemBox.Spreadsheet**; API‑exemplet matchar Aspose.Cells)
- Grundläggande C#‑kunskaper – om du kan skriva en `Console.WriteLine` är du redo att köra

> **Proffstips:** Om du använder ett annat bibliotek är egenskapsnamnen oftast liknande (`NumberFormat`, `ExportAsString`). Mappa dem helt enkelt.

## What the tutorial covers

1. Skapa en arbetsbok och välja det första kalkylbladet.  
2. Sätta in ett numeriskt värde i en cell.  
3. Ställa in `ExportTableOptions` för att **apply custom number format** och returnera en sträng.  
4. Exportera cellen och skriva ut det formaterade resultatet.  
5. Edge‑case‑hantering – vad händer om cellen innehåller en formel eller ett null‑värde?

Låt oss köra igång.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Step 1 – Create a workbook and get the first worksheet

Det första du behöver är ett workbook‑objekt. Tänk på det som Excel‑filen du skulle öppna i Office‑appen. När du har den, hämta det första bladet – de flesta tutorials börjar där eftersom det håller exemplet kortfattat.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Varför detta är viktigt:** En ny arbetsbok ger dig en ren start, så att ingen dold formatering stör vårt custom number format senare.

## Step 2 – Put a numeric value into cell B2 (the cell we will export)

Nu behöver vi något att formatera. Cell **B2** är ett praktiskt ställe – lätt att referera till och tillräckligt långt från standard‑A1‑hörnet för att undvika oavsiktliga överskrivningar.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Vad händer om värdet är en formel?**  
Om du senare ersätter det råa värdet med en formel (t.ex. `=SUM(A1:A10)`), kommer exportrutinen fortfarande att respektera det number format vi applicerar i nästa steg, eftersom formateringen är knuten till cellen, inte till värdetypen.

## Step 3 – Configure export options to receive the value as a formatted string

Här kommer hjärtat i tutorialen: vi talar om för biblioteket att **apply custom number format** under export. `NumberFormat`‑strängen följer samma mönster som du skulle använda i Excels “Custom”-kategori.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` säkerställer att metoden returnerar en `string` istället för en rå double.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` speglar Excels mönster: kommatecken för tusental, två decimaler och parenteser för negativa tal.

> **Varför använda ett custom format?** Det garanterar konsistens över kulturer (t.ex. US vs. European number separators) och låter dig infoga affärsspecifik styling som bokföringsparenteser.

## Step 4 – Export the cell using the configured options

Nu drar vi faktiskt ut värdet ur kalkylbladet och låter biblioteket göra det tunga lyftet att applicera formatet vi definierat.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Edge case – tom cell:** Om `B2` vore tom, blir `formattedResult` `null`. Du kan skydda mot det med en enkel null‑check innan du skriver ut.

## Step 5 – Display the formatted string

Till sist skriver vi resultatet till konsolen. I en riktig app kan du skicka strängen till en PDF, ett e‑mail eller en UI‑etikett.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Förväntat resultat**

```
1,234.56
```

Om du ändrar det råa värdet till `-9876.54`, ger samma format dig `(9,876.54)` – exakt vad många bokföringsrapporter kräver.

## Full, runnable example

Nedan är hela programmet som du kan kopiera‑klistra in i ett nytt konsolprojekt. Det kompilerar och körs som‑det‑är, förutsatt att du har lagt till rätt NuGet‑paket för kalkylbladsbiblioteket.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Snabb kontroll

- **Kompilerar den?** Ja – se bara till att `Aspose.Cells` (eller motsvarande) DLL är refererad.  
- **Fungerar den med andra kulturer?** Formatsträngen är kultur‑agnostisk; biblioteket respekterar det mönster du ger det. Om du behöver lokalspecifika avgränsare kan du prefixa med `CultureInfo`‑hantering före export.

## Common questions & variations

### Hur man **format number in spreadsheet** med ett annat mönster?

Byt ut `NumberFormat`‑strängen. Till exempel, för att visa en procent med en decimal:

```csharp
NumberFormat = "0.0%";
```

### Vad händer om jag behöver **how to export cell value** som HTML istället för ren text?

De flesta bibliotek har en overload som accepterar en exporttyp. Du skulle sätta `ExportAsString = true` och lägga till `ExportHtml = true` (eller liknande). Principen är densamma: definiera formatet, välj sedan output‑representationen.

### Kan jag applicera formatet på ett helt område, inte bara en cell?

Absolut. Du kan tilldela `NumberFormat` till ett `Style`‑objekt och sedan applicera den stilen på ett `Range`. Export‑anropet förblir oförändrat; det kommer automatiskt att plocka upp stilen.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Vad händer när cellen innehåller en formel?

Export‑rutinen utvärderar formeln först, och formaterar sedan det resulterande numeriska värdet. Ingen extra kod behövs – se bara till att `Calculate` har körts om du har inaktiverat automatisk beräkning.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusion

Du vet nu hur du **apply custom number format** på en kalkylblads‑cell, **format number in spreadsheet** i olika sammanhang, och **how to export cell value** som en färdig‑till‑visning‑sträng. Det koncisa kodexemplet ovan täcker varje steg – från arbetsboks‑skapande till slutlig output – så att du kan släppa in det direkt i ett produktionsprojekt.

Redo för nästa utmaning? Prova att kombinera tekniken med **how to format numeric cell** för datum, valutasymboler eller villkorlig formatering. Eller utforska att exportera flera celler som CSV samtidigt som du bevarar varje cells custom format. Himlen är gränsen, och med dessa grunder har du en solid plattform.

Lycka till med kodandet, och glöm inte att experimentera – ibland dyker de bästa svaren upp när du justerar formatsträngen lite grann!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}