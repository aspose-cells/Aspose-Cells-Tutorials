---
category: general
date: 2026-07-03
description: Leer hoe je een array in Excel kunt uitbreiden met Java. Deze tutorial
  behandelt het uitbreiden van een array naar rijen, hoe je expand gebruikt, en hoe
  je efficiënt een formule invoegt.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: nl
og_description: Array uitbreiden in Excel met Java. Volg deze gids om te leren hoe
  je expand gebruikt, een formule in een cel instelt en een array direct naar rijen
  uitbreidt.
og_title: Array uitbreiden in Excel met Java – Complete programmeergids
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Array uitbreiden in Excel met Java – Stapsgewijze handleiding
url: /nl/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Array uitbreiden in Excel met Java – Complete Programmeergids

Heb je je ooit afgevraagd hoe je **array in Excel kunt uitbreiden** zonder handmatig cellen te slepen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een dynamisch bereik moeten genereren – vooral nu de nieuwe Excel `EXPAND`‑functie nog vers is. In deze gids laten we je precies zien **hoe je EXPAND gebruikt**, de formule in een werkblad invoegt, en het resultaat laat uitvloeien over de rijen die je wilt. Aan het einde kun je **array naar rijen uitbreiden** met één enkele regel Java‑code.

We lopen een volledig, uitvoerbaar voorbeeld door met de Aspose.Cells for Java‑bibliotheek. Geen vage verwijzingen, alleen concrete code die je kunt kopiëren‑plakken, compileren en uitvoeren. Onderweg bespreken we waarom elke stap belangrijk is, behandelen we randgevallen zoals niet‑aaneengesloten arrays, en strooien we een paar pro‑tips uit die je niet in de officiële documentatie vindt. Klaar? Laten we beginnen.

## Prerequisites

Voordat we starten, zorg dat je het volgende hebt:

* Java 17 (of een recente JDK) geïnstalleerd.
* Maven of Gradle om afhankelijkheden te beheren.
* Een geldige Aspose.Cells for Java‑licentie (de gratis proefversie werkt voor testen).
* Basiskennis van Excel‑formules – als je eerder `VLOOKUP` of `SUMIF` hebt gebruikt, ben je klaar om te gaan.

Als een van deze onderdelen onbekend is, pauzeer dan en stel ze eerst in; de rest van de tutorial gaat ervan uit dat ze klaar zijn.

## Step 1: Set Up Your Maven Project and Add Aspose.Cells

Om alles overzichtelijk te houden, maak een nieuw Maven‑project aan genaamd `ExpandArrayDemo`. Voeg de Aspose.Cells‑dependency toe aan je `pom.xml`:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Als je Gradle gebruikt, ziet dezelfde dependency er als volgt uit: `implementation 'com.aspose:aspose-cells:23.12'`.

Zodra Maven klaar is met downloaden, kun je Java‑code schrijven die **formula in cell instelt**.

## Step 2: Create a Workbook and Access the First Worksheet

Het eerste code‑fragment spiegelt de snippet die je al zag, maar we voegen wat veiligheidscontroles en commentaar toe zodat je het *waarom* achter elke regel begrijpt.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Waarom dit belangrijk is:* Het instantieren van `Workbook` reserveert de interne structuren die Aspose nodig heeft om cellen, formules en stijlen te beheren. Het benaderen van het eerste werkblad is het meest voorkomende startpunt, vooral wanneer je net experimenteert.

## Step 3: Insert the EXPAND Formula – “How to Insert Formula”

Nu volgt het hart van de tutorial: **hoe je formule invoegt** die een array uitbreidt. De Excel‑functie `EXPAND` neemt drie argumenten – bron‑array, gewenste rijen en gewenste kolommen. In ons geval willen we `{1,2,3}` uitbreiden naar **5 rijen** en **1 kolom**.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

Let op: we gebruiken `putFormula` in plaats van `putValue`. Dit vertelt Aspose de string als een echte Excel‑formule te behandelen, niet als platte tekst. De methode `putFormula` parseert de string automatisch en slaat de formuleboom intern op.

### Why Use EXPAND?

`EXPAND` verwijdert de saaie stap van het slepen van de vulgreep. Het werkt ook met dynamische arrays, wat betekent dat als je bron‑array verandert, het uitgevloeide bereik automatisch wordt bijgewerkt. Dit is bijzonder handig bij het programmatisch genereren van rapporten.

