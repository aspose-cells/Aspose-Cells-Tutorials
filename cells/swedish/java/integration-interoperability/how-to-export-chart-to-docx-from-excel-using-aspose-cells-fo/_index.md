---
category: general
date: 2026-08-20
description: Lär dig hur du exporterar diagram till docx och konverterar Excel‑arbetsbok
  till docx med Aspose.Cells i Java. Steg‑för‑steg‑guide med komplett kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: sv
lastmod: 2026-08-20
og_description: Exportera diagram till docx och konvertera Excel‑arbetsbok till docx
  med Aspose.Cells för Java. Följ denna kompletta, körbara handledning.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Exportera diagram till docx med Aspose.Cells – Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Hur man exporterar diagram till docx från Excel med Aspose.Cells för Java
url: /sv/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera diagram till docx från en Excel-arbetsbok med Java

Om du behöver **export chart to docx** direkt från en Excel‑fil, visar den här handledningen en färdig‑att‑köra‑lösning. I slutet av guiden kommer du också att veta hur du **convert Excel workbook to docx** samtidigt som du bevarar ett redigerbart diagram, så att det resulterande Word‑dokumentet kan ändras utan att förlora kvalitet.

Att exportera diagram är vanligt när du skapar rapporter som kombinerar kalkylbladsberäkningar med rika Word‑layouter. Aspose.Cells for Java gör konverteringen enkel, och API‑et låter dig behålla diagrammet redigerbart—ingen statisk bild behövs.

## Vad den här handledningen täcker

* Laddar en befintlig arbetsbok som innehåller ett diagram.  
* Konfigurerar `ImageOrPrintOptions` för att rikta in sig på DOCX‑formatet.  
* Aktiverar flaggan `ExportEditableCharts` (tillgänglig från version 25.10).  
* Sparar arbetsboken som en DOCX‑fil som behåller ett redigerbart diagram.  

Inga externa verktyg behövs utöver Aspose.Cells‑JAR‑filen. Koden fungerar med Java 8+ och vilken recent version av Aspose.Cells som helst.

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| **Aspose.Cells for Java** (v25.10 or later) | Funktionen `setExportEditableCharts` introducerades i denna version. |
| **Java Development Kit (JDK) 8 or newer** | Tillhandahåller runtime för att kompilera och köra exemplet. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Diagrammet är det objekt som kommer att exporteras till DOCX. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Förenklar hantering av beroenden och körning. |

