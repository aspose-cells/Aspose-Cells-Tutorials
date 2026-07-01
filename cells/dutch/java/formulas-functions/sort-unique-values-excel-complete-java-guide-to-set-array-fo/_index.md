---
category: general
date: 2026-06-30
description: Sorteer unieke waarden in Excel met Java. Leer hoe je een formule instelt,
  formules opnieuw berekent en een unieke lijst in Excel genereert met Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: nl
og_description: Sorteer unieke waarden in Excel met Java. Deze gids laat zien hoe
  je een formule instelt, formules opnieuw berekent en in enkele minuten een unieke
  lijst in Excel genereert.
og_title: Unieke waarden sorteren in Excel – Java‑tutorial voor arrayformules
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Unieke waarden sorteren in Excel – Complete Java‑gids voor het instellen van
  matrixformules
url: /nl/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Unieke Waarden Sorteren in Excel – Complete Java-gids voor het Instellen van Arrayformules

Heb je je ooit afgevraagd hoe je **unieke waarden sorteren in Excel** zonder formules te slepen? Je bent niet de enige. In veel rapportagescenario's heb je een schone, alfabetisch gesorteerde lijst van unieke items nodig, en dit handmatig doen is een pijn.  

Het goede nieuws? Met een paar regels Java-code kun je **arrayformule instellen** op een werkblad, daarna **formules opnieuw berekenen** zodat het verspreide bereik zichzelf automatisch vult. In deze tutorial lopen we alles door — van het maken van een werkmap tot het genereren van een unieke lijst in Excel‑stijl — zodat je de oplossing direct in je applicatie kunt integreren.

## Wat deze tutorial behandelt

- Een Java-project opzetten met Aspose.Cells (de bibliotheek die de code‑snippet aandrijft).  
- De `SORT`- en `UNIQUE`-functies samen gebruiken om **unieke lijst Excel genereren** resultaten te genereren.  
- Een **arrayformule** programmatically op een cel toepassen.  
- Een berekeningspass uitvoeren zodat de stap **formules opnieuw berekenen** direct gebeurt.  
- De output verifiëren en de oplossing aanpassen voor randgevallen zoals lege cellen of niet‑aaneengesloten bereiken.

Aan het einde van deze gids kun je een kant‑en‑klare methode in elke Java-service plaatsen die schone Excel‑bladen moet exporteren.

> **Pro tip:** Als je al Maven gebruikt, bespaart het toevoegen van Aspose.Cells als afhankelijkheid je het handmatig beheren van JAR‑bestanden.

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Java 8 of nieuwer | Aspose.Cells richt zich op Java 8+. |
| Maven (of Gradle) | Vereenvoudigt het beheer van afhankelijkheden. |
| Aspose.Cells voor Java | Biedt de `Workbook`, `Worksheet` en formule‑API's die we gebruiken. |
| Basiskennis van Excel‑functies | Het begrijpen van `SORT` en `UNIQUE` helpt je de code aan te passen. |

> *Als je Aspose.Cells nog niet hebt, voeg dit toe aan je `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

## Stap 1: Een Nieuwe Werkmap Maken (Hoe een Formule In te Stellen Begint Hier)

Eerst hebben we een lege werkmap nodig. Beschouw het als een leeg canvas waarop we later **arrayformule instellen** op cel `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Waarom een nieuwe werkmap maken?*  
> Het garandeert een schone omgeving, waardoor verborgen formules die onze testgegevens kunnen verstoren, worden vermeden.

## Stap 2: Voorbeeldgegevens Invoeren (Optioneel maar Handig)

Om het resultaat duidelijk te zien, vullen we kolom **B** met enkele dubbele waarden.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Waarom kolom B gebruiken?*  
> De formule die we gaan schrijven verwijst naar `B1:B10`, dus het plaatsen van de gegevens daar weerspiegelt het klassieke Excel‑voorbeeld.

## Stap 3: Een Arrayformule Instellen Die **Unieke Waarden Sorteren in Excel**

Nu gebeurt de magie. We combineren `UNIQUE` (om duplicaten te verwijderen) met `SORT` (om ze alfabetisch te ordenen). De resulterende expressie is een **arrayformule**, wat betekent dat deze automatisch in aangrenzende cellen wordt verspreid.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Hoe Het Werkt

- `UNIQUE(B1:B10)` scant het bereik en retourneert een verticale array van unieke tekenreeksen.  
- `SORT(...)` neemt die array en ordent deze in oplopende volgorde.  
- Door het geheel te omgeven met `=` en `setFormulaArray` aan te roepen, vertelt men Aspose.Cells het resultaat te behandelen als een **verspreide array**, precies zoals Excel dat zou doen.

