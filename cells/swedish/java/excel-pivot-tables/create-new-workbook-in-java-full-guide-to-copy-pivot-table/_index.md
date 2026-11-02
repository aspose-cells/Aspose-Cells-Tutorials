---
category: general
date: 2026-07-23
description: Skapa en ny arbetsbok i Java och lär dig hur du kopierar pivottabell,
  kopierar Excel‑område och exporterar pivottabell med Aspose.Cells på några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: sv
lastmod: 2026-07-23
og_description: Skapa en ny arbetsbok i Java och kopiera omedelbart pivottabell, kopiera
  Excel‑område och exportera sedan pivottabellen med Aspose.Cells. Följ den här kompletta
  handledningen.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Skapa ny arbetsbok i Java – Kopiera pivottabell steg för steg
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Skapa ny arbetsbok i Java – Fullständig guide för att kopiera pivottabell
url: /sv/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i Java – Fullständig guide för att kopiera pivottabell

Har du någonsin funderat på hur man **skapar ny arbetsbok** i Java samtidigt som man bevarar en komplex pivottabell? Du är inte ensam om att klia dig i huvudet över detta. I många rapporteringsappar måste du flytta en pivottabell från en källfil till en ny arbetsbok, kanske för att skicka den till en kund eller för att köra ytterligare beräkningar. Den goda nyheten? Med några få rader kod kan du göra exakt det—utan manuellt kopiera‑klistra.

I den här handledningen går vi igenom hela processen: läsa in källfilen, definiera området som innehåller pivottabellen, **kopiera Excel‑området**, skapa en **ny arbetsbok** och slutligen **exportera pivottabellen** till en ny fil. När du är klar har du ett självständigt, körbart Java‑program som svarar på frågan “**hur man kopierar pivottabell**” utan gissningar.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- Java 17 eller senare (koden fungerar med vilken modern JDK som helst)
- Aspose.Cells for Java‑biblioteket (gratis provversion eller licensierad version)
- En exempel‑`source.xlsx` som innehåller en pivottabell i området `A1:G20`
- En IDE eller byggverktyg (Maven/Gradle) för att hantera Aspose.Cells‑JAR‑filen

Har du allt? Bra—låt oss komma igång.

## Steg 1: Ställ in projektet och importera Aspose.Cells

Först och främst måste du lägga till Aspose.Cells i ditt projekt. Om du använder Maven, lägg till detta beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Om du föredrar Gradle, är motsvarigheten:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

När biblioteket finns på klassvägen, importera de klasser du kommer att behöva:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells är ett kommersiellt bibliotek, men det erbjuder en fullt fungerande 30‑dagars utvärdering som sätter ett vattenstämpel på resultatet—perfekt för att prova detta.

## Steg 2: Läs in källarbetsboken

Nu ska vi **skapa ny arbetsbok**‑objekt, men först behöver vi källan som innehåller pivottabellen. Detta steg är grunden för alla **copy excel range**‑operationer eftersom område‑objektet vet exakt vilka celler (inklusive pivottabellens cache) som ska överföras.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Varför inte bara läsa in området direkt? För pivottabellens metadata ligger i kalkylbladets pivottabell‑cache, och Aspose.Cells paketerar automatiskt detta när du kopierar området.

## Steg 3: Definiera området som innehåller pivottabellen

I många verkliga filer upptar pivottabellen ett rektangulärt block. I det här exemplet antar vi att den ligger i `A1:G20`. Du kan naturligtvis justera adressen så att den matchar din faktiska layout.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Om du är osäker på den exakta adressen kan du använda `sourceSheet.getCells().getMaxDataRow()` och `getMaxDataColumn()` för att beräkna gränserna dynamiskt. Det är ett praktiskt trick när pivottabellens storlek förändras över tid.

## Steg 4: **Skapa ny arbetsbok** och destinationskalkylblad

