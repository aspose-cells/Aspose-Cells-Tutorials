---
category: general
date: 2026-09-27
description: Lär dig hur du genererar dynamiska bladnamn i Excel med Java medan du
  fyller i en Excel‑mall och skapar blad från data för robust rapportering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: sv
lastmod: 2026-09-27
og_description: Dynamiska bladnamn låter dig generera flera blad från en datamängd.
  Den här handledningen visar hur du fyller i en Excel-mall i Java och skapar blad
  från data med Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Skapa dynamiska bladnamn i Excel med Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man genererar dynamiska bladnamn i Excel med Java
url: /sv/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man genererar dynamiska bladnamn i Excel med Java

Om du behöver **dynamiska bladnamn** när du fyller i en Excel‑mall i Java, guidar den här handledningen dig genom hela processen. Du kommer att se hur du *genererar flera blad* från en samling data, och hur varje blad automatiskt får ett unikt namn. I slutet har du ett körbart exempel som skapar blad från data och sparar resultatet med önskad namngivningskonvention.

Att generera blad i farten är ett vanligt krav för rapporterings‑dashboards, fakturabatcher eller någon situation där antalet detaljsektioner inte är känt i förväg. Aspose.Cells Smart Marker‑motorn gör denna uppgift kortfattad och pålitlig, och koden nedan demonstrerar den rekommenderade metoden.

## Använda dynamiska bladnamn med Aspose.Cells

Aspose.Cells för Java tillhandahåller en **Smart Marker**‑processor som kan läsa platshållare i en mallarbok och expandera dem till rader, kolumner eller till och med nya kalkylblad. Genom att konfigurera `SmartMarkerOptions.DetailSheetNewName` styr du namnet på varje genererat blad. Platshållaren `{0}` ersätts med det noll‑baserade indexet för den aktuella dataraden, vilket ger dig helt **dynamiska bladnamn** såsom `Detail_0`, `Detail_1`, …​.

> **Pro tip:** Behåll mallarboken i en dedikerad resurser‑mapp och använd en relativ sökväg när det är möjligt. Detta undviker hårdkodade absoluta sökvägar som går sönder i olika miljöer.

## Steg 1: Ladda Excel‑mallen (populate excel template java)

Först, ladda arbetsboken som innehåller Smart Marker‑taggarna. Mallen bör ha ett blad som heter, till exempel, `Detail` med en markör som `&=Orders!A1` som talar om för processorn var den ska börja infoga rader.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Varför detta steg är viktigt:* Mallen definierar layouten (rubriker, formler, formatering) som kommer att kopieras till varje genererat blad. Utan en korrekt mall skulle resultatet förlora stil och formler.

## Steg 2: Förbered datakällan för att skapa blad från data

Nästa steg, bygg en datakälla som Smart Marker‑processorn kan iterera över. I detta exempel använder vi en `Map<String, Object>` där nyckeln `"Orders"` matchar markörnamnet i mallen.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Varför detta steg är viktigt:* Smart Marker‑motorn läser arrayen, skapar en rad för varje inre `Object[]`, och—eftersom vi kommer att be den generera nya blad—skapar ett separat kalkylblad för varje rad. Detta är kärnan i **create sheets from data**.

## Steg 3: Konfigurera SmartMarkerOptions för att generera flera blad med unika namn

Nu talar du om för Aspose.Cells hur varje nytt kalkylblad ska namnges. Platshållaren `{0}` ersätts med det aktuella radindexet.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Varför detta steg är viktigt:* Utan att sätta `DetailSheetNewName` skulle processorn återanvända det ursprungliga bladnamnet för varje rad, vilket skriver över data. Detta alternativ möjliggör **dynamic sheet names**.

## Steg 4: Bearbeta SmartMarkers och generera arbetsboken

Kör processorn med datakällan och de alternativ vi just konfigurerade.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Varför detta steg är viktigt:* Processorn expanderar markörerna, skapar det erforderliga antalet kalkylblad, kopierar mallens layout och fyller varje blad med motsvarande raddata.

## Steg 5: Spara och verifiera resultatet

Till sist, skriv arbetsboken till disk. Öppna filen i Excel för att se de automatiskt skapade bladen.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Förväntat resultat**

När du öppnar `MasterDetailResult.xlsx` bör du se tre nya kalkylblad:

* `Detail_0` – innehåller order 101 (Alice, 250.00)  
* `Detail_1` – innehåller order 102 (Bob, 175.50)  
* `Detail_2` – innehåller order 103 (Carol, 320.75)

Varje blad behåller formateringen, kolumnbredderna och eventuella formler som fanns i det ursprungliga `Detail`‑mallbladet.

## Fullständigt körbart exempel

Att sätta ihop alla sektioner ger dig ett självständigt program som du kan kompilera och köra:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Så kör du

1. Lägg till Aspose.Cells för Java JAR till ditt projekts classpath (tillgänglig via Maven Central eller på Aspose‑webbplatsen).  
2. Placera `MasterDetailTemplate.xlsx` i `templates/` relativt projektets rot.  
3. Kör `main`‑metoden. Mappen `output/` kommer att innehålla den genererade filen.

## Vanliga variationer och kantfall

| Situation | Vad som ska ändras |
|-----------|-------------------|
| **Olika namnmönster** | Använd `"OrderSheet_{0}_v{1}"` och inkludera ytterligare platshållare som `{1}` för ett andra index (t.ex. ett sidnummer). |
| **Stora datamängder** | Öka JVM‑heapen (`-Xmx2g`) för att undvika `OutOfMemoryError` när du genererar hundratals blad. |
| **Villkorlig bladskapning** | Innan du anropar `process`, filtrera dataarrayen så att rader som inte uppfyller ett kriterium utelämnas, vilket förhindrar onödiga blad. |
| **Bevara formler som refererar till andra blad** | Behåll det ursprungliga bladnamnet som en dold platshållare (t.ex. `DetailTemplate`) och använd `SmartMarkerOptions.setDetailSheetNewName` endast för det synliga namnet; formler som refererar till det dolda namnet kommer fortfarande att lösas korrekt. |

## Tips för robust Excel‑automation

* **Validate the data source** – Säkerställ att varje inre array har samma antal element som kolumnerna som definierats i mallen; ojämna längder orsakar körningsfel.  
* **Use named ranges** – Använd namngivna områden i mallen för tydligare Smart Marker‑syntax (`&=Orders!A1`).  
* **Close resources** – Även om Aspose.Cells hanterar strömmar internt, kan ett explicit anrop till `templateWorkbook.dispose()` i ett `finally`‑block frigöra native‑minne snabbare.  
* **Test with edge values** – Noll rader bör producera en arbetsbok med endast det ursprungliga mallbladet; en tom datakälla verifierar att din kod hanterar “ingen data” på ett smidigt sätt.

## Slutsats

Du vet nu hur du **genererar dynamiska bladnamn** i Excel med Java, hur du **fyller i en Excel‑mall** och **skapar blad från data**, samt hur du **genererar flera blad** automatiskt med Aspose.Cells Smart Markers. Genom att följa stegen ovan kan du anpassa mönstret till vilket rapporteringsscenario som helst—oavsett om du behöver dussintals detaljblad, anpassade namngivningskonventioner eller villkorsstyrd bladskapning.

Redo att utöka denna lösning? Prova att lägga till diagram i varje genererat blad, eller exportera arbetsboken till PDF med `Workbook.save("result.pdf", SaveFormat.PDF)`. Båda teknikerna bygger på samma dynamiska‑blad‑grund som du just har bemästrat. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Master Dynamic Excel Sheets in Java with Aspose.Cells: A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}