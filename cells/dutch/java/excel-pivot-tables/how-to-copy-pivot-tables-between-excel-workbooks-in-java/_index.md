---
category: general
date: 2026-10-01
description: Leer hoe je draaitabellen tussen Excel‑werkboeken kunt kopiëren met Java.
  Deze stapsgewijze gids laat ook zien hoe je een bereik tussen werkboeken kunt kopiëren
  en Excel‑bereiken veilig kunt dupliceren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: nl
lastmod: 2026-10-01
og_description: Hoe pivot‑tabellen tussen Excel‑werkboeken te kopiëren met Java. Volg
  deze gids om een bereik naar een werkboek te kopiëren, Excel‑bereiken te dupliceren
  en pivot‑gegevens te behouden.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Hoe je draaitabellen tussen Excel-werkboeken in Java kopieert – volledige
  gids
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Hoe pivot‑tabellen tussen Excel‑werkboeken te kopiëren in Java
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe pivot-tabellen tussen Excel-werkboeken in Java te kopiëren

Als je **how to copy pivot** tabellen van het ene Excel‑bestand naar het andere moet kopiëren, biedt deze gids een kant‑klaar‑te‑gebruiken oplossing. Aan het einde van de eerste twee zinnen weet je precies welke API‑aanroepen de pivot‑definitie behouden tijdens het kopiëren van het gegevens‑bereik.

Je leert ook hoe je **copy range between workbooks**, **duplicate Excel range** objecten kunt dupliceren, en veilig **copy range to workbook** kunt uitvoeren zonder formules of opmaak te verliezen. Er zijn geen externe scripts nodig—alleen een enkel Java‑project dat Aspose.Cells for Java gebruikt.

## Vereisten

* Java Development Kit 17 of hoger.
* Maven of Gradle om afhankelijkheden te beheren.
* Een geldige Aspose.Cells for Java‑licentie (de gratis evaluatie werkt voor testen).
* Twee Excel‑bestanden: `source.xlsx` (bevat de pivot‑tabel) en een lege `destination.xlsx` (of laat de code deze aanmaken).

## Stap 1: Het Maven‑project opzetten

Maak een `pom.xml` aan die Aspose.Cells bevat. Deze afhankelijkheid levert de `Workbook`, `Worksheet` en `Range` klassen die in het voorbeeld worden gebruikt.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Houd de Aspose.Cells‑versie up‑to‑date; nieuwere releases bieden betere ondersteuning voor complexe pivot‑cache‑structuren.

## Stap 2: Laad het bron‑werkboek dat de pivot‑tabel bevat

Het eerste code‑blok laat **how to copy excel** gegevens zien door het bronbestand te laden. De `Workbook`‑constructor leest het volledige bestand in het geheugen in, waarbij alle blad‑objecten, inclusief pivots, behouden blijven.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Waarom dit belangrijk is:* Aspose.Cells slaat pivot‑tabellen op als onderdeel van het interne model van het werkblad. Het laden van het werkboek zorgt ervoor dat de pivot‑cache beschikbaar is voor later kopiëren.

## Stap 3: Definieer het bereik dat de pivot‑tabel bevat

Een pivot‑tabel kan zich over meerdere rijen en kolommen uitstrekken. In de meeste gevallen kun je het volledige gebruikte bereik van het blad kopiëren. De `createRange`‑methode bouwt een `Range`‑object dat door de kopieer‑operatie wordt verwerkt.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Als de pivot zich uitstrekt voorbij `H20`, wijzig dan eenvoudig de adres‑string. Deze stap is de kern van **duplicate excel range** verwerking; het bereik‑object kent formules, stijlen en verborgen rijen.

## Stap 4: Maak een nieuw werkboek aan dat het gekopieerde bereik ontvangt

Je kunt beginnen met een leeg werkboek of een bestaand bestemmingsbestand laden. Hier maken we een nieuw werkboek aan, wat de schoonste manier is om **copy range to workbook** uit te voeren.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Opmerking:** Als je de pivot naar een specifieke bladnaam wilt kopiëren, hernoem `destWs` met `destWs.setName("Report")` vóór het plakken.

