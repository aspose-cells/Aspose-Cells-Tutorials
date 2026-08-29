---
category: general
date: 2026-08-17
description: Hur man duplicerar kalkylblad i Java med Aspose.Cells, bevarar pivottabellen,
  kopierar pivottabellen till en ny arbetsbok och skapar en arbetsbok från ett blad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: sv
lastmod: 2026-08-17
og_description: Hur man duplicerar kalkylblad i Java med Aspose.Cells, bevarar pivottabellen,
  kopierar pivottabellen till en ny arbetsbok och skapar en arbetsbok från ett blad
  – alla steg förklarade.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Hur man duplicerar kalkylblad och behåller pivottabeller – Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Hur man duplicerar kalkylblad och bevarar pivottabeller i Java
url: /sv/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man duplicerar kalkylblad och bevarar pivottabeller i Java

Att duplicera ett kalkylblad samtidigt som pivottabellen förblir intakt är ett vanligt behov när du automatiserar Excel‑rapportering. Denna guide visar hur du kopierar en pivottabell till en ny arbetsbok med Aspose.Cells för Java, och täcker också hur du bevarar pivottabellen när du skapar en arbetsbok från ett blad.

Du kommer att lära dig hur du laddar en befintlig arbetsbok, duplicerar kalkylbladet som innehåller en pivottabell och sparar resultatet som en ny fil. Handledningen förutsätter att du har en grundläggande Java‑utvecklingsmiljö och en giltig Aspose.Cells‑licens (den kostnadsfria utvärderingen fungerar för testning). Inga externa verktyg krävs förutom Aspose.Cells‑JAR‑filen.

## Förutsättningar

* Java Development Kit (JDK) 8 eller nyare.
* Maven eller Gradle för att hantera Aspose.Cells‑beroendet.
* En Excel‑fil (`source.xlsx`) som innehåller minst en pivottabell på det första kalkylbladet.
* En katalog där du kan läsa källfilen och skriva den duplicerade arbetsboken.

Lägg till Aspose.Cells‑beroendet i din `pom.xml` (Maven) eller `build.gradle` (Gradle). För Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Så duplicerar du ett kalkylblad med en pivottabell

Kärnoperationen är en trestegsprocess: ladda, kopiera och spara. Varje steg förklaras nedan.

### Steg 1 – Ladda arbetsboken som innehåller pivottabellen

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Varför detta steg är viktigt*: `Workbook`‑objektet representerar hela Excel‑filen. Genom att hämta det första kalkylbladet (`get(0)`) riktar du in dig på bladet som innehåller den pivottabell du vill duplicera.

### Steg 2 – Skapa en ny arbetsbok och duplicera hela kalkylbladet

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` klonar kalkylbladet **inklusive** alla inbäddade objekt, formler och pivottcache‑data. Detta är det rekommenderade sättet att **kopiera pivottabell** eftersom pivottdefinitionen och dess datakälla överförs tillsammans.

### Steg 3 – Spara den nya arbetsboken

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Efter körning innehåller `copy_with_pivot.xlsx` en exakt kopia av det ursprungliga bladet, och pivottabellen fungerar utan ytterligare konfiguration.

**Förväntat resultat**: När du öppnar `copy_with_pivot.xlsx` i Excel visas det duplicerade kalkylbladet med samma pivottabellslayout, filter och beräknade fält som källfilen.

## Så kopierar du en pivottabell till en annan arbetsbok

Om du behöver flytta en pivottabell utan att kopiera hela bladet kan du extrahera pivottcachen och bifoga den till ett nytt kalkylblad. Följande kodsnutt demonstrerar detta tillvägagångssätt:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Denna kod svarar på **hur man kopierar pivottabell** genom att bara kopiera pivottobjektet, inte hela kalkylbladet. Metoden `addCopy` på `PivotTables`‑samlingen säkerställer att pivottcachen dupliceras, vilket uppfyller kraven för **hur man bevarar pivottabell**.

## Så bevarar du pivottabellen när du skapar en arbetsbok från ett blad

Ibland börjar du med ett blad som inte tillhör någon arbetsbok (t.ex. du genererar ett blad i minnet). För att **skapa arbetsbok från blad** samtidigt som du behåller pivottabellen, följ dessa steg:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Genom att lägga till kalkylbladet i en ny `Workbook` efter att pivottabellen är fullständigt definierad, garanterar du att **hur man bevarar pivottabell** fungerar även när kalkylbladet har skapats utanför en befintlig fil.

## Praktiska tips och vanliga fallgropar

| Tip | Varför det är viktigt |
|-----|-----------------------|
| Använd `addCopy` istället för `copy` | `addCopy` klonar den underliggande pivottcachen; en vanlig `copy` kan förlora anslutningen till datakällan. |
| Behåll käll- och destinationsfiler på samma filsystem | Relativa sökvägar i pivottabellens datakälla löses korrekt, vilket minskar felmeddelanden som “source not found”. |
| Verifiera pivottcachen efter kopiering | Anropa `pivot.refresh()` om källdata har ändrats mellan kopieringen och sparandet. |
| Frigör arbetsböcker när du är klar | `sourceWorkbook.dispose();` frigör inhemska resurser, vilket är viktigt för stora filer. |

## Kantfall du kan stöta på

* **Flera kalkylblad med ömsesidigt beroende pivottabeller** – Kopiera varje kalkylblad individuellt; delade cachar dupliceras automatiskt, men du kan behöva omdefiniera externa datakopplingar.
* **Pivottabeller baserade på externa SQL‑frågor** – Säkerställ att målmiljön kan nå samma databas; annars visar pivottabellen felmeddelandet “#REF!”.
* **Stora arbetsböcker (>100 MB)** – Använd `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` för att minska minnesbelastningen under kopieringsoperationen.

## Fullständigt, körbart exempel

Nedan är det fullständiga programmet som inkluderar alla steg som diskuterats. Spara det som `CopyPivotTable.java`, justera filsökvägarna och kör det med din föredragna IDE eller via `javac`/`java`.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hur man uppdaterar Excel-pivottabellens källa med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hur man implementerar skivare i pivottabeller med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}