---
category: general
date: 2026-07-16
description: Maak een nieuwe werkmap en kopieer een draaitabel met Aspose.Cells voor
  Java. Leer hoe je een draaitabel dupliceert en een Excel-bereik in enkele minuten
  kopieert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: nl
lastmod: 2026-07-16
og_description: Maak een nieuwe werkmap en kopieer een draaitabel met Aspose.Cells
  voor Java. Deze gids laat zien hoe je een draaitabel dupliceert en een Excel-bereik
  efficiënt kopieert.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Maak een nieuw werkboek & kopieer draaitabel in Java – Complete tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Maak een nieuw werkboek en kopieer draaitabel in Java – Volledige stapsgewijze
  handleiding
url: /nl/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuw werkboek maken en draaitabel kopiëren in Java – volledige stap‑voor‑stap gids

Heb je je ooit afgevraagd hoe je **create new workbook** kunt maken terwijl je een complexe draaitabel uit een bestaand bestand behoudt? Als je ooit naar een Excel‑blad hebt gekeken, dacht “Ik heb deze draaitabel in een ander werkboek nodig,” en vervolgens je hoofd hebt gestreken, ben je niet de enige. Het goede nieuws is dat je met Aspose.Cells for Java een draaitabel kunt dupliceren in slechts een handvol regels.

In deze tutorial lopen we de exacte stappen door om **copy pivot table** gegevens te kopiëren, **duplicate pivot table** structuren te dupliceren, en **copy Excel range** inhoud te kopiëren — allemaal terwijl we een nieuw werkboek vanaf nul maken. Aan het einde heb je een kant‑klaar Java‑programma dat precies doet wat je vroeg.

## Wat je zult leren

- Hoe je **create new workbook** programmatically kunt maken met Aspose.Cells.
- De precieze manier om het bereik te definiëren dat een draaitabel bevat.
- Technieken om **copy pivot table** en **duplicate pivot table** uit te voeren zonder verlies van opmaak of dataverbindingen.
- Hoe je **copy Excel range** efficiënt kunt gebruiken en het resultaat opslaat.
- Veelvoorkomende valkuilen en tips voor het omgaan met grotere draaitabellen.

Geen externe referenties nodig — alles is zelf‑voorzienend, uitvoerbaar en uitgelegd.

---

## Vereisten

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

1. **Java Development Kit (JDK) 11+** – elke recente versie werkt.
2. **Aspose.Cells for Java** bibliotheek (de nieuwste versie van 2026‑07‑16). Je kunt deze ophalen van Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Een bron‑Excel‑bestand (`SourceWithPivot.xlsx`) dat al een draaitabel bevat die je wilt kopiëren.
4. Een IDE of eenvoudige teksteditor — IntelliJ IDEA, Eclipse of VS Code volstaat.

Heb je alles? Geweldig — laten we beginnen.

## Stap 1: **Create New Workbook** en laad het bronbestand

Het eerste wat we nodig hebben is een nieuw werkboekobject dat uiteindelijk de gedupliceerde draaitabel zal bevatten. Tegelijkertijd moeten we het originele werkboek laden zodat we naar het bereik van de draaitabel kunnen verwijzen.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Waarom dit belangrijk is:**  
> Het laden van het bron‑werkboek geeft ons toegang tot het onderliggende `Range`‑object dat de draaitabel omvat. Als je deze stap overslaat, heb je niets om te kopiëren, en zal de **duplicate pivot table**‑operatie stil falen.

## Stap 2: Definieer de **Copy Excel Range** die de draaitabel bevat

Een draaitabel is niet één enkele cel — hij beslaat een rechthoekig blok. We moeten Aspose.Cells precies vertellen welke cellen gekopieerd moeten worden.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Tip:**  
> Als je niet zeker bent van het exacte bereik, open dan het bron‑werkboek in Excel, selecteer de draaitabel en kijk in het naamvak. Het toont iets als `A1:G20`. Het gebruiken van het exacte bereik zorgt ervoor dat alle veldinstellingen, filters en berekeningen behouden blijven wanneer we later **copy pivot table** uitvoeren.

## Stap 3: **Create New Workbook** die de gekopieerde draaitabel ontvangt

Nu maken we een gloednieuw werkboek — hier zal onze **duplicate pivot table** worden geplaatst.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Wat er onder de motorkap gebeurt:**  
> De standaardconstructor maakt een werkboek met één leeg blad. Dit is het schone canvas dat we nodig hebben voor een **create new workbook**‑scenario. Geen overgebleven stijlen of verborgen bladen om ons zorgen over te maken.

## Stap 4: **Copy Pivot Table** – Kopieer daadwerkelijk het gedefinieerde Excel‑bereik