Du kan ladda ner den senaste Aspose.Cells JAR‑filen från [Aspose website](https://products.aspose.com/cells/java/).

## Steg 1: Ställ in projektet och lägg till Aspose.Cells‑beroendet

Om du använder Maven, lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

För Gradle, lägg till:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** Använd exakt den version som introducerade `ExportEditableCharts` (25.10) eller någon nyare version. Äldre versioner kommer att ignorera flaggan och producera en statisk bild istället.

## Steg 2: Ladda arbetsboken som innehåller diagrammet

`Workbook`‑klassen representerar hela Excel‑filen. Att ladda den är en endaste‑rad‑operation:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Varför detta är viktigt:** Arbetsboken måste vara helt inläst innan du kan tillämpa några exportalternativ. Om filsökvägen är felaktig kastar Aspose.Cells ett `FileNotFoundException`.

## Steg 3: Konfigurera bild-/utskriftsalternativ för DOCX‑utdata

`ImageOrPrintOptions` styr hur arbetsboken renderas. Genom att sätta sparformatet till `DOCX` instrueras Aspose.Cells att producera ett Word‑dokument istället för en bild.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Du kan också justera sidstorlek, DPI eller bildkvalitet här, men de är valfria för diagramexport.

## Steg 4: Aktivera export av redigerbara diagram

Från version 25.10 och framåt kan Aspose.Cells bädda in diagram som inbyggda Word‑diagramobjekt. Detta gör dem fullt redigerbara i Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Särskilt fall:** Om du sätter denna flagga till `false` (eller utelämnar den) kommer diagrammet att renderas som en statisk bild. Använd `true` endast när målgruppen behöver redigera diagrammet efter konvertering.

## Steg 5: Spara arbetsboken som en DOCX‑fil

Slutligen anropar du `Workbook.save` med de konfigurerade alternativen:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

När programmet är klart, öppna `ChartEditable.docx` i Microsoft Word. Du bör se det ursprungliga diagrammet, och om du högerklickar på det kommer alternativet **Edit Data** att vara tillgängligt—vilket bekräftar att diagrammet verkligen är redigerbart.

## Fullständigt, körbart exempel

Nedan är den kompletta källfilen. Kopiera den till din IDE, ersätt `YOUR_DIRECTORY` med en absolut eller relativ sökväg, och kör den.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Förväntat resultat**

* En fil med namnet `ChartEditable.docx` i den angivna katalogen.  
* När du öppnar filen i Word visas diagrammet exakt som det såg ut i Excel, och du kan dubbelklicka på diagrammet för att redigera dess dataserier.

## Vanliga fallgropar och hur man undviker dem

| Symtom | Orsak | Lösning |
|--------|-------|---------|
| Word visar en **static image** istället för ett redigerbart diagram | `setExportEditableCharts` inte anropad eller använder en version < 25.10 | Se till att flaggan är satt till `true` och att du använder Aspose.Cells 25.10 eller nyare. |
| Den genererade DOCX‑filen är **blank** | Felaktig filsökväg för källarbetsboken eller otillräckliga behörigheter | Verifiera arbetsbokens sökväg och att applikationen har läs‑/skrivrättigheter. |
| Diagramlayouten ser **distorted** ut | Sidinställningarna i Excel (t.ex. dolda rader/kolumner) skiljer sig från Words standardinställningar | Justera `ImageOrPrintOptions` (t.ex. `setOnePagePerSheet(true)`) för att kontrollera skalning. |
| **Performance** försämras i stora arbetsböcker | Export av många diagram eller stora datamängder | Exportera endast de nödvändiga bladen eller använd `setSheetIndex` för att begränsa bearbetningen. |

## Utöka lösningen

* **Multiple charts:** Iterera över alla arbetsblad och anropa `worksheet.getCharts()` för att exportera varje diagram individuellt.  
* **Custom DOCX styling:** Efter sparning, använd Aspose.Words för att applicera sidhuvuden, sidfötter eller stilar på det genererade dokumentet.  
* **Batch conversion:** Inslå koden i en loop som bearbetar en katalog med `.xlsx`‑filer och producerar en DOCX för varje.  

## Slutsats

Du har nu en pålitlig metod för att **export chart to docx** och **convert Excel workbook to docx** samtidigt som du bevarar full redigerbarhet av diagrammet. De viktigaste stegen är att ladda arbetsboken, konfigurera `ImageOrPrintOptions` för DOCX, aktivera `ExportEditableCharts` och spara resultatet.

Experimentera med ytterligare alternativ—såsom att ställa in sidmarginaler eller bädda in arbetsbokens formler—för att anpassa utskriften till ditt rapporteringsflöde. När du behöver generera Word‑rapporter från Excel‑data programatiskt, ger detta tillvägagångssätt en ren, underhållbar lösning.

--- 

*Redo att prova? Klona exemplet, uppdatera filsökvägarna och kör programmet. Om du stöter på problem, konsultera Aspose.Cells for Java‑dokumentationen eller utforska de relaterade ämnena nedan.*  

### Relaterade ämnen du kan utforska härnäst

* **convert excel workbook to pdf** – generera PDF‑rapporter från samma arbetsbok.  
* **Aspose.Cells chart formatting** – anpassa färger, markörer och axlar innan export.  
* **Embedding images in DOCX with Aspose.Words** – kombinera diagram med annat Word‑innehåll.  

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar Excel‑diagram med trendlinje och exporterar till bild med Aspose.Cells för Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automatisera åtkomst till Excel‑diagram med Aspose.Cells Java: En steg‑för‑steg‑guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Anpassa Excel‑diagrammets datalabels med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}