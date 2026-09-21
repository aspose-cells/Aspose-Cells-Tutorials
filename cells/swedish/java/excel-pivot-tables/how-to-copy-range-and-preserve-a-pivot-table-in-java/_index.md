---
category: general
date: 2026-09-21
description: Lär dig hur du kopierar ett område i Java samtidigt som du bevarar pivottabellen.
  Denna steg‑för‑steg‑guide visar dig hur du exporterar en pivottabell på ett säkert
  sätt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: sv
lastmod: 2026-09-21
og_description: Hur du kopierar ett område i Java samtidigt som du bevarar pivottabellen.
  Följ den här kompletta guiden för att exportera pivottabeller på ett säkert sätt.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Hur man kopierar ett område och bevarar en pivottabell i Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Hur man kopierar ett område och bevarar en pivottabell i Java
url: /sv/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar område och bevarar en pivottabell i Java

Om du behöver **how to copy range** som innehåller en pivottabell, visar den här guiden ett pålitligt sätt att behålla pivottabellen intakt. Många utvecklare har problem med att förlora pivottabellen när de exporterar data, men metoden nedan låter dig **copy pivot table** data utan att bryta dess funktionalitet. I slutet av den här tutorialen kommer du att kunna **preserve pivot table** struktur, **export pivot table** filer, och förstå **how to preserve pivot** i olika scenarier.

Exemplet använder Aspose.Cells for Java, ett populärt bibliotek för Excel‑automatisering. Ingen extra verktyg behövs utöver en standard Java‑utvecklingsmiljö.

## Förutsättningar

* Java 17 (eller senare) installerat.
* Maven eller Gradle för att hantera beroenden.
* Aspose.Cells for Java (version 23.9 eller nyare). Lägg till följande Maven‑beroende:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* En källarbok (`Source.xlsx`) som innehåller pivottabellen du vill kopiera.

## Hur man kopierar område och behåller pivottabellen intakt

Kärnidén är att kopiera **range** som omsluter hela pivottabellen—inklusive dess datakälla—med `copyRange`. Denna metod kopierar både rådata och pivottabellens definition, vilket säkerställer att destinationsarboken får en fullt funktionell pivot.

### Steg 1: Läs in källarboken

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Varför detta steg?*  
Att läsa in arbetsboken ger dig åtkomst till kalkylbladet som innehåller pivottabellen. Klassen `Workbook` abstraherar hela Excel‑filen, medan `Worksheet` ger cell‑nivå operationer.

### Steg 2: Definiera området som täcker pivottabellen

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Varför detta steg?*  
En pivottabell är inte en enskild cell; den sträcker sig över ett block som inkluderar rubriker, datarader och pivot‑cachen. Genom att ange ett område som helt innehåller pivottabellen garanterar du att `copyRange` också kopierar den underliggande cachen, vilket är avgörande för **preserve pivot table**‑beteendet.

### Steg 3: Skapa en tom destinationsarbok

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Varför detta steg?*  
Att börja med en tom arbetsbok förhindrar oavsiktliga konflikter med befintliga blad eller namngivna områden. Destinationsarboken kommer att ta emot det kopierade området, vilket effektivt **export pivot table**‑innehållet.

### Steg 4: Kopiera området – pivottabellen bevaras

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Varför detta steg?*  
`copyRange` utför en djup kopiering: cellvärden, formatering och pivot‑metadata överförs. Detta är den kritiska operationen som möjliggör **copy pivot table** utan att förlora dess funktionalitet. Objektet `CellArea` definierar var området placeras i destinationsbladet.

### Steg 5: Spara destinationsarboken

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Varför detta steg?*  
Att spara slutför **export pivot table**‑processen. Den resulterande filen (`DestWithPivot.xlsx`) innehåller en fullt fungerande pivot som du kan öppna i Excel, Google Sheets eller någon annan kalkylbladsvisare.

## Verifiera att pivottabellen bevarades

Öppna `DestWithPivot.xlsx` i Excel och kontrollera följande:

1. Pivottabellen visas på samma plats (A1:G20) som i källan.  
2. Att uppdatera pivottabellen uppdaterar data korrekt, vilket bevisar att cachen kopierades.  
3. All formatering (kolumnbredder, talformat) matchar originalet.

Om någon av dessa kontroller misslyckas, verifiera att källområdet helt omsluter pivottabellen och dess datakälla. Ett vanligt misstag är att välja ett område som slutar för tidigt innan datacachen, vilket leder till en trasig pivot.

## Ytterligare överväganden

### Kopiera pivottabell över olika arbetsboksversioner

Aspose.Cells stöder äldre `.xls`‑filer såväl som det nyare `.xlsx`‑formatet. Samma kod fungerar oavsett filändelse, vilket gör det till en universell lösning för **how to preserve pivot** över versioner.

### Bevara pivottabell vid användning av en filtrerad källa

Om den källpivottabell som är filtrerad, kopieras även filtertillståndet. Behöver du återställa filter i destinationen, anropa `PivotTable.refreshData()` efter kopiering:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Exportera pivottabell som en statisk ögonblicksbild

Ibland kan du vilja ha en statisk kopia (endast värden) snarare än en live‑pivot. Ersätt `copyRange` med `copyRange` följt av `pt.setEnableRefresh(false)` för att inaktivera vidare beräkningar.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Hantera stora arbetsböcker

För arbetsböcker med många kalkylblad, begränsa kopieringsoperationen till det specifika bladet för att minska minnesanvändning. Använd `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` för att finjustera prestanda.

## Fullständigt körbart exempel

Nedan är hela programmet som du kan kopiera, klistra in och köra. Anpassa filsökvägarna så att de matchar din miljö.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Förväntad output**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

När du öppnar `DestWithPivot.xlsx` bör du se den ursprungliga pivottabellen fullt funktionell, vilket bekräftar att du framgångsrikt har **how to copy range** medan du **preserve pivot table**.

## Vanliga fallgropar och pro‑tips

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Pivot visas men visar `#REF!`‑fel | The copied range omitted the hidden cache sheet | Utöka källområdet för att inkludera hela cachen (vanligtvis raderna under pivottabellen) |
| Destinationsarboken är större än förväntat | `copyRange` also copies formatting | Använd `CopyOptions` för att exkludera formatering om storleken är ett problem |
| Uppdatering misslyckas med “Data source not found” | Source workbook used external data connections | Replikera anslutningen i destinationen eller kopiera datakällbladet först |

**Pro‑tips:** Kör alltid en snabb `destWs.getPivotTables().size()`‑kontroll efter kopiering. Om antalet är noll, så inkluderade inte området pivottabellens definition och du måste utöka det.

## Slutsats

I den här tutorialen demonstrerade vi **how to copy range** som innehåller en pivottabell och garanterade att **preserve pivot table**‑beteendet förblir intakt. Genom att läsa in källarboken, definiera ett omfattande område, använda `copyRange` och spara destinationsfilen, kan du på ett pålitligt sätt **export pivot table**‑data och besvara frågan **how to preserve pivot** i Java‑projekt.

Nästa steg du kan utforska inkluderar:

* Automatisera kopieringen för flera blad (använd det sekundära nyckelordet **copy pivot table** i en loop).
* Konvertera den exporterade arbetsboken till CSV samtidigt som rådata behålls (fortfarande **preserve pivot table**‑logik för källan).

## Vad bör du lära dig härnäst?

Följande tutorialer täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}