Här är ögonblicket då vi faktiskt **skapar ny arbetsbok** som ska ta emot det kopierade innehållet. Tänk på det som en tom duk som du ska klistra pivottabellen på.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Varför börja med en tom arbetsbok? Det garanterar att inga dolda stilar eller tidigare pivottabeller stör kopieringen, vilket ger ett rent resultat redo för **export pivot table**.

## Steg 5: Kopiera pivottabellen (och dess underliggande område)

Nu kommer kärnan i handledningen: **copy pivot table**. Aspose.Cells behandlar en område‑kopiering som en djup kopia, vilket betyder att pivottabellens cache följer med cellerna. Det är därför den här enda raden gör det tunga arbetet.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Om du någonsin har undrat **how to copy pivot** utan att förlora funktionaliteten, är detta svaret. Destinationsbladet innehåller nu en fullt fungerande pivottabell som du kan uppdatera, ändra eller helt enkelt exportera.

### Edge Case: Bevara uppdateringsinställningar

Ibland är källpivottabellen inställd på att uppdateras vid öppning. För att behålla detta beteende kan du kopiera pivottabellens alternativ explicit:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Detta kodstycke säkerställer att den kopierade pivottabellen beter sig exakt som originalet.

## Steg 6: Spara destinationsarbetsboken – **Export Pivot Table**

Till sist **exporterar vi pivottabellen** genom att spara den nya arbetsboken till disk. Du kan välja vilket format som helst som Aspose stödjer: XLSX, XLS, CSV, PDF, osv. För den här guiden håller vi oss till XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Om du behöver skicka filen via en webbtjänst kan du skriva den till en `ByteArrayOutputStream` istället för en filsökväg—Aspose gör detta enkelt.

## Fullt fungerande exempel

Sätter vi ihop allt, får du ett komplett, körbart program. Känn dig fri att kopiera, klistra in och köra det i din IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Förväntad output

När du kör programmet skrivs följande till konsolen:

```
Pivot table copied successfully!
```

Och filen `copied_with_pivot.xlsx` dyker upp i `YOUR_DIRECTORY`. Öppna den i Excel så ser du pivottabellen intakt, redo att uppdateras eller redigeras.

## Vanliga frågor & felsökning

- **Vad händer om källpivottabellen sträcker sig över mer än ett kalkylblad?**  
  Du måste kopiera varje relevant område separat och sedan återskapa pivottabellen på destinationsbladet med hjälp av `PivotTable`‑API:erna.

- **Kan jag bara kopiera pivottabellens layout utan datan?**  
  Sätt `sourceRange.setCopyDataOnly(false)` innan kopieringen. Detta instruerar Aspose att behålla cachen men inte den underliggande källdata.

- **Finns det ett sätt att kopiera pivottabellen till en CSV‑fil?**  
  CSV stödjer inte pivottabeller, men du kan exportera pivottabellens *resultat* genom att anropa `pivotTable.calculate()` och sedan spara bladet som CSV.

- **Varför förlorar den kopierade pivottabellen sin formatering?**  
  Formatering ligger i stil‑samlingen. Efter kopieringen kan du anropa `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` för att överföra stilar.

## Slutsats

Vi har just visat dig hur man **skapar ny arbetsbok** i Java, **kopierar pivottabell** och **exporterar pivottabell**—allt med ett rent, reproducerbart kodexempel. Genom att definiera det exakta **copy excel range**, utnyttja Aspose.Cells djupkopieringssemantik och bevara valfria inställningar kan du automatisera praktiskt taget alla pivottabell‑migrationsuppgifter.

Redo för nästa steg? Prova att byta ut output‑formatet till PDF, eller loopa igenom flera källfiler för att batch‑processa dussintals pivottabeller. Samma mönster gäller—justera bara filsökvägar och områdeadresser.

Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose.Cells‑dokumentationen för avancerad pivottabellshantering. Lycka till med kodandet, och njut av den tid du sparat genom att automatisera de tråkiga kopiera‑klistra‑uppgifterna!

## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}