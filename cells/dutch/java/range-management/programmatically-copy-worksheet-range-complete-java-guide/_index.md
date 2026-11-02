---
category: general
date: 2026-06-21
description: Programmeermatig een werkbladbereik kopiëren in Java met Aspose.Cells.
  Leer hoe je een Excel‑bereik efficiënt naar een ander werkboek kunt kopiëren.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: nl
og_description: Programmeermatig een werkbladbereik kopiëren in Java. Deze gids laat
  zien hoe je een Excel-bereik naar een andere werkmap kopieert met volledige code
  en tips.
og_title: Programmatig Werkbladbereik Kopiëren – Java Stap‑voor‑stap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Programmatig Werkbladbereik Kopiëren – Complete Java‑gids
url: /nl/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmatiche Kopie van Werkbladbereik – Complete Java Gids

Heb je je ooit afgevraagd hoe je **programmatiche een werkbladbereik kunt kopiëren** zonder Excel handmatig te openen? Je bent niet de enige. Of je nu een rapport wilt dupliceren, een pivot‑gedreven dashboard wilt klonen, of simpelweg gegevens tussen bestanden wilt verplaatsen, dit in code doen bespaart tijd en elimineert menselijke fouten.

In deze tutorial lopen we stap voor stap door een nette, end‑to‑end oplossing die laat zien **hoe je een Excel‑bereik naar een andere werkmap kopieert** met Java en de Aspose.Cells‑bibliotheek. Aan het einde heb je een kant‑klaar programma, begrijp je de reden achter elke stap, en weet je welke valkuilen je moet vermijden.

---

## Wat je nodig hebt

- **Java Development Kit (JDK) 11+** – de code compileert met elke recente JDK.
- **Aspose.Cells for Java** (gratis proefversie of gelicentieerde versie). Voeg de Maven‑dependency toe of download de JAR.
- Twee Excel‑bestanden: een `input.xlsx` dat het bronbereik bevat (inclusief een draaitabel) en een lege `output.xlsx` waar het bereik terechtkomt.
- Elke IDE die je wilt – IntelliJ IDEA, Eclipse, of zelfs een eenvoudige teksteditor.

Dat is alles. Geen extra services, geen COM‑interop, alleen pure Java.

---

![Diagram illustrating programmatically copy worksheet range between two workbooks](image.png)

*Afbeelding alt‑tekst: illustratie van programmatiche kopie van werkbladbereik*

---

## Stap 1: Het project opzetten en Aspose.Cells importeren

Allereerst moeten we de bibliotheek op het classpath hebben. Als je Maven gebruikt, voeg dan toe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Als je de JAR handmatig wilt gebruiken, plaats deze dan in je `libs`‑map en voeg hem toe aan het build‑pad.

Waarom dit belangrijk is: Aspose.Cells biedt ons een rijk objectmodel (`Workbook`, `Worksheet`, `Range`) waarmee we gegevens **inclusief draaitabellen, formules en opmaak** in één enkele oproep kunnen kopiëren – iets wat de gewone Apache POI‑bibliotheek niet zo netjes kan.

---

## Stap 2: Het bron‑werkboek laden

We openen het werkboek dat de gegevens bevat die we willen klonen. De `Workbook`‑constructor neemt een bestandspad, en Aspose leest het volledige bestand in het geheugen.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Pro tip:* Plaats het laden in een try‑catch‑blok als het bestand mogelijk ontbreekt; anders stopt het programma met een duidelijke foutmelding.

---

## Stap 3: Een leeg bestemmings‑werkboek maken

Een nieuw werkboek geeft ons een schoon canvas. We hoeven geen bladen vooraf te vullen; Aspose voegt er één voor ons toe.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Waarom niet het bron‑werkboek hergebruiken? Door ze gescheiden te houden voorkom je per ongeluk overschrijven en maak je de code herbruikbaar voor batch‑operaties.

---

## Stap 4: Het exacte bereik definiëren dat gekopieerd moet worden

Hier begint de **programmatiche kopie van werkbladbereik** magie. We selecteren de cellen `A1:D20` van het eerste werkblad van het bronbestand. De methode `createRange` retourneert een `Range`‑object dat precies die cellen representeert, inclusief draaitabellen.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Als je een dynamisch bereik nodig hebt (bijv. “laatste gebruikte rij”), kun je het hard‑gecodeerde adres vervangen door `Cells.maxDisplayRange` of berekenen met `Cells.getMaxDataColumn()` en `Cells.getMaxDataRow()`.

---

## Stap 5: Een doelwerkblad toevoegen in het bestemmings‑werkboek

