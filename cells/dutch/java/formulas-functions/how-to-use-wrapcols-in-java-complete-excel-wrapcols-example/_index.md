---
category: general
date: 2026-06-21
description: Hoe WRAPCOLS te gebruiken met Aspose.Cells Java om een array naar rijen
  te converteren, een formule in een cel te schrijven en cellen met de formule te
  vullen – stap‑voor‑stap gids.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: nl
og_description: Hoe je WRAPCOLS in Java met Aspose.Cells gebruikt om een array om
  te zetten in rijen, een formule naar een cel te schrijven en cellen met een formule
  te vullen — allemaal in één gids.
og_title: Hoe WRAPCOLS te gebruiken in Java – Volledig Excel WRAPCOLS-voorbeeld
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Hoe WRAPCOLS te gebruiken in Java – Volledig Excel WRAPCOLS‑voorbeeld
url: /nl/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe WRAPCOLS te gebruiken in Java – Volledig Excel WRAPCOLS voorbeeld

Heb je je ooit afgevraagd **hoe je WRAPCOLS** moet gebruiken wanneer je een eenvoudige array moet omzetten in een nette tabel in Excel? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze de `WRAPCOLS`‑functie voor het eerst zien en denken: “Hoe schrijf ik die formule eigenlijk naar een cel vanuit Java?” Het goede nieuws? Het is vrij eenvoudig zodra je de juiste stappen kent.

In deze tutorial lopen we een volledig uitvoerbaar Aspose.Cells Java‑voorbeeld door dat **een array naar rijen converteert**, de formule direct in een cel schrijft, en je laat zien hoe je **cellen kunt vullen met een formule** voor real‑world scenario’s. Aan het einde heb je een duidelijk beeld van het **excel wrapcols voorbeeld** en ben je klaar om het aan je eigen projecten aan te passen.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- Java 17 of hoger (de code werkt met elke recente JDK).
- Aspose.Cells for Java‑bibliotheek (je kunt de nieuwste JAR van Maven Central halen).
- Een basisbegrip van Java‑syntaxis en Excel‑formules.
- Een IDE of eenvoudige teksteditor – geen speciale tooling vereist.

Alles klaar? Geweldig, laten we beginnen.

## Stap 1: Het project opzetten en een werkmap laden

Allereerst – maak een nieuw Maven (of Gradle) project en voeg de Aspose.Cells‑dependency toe:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Nu kunnen we een bestaande werkmap laden (of een nieuwe maken) en het eerste werkblad pakken:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Waarom we een werkmap laden** – Aspose.Cells werkt met een in‑memory representatie van een Excel‑bestand. Door een werkmap te laden (of te maken) krijgen we toegang tot cellen, rijen en formules, wat essentieel is voor elke **write formula to cell**‑operatie.

## Stap 2: De WRAPCOLS‑formule in een cel invoegen

Het hart van de tutorial is de `WRAPCOLS`‑functie. Deze neemt een één‑dimensionale array en “wrapt” deze naar een opgegeven aantal kolommen, waarbij de rest automatisch in nieuwe rijen wordt geplaatst. Hier is de syntaxis die we gaan gebruiken:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Merk op dat de formule een gewone string is die wordt doorgegeven aan `setFormula`. Aspose.Cells doet het zware werk – het parseren van de formule, het evalueren ervan, en het verspreiden van de resultaten naar het werkblad. Dit is de meest directe manier om **populate cells with formula** uit te voeren zonder handmatig over rijen en kolommen te itereren.

### Wat de formule doet

- `{1,2,3}` – een letterlijke array met drie getallen.
- `2` – het aantal kolommen per rij.
- Resultaat:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (leeg)

Als je drie kolommen wilt, wijzig je simpelweg het tweede argument naar `3`, en de array vult één enkele rij.

## Stap 3: De werkmap opslaan en de output verifiëren

