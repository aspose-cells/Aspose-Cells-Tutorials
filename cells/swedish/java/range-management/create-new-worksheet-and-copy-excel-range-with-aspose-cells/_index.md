---
category: general
date: 2026-09-11
description: Skapa ett nytt kalkylblad och kopiera Excel‑område med Aspose.Cells.
  Lär dig hur du kopierar ett område mellan blad samtidigt som pivottabeller bevaras.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: sv
lastmod: 2026-09-11
og_description: Skapa ett nytt kalkylblad och kopiera Excel‑område med Aspose.Cells.
  Denna handledning visar de exakta stegen för att kopiera område mellan blad och
  behålla pivottabeller intakta.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Skapa nytt kalkylblad och kopiera Excel‑område – Aspose.Cells‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Skapa ett nytt arbetsblad och kopiera Excel‑område med Aspose.Cells
url: /sv/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa nytt kalkylblad och kopiera Excel‑intervall med Aspose.Cells

Om du behöver **skapa ett nytt kalkylblad** och flytta data i en Excel‑fil, gör Aspose.Cells det enkelt. Denna guide visar exakt hur du kopierar ett Excel‑intervall från ett blad till ett annat samtidigt som eventuella pivottabeller i intervallet bevaras.

Du kommer att lära dig hur du **kopierar excel‑intervall**, hur du **kopierar intervall mellan blad**, och varför Aspose.Cells `copy`‑metod behåller pivottabelldefinitionerna intakta. Inga externa verktyg krävs – bara ett Java‑projekt med Aspose.Cells‑biblioteket.

## Förutsättningar

Innan du börjar, se till att du har:

- Java 17 eller senare installerat
- Aspose.Cells för Java (version 23.12 eller nyare) tillagd i ditt projekts classpath
- En källarbok (`input.xlsx`) som innehåller en pivottabell i det intervall du vill kopiera
- Grundläggande kunskap om Java‑syntax och Maven/Gradle‑beroendehantering

## Steg 1: Ställ in projektet och importera Aspose.Cells

Skapa ett enkelt Maven‑projekt (eller Gradle, om du föredrar) och lägg till Aspose.Cells‑beroendet:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Importera sedan de nödvändiga klasserna i din Java‑källfil:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Varför detta steg är viktigt*: Genom att importera rätt klasser får du åtkomst till `Workbook`, `Worksheet`, `Range` och `copy`‑metoden som hanterar intervallöverföringen.

## Steg 2: Läs in källarboken

Öppna arbetsboken som innehåller de data du vill kopiera. Följande kod läser in `input.xlsx` från en katalog du anger:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Förklaring*: `Workbook` representerar hela Excel‑filen. Att läsa in den en gång ger dig läs‑/skriv‑åtkomst till varje blad och cellsamling.

## Steg 3: Identifiera källintervallet som inkluderar pivottabellen

Välj bladet som innehåller pivottabellen och definiera exakt vilket cellblock du vill kopiera. I detta exempel kopierar vi cellerna A1 till D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Varför detta är viktigt*: Genom att skapa ett `Range`‑objekt talar du om för Aspose.Cells exakt vilka celler (inklusive inbäddade objekt som pivottabeller) som ska dupliceras.

## Steg 4: **Skapa nytt kalkylblad** som ska ta emot de kopierade data

Nu lägger vi till ett nytt blad i samma arbetsbok. Detta är den punkt där huvudnyckelordet visas:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Förklaring*: Att lägga till ett nytt blad isolerar de kopierade data, vilket gör det enkelt att verifiera att **copy excel range**‑operationen lyckades utan att påverka originalbladet.

## Steg 5: Kopiera intervallet – pivottabellen bevaras automatiskt

Använd `copy`‑metoden för att flytta intervallet från källbladet till destinationsbladet. Aspose.Cells kopierar formler, formatering och pivottabellsdefinitioner:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Varför detta fungerar*: `copy`‑metoden utför en djup kopiering av källcellerna. Den kopierar inte bara värden; den replikerar hela cellstrukturen, inklusive pivottabellens cache. Därför kan du **copy range aspose.cells** och fortfarande se en fungerande pivottabell på det nya bladet.

## Steg 6: Spara arbetsboken med det nya kalkylbladet

Till sist skriver du den modifierade arbetsboken till disk:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Resultat*: `output.xlsx` innehåller nu originalbladet plus ett nytt blad som heter **Copy** och som har exakt samma intervall, pivottabell inkluderad.

## Fullständigt fungerande exempel

När alla delarna sätts ihop blir det kompletta, körbara programmet:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Förväntad output**: Öppna `output.xlsx` i Excel. Du kommer att se ett blad med namnet **Copy** där cellerna A1:D20 innehåller samma data, formatering och en aktiv pivottabell som den ursprungliga.

## Vanliga frågor och kantfall

- **Vad händer om källintervallet innehåller sammanslagna celler?**  
  `copy`‑metoden kopierar även sammanslagningsinformation, så sammanslagna celler förblir oförändrade på destinationsbladet.

- **Kan jag kopiera till en annan arbetsbok?**  
  Ja. Läs in en andra `Workbook`‑instans, skapa ett destinationsintervall i den arbetsboken och anropa `sourceRange.copy(destinationRange)`. Metoden hanterar kors‑arbetsboks‑kopiering automatiskt.

- **Vad händer om destinationsbladet redan har data?**  
  Kopieringsoperationen skriver över eventuella befintliga celler som överlappar destinationsintervallet. För att undvika dataförlust, se till att målområdet är tomt eller använd en annan startcell (t.ex. `"B2"`).

- **Dupliceras pivottabellens cache?**  
  Aspose.Cells återanvänder den ursprungliga pivottabellscachen, vilket innebär att den nya pivottabellen förblir länkad till samma källdata. Om du behöver en oberoende cache måste du återskapa pivottabellen efter kopieringen.

## Tips och bästa praxis

- **Proffstips**: Använd `Workbook.setForceFormulaRecalculation(true)` innan du sparar om ditt intervall innehåller formler som beror på data utanför det kopierade blocket.
- **Var uppmärksam på** stora intervall: att kopiera enorma blad kan förbruka mycket minne. Överväg att kopiera i mindre delar om du får `OutOfMemoryError`.
- **Prestandatips**: Inaktivera skärmuppdatering (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) när du arbetar med väldigt stora filer för att snabba upp kopieringsprocessen.

## Slutsats

Du vet nu hur du **skapar ett nytt kalkylblad** och **kopierar excel‑intervall** mellan blad med Aspose.Cells, samtidigt som pivottabeller och alla cellattribut bevaras. Denna teknik låter dig programatiskt duplicera datablokkar, bygga rapportmallar eller omstrukturera arbetsböcker utan manuell kopiera‑och‑klistra.

Nästa steg är att utforska relaterade ämnen som **copy range aspose.cells** för kors‑arbetsboks‑operationer, automatisera pivottabelluppdateringar eller exportera det kopierade bladet till PDF. Experimentera med olika källintervall och bladnamn för att anpassa lösningen till ditt specifika automationsscenario. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}