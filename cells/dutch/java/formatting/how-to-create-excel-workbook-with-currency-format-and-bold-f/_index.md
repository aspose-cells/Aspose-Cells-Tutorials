---
category: general
date: 2026-08-20
description: Maak een Excel-werkmap in Java met Aspose.Cells, stel het valutavormaat
  in, voeg vette opmaak toe en importeer een stijlarray voor gestylede cellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: nl
lastmod: 2026-08-20
og_description: Maak een Excel-werkmap in Java, stel het valutavormaat in, voeg vetgedrukte
  tekst toe en leer hoe je stijl kunt importeren met Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Maak een Excel-werkboek met gestylede valutacellen in Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Hoe een Excel-werkboek te maken met valutavormaat en vet lettertype in Java
url: /nl/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel-werkmap te maken met valutavormaat en vet lettertype in Java

Als je **een Excel-werkmap** programmatisch moet maken, laat deze gids je precies zien hoe. We lopen stap voor stap door het bouwen van een werkmap, het toepassen van een valutavormaat, het toevoegen van een vet lettertype, en het gebruiken van de **how to import style**‑functie van Aspose.Cells zodat elke geïmporteerde cel er consistent uitziet.

Je eindigt met een kant‑klaar `DataTableWithStyleArray.xlsx`‑bestand dat getallen als dollars weergeeft en ze vet markeert. Handmatige opmaak in Excel is niet nodig.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

- Java 17 of later geïnstalleerd.  
- Een Aspose.Cells for Java‑licentie (of een gratis evaluatiesleutel).  
- Maven of Gradle om de `aspose-cells`‑afhankelijkheid te beheren.  
- Basiskennis van Java‑collecties en `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** Als je een `LicenseException` tegenkomt, plaats je licentiebestand in de classpath en roep `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` aan voordat je de werkmap maakt.

## Hoe een Excel-werkmap te maken met gestileerde valutacellen

Deze sectie bevat de kernstappen. Elke stap legt **waarom** het belangrijk is uit, niet alleen **wat** je moet typen.

### Stap 1: Initialiseer de werkmap en het werkblad

Het maken van een nieuwe werkmap geeft je een schone container voor alle daaropvolgende opmaak.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Waarom:** Het `Workbook`‑object vertegenwoordigt het volledige Excel‑bestand. Toegang tot het eerste `Worksheet` stelt je in staat meteen gegevens te gaan vullen.

### Stap 2: Bouw een DataTable met numerieke gegevens

Een `DataTable` bootst een databasetabel na, waardoor het eenvoudig is om rijen in één keer te importeren.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Waarom:** Het gebruik van `DOUBLE` garandeert dat de waarden hun decimale precisie behouden, wat essentieel is wanneer je later **cellen valuta opmaakt**.

### Stap 3: Definieer een stijl – valutavormaat en vet lettertype

Hier **stellen we het valutavormaat in** en **voegen we vet lettertype toe** aan een `Style`‑object.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Waarom:** De `Number`‑opmaakstring `$#,##0.00` vertelt Excel de cel als een geldwaarde te behandelen, terwijl `setBold(true)` de aandacht op de getallen vestigt. Het plaatsen van de stijl in een array bereidt ons voor op de **how to import style**‑stap.

### Stap 4: Configureer importopties om de stijlarray te gebruiken

Aspose.Cells laat je een `Style[]` doorgeven via `ImportTableOptions`. Dit is de officiële **how to import style**‑methode.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Waarom:** Zonder `ImportTableOptions` zouden geïmporteerde cellen de standaardstijl erven, waardoor de valutavormaat en vetgedruktheid die we hebben gedefinieerd verloren gaan.

### Stap 5: Importeer de DataTable in het werkblad

Nu brengen we de gegevens in het blad op cel `A1`, waarbij de stijlarray automatisch wordt toegepast.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` geeft aan dat de eerste rij van de `DataTable` kolomkoppen bevat.  
- `"A1"` is de linkerbovenhoek waar de import begint.

> **Waarom:** Importeren met de stijlarray garandeert dat elke geïmporteerde cel de **format cells currency**‑stijl krijgt die we eerder hebben voorbereid.

### Stap 6: Sla de werkmap op naar schijf

Tot slot schrijven we de in‑memory werkmap naar een fysiek bestand.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Waarom:** Opslaan maakt de opmaak permanent, zodat jij of downstream‑processen het bestand in Excel kunnen openen met het gewenste uiterlijk.

## Volledige broncode

Hieronder staat de complete, kant‑klaar te draaien Java‑klasse. Kopieer deze in je IDE, vervang `YOUR_DIRECTORY` door een bestaande map, en voer uit.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Verwachte output

Wanneer je `DataTableWithStyleArray.xlsx` opent in Microsoft Excel, zie je:

| Bedrag |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- De getallen worden weergegeven met een **valutavormaat** (`$`‑symbool, twee decimalen).  
- Het lettertype van beide cellen is **vet**, waardoor ze opvallen.

## Veelvoorkomende variaties en randgevallen

| Scenario | Wat te wijzigen | Reden |
|----------|----------------|--------|
| **Andere valuta** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Gebruik het Euro‑symbool of een locale‑specifiek formaat. |
| **Meerdere kolommen met verschillende stijlen** | Maak meerdere `Style`‑objecten, vul `styleArray` in dezelfde volgorde als de kolommen. | Elke kolom kan zijn eigen getalopmaak, lettertype, achtergrond, enz. hebben. |
| **Grote datasets** | Gebruik `cells.importDataTable(dataTable, false, "A1", importOptions);` en stel `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` in | Verbetert de prestaties door header‑rijen of onnodige metadata over te slaan. |
| **Stijl toepassen na import** | Roep `cells.get("A2").setStyle(currencyStyle);` aan voor individuele cellen. | Handig wanneer alleen een subset van rijen speciale opmaak nodig heeft. |

## Tips voor productiegebruik

- **Licentie vroegtijdig**: Registreer je Aspose.Cells‑licentie voordat je de werkmap maakt om het evaluatiewatermerk te vermijden.  
- **Thread‑veiligheid**: `Workbook`‑instanties zijn **niet** thread‑safe. Maak een aparte instantie per thread als je veel bestanden gelijktijdig genereert.  
- **Geheugenbeheer**: Voor zeer grote bladen, overweeg het streaming‑API van `Workbook` (`Workbook` → `WorkbookDesigner`) om het geheugenverbruik laag te houden.  
- **Testen**: Voeg een unit‑test toe die het opgeslagen bestand opent met Apache POI en controleert of de celstijl‑nummeropmaak overeenkomt met `"$#,##0.00"`.

## Conclusie

Je weet nu hoe je **een Excel-werkmap** in Java **valutavormaat** kunt instellen, **vet lettertype** kunt toevoegen, en correct **how to import style** kunt toepassen met Aspose.Cells’ `ImportTableOptions`. Deze end‑to‑end‑oplossing elimineert handmatige Excel‑stappen en garandeert dat elke geïmporteerde cel dezelfde **format cells currency**‑opmaak volgt.

Klaar voor de volgende uitdaging? Probeer voorwaardelijke opmaak toe te voegen, grafieken in te sluiten, of de werkmap naar PDF te exporteren — allemaal met dezelfde stijl‑array‑techniek. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Een Excel-werkmap maken met Aspose.Cells in Java: Een stapsgewijze handleiding](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Hoe Excel‑cellen maken & opmaken met Aspose.Cells voor Java: Een stapsgewijze handleiding](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Hoe Excel‑cellen stijlen en hyperlinks toevoegen met Aspose.Cells voor Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}