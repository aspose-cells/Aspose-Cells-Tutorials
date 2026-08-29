---
category: general
date: 2026-07-16
description: Ange anpassad cellseparator vid export av Excel‑tabell till TXT med Aspose.Cells.
  Lär dig hur du exporterar Excel‑formler till text och sparar kalkylbladet som txt‑fil.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: sv
lastmod: 2026-07-16
og_description: Ställ in en anpassad cellseparator i Aspose.Cells gör att du kan exportera
  en Excel‑tabell till TXT med exakt formatering. Exportera Excel‑formler till text
  och spara kalkylbladet som en txt‑fil enkelt.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Ställ in anpassad cellseparator – Exportera Excel‑tabell till TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Ställ in anpassad cellavgränsare – Exportera Excel‑tabell till TXT
url: /sv/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange anpassad cellseparator – Exportera Excel‑tabell till TXT

Att ange en anpassad cellseparator är den hemliga ingrediensen du behöver när du vill ha en prydlig textdump från ett Excel‑ark. Har du någonsin undrat hur man **export excel table to txt** utan att sluta med ett rörigt gäng kommatecken och radbrytningar? I den här handledningen går vi igenom hela processen med Aspose.Cells för Java, från att ladda en arbetsbok till **save worksheet as txt file** med en avgränsare du väljer.

## Vad du kommer att lära dig

- Hur man **set custom cell separator** för textexport.
- De exakta stegen för att **export excel formulas to text** så att de utvärderade värdena följer med.
- Sätt att **export excel data as plain text** samtidigt som layouten bevaras.
- Ett komplett, färdigt‑att‑köra kodexempel som du kan kopiera‑klistra in i ditt projekt.

I slutet av den här guiden kommer du kunna ta vilken Excel‑arbetsbok som helst, välja ett rörtecken (`|`), ett tabbtecken (`\t`) eller vilket tecken du vill, och skapa en ren, avgränsad textfil som nedströmsystem älskar.

### Förutsättningar

- Java 8 eller nyare installerat.
- Maven (eller något annat byggverktyg) för att hämta Aspose.Cells för Java‑biblioteket.
- En exempelarbetsbok (`TableDemo.xlsx`) som innehåller en tabell med formler.

Om du har detta, låt oss dyka ner—utan onödig utfyllnad, bara praktiska steg.

## Steg 1: Lägg till Aspose.Cells i ditt projekt

Innan du kan **set custom cell separator** behöver du Aspose.Cells‑JAR‑filen på classpath. Det enklaste sättet är via Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Om du föredrar Gradle, byt ut XML‑delen mot motsvarande `implementation 'com.aspose:aspose-cells:24.10'`. När beroendet är löst är du redo att skriva Java‑kod som kommunicerar med Excel‑filer.

## Steg 2: Ladda arbetsboken – Förberedelse för att exportera Excel‑tabell till TXT

Den första faktiska kodraden är alltid densamma: öppna arbetsboken som innehåller tabellen du vill exportera.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Här hämtar vi det första kalkylbladet (`get(0)`). Om dina data finns på ett annat blad, ändra bara indexet eller använd `get("SheetName")`. Denna del är avgörande för **export excel table to txt** eftersom exportören arbetar på kalkylbladsnivå.

## Steg 3: Ange anpassad cellseparator – Kärnan i exporten

Nu kommer stjärnan i föreställningen: konfigurering av `ExportTableOptions`. Detta objekt låter dig bestämma exakt hur varje cell visas i den slutliga textfilen.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Varför **set custom cell separator**? Eftersom standardseparatorn är en tabb, vilket kan kollidera med data som redan innehåller tabbar. Genom att välja ett rörtecken (`|`) eller ett semikolon säkerställer du att varje kolumn förblir tydlig när en nedströmsparser läser filen.

### Exportera Excel‑formler till text

Raden `setFormulaValueInCell(true)` instruerar Aspose.Cells att skriva **export excel formulas to text** som *resultatet* av formeln, inte formelsträngen själv. Om du utelämnar detta skulle en cell som innehåller `=SUM(A1:A5)` visas som `=SUM(A1:A5)` i TXT‑filen, vilket sällan är önskvärt.

## Steg 4: Bifoga exportalternativ till TXT‑sparaalternativ

Nu binder vi dessa tabellalternativ till den övergripande TXT‑exportkonfigurationen.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` är det övergripande objektet som styr hur hela kalkylbladet skrivs ut. Genom att ansluta `exportTableOptions` till det säkerställer du att varje tabell på bladet följer regeln **set custom cell separator**.

## Steg 5: Spara kalkylbladet som TXT‑fil – Avsluta exporten

Till sist skriver vi filen till disk.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

När du kör programmet skapas `TableExported.txt`. Varje rad i den ursprungliga Excel‑tabellen kommer nu att visas som en rad med rör‑avgränsade värden, exempelvis:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Observera hur formeln i **Total**‑kolumnen utvärderades innan den skrevs—tack vare `setFormulaValueInCell(true)`. Det är kärnan i **export excel data as plain text** samtidigt som beräknade resultat bevaras.

## Steg 6: Verifiera resultatet – Ser det rätt ut?

Öppna den genererade `TableExported.txt` i en textredigerare. Du bör se:

- En rad per Excel‑rad.
- Kolumner separerade med rörtecknet du angav med `setCellValueSeparator`.
- Inga lösa kommatecken eller tabbar om de inte var en del av de ursprungliga cellvärdena.
- Formleresultat, inte formlerna själva.

Om du upptäcker oväntade tecken, dubbelkolla separatorn du valde. Vissa tecken (som rörtecknet) är säkra för de flesta CSV‑liknande parserar, men om dina data redan innehåller rör, överväg en annan avgränsare såsom `~` eller en tabb (`\t`).

## Tips, kantfall och bästa praxis – Exportera Excel‑data som vanlig text

| Situation | What to Do |
|-----------|------------|
| **Data already contains your chosen separator** | Switch to a less common character (`^`, `~`, or Unicode non‑printing chars). |
| **You need UTF‑8 encoding** |  |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}