## Step 4: Force Calculation – Materializing the Result

Wanneer je *formula in cell instelt* via de API, recalculeren de werkmap en de formule niet automatisch. Je moet een berekeningspass uitvoeren zodat de array **naar rijen wordt uitgebreid** en de waarden in het blad verschijnen.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Als je deze stap overslaat, zie je bij het openen van de gegenereerde `.xlsx` in Excel de formule maar niet de uitgevloeide waarden totdat je **F9** indrukt. Door `calculate()` aan te roepen, zorg je ervoor dat de werkmap direct klaar is voor gebruik.

## Step 5: Save the Workbook and Verify Output

Schrijf tenslotte de werkmap naar een bestand en print eventueel de uitgevloeide waarden naar de console ter verificatie.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Wanneer je het programma uitvoert, zou je de volgende console‑output moeten zien:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel vult de resterende rijen met nullen omdat de bron‑array slechts drie elementen bevatte. Dit is het standaardgedrag van `EXPAND`. Als je liever lege cellen ziet in plaats van nullen, kun je de array omhullen met `IFERROR` of `CHOOSE`‑trucs gebruiken – meer hierover in de sectie “Advanced Variations” hieronder.

## Advanced Variations & Edge Cases

### 1. Expanding a Horizontal Array to Multiple Columns

Als je **array naar rijen** *en* kolommen wilt uitbreiden, wijzig dan simpelweg het derde argument:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Nu stroomt het bereik uit naar een 5 × 3‑blok, waarbij ontbrekende cellen met nullen worden gevuld.

### 2. Using a Named Range as the Source

In plaats van een letterlijke `{1,2,3}` kun je een benoemd bereik refereren dat tijdens runtime kan veranderen:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

Zorg ervoor dat `MySourceRange` bestaat (je kunt het aanmaken via `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")`).

### 3. Handling Non‑Numeric Data

`EXPAND` werkt ook met tekst. Bijvoorbeeld:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

De extra rij verschijnt als een lege tekenreeks, niet als nul.

### 4. Avoiding Zero Fill with `IFERROR`

Als je liever lege cellen ziet in plaats van nullen, omhul dan `EXPAND` met `IFERROR`:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Nu zullen rijen 4 en 5 echt leeg zijn.

## Common Pitfalls and How to Dodge Them

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Formula not recalculated** | Forgetting `ws.getCells().calculate()` | Always call `calculate()` after `putFormula`. |
| **Zero values where blanks expected** | `EXPAND` pads with zeros by default | Use `IFERROR(..., "")` or wrap with `CHOOSE`. |
| **Incorrect cell address** | Using `"A0"` or `"1A"` | Excel addresses start at 1; Aspose expects `"A1"` style. |
| **Library version mismatch** | Using an old Aspose.Cells version that lacks `EXPAND` support | Upgrade to the latest version (23.12 at time of writing). |

## Full Working Example (All Steps Combined)

Hieronder vind je het complete, copy‑paste‑klare programma. Sla het op als `ExpandArrayDemo.java`, compileer en voer uit.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Het uitvoeren van dit programma produceert een Excel‑bestand waarin **cel A1** nu de `EXPAND`‑formule bevat, en rijen 1‑5 van kolom A tonen `1, 2, 3, 0, 0`. Open het bestand in Excel om hetzelfde resultaat direct te zien – geen handmatig slepen nodig.

## Conclusion

Je hebt zojuist geleerd hoe je **array in Excel kunt uitbreiden** met Java, **hoe je EXPAND gebruikt**, en de exacte stappen om **formula in cell in te stellen** en **array naar rijen uit te breiden** programmatically. Door Aspose.Cells te gebruiken, vermijd je de onhandige UI‑trucs en laat je de code het zware werk doen. Of je nu een rapportage‑engine bouwt, een geautomatiseerde data‑invoertool, of een aangepaste spreadsheet‑generator, deze techniek bespaart je talloze uren.

Wat nu? Probeer de statische array te vervangen door een dynamisch bereik dat uit een ander blad wordt gehaald, experimenteer met multi‑kolom‑spills, of combineer `EXPAND` met `FILTER` voor krachtige datatransformaties. De mogelijkheden zijn eindeloos, en nu heb je een solide basis om op voort te bouwen.

Heb je vragen of wil je een cool use‑case delen? Laat een reactie achter.


## What Should You Learn Next?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}