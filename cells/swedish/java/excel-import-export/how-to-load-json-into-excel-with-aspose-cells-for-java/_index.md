---
category: general
date: 2026-10-07
description: Lär dig hur du laddar JSON i Excel och genererar XLSX från JSON med Aspose.Cells.
  Denna steg‑för‑steg‑guide visar också hur du fyller i Excel från JSON och sparar
  arbetsboken som XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: sv
lastmod: 2026-10-07
og_description: Läs in JSON i Excel och generera XLSX från JSON med Aspose.Cells för
  Java. Följ den här guiden för att fylla Excel med JSON och spara arbetsboken som
  XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Läs in JSON i Excel med Aspose.Cells – komplett Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man laddar JSON i Excel med Aspose.Cells för Java
url: /sv/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Läs in JSON i Excel med Aspose.Cells för Java

Om du behöver **läsa in JSON i Excel**, visar den här handledningen ett pålitligt sätt att göra det med Aspose.Cells för Java. Du får se hur du genererar XLSX från JSON, fyller Excel från JSON och slutligen **sparar arbetsboken som XLSX**—allt i ett enda, självständigt program.

Att arbeta med JSON i kalkylblad är vanligt när du exporterar data från webbtjänster, API:er eller NoSQL‑lagringar. I slutet av den här guiden har du en färdig‑att‑köra Java‑klass som skapar en arbetsbok från JSON och skriver resultatet till en fil på disk.

## Förutsättningar

Innan du börjar, se till att du har:

* Java 8 eller nyare installerat (koden använder standard‑Java‑funktioner).
* Aspose.Cells för Java‑biblioteket (version 23.10 eller senare). Du kan hämta det från [Aspose‑webbplatsen](https://downloads.aspose.com/cells/java) eller via Maven Central.
* En IDE eller en enkel textredigerare och en terminal för att kompilera och köra Java‑kod.
* Grundläggande kunskap om JSON‑syntax och Excel‑koncept.

> **Proffstips:** Om du använder Maven, lägg till följande beroende i din `pom.xml` för att undvika manuell JAR‑hantering:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Steg 1: Ställ in projektet och importera nödvändiga klasser

Skapa en ny Java‑klass som heter `JsonToExcelDemo`. Importera de Aspose.Cells‑klasser du kommer att behöva för arbetsboks‑skapande, kalkylblads‑hantering och Smart‑Marker‑bearbetning.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Varför detta steg är viktigt:* Att importera rätt klasser säkerställer att kompilatorn kan hitta Aspose.Cells‑API:er. Klassen `Workbook` representerar Excel‑filen, medan `SmartMarkerProcessor` driver JSON‑till‑Excel‑konverteringen.

## Steg 2: Definiera JSON‑källan som ska läsas in i Excel

I det här exemplet använder vi en liten JSON‑array som innehåller två objekt. I ett riktigt scenario kan du läsa JSON från en fil, en REST‑endpoint eller en databas.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Varför detta steg är viktigt:* JSON‑strängen är datakällan för **populate Excel from JSON**‑operationen. Att hålla JSON i en `String`‑variabel gör det enkelt att skicka den till `SmartMarkerProcessor`.

## Steg 3: Skapa en ny arbetsbok och hämta det första kalkylbladet

En ny arbetsbok ger dig en ren start. Det första kalkylbladet (index 0) är där vi kommer att infoga Smart‑Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Varför detta steg är viktigt:* Aspose.Cells arbetar med ett `Workbook`‑objekt som senare kan sparas som en XLSX‑fil. Genom att komma åt den första `Worksheet` kan vi placera markören på en känd celladress.

## Steg 4: Infoga en Smart Marker som talar om för Aspose.Cells hur JSON‑en ska behandlas

Smart Markers är platshållare som Aspose.Cells ersätter med data från en källa. Markören `&=JSONData.ArrayAsSingle` instruerar biblioteket att behandla hela JSON‑arrayen som ett enda cellvärde.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Varför detta steg är viktigt:* Att använda `ArrayAsSingle` undviker standardbeteendet att expandera varje array‑element till separata rader. Detta är användbart när du vill att JSON‑texten ska visas ordagrant i en cell, eller när du planerar att dela upp den senare med formler.

## Steg 5: Konfigurera SmartMarkerProcessor med JSON‑datakällan

Bind nu JSON‑strängen till det logiska namnet `JSONData`. Processorn kommer att ersätta markören med den faktiska datan.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Varför detta steg är viktigt:* `setDataSource` länkar namnet som används i markören (`JSONData`) med den faktiska JSON‑payloaden. `process()` utför det tunga arbetet: parsning av JSON, tillämpning av markörlogiken och skrivning av resultatet till kalkylbladet.

## Steg 6: Spara den resulterande arbetsboken som en XLSX‑fil

Skriv slutligen arbetsboken till disk. Konstanten `SaveFormat.XLSX` garanterar korrekt Office Open XML‑format.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Varför detta steg är viktigt:* Att spara filen fullbordar **generate XLSX from JSON**‑arbetsflödet. Den skapade filen kan öppnas i Excel, LibreOffice eller något annat kalkylprogram som stödjer XLSX.

### Fullständig källkod

När alla bitar sätts ihop får du det kompletta, körbara programmet som **creates workbook from JSON**, **populates Excel from JSON** och **saves workbook as XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Förväntat resultat

När du öppnar `JsonSingleCell.xlsx` ser du JSON‑arrayen visas i cell **A1** exakt som den ursprungliga strängen:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Om du föredrar varje objekt på en separat rad, ersätt markören med `&=JSONData` (utan `.ArrayAsSingle`). Processorn kommer då att expandera arrayen till individuella rader, vilket demonstrerar en annan **populate Excel from JSON**‑teknik.

## Vanliga variationer och kantfall

| Situation | Justering |
|-----------|-----------|
| **Stort JSON‑payload (> 10 MB)** | Öka JVM‑heap‑storleken (`-Xmx2g`) och överväg att streama JSON för att undvika `OutOfMemoryError`. |
| **Nästlade objekt** | Använd hierarkiska markörer som `&=JSONData.Name` och `&=JSONData.Age` i en tabell för att mappa varje egenskap till en kolumn. |
| **JSON‑fil istället för en sträng** | Läs in filen till en `String` med `java.nio.file.Files.readString(Path.of("data.json"))` och skicka den till `setDataSource`. |
| **Behov av att behålla original‑JSON‑formatet** | Behåll suffixet `.ArrayAsSingle`, eller omslut JSON i CDATA om du planerar att använda Excel‑formler som senare parsar JSON. |
| **Flera kalkylblad** | Skapa ytterligare kalkylblad (`workbook.getWorksheets().add("Sheet2")`) och upprepa markörinfogningen på varje blad. |

> **Varning:** Smart Markers är skiftlägeskänsliga. Säkerställ att det logiska namnet (`JSONData`) matchar exakt mellan markören och `setDataSource`.

## Testa lösningen

1. Kompilera programmet:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Kör det:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verifiera att `JsonSingleCell.xlsx` finns i arbetskatalogen och öppnas utan fel.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Skapa Excel‑arbetsbok från JSON – Komplett Aspose.Cells‑guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Skapa Excel‑arbetsbok C# – Infoga JSON och spara som XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Spara Excel‑arbetsbok från JSON – Komplett guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}