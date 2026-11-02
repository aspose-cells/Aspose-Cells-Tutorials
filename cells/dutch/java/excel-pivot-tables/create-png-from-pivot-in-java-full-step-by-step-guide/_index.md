---
category: general
date: 2026-06-18
description: Maak snel een PNG van een draaitabel met Java. Leer hoe je een Excel‑gegevensafbeelding
  exporteert, een draaitabelafbeelding exporteert en het bereik opslaat als een PNG‑bestand.
draft: false
keywords:
- create png from pivot
- export excel data image
- export pivot table image
- export excel range image
- export pivot table file
language: nl
og_description: Maak PNG van draaitabel in Java. Deze gids laat zien hoe je een Excel-gegevensafbeelding
  exporteert, een draaitabelafbeelding exporteert en een PNG-bestand genereert van
  een draaitabelbereik.
og_title: Maak PNG van Pivot in Java – Complete exporthandleiding
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  headline: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  name: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  steps:
  - name: '**File exists** – `new File(outputPath).exists()` should return `true`.'
    text: '**File exists** – `new File(outputPath).exists()` should return `true`.'
  - name: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
    text: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
  - name: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
    text: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Maak PNG van Pivot in Java – Volledige stap‑voor‑stap gids
url: /nl/java/excel-pivot-tables/create-png-from-pivot-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG maken van een draaitabel in Java – Volledige stap‑voor‑stap gids

Heb je je ooit afgevraagd hoe je **PNG van een draaitabel** kunt maken zonder Excel handmatig te openen? Misschien moet je een draaitabel‑grafiek in een rapport insluiten, of bouw je een dashboard dat live gegevens uit een .xlsx‑bestand haalt. Het goede nieuws is dat je niet met COM‑objecten of screen‑scraping hoeft te worstelen – Java kan het netjes doen.

In deze tutorial lopen we een volledige oplossing door die **een Excel‑bereikafbeelding exporteert**, specifiek een draaitabel, naar een PNG‑bestand. Je ziet precies hoe je **excel data image exporteert**, waarom `ImageOrPrintOptions` belangrijk zijn, en waar je op moet letten bij het **exporteren van een draaitabelbestand**. Aan het einde heb je een kant‑klaar Java‑programma dat `pivot.png` naast je werkmap schrijft.

## Vereisten

- Java 17 (of een recente JDK) – de code gebruikt de standaardtaalfeatures, geen lambdas vereist.
- Aspose.Cells for Java‑bibliotheek (gratis proefversie of betaalde licentie). Voeg de Maven‑dependency toe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

- Een Excel‑werkmap (`pivots.xlsx`) die al minstens één draaitabel bevat.  
- Basiskennis van Java `main`‑methoden; geen extra frameworks nodig.

> **Pro tip:** Als je Gradle gebruikt, vervang dan het XML‑fragment door `implementation "com.aspose:aspose-cells:24.9"`.

## Stap 1: Laad de werkmap die de draaitabel bevat

Het eerste wat we doen is de werkmap openen. Aspose.Cells abstraheert het lage‑niveau bestandsbeheer, zodat één regel je een volledig functioneel `Workbook`‑object geeft.

```java
import com.aspose.cells.*;

public class ExportPivotToPng {
    public static void main(String[] args) throws Exception {
        // Adjust the path to point at your actual file location
        String workbookPath = "YOUR_DIRECTORY/pivots.xlsx";
        Workbook workbook = new Workbook(workbookPath);
```

> **Waarom dit belangrijk is:** Het laden van de werkmap valideert het bestandsformaat en bereidt het interne model voor, wat essentieel is voordat je draaitabellen kunt opvragen.

## Stap 2: Toegang tot het eerste werkblad

De meeste spreadsheets plaatsen draaitabellen op het eerste blad, maar je kunt de index aanpassen indien nodig. Hier halen we simpelweg het eerste werkblad op.

```java
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

> **Randgeval:** Als je werkmap verborgen bladen bevat, retourneert Aspose ze nog steeds; je moet mogelijk `sheet.isVisible()` controleren voordat je verder gaat.

## Stap 3: Haal het bereik op dat door de eerste draaitabel wordt ingenomen

Nu volgt het hart van de operatie: het vinden van het bereik van de draaitabel. De collectie `getPivotTables()` laat ons de gewenste draaitabel kiezen, waarna `getRange()` een `Range`‑object retourneert dat de exacte cellen vertegenwoordigt.

```java
        // Assume the workbook has at least one pivot table
        PivotTable pivot = sheet.getPivotTables().get(0);
        Range pivotRange = pivot.getRange();
```

> **Waarom deze stap cruciaal is:** Het `Range`‑object kent de afmetingen, opmaak en gegevens van de draaitabel. Wanneer we later `toImage` aanroepen, gebruikt het deze metadata om een pixel‑perfecte PNG te renderen.

## Stap 4: Configureer afbeeldings‑exportopties – PNG‑formaat

Aspose geeft je fijnmazige controle over de uitvoerafbeelding: DPI, schaal, randen en natuurlijk het bestandsformaat. Omdat we een PNG willen, stellen we `ImageFormat.PNG` in. Je kunt ook `setTransparent(true)` gebruiken als je een alfakanaal nodig hebt.

```java
        // Set up export options for a high‑quality PNG
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setImageFormat(ImageFormat.PNG);
        // Optional: increase resolution for sharper output
        options.setResolution(300);
