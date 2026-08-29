---
category: general
date: 2026-07-14
description: Kopieer draaitabel tussen werkmappen met Java. Leer hoe je een draaitabel
  kopieert, een Excel-bereik kopieert en een draaitabel in enkele minuten exporteert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: nl
lastmod: 2026-07-14
og_description: Kopieer draaitabel in Java snel. Deze gids laat zien hoe je een draaitabel
  kopieert, een Excel-bereik kopieert en een draaitabel exporteert met Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Kopieer draaitabel tussen werkmappen – Java‑automatiseringstutorial
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Kopieer draaitabel tussen werkmappen – Stapsgewijze Java‑gids
url: /nl/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel tussen werkboeken – Complete Java-tutorial

Heb je ooit een **draaitabel moeten kopiëren** van het ene werkboek naar het andere en je afgevraagd waarom de gebruikelijke copy‑paste trucjes de lay-out breken? Je bent niet de enige. In veel rapportage‑pipelines staat de draaitabel in een master‑bestand, maar downstream‑processen hebben een lichtgewicht kopie nodig.  

In deze gids lopen we stap voor stap een nette, programmeerbare manier door om een draaitabel te dupliceren – zonder handmatig gedoe. Aan het einde weet je **hoe je een draaitabel kopieert**, hoe je **een Excel‑bereik veilig kopieert**, en zelfs hoe je **een draaitabel exporteert** naar een nieuw bestand, allemaal met Aspose.Cells voor Java.

## Wat je gaat bouwen

- Laad een bron‑werkboek dat al een draaitabel bevat.  
- Maak (of open) een doel‑werkboek.  
- Definieer het exacte bereik dat de draaitabel bevat.  
- Kopieer dat bereik – inclusief de draaitabeldefinitie – naar het nieuwe werkboek.  
- Sla het resultaat op zodat andere apps het kunnen openen zonder berekeningen te verliezen.

Geen externe tools, geen VBA, alleen pure Java‑code die je in elk Maven‑ of Gradle‑project kunt plaatsen.

## Vereisten

- Java 17 of hoger (de code werkt op Java 8+, maar nieuwere JDK’s geven betere prestaties).  
- Aspose.Cells voor Java 23.9 of nieuwer – voeg de dependency toe vanuit Maven Central.  
- Twee Excel‑bestanden: `SourceWithPivot.xlsx` (bevat de draaitabel) en een lege placeholder voor de kopie.  

Als je nieuw bent met Aspose.Cells, abstraheert de bibliotheek de low‑level OOXML‑details, zodat je werkbladen kunt behandelen als gewone Java‑objecten.

## Stap 1: Zet je project op

Voeg eerst het Aspose.Cells Maven‑artifact toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Of, voor Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Pro tip:** Als je een IDE zoals IntelliJ gebruikt, laat die de bibliotheek automatisch importeren; dat bespaart veel typen.

## Stap 2: Laad het bron‑werkboek

We hebben een `Workbook`‑instantie nodig die naar het bestand wijst dat de draaitabel bevat. De constructor leest het volledige bestand in het geheugen, zodat je offline kunt werken.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Waarom eerst laden? Omdat de cache, veldlijst en lay-out van de draaitabel allemaal in het blad zijn opgeslagen. Het werkboek in het geheugen halen garandeert dat we de *definitie* kopiëren en niet alleen de gerenderde waarden.

## Stap 3: Maak of open het doel‑werkboek

Je hebt twee opties: begin met een gloednieuw werkboek, of open een bestaand sjabloon. Hier maken we een leeg werkboek, wat de meest voorkomende situatie is wanneer je een schone kopie nodig hebt.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Als je later besluit om naar een specifiek blad te kopiëren, vervang dan `getWorksheets().get(0)` door de juiste index of naam.

## Stap 4: Definieer het exacte bereik dat de draaitabel bevat

