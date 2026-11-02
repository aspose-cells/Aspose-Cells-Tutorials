---
category: general
date: 2026-09-08
description: Hur man kopierar ett område i Java med Aspose.Cells – lär dig att kopiera
  pivottabell, duplicera pivottabell och exportera pivottabell samtidigt som du bevarar
  formateringen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: sv
lastmod: 2026-09-08
og_description: Hur man kopierar ett område i Java med Aspose.Cells. Denna handledning
  visar hur du kopierar pivottabell, duplicerar pivottabell och exporterar pivottabell
  samtidigt som formateringen bevaras.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Hur man kopierar område i Java – komplett Aspose.Cells-guide
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man kopierar ett område i Java med Aspose.Cells
url: /sv/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar område i Java med Aspose.Cells

Om du behöver **how to copy range** i Java, gör Aspose.Cells uppgiften enkel. Oavsett om du flyttar ett vanligt cellblock eller en fullutrustad pivottabell, hanterar biblioteket kopieringsoperationen samtidigt som formler, stilar och pivottabellens cache behålls. I den här guiden kommer du att lära dig att **copy pivot table**, **duplicate pivot table**, och till och med **export pivot table** till en ny arbetsbok med full formatering.

Handledningen täcker allt från projektuppsättning till det sista verifieringssteget, så att du kan köra koden omedelbart efter att ha läst. Inga externa verktyg krävs förutom Aspose.Cells for Java JAR.

## Förutsättningar

- Java 17 (eller någon annan stödd JDK) installerad och konfigurerad i din IDE.
- Maven eller Gradle för beroendehantering (exemplen använder Maven).
- En käll‑Excel‑fil (`source.xlsx`) som innehåller en pivottabell i området `A1:H20`.
- Grundläggande kunskap om Java‑programmering.

## Steg 1: Lägg till Aspose.Cells i ditt projekt

Aspose.Cells är ett kommersiellt bibliotek, men en gratis utvärderingsversion finns tillgänglig. Lägg till beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Om du föredrar Gradle, är motsvarande post:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Att lägga till JAR‑filen ger dig åtkomst till klasserna `Workbook`, `Worksheet`, `Range` och `CopyOptions` som används genom hela guiden.

## Steg 2: Läs in källarboken och välj det första kalkylbladet

Den första delen av **how to copy range** är att öppna arbetsboken som innehåller de data du vill flytta.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Varför detta är viktigt:** Att öppna arbetsboken skapar en representation i minnet som API:et kan manipulera utan att röra den ursprungliga filen på disken.

## Steg 3: Definiera området som innehåller pivottabellen

En pivottabell finns inom ett rektangulärt block. Du måste ange det blocket så att Aspose.Cells vet vad som ska kopieras.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Obs:** Metoden `createRange` **kopierar** ännu inget; den skapar bara ett `Range`‑objekt som pekar på de celler du avser att duplicera.

## Steg 4: Skapa en ny arbetsbok och hämta dess första kalkylblad

Skapa nu destinationsarbetsboken där det kopierade området ska ligga.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Varför en ny arbetsbok?** Att använda en ny fil garanterar att inga dolda stilar eller namngivna områden stör kopieringsoperationen, vilket är särskilt viktigt när du **export pivot table** till en separat fil.

## Steg 5: Kopiera området (inklusive pivottabellen) till destinationsarket

Detta är kärnan i **how to copy range with formatting**. `CopyOptions`‑objektet instruerar Aspose.Cells att bevara allt: värden, formler, stilar och pivottabellens cache.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Kopiera pivottabell:** Eftersom källområdet inkluderar pivottabellen duplicerar API:et automatiskt pivottabellens cache, så det nya kalkylbladet innehåller en fullt funktionell pivottabell som beter sig exakt som originalet.

## Steg 6: Spara destinationsarbetsboken

Skriv slutligen resultatet till disk.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

När du öppnar `dest.xlsx` kommer du att se en exakt kopia av den ursprungliga pivottabellen, komplett med dess formatering, skivare och beräknade fält.

## Förväntat resultat

- `dest.xlsx` innehåller ett kalkylblad med namnet **Sheet1**.
- Cellerna `A1:H20` har samma data och pivottabell som källan.
- Alla cellstilar (teckensnitt, färger, kanter) bevaras.
- Pivottabellen är fullt interaktiv; en uppdatering av den reflekterar de underliggande data i det kopierade området.

## Så kopierar du område med formatering – djupare genomgång

Det föregående exemplet visar det enklaste scenariot, men du kan stöta på variationer som kräver en något annorlunda metod.

### Kopiera pivottabell till en befintlig arbetsbok

Om du behöver **duplicate pivot table** i en arbetsbok som redan har data, använd samma `copyRange`‑anrop men peka på en annan destinationsadress:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Exportera endast pivottabell (utan omgivande data)

Ibland vill du bara ha pivottabellen, inte källdata. Identifiera pivottabellens visningsområde via dess `getPivotTable`‑metod:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Bevara villkorsstyrd formatering

Regler för villkorsstyrd formatering är en del av stilkollektionen. Flaggan `PasteType.ALL` kopierar dem redan, men du kan vara explicit:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Kantfall och felsökning

| Situation | Vad att hålla utkik efter | Rekommenderad åtgärd |
|-----------|---------------------------|----------------------|
| Käll- och destinationsarbetsböcker använder olika Excel‑versioner | Vissa nyare pivottabellfunktioner (t.ex. datamodell) kanske inte renderas korrekt | Använd den senaste versionen av Aspose.Cells och sätt `Workbook.setFileFormatType(FileFormatType.XLSX)` för båda arbetsböckerna |
| Mycket stora pivottabeller (> 10 000 rader) orsakar minnespress | Out‑of‑memory‑fel under kopiering | Aktivera `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` innan inläsning |
| Destinationsarket innehåller redan ett namngivet område med samma namn som källan | Namnkollision leder till fel i `CopyOptions` | Anropa `copyOptions.setIgnoreNameConflicts(true)` |

## Fullt körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en Java‑klass. Det inkluderar alla importeringar, felhantering och kommentarer.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Kör programmet, öppna sedan `dest.xlsx` för att verifiera att pivottabellen fungerar exakt som originalet.

## Slutsats

Du vet nu **how to copy range** i Java med Aspose.Cells, inklusive hur man **copy pivot table**, **duplicate pivot table** och **export pivot table** samtidigt som all formatering bevaras. Biblioteket abstraherar bort de lågnivå‑detaljer i Excels XML‑struktur, så att du kan fokusera på affärslogiken.

### Nästa steg

- Utforska **copy range with formatting** för diagram och bilder (använd `PasteType.PICTURES`).
- Automatisera batch‑bearbetning: loopa över flera källfiler och konsolidera deras pivottabeller i en sammanfattningsarbetsbok.
- Kombinera denna teknik med Aspose.Slides för att generera PowerPoint‑rapporter som bäddar in den kopierade pivottabellen

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells – A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}