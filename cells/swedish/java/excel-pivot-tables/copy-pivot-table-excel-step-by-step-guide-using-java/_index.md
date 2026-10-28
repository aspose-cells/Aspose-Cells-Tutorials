---
category: general
date: 2026-06-27
description: Kopiera pivottabell i Excel med Java på några minuter – lär dig hur du
  kopierar ett område till en annan arbetsbok och upptäck hur du kopierar pivottabeller
  effektivt.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: sv
og_description: Kopiera pivottabell i Excel med Java. Den här guiden visar hur man
  kopierar ett område till en annan arbetsbok och besvarar hur man kopierar en pivottabell
  med ett komplett exempel.
og_title: Kopiera pivottabell Excel – Java-handledning
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Kopiera pivottabell i Excel – Steg‑för‑steg guide med Java
url: /sv/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell Excel – Java‑handledning

Har du någonsin undrat hur man **copy pivot table excel** filer utan att förlora de underliggande datakonnectionerna? Du är inte ensam. Många utvecklare stöter på problem när de försöker flytta en pivottabell från en arbetsbok till en annan, bara för att sluta med ett statiskt område eller en trasig referens.  

Den goda nyheten? Med några rader Java och rätt bibliotek kan du **copy pivot table excel** arbetsböcker på ett rent sätt, och bevara varje fält, filter och layout. I den här guiden visar vi också **how to copy pivot table** med Aspose.Cells för Java‑API, och vi strör in tips om **copy range to another workbook** för de där kant‑fallsscenarierna.

> **Vad du får med dig:** ett fullt körbart program som laddar en källarbetsbok, kopierar det pivottabell‑innehållande området, och sparar en ny arbetsbok som ser exakt ut som originalet.

## Förutsättningar

- Java 17 eller nyare (koden kompileras med vilken recent JDK som helst).
- Aspose.Cells för Java 23.10 eller senare – gratis provversion fungerar bra för testning.
- En käll‑Excel‑fil (`source.xlsx`) som redan innehåller en pivottabell på det första kalkylbladet.
- En IDE eller en enkel kommandorads‑byggmiljö (Maven/Gradle).

Inga andra externa beroenden krävs.

## Steg 1: Ställ in projektet och importera klasser

Först, skapa ett Maven‑projekt (eller Gradle, om du föredrar) och lägg till Aspose.Cells‑beroendet:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Importera nu de klasser vi kommer att behöva:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro‑tips:** Håll din `src/main/resources`‑mapp prydlig; placera `source.xlsx` där och referera den med en relativ sökväg för att undvika hårdkodade absoluta kataloger.

## Steg 2: Ladda källarbetsboken som innehåller pivottabellen

Den första raden i varje **copy pivot table excel**‑operation är att ladda arbetsboken som innehåller den pivottabell du vill duplicera.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Varför laddar vi hela arbetsboken istället för bara bladet? Eftersom pivot‑cachen finns på arbetsboksnivå; att bara kopiera bladet skulle bryta cachen och din pivottabell skulle bli ett vanligt område.

## Steg 3: Hämta kalkylbladet och definiera pivottabell‑området

Därefter hittar vi kalkylbladet och det exakta cellblocket som omsluter pivottabellen. I de flesta fall börjar pivottabellen på `A1`, men du bör justera området så att det matchar din fil.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

Om du är osäker på området kan du låta Aspose.Cells beräkna de använda cellerna:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

Den lilla kodsnutten är praktisk när du behöver **copy range to another workbook** utan att hårdkoda adressen.

## Steg 4: Skapa målarbetsboken

Nu skapar vi en ny arbetsbok som ska ta emot den kopierade pivottabellen. Detta är kärnan i **how to copy pivot table** — du skapar en ren tavla och klistrar sedan in området.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

Om du redan har en mallfil du vill berika, ersätt bara konstruktorn med `new Workbook("template.xlsx")`.

## Steg 5: Lägg till ett kalkylblad i målarbetsboken

Även om en ny `Workbook` redan innehåller ett standardsblad, lägger vi till ett andra blad för att demonstrera processen att kopiera till en specifik plats.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

Du kan byta namn på bladet för tydlighet:

```java
dstWs.setName("CopiedPivot");
```

## Steg 6: Kopiera området – pivottabellen bevaras

Här är den magiska raden som faktiskt **copy range to another workbook** samtidigt som pivottabellen förblir intakt. `CopyOptions`‑objektet instruerar Aspose.Cells att bevara allt, inklusive pivot‑cachen.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Varför sätter vi `PasteType.PASTE_ALL`? För att standardklistra‑operationen bara kopierar värden och formatering, och kastar bort pivot‑cachen. Genom att explicit begära `PASTE_ALL` säkerställer vi att målarbetsboken får en fullt funktionell pivottabell.

## Steg 7: Spara målarbetsboken

Slutligen skriver du den nya filen till disk. Efter detta steg kan du öppna `destination.xlsx` i Excel och se pivottabellen exakt som den såg ut i källfilen.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Förväntat resultat

- Att öppna `destination.xlsx` visar ett blad med namnet **CopiedPivot**.
- Bladet innehåller en pivottabell som kan uppdateras, filtreras och omarrangeras precis som originalet.
- Inga felmeddelanden visas i konsolen, vilket bekräftar att **copy pivot table excel** lyckades.

## Vanliga frågor & kantfall

### Vad händer om källarbetsboken har flera pivottabeller?

Du kan upprepa logiken för områdesval för varje pivottabell, eller så kan du kopiera hela kalkylbladet:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Kopierar du hela bladet flyttas också alla pivot‑cacher, vilket gör det till ett snabbt sätt att **copy range to another workbook** när du har många tabeller.

### Hur hanterar man externa datakonnectioner?

Om din pivottabell hämtar data från en extern databas, kommer målarbetsboken att behålla anslutningssträngen. För att undvika brutna länkar, uppdatera anslutningen efter kopiering:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Fungerar detta med .xls‑filer?

Ja. Aspose.Cells abstraherar filformatet, så samma kod fungerar för `.xls`, `.xlsx`, `.xlsb` och även `.ods`. Ändra bara filändelsen i `Workbook`‑konstruktörerna.

## Fullt fungerande exempel

Sätter vi ihop allt, här är en klar‑för‑körning Java‑klass som demonstrerar **how to copy pivot table** från en arbetsbok till en annan:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Kör klassen, öppna `destination.xlsx`, och du kommer att se den exakta kopian av den ursprungliga pivottabellen. 🎉

## Slutsats

Vi har just gått igenom ett komplett **copy pivot table excel**‑arbetsflöde med Java. Genom att ladda källarbetsboken, identifiera pivottabell‑området och använda `CopyOptions` med `PASTE_ALL` kan du på ett pålitligt sätt **copy range to another workbook** samtidigt som du bevarar varje pivot‑funktion.  

Om du är nyfiken på **how to copy pivot table** i andra språk, gäller samma koncept — byt bara ut Aspose.Cells‑SDK‑et mot den lämpliga plattformen. Därefter kan du utforska att programatiskt uppdatera den kopierade pivottabellen, eller exportera den till PDF för rapporteringsändamål.  

Har du en variant på detta scenario? Kanske behöver du kopiera ett diagram som är länkat till en pivottabell, eller du vill batch‑processa dussintals filer. Dessa ämnen är naturliga vidareutvecklingar av det vi täckte idag.  

Kör koden, justera området, och låt dina Excel‑automatiseringsäventyr börja. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man uppdaterar Excel-pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatisera Excel-pivottabellens styling och sparande med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipulering av Excel-pivottabeller med Aspose.Cells Java: En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}