Een draaitabel beslaat meestal een rechthoekig blok. De veiligste aanpak is om de boven‑linker‑ en onder‑rechter‑cellen expliciet op te geven. In ons voorbeeld leeft de draaitabel van **A1** tot **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Waarom niet `copyRows` gebruiken?**  
> `copyRows` kopieert ruwe celwaarden maar negeert de onderliggende draaitabel‑cache. Door het hele bereik te kopiëren behoudt Aspose.Cells de metadata van de draaitabel, waardoor de bestemming volledige interactiviteit behoudt.

## Stap 5: Kopieer het bereik (inclusief de draaitabel) naar de bestemming

Nu gebeurt de magie. De `copy`‑methode kloont alles – waarden, formules, opmaak en het draaitabel‑object zelf – naar de doel‑locatie.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Als je naar een andere cel wilt plakken, wijzig dan `"A1"` naar `"C5"` of een ander adres. De methode past interne referenties automatisch aan zodat de draaitabel blijft werken.

## Stap 6: Sla het doel‑werkboek op

Schrijf tenslotte het nieuwe werkboek naar schijf. Het resulterende bestand kan worden geopend in Excel, LibreOffice of elke andere spreadsheet‑viewer, en de draaitabel zal zich exact hetzelfde gedragen als in de bron.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Verwacht resultaat

- `CopyPivotResult.xlsx` opent met een volledig functionerende draaitabel die identiek is aan het origineel.  
- Alle slicers, filters en berekende velden blijven intact.  
- Geen gegevensverlies – waarden worden on‑the‑fly berekend wanneer je de draaitabel vernieuwt.

## Veelvoorkomende variaties & randgevallen

| Situatie | Wat aan te passen |
|-----------|----------------|
| **Kopiëren naar een bestaand werkboek** | Laad het doel‑werkboek in plaats van een nieuw te maken: `new Workbook("ExistingFile.xlsx")`. |
| **Draaitabel heeft onbekende grootte** | Gebruik `Worksheet.getPivotTables().get(0).getPivotTableRange()` om het exacte adres programmatisch op te halen. |
| **Gegevensverbindingen behouden** | Roep na het kopiëren `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` aan om externe datakoppelingen levend te houden. |
| **Draaitabel exporteren als CSV** | Zodra gekopieerd, kun je `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` aanroepen – dit vlakt alleen de draaitabelwaarden uit. |

> **Let op:** Wanneer de bron‑ en doel‑werkboeken verschillende locale‑instellingen gebruiken, kunnen getal‑formaten verschuiven. Stel expliciet de workbook‑`setLocale` in als je consistentie nodig hebt.

## Volledig werkend voorbeeld (Alle imports inbegrepen)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Voer het programma uit, open `CopyPivotResult.xlsx`, en je ziet exact dezelfde draaitabel als waarmee je begon – klaar voor verdere analyse of distributie.

## Samenvatting

We hebben zojuist **hoe je een draaitabel kopieert** van het ene werkboek naar het andere laten zien met Aspose.Cells voor Java. De stappen omvatten het laden van de bron, het definiëren van het exacte **Excel‑bereik kopiëren**, het uitvoeren van de kopie, en tenslotte **de draaitabel exporteren** naar een nieuw bestand. Door het bereik te behandelen in plaats van individuele cellen, garanderen we dat de interne cache van de draaitabel meereist, waardoor het rapport dynamisch blijft.

## Wat je hierna kunt verkennen

- **Automatisch vernieuwen**: Plan de kopieer‑operatie met een Quartz‑job zodat je downstream‑bestanden up‑to‑date blijven.  
- **Meerdere draaitabellen kopiëren**: Loop door `sourceWorkbook.getWorksheets().get(0).getPivotTables()` en kopieer elke naar afzonderlijke bladen.  
- **Stijlen toepassen**: Gebruik `Style`‑objecten om lettertypen en kleuren in het doel‑werkboek te harmoniseren.  

Als je vragen hebt over het omgaan met grote werkboeken of het behouden van externe gegevensbronnen, laat dan een reactie achter. Veel programmeerplezier, en geniet van de vrijheid van programmeerbare Excel‑automatisering!


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}