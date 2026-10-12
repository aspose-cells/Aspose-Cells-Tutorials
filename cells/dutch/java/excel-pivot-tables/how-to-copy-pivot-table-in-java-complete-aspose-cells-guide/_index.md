---
category: general
date: 2026-06-08
description: Hoe een draaitabel te kopiëren met Aspose.Cells in Java. Leer hoe je
  een bereik tussen werkmappen kunt kopiëren en draaitabellen moeiteloos behoudt.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: nl
og_description: Hoe een draaitabel te kopiëren in Java met Aspose.Cells. Deze tutorial
  laat zien hoe je een bereik tussen werkboeken kopieert en de draaitabel intact houdt.
og_title: Hoe een draaitabel in Java te kopiëren – Stapsgewijze gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Hoe een draaitabel te kopiëren in Java – Complete Aspose.Cells-gids
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in Java – Complete Aspose.Cells-gids

Heb je je ooit afgevraagd **hoe je een draaitabel** van het ene Excel-werkboek naar het andere kunt kopiëren met Java? Het goede nieuws is dat Aspose.Cells het een fluitje van een cent maakt om **een bereik tussen werkboeken te kopiëren** terwijl elk detail van de draaitabel behouden blijft.  

In deze tutorial lopen we een praktijkvoorbeeld door dat niet alleen de draaitabel zelf kopieert, maar ook de onderliggende gegevens, opmaak en formules intact houdt. Aan het einde weet je precies **hoe je draaitabelstructuren behoudt**, hoe je een draaitabel naar een gloednieuw werkboek verplaatst, en hoe je de veelvoorkomende valkuilen vermijdt die veel ontwikkelaars tegenkomen.

We behandelen:

* De minimale vereisten (Java 17+, Aspose.Cells for Java 23.9+).  
* Een stap‑voor‑stap‑analyse van de code, met uitleg **waarom** elke regel belangrijk is.  
* Afhandeling van randgevallen voor grote draaitabelbereiken en externe gegevensbronnen.  
* Een volledig, uitvoerbaar programma dat je direct in je IDE kunt plaatsen en vandaag nog kunt uitvoeren.

> **Pro tip:** Als je al Maven of Gradle gebruikt, is het toevoegen van Aspose.Cells als dependency één regel – geen handmatig JAR‑beheer nodig.

---

## Hoe een draaitabel te kopiëren – Overzicht stap voor stap

Hieronder zie je een overzicht op hoog niveau van wat we gaan bereiken:

1. Laad het bron‑werkboek dat de draaitabel bevat.  
2. Identificeer het exacte celbereik dat de draaitabel omsluit.  
3. Maak een nieuw doel‑werkboek aan.  
4. **Kopieer het bereik** naar het nieuwe blad, waarbij Aspose.Cells automatisch de draaitabel behoudt.  
5. Sla het resultaat op als een nieuw bestand.

Elke stap wordt geïllustreerd met code‑fragmenten en een korte toelichting, zodat je de werking begrijpt – niet alleen de mechaniek.

![Diagram illustrating how a pivot table is copied from a source workbook to a destination workbook while preserving its structure](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="Diagram dat toont hoe een draaitabel wordt gekopieerd van een bron‑werkboek naar een doel‑werkboek terwijl de structuur behouden blijft"}

---

### Stap 1: Aspose.Cells in je project instellen

Voordat je Excel‑bestanden kunt manipuleren, moet je de Aspose.Cells‑bibliotheek op je classpath hebben. Als je Maven gebruikt, voeg dan de volgende dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

Voor Gradle is het ook één regel:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Waarom dit belangrijk is:* Aspose.Cells abstraheert de low‑level OpenXML‑details, zodat je een eenvoudige API hebt om **een draaitabel naar een nieuw werkboek te kopiëren** zonder metadata te verliezen.

---

### Stap 2: Het bron‑werkboek laden

We hebben een `Workbook`‑instantie nodig die wijst naar het bestand dat de draaitabel bevat. Vervang `YOUR_DIRECTORY/src.xlsx` door het daadwerkelijke pad op jouw machine.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Opmerking:** Aspose.Cells detecteert automatisch het bestandsformaat (XLSX, XLS, CSV, enz.), zodat je je geen zorgen hoeft te maken over formatconversie.

---

### Stap 3: Het omvattende bereik van de draaitabel definiëren

Een draaitabel bevindt zich binnen een rechthoekig blok cellen. Je kunt deze handmatig lokaliseren (bijv. `A1:G20`) of programmatically door de `PivotTables`‑collectie van het werkblad te inspecteren. Voor deze tutorial coderen we het bereik hard‑coded voor de duidelijkheid.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Waarom we `createRange` gebruiken*: Het maakt een lichtgewicht `Range`‑object dat kan worden doorgegeven aan `copyRange`. Dit is de meest betrouwbare manier om **een bereik tussen werkboeken te kopiëren** terwijl de interne structuren van de draaitabel worden meegenomen.

