---
category: general
date: 2026-06-08
description: Hoe reduce te gebruiken in Excel met Java via Aspose.Cells. Leer lambda‑formule
  Excel, dynamische arrays Java, hoe je lambda schrijft, en som met reduce in een
  duidelijke stapsgewijze tutorial.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: nl
og_description: Hoe reduce te gebruiken in Excel met Java. Beheers de lambda‑formule
  in Excel, dynamische arrays in Java en som met reduce met een compleet, uitvoerbaar
  voorbeeld.
og_title: Hoe Reduce in Excel met Java te gebruiken – Lambda Formulegids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Hoe Reduce te gebruiken in Excel met Java – Lambda‑formulegids
url: /nl/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Reduce te gebruiken in Excel met Java – Lambda‑formulegids

Heb je je ooit afgevraagd **how to use reduce** in Excel wanneer je Java‑code schrijft? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan bij het combineren van Excel’s new dynamic array functions met Java‑gebaseerde automatisering, en het antwoord is niet zo cryptisch als het eerst lijkt.

In deze tutorial lopen we een concreet voorbeeld door dat **how to use reduce** laat zien samen met een **lambda formula Excel**‑expressie, allemaal aangedreven door de Aspose.Cells for Java‑bibliotheek. Aan het einde kun je dynamische arrays genereren in Java, lambda‑functies schrijven en een **sum with reduce** berekenen — geen handmatig spreadsheet‑geklungel meer nodig.

---

## Wat je gaat bouwen

- Een nieuw werkboek volledig gecreëerd vanuit Java.  
- Een **EXPAND** dynamic array die de cellen A1:A5 vult met de getallen 1‑5.  
- Een **REDUCE** formule die die getallen optelt met behulp van een **lambda formula Excel**.  
- Een opgeslagen `.xlsx`‑bestand dat je in elk spreadsheet‑programma kunt openen om het resultaat te verifiëren.

Geen externe macro's, geen VBA — alleen pure Java‑code en de moderne functies van Excel.

## Vereisten

- Java 17 (of een recente JDK) – oudere versies werken, maar je mist de `var`‑syntaxis.  
- Aspose.Cells for Java (de gratis proefversie werkt prima voor deze demo).  
- Basiskennis van Java‑syntaxis en Excel‑formules.

Als je nieuw bent met **dynamic arrays java**, maak je geen zorgen — deze gids legt elk onderdeel uit.

## Stap 1: Stel je project in en importeer Aspose.Cells

Allereerst, voeg de Aspose.Cells Maven‑dependency toe aan je `pom.xml` (of haal de JAR handmatig).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** Houd je dependencies up‑to‑date; nieuwere versies verbeteren de snelheid van formule‑evaluatie, wat van belang is wanneer je **how to use reduce** in grote werkbladen.

## Stap 2: Maak een werkboek aan en krijg toegang tot het eerste werkblad

Nu maken we een gloednieuw werkboek aan. Dit is de basis om **how to use reduce** te leren, omdat het workbook‑object ons een sandbox biedt om formules in te plaatsen.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Waarom dit belangrijk is:* De `Workbook`‑klasse abstraheert het volledige Excel‑bestand, terwijl `Worksheet` een enkel tabblad vertegenwoordigt. Later zul je zien hoe **dynamic arrays java** veel cellen kan vullen vanuit één formule die in A1 wordt geplaatst.

## Stap 3: Genereer een verticale array met EXPAND

De `EXPAND`‑functie van Excel kan waarden in een bereik laten uitvloeien. We gebruiken deze om de getallen 1 tot 5 in kolom A te maken.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Als je het resulterende werkboek opent, zullen de cellen A1:A5 1, 2, 3, 4, 5 tonen. Dit is het **dynamic arrays java**‑deel — één formule vult een heel bereik.

## Stap 4: Schrijf een REDUCE‑lambda om de array op te tellen

Hier beantwoorden we de kernvraag: **how to use reduce** in Excel vanuit Java. De `REDUCE`‑functie doorloopt een array en past een lambda toe die je opgeeft. In ons geval zullen we de getallen optellen.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Laten we dat ontleden:

- `0` – de initiële accumulatorwaarde (`acc`).  
- `A1:A5` – de array die we hebben gegenereerd met **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – de **lambda formula Excel** die elk element (`x`) bij de accumulator (`acc`) optelt.  

Wanneer de formule wordt uitgevoerd, bevat `B1` **15**, de **sum with reduce** van de getallen 1‑5.

> **How to write lambda** in Excel? Beschouw het als een anonieme functie waarbij de eerste argumenten de parameters zijn, en de laatste expressie de retourwaarde. In Java voegen we gewoon de tekst in; de Excel‑engine doet het zware werk.

## Stap 5: Sla het werkboek op

Tot slot slaan we het werkboek op schijf zodat je het kunt openen in Excel, Google Sheets, of elke viewer die `.xlsx` ondersteunt.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open het bestand en je zult zien:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

De **sum with reduce** verschijnt in B1, wat bevestigt dat we succesvol hebben aangetoond **how to use reduce** samen met een **lambda formula Excel** vanuit Java.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar Java‑programma. Kopieer‑en‑plak het in je IDE, pas de uitvoermap aan, en klik op **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Verwachte output** wanneer je `new-functions.xlsx` opent:

- Cellen **A1:A5** bevatten `1, 2, 3, 4, 5`.  
- Cel **B1** toont `15`, wat de **sum with reduce** bevestigt.

## Veelgestelde vragen & randgevallen

### Wat als ik een horizontale array nodig heb in plaats van een verticale?

Swap the column/row arguments in `EXPAND`. For a horizontal spill across B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Kan ik REDUCE gebruiken om te vermenigvuldigen in plaats van op te tellen?

Absolutely. Just change the lambda body:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Nu zal B1 `120` tonen (5 ! = 120).

### Ondersteunt Aspose.Cells aangepaste LAMBDA‑functies?

Ja, je kunt benoemde LAMBDA‑functies definiëren via de `Names`‑collectie van het werkboek, en ze vervolgens aanroepen zoals elke ingebouwde formule. Dat is een dieper onderwerp voor een latere tutorial over **how to write lambda**‑functies die verder gaan dan één enkele cel.

### Wat als oudere Excel‑versies REDUCE niet herkennen?

If you target Excel 2019 or earlier, the engine will return `#NAME?`. In such cases

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}