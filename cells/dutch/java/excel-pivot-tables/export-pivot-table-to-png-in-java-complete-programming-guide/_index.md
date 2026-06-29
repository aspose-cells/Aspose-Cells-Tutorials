---
category: general
date: 2026-06-27
description: Exporteer draaitabel als een Excel‑draaitabelafbeelding in Java. Leer
  hoe je PNG‑formaat instelt, opties configureert en het bestand in slechts een paar
  stappen opslaat.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: nl
og_description: Exporteer een draaitabel als een Excel‑draaitabelafbeelding met Java.
  Deze gids laat zien hoe je PNG‑formaat instelt en de afbeelding met vertrouwen opslaat.
og_title: Exporteer draaitabel naar PNG in Java – Stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Draaitabel exporteren naar PNG in Java – Complete programmeergids
url: /nl/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot-tabel exporteren naar PNG in Java – Complete programmeergids

Heb je ooit een **pivot table** moeten **exporteren** uit een Excel-werkmap, maar wist je niet hoe je een schoon afbeeldingsbestand kon krijgen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit obstakel aan bij het bouwen van rapportagedashboards. Het goede nieuws is dat je met een paar regels Java-code elke pivot-tabel kunt omzetten in een scherpe **Excel pivot-afbeelding** die als PNG wordt opgeslagen.  

In deze tutorial lopen we het volledige proces door: het lezen van de werkmap, het vinden van de eerste pivot-tabel, het configureren van de export om **PNG-formaat in te stellen**, en tenslotte het schrijven van de afbeelding naar schijf. Aan het einde heb je een herbruikbare snippet die je in elk project kunt gebruiken.

## Wat je zult leren

- Hoe je een Excel‑bestand laadt met Aspose.Cells (of Apache POI als je dat verkiest).
- De exacte API‑aanroepen die nodig zijn om een **pivot table** als PNG te **exporteren**.
- Waarom het instellen van het afbeeldingsformaat belangrijk is en hoe je **PNG-formaat correct instelt**.
- Veelvoorkomende valkuilen—zoals het omgaan met meerdere pivot‑tabellen of ontbrekende werkbladen—en hoe je ze kunt vermijden.
- Een complete, kant‑klaar Java‑voorbeeld dat je kunt kopiëren‑plakken.

> **Voorvereisten**  
> • Java 17 of nieuwer (de code werkt met eerdere versies, maar 17 wordt aanbevolen).  
> • Aspose.Cells for Java bibliotheek (gratis proefversie werkt prima).  
> • Basiskennis van Excel‑bestanden en Java I/O.

---

