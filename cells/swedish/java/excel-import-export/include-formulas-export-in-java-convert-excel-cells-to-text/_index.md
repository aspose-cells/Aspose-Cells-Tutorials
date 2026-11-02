---
category: general
date: 2026-07-03
description: Inkludera formelexport i Java för att konvertera Excel-celler till text
  med Aspose.Cells. Lär dig hur du skriver ut ett Excel‑område och effektivt får cellvärden
  som sträng.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: sv
og_description: Inkludera formler export i Java för att konvertera Excel-celler till
  text. Steg‑för‑steg‑guide som visar hur man skriver ut ett Excel‑område och hämtar
  cellvärden som en sträng.
og_title: Inkludera formler i export i Java – Konvertera Excel-celler till text
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Inkludera export av formler i Java – Konvertera Excel-celler till text
url: /sv/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Inkludera formler export i Java – Konvertera Excel-celler till text

Har du någonsin behövt **include formulas export** när du hämtar data från en Excel-arbetsbok? Kanske bygger du en rapporteringstjänst som måste bevara de ursprungliga formlerna samtidigt som den levererar en prydlig textblob. I så fall är du på rätt plats. Den här guiden visar hur du konverterar Excel-celler till vanlig text—*inklusive* eventuella inbäddade formler—med Aspose.Cells för Java.

Vi kommer också att beröra hur man **print Excel range**, justerar **export table options**, och slutligen **get cell values string** som du kan logga, skicka via ett API eller lagra i en databas. När du är klar har du ett fullt körbart kodexempel och en solid förståelse för varför varje anrop görs.

## Vad du får med dig

- Ett komplett, kopiera‑och‑klistra‑klart Java‑program som läser en `.xlsx`‑fil, väljer ett område och exporterar det som en formaterad sträng.
- En förståelse för `ExportTableOptions`‑klassen och varför man växlar `setExportAsString` och `setIncludeFormula`.
- Tips för att hantera stora arbetsblad, olika datatyper och anpassa utdataformatet.
- En snabb checklista för vanliga fallgropar (tänk sammanslagna celler, dolda rader och regionsspecifika talformat).

### Förutsättningar

- Java 17 eller nyare (koden kompilerar med äldre versioner men vi håller oss till den senaste LTS).
- Aspose.Cells för Java 23.10 (eller någon nyare version) — du kan hämta den från Maven Central.
- En exempel‑`input.xlsx` placerad i en mapp du kontrollerar (sökvägen är hårdkodad i exemplet för tydlighet).

Om du redan har dem, låt oss dyka ner.

## Steg 1: Ställ in projektet och lägg till beroenden

Först, skapa ett Maven‑projekt (eller Gradle, om du föredrar). Lägg till Aspose.Cells‑beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Om du använder en företagsproxy, se till att lagret är åtkomligt; annars misslyckas bygget med felet “Could not resolve dependencies”.

När Maven är klar med nedladdning är du redo att skriva lite Java.

## Steg 2: Ladda arbetsboken och hämta önskat arbetsblad

Den första raden i kodexemplet visar hur man öppnar en befintlig arbetsbok:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Byt ut `YOUR_DIRECTORY` mot den absoluta eller relativa sökvägen till din fil. `Workbook`‑konstruktorn upptäcker automatiskt filformatet (XLS, XLSX, CSV osv.), så du behöver inte ange det.

Därefter hämtar vi det första bladet:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Varför det första bladet? I många mallar finns data på den första fliken, men du kan ange vilket index som helst eller till och med använda `get("SheetName")` om du föredrar ett namn‑baserat tillvägagångssätt.

## Steg 3: Definiera området du vill exportera

Nu kommer kärnan i **convert excel cells text**‑operationen. Du talar om för Aspose.Cells vilka celler som ska hämtas genom att skapa ett `Range`‑objekt:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Strängen `"A1:C3"` är en klassisk A1‑stiladress. Den kan också byggas programatiskt:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Den flexibiliteten hjälper när områdesstorleken är dynamisk—t.ex. när du läser den sista använda raden med `ws.getCells().getMaxDataRow()`.

## Steg 4: Konfigurera Export Table Options för att inkludera formler

Här sker magin med **include formulas export**. Som standard returnerar Aspose.Cells de *visade* värdena. Om en cell innehåller `=SUM(A1:A3)` får du det beräknade talet, inte formeltexten. För att ändra detta, konfigurera `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Varför båda flaggorna? `setExportAsString(true)` instruerar API:t att sammanfoga cellerna med standardavgränsare (tab för kolumner, ny rad för rader). `setIncludeFormula(true)` byter värdekällan från “visat värde” till “rå formel”. Om du bara vill ha värden, låt den vara `false`.

### Valfria justeringar

- `eto.setExportHiddenRows(true);` – inkludera rader som är dolda i Excel.
- `eto.setExportHiddenColumns(true);` – samma för kolumner.
- `eto.setExportAsHTML(true);` – få HTML istället för vanlig text.

Känn dig fri att experimentera; options‑klassen är en **export table options**‑lekplats.

## Steg 5: Hämta området som en formaterad sträng

Nu hämtar vi data:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Den returnerade `txt` ser ungefär ut så här (förutsatt att A1:C3 innehåller en blandning av värden och formler):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Observera tabben (`\t`) som separerar kolumner och ny rad (`\n`) som separerar rader. Du kan dela strängen senare om du behöver en 2‑D‑array:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Steg 6: Skriv ut resultatet – “Print Excel Range” gjort enkelt

Till sist skriver vi ut strängen till konsolen:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

När programmet körs skrivs exakt samma utdata som visas ovan. Därefter kan du skriva strängen till en loggfil, skicka den via HTTP eller lagra den i ett NoSQL‑dokument.

## Fullt, körklart exempel

När allt sätts ihop, här är hela programmet. Kopiera, klistra in och tryck på **Run**—inga saknade imports.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Förväntad utdata (exempel)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Om din arbetsbok innehåller tal formaterade som datum, visas de i det regions-specifika formatet (t.ex. `2026‑07‑03`). För att tvinga ISO‑datum kan du justera `ExportTableOptions` med ett anpassat `NumberFormat`.

## Hantera kantfall och vanliga frågor

### Vad händer om området innehåller sammanslagna celler?

Sammanslagna celler behandlas som värdet i den översta vänstra cellen. Resten av det sammanslagna området visas som tomma strängar. Om du behöver adressen för den sammanslagna regionen, fråga `Cell.getMergedRange()` innan export.

### Kan jag exportera ett massivt blad (hundratusentals rader)?

Ja, men var medveten om minnesanvändning. Använd `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` för att låta Aspose.Cells strömma data till disk. Överväg också att exportera i delar (t.ex. 10 000 rader åt gången) för att hålla strängen hanterbar.

### Hur ändrar jag kolumnavgränsaren?

`ExportTableOptions` erbjuder `setSeparator(char separator)`. För CSV‑liknande utdata, sätt den till `','`:

```java
eto.setSeparator(',');
```

### Respekterar formler externa referenser?

Om en formel pekar på en annan arbetsbok, behåller Aspose.Cells referenstexten (`='[Other.xlsx]Sheet1'!A1`). Den kommer inte att utvärdera det externa värdet om du inte också laddar den arbetsboken.

## Pro‑tips för produktionsklar kod

- **Cache arbetsboken** om du läser den

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}