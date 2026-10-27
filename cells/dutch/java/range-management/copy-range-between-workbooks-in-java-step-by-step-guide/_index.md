---
category: general
date: 2026-08-14
description: Bereik tussen werkmappen kopiëren met Java en Aspose.Cells. Leer hoe
  je een draaitabel-werkmap kopieert, een afbeelding exporteert naar PowerPoint en
  AutoFilter verwijdert uit een Excel‑tabel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: nl
lastmod: 2026-08-14
og_description: Kopieer bereik tussen werkboeken in Java. Deze gids laat zien hoe
  je een draaitabel‑werkboek kopieert, een afbeelding exporteert naar PowerPoint en
  AutoFilter verwijdert uit een Excel‑tabel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Bereik kopiëren tussen werkboeken in Java – volledige Aspose.Cells‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Bereik kopiëren tussen werkboeken in Java – stap‑voor‑stap gids
url: /nl/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bereik tussen werkboeken kopiëren in Java – stapsgewijze handleiding

Als je **een bereik tussen werkboeken** in Java moet kopiëren, biedt Aspose.Cells een nette API die complexe objecten zoals draaitabellen en afbeeldingen afhandelt. Deze tutorial laat zien hoe je **een draaitabel‑werkboek kopieert**, **een afbeelding exporteert naar PowerPoint**, en **AutoFilter verwijdert uit een Excel‑tabel**, terwijl de code gemakkelijk leesbaar en onderhoudbaar blijft.

Je leert hoe je:

* Een bron‑werkboek laadt en het bron‑bereik definieert.  
* Een bestemmings‑werkboek maakt en het bereik kopieert zodat de draaitabel intact blijft.  
* De eerste afbeelding op het blad exporteert als een bewerkbaar PowerPoint‑object.  
* Een AutoFilter verwijdert uit de eerste Excel‑tabel.  
* Een werkboek laadt met `SmartMarkerOptions` om JSON‑arrays als één celwaarde te behandelen.

Het voorbeeld gebruikt Aspose.Cells 23.10 voor Java, maar de concepten zijn ook van toepassing op eerdere versies.

---

## Voorwaarden

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Java 17 of nieuwer | Vereist door de nieuwste Aspose.Cells runtime. |
| Aspose.Cells for Java (Maven‑artifact `com.aspose:aspose-cells`) | Biedt de `Workbook`, `Worksheet`, `Range` en gerelateerde klassen die in de code worden gebruikt. |
| Een bron‑Excel‑bestand (`src.xlsx`) dat een draaitabel, een afbeelding en een tabel met een AutoFilter bevat. | De tutorial manipuleert deze objecten om elke functie te demonstreren. |
| De tutorial manipuleert deze objecten om elke functie te demonstreren. | |

Voeg de Maven‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Bereik tussen werkboeken kopiëren – bron‑ en bestemmings‑werkboek laden

De eerste stap is het bron‑werkboek openen, het bereik selecteren dat de gegevens bevat die je wilt kopiëren, en een leeg bestemmings‑werkboek maken.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Waarom dit belangrijk is:** Door `Range.copy` te gebruiken, kopieert Aspose.Cells niet alleen ruwe celwaarden maar ook de onderliggende draaitabel‑cache, waardoor de draaitabel functioneel blijft in het bestemmings‑werkboek.

---

## Draaitabel‑werkboek kopiëren terwijl het bereik wordt gekopieerd

Kopieer nu het gedefinieerde bereik van het bron‑werkboek naar het bestemmings‑werkboek. De draaitabel wordt automatisch behouden omdat het bereik de draaitabel‑cache bevat.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Resultaat:** Het openen van `destination.xlsx` toont dezelfde draaitabel‑indeling als `src.xlsx`. Er is geen extra code nodig om de draaitabel‑cache opnieuw op te bouwen.

---

## Afbeelding exporteren naar PowerPoint

Aspose.Cells kan een afbeelding markeren voor export naar een bewerkbaar PowerPoint‑object. De onderstaande code selecteert de eerste afbeelding op het bestemmingsblad en zet de export‑vlag.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Wat je ziet:** Het openen van `destination.pptx` in PowerPoint toont de afbeelding als een native vorm die je kunt bewerken, schalen of animeren.

---

## AutoFilter verwijderen uit Excel‑tabel

Als het bronblad een tabel met een AutoFilter bevat, wil je deze mogelijk na het kopiëren wissen. De code hieronder benadert de eerste tabel en verwijdert de filter.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effect:** De tabel blijft in het werkboek, maar de vervolgkeuzepijlen van de filter verdwijnen, waardoor je een overzichtelijke weergave van de gegevens krijgt.

---

## Werkboek laden met SmartMarker‑opties – JSON‑arrays behandelen als één cel

Wanneer je een rapport genereert vanuit JSON, kan Aspose.Cells een volledige array als één celwaarde behandelen. Dit is handig om JSON‑strings in een sjabloon in te voegen zonder ze over meerdere cellen te verspreiden.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Waarom je dit zou gebruiken:** Als je JSON‑payload een array bevat die als een JSON‑string in één cel moet verschijnen, voorkomt `setArrayAsSingle(true)` dat Aspose.Cells de array uitbreidt naar afzonderlijke rijen of kolommen.

---

![Bereik tussen werkboeken kopiëren in Java – Aspose.Cells codevoorbeeld](copy-range-workbooks.png)

*Afbeeldingsalt‑tekst:* **Bereik tussen werkboeken kopiëren in Java – Aspose.Cells codevoorbeeld** (komt overeen met het primaire zoekwoord).

---

## Verwachte output

| Bestandsnaam               | Bevat |
|----------------------------|-------|
| `destination.xlsx`         | Gekopieerd bereik met functionele draaitabel. |
| `destination.pptx`         | Afbeelding geëxporteerd als een bewerkbare PowerPoint‑vorm. |
| `final_output.xlsx`        | Tabel zonder AutoFilter‑pijlen. |
| `template_filled.xlsx`     | JSON‑array opgeslagen als een enkele celwaarde. |

Open elk bestand in de bijbehorende applicatie (Excel of PowerPoint) om te verifiëren dat de bewerkingen geslaagd zijn.

---

## Conclusie

Je weet nu hoe je **een bereik tussen werkboeken** in Java kunt kopiëren met Aspose.Cells, terwijl je een draaitabel behoudt, een afbeelding exporteert naar PowerPoint en een AutoFilter verwijdert uit een Excel‑tabel. Hetzelfde patroon kan worden uitgebreid om elk Excel‑bereik naar een nieuw werkboek te kopiëren, SmartMarker‑JSON‑arrays te verwerken, of extra transformaties te ketenen.

Volgende stappen die je kunt verkennen:

* **Excel‑bereik kopiëren naar nieuw werkboek** met meerdere werkbladen.  
* Gebruik **export picture to PowerPoint** voor batch‑afbeeldingsextractie.  
* Pas **remove autofilter from excel table** toe in grotere rapportage‑pijplijnen.  
* Combineer deze technieken met Aspose.Slides voor volledige Excel‑naar‑PowerPoint‑automatisering.

Voel je vrij om te experimenteren met verschillende bereik‑adressen, meerdere draaitabellen of aangepaste afbeeldingsformaten. De Aspose.Cells API is ontworpen voor programmeerbare flexibiliteit, zodat je de hier getoonde patronen kunt aanpassen aan elke enterprise‑Excel‑automatiseringsscenario.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Afbeeldingen tussen werkbladen kopiëren in Excel met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Pagina‑instellingen kopiëren tussen werkbladen in Excel met Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel‑werkbladen kopiëren tussen werkboeken](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}