## Stap 5: Kopieer het bereik – Aspose.Cells behoudt automatisch de pivot

De `copy`‑methode verplaatst alles binnen het bron‑bereik, inclusief de pivot‑definitie, cache en opmaak. Er is geen extra code nodig om de pivot functioneel te houden.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Waarom het werkt:* Aspose.Cells beschouwt de pivot als een verzameling verborgen cellen en metadata die aan het bereik zijn gekoppeld. Wanneer je `copy` aanroept, dupliceert de bibliotheek die metadata in het doel‑werkboek.

## Stap 6: Sla het bestemmings‑werkboek op

Schrijf tenslotte het resultaat naar schijf. Het opgeslagen bestand bevat een identieke pivot‑tabel die je kunt vernieuwen of aanpassen, net als het origineel.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Het uitvoeren van het programma geeft een bevestiging weer en produceert `destination.xlsx` met een volledig functionele pivot.

## Volledig, uitvoerbaar voorbeeld

Alle stappen samengevoegd ziet de volledige Java‑klasse er als volgt uit:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Verwachte output

* Console: `Pivot table copied successfully.`
* `destination.xlsx` opent in Excel met een pivot‑tabel die identiek is aan die in `source.xlsx`. Het vernieuwen van de pivot toont dezelfde gegevensbron, wat bewijst dat **how to copy pivot** werkt zoals bedoeld.

## Veelvoorkomende variaties behandelen

### Meerdere werkbladen kopiëren

Als je project vereist dat meerdere bladen worden gekopieerd, loop dan door de werkbladen van het werkboek en herhaal stappen 2‑4 voor elk blad. De pivot in elk blad wordt onafhankelijk behouden.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Externe gegevensverbindingen behouden

Pivot‑tabellen die afhankelijk zijn van externe gegevensbronnen behouden de verbindingsreeks na het kopiëren. Het bestemmingsbestand moet echter toegang hebben tot dezelfde gegevensbron. Controleer de verbinding door de pivot te openen en het **Data**‑tabblad te bekijken.

### Omgaan met samengevoegde cellen

Als het bron‑bereik samengevoegde cellen bevat, kopieert Aspose.Cells de samenvoeg‑indeling automatisch. Controleer het resultaat toch als het bestemmings‑werkboek een andere standaard kolombreedte gebruikt.

## Best practices voor betrouwbaar kopiëren

| Praktijk | Reden |
|----------|-------|
| Gebruik het exacte gebruikte bereik (`srcWs.getCells().getMaxDisplayRange()`) in plaats van een hard‑gecodeerd adres | Garandeert dat de volledige pivot en de brongegevens zijn inbegrepen. |
| Pas een licentie toe vóór zware bewerkingen | Voorkomt het evaluatiewatermerk en verbetert de prestaties. |
| Vernieuw de pivot na het kopiëren (`pivotTable.refresh()`) als de brongegevens zijn gewijzigd | Zorgt ervoor dat de bestemming de nieuwste waarden weergeeft. |
| Schrijf unit‑tests die het bestemmings‑werkboek openen en controleren of `pivotTable.getPivotFields().size()` overeenkomt met de bron | Detecteert per ongeluk verlies van velden bij toekomstige code‑wijzigingen. |

## Conclusie

Je weet nu **how to copy pivot** tabellen tussen Excel‑werkboeken in Java, evenals hoe je **copy range between workbooks**, **duplicate excel range** en **copy range to workbook** kunt uitvoeren terwijl alle opmaak en formules behouden blijven. Het voorbeeld maakt gebruik van Aspose.Cells, dat de low‑level XML‑verwerking die door de OpenXML SDK vereist is, abstraheert.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **updating pivot cache programmatically**, **exporting pivot data to CSV**, of **creating pivot tables from scratch**. Elk van deze bouwt voort op dezelfde concepten die hier worden getoond.

Veel plezier met coderen, en voel je vrij om te experimenteren met grotere bereiken, meerdere pivots of aangepaste stijlen – hetzelfde patroon is van toepassing in alle scenario's.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}