---
category: general
date: 2026-11-25
description: Leer hoe je een Excel‑werkmap maakt, een cel algemeen formatteert, een
  stijl op een Excel‑cel toepast en de werkmap opslaat als XLSX met Java en Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: nl
lastmod: 2026-11-25
og_description: Maak een Excel-werkmap in Java, formatteer de cel als algemeen, pas
  een stijl toe op de Excel-cel en sla de werkmap op als XLSX terwijl je Japanse jaartellingdata
  verwerkt.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Maak Excel-werkboek met Japanse jaartelling – stapsgewijze Java‑gids
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Hoe maak je een Excel-werkmap met Japanse jaartelling datums in Java
url: /nl/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑werkmap te maken met Japanse era‑datums in Java

Als je een **Excel‑werkmap** moet **maken** die Japanse era‑datums opslaat, laat deze gids je de exacte stappen zien. Je ziet hoe je de cel formatteert als Algemeen, een stijl toepast op de Excel‑cel, en uiteindelijk de **werkmap opslaat als XLSX** zodat de datum correct wordt geïnterpreteerd.

Werken met Japanse era‑strings (zoals “R3‑04‑01”) kan lastig zijn omdat Excel een echte `DateTime`‑waarde verwacht, niet alleen tekst. Aan het einde van deze tutorial heb je een volledig functioneel `.xlsx`‑bestand dat de juiste gregoriaanse datum weergeeft terwijl de oorspronkelijke era‑notatie behouden blijft.

## Prerequisites

- Java 17 of hoger (de code compileert ook met eerdere versies)
- Aspose.Cells for Java‑bibliotheek (`aspose-cells-xx.x.jar`) – de bibliotheek is gratis voor evaluatie en volledig uitgerust voor productie
- Basiskennis van Java en Maven/Gradle (of de mogelijkheid om een JAR aan je classpath toe te voegen)
- Een IDE zoals IntelliJ IDEA, Eclipse of VS Code (elke werkt)

## Step 1 – Create an Excel workbook

De eerste handeling is het instantieren van een nieuw workbook‑object. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen en geeft je toegang tot werkbladen, cellen en stijlen.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Waarom dit belangrijk is:**  
Het programmatically maken van de werkmap elimineert de noodzaak van een sjabloonbestand en garandeert dat het resulterende bestand in een schone staat begint. De `Workbook`‑constructor maakt automatisch een standaardblad aan, dat we ophalen voor verdere manipulatie.

## Step 2 – Format the cell as General

Excel slaat getallen op met verschillende opmaakstijlen. Voor een datum die we later uit een Japanse era‑string zullen converteren, stellen we eerst het getalformaat van de cel in op *Algemeen* zodat Excel de tekst niet voortijdig probeert te interpreteren.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Waarom dit belangrijk is:**  
Het **format cell general** instellen voorkomt dat Excel de era‑string automatisch formatteert als tekst met een aangepast formaat, wat later de conversie naar een echte `DateTime` zou blokkeren. De aanroep `setNumber(0)` is het Aspose.Cells‑equivalent van Excel’s “General”‑formaat.

## Step 3 – Apply style to the Excel cell

Hoewel het primaire doel is om een datum op te slaan, wil je misschien dat de cel er consistent uitziet met de rest van het blad—bijvoorbeeld een dunne rand of een specifiek lettertype. Het toepassen van een stijl laat ook zien hoe je de esthetiek van een cel programmatically kunt manipuleren.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Waarom dit belangrijk is:**  
De stap **apply style excel cell** toont hoe je de visuele presentatie kunt verrijken zonder de onderliggende data te beïnvloeden. Randen en achtergrondkleuren worden opgeslagen als onderdeel van het stijl‑object van de cel, waardoor de uiteindelijke werkmap er gepolijst uitziet wanneer deze in Excel wordt geopend.

## Step 4 – Convert the Japanese era string to a DateTime object

Nu vervangen we de ruwe tekst door een juiste `DateTime`‑waarde. Aspose.Cells kan een string parseren met een specifieke `CultureInfo`. Door de Japanse cultuur (`ja-JP`) door te geven, interpreteert de bibliotheek “R3‑04‑01” correct als het 3e jaar van het Reiwa‑era, wat overeenkomt met 2021‑04‑01 in de gregoriaanse kalender.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Waarom dit belangrijk is:**  
Zonder het specificeren van de cultuur zou “R3‑04‑01” als platte tekst worden behandeld, waardoor de datumsemantiek verloren gaat. Het `CultureInfo`‑object vertelt Aspose.Cells om het Japanse kalendersysteem te gebruiken, waardoor de era‑conversie automatisch wordt afgehandeld. De resulterende cel bevat nu een echte Excel‑datum, waardoor sorteren, filteren en datumrekenkunde mogelijk zijn.

