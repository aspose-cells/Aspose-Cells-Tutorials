---
category: general
date: 2026-08-11
description: Maak een nieuwe werkmap met Aspose in Java, voeg een aangepaste eigenschap
  toe in Excel, en sla de werkmap vervolgens op als XLSB met een volledig stapsgewijs
  voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: nl
lastmod: 2026-08-11
og_description: Maak een nieuwe werkmap met Aspose in Java, voeg een aangepaste eigenschap
  toe aan Excel en sla de werkmap op als XLSB met een volledig, kant‑klaar voorbeeld.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Nieuw werkboek maken Aspose – aangepaste eigenschap toevoegen in Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Maak een nieuw werkboek met Aspose – voeg aangepaste eigenschap toe aan Excel
  en sla op als XLSB
url: /nl/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe workbook Aspose maken – aangepaste eigenschap Excel toevoegen en opslaan als XLSB

Als je een **create new workbook Aspose** moet maken in een Java‑applicatie, laat deze gids je precies zien hoe je dat doet. Je leert hoe je **add custom property Excel** kunt toevoegen, de waarde kunt ophalen, en **save workbook as XLSB** zonder metadata te verliezen.

De tutorial behandelt alles van projectconfiguratie tot verificatie van het opgeslagen bestand. Er is geen externe documentatie nodig; volg gewoon de stappen en voer de code uit.

## Voorvereisten

- Java Development Kit (JDK) 8 of hoger geïnstalleerd.
- Maven of Gradle om afhankelijkheden te beheren (het voorbeeld gebruikt Maven).
- Een actieve Aspose.Cells for Java‑licentie (of gebruik de gratis evaluatiemodus voor testen).

## Stap 1: Aspose.Cells toevoegen aan je project

Voeg het Aspose.Cells Maven‑artifact toe aan je `pom.xml`. Deze afhankelijkheid levert de klassen die nodig zijn om **create new workbook Aspose**‑objecten te maken.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Als je de voorkeur geeft aan Gradle, vervang dan het Maven‑fragment door de equivalente `implementation "com.aspose:aspose-cells:23.12"`‑regel.

## Stap 2: Een nieuwe workbook Aspose maken

De eerste functionele stap is het instantieren van een `Workbook`‑object. Dit object vertegenwoordigt een Excel‑bestand in het geheugen en is het toegangspunt voor alle verdere bewerkingen.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Het maken van een nieuwe workbook Aspose geeft je een schoon workbook met een standaard werkblad, klaar voor aanpassingen.

## Stap 3: Aangepaste eigenschap Excel toevoegen

Aangepaste eigenschappen stellen je in staat willekeurige metadata op te slaan in een Excel‑bestand. Hier **add custom property Excel** we een eigenschap genaamd `ProjectId` met een numerieke waarde.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

De `add`‑methode accepteert een eigenschapsnaam en een waarde van elk ondersteund type (string, getal, datum, enz.). Deze metadata reist mee met het bestand waar je het ook kopieert.

## Stap 4: De aangepaste eigenschap ophalen en weergeven

Het teruglezen van de eigenschap verifieert dat deze correct is opgeslagen. Je kunt de opgehaalde waarde ook gebruiken in je bedrijfslogica.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Casten naar `int` werkt omdat we een numerieke waarde hebben opgeslagen. Als je een string opslaat, gebruik dan `(String)`.

## Stap 5: Workbook opslaan als XLSB

Nu **save workbook as XLSB**. Het XLSB‑formaat slaat het workbook op in een binaire representatie, die sneller te openen is en minder schijfruimte gebruikt. Alle aangepaste eigenschappen worden automatisch bewaard.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Vervang `"WithCustomProps.xlsb"` door een absoluut pad als je het bestand in een specifieke map wilt plaatsen. De `SaveFormat.XLSB`‑enum vertelt Aspose.Cells om het binaire formaat te schrijven.

## Stap 6: De uitvoer verifiëren

Run het programma vanuit je IDE of de commandoregel:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Je zou moeten zien:

```
ProjectId = 12345
```

Open `WithCustomProps.xlsb` in Excel. Navigeer naar **File → Info → Properties → Advanced Properties → Custom**. Het `ProjectId`‑item met waarde `12345` wordt weergegeven, wat bevestigt dat de **add custom property excel**‑stap geslaagd is en de **save workbook as xlsb**‑operatie de metadata heeft behouden.

## Veelgestelde vragen en randgevallen

### Wat als ik een string‑eigenschap moet opslaan?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Haal het op met:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Kan ik meerdere aangepaste eigenschappen in één keer toevoegen?

Ja. Roep `add` herhaaldelijk aan voor elk naam/waarde‑paar. Aspose.Cells beperkt het aantal aangepaste eigenschappen niet, maar houd de totale grootte redelijk om het bestand niet te laten groeien.

### Hoe beïnvloedt het binaire formaat de prestaties?

XLSB‑bestanden laden sneller omdat ze XML‑parsing vermijden. Dit is vooral merkbaar bij workbooks met veel rijen, formules of ingesloten afbeeldingen.

### Wat als ik met een bestaand XLSX‑bestand moet werken?

Vervang de `new Workbook()`‑constructor door `new Workbook("ExistingFile.xlsx")`. De rest van de stappen (eigenschappen toevoegen, opslaan als XLSB) blijven identiek.

## Volledige broncode

Hieronder staat het volledige, kant‑klaar voorbeeld. Kopieer het naar een bestand met de naam `CustomPropertiesXlsb.java` in je `src/main/java`‑map.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Het uitvoeren van deze klasse produceert een XLSB‑bestand dat de aangepaste eigenschap bevat en kan worden geopend in elke moderne versie van Microsoft Excel.

## Conclusie

Je weet nu hoe je **create new workbook Aspose**, **add custom property Excel**, en **save workbook as XLSB** kunt gebruiken met Java. Het voorbeeld toont de volledige levenscyclus: initialisatie, metadata‑injectie, verificatie en binaire serialisatie.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **setting document properties**, **working with Excel formulas**, of **converting between XLSX and XLSB**. Elk van deze bouwt voort op dezelfde Aspose.Cells‑API die je zojuist hebt gebruikt, zodat je de oplossing kunt uitbreiden zonder nieuwe bibliotheken te leren.

Voel je vrij om te experimenteren met verschillende datatypes, meerdere werkbladen, of wachtwoordbeveiliging—Aspose.Cells ondersteunt al deze scenario's direct. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Workbook Excel maken en opslaan met Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Hoe een Excel‑workbook maken en opslaan als SVG met Aspose.Cells voor Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel‑workbook maken en labels toevoegen met Aspose.Cells voor Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}