---
category: general
date: 2026-06-30
description: Sortera unika värden i Excel med Java. Lär dig hur du anger formel, beräknar
  om formler och genererar en unik lista i Excel med Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: sv
og_description: Sortera unika värden i Excel med Java. Den här guiden visar hur du
  anger formel, omberäknar formler och genererar en unik lista i Excel på några minuter.
og_title: Sortera unika värden i Excel – Java‑handledning för matrisformler
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
title: Sortera unika värden i Excel – Komplett Java‑guide för att skapa matrisformler
url: /sv/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sortera unika värden i Excel – Komplett Java‑guide för att sätta array‑formler

Har du någonsin undrat hur man **sorterar unika värden i Excel** utan att dra formler runt? Du är inte ensam. I många rapporteringsscenario behöver du en ren, alfabetiskt sorterad lista med distinkta poster, och att göra det manuellt är jobbigt.  

Den goda nyheten? Med några rader Java‑kod kan du **sätta array‑formel** på ett kalkylblad, sedan **omberäkna formler** så att det spillda området fylls automatiskt. I den här handledningen går vi igenom allt—från att skapa en arbetsbok till att generera en unik lista i Excel‑stil—så att du kan bädda in lösningen direkt i din applikation.

## Vad den här handledningen täcker

- Att sätta upp ett Java‑projekt med Aspose.Cells (biblioteket som driver kodsnutten).  
- Att använda `SORT`‑ och `UNIQUE`‑funktionerna tillsammans för att **generera unik lista i Excel** resultat.  
- Att applicera en **array‑formel** på en cell programatiskt.  
- Att trigga ett beräkningspass så steget **hur man omberäknar formler** sker omedelbart.  
- Att verifiera resultatet och justera lösningen för kantfall som tomma celler eller icke‑sammanhängande områden.

Vid slutet av den här guiden kommer du kunna släppa in en färdig metod i vilken Java‑tjänst som helst som behöver exportera rena Excel‑ark.

> **Proffstips:** Om du redan använder Maven sparar det dig från att manuellt hantera JAR‑filer att lägga till Aspose.Cells som ett beroende.

---

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| Java 8 eller nyare | Aspose.Cells riktar sig mot Java 8+. |
| Maven (eller Gradle) | Förenklar hantering av beroenden. |
| Aspose.Cells för Java | Tillhandahåller `Workbook`, `Worksheet` och formel‑API:er som vi kommer att använda. |
| Grundläggande kunskap om Excel‑funktioner | Förståelse för `SORT` och `UNIQUE` hjälper dig att anpassa koden. |

> *Om du ännu inte har Aspose.Cells, lägg till detta i din `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Steg 1: Skapa en ny arbetsbok (Hur man sätter formel börjar här)

Först behöver vi en tom arbetsbok. Tänk på den som en tom duk där vi senare kommer att **sätta array‑formel** på cell `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Varför skapa en ny arbetsbok?*  
> Den garanterar en ren miljö och undviker dolda formler som kan störa våra testdata.

---

## Steg 2: Fyll med exempeldata (Valfritt men hjälpsamt)

För att tydligt se resultatet, låt oss fylla kolumn **B** med några dubblettposter.

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

> *Varför använda kolumn B?*  
> Formeln vi kommer att skriva refererar till `B1:B10`, så att hålla datan där speglar det klassiska Excel‑exemplet.

---

## Steg 3: Sätt en array‑formel som **sorterar unika värden i Excel**

Nu händer magin. Vi kombinerar `UNIQUE` (för att ta bort dubbletter) med `SORT` (för att sortera dem alfabetiskt). Det resulterande uttrycket är en **array‑formel**, vilket betyder att den spills över intilliggande celler automatiskt.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Så fungerar det

- `UNIQUE(B1:B10)` skannar området och returnerar en vertikal array med distinkta strängar.  
- `SORT(...)` tar den arrayen och sorterar den i stigande ordning.  
- Genom att omsluta hela uttrycket med `=` och anropa `setFormulaArray` instruerar vi Aspose.Cells att behandla resultatet som en **spilld array**, precis som Excel skulle göra.

