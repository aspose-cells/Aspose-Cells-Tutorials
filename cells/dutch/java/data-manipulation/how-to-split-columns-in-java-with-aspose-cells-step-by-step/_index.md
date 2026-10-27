---
category: general
date: 2026-10-07
description: Hoe kolommen splitsen met Aspose.Cells voor Java. Leer een tekenreeks
  in kolommen te splitsen, Excel‑formules te automatiseren en een formule naar een
  cel te schrijven in een paar regels code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: nl
lastmod: 2026-10-07
og_description: Hoe kolommen splitsen in Java met Aspose.Cells. Deze tutorial laat
  zien hoe je een tekenreeks in kolommen splitst, de evaluatie van Excel‑formules
  automatiseert en een formule naar een cel schrijft.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Hoe kolommen splitsen in Java met Aspose.Cells – snelle tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe kolommen splitsen in Java met Aspose.Cells – stapsgewijze handleiding
url: /nl/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe kolommen splitsen in Java met Aspose.Cells – stapsgewijze handleiding

Als je **kolommen wilt splitsen** in een Excel-werkblad programmatically, laat deze gids je het volledige proces zien met Aspose.Cells voor Java. Je leert ook hoe je **string in kolommen splitst**, **Excel-formule** automatisch laat evalueren, en **een formule naar een cel schrijft** met beknopte, productieklare code.

Programma‑matig kolommen splitsen elimineert handmatig kopiëren‑plakken, vermindert fouten, en maakt grootschalige datatransformaties mogelijk. Aan het einde van deze tutorial kun je formules genereren, wijzigen en evalueren on‑the‑fly, waardoor Excel een echt onderdeel van je Java‑backend wordt.

## Vereisten

* Java 17 of later geïnstalleerd.
* Maven 3.8+ (of Gradle) voor afhankelijkheidsbeheer.
* Een Aspose.Cells voor Java‑licentie (de gratis evaluatieversie werkt voor leren).
* Basiskennis van Java‑syntaxis en Excel‑concepten.

Als een van deze items ontbreekt, installeer ze dan eerst; de code‑voorbeelden gaan uit van een standaard Maven‑project.

## Stap 1: Voeg Aspose.Cells toe aan je project

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Waarom deze stap belangrijk is:** De bibliotheek levert de `Workbook`, `Worksheet` en `Cell` klassen die nodig zijn om Excel‑bestanden te manipuleren zonder Microsoft Office. Zonder de afhankelijkheid compileert de code niet.

## Stap 2: Maak een werkmap en selecteer het eerste werkblad

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Het `Workbook`‑object vertegenwoordigt het volledige Excel‑bestand. Het benaderen van het eerste werkblad zorgt voor een voorspelbaar startpunt voor de formule die we gaan schrijven.

## Stap 3: Schrijf de WRAPCOLS‑formule naar een doelcel

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Waarom we `WRAPCOLS` gebruiken:** De ingebouwde Excel‑functie `WRAPCOLS` splitst automatisch een enkele tekstwaarde over een gedefinieerd aantal kolommen, waarbij woordgrenzen intelligent worden behandeld. Dit is de meest betrouwbare manier om **string in kolommen te splitsen** zonder aangepaste parse‑logica.

## Stap 4: Forceer de werkmap om de formule te evalueren

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Het aanroepen van `calculateFormula()` **automatiseert de evaluatie van Excel‑formules** aan de serverzijde. Zonder deze oproep zou de cel nog steeds de formule‑tekst bevatten, niet de berekende waarden.

## Stap 5: Haal het ingepakte resultaat op en toon het

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Wanneer je het programma uitvoert, print de console:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Het gegenereerde bestand `SplitColumnsResult.xlsx` toont de drie kolommen gevuld met de gesplitste tekst.

## Begrijpen van de WRAPCOLS‑functie

* **Syntax:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameters:**
  * `text` – de string die je wilt splitsen.
  * `columns` – het aantal kolommen waarin de tekst moet worden verdeeld.
  * `delimiter` (optioneel) – teken dat wordt gebruikt om de string te splitsen; standaard is een spatie.
* **Return value:** Een array die zich uitstrekt over aangrenzende cellen, elk element bevat een deel van de oorspronkelijke tekst.

Omdat de functie horizontaal uitstrekt, hoef je de formule alleen naar de meest linkse cel (A1 in het voorbeeld) te schrijven. Excel vult automatisch B1, C1, … naar behoefte.

## Veelvoorkomende variaties en randgevallen

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Variabele kolomtelling** | Vervang de hard‑coded `3` door een variabele: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Aangepaste scheidingsteken** | Gebruik het derde argument, bv. `=WRAPCOLS(A2,4,",")` om te splitsen op komma's. |
| **Lege bronstring** | De functie retourneert lege cellen; controleer op `null` of lege strings voordat je de formule instelt. |
| **Grote datasets** | Pas de formule toe in een lus voor elke rij, en roep daarna één keer `calculateFormula()` aan na de lus om de prestaties te verbeteren. |
| **Niet‑ASCII tekens** | WRAPCOLS werkt met Unicode; zorg ervoor dat je Java‑bronbestand is opgeslagen als UTF‑8. |

**Pro tip:** Wanneer je veel rijen verwerkt, sla de formule op in een string‑variabele en hergebruik deze om herhaalde string‑concatenatie‑overhead te vermijden.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma klaar om te kopiëren en plakken. Het bevat import‑statements, foutafhandeling en een optionele opslaan‑operatie.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Het uitvoeren van dit programma levert dezelfde console‑output op als eerder getoond en schrijft een Excel‑bestand dat duidelijk laat zien **hoe kolommen te splitsen**.

## Checklist voor probleemoplossing

* **Formule wordt niet geëvalueerd** – Zorg ervoor dat `workbook.calculateFormula()` wordt aangeroepen na het instellen van de formule.
* **Lege cellen na splitsen** – Controleer of de bronstring niet `null` of leeg is, en of het aantal kolommen groter is dan nul.
* **Licentie‑exception** – Lever een geldig Aspose.Cells‑licentiebestand (`License license = new License(); license.setLicense("Aspose.Total.lic");`) voordat je de werkmap maakt om evaluatiewatermerken te verwijderen.
* **Prestatie‑vertraging bij grote bladen** – Roep `calculateFormula()` één keer aan nadat alle formules zijn geschreven, niet na elke individuele cel.

## Conclusie

Je weet nu **hoe kolommen te splitsen** in Java met Aspose.Cells, hoe je **string in kolommen splitst** met de `WRAPCOLS`‑functie, hoe je **Excel‑formules** automatisch laat evalueren, en hoe je **een formule naar een cel schrijft** programmatically. Deze techniek verwijdert handmatige datavoorbereidingsstappen en integreert de krachtige tekst‑verwerkingsmogelijkheden van Excel direct in je Java‑applicaties.

### Volgende stappen

* Verken andere tekstfuncties zoals `TEXTSPLIT` en `FILTERXML` voor complexere parse‑scenario's.
* Combineer `WRAPCOLS` met `IFERROR` om onverwachte invoer elegant af te handelen.
* Integreer de oplossing in een Spring Boot‑service die CSV‑gegevens via REST ontvangt en een ingevuld Excel‑bestand retourneert.

Door deze patronen onder de knie te krijgen kun je robuuste, geautomatiseerde Excel‑workflows bouwen die meegroeien met de behoeften van je bedrijf. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [aspose cells java – Namen splitsen in kolommen](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}