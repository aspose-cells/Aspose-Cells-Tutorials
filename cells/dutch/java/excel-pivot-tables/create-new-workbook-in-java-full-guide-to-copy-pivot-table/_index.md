---
category: general
date: 2026-07-23
description: Maak een nieuwe werkmap in Java en leer hoe je een draaitabel kunt kopiëren,
  een Excel-bereik kunt kopiëren en een draaitabel kunt exporteren met Aspose.Cells
  in enkele minuten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: nl
lastmod: 2026-07-23
og_description: Maak een nieuw werkboek in Java en kopieer direct een draaitabel,
  kopieer een Excel-bereik en exporteer vervolgens de draaitabel met Aspose.Cells.
  Volg deze volledige tutorial.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Maak een nieuw werkboek in Java – Kopieer draaitabel stap‑voor‑stap
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Maak een nieuw werkboek in Java – Volledige gids voor het kopiëren van een
  draaitabel
url: /nl/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een nieuw werkboek in Java – Volledige gids voor het kopiëren van een draaitabel

Heb je je ooit afgevraagd hoe je **create new workbook** in Java kunt maken terwijl je een complexe draaitabel behoudt? Je bent niet de enige die zich hier zorgen over maakt. In veel rapportage‑apps moet je een draaitabel van een bronbestand naar een nieuw werkboek verplaatsen, misschien om het naar een klant te sturen of om verdere berekeningen uit te voeren. Het goede nieuws? Met een handvol regels kun je precies dat doen—geen handmatig kopiëren‑plakken nodig.

In deze tutorial lopen we het volledige proces door: het laden van het bronbestand, het definiëren van het bereik dat de draaitabel bevat, **copying the Excel range**, het maken van een **new workbook**, en uiteindelijk **exporting the pivot table** naar een nieuw bestand. Aan het einde heb je een zelf‑containend, uitvoerbaar Java‑programma dat de vraag “**how to copy pivot**” beantwoordt zonder giswerk.

## Prerequisites

- Java 17 of later (de code werkt met elke recente JDK)
- Aspose.Cells for Java‑bibliotheek (gratis proefversie of gelicentieerde versie)
- Een voorbeeld `source.xlsx` dat een draaitabel bevat in het bereik `A1:G20`
- Een IDE of build‑tool (Maven/Gradle) om de Aspose.Cells‑JAR te beheren

Heb je die? Geweldig—laten we beginnen.

## Step 1: Set Up the Project and Import Aspose.Cells

Allereerst moet je Aspose.Cells aan je project toevoegen. Als je Maven gebruikt, voeg dan deze afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Als je liever Gradle gebruikt, is het equivalent:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Zodra de bibliotheek op het classpath staat, importeer je de klassen die je nodig hebt:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells is een commerciële bibliotheek, maar biedt een volledig functionele 30‑daagse evaluatie die een watermerk op de output plaatst—perfect om dit uit te proberen.

## Step 2: Load the Source Workbook

Nu gaan we **create new workbook** objecten maken, maar eerst hebben we de bron nodig die de draaitabel bevat. Deze stap is de basis voor elke **copy excel range**‑operatie omdat het bereik‑object precies weet welke cellen (inclusief de draaitabel‑cache) moeten worden overgebracht.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Waarom niet gewoon het bereik direct lezen? Omdat de metadata van de draaitabel zich in de draaitabel‑cache van het werkblad bevindt, en Aspose.Cells dat automatisch meeneemt wanneer je het bereik kopieert.

## Step 3: Define the Range That Holds the Pivot Table

In veel real‑world bestanden beslaat de draaitabel een rechthoekig blok. Voor dit voorbeeld gaan we ervan uit dat het zich bevindt in `A1:G20`. Je kunt uiteraard het adres aanpassen aan je werkelijke indeling.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Als je niet zeker bent van het exacte adres, kun je `sourceSheet.getCells().getMaxDataRow()` en `getMaxDataColumn()` gebruiken om de grenzen dynamisch te berekenen. Dat is een handige truc wanneer de grootte van de draaitabel in de loop van de tijd verandert.

## Step 4: **Create New Workbook** and Destination Worksheet

Hier is het moment waarop we daadwerkelijk **create new workbook** maken dat de gekopieerde inhoud zal ontvangen. Beschouw dit als het lege canvas waarop je de draaitabel plakt.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Waarom beginnen met een leeg werkboek? Het garandeert dat er geen verborgen stijlen of eerdere draaitabellen de kopie verstoren, waardoor je een schoon resultaat krijgt dat klaar is voor **export pivot table**.

