---
category: general
date: 2026-03-01
description: Kopiera pivottabell i Java och bevara pivottabellen, exportera sedan
  Excel till PPTX, inaktivera Excel AutoFilter och använd Smart Marker för JSON‑arrayer
  – fullständig steg‑för‑steg‑guide.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: sv
og_description: Kopiera pivottabell i Java, bevara pivottdefinitionen, exportera till
  PPTX, inaktivera AutoFilter och använd Smart Marker – komplett guide för utvecklare.
og_title: Kopiera pivottabell i Java – bevara den, exportera till PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Kopiera pivottabell i Java – bevara den, exportera till PPTX
url: /sv/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell i Java – bevara den, exportera till PPTX

Har du någonsin behövt **copy pivot table** från en arbetsbok till en annan utan att förlora den underliggande pivottabelldefinitionen? Du är inte den enda som kliar dig i huvudet över detta. I många verkliga projekt kommer du att flytta data runt, och det sista du vill ha är en trasig pivottabell som kastar fel vid körning.  

I den här handledningen går vi igenom en komplett lösning som inte bara **copy pivot table** utan också visar hur du **preserve pivot table** när du kopierar, **export Excel to PPTX**, **disable Excel AutoFilter**, och **use smart marker** för att stoppa in en JSON‑array i en enda cell. I slutet har du ett enda körbart Java‑program som täcker alla fyra scenarierna.

## Förutsättningar

- Java 8 eller nyare (koden fungerar även med Java 11)  
- Aspose.Cells for Java‑biblioteket (version 23.9 eller senare) – du kan hämta det från Maven Central  
- Grundläggande kunskap om Excel‑koncept som pivottabeller, tabeller och textrutor  

Om du saknar Aspose.Cells‑JAR‑filen, lägg till detta i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Nu, låt oss dyka ner.

## Steg 1: Kopiera pivottabell – bevara pivottabelldefinitionen

När du helt enkelt kopierar cellområdet som innehåller en pivottabell, lämnas pivottmetadata ofta kvar. Aspose.Cells ger oss ett smidigt sätt att behålla definitionen intakt genom att använda `copyRange` med en `CopyOptions`‑instans.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Varför detta fungerar:** `CopyOptions` instruerar Aspose.Cells att föra över allt, inklusive pivot‑cachen och fältinställningarna. Utan den skulle du bara få rena värden och förlora möjligheten att uppdatera pivottabellen.

**Edge case:** Om din källpivottabell sträcker sig över mer än det hårdkodade `A1:G20`, justera området därefter eller använd `sourceSheet.getPivotTables().get(0).getDataRange()` för att hämta det dynamiskt.

![Exempel på kopiering av pivottabell](image.png "Kopiera pivottabell i Java")

*Bildtext: diagram för kopiera pivottabell i Java*

## Steg 2: Exportera ett kalkylblad med en redigerbar textruta till PPTX

Ofta behöver du omvandla ett Excel‑blad till en PowerPoint‑bild—tänk på veckovisa instrumentpaneler som måste presenteras. Aspose.Cells kan direkt spara ett kalkylblad som en PPTX‑fil samtidigt som former som textrutor bevaras.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Vad som händer:** `save`‑metoden med `SaveFormat.PPTX` konverterar hela bladet, inklusive eventuell redigerbar TextBox, till en PowerPoint‑bild. Texten i rutan förblir redigerbar när du öppnar PPTX‑filen i PowerPoint.

**Tips:** Om du har flera blad och bara vill ha ett specifikt, anropa `wb.getWorksheets().removeAt(index)` för de andra innan du sparar.

## Steg 3: Inaktivera Excel AutoFilter från en tabell

AutoFilter är praktiskt för slutanvändare, men ibland behöver du programatiskt stänga av det—kanske innan du exporterar data eller när du genererar en ren rapport. Så här **disable excel autofilter** på en Excel‑tabell.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Varför du kan behöva detta:** Export till format som inte stödjer AutoFilter (som CSV eller PDF) kan leda till att oönskade filterikoner visas. Att inaktivera det säkerställer ett rent resultat.

**Vanligt fallgropp:** Om bladet saknar tabeller, kommer `getTables().get(0)` att kasta ett `IndexOutOfBoundsException`. Kontrollera alltid `sheet.getTables().size()` först i produktionskod.

## Steg 4: Använd Smart Marker – infoga en JSON‑array som ett enda cellvärde

Smart Marker är Asposes mallmotor. Ett praktiskt trick är att behandla en hel JSON‑array som ett enda cellvärde, vilket är perfekt för loggning eller för att skicka strukturerad data vidare. Låt oss **use smart marker** för att uppnå detta.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Hur det fungerar:** Markören `${json}` i arbetsboken ersätts med hela JSON‑strängen eftersom vi har satt `ArrayAsSingle`. Utan detta alternativ skulle Aspose försöka expandera varje array‑element till separata rader.

**Variation:** Om du behöver att arrayen delas upp över rader, utelämna helt enkelt `ArrayAsSingle` och låt Smart Marker hantera expansionen automatiskt.

## Fullständigt fungerande exempel – alla steg kombinerade

Nedan är en enda Java‑klass som kedjar ihop alla operationer vi har gått igenom. Kör den som en vanlig `main`‑metod; justera bara filsökvägarna så att de matchar din miljö.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}