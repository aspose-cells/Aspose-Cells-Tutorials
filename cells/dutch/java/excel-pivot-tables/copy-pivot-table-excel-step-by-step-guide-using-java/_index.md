---
category: general
date: 2026-06-27
description: Kopieer draaitabel in Excel met Java in enkele minuten – leer hoe je
  een bereik naar een andere werkmap kopieert en ontdek hoe je een draaitabel efficiënt
  kopieert.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: nl
og_description: Kopieer een draaitabel in Excel met Java. Deze gids toont hoe je een
  bereik naar een andere werkmap kopieert en beantwoordt hoe je een draaitabel kopieert
  met een volledig voorbeeld.
og_title: Kopieer draaitabel Excel – Java‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Kopieer draaitabel Excel – Stapsgewijze handleiding met Java
url: /nl/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel Excel – Java Tutorial

Heb je je ooit afgevraagd hoe je **copy pivot table excel** bestanden kunt kopiëren zonder de onderliggende gegevensverbindingen te verliezen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze proberen een draaitabel van het ene werkboek naar het andere te verplaatsen, alleen om uiteindelijk een statisch bereik of een verbroken verwijzing te krijgen.  

Het goede nieuws? Met een paar regels Java en de juiste bibliotheek kun je **copy pivot table excel** werkboeken netjes kopiëren, waarbij elk veld, filter en lay-out behouden blijft. In deze gids laten we je ook zien **how to copy pivot table** met behulp van de Aspose.Cells for Java API, en geven we tips over **copy range to another workbook** voor die rand‑geval scenario's.

> **What you’ll walk away with:** een volledig uitvoerbaar programma dat een bronwerkboek laadt, het bereik met de draaitabel kopieert, en een nieuw werkboek opslaat dat er precies uitziet als het origineel.

## Vereisten

- Java 17 of nieuwer (de code compileert met elke recente JDK).
- Aspose.Cells for Java 23.10 of later – de gratis proefversie werkt prima voor testen.
- Een bron‑Excel‑bestand (`source.xlsx`) dat al een draaitabel bevat op het eerste werkblad.
- Een IDE of een eenvoudige command‑line build‑opstelling (Maven/Gradle).

Er zijn geen andere externe afhankelijkheden vereist.

## Stap 1: Het project opzetten en klassen importeren

Maak eerst een Maven‑project (of Gradle, als je dat liever hebt) en voeg de Aspose.Cells‑dependency toe:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Importeer nu de klassen die we nodig hebben:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Houd je `src/main/resources` map netjes; plaats `source.xlsx` daar en verwijs ernaar met een relatief pad om absolute paden niet hard‑coded te gebruiken.

## Stap 2: Laad het bronwerkboek dat de draaitabel bevat

De eerste stap van elke **copy pivot table excel** operatie is het laden van het werkboek dat de draaitabel bevat die je wilt dupliceren.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Waarom laden we het volledige werkboek in plaats van alleen het blad? Omdat de pivot‑cache op werkboekniveau leeft; alleen het blad kopiëren zou de cache breken en zou je draaitabel veranderen in een gewoon bereik.

## Stap 3: Haal het werkblad op en definieer het draaitabel‑bereik

Vervolgens zoeken we het werkblad en het exacte celblok dat de draaitabel omsluit. In de meeste gevallen begint de draaitabel bij `A1`, maar je moet het bereik aanpassen aan je bestand.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

Als je niet zeker bent van het bereik, kun je Aspose.Cells de gebruikte cellen laten berekenen:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

Dat kleine fragment is handig wanneer je **copy range to another workbook** moet uitvoeren zonder het adres hard‑coded te gebruiken.

## Stap 4: Maak het bestemmings‑werkboek

Nu maken we een nieuw werkboek aan dat de gekopieerde draaitabel zal ontvangen. Dit is het hart van **how to copy pivot table** — je creëert een schone lei en plakt vervolgens het bereik.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

Als je al een sjabloonbestand hebt dat je wilt verrijken, vervang dan gewoon de constructor door `new Workbook("template.xlsx")`.

