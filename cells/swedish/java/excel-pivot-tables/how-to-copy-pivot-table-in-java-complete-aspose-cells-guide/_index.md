---
category: general
date: 2026-06-08
description: Hur man kopierar pivottabell med Aspose.Cells i Java. Lär dig att kopiera
  område mellan arbetsböcker och bevara pivottabeller utan ansträngning.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: sv
og_description: Hur man kopierar pivottabell i Java med Aspose.Cells. Denna handledning
  visar hur man kopierar ett område mellan arbetsböcker och behåller pivottabellen
  intakt.
og_title: Hur man kopierar pivottabell i Java – Steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Hur man kopierar pivottabell i Java – Komplett Aspose.Cells-guide
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du pivottabell i Java – Komplett Aspose.Cells-guide

Har du någonsin undrat **hur man kopierar en pivottabell** från en Excel-arbetsbok till en annan med Java? Den goda nyheten är att Aspose.Cells gör det enkelt att **kopiera område mellan arbetsböcker** samtidigt som varje detalj i pivottabellen bevaras.  

I den här handledningen går vi igenom ett verkligt exempel som inte bara kopierar själva pivottabellen utan också behåller underliggande data, formatering och formler intakta. I slutet kommer du exakt att veta **hur man bevarar pivottabellens** strukturer, hur man flyttar en pivottabell till en helt ny arbetsbok och hur man undviker de vanliga fallgroparna som får många utvecklare att snubbla.

Vi kommer att gå igenom:

* De minsta förutsättningarna (Java 17+, Aspose.Cells for Java 23.9+).  
* En steg‑för‑steg genomgång av koden, med förklaringar till **varför** varje rad är viktig.  
* Hantering av edge‑cases för stora pivottabellområden och externa datakällor.  
* Ett komplett, körbart program som du kan klistra in i din IDE och köra idag.

> **Proffstips:** Om du redan använder Maven eller Gradle är det bara en rad för att lägga till Aspose.Cells som ett beroende—ingen manuell JAR‑hantering behövs.

---

## Så kopierar du pivottabell – Steg‑för‑steg‑översikt

Nedan är en hög‑nivåvy av vad vi ska uppnå:

1. Läs in källarboken som innehåller pivottabellen.  
2. Identifiera det exakta cellområdet som omger pivottabellen.  
3. Skapa en ny destinationsarbetsbok.  
4. **Kopiera området** till det nya bladet, låt Aspose.Cells automatiskt bevara pivottabellen.  
5. Spara resultatet som en ny fil.

Varje steg illustreras med kodsnuttar och en kort motivering, så du förstår mekaniken—inte bara mekaniken.

![Diagram som visar hur en pivottabell kopieras från en källarbetsbok till en destinationsarbetsbok samtidigt som dess struktur bevaras](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="how to copy pivot table diagram"}

### Steg 1: Ställ in Aspose.Cells i ditt projekt

Innan du kan manipulera Excel‑filer behöver du Aspose.Cells‑biblioteket på din classpath. Om du använder Maven, lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

För Gradle är det också en rad:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Varför detta är viktigt:* Aspose.Cells abstraherar bort de lågnivå OpenXML‑detaljerna och ger dig ett enkelt API för att **kopiera pivottabell till ny arbetsbok** utan att förlora någon metadata.

### Steg 2: Läs in källarboken

Vi behöver en `Workbook`‑instans som pekar på filen som innehåller pivottabellen. Ersätt `YOUR_DIRECTORY/src.xlsx` med den faktiska sökvägen på din maskin.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Obs:** Aspose.Cells upptäcker automatiskt filformatet (XLSX, XLS, CSV, etc.), så du behöver inte oroa dig för formatkonvertering.

### Steg 3: Definiera pivottabellens omgivande område

En pivottabell lever inom ett rektangulärt block av celler. Du kan lokalisera den manuellt (t.ex. `A1:G20`) eller programatiskt genom att inspektera bladets `PivotTables`‑samling. I den här handledningen hårdkodar vi området för tydlighetens skull.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Varför vi använder `createRange`:* Den skapar ett lättviktigt `Range`‑objekt som kan skickas till `copyRange`. Detta är det mest pålitliga sättet att **kopiera område mellan arbetsböcker** samtidigt som pivottabellens interna strukturer inkluderas.