## Step 5 – Save the workbook as XLSX

Tot slot schrijven we de in‑memory werkmap naar een fysiek bestand. Het gebruik van het `.xlsx`‑formaat garandeert compatibiliteit met moderne versies van Excel, Google Sheets en andere spreadsheet‑tools.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Waarom dit belangrijk is:**  
De **save workbook xlsx**‑operatie finaliseert alle wijzigingen. Aspose.Cells schrijft de werkmap in het Open XML‑formaat, waarbij zowel de data als de eerder toegepaste styling behouden blijven. Het resulterende bestand kan direct in Excel worden geopend, waar de cel `2021‑04‑01` (de gregoriaanse equivalent) weergeeft, maar de oorspronkelijke era‑string kan nog steeds worden teruggehaald via Excel’s “Format Cells → Number → Custom” indien nodig.

## Expected output

Wanneer je `JapaneseEra.xlsx` opent in Microsoft Excel:

- Cel **A1** toont de datum `2021‑04‑01` (Excel’s standaard datumformaat).  
- De cel heeft een dunne grijze rand en een lichtgrijze achtergrond, wat bevestigt dat de stap **apply style excel cell** geslaagd is.  
- Als je het celformaat wijzigt naar “Algemeen”, blijft de onderliggende waarde een echte datum, niet de oorspronkelijke string.

De console zal afdrukken:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Common variations and edge cases

| Situation | What to change |
|-----------|----------------|
| **Different era (e.g., Heisei)** | Gebruik het juiste era‑voorvoegsel (`H` voor Heisei) in de invoerstring. Dezelfde `CultureInfo` zal de conversie afhandelen. |
| **Multiple dates** | Loop over een bereik van cellen en pas dezelfde conversielogica op elke cel toe. |
| **Custom date format** | Na `setValue(japaneseDate)`, roep `cellStyle.setNumber(14)` (of een andere Excel‑nummerformaat‑ID) aan om datums weer te geven als `yyyy/MM/dd`. |
| **Large workbooks** | Hergebruik één enkel `Style`‑object voor betere prestaties, of gebruik `StyleFlag` om alleen de benodigde attributen te wijzigen. |
| **Saving to a stream** | Vervang `workbook.save(outputPath, SaveFormat.XLSX)` door `workbook.save(outputStream, SaveFormat.XLSX)` wanneer je het bestand via HTTP verzendt. |

## Tips from the field

- **Pro tip:** Stel altijd het getalformaat van de cel *voordat* je een `DateTime` toewijst. Het later wijzigen van het formaat kan ervoor zorgen dat Excel de verkeerde visuele weergave toont.
- **Watch out for:** Het gebruik van `CultureInfo("ja-JP")` zonder `createSpecificCulture` kan terugvallen op de gregoriaanse kalender, wat leidt tot onjuiste datums.
- **Performance note:** Wanneer je veel gestylede cellen maakt, kloon dan een bestaand `Style`‑object in plaats van `getStyle()` voor elke cel aan te roepen; dit vermindert interne kopieeroverhead.

## Conclusion

In deze tutorial heb je geleerd hoe je een **Excel‑werkmap** in Java **maakt**, **cel als Algemeen formatteert**, **stijl toepast op een Excel‑cel**, en **de werkmap opslaat als XLSX** terwijl je correct omgaat met Japanse era‑datums. De volledige code‑voorbeeld staat klaar om te kopiëren, plakken en uit te voeren, en biedt een betrouwbaar fundament voor elke Excel‑automatisering die niet‑Gregoriaanse kalenders omvat.

Vervolgens kun je verkennen:

- Formules toevoegen die verwijzen naar de geconverteerde datums (bijv. `=YEAR(A1)`).
- De werkmap exporteren naar PDF met `workbook.save("output.pdf", SaveFormat.PDF)`.
- Deze logica integreren in een Spring Boot REST‑endpoint om rapporten on‑demand te genereren.

Voel je vrij om te experimenteren met verschillende culturen, aangepaste getalformaten of bulk‑data‑imports. Veel programmeerplezier!

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel Workbook Initialization & Cell Styling using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}