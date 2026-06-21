---
category: general
date: 2026-06-21
description: Hur man använder WRAPCOLS med Aspose.Cells Java för att konvertera en
  array till rader, skriva formel till cell och fylla celler med formeln – steg‑för‑steg‑guide.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: sv
og_description: Hur man använder WRAPCOLS i Java med Aspose.Cells för att konvertera
  en array till rader, skriva en formel till en cell och fylla celler med formel –
  allt i en guide.
og_title: Hur du använder WRAPCOLS i Java – Fullt Excel WRAPCOLS‑exempel
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
title: Hur man använder WRAPCOLS i Java – Komplett Excel WRAPCOLS‑exempel
url: /sv/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS i Java – Komplett Excel WRAPCOLS‑exempel

Har du någonsin funderat **hur man använder WRAPCOLS** när du behöver omvandla en enkel array till en prydlig tabell i Excel? Du är inte ensam. Många utvecklare fastnar när de första gången ser funktionen `WRAPCOLS` och tänker: “Hur skriver jag egentligen den här formeln till en cell från Java?” Den goda nyheten? Det är ganska enkelt när du känner till rätt steg.

I den här handledningen går vi igenom ett fullt körbart Aspose.Cells‑Java‑exempel som **omvandlar en array till rader**, skriver formeln direkt i en cell och visar hur du **fyller celler med formel** för verkliga scenarier. När du är klar har du en klar bild av **excel wrapcols‑exemplet** och är redo att anpassa det till dina egna projekt.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- Java 17 eller senare (koden fungerar med vilken modern JDK som helst).
- Aspose.Cells för Java‑biblioteket (du kan hämta den senaste JAR‑filen från Maven Central).
- Grundläggande förståelse för Java‑syntax och Excel‑formler.
- En IDE eller en enkel textredigerare – inga speciella verktyg krävs.

Allt på plats? Bra, låt oss börja.

## Steg 1: Ställ in projektet och läs in en arbetsbok

Det första steget – skapa ett nytt Maven‑ (eller Gradle‑) projekt och lägg till Aspose.Cells‑beroendet:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Nu kan vi läsa in en befintlig arbetsbok (eller skapa en ny) och hämta det första kalkylbladet:

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

> **Varför vi läser in en arbetsbok** – Aspose.Cells arbetar med en minnesrepresentation av en Excel‑fil. Genom att läsa in (eller skapa) en arbetsbok får vi åtkomst till celler, rader och formler, vilket är avgörande för alla **write formula to cell**‑operationer.

## Steg 2: Infoga WRAPCOLS‑formeln i en cell

Kärnan i handledningen är `WRAPCOLS`‑funktionen. Den tar en endimensionell array och “wrappar” den till ett angivet antal kolumner, och låter automatiskt resten spilla över till nya rader. Så här ser syntaxen ut:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Observera hur formeln är en vanlig sträng som skickas till `setFormula`. Aspose.Cells gör det tunga arbetet – parsar formeln, utvärderar den och spillar resultatet i kalkylbladet. Detta är det mest direkta sättet att **populate cells with formula** utan att manuellt iterera över rader och kolumner.

### Vad formeln gör

- `{1,2,3}` – en litteral array som innehåller tre tal.
- `2` – antalet kolumner per rad.
- Resultat:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (tom)

Om du ville ha tre kolumner istället, ändra helt enkelt det andra argumentet till `3`, så fyller arrayen en enda rad.

## Steg 3: Spara arbetsboken och verifiera resultatet

Nu när formeln sitter i **A1**, låt oss spara arbetsboken till disk så att du kan öppna den i Excel och se spillage‑resultatet:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Öppna `output.xlsx` så kommer du att se exakt det som kommentaren beskrev – två kolumner i den första raden och det återstående värdet i den andra raden. Det är kärnan i **excel wrapcols‑exemplet**.

## Steg 4: Utöka exemplet – konvertera större arrayer

Verkliga projekt arbetar sällan bara med tre tal. Föreställ dig att du har en större samling, t.ex. `{10,20,30,40,50,60,70}` och du vill ha tre kolumner per rad. Så här justerar du koden:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Nu startar spillage i **C5**, vilket ger:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Detta visar hur du kan **convert array to rows** dynamiskt, bara genom att ändra formelsträngen. Inga loopar, inga manuella celltilldelningar – Aspose.Cells sköter resten.

## Steg 5: Hantera kantfall och vanliga fallgropar

### 1. Tomma arrayer

Om array‑litteralen är tom (`{}`) returnerar `WRAPCOLS` ett `#VALUE!`‑fel. För att undvika att ditt blad går sönder, skydda formelgenereringen:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Icke‑numerisk data

`WRAPCOLS` fungerar även med text. Till exempel, `WRAPCOLS({"A","B","C","D"},2)` ger en två‑kolumnslayout av strängar. Kom bara ihåg att citera strängar inom array‑litteralen.

### 3. Kompatibilitet

`WRAPCOLS`‑funktionen finns i Excel 365 och Excel 2019+ (Office 2019, Excel för webben). Om du behöver stödja äldre versioner måste du falla tillbaka på manuell looping eller använda en annan spill‑kompatibel funktion.

## Steg 6: Praktiska tips och pro‑trick

- **Pro‑tips:** Använd `Cell.setFormulaLocal` om du behöver en localespecifik separator (komma vs semikolon) beroende på användarens regionala inställningar.
- **Se upp för:** Att skriva över befintlig data. Spill‑området kommer att ersätta allt innehåll som redan finns i målområdet.
- **Prestanda‑notering:** Att sätta en formel är billigt; det tunga arbetet sker när du **save** eller **recalculate** arbetsboken. Om du genererar tusentals formler, överväg att inaktivera automatisk beräkning (`wb.calculateFormula()` senare) för att snabba upp bearbetningen.

## Fullt fungerande exempel

Nedan följer den kompletta, färdiga Java‑klassen som innehåller allt vi har gått igenom:

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

**Förväntat resultat:** Öppna `output.xlsx` så ser du tre distinkta spill‑regioner:

- **A1:B2** – siffrorna 1‑3 wrapade i två kolumner.
- **C5:E7** – siffrorna 10‑70 wrapade i tre kolumner.
- **G1:H2** – fruktnamn wrapade i två kolumner.

## Slutsats

Vi har just gått igenom **hur man använder WRAPCOLS** med Aspose.Cells för Java, visat hur du **convert array to rows**, **write formula to cell**, och **populate cells with formula** på ett rent, återanvändbart sätt. Metoden eliminerar tråkig looping, utnyttjar Excels inbyggda spill‑beteende och håller din kod koncis.

Redo för nästa utmaning? Prova att kombinera `WRAPCOLS` med dynamiska datakällor – kanske hämta värden från en databas, konstruera array‑strängen i farten, och låta Excel göra layout‑arbetet. Du kan också experimentera med andra spill‑funktioner som `SEQUENCE` eller `FILTER` för att bygga ännu rikare rapporter.

Om du stöter på problem, lämna en kommentar nedan eller utforska Asposes omfattande dokumentation. Lycka till med kodningen, och njut av kraften i moderna Excel‑formler direkt från Java!

![how to use wrapcols example](/images/wrapcols-demo.png "hur man använder wrapcols i Java – skärmbild av spildata")


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}