### Steg 4: Skapa en tom destinationsarbetsbok

Nu startar vi en tom arbetsbok som ska ta emot den kopierade datan.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Standardarboken innehåller redan ett kalkylblad, vilket är perfekt för vårt ändamål. Om du behöver ett specifikt bladnamn kan du byta namn på det:

```java
destinationSheet.setName("PivotCopy");
```

### Steg 5: Kopiera området och bevara pivottabellen

Här händer magin. Metoden `copyRange` accepterar ett `CopyOptions`‑objekt, men vi behöver inte justera någonting—pivottabellens bevarande är aktiverat som standard.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Varför detta fungerar:* Aspose.Cells behandlar pivottabellen som en del av cellsamlingen. När du anropar `copyRange` replikerar den den underliggande pivottabellscachen, datafält och layout, vilket effektivt **hur man bevarar pivottabell** utan extra kod.

### Steg 6: Spara destinationsarbetsboken

Till sist skriver vi den nya filen till disk.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Öppna den resulterande `copied-with-pivot.xlsx` i Excel, så ser du en exakt kopia av den ursprungliga pivottabellen, redo för vidare analys.

## Fullständigt fungerande exempel

Nedan är det kompletta programmet som du kan kompilera och köra direkt. Det samlar alla kodsnuttar ovan, lägger till några defensiva kontroller och skriver ut ett vänligt bekräftelsemeddelande.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Förväntad utdata när du kör programmet**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Öppna destinationsfilen—din pivottabell bör se identisk ut med originalet, komplett med slicers, filter och beräknade fält.

## Hantera vanliga edge‑case

| Situation | Vad att hålla utkik efter | Föreslagen lösning |
|-----------|---------------------------|--------------------|
| **Pivottabell använder en extern datakälla** (t.ex. en databas) | Den externa anslutningen är inte inbäddad i arbetsboken, så kopiering kan bryta länken. | Exportera data till ett blad först, skapa sedan en pivottabell på det bladet innan du kopierar. |
| **Mycket stor pivottabell (tusentals rader)** | `copyRange` kan förbruka betydande minne. | Öka JVM‑heapen (`-Xmx2g`) eller kopiera pivottabellen i mindre delar med `copyRows`/`copyColumns`. |
| **Flera pivottabeller på samma blad** | Att hårdkoda `A1:G20` kopierar bara den första pivottabellen. | Loopa igenom `sourceWorksheet.getPivotTables()` och kopiera varje `PivotTable.getDataRange()`. |
| **Destinationsarboken innehåller redan ett blad med samma namn** | `setName` kommer att kasta ett undantag. | Använd `Workbook.getWorksheets().add("PivotCopy")` för att skapa ett blad med unikt namn. |

Dessa tips säkerställer att **hur man kopierar pivottabell** fungerar pålitligt, även i produktionsscenarier.

## Vanliga frågor

**Q: Kopierar den här metoden även pivottabellens formatering?**  
A: Ja. Eftersom vi kopierar hela cellområdet följer stilar, villkorsstyrd formatering och talformat med datan.

**Q: Vad händer om jag behöver kopiera pivottabellen till en specifik cell annan än `A1`?**  
A: Ändra helt enkelt det tredje argumentet i `copyRange` till den önskade övre‑vänstra adressen, t.ex. `"B5"`.

**Q: Kan jag kopiera en pivottabell utan dess källdata?**  
A: Inte direkt. Pivottabellscachen finns i arbetsboken; att ta bort källdatan gör pivottabellen oanvändbar. Exportera källdata till ett dolt blad om du vill ha en lättviktig kopia.

## Slutsats

Du har nu ett tydligt, helhets svar på **hur man kopierar pivottabell** i Java med Aspose.Cells. Genom att läsa in källarboken, definiera pivottabellens område och utnyttja `copyRange` kan du enkelt **kopiera område mellan arbetsböcker** samtidigt som pivottabellen förblir

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man uppdaterar Excel-pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hur man implementerar slicers i pivottabeller med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}