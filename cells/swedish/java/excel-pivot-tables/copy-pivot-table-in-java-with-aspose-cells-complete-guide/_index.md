---
category: general
date: 2026-07-20
description: Kopiera pivottabell i Java med Aspose.Cells. Lär dig hur du kopierar
  pivottabell till en annan fil, extraherar pivottabellens område och kopierar området
  till en ny arbetsbok.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy pivot table to another file
- copy range to new workbook
- how to copy pivot table
- extract pivot table range
language: sv
lastmod: 2026-07-20
og_description: Kopiera pivottabell i Java med Aspose.Cells. Följ den här guiden för
  att kopiera pivottabellen till en annan fil, extrahera dess område och kopiera området
  till en ny arbetsbok.
og_image_alt: Diagram illustrating how to copy pivot table from one workbook to another
  using Java
og_title: Kopiera pivottabell i Java – Steg‑för‑steg Aspose.Cells‑handledning
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  headline: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  type: TechArticle
- description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  name: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  steps:
  - name: Expected Output
    text: '- `CopyWithPivot.xlsx` contains a single worksheet. - The worksheet shows
      the same pivot layout as the source. - All pivot fields, filters, and calculated
      items are intact. - Refreshing the pivot updates totals based on the newly copied
      data.'
  - name: Copying Multiple Pivot Tables
    text: If your source sheet has more than one pivot, repeat the `createRange`/`copy`
      pair for each table, adjusting the address accordingly. You can also loop through
      `sourceWorksheet.getPivotTables()` to automate discovery.
  - name: Preserving Styles and Formatting
    text: The `Range.copy` method copies cell values, formulas, and formatting by
      default. However, if you only need the data without styles, use `sourceRange.copy(destinationRange,
      new CopyOptions());` and tweak the `CopyOptions` flags.
  - name: Working with Large Workbooks
    text: 'For workbooks exceeding a few hundred MB, consider enabling **memory‑efficient
      loading**:'
  - name: Quick Recap
    text: '- Loaded a source workbook containing a pivot table. - Identified the exact
      **extract pivot table range** (`A1:G20`). - Created a fresh workbook and **copied
      range to new workbook**, preserving the pivot. - Saved the result, effectively
      **copying pivot table to another file**.'
  type: HowTo
