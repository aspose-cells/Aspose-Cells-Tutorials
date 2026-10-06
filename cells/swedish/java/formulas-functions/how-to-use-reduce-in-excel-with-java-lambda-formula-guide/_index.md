---
category: general
date: 2026-06-08
description: Hur man använder reduce i Excel med Java med Aspose.Cells. Lär dig lambda‑formel
  i Excel, dynamiska arrayer i Java, hur man skriver lambda och summerar med reduce
  i en tydlig steg‑för‑steg‑handledning.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: sv
og_description: Hur man använder reduce i Excel med Java. Behärska lambda‑formler
  i Excel, dynamiska arrayer i Java och summera med reduce med ett komplett, körbart
  exempel.
og_title: Hur du använder Reduce i Excel med Java – Lambda‑formelguide
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
title: Hur man använder Reduce i Excel med Java – Lambda‑formelguide
url: /sv/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Reduce i Excel med Java – Lambda‑formelguide

Har du någonsin undrat **how to use reduce** i Excel när du skriver Java‑kod? Du är inte ensam. Många utvecklare stöter på problem när de försöker kombinera Excels nya dynamiska array‑funktioner med Java‑baserad automatisering, och svaret är inte så kryptiskt som det först verkar.

I den här handledningen går vi igenom ett konkret exempel som visar **how to use reduce** tillsammans med ett **lambda formula Excel**‑uttryck, allt drivet av Aspose.Cells for Java‑biblioteket. I slutet kommer du att kunna generera dynamiska arrayer i Java, skriva lambda‑funktioner och beräkna en **sum with reduce**—utan manuellt arbete i kalkylbladet.

---

## Vad du kommer att bygga

- En ny arbetsbok skapad helt från Java.  
- En **EXPAND** dynamisk array som fyller cellerna A1:A5 med siffrorna 1‑5.  
- En **REDUCE**‑formel som summerar dessa siffror med en **lambda formula Excel**.  
- En sparad `.xlsx`‑fil som du kan öppna i vilket kalkylprogram som helst för att verifiera resultatet.

Inga externa makron, ingen VBA—bara ren Java‑kod och Excels moderna funktioner.

## Förutsättningar

- Java 17 (eller någon nyare JDK) – äldre versioner fungerar men du missar `var`‑syntaxen.  
- Aspose.Cells for Java (gratis provversion fungerar bra för denna demo).  
- Grundläggande kunskap om Java‑syntax och Excel‑formler.  

Om du är ny på **dynamic arrays java**, oroa dig inte—denna guide förklarar varje del.

## Steg 1: Ställ in ditt projekt och importera Aspose.Cells

Först och främst, lägg till Aspose.Cells Maven‑beroendet i din `pom.xml` (eller hämta JAR‑filen manuellt).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** Håll dina beroenden uppdaterade; nyare versioner förbättrar hastigheten för formelutvärdering, vilket är viktigt när du **how to use reduce** i stora blad.

## Steg 2: Skapa en arbetsbok och få åtkomst till det första kalkylbladet

Nu skapar vi en helt ny arbetsbok. Detta är grunden för att lära sig **how to use reduce** eftersom arbetsboksobjektet ger oss en sandlåda att placera formler i.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Varför detta är viktigt:* `Workbook`‑klassen abstraherar hela Excel‑filen, medan `Worksheet` representerar en enskild flik. Du kommer senare att se hur **dynamic arrays java** kan fylla många celler från en enda formel placerad i A1.

## Steg 3: Generera en vertikal array med EXPAND

Excels `EXPAND`‑funktion kan spilla värden i ett område. Vi använder den för att skapa siffrorna 1 till 5 i kolumn A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Om du öppnar den resulterande arbetsboken kommer cellerna A1:A5 att visa 1, 2, 3, 4, 5. Detta är **dynamic arrays java**‑delen—en formel fyller ett helt område.

## Steg 4: Skriv en REDUCE‑lambda för att summera arrayen

Här svarar vi på huvudfrågan: **how to use reduce** i Excel från Java. `REDUCE`‑funktionen itererar över en array och applicerar en lambda du anger. I vårt fall kommer vi att summera siffrorna.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Låt oss bryta ner det:

- `0` – det initiala ackumulatorvärdet (`acc`).  
- `A1:A5` – arrayen vi genererade med **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel** som lägger till varje element (`x`) till ackumulatorn (`acc`).  

När formeln körs kommer `B1` att innehålla **15**, **sum with reduce** av siffrorna 1‑5.

> **How to write lambda** i Excel? Tänk på det som en anonym funktion där de första argumenten är parametrarna, och det sista uttrycket är returvärdet. I Java bäddar vi bara in texten; Excel‑motorn gör det tunga arbetet.

## Steg 5: Spara arbetsboken

Till sist sparar vi arbetsboken till disk så att du kan öppna den i Excel, Google Sheets eller någon annan visare som stödjer `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Öppna filen så ser du:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**sum with reduce** visas i B1, vilket bekräftar att vi framgångsrikt har demonstrerat **how to use reduce** tillsammans med en **lambda formula Excel** från Java.

## Fullt fungerande exempel

Nedan är det kompletta, klar‑för‑körning Java‑programmet. Kopiera‑klistra in det i din IDE, justera utskriftskatalogen och tryck på **Run**.

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

**Förväntad output** när du öppnar `new-functions.xlsx`:

- Cellerna **A1:A5** innehåller `1, 2, 3, 4, 5`.  
- Cellen **B1** visar `15`, vilket bekräftar **sum with reduce**.

## Vanliga frågor & kantfall

### Vad händer om jag behöver en horisontell array istället för en vertikal?

Byt kolumn-/rad‑argumenten i `EXPAND`. För en horisontell spill över B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Kan jag använda REDUCE för att multiplicera istället för att summera?

Absolut. Ändra bara lambda‑kroppen:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Nu kommer B1 att visa `120` (5 ! = 120).

Stöder Aspose.Cells anpassade LAMBDA‑funktioner?

Ja, du kan definiera namngivna LAMBDA‑funktioner via arbetsbokens `Names`‑samling och sedan anropa dem som vilken inbyggd formel som helst. Det är ett djupare ämne för en senare handledning om **how to write lambda**‑funktioner som lever längre än en enda cell.

Vad händer med äldre Excel‑versioner som inte känner igen REDUCE?

Om du riktar dig mot Excel 2019 eller tidigare kommer motorn att returnera `#NAME?`. I sådana fall

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Mästra Aspose.Cells Java: Hur man avbryter formelberäkning i Excel‑arbetsböcker](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Hur man konverterar Excel‑cellnamn till index med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Hur man skapar och formaterar Excel‑celler med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}