---
category: general
date: 2026-09-18
description: Exportera JSON till Excel med Aspose.Cells i Java. Lär dig att infoga
  JSON i Excel, konvertera JSON till Excel och spara arbetsboken som XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export json to excel
- insert json into excel
- how to insert json
- convert json to excel
- save workbook as xlsx
language: sv
lastmod: 2026-09-18
og_description: Exportera JSON till Excel med Aspose.Cells för Java. Steg‑för‑steg‑handledning
  visar hur man infogar JSON i Excel, konverterar JSON till Excel och sparar arbetsboken
  som XLSX.
og_image_alt: Aspose.Cells Java code inserting JSON array into a single Excel cell
og_title: Exportera JSON till Excel med Aspose.Cells – Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  headline: Export JSON to Excel with Aspose.Cells in Java
  type: TechArticle
- description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  name: Export JSON to Excel with Aspose.Cells in Java
  steps:
  - name: Prepare your development environment.
    text: Prepare your development environment.
  - name: Define the JSON data source.
    text: Define the JSON data source.
  - name: Create a workbook and worksheet.
    text: Create a workbook and worksheet.
  - name: Insert JSON into Excel using a Smart Marker.
    text: Insert JSON into Excel using a Smart Marker.
  - name: Process the Smart Marker so the JSON appears in a single cell.
    text: Process the Smart Marker so the JSON appears in a single cell.
  - name: Save the workbook as an XLSX file.
    text: Save the workbook as an XLSX file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Exportera JSON till Excel med Aspose.Cells i Java
url: /sv/java/excel-import-export/export-json-to-excel-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera JSON till Excel med Aspose.Cells i Java

Om du behöver **exportera JSON till Excel**, visar den här guiden en komplett lösning med Aspose.Cells för Java. Du kommer att se exakt hur du infogar JSON i Excel, konverterar JSON till Excel och slutligen **sparar arbetsboken som XLSX** utan att lämna din IDE.

Att arbeta med JSON‑data är vanligt när du bygger API:er, rapport‑dashboards eller datamigreringsverktyg. Istället för att manuellt kopiera‑klistra automatiserar metoden nedan hela pipeline‑processen så att du kan generera Excel‑filer programatiskt.

## Exportera JSON till Excel – steg‑för‑steg guide

Följande avsnitt guidar dig genom varje nödvändigt steg:

1. Förbered din utvecklingsmiljö.  
2. Definiera JSON‑datakällan.  
3. Skapa en arbetsbok och ett kalkylblad.  
4. Infoga JSON i Excel med en Smart Marker.  
5. Bearbeta Smart Marker så att JSON visas i en enda cell.  
6. Spara arbetsboken som en XLSX‑fil.

När du har gått igenom hela tutorialen har du ett körbart Java‑program som producerar en `JsonExport.xlsx`‑fil som innehåller JSON‑arrayen i cell **A1**.

## Förutsättningar

- Java Development Kit 8 eller nyare.  
- Maven eller Gradle för att hantera beroenden.  
- Aspose.Cells for Java (senaste versionen vid skrivtillfället, 24.10).  
- Grundläggande kunskap om Java‑syntax och JSON‑format.

> **Pro tip:** Aspose.Cells är ett kommersiellt bibliotek, men en gratis utvärderingslicens fungerar för utveckling och testning.

## Steg 1: Ställ in ditt Java‑projekt

Lägg till Aspose.Cells‑beroendet i din `pom.xml` (Maven) eller `build.gradle` (Gradle).

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

**Gradle**

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

När beroendet har lösts kan du importera de nödvändiga klasserna:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;
```

## Steg 2: Definiera JSON‑datakällan

JSON‑strängen representerar en array av objekt. I ett riktigt projekt kan du läsa detta från en fil, ett REST‑slutpunkt eller en databas. För illustration embedder vi JSON‑strängen direkt i koden.

```java
// Step 2: Define the JSON data source (an array of objects)
String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";
```

**Varför detta är viktigt:** Aspose.Cells kan behandla en JSON‑array som en enda cell när du använder alternativet `ArrayAsSingle`. Detta undviker behovet av att dela upp arrayen över rader och kolumner, vilket är idealiskt för export av råa JSON‑payloads.

## Steg 3: Skapa en arbetsbok och hämta det första kalkylbladet

Ett `Workbook`‑objekt representerar hela Excel‑filen. Det första kalkylbladet (index 0) är där vi placerar JSON‑data.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Förklaring:** Att instansiera `Workbook` utan parametrar skapar en tom arbetsbok med ett standardsheet. Du kan senare lägga till fler blad om ditt scenario kräver flera dataset.

## Steg 4: Infoga JSON i Excel med en Smart Marker

Smart Markers är platshållare som Aspose.Cells ersätter med data vid körning. Markören `&=jsonArray(ArrayAsSingle)` instruerar motorn att skriva hela JSON‑arrayen i en enda cell.

```java
// Step 4: Insert a Smart Marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");
```

**Varför använda en Smart Marker?** Den abstraherar data‑bindningslogiken, så att du kan fokusera på källformatet (JSON) snarare än låg‑nivå cellmanipulation.

## Steg 5: Koppla Smart Marker‑namnet till JSON‑data

Du måste binda marköridentifieraren (`jsonArray`) till den faktiska JSON‑strängen.

```java
// Step 5: Associate the Smart Marker name with the JSON data
workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);
```

**Obs:** Metoden `setDataSource` accepterar vilket objekt som helst som Smart Marker‑motorn kan serialisera, inklusive JSON‑strängar, Java‑samlingar eller DataTables.

## Steg 6: Bearbeta Smart Markers så att JSON‑arrayen skrivs in i cellen

Anropet `processSmartMarkers()` triggar ersättningen av markören med den bundna JSON‑data.

```java
// Step 6: Process the Smart Markers so the JSON array is written into the cell
workbook.processSmartMarkers();
```

Om JSON‑strängen är felaktig kastar Aspose.Cells ett `SmartMarkerException`. Omslut anropet i ett try‑catch‑block för produktionsklar robusthet.

## Steg 7: Spara arbetsboken som en XLSX‑fil

Skriv slutligen arbetsboken till disk. Filändelsen bestämmer utdataformatet; att använda `.xlsx` säkerställer det moderna Office Open XML‑formatet.

```java
// Step 7: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonExport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

