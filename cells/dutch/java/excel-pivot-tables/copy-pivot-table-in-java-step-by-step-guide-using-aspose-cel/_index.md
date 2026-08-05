---
category: general
date: 2026-08-04
description: Kopieer draaitabel met Aspose.Cells voor Java. Leer hoe je een Excel-bereik
  kopieert, een draaitabel dupliceert en een werkblad met draaitabel kopieert in slechts
  een paar regels.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: nl
lastmod: 2026-08-04
og_description: Kopieer draaitabel met Aspose.Cells voor Java. Deze tutorial leidt
  je door het kopiëren van een Excel-bereik, het dupliceren van een draaitabel en
  het behouden van alle gegevens in een nieuw werkblad.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Kopieer draaitabel in Java – volledige Aspose.Cells‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Kopieer draaitabel in Java – stapsgewijze handleiding met Aspose.Cells
url: /nl/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel in Java – stapsgewijze handleiding met Aspose.Cells

Als je een **draaitabel wilt kopiëren** van het ene werkblad naar het andere in Java, laat deze gids je precies zien hoe je dat doet met Aspose.Cells. Of je nu rapporten programmatically genereert of een data‑migratietool bouwt, je ziet een compleet, uitvoerbaar voorbeeld dat de definitie en gegevens van de draaitabel behoudt.

Het kopiëren van een draaitabel is meer dan alleen een celbereik kopiëren; de onderliggende cache en gegevensbron moeten intact blijven. In deze tutorial behandelen we ook hoe je **excelbereik kunt kopiëren**, hoe je een **draaitabel kunt dupliceren** over werkbladen, en hoe je **een werkblad met draaitabel kunt kopiëren** met dezelfde API.

## Vereisten

* Java Development Kit (JDK) 8 of nieuwer.
* Maven of Gradle om afhankelijkheden te beheren.
* Aspose.Cells voor Java (de nieuwste versie, bijv. 23.12). Voeg de volgende Maven-coördinaat toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Een bronwerkmap (`Source.xlsx`) die een draaitabel bevat op het eerste werkblad.

## Hoe een draaitabel te kopiëren in Java met Aspose.Cells

Het kernidee is om het *bronbereik* dat de draaitabel omsluit te kopiëren en vervolgens in een nieuw werkblad te plakken. Aspose.Cells kopieert automatisch de pivot-cache, zodat het resulterende blad een volledig functionele **dubbele draaitabel** bevat.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Waarom dit werkt

* **Bereikkopie bevat de pivot-cache** – Aspose.Cells behandelt een draaitabel als een speciaal object dat in het celbereik is ingebed. Wanneer je `Range.copy` aanroept, kopieert de bibliotheek zowel de zichtbare cellen als de verborgen cache die de draaitabel aandrijft.
* **Geen handmatige recreatie nodig** – Je hoeft de pivot-velden of gegevensbron niet opnieuw op te bouwen; de duplicaat is direct klaar om te vernieuwen.
* **Werkt met elke Excel-versie** – Het gegenereerde bestand volgt de Office Open XML (XLSX) standaard, zodat Excel 2007+ het kan openen zonder waarschuwingen.

## Excelbereik kopiëren – dezelfde code hergebruiken voor niet‑draaitabelgegevens

Als je alleen een **excelbereik wilt kopiëren** zonder een draaitabel, geldt hetzelfde patroon. Pas gewoon het bereikadres aan naar het gebied dat je wilt dupliceren.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

De methode `copy` behoudt formules, opmaak en opmerkingen, waardoor het een universele oplossing is voor elk blok Excel-gegevens.

## Draaitabel dupliceren over meerdere werkbladen

Soms moet je een **draaitabel dupliceren** meerdere keren—bijv. één per afdeling. Loop over de bestemmingswerkbladen en hergebruik dezelfde `sourceRange.copy`‑aanroep:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Elk nieuw blad bevat een onafhankelijke draaitabel die afzonderlijk kan worden vernieuwd. De cache wordt gedupliceerd, zodat wijzigingen in één blad de anderen niet beïnvloeden.

## Werkblad met draaitabel kopiëren – blad‑niveau instellingen behouden

Als je een **werkblad met draaitabel wilt kopiëren** terwijl je ook de paginainstelling, kolombreedtes en benoemde bereiken behoudt, gebruik dan `Worksheet.copy` in plaats van handmatig een bereik te kopiëren. Deze methode kloont het volledige blad, inclusief de draaitabel.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` is handig wanneer het werkblad grafieken, afbeeldingen of aangepaste stijlen bevat die samen met de draaitabel moeten worden meegenomen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Pivot-cache verloren na kopiëren** | Het gebruik van `Cell.copy` op individuele cellen (in plaats van een bereik) verwijdert de verborgen cache. | Kopieer altijd het *volledige* bereik dat de draaitabel omsluit, zoals getoond in Stap 2. |
| **Bronbereik te klein** | Het bereik omvat niet het gegevensgebied van de draaitabel, waardoor het nieuwe blad alleen statische waarden toont. | Breid het adres uit (bijv. `A1:G20`) om de volledige draaitabel plus eventuele slicers of filters te dekken. |
| **Versie‑mismatch van bestemmingswerkmap** | Opslaan als XLS (legacy) verwijdert moderne draaitabel‑functies. | Sla op als XLSX (standaard) of stel expliciet `SaveFormat.XLSX` in. |
| **Externe gegevensbron verbroken** | De draaitabel verwijst naar een gegevensbron buiten de werkmap; kopiëren embedt deze niet. | Gebruik `PivotTable.refreshData()` na het kopiëren, of embed de brongegevens in dezelfde werkmap. |

## Verwachte output

Na het uitvoeren van het programma:

1. `CopyWithPivot.xlsx` verschijnt in `YOUR_DIRECTORY`.
2. Het openen van het bestand in Excel toont een nieuw blad met de naam **CopySheet**.
3. **CopySheet** bevat een volledig functionele draaitabel die identiek is aan de originele, klaar om te vernieuwen.
4. Alle opmaak, filters en berekende velden zijn behouden.

Als je `FullCopy.xlsx` opent, zie je een volledige replica van het originele werkblad, inclusief eventuele grafieken of afbeeldingen die op het bronblad stonden.

## Samenvatting

* Je hebt geleerd hoe je een **draaitabel kunt kopiëren** in Java met Aspose.Cells.
* Dezelfde aanpak werkt voor een eenvoudige **excelbereik kopiëren** of **copy range java** scenario's.
* Voor bulkbewerkingen kun je een **draaitabel dupliceren** over vele bladen.
* Wanneer je het hele blad nodig hebt, **kopieer een werkblad met draaitabel** met `addCopy`.

## Volgende stappen

* Verken **PivotTable.refreshData()** om de cache programmatically bij te werken na het kopiëren.
* Combineer de kopieerlogica met **Excel-bestandsstreaming** om grote werkmappen te verwerken zonder alles in het geheugen te laden.
* Bekijk de ondersteuning van Aspose.Cells voor **pivot-slicers** als je rapporten afhankelijk zijn van interactieve filters.

Voel je vrij om de code aan te passen aan je eigen projectstructuur, te experimenteren met verschillende bereikgroottes, of het te integreren in een grotere data‑verwerkingspipeline. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende codevoorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel draaitabelbron bij te werken met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel draaitabel manipulatie Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Nieuw Excel-werkboek maken – Kopiëren & dupliceren draaitabel](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}