## Step 5: Copy the Pivot Table (and Its Underlying Range)

Nu het kernpunt van de tutorial: **copy pivot table**. Aspose.Cells behandelt een bereik‑kopie als een diepe kopie, wat betekent dat de draaitabel‑cache met de cellen meereist. Daarom doet deze enkele regel het zware werk.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Als je je ooit afvroeg **how to copy pivot** zonder de functionaliteit te verliezen, is dit het antwoord. Het bestemmingsblad bevat nu een volledig werkende draaitabel die je kunt vernieuwen, aanpassen of simpelweg exporteren.

### Edge Case: Preserving Refresh Settings

Soms is de bron‑draaitabel ingesteld om te vernieuwen bij openen. Om dat gedrag te behouden, kun je de opties van de draaitabel expliciet kopiëren:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Dat fragment zorgt ervoor dat de gekopieerde draaitabel zich precies gedraagt als het origineel.

## Step 6: Save the Destination Workbook – **Export Pivot Table**

Tot slot **export pivot table** we door het nieuwe werkboek op schijf op te slaan. Je kunt elk formaat kiezen dat Aspose ondersteunt: XLSX, XLS, CSV, PDF, enz. Voor deze gids blijven we bij XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Als je het bestand via een webservice moet verzenden, kun je het naar een `ByteArrayOutputStream` schrijven in plaats van een bestandspad—Aspose maakt dat triviaal.

## Full Working Example

Alles bij elkaar, hier is een compleet, kant‑klaar programma. Voel je vrij om het te kopiëren, plakken en uit te voeren in je IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Expected Output

Wanneer je het programma uitvoert, print de console:

```
Pivot table copied successfully!
```

En het bestand `copied_with_pivot.xlsx` verschijnt in `YOUR_DIRECTORY`. Open het in Excel, en je ziet de draaitabel intact, klaar om te vernieuwen of te bewerken.

## Common Questions & Troubleshooting

- **Wat als de bron‑draaitabel zich over meer dan één werkblad uitstrekt?**  
  Je moet elk relevant bereik afzonderlijk kopiëren en vervolgens de draaitabel op het bestemmingsblad opnieuw maken met behulp van de `PivotTable`‑API's.

- **Kan ik alleen de draaitabel‑lay-out kopiëren zonder de gegevens?**  
  Stel `sourceRange.setCopyDataOnly(false)` in vóór het kopiëren. Dit vertelt Aspose de cache te behouden maar niet de onderliggende brongegevens.

- **Is er een manier om de draaitabel naar een CSV‑bestand te kopiëren?**  
  CSV ondersteunt geen draaitabellen, maar je kunt het *resultaat* van de draaitabel exporteren door `pivotTable.calculate()` aan te roepen en vervolgens het blad als CSV op te slaan.

- **Waarom verliest de gekopieerde draaitabel zijn opmaak?**  
  Opmaak zit in de stijl‑collectie. Na het kopiëren kun je `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` aanroepen om stijlen over te dragen.

## Conclusion

We hebben je zojuist laten zien hoe je **create new workbook** in Java kunt maken, **copy pivot table**, en **export pivot table**—alles met een schoon, reproduceerbaar code‑voorbeeld. Door het exacte **copy excel range** te definiëren, gebruik te maken van de deep‑copy‑semantiek van Aspose.Cells, en optionele instellingen te behouden, kun je vrijwel elke draaitabel‑migratietaak automatiseren.

Klaar voor de volgende stap? Probeer het uitvoerformaat naar PDF te wijzigen, of loop door meerdere bronbestanden om tientallen draaitabellen in batch te verwerken. Hetzelfde patroon geldt—pas alleen de bestandspaden en bereik‑adressen aan.

Als je een probleem tegenkomt, laat dan een reactie achter of raadpleeg de Aspose.Cells‑documentatie voor geavanceerde draaitabel‑manipulatie. Veel plezier met coderen, en geniet van de tijd die je bespaart door die vervelende copy‑paste‑taken te automatiseren!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabellen te maken in Excel met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑draaitabel bij te werken met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hoe Excel te maken en te exporteren naar HTML met Aspose.Cells Java | Gids voor werkboek‑operaties](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}