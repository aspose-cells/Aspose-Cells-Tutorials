---
category: general
date: 2026-10-23
description: Lär dig hur du duplicerar ett Excel‑ark i Java samtidigt som du bevarar
  pivottabeller. Den här guiden visar också hur du kopierar pivottabeller, kopierar
  Excel‑områden och kopierar ett ark med pivottabellsdata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: sv
lastmod: 2026-10-23
og_description: Duplicera ett Excel‑ark i Java samtidigt som pivottabeller bevaras.
  Följ den här kompletta handledningen för att kopiera pivottabeller, kopiera Excel‑områden
  och kopiera ett ark med pivottabellsdata.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplicera ett Excel‑blad med pivottabeller i Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Hur man duplicerar ett Excel‑ark och behåller pivottabeller intakta i Java
url: /sv/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du duplicerar ett Excel‑ark och behåller pivottabeller intakta i Java

Om du behöver **duplicera ett Excel‑ark** medan du behåller varje pivottabell intakt, visar den här guiden exakt hur du gör. Du får se en kortfattad lösning som kopierar ett ark, kopierar ett specifikt område och till och med kopierar en pivottabell till en annan arbetsbok—allt i ren Java med Aspose.Cells.

Att duplicera ett Excel‑ark är en vanlig uppgift när du genererar månatliga rapporter från en mall eller när du behöver en sandlådekopia för testning. Koden nedan fungerar med Aspose.Cells 25.11 eller senare, som introducerade alternativet `setCopyPivotTable(true)`.

## Vad du behöver

Innan du börjar, se till att du har:

- Java 17 (eller någon nyare JDK) installerad
- Aspose.Cells for Java 25.11 eller nyare i ditt projekt (Maven‑koordinat `com.aspose:aspose-cells:25.11`)
- En källarbok (`SourceWithPivot.xlsx`) som redan innehåller en pivottabell
- En IDE eller ett byggverktyg du föredrar (IntelliJ IDEA, Eclipse, Maven, Gradle, osv.)

## Steg 1: Läs in källarboken som innehåller pivottabellen

Den första operationen är att öppna arbetsboken som innehåller den pivottabell du vill bevara.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Varför detta steg är viktigt:** Att läsa in källarboken ger dig åtkomst till arbetsbladsobjekten, cellerna och de inbäddade pivottabellerna. Utan detta kan du inte referera till pivottabellsdata som du planerar att kopiera.

## Steg 2: Skapa en tom målarbok (eller läs in en befintlig)

Du kan antingen börja med en tom arbetsbok eller öppna en befintlig fil som ska ta emot det duplicerade arket.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tips:** Om du redan har en rapportarbok, ersätt raden ovan med `new Workbook("ExistingReport.xlsx")` för att lägga till det duplicerade arket i den.

## Steg 3: Kopiera hela arbetsbladet – pivottabellen bevaras automatiskt

Att kopiera hela arbetsbladet är det enklaste sättet att **kopiera ark med pivottabell**. Aspose.Cells kopierar pivottabellens definition och dess cache automatiskt.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Varför det fungerar:** `addCopy` klonar bladstrukturen, cellvärden, format och eventuella inbäddade pivottabeller. Det nya arbetsbladet i `dstWb` kommer att se identiskt ut med originalet, inklusive pivottabellens cache.

## Steg 4: (Valfritt) Kopiera endast ett specifikt område som inkluderar pivottabellen

Ibland vill du inte ha hela bladet—kanske behöver du bara en del som innehåller pivottabellen. Här är det du **kopierar Excel‑område** och explicit begär att pivottabellen ska kopieras.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Hur det hjälper:** `setCopyPivotTable(true)` tvingar motorn att duplicera pivottabellens definition även när du kopierar ett begränsat område. Utan detta flagga skulle bara rådata kopieras och pivottabellen gå förlorad.

## Steg 5: Spara målarboken

Slutligen skriver du det duplicerade innehållet till en ny fil.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Förväntat resultat

När programmet körs skapas `DuplicatedWithPivot.xlsx` i mål katalogen. Öppna filen i Excel så ser du:

- Ett nytt arbetsblad med namnet `Sheet1 (Copy)` (eller originalnamnet med “Copy” tillagt)
- Pivottabellen visas exakt som i källbladet, fullt funktionell
- Om du använde det valfria områdeskopieringen finns bara cellerna A1:G30, men pivottabellen fungerar fortfarande eftersom dess cache kopierades

## Vanliga frågor och edge‑cases

### Hur kopierar man en pivottabell till en annan arbetsbok utan att kopiera hela bladet?

Om du bara behöver pivottabellen och dess underliggande data, kopiera området som innehåller både källdata och pivottabellen, och använd sedan `setCopyPivotTable(true)`. Samma kod som i **Steg 4** gäller; se bara till att området täcker datakällan.

### Vad händer om källarboken har flera arbetsblad med pivottabeller?

Upprepa **Steg 3** för varje arbetsblad du vill duplicera:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Fungerar detta med skyddade arbetsblad?

Aspose.Cells kan kopiera skyddade blad, men du måste ta bort skyddet först om du behöver modifiera pivottabellen efter kopieringen:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Kan jag kopiera en pivottabell till en befintlig arbetsbok som redan innehåller ett blad med samma namn?

Ja. Använd `addCopy` med ett unikt namn:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro‑tips: verifiera pivottabellens cache

Efter kopieringen kan du programatiskt bekräfta att pivottabellens cache finns:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Om cache‑ID‑talet skrivs ut som ett icke‑negativt tal, har pivottabellen duplicerats framgångsrikt.

## Slutsats

Du vet nu hur du **duplicerar ett Excel‑ark** i Java samtidigt som du bevarar varje pivottabell, hur du **kopierar pivottabeller** direkt, hur du **kopierar Excel‑område** som inkluderar en pivottabell, och hur du **kopierar ark med pivottabell** eller **kopierar pivottabell till arbetsbok** med Aspose.Cells 25.11+. Använd dessa mönster för att automatisera rapportgenerering, skapa mallkloner eller bygga testmiljöer som kräver identisk pivottabellsdriven analys.

Redo att utforska mer? Prova att exportera den duplicerade arbetsboken till PDF, eller programatiskt uppdatera pivottabellens cache efter kopieringen för att säkerställa att den senaste datan återspeglas. Lycka till med kodandet!

## Vad du bör lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur du duplicerar arbetsblad och bevarar pivottabeller i Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Hur du kopierar pivottabell i Java – Komplett Aspose.Cells‑guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Hur du kopierar område och bevarar en pivottabell i Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}