Nu de formule in **A1** staat, laten we de werkmap naar schijf schrijven zodat je deze in Excel kunt openen en de spill kunt zien:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Open `output.xlsx` en je ziet precies wat de opmerking beschreef – twee kolommen in de eerste rij en de resterende waarde in de tweede rij. Dat is de essentie van het **excel wrapcols voorbeeld**.

## Stap 4: Het voorbeeld uitbreiden – Grotere arrays converteren

Echte projecten werken zelden met slechts drie getallen. Stel dat je een grotere collectie hebt, bijvoorbeeld `{10,20,30,40,50,60,70}` en je wilt drie kolommen per rij. Zo pas je de code aan:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Nu begint de spill bij **C5**, met als resultaat:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Dit laat zien hoe je **convert array to rows** dynamisch kunt uitvoeren, simpelweg door de formule‑string aan te passen. Geen loops, geen handmatige cel‑toewijzingen – Aspose.Cells regelt de rest.

## Stap 5: Randgevallen en veelvoorkomende valkuilen behandelen

### 1. Lege arrays

Als de array‑literal leeg is (`{}`), geeft `WRAPCOLS` een `#VALUE!`‑fout terug. Om te voorkomen dat je blad breekt, bescherm je de formule‑generatie:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Niet‑numerieke data

`WRAPCOLS` werkt ook met tekst. Bijvoorbeeld, `WRAPCOLS({"A","B","C","D"},2)` produceert een twee‑koloms lay‑out van strings. Vergeet niet strings binnen de array‑literal te omringen met aanhalingstekens.

### 3. Compatibiliteit

De `WRAPCOLS`‑functie is beschikbaar in Excel 365 en Excel 2019+ (Office 2019, Excel voor het web). Als je oudere versies moet ondersteunen, moet je terugvallen op handmatige loops of een andere spill‑compatibele functie gebruiken.

## Stap 6: Praktische tips en pro‑trucs

- **Pro tip:** Gebruik `Cell.setFormulaLocal` als je een locale‑specifieke scheidingsteken (komma vs puntkomma) nodig hebt, afhankelijk van de regionale instellingen van de gebruiker.
- **Let op:** Het overschrijven van bestaande data. Het spill‑gebied zal elke inhoud die al bestaat in het doelbereik vervangen.
- **Prestatienota:** Een formule instellen is goedkoop; het zware werk gebeurt wanneer je **save** of **recalculate** de werkmap uitvoert. Als je duizenden formules genereert, overweeg dan om automatische berekening uit te schakelen (`wb.calculateFormula()` later) om de verwerking te versnellen.

## Volledig werkend voorbeeld

Hieronder staat de complete, kant‑klaar‑te‑runnen Java‑klasse die alles bevat wat we hebben besproken:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Verwachte output:** Open `output.xlsx` en je ziet drie afzonderlijke spill‑regio’s:

- **A1:B2** – getallen 1‑3 gewrapt in twee kolommen.
- **C5:E7** – getallen 10‑70 gewrapt in drie kolommen.
- **G1:H2** – fruitnamen gewrapt in twee kolommen.

## Conclusie

We hebben net behandeld **hoe je WRAPCOLS** gebruikt met Aspose.Cells voor Java, en laten zien hoe je **convert array to rows**, **write formula to cell**, en **populate cells with formula** op een nette, herhaalbare manier kunt uitvoeren. De aanpak elimineert omslachtige loops, maakt gebruik van Excel’s native spill‑gedrag, en houdt je code beknopt.

Klaar voor de volgende uitdaging? Probeer `WRAPCOLS` te combineren met dynamische gegevensbronnen – misschien waarden uit een database halen, de array‑string on‑the‑fly bouwen, en Excel het layout‑werk laten doen. Je kunt ook experimenteren met andere spill‑functies zoals `SEQUENCE` of `FILTER` om nog rijkere rapporten te bouwen.

Als je ergens vastloopt, laat dan een reactie achter of bekijk de uitgebreide documentatie van Aspose. Veel plezier met coderen, en geniet van de kracht van moderne Excel‑formules direct vanuit Java! 

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}