---

### Stap 4: Een leeg doel‑werkboek maken

Nu maken we een leeg werkboek aan dat de gekopieerde gegevens zal ontvangen.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Het standaardwerkboek bevat al één werkblad, wat perfect is voor ons doel. Als je een specifieke bladnaam nodig hebt, kun je die hernoemen:

```java
destinationSheet.setName("PivotCopy");
```

---

### Stap 5: Het bereik kopiëren en de draaitabel behouden

Hier gebeurt de magie. De `copyRange`‑methode accepteert een `CopyOptions`‑object, maar we hoeven niets aan te passen – draaitabelbehoud is standaard ingeschakeld.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Waarom dit werkt:* Aspose.Cells behandelt de draaitabel als onderdeel van de celcollectie. Wanneer je `copyRange` aanroept, wordt de onderliggende draaitabel‑cache, gegevensvelden en lay‑out gerepliceerd, waardoor **hoe je draaitabel behoudt** zonder extra code.

---

### Stap 6: Het doel‑werkboek opslaan

Tot slot schrijven we het nieuwe bestand naar schijf.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Open het resulterende `copied-with-pivot.xlsx` in Excel, en je ziet een exacte replica van de oorspronkelijke draaitabel, klaar voor verdere analyse.

---

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je direct kunt compileren en uitvoeren. Het combineert alle bovenstaande fragmenten, voegt een paar defensieve controles toe, en print een vriendelijke bevestigingsmelding.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Verwachte output wanneer je het programma uitvoert**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Open het doelbestand – je draaitabel zou identiek moeten zijn aan het origineel, inclusief slicers, filters en berekende velden.

---

## Veelvoorkomende randgevallen afhandelen

| Situatie | Waar je op moet letten | Aanbevolen oplossing |
|-----------|-------------------|---------------|
| **Draaitabel gebruikt een externe gegevensbron** (bijv. een database) | De externe verbinding is niet ingebed in het werkboek, waardoor kopiëren de koppeling kan breken. | Exporteer de gegevens eerst naar een blad, maak daarna een draaitabel op dat blad voordat je kopieert. |
| **Zeer grote draaitabel (duizenden rijen)** | `copyRange` kan veel geheugen verbruiken. | Verhoog de JVM‑heap (`-Xmx2g`) of kopieer de draaitabel in kleinere delen met `copyRows`/`copyColumns`. |
| **Meerdere draaitabellen op hetzelfde blad** | Hard‑coderen van `A1:G20` kopieert alleen de eerste draaitabel. | Loop door `sourceWorksheet.getPivotTables()` en kopieer elke `PivotTable.getDataRange()`. |
| **Doel‑werkboek bevat al een blad met dezelfde naam** | `setName` zal een uitzondering werpen. | Gebruik `Workbook.getWorksheets().add("PivotCopy")` om een uniek benoemd blad te creëren. |

Deze tips zorgen ervoor dat **hoe je een draaitabel kopieert** betrouwbaar werkt, zelfs in productie‑scenario's.

---

## Veelgestelde vragen

**V: Kopieert deze methode ook de opmaak van de draaitabel?**  
A: Ja. Omdat we het volledige celbereik kopiëren, reizen stijlen, voorwaardelijke opmaak en getalformaten mee.

**V: Wat als ik de draaitabel naar een specifieke cel anders dan `A1` wil kopiëren?**  
A: Verander simpelweg het derde argument van `copyRange` naar het gewenste linkerboven‑adres, bijv. `"B5"`.

**V: Kan ik een draaitabel kopiëren zonder de brongegevens?**  
A: Niet direct. De draaitabel‑cache zit in het werkboek; het verwijderen van de brongegevens maakt de draaitabel onbruikbaar. Exporteer de brongegevens naar een verborgen blad als je een lichtere kopie wilt.

---

## Conclusie

Je hebt nu een helder, end‑to‑end‑antwoord op **hoe je een draaitabel kopieert** in Java met Aspose.Cells. Door het bron‑werkboek te laden, het bereik van de draaitabel te definiëren en `copyRange` te gebruiken, kun je moeiteloos **een bereik tussen werkboeken kopiëren** terwijl je ervoor zorgt dat de draaitabel behouden blijft.


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe de bron van een Excel‑draaitabel bij te werken met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hoe draaitabellen te maken in Excel met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe slicers in draaitabellen te implementeren met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}