## Stap 5: Voeg een werkblad toe aan het bestemmings‑werkboek

Hoewel een nieuw `Workbook` al één standaardblad bevat, voegen we een tweede blad toe om het proces van kopiëren naar een specifieke locatie te demonstreren.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

Je kunt het blad een nieuwe naam geven voor duidelijkheid:

```java
dstWs.setName("CopiedPivot");
```

## Stap 6: Kopieer het bereik – draaitabel wordt behouden

Hier is de magische regel die daadwerkelijk **copy range to another workbook** uitvoert terwijl de draaitabel intact blijft. Het `CopyOptions`‑object vertelt Aspose.Cells alles te behouden, inclusief de pivot‑cache.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Waarom stellen we `PasteType.PASTE_ALL` in? Omdat de standaard plakbewerking alleen waarden en opmaak kopieert, waardoor de pivot‑cache wordt weggegooid. Door expliciet `PASTE_ALL` aan te vragen, zorgen we ervoor dat het bestemmings‑werkboek een volledig functionele draaitabel ontvangt.

## Stap 7: Sla het bestemmings‑werkboek op

Schrijf tenslotte het nieuwe bestand naar schijf. Na deze stap kun je `destination.xlsx` in Excel openen en de draaitabel precies zien zoals die in het bronbestand verscheen.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Verwacht resultaat

- Het openen van `destination.xlsx` toont een blad met de naam **CopiedPivot**.
- Het blad bevat een draaitabel die kan worden vernieuwd, gefilterd en herschikt, net als het origineel.
- Er verschijnen geen foutmeldingen in de console, wat bevestigt dat **copy pivot table excel** geslaagd is.

## Veelgestelde vragen & randgevallen

### Wat als het bronwerkboek meerdere draaitabellen heeft?

Je kunt de logica voor bereikselectie herhalen voor elke draaitabel, of je kunt het volledige werkblad kopiëren:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Het kopiëren van het hele blad verplaatst ook alle pivot‑caches, waardoor het een snelle manier is om **copy range to another workbook** uit te voeren wanneer je veel tabellen hebt.

### Hoe om te gaan met externe gegevensverbindingen?

Als je draaitabel gegevens haalt uit een externe database, behoudt het bestemmings‑werkboek de verbindingsreeks. Om verbroken koppelingen te voorkomen, werk je de verbinding bij na het kopiëren:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Werkt dit met .xls‑bestanden?

Ja. Aspose.Cells abstraheert het bestandsformaat, dus dezelfde code werkt voor `.xls`, `.xlsx`, `.xlsb` en zelfs `.ods`. Verander gewoon de bestandsextensie in de `Workbook`‑constructors.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is een kant‑klaar Java‑klasse die **how to copy pivot table** van het ene werkboek naar het andere demonstreert:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Voer de klasse uit, open `destination.xlsx`, en je ziet een exacte replica van de oorspronkelijke draaitabel. 🎉

## Conclusie

We hebben zojuist een volledige **copy pivot table excel** workflow doorlopen met Java. Door het bronwerkboek te laden, het draaitabel‑bereik te bepalen en `CopyOptions` met `PASTE_ALL` te gebruiken, kun je betrouwbaar **copy range to another workbook** uitvoeren terwijl elke draaitabel‑functie behouden blijft.  

Als je benieuwd bent naar **how to copy pivot table** in andere talen, gelden dezelfde concepten — vervang gewoon de Aspose.Cells SDK door het juiste platform. Vervolgens kun je onderzoeken hoe je de gekopieerde draaitabel programmatisch kunt vernieuwen, of hoe je deze naar PDF exporteert voor rapportagedoeleinden.  

Heb je een variatie op dit scenario? Misschien moet je een grafiek kopiëren die gekoppeld is aan een draaitabel, of wil je tientallen bestanden in batch verwerken. Die onderwerpen zijn natuurlijke uitbreidingen van wat we vandaag hebben behandeld.  

Probeer de code, pas het bereik aan, en laat je Excel‑automatiseringsavonturen beginnen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}