Aspose maakt een standaardblad genaamd “Sheet1” aan wanneer je `Workbook` instantiateert. We voegen een nieuw blad toe om het overzichtelijk te houden, vooral als je later meerdere bereiken wilt kopiëren.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Je kunt het blad een vriendelijke naam geven:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Stap 6: De kopie uitvoeren – inclusief draaitabellen

Nu de kernoperatie: `copyRange`. Deze methode kopieert **waarden, formules, opmaak en ingesloten objecten** (zoals draaitabellen) van het bronbereik naar een doelcel (`A1` in ons nieuwe blad). Het is de eenvoudigste manier om **hoe je een Excel‑bereik naar een andere werkmap kopieert** te realiseren zonder low‑level cel‑lussen.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Achter de schermen serialiseert Aspose het bronbereik naar een intermediair formaat en deserialiseert het vervolgens in het doelblad—zodat alles intact blijft.

---

## Stap 7: Het bestemmings‑werkboek opslaan en verifiëren

Tot slot schrijven we het bestemmings‑werkboek naar schijf. Open `output.xlsx` in Excel om het gekopieerde bereik, de draaitabel en alle opmaak te zien.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Wanneer je `output.xlsx` opent, zou je een blad met de naam “CopiedData” moeten zien met dezelfde lay‑out als `A1:D20` uit de bron, inclusief de draaitabel die nu naar de gekopieerde gegevens wijst.

---

## Veelvoorkomende randgevallen afhandelen

### 1. Kopiëren tussen verschillende Excel‑versies
Aspose.Cells werkt met `.xls`, `.xlsx`, `.xlsb` en zelfs `.csv`. Als de bron‑ en bestemmingsformaten verschillen, converteert de bibliotheek ze automatisch. Zorg er alleen voor dat de bestandsextensies overeenkomen met de gewenste output.

### 2. Externe gegevensbronnen in draaitabellen behouden
Als de draaitabel in de bron een externe gegevensbron (bijv. een database‑verbinding) referereert, behoudt de gekopieerde draaitabel de connection‑string maar **ververst deze niet automatisch**. Roep `pivotTable.refreshData()` aan na het kopiëren als je up‑to‑date resultaten nodig hebt.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Grote bereiken en geheugenverbruik
Het kopiëren van enorme bereiken (honderdduizenden rijen) kan het geheugen sterk belasten. Gebruik `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` vóór het laden van grote bestanden om de footprint laag te houden.

### 4. Meerdere bladen of bereiken
Als je verschillende niet‑aaneengesloten bereiken moet kopiëren, herhaal dan stappen 4‑6 voor elk bereik, of gebruik `copyRange` met een unie‑bereik (`Cells.createRange("A1:B10,C1:D10")`).

---

## Pro‑tips voor robuuste automatisering

- **Valideer het bronbereik** vóór het kopiëren. Gebruik `sourceRange.isValid()` om runtime‑fouten te voorkomen.
- **Ontgrendel het bestemmingsbestand** met `FileInfo.setReadOnly(false)` als je een bestaand werkboek overschrijft.
- **Log acties** met een lichte logger (SLF4J) – vooral handig bij batch‑verwerking.
- **Dispose werkboeken** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) in langdurige services om native resources vrij te geven.

---

## Volledig Werkend Voorbeeld Samenvatting

Hieronder vind je de complete, zelfstandige Java‑klasse die je kunt plakken in je IDE en uitvoeren. Vergeet niet `YOUR_DIRECTORY` te vervangen door het daadwerkelijke mappad op jouw machine.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Verwachte output:** Een `output.xlsx`‑bestand met een blad genaamd “CopiedData”. Cellen `A1:D20` zullen een exacte kopie van de bron zijn, en elke draaitabel binnen dat blok zal volledig functioneel zijn, wijzend naar de gekopieerde gegevens.

---

## Conclusie

We hebben zojuist een nette, **programmatiche kopie van werkbladbereik** oplossing in Java gedemonstreerd, waarmee de veelgestelde vraag **hoe je een Excel‑bereik naar een andere werkmap kopieert** wordt beantwoord. Door gebruik te maken van de high‑level API van Aspose.Cells vermeden we low‑level cel‑lussen, behouden we draaitabellen en blijft de code leesbaar.

Wat nu? Probeer dit patroon uit te breiden naar:

- Het kopiëren van volledige werkbladen in plaats van één bereik.
- Batch‑verwerking van tientallen werkboeken in een map.
- Exporteren van het gekopieerde bereik naar CSV of PDF voor rapportage‑pijplijnen.

Voel je vrij om te experimenteren, en als je ergens vastloopt, laat een reactie achter. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Excel Columns Efficiently Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}