- questions:
  - answer: Yes. Aspose handles format conversion automatically during `save()`. Just
      specify the desired extension in the output path.
    question: Can I copy a pivot table across different Excel formats (XLSX → XLS)?
  - answer: The copy will overwrite existing cells. To avoid data loss, either clear
      the area first (`destinationSheet.getCells().clearRange("A1:G20")`) or choose
      a different start cell.
    question: What if the destination workbook already contains data in the target
      range?
  - answer: 'The source workbook is opened in read‑write mode by default. If you only
      need to read, pass `LoadOptions` with `setReadOnly(true)`. ## Next Steps & Related
      Topics Now that you know **how to copy pivot table** programmatically, you might
      explore: - **Refreshing pivot caches** after copying (`pivotTab'
    question: Does this work with read‑only source files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot Table
title: Kopiera pivottabell i Java med Aspose.Cells – Komplett guide
url: /sv/java/excel-pivot-tables/copy-pivot-table-in-java-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell i Java med Aspose.Cells – Komplett guide

Har du någonsin behövt **copy pivot table** från en Excel‑fil till en annan men varit osäker på var du ska börja? Du är inte ensam. I många rapporteringspipeline måste vi flytta en pivot‑driven sammanfattning från en huvudarbetsbok till en lättviktig fil för distribution, och att göra det manuellt är besvärligt.  

I den här handledningen går vi igenom en ren, programmatisk lösning som låter dig **copy pivot table to another file**, extrahera dess exakta område och till och med **copy range to new workbook** i ett enda steg. I slutet har du ett återanvändbart kodsnutt som fungerar med alla Aspose.Cells‑aktiverade Java‑projekt.

## Vad den här guiden täcker

- Laddar en källarbetsbok som redan innehåller en pivottabell  
- Bestämmer det exakta **extract pivot table range** du behöver  
- Skapar en ny arbetsbok och klistrar in området samtidigt som pivottlogiken bevaras  
- Sparar resultatet som en ny fil, redo för efterföljande bearbetning  

Inga externa verktyg, inga makro‑akrobatik—bara ren Java‑kod och ett fåtal Aspose.Cells‑anrop. Om du har arbetat med Excel tidigare kommer koncepten att kännas bekanta; om du är ny på Aspose abstraherar biblioteket bort den lågnivå‑XML‑hanteringen, så att du kan fokusera på affärslogik.

> **Förutsättningar**  
> - Java 8 eller nyare  
> - Aspose.Cells for Java (senaste versionen per juli 2026)  
> - Grundläggande kunskap om Excel‑pivottabeller  

Nu, låt oss dyka ner.

## Steg 1: Ställ in ditt projekt och importera Aspose.Cells

Innan vi rör någon arbetsbok, se till att Aspose.Cells‑JAR‑filen finns i din classpath. Om du använder Maven, lägg till beroendet:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of 2026 -->
</dependency>
```

Om du föredrar en manuell installation, släpp `aspose-cells-24.10.jar` i din `libs`‑mapp och referera den i din IDE.

> **Pro tip:** Håll biblioteksversionen i linje med din Java‑runtime för att undvika `UnsupportedClassVersionError`.

## Steg 2: Ladda källarbetsboken som innehåller pivottabellen

Det första vi behöver är ett `Workbook`‑objekt som pekar på filen där pivottabellen finns. Detta är där **copy pivot table**‑operationen börjar.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that already has the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Varför laddar vi den på detta sätt? Aspose läser in hela filen i minnet, vilket ger oss full åtkomst till kalkylblad, celler och den underliggande pivot‑cachen. Detta säkerställer att pivot‑definitionen (fält, filter, datakälla) förblir intakt när vi senare kopierar den.

## Steg 3: Identifiera det exakta området som innehåller pivottabellen

En pivottabell är inte bara ett block med celler; den stöds av en dold cache. Men när du kopierar det visuella området, tar Aspose automatiskt med cachen. För att vara säker definierar vi området explicit—detta är steget **extract pivot table range**.

```java
        // Define the range covering the pivot table (adjust as needed)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                // first worksheet
                                          .getCells()
                                          .createRange("A1:G20"); // typical size; change if larger
```

Om du är osäker på dimensionerna kan du programatiskt lokalisera pivottabellen med `Worksheet.getPivotTables()`. För korthetens skull antar vi en känd rektangel, men samma logik fungerar för dynamisk upptäckt.

## Steg 4: Skapa en ny arbetsbok för att ta emot det kopierade området

Nu skapar vi en ny arbetsbok som blir destinationsfilen. Detta är där **copy range to new workbook** sker.

```java
        // Create an empty workbook that will receive the copy
        Workbook destinationWorkbook = new Workbook(); // starts with a default sheet
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Varför en helt ny arbetsbok? Att börja rent garanterar att ingen oönskad formatering eller dolda blad stör pivotens interna referenser. Om du behöver slå ihop med en befintlig fil, ladda helt enkelt den filen istället för `new Workbook()`.

## Steg 5: Utför kopieringen – pivottabellen bevaras

Här är kärnan i handledningen: kopiera området samtidigt som pivottabellen förblir funktionell. Aspose:s `Range.copy`‑metod gör det tunga arbetet.

```java
        // Copy the source range (including the pivot) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

När den här raden körs klonar Aspose de visuella cellerna **och** klonar den underliggande pivot‑cachen till den nya arbetsboken. Resultatet är en fullt fungerande pivottabell som du kan uppdatera, filtrera eller exportera precis som originalet.

> **Vanlig fråga:** *Vad händer om destinationen redan har en pivottabell med samma namn?*  
> Aspose byter automatiskt namn på den kopierade pivottabellen för att undvika kollisioner (t.ex. “PivotTable1_1”).

## Steg 6: Spara destinationsarboken

Till sist sparar vi den nya filen. Detta är steget som faktiskt **copy pivot table to another file** på disken.

```java
        // Save the workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

Efter att programmet har körts, öppna `CopyWithPivot.xlsx` i Excel. Du kommer att se samma pivottabellslayout, filter och datakälla (som nu pekar på det kopierade området). Att uppdatera pivottabellen kommer att beräkna om baserat på det nya datablocket.

## Fullt fungerande exempel

Sätter vi ihop allt, här är den kompletta, färdig‑till‑körning klassen:

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Define the range that includes the pivot table (e.g., A1:G20)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:G20");

        // 3️⃣ Create a new workbook to receive the copied range
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range to the destination worksheet; the pivot table is preserved
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Förväntat resultat

- `CopyWithPivot.xlsx` innehåller ett enda kalkylblad.  
- Kalkylbladet visar samma pivottabellslayout som källan.  
- Alla pivotfält, filter och beräknade objekt är intakta.  
- Att uppdatera pivottabellen uppdaterar totalerna baserat på den nykopierade datan.

## Hantera kantfall och variationer

### Kopiera flera pivottabeller

Om ditt källblad har mer än en pivottabell, upprepa `createRange`/`copy`‑paret för varje tabell och justera adressen därefter. Du kan också loopa igenom `sourceWorksheet.getPivotTables()` för att automatisera upptäckten.

### Bevara stilar och formatering

`Range.copy`‑metoden kopierar cellvärden, formler och formatering som standard. Men om du bara behöver data utan stilar, använd `sourceRange.copy(destinationRange, new CopyOptions());` och justera flaggorna i `CopyOptions`.

### Arbeta med stora arbetsböcker

För arbetsböcker som överstiger några hundra MB, överväg att aktivera **memory‑efficient loading**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook sourceWorkbook = new Workbook("bigfile.xlsx", loadOptions);
```

## Vanliga frågor

**Q: Kan jag kopiera en pivottabell mellan olika Excel‑format (XLSX → XLS)?**  
A: Ja. Aspose hanterar formatkonvertering automatiskt under `save()`. Ange bara önskad filändelse i utdata‑sökvägen.

**Q: Vad händer om destinationsarboken redan innehåller data i målområdet?**  
A: Kopieringen kommer att skriva över befintliga celler. För att undvika dataförlust, rensa området först (`destinationSheet.getCells().clearRange("A1:G20")`) eller välj en annan startcell.

**Q: Fungerar detta med skrivskyddade källfiler?**  
A: Källarboken öppnas i läs‑/skriv‑läge som standard. Om du bara behöver läsa, skicka `LoadOptions` med `setReadOnly(true)`.

## Nästa steg och relaterade ämnen

Nu när du vet **how to copy pivot table** programatiskt, kan du utforska:

- **Refreshing pivot caches** efter kopiering (`pivotTable.refresh();`)  
- **Exporting pivot data to CSV** för efterföljande analys  
- **Programmatically adding slicers** till den kopierade pivottabellen (`PivotTable.addSlicer(...)`)  
- **Copying charts linked to pivot tables** med `Chart.copy()`  

Var och en av dessa bygger på grunden vi just lagt, så att du kan bygga end‑to‑end Excel‑automatiseringspipeline i Java.

---

### Snabb sammanfattning

- Laddade en källarbetsbok som innehåller en pivottabell.  
- Identifierade det exakta **extract pivot table range** (`A1:G20`).  
- Skapade en ny arbetsbok och **copied range to new workbook**, bevarade pivottabellen.  
- Sparade resultatet, vilket effektivt **copy pivot table to another file**.  

Prova det med dina egna filer, justera området och se hur pivottabellen migrerar felfritt. Om du stöter på problem, lämna en kommentar nedan—lycklig kodning!

![Copy pivot table diagram showing source and destination workbooks](https://example.com/images/copy-pivot-table-diagram.png)


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur du uppdaterar Excel‑pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimera laddning av pivottabeller i Java med Aspose.Cells: En omfattande guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Excel‑pivottabellmanipulation med Aspose.Cells Java: En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}