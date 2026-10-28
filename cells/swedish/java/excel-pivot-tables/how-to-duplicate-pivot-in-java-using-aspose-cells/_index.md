---
category: general
date: 2026-09-18
description: hur man duplicerar en pivottabell i Java med Aspose.Cells – kopiera en
  pivottabell mellan arbetsböcker snabbt och pålitligt
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: sv
lastmod: 2026-09-18
og_description: hur man duplicerar en pivottabell i Java med Aspose.Cells. Följ den
  här kompletta handledningen för att kopiera en pivottabell mellan arbetsböcker med
  ren Java‑kod.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplicera en pivottabell i Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man duplicerar pivottabell i Java med Aspose.Cells
url: /sv/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du duplicerar en pivot i Java med Aspose.Cells

Om du behöver **duplicera en pivot** i en Java‑applikation visar den här guiden dig de exakta stegen. Genom att läsa in en Excel‑arbetsbok, definiera pivotens cellområde och kopiera det området till en ny arbetsbok kan du flytta en pivottabell utan att förlora dess definition eller data.

Att kopiera en pivottabell är ett vanligt krav när du genererar rapporter, arkiverar analyser eller delar upp en stor arbetsbok i modulära delar. I den här handledningen kommer du att lära dig hur du **kopierar område mellan arbetsböcker**, hur du **läser in Excel‑arbetsbok Java**, och nyanserna kring **hur du kopierar en pivot** på ett säkert sätt.

Du avslutar med ett färdigt Java‑program som duplicerar en pivottabell från `Source.xlsx` till `PivotCopied.xlsx` med Aspose.Cells för Java.

## Förutsättningar

* JDK 8 eller nyare installerat.
* Maven (eller annat byggverktyg) för att hantera beroenden.
* Aspose.Cells för Java version 23.10 eller senare. Lägg till följande Maven‑beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* En källarbetsbok (`Source.xlsx`) som innehåller en pivottabell i området **A1:H30**.

## Så duplicerar du en pivot i Java

Kärnidén är enkel:

1. **Läs in källarbetsboken** – detta ger dig åtkomst till kalkylbladet som innehåller pivoten.
2. **Definiera cellområdet** som omger pivoten.
3. **Skapa en destinationsarbetsbok** – en tom fil som ska ta emot det kopierade området.
4. **Kopiera området** – Aspose.Cells duplicerar automatiskt pivotdefinitionen.
5. **Spara destinationsarbetsboken** – du har nu en separat fil med samma pivot.

Nedan finns ett komplett, körbart Java‑program som följer dessa steg:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Varför detta fungerar

* **Aspose.Cells** behandlar en pivottabell som en del av kalkylbladets cellsamling. När du anropar `copyRange` kopierar biblioteket inte bara cellvärden utan även den underliggande pivot‑cachen och definitionen, så den nya arbetsboken innehåller en fullt funktionell kopia.
* `CopyOptions`‑objektet har som standard att bevara formler, format och inbäddade objekt. Du kan anpassa det (t.ex. `setCopyColumnWidths(true)`) om du behöver extra kontroll.

## Kopiera område mellan arbetsböcker – djupare titt

Även om exemplet ovan kopierar ett enda sammanhängande block kan `copyRange` hantera vilket rektangulärt område som helst. Om din pivot sträcker sig över icke‑intilliggande områden kan du anropa `copyRange` flera gånger eller använda `Worksheet.copy` för att duplicera hela bladet.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tips:** När du kopierar stora arbetsböcker, aktivera `CopyOptions.setPreserveCellStyle(true)` för att undvika onödig stilduplication, vilket kan förbättra prestandan.

## Så kopierar du en pivot till arbetsbok – hantera flera pivoter

Om källbladet innehåller mer än en pivot kan du iterera över kalkylbladets pivottabeller och kopiera varje enskild separat:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Detta tillvägagångssätt säkerställer att varje pivot behåller sitt ursprungliga namn och datakälla.

## Läs in Excel‑arbetsbok Java – vanliga fallgropar

* **Filvägsavgränsare:** Använd snedstreck (`/`) eller `File.separator` för att hålla koden plattformsoberoende.
* **Saknad licens:** Aspose.Cells fungerar i evalueringsläge, men utdata kommer att innehålla ett vattenmärke. Registrera en licens med `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` innan du läser in arbetsboken för att ta bort vattenmärket.
* **Stora filer:** För arbetsböcker större än 100 MB, överväg att använda `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` med streaming‑alternativ för att minska minnesförbrukningen.

## Fullständig end‑to‑end‑exempel‑sammanfattning

När du sätter ihop allt, här är det slutgiltiga programmet som du kan kopiera‑klistra in i din IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Förväntat resultat:** Efter körning visas `PivotCopied.xlsx` i den angivna katalogen. När du öppnar den i Excel visas samma pivottabell‑layout, filter och data som i `Source.xlsx`. Alla beräknade fält och formatering är bevarade.

## Vanliga frågor

* **Fungerar detta med äldre Excel‑format (.xls)?**  
  Ja. Aspose.Cells upptäcker automatiskt formatet. Använd `new Workbook("file.xls")` så gäller samma kopieringslogik.

* **Vad händer om pivoten refererar till externa datakällor?**  
  Kopian behåller den ursprungliga referensen till datakällan. Om destinationsmiljön inte kan nå den källan kommer pivoten att visa `#REF!`‑fel. För att undvika detta, uppdatera pivoten efter kopiering eller ändra dess datakälla via `PivotTable.setDataSource(...)`.

* **Kan jag kopiera en pivot till ett specifikt bladnamn?**  
  Absolut. Efter att du skapat destinationsarbetsbladet, byt namn på det:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Slutsats

Du vet nu **hur du duplicerar pivottabeller** i Java med Aspose.Cells, hur du **kopierar område mellan arbetsböcker**, och bästa praxis för **läsa in Excel‑arbetsbok Java**. Genom att följa den femstegsprocess – läsa in, definiera, skapa destination, kopiera och spara – kan du automatisera rapportgenerering, arkivera analyser eller dela upp komplexa arbetsböcker utan att förlora pivottabellens funktionalitet.

Nästa steg, utforska relaterade ämnen som **kopiera pivot till arbetsbok** med flera blad, eller integrera den duplicerade pivoten i en större databehandlingspipeline med Apache POI för icke‑Aspose‑scenarier. Experimentera med olika `CopyOptions`‑inställningar för att finjustera prestandan för massiva arbetsböcker.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur du skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hur du uppdaterar Excel‑pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Gruppera pivotfält i Excel‑arbetsböcker med Aspose.Cells för Java – Omfattande guide](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}