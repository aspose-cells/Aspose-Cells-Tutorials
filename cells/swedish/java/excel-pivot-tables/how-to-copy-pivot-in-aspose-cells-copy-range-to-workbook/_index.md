---
category: general
date: 2026-08-08
description: Hur man kopierar en pivottabell i Aspose.Cells och kopierar ett område
  till arbetsboken med Java. Lär dig de exakta stegen för att duplicera en pivottabell
  med CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: sv
lastmod: 2026-08-08
og_description: Hur man kopierar en pivottabell i Aspose.Cells och kopierar ett område
  till arbetsboken med Java. Följ den här kompletta guiden för att duplicera en pivottabell
  med hjälp av CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Hur man kopierar pivottabell i Aspose.Cells – kopiera område till arbetsbok
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Hur man kopierar pivottabell i Aspose.Cells – kopiera område till arbetsbok
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här kopierar du pivottabell i Aspose.Cells – kopiera område till arbetsbok

Om du behöver **how to copy pivot** i en Excel-fil med Aspose.Cells, visar den här guiden den exakta processen. I slutet av handledningen kommer du att kunna **copy range to workbook** samtidigt som pivottabellens definition bevaras.

Exemplet använder Java, men samma koncept gäller för alla .NET-språk som fungerar med Aspose.Cells. Inga externa verktyg krävs—bara Aspose.Cells for Java-biblioteket och en grundläggande utvecklingsmiljö.

## Förutsättningar

Innan du börjar, se till att du har:

* Java Development Kit (JDK) 8 eller senare.
* Maven eller Gradle för att hantera beroenden (exemplet använder Maven).
* Aspose.Cells for Java 23.9 (eller den senaste versionen) tillagt i ditt projekt.
* En inmatningsarbetsbok (`input.xlsx`) som innehåller minst en pivottabell på det första kalkylbladet.

Att ha dessa komponenter redo förhindrar körningsfel när koden får åtkomst till arbetsboken.

## Så här kopierar du pivottabell med Aspose.Cells

Detta avsnitt går igenom varje steg som krävs för att **how to copy pivot** från en del av ett blad till en annan, med hjälp av klassen `CopyOptions`.

### Steg 1: Lägg till Aspose.Cells i ditt projekt

Om du använder Maven, lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Varför detta steg är viktigt*: Biblioteket tillhandahåller `Workbook`, `CopyOptions` och andra klasser som krävs för **aspose.cells copy range**-operationer. Utan beroendet kan kompilatorn inte lösa dessa typer.

### Steg 2: Läs in källarbetsboken

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Att läsa in filen skapar en minnesrepresentation av kalkylbladet. `Workbook`‑objektet ger dig åtkomst till kalkylblad, celler och pivottabeller.

### Steg 3: Konfigurera kopieringsalternativ för att inkludera pivottabellen

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` talar om för Aspose.Cells att operationen ska bevara pivottabellens metadata. Om du utelämnar detta flagga kommer pivottabellen att reduceras till statisk data, vilket förlorar dess interaktivitet.

### Steg 4: Kopiera önskat område med pivottabellen

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange`‑metoden kopierar celler, formatering och—på grund av alternativen som sattes i föregående steg—alla pivottabeller som skär området. Detta är kärnan i **copy range to workbook**‑funktionaliteten.

### Steg 5: Spara den modifierade arbetsboken

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Spara skriver ändringarna till en ny fil (`output.xlsx`). Du kan nu öppna den här filen i Excel och se att pivottabellen har duplicerats exakt där området kopierades.

## Fullt, körbart exempel

Genom att sätta ihop alla delar får du det kompletta programmet som du kan kompilera och köra:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Förväntat resultat

* `output.xlsx` innehåller samma data som `input.xlsx`.
* Pivottabellen som ursprungligen upptog källområdet visas i destinationscellerna, fullt funktionell (filter, uppdateringsmöjlighet, etc.).
* All cellformatering, formler och kolumnbredder bevaras eftersom `copyRange` kopierar hela cellblocket.

## Vanliga frågor och kantfall

**Vad händer om destinationsområdet överlappar en befintlig pivottabell?**  
Aspose.Cells kommer att skriva över målcellena. För att undvika dataförlust, se till att destinationsområdet är tomt eller flytta den befintliga pivottabellen först.

**Kan jag kopiera en pivottabell över kalkylblad?**  
Ja. Använd `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` där `targetSheetIndex` pekar på destinationsbladet.

**Kopierar `setCopyPivotTable(true)` den underliggande datakällan?**  
Metoden kopierar endast referensen till pivottabellens cache. Om källdata finns i samma arbetsbok kommer destinationens pivottabell att peka på samma cache. För att duplicera cachen måste du skapa en ny pivottabellscache manuellt.

**Hur kopierar man ett stort område effektivt?**  
När du kopierar mycket stora områden, överväg att endast använda `CopyOptions.setCopyFormula(true)` och `setCopyDataValidation(true)` om det behövs. Att minska antalet alternativ kan förbättra prestandan.

## Tips för pålitlig **aspose.cells copy range**-användning

* **Proffstips:** Anropa alltid `workbook.calculateFormula()` efter kopiering om området innehåller formler som beror på pivottabellens cache.
* **Se upp för:** Dolda kalkylblad. `copyRange` fungerar endast på synliga kalkylblad om du inte explicit refererar till det dolda bladet via index.
* **Versionskontroll:** Flaggan `setCopyPivotTable` är tillgänglig från Aspose.Cells 20.9. Säkerställ att din biblioteksversion stöder den.

## Slutsats

Du vet nu **how to copy pivot** i Aspose.Cells och hur du **copy range to workbook** samtidigt som du bevarar full pivottabellfunktionalitet. Stegen—att lägga till biblioteket, läsa in arbetsboken, konfigurera `CopyOptions`, utföra kopieringen och spara—utgör ett återanvändbart mönster som du kan anpassa till andra kopiera‑och‑klistra‑scenarier.

Nästa steg, utforska relaterade ämnen som **aspose.cells copy range** för diagram, villkorsstyrd formatering och datavalidering. Experimentera med att kopiera mellan olika filformat (XLSX → XLS) för att bredda dina automatiseringsmöjligheter. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hur man uppdaterar Excel-pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hur man implementerar slicers i pivottabeller med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}