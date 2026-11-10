---
category: general
date: 2026-09-27
description: Kopieer draaitabel in Java met Aspose.Cells – een stapsgewijze handleiding
  die laat zien hoe je een bereik kopieert en draaitabeldefinities behoudt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: nl
lastmod: 2026-09-27
og_description: Kopieer een draaitabel in Java met Aspose.Cells. Volg deze volledige
  tutorial om een bereik te kopiëren met Aspose.Cells en de draaitabeldefinities intact
  te houden.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Kopieer een draaitabel in Java – Aspose.Cells snelle gids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe een draaitabel te kopiëren in Java met Aspose.Cells
url: /nl/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een pivot table te kopiëren in Java met Aspose.Cells

Als je een **pivot table** van het ene werkboek naar het andere moet kopiëren, laat deze gids je precies zien hoe je dat doet met Aspose.Cells voor Java. De oplossing werkt voor elke pivot die je hebt gemaakt, en behoudt de pivot‑definitie zonder handmatige recreatie.

Je leert hoe je het bronbestand laadt, het bereik dat de pivot bevat definieert, dat bereik naar een nieuw werkboek kopieert en uiteindelijk het resultaat opslaat. De tutorial behandelt ook veelvoorkomende valkuilen, zoals het behouden van gegevensbronnen en het omgaan met grote werkboeken.

## Wat je nodig hebt

* Java 17 of later (de code compileert ook met JDK 8+)
* Aspose.Cells for Java 23.9 of nieuwer – de nieuwste versie biedt de meest betrouwbare **copy range aspose cells** ondersteuning
* Een bron‑Excel‑bestand dat een pivot table bevat (bijv. `SourceWithPivot.xlsx`)
* Een IDE of build‑tool (Maven/Gradle) die de Aspose.Cells‑JAR kan refereren

## Stap 1: Laad het bron‑werkboek dat de pivot table bevat

De eerste actie is het openen van het werkboek dat de pivot bevat die je wilt dupliceren. Het laden van het bestand creëert een in‑memory weergave van alle werkbladen, cellen en pivot‑caches.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Waarom dit belangrijk is:**  
Aspose.Cells leest het volledige werkboek, inclusief verborgen pivot‑cache‑bladen. Als je deze stap overslaat, zou de daaropvolgende **copy pivot table**‑bewerking de onderliggende gegevensbron verliezen.

## Stap 2: Maak een leeg bestemmings‑werkboek

Vervolgens maak je een nieuw werkboek aan dat de gekopieerde pivot zal ontvangen. Beginnen met een schoon werkboek voorkomt onbedoelde overschrijvingen.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tip:** Het standaard werkboek bevat één leeg blad, wat perfect is voor een eenvoudige kopie. Als je moet kopiëren naar een specifiek bladnaam, hernoem `destWs` met `destWs.setName("TargetSheet")`.

## Stap 3: Definieer het bronbereik dat de pivot table bevat

Een pivot table beslaat een rechthoekig blok cellen. Je moet het exacte bereik specificeren; anders wordt alleen ruwe data gekopieerd. In dit voorbeeld gaan we ervan uit dat de pivot **A1:G20** beslaat, maar je kunt het adres aanpassen aan je bestand.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Waarom dit werkt:**  
Wanneer je `createRange` aanroept op de `Cells`‑collectie van het werkblad, neemt Aspose.Cells de pivot‑definitie, de cache en eventuele opmaak op. Dit is de kern van **how to copy pivot table** correct.

## Stap 4: Kopieer het gedefinieerde bereik naar het bestemmingsblad

Gebruik nu de `copy`‑methode om het bereik te dupliceren. De methode kopieert alles binnen het bereik, inclusief de pivot‑definitie, formules en stijlen.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Belangrijke opmerking:**  
Als je alleen de data zonder de pivot nodig hebt, kun je `srcRange.copyData` gebruiken. Voor een echte **copy pivot table** moet je echter het volledige bereik kopiëren zoals hierboven getoond.

## Stap 5: Sla het bestemmings‑werkboek op

Schrijf tenslotte het nieuwe werkboek naar schijf. Het resulterende bestand zal een volledig functionele pivot table bevatten die identiek is aan de bron.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Het uitvoeren van het programma produceert `CopyPivotResult.xlsx` met dezelfde pivot‑lay-out, filters en berekeningen als het originele bestand.

## Verwachte output

Wanneer je `CopyPivotResult.xlsx` in Excel opent:

* De pivot table verschijnt op **A1:G20** op het eerste blad.
* Alle rij‑/kolomvelden, filters en waardevelden blijven intact.
* Het vernieuwen van de pivot werkt dezelfde gegevensbron bij als het bron‑werkboek (als de brongegevens zijn ingebed).

## Randgevallen en praktische tips

| Situation | How to handle it |
|-----------|------------------|
| **Pivot beslaat meer kolommen dan verwacht** | Gebruik `srcWs.getPivotTables().get(0).getPivotTableArea()` om het exacte adres programmatisch te verkrijgen. |
| **Bron‑werkboek bevat meerdere pivots** | Loop door `srcWs.getPivotTables()` en kopieer elk bereik afzonderlijk, waarbij je de bestemmingsadressen aanpast. |
| **Grote werkboeken veroorzaken geheugenbelasting** | Schakel `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` in vóór het laden van de bron. |
| **Je moet alleen de pivot‑definitie kopiëren, niet de gegevens** | Verwijder na het kopiëren de bron‑datageregels in de bestemming met `destWs.getCells().deleteRows(startRow, count)`. |
| **Bestemmingsbestand moet originele opmaak behouden** | Stel `CopyOptions` in met `options.setPasteType(PasteType.ALL)` voor een volledige kopie met behoud van opmaak. |

**Pro tip:** Controleer altijd de gekopieerde pivot door programmatically `destWs.getPivotTables().get(0).refresh()` aan te roepen. Dit zorgt ervoor dat de cache up‑to‑date is, vooral wanneer de brongegevens zich in een externe verbinding bevinden.

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt copy‑paste in je IDE. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op jouw machine.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Het uitvoeren van deze code zal **copy pivot table** precies zoals beschreven, en het demonstreert de meest rechttoe rechtaan manier om **copy range aspose cells** te gebruiken terwijl de pivot‑functionaliteit behouden blijft.

## Conclusie

Je weet nu hoe je een **copy pivot table** in Java kunt uitvoeren met Aspose.Cells, van het laden van het bron‑werkboek tot het opslaan van het bestemmingsbestand. De gids besprak de essentiële stappen, legde uit waarom elke stap belangrijk is, en behandelde veelvoorkomende randgevallen.

Vervolgens kun je verkennen:

* **how to copy pivot table** over verschillende werkbladen binnen hetzelfde werkboek
* Het gebruik van **copy range aspose cells** om grafieken of voorwaardelijke opmaak te dupliceren
* Het automatiseren van pivot‑verversing na het kopiëren om gegevens actueel te houden

Voel je vrij om te experimenteren met grotere bereiken, meerdere pivots, of deze logica te integreren in een grotere Excel‑verwerkingspipeline. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Kopieer Pivot Table in Java – Bewaar het, Exporteer naar PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Hoe de bron van een Excel Pivot Table bij te werken met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulatie met Aspose.Cells Java: Een uitgebreide gids](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}