**Resultat:** När du öppnar `JsonExport.xlsx` visas JSON‑arrayen exakt som den står i `jsonData`, placerad i cell **A1**.

## Komplett körbart exempel

Nedan finns en självständig Java‑klass som du kan kopiera, klistra in och köra.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;

/**
 * Demonstrates how to export JSON to Excel using Aspose.Cells.
 * The program inserts a JSON array into a single cell and saves the workbook as XLSX.
 */
public class JsonToExcelExporter {
    public static void main(String[] args) {
        // 1. Define the JSON data source (an array of objects)
        String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";

        try {
            // 2. Create a new workbook and obtain the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Insert a Smart Marker that treats the JSON array as a single cell
            worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");

            // 4. Bind the Smart Marker name to the JSON string
            workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);

            // 5. Process Smart Markers – this writes the JSON into cell A1
            workbook.processSmartMarkers();

            // 6. Save the workbook as an XLSX file
            String outputPath = "JsonExport.xlsx";
            workbook.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (SmartMarkerException e) {
            System.err.println("Error processing Smart Markers: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e.getMessage());
        }
    }
}
```

### Förväntat resultat

Kör programmet så skrivs:

```
Workbook saved to JsonExport.xlsx
```

När du öppnar **JsonExport.xlsx** visas cell **A1** med:

```
[{"Name":"John","Score":85},{"Name":"Anna","Score":92}]
```

## Vanliga variationer och edge‑cases

| Situation | Så anpassar du koden |
|-----------|----------------------|
| **Stort JSON‑payload** ( > 1 MB) | Öka JVM‑heap‑storleken (`-Xmx2g`) för att undvika `OutOfMemoryError`. |
| **Flera JSON‑objekt** som kräver separata rader | Använd `ArrayAsRows` istället för `ArrayAsSingle` och mappa markören till en samling POJO‑objekt. |
| **Spara som CSV** | Ersätt `workbook.save(outputPath)` med `workbook.save(outputPath, com.aspose.cells.SaveFormat.CSV);`. |
| **Lägga till en rubrikrad** | Skriv en statisk sträng till `worksheet.getCells().putValue(0, 0, "JSON Payload");` innan du infogar Smart Marker. |
| **Använda en annan katalog** | Säkerställ att katalogen finns eller skapa den med `new java.io.File(dir).mkdirs();`. |

## Tips för produktionsanvändning

- **Validera JSON** innan du skickar den till Aspose.Cells för att förhindra körningsfel.  
- **Använd try‑with‑resources** för alla strömmar du öppnar när du läser JSON från externa källor.  
- **Lås arbetsboken** om flera trådar kan skriva till samma fil samtidigt.  
- **Licensregistrering**: anropa `com.aspose.cells.License license = new com.aspose.cells.License(); license.setLicense("Aspose.Cells.lic");` vid applikationens start.

## Nästa steg

Nu när du kan **exportera JSON till Excel**, överväg att utforska relaterade funktioner:

- **Infoga JSON i Excel** med formatering: applicera cellstilar efter att Smart Marker har bearbetats.  
- **Konvertera JSON till Excel‑tabeller**: mappa JSON‑objekt till rader och kolumner

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Importera JSON‑data till Excel med Aspose.Cells Java: En omfattande guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Hur man infogar flera rader i Excel med Aspose.Cells för Java](/cells/english/java/cell-operations/excel-automation-aspose-cells-java-insert-multiple-rows/)
- [Hur man infogar bilder i Excel med Java och Aspose.Cells](/cells/english/java/images-shapes/insert-image-into-excel-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}