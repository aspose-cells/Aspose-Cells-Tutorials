---
category: general
date: 2026-08-17
description: Lär dig hur du skapar duplicerade detaljblad med Aspose.Cells för Java
  och tillåter duplicerade bladnamn med SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: sv
lastmod: 2026-08-17
og_description: Skapa dubblett‑detaljblad i Aspose.Cells för Java och tillåt dubblettbladnamn.
  Följ den här kompletta handledningen för omedelbara resultat.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Skapa duplicerade detaljblad i Aspose.Cells för Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man skapar duplicerade detaljblad i Aspose.Cells för Java
url: /sv/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar duplicerade detaljblad i Aspose.Cells för Java

Om du behöver **skapa duplicerade detaljblad** i en Excel-arbetsbok, gör Aspose.Cells för Java det enkelt. Denna handledning visar exakt hur du tillåter duplicerade bladnamn när du genererar detaljblad med SmartMarkerProcessor, så att du kan skapa en arbetsbok som innehåller flera blad som delar samma namn.

Du kommer att se ett komplett, körbart exempel, en genomgång av varje konfigurationsalternativ och tips för att hantera vanliga kantfall såsom namnkonflikter och stora datamängder. Inga externa referenser krävs—allt du behöver finns med i koden nedan.

## Förutsättningar

* Java Development Kit (JDK) 8 eller nyare.
* Maven eller Gradle för att hantera beroenden.
* Aspose.Cells för Java-biblioteket (version 23.9 eller senare). Lägg till följande Maven‑beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* En huvudmallarbetsbok (`master_template.xlsx`) som innehåller ett Smart Marker‑område för detaljdata.

## Översikt av lösningen

Lösningen följer fyra logiska steg:

1. Ladda huvudmallarbetsboken.
2. Konfigurera `SmartMarkerProcessor` för att **tillåta duplicerade bladnamn**.
3. Bearbeta arbetsboken så att ett nytt detaljblad skapas för varje datagrupp.
4. Spara den resulterande arbetsboken som nu innehåller duplicerade detaljblad.

Varje steg förklaras i detalj nedan, och den kompletta källfilen finns tillgänglig i slutet av guiden.

## Steg 1: Ladda huvudmallarbetsboken

Den första operationen skapar en `Workbook`‑instans som representerar mallfilen. Mallen måste innehålla en Smart Marker‑platshållare (t.ex. `&=DetailData`) som instruerar processorn var data ska infogas.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Varför detta är viktigt:** Att ladda mallen isolerar layout och formatering från logiken för datagenerering, vilket håller din kod ren och gör det enkelt att återanvända samma mall för olika datamängder.

## Steg 2: Konfigurera SmartMarkerProcessor för att tillåta duplicerade bladnamn

Som standard genererar Aspose.Cells unika bladnamn när detaljblad skapas. För att **tillåta duplicerade bladnamn**, sätt `DetailSheetNewName`‑alternativet till ett konstant värde. Processorn kommer att återanvända detta namn för varje genererat blad.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Varför detta är viktigt:** Genom att sätta `DetailSheetNewName` talar du om för motorn att återanvända samma namn för varje detaljblad, vilket direkt uppfyller kravet att **tillåta duplicerade bladnamn**. Detta tillvägagångssätt är användbart när efterföljande verktyg identifierar blad efter deras position snarare än deras namn.

## Steg 3: Bearbeta arbetsboken för att generera detaljbladen

Efter konfiguration, anropa `process` på arbetsboken. Processorn läser Smart Marker‑området, skapar ett nytt blad för varje datagrupp och fyller det med motsvarande rader.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Varför detta är viktigt:** `process`‑anropet utför det tunga arbetet—parsing av Smart Markers, kloning av mallbladet och infogning av data. Eftersom `DetailSheetNewName`‑alternativet redan är satt, får varje nytt blad samma namn, vilket resulterar i duplicerade bladnamn i den slutliga filen.

## Steg 4: Spara den resulterande arbetsboken

Slutligen, skriv den modifierade arbetsboken till en ny fil. Utdatafilen kommer att innehålla lika många “DetailSheet”-flikar som det finns datagrupper.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Varför detta är viktigt:** Att spara filen slutför de förändringar som processorn gjort. Den resulterande arbetsboken kan öppnas i Microsoft Excel, LibreOffice eller någon annan kalkylprogramvara som stödjer XLSX‑formatet.

## Komplett källkod

När alla delar sätts ihop, här är det fullständiga programmet som du kan kopiera, klistra in och köra:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Förväntat resultat

När du öppnar `duplicate_detail.xlsx` kommer du att se flera flikar namngivna **DetailSheet**. Varje flik innehåller den datamängd som motsvarade en specifik Smart Marker‑grupp i mallen. Layout, formatering och formler från huvudmallen bevaras på varje duplicerat blad.

## Hantera vanliga fallgropar

| Problem | Förklaring | Åtgärd |
|---------|------------|--------|
| Excel visar en varning om duplicerade bladnamn | Excel tillåter duplicerade namn men kan visa en varning när filen öppnas. | Varningen är ofarlig; arbetsboken fungerar korrekt. Om du föredrar att undertrycka varningen, byt namn på bladen efter bearbetning med `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Stora datamängder orsakar hög minnesanvändning | Varje duplicerat blad skapar en fullständig kopia av mallen, vilket kan förbruka RAM. | Aktivera streamingläge med `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` innan mallen laddas. |
| Smart Marker‑område hittades inte | Processorn kan inte hitta `&=DetailData` i mallen. | Verifiera att platshållarsyntaxen matchar datakällan och att mallbladet inte är dolt. |

## Proffstips: anpassa namngivningsschemat för duplicering

Om du behöver ett förutsägbart namnmönster samtidigt som du tillåter duplicering, kombinera ett basnamn med ett index:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

`{0}`‑platshållaren ersätts av bladindexet, vilket ger namn som `DetailSheet_1`, `DetailSheet_2` osv. Detta uppfyller fortfarande kravet att **tillåta duplicerade bladnamn** eftersom basnamnet förblir konstant.

## Nästa steg

Nu när du kan **skapa duplicerade detaljblad**, kan du utforska följande ämnen:

* **Fyll i detaljblad med bilder** – använd `Picture`‑objekt för att bädda in logotyper eller diagram.
* **Tillämpa villkorsstyrd formatering** – lägg till `FormatCondition`‑regler för att markera rader baserat på värden.
* **Exportera till PDF** – anropa `workbook.save("output.pdf", SaveFormat.PDF);` för att generera en PDF‑version av de duplicerade bladen.

Var och en av dessa utökningar bygger på samma Smart Marker‑arbetsflöde som demonstrerats här, vilket låter dig automatisera komplexa Excel‑rapporteringsuppgifter med förtroende.

---

*Du har lärt dig hur man skapar duplicerade detaljblad i Aspose.Cells för Java och hur man tillåter duplicerade bladnamn med SmartMarkerProcessor. Använd koden, anpassa mallen och integrera tekniken i dina rapporteringspipeline.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa och komma åt Excel‑blad, lägg till PDF‑bokmärken med Aspose.Cells för Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Skapa åtkomst till Excel‑blad, lägg till PDF‑bokmärken Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Skapa åtkomst till Excel‑blad, lägg till PDF‑bokmärken Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}