```

> **Veelgestelde vraag:** *Kan ik in plaats daarvan naar JPEG of BMP exporteren?* Ja – vervang gewoon `ImageFormat.PNG` door `ImageFormat.JPEG` of `ImageFormat.BMP`.

## Stap 5: Exporteer het draaitabel‑bereik naar een afbeeldingsbestand

Tot slot roepen we `toImage` aan op de `Range`. De methode neemt het bestemmingspad en de opties die we zojuist geconfigureerd hebben. De operatie schrijft het bestand in één regel naar de schijf.

```java
        // Define the output file path
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        // Export the pivot range as a PNG image
        pivotRange.toImage(outputPath, options);

        System.out.println("Pivot table exported successfully to " + outputPath);
    }
}
```

> **Verwachte output:** Na het uitvoeren van het programma zie je `pivot.png` in de opgegeven map. Open het met een willekeurige afbeeldingsviewer en je ziet precies de lay‑out van de oorspronkelijke Excel‑draaitabel, inclusief kolom‑koppen, subtotaal‑rijen en eventuele toegepaste stijlen.

## Het resultaat verifiëren – Snelle checklist

1. **Bestand bestaat** – `new File(outputPath).exists()` moet `true` retourneren.  
2. **Afbeeldingsafmetingen** – Open de PNG; de breedte/hoogte moet overeenkomen met de visuele grootte van het bereik.  
3. **Gegevensgetrouwheid** – Vergelijk een screenshot van het Excel‑blad met de PNG; ze moeten pixel‑voor‑pixel identiek zijn.

Als een van deze controles faalt, controleer dan of het pad naar de werkmap correct is en of de draaitabel niet verborgen of gefilterd is.

## Export Excel Range Image vs. Export Pivot Table Image

Je vraagt je misschien af of er een verschil is tussen **export excel range image** en **export pivot table image**. In de praktijk:

| Doel | Methode | Typisch gebruik |
|------|--------|-----------------|
| Exporteer een willekeurig bereik (bijv. A1:D20) | `sheet.getCells().createRange("A1:D20").toImage(...)` | Een statische tabel of grafiek‑gebied vastleggen |
| Exporteer specifiek een draaitabel | `pivot.getRange().toImage(...)` | De dynamische lay‑out, subtotaal‑ en filterinstellingen behouden |

Beide benaderingen gebruiken dezelfde `toImage`‑API; het verschil zit in het kiezen van het juiste `Range`‑object. Wanneer je **export pivot table file** doe je in feite de visuele weergave persisteert in plaats van de ruwe data.

## Meerdere draaitabellen verwerken

Bevat je werkmap meerdere draaitabellen, loop dan simpelweg over de collectie:

```java
        for (int i = 0; i < sheet.getPivotTables().getCount(); i++) {
            PivotTable pt = sheet.getPivotTables().get(i);
            String out = "YOUR_DIRECTORY/pivot_" + i + ".png";
            pt.getRange().toImage(out, options);
            System.out.println("Exported pivot #" + i + " to " + out);
        }
```

> **Waarom een lus?** Geautomatiseerde rapportage‑pipelines moeten vaak elke draaitabel in een werkmap publiceren. De lus maakt de oplossing schaalbaar zonder extra code.

## Veelvoorkomende valkuilen en hoe ze te vermijden

- **Ontbrekende licentie** – Zonder een geldige Aspose.Cells‑licentie voegt de bibliotheek een watermerk toe aan de PNG. Registreer je licentie vroeg: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.  
- **Grote draaitabellen veroorzaken geheugen‑druk** – Als de draaitabel duizenden rijen beslaat, overweeg dan de JVM‑heap te vergroten (`-Xmx2g`) of in secties te exporteren.  
- **Onjuist afbeeldingsformaat** – Het doorgeven van `ImageFormat.JPEG` terwijl je transparantie verwacht resulteert in een egale achtergrond. Gebruik PNG wanneer je alfa‑kanaal nodig hebt.

## Bonus: Exporteren naar een byte‑array voor web‑API’s

Soms wil je geen bestand op schijf; je hebt de afbeeldingsbytes nodig om via HTTP te versturen. Vervang de bestands‑gebaseerde aanroep door een `MemoryStream` (Aspose’s `ByteArrayOutputStream`):

```java
        java.io.ByteArrayOutputStream stream = new java.io.ByteArrayOutputStream();
        pivotRange.toImage(stream, options);
        byte[] pngBytes = stream.toByteArray();
        // Now you can return pngBytes from a REST endpoint
```

> **Praktisch voorbeeld:** Een Spring Boot‑controller kan `ResponseEntity<byte[]>` retourneren met `Content-Type: image/png`, waardoor browsers de draaitabel on‑the‑fly kunnen weergeven.

## Conclusie

Je weet nu precies hoe je **PNG van een draaitabel** maakt met Java en Aspose.Cells. De tutorial behandelde alles van het laden van de werkmap, het vinden van het draaitabel‑bereik, het configureren van PNG‑exportopties, tot het uiteindelijk schrijven van het afbeeldingsbestand. We hebben ook gerelateerde taken bekeken zoals **export excel data image**, **export pivot table image**, en zelfs hoe je **export excel range image** voor niet‑draaien‑secties uitvoert.

Volgende stappen? Probeer aangepaste opmaak toe te voegen aan de PNG (bijv. een achtergrondkleur), of integreer de exportroutine in een grotere batch‑job die ’s nachts tientallen werkmappen verwerkt. Je kunt ook experimenteren met andere uitvoerformaten – PDF, SVG of zelfs multi‑page TIFF – door de `ImageFormat`‑enum te wijzigen.

Heb je vragen over randgevallen, licenties of prestatie‑optimalisatie? Laat een reactie achter, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Customize Pivot Table Globalization & PDF Export in Java with Aspose.Cells](/cells/english/java/data-analysis/customize-pivot-table-globalization-pdf-export-java/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}