> **Obs:** Om du använder en äldre version av Excel som saknar `SORT` eller `UNIQUE` kan du falla tillbaka på `SORT(UNIQUE(...))` med **LET**‑funktionen eller använda äldre array‑formler (`=INDEX(...)`). Handledningen fokuserar på den moderna dynamiska array‑metoden eftersom den är det renaste sättet att **generera unik lista i Excel** idag.

---

## Steg 4: Omberäkna formler så att det spillda området fylls

Efter att formeln är på plats utvärderas den inte automatiskt av arbetsboken. Det är här steget **hur man omberäknar formler** kommer in.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Anropet `calculateFormula()` tvingar Aspose.Cells att köra Excel‑motorn, vilket fyller cellerna `A1`, `A2`, … med de sorterade unika värdena.

> *Varför inte förlita sig på lat utvärdering?*  
> I ett server‑sidigt sammanhang behöver du ofta datan klar för export (CSV, PDF, etc.) direkt efter beräkningen, så ett explicit anrop garanterar konsistens.

---

## Steg 5: Verifiera resultatet (Valfri felsökning)

Det är alltid en bra idé att skriva ut de spillda värdena till konsolen—särskilt när du lär dig ett nytt API.

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

Running the program prints:

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

Öppna `SortedUniqueValues.xlsx` så ser du samma data som spillts från `A1` och nedåt.

---

## Hantera kantfall

### Tomma celler i källområdet

Om `B1:B10` innehåller tomma celler kommer `UNIQUE` att behandla dem som en distinkt post. För att ignorera tomma celler, omslut området med `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Icke‑sammanhängande data

När dina data finns i flera kolumner kan du slå ihop dem med `CHOOSE` eller `TEXTJOIN` innan du applicerar `UNIQUE`. Till exempel:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Dessa justeringar visar flexibiliteten i **hur man sätter formel** för mer komplexa scenarier.

---

## Fullt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta, körbara Java‑programmet. Kopiera‑klistra in det i din IDE, lägg till Aspose.Cells‑beroendet och kör *Run*.

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

**Förväntad output** (visas i konsolen) matchar den sorterade, deduplicerade listan vi diskuterade tidigare. När du öppnar den genererade Excel‑filen ser du samma värden som spillts från `A1` och nedåt.

---

## Vanliga frågor

**Q: Fungerar detta med äldre Excel‑versioner (före Office 365)?**  
A: `SORT`‑ och `UNIQUE`‑funktionerna är en del av Dynamic Array‑motorn som introducerades i Excel 365. För äldre filer måste du använda klassiska array‑formler som `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells kan fortfarande utvärdera dem, men syntaxen är mer omständlig.

**Q: Kan jag sätta array‑formeln på ett annat område än `A1`?**  
A: Absolut. Ändra bara adressen i `cells.get("A1")`. Den spillda arrayen kommer alltid att börja i den cell du anger och expandera åt höger och ner efter behov.

**Q: Vad händer om min källdata är större än `B1:B10`?**  
A: Ersätt det statiska området med ett dynamiskt, t.ex. `B:B` eller ett namngivet område. Formeln blir `=SORT(UNIQUE(B:B))`. Var försiktig med kolumn‑omfattande referenser i mycket stora blad; de kan påverka prestandan.

---

## Slutsats

Vi har precis gått igenom **hur man sätter formel** i Java för att **sortera unika värden i Excel**, hur man **omberäknar formler**, och hur man **genererar unik lista i Excel** med Aspose.Cells kraftfulla API. Stegen är enkla: skapa en arbetsbok, fyll data, applicera en array‑formel, trigga beräkning och verifiera resultatet.  

Från detta kan du gå vidare—lägga till villkorsstyrd formatering, exportera till PDF, eller integrera metoden i en webbtjänst som levererar färdiga rapporter. Kärnidén förblir densamma: låt Excels egna funktioner göra det tunga arbetet, och låt Java orkestrera processen.

Redo att ta din Excel‑automation till nästa nivå? Prova att byta ut `SORT` mot `SORTBY` för att sortera efter en sekundär kolumn, eller experimentera med `FILTER` för att utesluta rader som inte uppfyller affärsregler. Möjligheterna är praktiskt taget oändliga.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}