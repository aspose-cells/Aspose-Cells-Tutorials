---
category: general
date: 2026-08-04
description: Kopiera pivottabell med Aspose.Cells för Java. Lär dig hur du kopierar
  ett Excel‑område, duplicerar en pivottabell och kopierar ett kalkylblad med pivottabell
  på bara några rader.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: sv
lastmod: 2026-08-04
og_description: Kopiera pivottabell med Aspose.Cells för Java. Denna handledning guidar
  dig genom att kopiera ett Excel‑område, duplicera en pivottabell och bevara all
  data i ett nytt kalkylblad.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Kopiera pivottabell i Java – fullständig Aspose.Cells-handledning
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Kopiera pivottabell i Java – steg‑för‑steg guide med Aspose.Cells
url: /sv/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell i Java – steg‑för‑steg guide med Aspose.Cells

Om du behöver **kopiera en pivottabell** från ett kalkylblad till ett annat i Java, visar den här guiden exakt hur du gör det med Aspose.Cells. Oavsett om du genererar rapporter programatiskt eller bygger ett datamigrationsverktyg, kommer du att se ett komplett, körbart exempel som bevarar pivottabellens definition och data.

Att kopiera en pivottabell är mer än att bara kopiera ett cellområde; den underliggande cachen och datakällan måste förbli intakta. I den här tutorialen täcker vi också hur man **kopierar excel‑område**, hur man **duplicerar pivottabell** över kalkylblad, och hur man **kopierar kalkylblad med pivottabell** med samma API.

## Förutsättningar

Innan du börjar, se till att du har:

* Java Development Kit (JDK) 8 eller nyare.
* Maven eller Gradle för att hantera beroenden.
* Aspose.Cells för Java (senaste versionen, t.ex. 23.12). Lägg till följande Maven‑koordinat i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* En källarbok (`Source.xlsx`) som innehåller en pivottabell på det första kalkylbladet.

## Så kopierar du pivottabell i Java med Aspose.Cells

Kärnidén är att kopiera *källområdet* som omger pivottabellen och sedan klistra in det i ett nytt kalkylblad. Aspose.Cells kopierar automatiskt pivottcachen, så det resulterande bladet innehåller en fullt funktionell **duplicerad pivottabell**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Varför detta fungerar

* **Range copy includes the pivot cache** – Aspose.Cells behandlar en pivottabell som ett speciellt objekt inbäddat i cellområdet. När du anropar `Range.copy` kopierar biblioteket både de synliga cellerna och den dolda cachen som driver pivottabellen.
* **No manual recreation needed** – Du behöver inte återskapa pivottabellens fält eller datakälla; duplicaten är klar att uppdateras omedelbart.
* **Works with any Excel version** – Den genererade filen följer Office Open XML (XLSX)-standarden, så Excel 2007+ kan öppna den utan varningar.

## Kopiera excel‑område – återanvänd samma kod för icke‑pivottabell‑data

Om du bara behöver **kopiera excel‑område** utan en pivottabell, gäller samma mönster. Justera bara områdeadressen till den region du vill duplicera.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Metoden `copy` bevarar formler, formatering och kommentarer, vilket gör den till en universell lösning för vilket Excel‑datablock som helst.

## Duplicera pivottabell över flera kalkylblad

Ibland behöver du **duplicera pivottabell** flera gånger—t.ex. en per avdelning. Loopa över destinationskalkylbladen och återanvänd samma `sourceRange.copy`‑anrop:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

## Kopiera kalkylblad med pivottabell – bevara blad‑nivåinställningar

Om du vill **kopiera kalkylblad med pivottabell** samtidigt som du behåller sidinställningar, kolumnbredder och namngivna områden, använd `Worksheet.copy` istället för att kopiera ett område manuellt. Denna metod klonar hela bladet, inklusive pivottabellen.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` är praktisk när kalkylbladet innehåller diagram, bilder eller anpassade stilar som måste följa med pivottabellen.

## Vanliga fallgropar och hur du undviker dem

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivotcache förlorad efter kopiering** | Att använda `Cell.copy` på enskilda celler (istället för ett område) kastar den dolda cachen. | Kopiera alltid det *hela* området som omger pivottabellen, som visas i Steg 2. |
| **Källområdet för litet** | Området inkluderar inte pivottabellens dataområde, så det nya bladet visar bara statiska värden. | Utöka adressen (t.ex. `A1:G20`) så att den täcker hela pivottabellen samt eventuella slicers eller filter. |
| **Målbokens version stämmer inte** | Att spara som XLS (legacy) tar bort moderna pivottabellfunktioner. | Spara som XLSX (standard) eller ange explicit `SaveFormat.XLSX`. |
| **Extern datakälla trasig** | Pivottabellen pekar på en datakälla utanför arbetsboken; kopiering bäddar inte in den. | Använd `PivotTable.refreshData()` efter kopiering, eller bädda in källdata i samma arbetsbok. |

## Förväntat resultat

Efter att programmet har körts:

1. `CopyWithPivot.xlsx` visas i `YOUR_DIRECTORY`.
2. När du öppnar filen i Excel visas ett nytt blad med namnet **CopySheet**.
3. **CopySheet** innehåller en fullt funktionell pivottabell som är identisk med originalet, redo att uppdateras.
4. All formatering, filter och beräknade fält bevaras.

Om du öppnar `FullCopy.xlsx` kommer du att se en komplett kopia av det ursprungliga kalkylbladet, inklusive eventuella diagram eller bilder som fanns på källbladet.

## Sammanfattning

* Du har lärt dig hur du **kopierar pivottabell** i Java med Aspose.Cells.
* Samma tillvägagångssätt fungerar för ett enkelt **kopiera excel‑område** eller **copy range java**‑scenario.
* För massoperationer kan du **duplicera pivottabell** över många blad.
* När du behöver hela bladet, **kopiera kalkylblad med pivottabell** med `addCopy`.

## Nästa steg

* Utforska **PivotTable.refreshData()** för att programatiskt uppdatera cachen efter kopiering.
* Kombinera kopieringslogiken med **Excel file streaming** för att hantera stora arbetsböcker utan att ladda in allt i minnet.
* Kolla in Aspose.Cells stöd för **pivot slicers** om dina rapporter förlitar sig på interaktiva filter.

Känn dig fri att anpassa koden till din egen projektstruktur, experimentera med olika områdesstorlekar, eller integrera den i en större databehandlingspipeline. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}