Met zowel bron als bestemming gereed, voeren we de kopieer‑operatie uit. Deze stap realiseert het **how to copy pivot**‑deel van de puzzel.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Waarom `copy` werkt voor draaitabellen:**  
> Aspose.Cells beschouwt de draaitabel als onderdeel van de celcollectie. Wanneer je het bereik kopieert, wordt de pivot‑cache, veldlijst en lay‑out meegenomen. Het resultaat is een volledig functionele **duplicate pivot table** in het nieuwe werkboek.

## Stap 5: Sla het resultaat op en verifieer de **Copy Pivot Table**‑operatie

Tot slot slaan we het bestemmings‑werkboek op naar schijf. Open het bestand in Excel om te bevestigen dat de draaitabel precies zo verschijnt als in de bron.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Verwacht resultaat:**  
- `CopyPivotResult.xlsx` opent met een werkblad dat dezelfde draaitabel bevat als in `SourceWithPivot.xlsx`.  
- Alle rij‑/kolom‑labels, filters en berekende velden blijven behouden.  
- Je kunt nu de brongegevens onafhankelijk bewerken, en het nieuwe werkboek behoudt zijn eigen pivot‑cache.

## Randgevallen & Veelgestelde vragen

### Wat als de bron‑draaitabel zich over meer dan één blad uitstrekt?

Aspose.Cells kan per keer alleen bereiken binnen één werkblad kopiëren. Als je draaitabel zich over meerdere bladen uitstrekt, moet je elk relevant bereik afzonderlijk kopiëren en daarna handmatig opnieuw koppelen.

### Behoudt deze methode aangepaste getalnotaties?

Ja. De `copy`‑methode kopieert celstijlen, inclusief getalnotaties, lettertypen en kleuren. Als je echter voorwaardelijke opmaak hebt die naar externe bereiken verwijst, controleer die referenties na het kopiëren nogmaals.

### Hoe een draaitabel kopiëren die een externe gegevensbron gebruikt?

Wanneer de draaitabel gegevens haalt uit een externe verbinding (bijv. een SQL‑query), wordt de verbindingsinformatie **niet** overgedragen door `copy`. Je moet de gegevensbron in het bestemmings‑werkboek opnieuw aanmaken of de brongegevens vooraf insluiten.

### Kan ik alleen de draaitabellay-out kopiëren zonder de onderliggende gegevens?

Dit kun je bereiken door eerst de gegevenscellen in het bronbereik te wissen en vervolgens alleen de lay‑out van de draaitabel te kopiëren. Dit is een meer geavanceerd scenario en meestal niet nodig voor een eenvoudige **duplicate pivot table**‑taak.

## Volledig werkend voorbeeld (alle stappen gecombineerd)

Hieronder staat de volledige, kant‑klaar te draaien Java‑klasse. Vervang `YOUR_DIRECTORY` gewoon door het daadwerkelijke mappad op jouw machine.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Voer het programma uit (`java CopyPivotTableDemo`) en je ziet het console‑bericht dat succes bevestigt.

## Pro‑tips & best practices

- **Validate the range** before copying. Gebruik `srcWs.getCells().maxDisplayRange` om programmatically het gebruikte gebied te ontdekken als je `"A1:G20"` niet hard‑coded wilt.
- **Turn off calculation** temporarily for huge workbooks to speed up the copy:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) in langdurige services om geheugenlekken te voorkomen.
- **Version compatibility:** De code werkt met Aspose.Cells 23.12 en later. Oudere versies kunnen `srcRange.copyTo` in plaats van `copy` vereisen.

## Volgende stappen

Nu je **create new workbook** en **copy pivot table** onder de knie hebt, kun je het volgende verkennen:

- **How to copy pivot** over meerdere werkbladen in een batch‑taak.
- Het toevoegen van **copy excel range** voor reguliere datatabellen naast de draaitabel.
- Het automatiseren van **duplicate pivot table**‑creatie voor elke maandrapportage met een lus.
- Het exporteren van de gedupliceerde draaitabel naar PDF of HTML met de ingebouwde renderers van Aspose.Cells.

Elk van deze onderwerpen bouwt voort op de hier gelegde basis, en ze profiteren allemaal van dezelfde schone, programmatic aanpak.

## Conclusie

We hebben het volledige proces doorlopen van **create new workbook**, het definiëren van de bron **copy excel range**, en **copy pivot table** om een **duplicate pivot table** in Java te produceren met Aspose.Cells. De oplossing is beknopt, volledig functioneel en klaar voor productiegebruik. Voel je vrij om het bereik aan te passen, te experimenteren met verschillende bronbestanden, of deze logica in een grotere rapportage‑pipeline te integreren.

Als je tegen problemen aanloopt of ideeën hebt om deze tutorial uit te breiden, laat dan een reactie achter. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabellen te maken in Excel met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑draaitabel bij te werken met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulatie van Excel‑draaitabellen met Aspose.Cells Java: Een uitgebreide gids](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}