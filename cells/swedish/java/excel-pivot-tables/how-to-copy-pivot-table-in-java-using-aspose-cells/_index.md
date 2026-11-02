---
category: general
date: 2026-07-06
description: Hur man kopierar pivottabell i Java med Aspose.Cells – steg‑för‑steg‑guide
  för att duplicera Excel‑pivottabeller programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: sv
lastmod: 2026-07-06
og_description: Att kopiera en pivottabell i Java med Aspose.Cells låter dig duplicera
  Excel‑pivottabeller snabbt och pålitligt.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Hur man kopierar pivottabell i Java – Komplett guide till Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Hur man kopierar pivottabell i Java med Aspose.Cells
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar pivottabell i Java med Aspose.Cells

Har du någonsin undrat **hur man kopierar pivottabeller** i en Excel-fil utan att öppna arbetsboken manuellt? Du är inte ensam. I många rapporteringspipeline behöver du **duplicera Excel‑pivottabeller** i farten—kanske för att skapa en ögonblicksbild, flytta den till ett nytt blad, eller generera en mall för nedströmsanvändare.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar exakt detta. Med Aspose.Cells for Java‑biblioteket laddar vi en arbetsbok, hittar källpivotrangen, kopierar den till en ny plats och sparar resultatet. Inga vaga referenser, bara en konkret lösning som du kan lägga in i ditt projekt idag.

---

## Förutsättningar

* **Java Development Kit (JDK) 8+** – koden kompileras med någon nyare JDK.
* **Aspose.Cells for Java** version 25.11 eller nyare – `Range.copy`‑metoden som stödjer pivottabeller introducerades i denna version.
* En **input.xlsx**‑fil som redan innehåller en pivottabell (du kan skapa en i Excel för testning).
* Ett byggverktyg du föredrar (Maven, Gradle eller ren `javac`). Vi visar Maven‑beroendet för snabb start.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Steg 1: Ladda källarbetsboken

Det första vi gör är att öppna Excel‑filen som innehåller den ursprungliga pivottabellen. Aspose.Cells behandlar arbetsboken som ett objekt i minnet, så du kan manipulera den utan att starta Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Varför detta är viktigt:** Att ladda arbetsboken ger oss åtkomst till kalkylblad, celler och, avgörande, pivot‑cachen som stöder pivottabellen. Utan detta steg har biblioteket inget att kopiera.

---

## Steg 2: Hämta kalkylbladet som innehåller pivottabellen

Om din arbetsbok har flera blad måste du peka på rätt. Här tar vi helt enkelt det första bladet, men du kan också använda `get("SheetName")` för en namngiven sökning.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Proffstips:** När du hanterar många blad, cacha indexet eller namnet i en konfigurationsfil för att undvika hårdkodade siffror.

---

## Steg 3: Definiera källintervallet som inkluderar pivottabellen

Från och med version 25.11 låter Aspose.Cells dig behandla en pivottabell som ett vanligt cellintervall. Ange den övre vänstra och nedre högra cellen som omsluter hela pivottabellen.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Edge case:** Om din pivottabell expanderar dynamiskt (t.ex. rader läggs till senare), överväg att använda `worksheet.getPivotTables().get(0).getDataRange()` för att programatiskt hämta exakt intervall.

---

## Steg 4: Definiera destinationsintervallet där pivottabellen ska kopieras

Välj någon tom cell där du vill att den duplicerade pivottabellen ska visas. I den här demonstrationen börjar vi på **F1**, vilket lämnar ett mellanrum mellan originalet och kopian.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Varför inte ett nytt blad?** Du kan också skapa ett nytt kalkylblad (`workbook.getWorksheets().add("Copy")`) och använda dess celler som destination. Samma `copy`‑metod fungerar över blad.

---

## Steg 5: Kopiera pivottabellen till den nya platsen

Nu händer magin. `copy`‑metoden klonar pivottabellen, dess cache, formatering och även eventuella associerade slicers (från och med den senaste versionen).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Viktigt:** Kopieringsoperationen är *djup*; den skapar **inte** en referens tillbaka till den ursprungliga pivottabellen. Du kan modifiera den nya pivottabellen oberoende utan att påverka källan.

---

## Steg 6: Spara arbetsboken med den duplicerade pivottabellen

Slutligen skriver du den modifierade arbetsboken tillbaka till disk. Du kan skriva över originalet eller skapa en ny fil; här väljer vi det senare för att behålla källan intakt.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

När du öppnar **output.xlsx** i Excel ser du den ursprungliga pivottabellen i kolumnerna A‑D och en perfekt kopia som börjar i kolumn F. Båda pivottabellerna kan uppdateras separat.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är den kompletta Java‑klassen som du kan kompilera och köra direkt:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Förväntat resultat:** När du öppnar `output.xlsx` visas den ursprungliga pivottabellen (A1:D20) och en identisk pivottabell som börjar på F1. Båda tabellerna behåller sina filter, stilar och beräknade fält.

---

## Hantera vanliga variationer

| Situation | Vad som ska justeras |
|-----------|----------------------|
| **Multiple pivots** on the same sheet | Loopa igenom `worksheet.getPivotTables()` och kopiera varje med sitt eget destinationsintervall. |
| **Dynamic data range** | Använd `worksheet.getPivotTables().get(0).getDataRange()` för att automatiskt upptäcka källområdet. |
| **Copy to another workbook** | Ladda en andra `Workbook`‑instans, skapa ett destinationskalkylblad och anropa sedan `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | Från och med 25.12 kopieras slicers automatiskt när intervallet inkluderar dem. Verifiera i Excel efter sparning. |

---

## Proffstips & fallgropar

* **Version check:** `copy`‑metoden som stödjer pivottabeller lades till i **Aspose.Cells 25.11**. Om du använder en äldre version får du ett undantag. Verifiera alltid `aspose-cells`‑versionen i din `pom.xml`.
* **Performance:** Att kopiera stora pivottabeller kan vara minnesintensivt. Om du bara behöver data, överväg att exportera pivottabellen till en platt tabell istället för att klona hela objektet.
* **Refresh behavior:** Den duplicerade pivottabellen behåller sin egen cache. Om du ändrar underliggande data, anropa `pivotTable.refresh()` på den nya pivottabellen för att beräkna om.
* **Formatting quirks:** Vissa anpassade talformat kanske inte överlever kopieringen i mycket gamla Excel‑versioner (<2007). Testa med din målgrupps Excel‑version.

---

## Slutsats

Du har nu ett gediget, end‑to‑end‑svar på **hur man kopierar pivottabeller** med Aspose.Cells för Java, och du har sett hur man **duplicerar Excel‑pivottabeller** på några få kodrader. Metoden fungerar för enskilda eller flera pivottabeller, över kalkylblad och även mellan arbetsböcker.

Nästa steg kan inkludera:

* Automatisera kopieringen för varje pivottabell i ett batch‑jobb.
* Lägg till kod för att byta namn på den duplicerade pivottabellen (t.ex. `pivotTable.setName("Copy_of_Sales")`).
* Integrera rutinen i en större rapporteringstjänst som genererar PDF‑ eller CSV‑exporter.

Prova det, justera intervallen så de matchar dina faktiska data, och låt biblioteket sköta det tunga arbetet. Lycka till med kodandet!

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java&#58; En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Manipulering av Excel‑pivottabeller med Aspose.Cells Java&#58; En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Hur man uppdaterar källan för Excel‑pivottabell med Aspose.Cells för Java&#58; En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}