## Stap 1: Voeg Aspose.Cells‑afhankelijkheid toe

Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`. Anders download je de JAR van de Aspose‑website en voeg je deze toe aan je classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* Houd je bibliotheekversies gesynchroniseerd met de officiële release‑notes om onverwachte bugs te voorkomen.

## Stap 2: Laad de werkmap en vind de pivot‑tabel

Eerst openen we het Excel‑bestand, vervolgens halen we de eerste pivot‑tabel op van het eerste werkblad. Als de werkmap geen pivot‑tabellen bevat, stoppen we netjes.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Waarom deze stap belangrijk is** – Het `PivotTable`‑object is het toegangspunt voor elke afbeeldingsexport. Als je `toImage` probeert aan te roepen op een niet‑bestaande pivot, krijg je een `NullPointerException`, daarom controleren we eerst het aantal.

## Stap 3: Configureer afbeeldings‑exportopties (PNG‑formaat instellen)

Nu maken we een `ImageOrPrintOptions`‑instantie aan en stellen we expliciet **PNG‑formaat in**. PNG is verliesloos, waardoor de scherpte van rasterlijnen en lettertypen behouden blijft.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Opmerking:* Als je in plaats daarvan een JPEG nodig hebt, vervang dan `ImageFormat.PNG` door `ImageFormat.JPEG`. Hetzelfde opties‑object werkt voor beide.

## Stap 4: Exporteer de pivot‑tabel als een afbeeldingsbestand

Met de opties klaar, roepen we `toImage` aan. De methode schrijft het bestand direct, dus er zijn geen extra streams nodig.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Het uitvoeren van het programma maakt een bestand genaamd `pivot.png` dat er precies uitziet als de pivot die je in Excel ziet. Open het met een willekeurige afbeeldingsviewer om te verifiëren.

### Verwachte output

```
Pivot table exported successfully to: C:/exports/pivot.png
```

De resulterende afbeelding zal overeenkomen met de weergave op het scherm, inclusief kolombreedtes, rijhoogtes en eventuele voorwaardelijke opmaak die je hebt toegepast.

## Meerdere pivot‑tabellen verwerken (Geavanceerd)

Wat als je werkblad meerdere pivot‑tabellen bevat en je slechts één specifieke wilt? Je kunt door `ws.getPivotTables()` itereren en kiezen op naam:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Waarom dit nuttig is*: In rapporten uit de praktijk heb je vaak een samenvattende pivot plus een gedetailleerde. Selecteren op naam voorkomt per ongeluk overschrijven.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Symptoom | Oplossing |
|------|----------|-----|
| **Ontbrekend werkblad** | `IndexOutOfBoundsException` bij het benaderen van `ws` | Controleer `workbook.getWorksheets().getCount() > 0` voordat je indexeert. |
| **Geen pivot‑tabellen** | Stille fout of lege afbeelding | Gebruik een `ws.getPivotTables().getCount()`‑controle (zie Stap 2). |
| **Verkeerd afbeeldingsformaat** | Uitvoer is onscherp of bevat artefacten | Stel altijd `setImageFormat(ImageFormat.PNG)` in voor verliesloze output; vermijd JPEG voor tekst‑zware tabellen. |
| **Bestandspad niet schrijfbaar** | `IOException` bij `toImage` | Zorg ervoor dat de map bestaat (`new File(outputPath).getParentFile().mkdirs()`). |

## Pro tip: Exporteren naar een byte‑array voor web‑apps

Als je een webservice bouwt die de PNG direct naar de browser retourneert, kun je naar een `ByteArrayOutputStream` schrijven in plaats van naar een bestand:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Dit elimineert de noodzaak voor tijdelijke bestanden en versnelt de respons.

---

## Volledig werkend voorbeeld (alle stappen gecombineerd)

Hieronder staat het volledige, klaar‑om‑te‑kopiëren‑en‑plakken programma dat alle besproken best practices bevat.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Het uitvoeren van deze klasse genereert `pivot.png` in `C:/exports`. Open het bestand en je ziet een exacte visuele replica van de oorspronkelijke pivot‑tabel—perfect om in rapporten, e‑mails of webpagina's in te sluiten.

![Exported pivot table saved as PNG – voorbeeld van een Excel pivot‑afbeelding](https://example.com/images/pivot-export.png "voorbeeld export pivot-tabel")

*Image alt text:* **voorbeeld export pivot‑tabel die een PNG Excel pivot‑afbeelding toont**

## Conclusie

We hebben je net laten zien hoe je **pivot table**‑gegevens uit Excel kunt **exporteren** naar een hoogwaardige PNG met Java. De belangrijkste stappen zijn het laden van de werkmap, het vinden van de pivot, het configureren van `ImageOrPrintOptions` om **PNG‑formaat in te stellen**, en tenslotte het aanroepen van `toImage`.  

Met deze kennis kun je nu rapportgeneratie automatiseren, pivot‑momentopnames in dashboards insluiten, of ze direct vanuit een web‑API aanbieden. Als volgende stap kun je **excel pivot image**‑schaalopties verkennen, watermerken toevoegen, of zelfs de PNG naar een PDF converteren voor afdrukbare rapporten.  

Heb je vragen over het verwerken van grotere werkmappen of integratie met Spring Boot? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je de bron van een Excel Pivot Table bijwerkt met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatiseer Excel Pivot Table styling en opslaan met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table manipulatie met Aspose.Cells Java: Een uitgebreide gids](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}