> **Opmerking:** Als je een oudere versie van Excel gebruikt die `SORT` of `UNIQUE` niet heeft, kun je terugvallen op `SORT(UNIQUE(...))` met de **LET**‑functie of legacy array‑formules gebruiken (`=INDEX(...)`). De tutorial richt zich op de moderne dynamische array‑benadering omdat dit de schoonste manier is om **unieke lijst Excel genereren** vandaag te **genereren**.

## Stap 4: Formules Opnieuw Berekenen Zodat het Verspreide Bereik Wordt Gepopt

Nadat de formule is geplaatst, evalueert de werkmap deze niet automatisch. Hier komt de stap **formules opnieuw berekenen** om de hoek kijken.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Het aanroepen van `calculateFormula()` dwingt Aspose.Cells de Excel‑engine te draaien, waardoor cellen `A1`, `A2`, … worden gevuld met de gesorteerde unieke waarden.

> *Waarom niet vertrouwen op luie evaluatie?*  
> In een server‑side context heb je vaak de gegevens direct na de berekening klaar nodig voor export (CSV, PDF, enz.), dus een expliciete aanroep garandeert consistentie.

## Stap 5: Het Resultaat Verifiëren (Optioneel Debuggen)

Het is altijd een goed idee om de verspreide waarden naar de console te printen — vooral wanneer je jezelf een nieuwe API leert.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Het uitvoeren van het programma print:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Open `SortedUniqueValues.xlsx` en je zult dezelfde gegevens zien die vanaf `A1` naar beneden worden verspreid.

## Randgevallen Afhandelen

### Lege Cellen in het Bronbereik

Als `B1:B10` lege cellen bevat, zal `UNIQUE` ze behandelen als een aparte invoer. Om lege cellen te negeren, wikkel je het bereik met `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Niet‑Aaneengesloten Gegevens

Wanneer je gegevens zich over meerdere kolommen verspreiden, kun je ze combineren met `CHOOSE` of `TEXTJOIN` voordat je `UNIQUE` toepast. Bijvoorbeeld:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Deze aanpassingen tonen de flexibiliteit van **formule instellen** voor complexere scenario's.

## Volledig Werkend Voorbeeld (Alle Stappen Gecombineerd)

Hieronder staat het volledige, uitvoerbare Java‑programma. Kopieer‑en‑plak het in je IDE, voeg de Aspose.Cells‑afhankelijkheid toe, en klik op *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Verwachte output** (weergegeven in de console) komt overeen met de gesorteerde, gededupliceerde lijst die we eerder bespraken. Het openen van het gegenereerde Excel‑bestand toont dezelfde waarden die vanaf `A1` naar beneden worden verspreid.

## Veelgestelde Vragen

**Q: Werkt dit met oudere Excel‑versies (pre‑Office 365)?**  
A: De `SORT`‑ en `UNIQUE`‑functies maken deel uit van de Dynamic‑Array‑engine geïntroduceerd in Excel 365. Voor legacy‑bestanden moet je klassieke array‑formules gebruiken zoals `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells kan ze nog steeds evalueren, maar de syntaxis is uitgebreider.

**Q: Kan ik de arrayformule op een ander bereik dan `A1` instellen?**  
A: Zeker. Verander gewoon het adres in `cells.get("A1")`. De verspreide array begint altijd bij de opgegeven cel en breidt zich naar rechts en beneden uit zoals nodig.

**Q: Wat als mijn brongegevens groter zijn dan `B1:B10`?**  
A: Vervang het statische bereik door een dynamisch bereik, bijvoorbeeld `B:B` of een benoemd bereik. De formule wordt `=SORT(UNIQUE(B:B))`. Wees voorzichtig met kolom‑brede verwijzingen in zeer grote bladen; ze kunnen de prestaties beïnvloeden.

## Conclusie

We hebben zojuist **formule instellen** in Java behandeld om **unieke waarden sorteren in Excel** te doen, hoe **formules opnieuw berekenen**, en hoe **unieke lijst Excel genereren** met de krachtige API van Aspose.Cells. De stappen zijn eenvoudig: een werkmap maken, gegevens invoeren, een arrayformule toepassen, berekening starten en het resultaat verifiëren.  

Vanaf hier kun je uitbreiden — conditionele opmaak toevoegen, exporteren naar PDF, of de methode integreren in een webservice die kant‑en‑klare rapporten levert. Het kernidee blijft hetzelfde: laat de eigen functies van Excel het zware werk doen, en laat Java het proces orkestreren.

Klaar om je Excel‑automatisering naar een hoger niveau te tillen? Probeer `SORT` te vervangen door `SORTBY` om te sorteren op een secundaire kolom, of experimenteer met `FILTER` om rijen uit te sluiten die niet aan de bedrijfsregels voldoen. De mogelijkheden zijn praktisch eindeloos.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}