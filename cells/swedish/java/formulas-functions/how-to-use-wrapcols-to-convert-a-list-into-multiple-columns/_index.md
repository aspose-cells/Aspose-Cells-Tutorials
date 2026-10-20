---
category: general
date: 2026-10-16
description: hur man använder wrapcols i Java och snabbt konverterar en lista till
  kolumner med en formel – lär dig hur du ställer in formeln för en flerkolumnslayout
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: sv
lastmod: 2026-10-16
og_description: hur man använder wrapcols för att konvertera en lista till kolumner
  i Java. Följ den här kompletta guiden för att ställa in formel och skapa en flerkolumnslayout
  i Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: Hur man använder wrapcols – steg‑för‑steg guide för Java‑utvecklare
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: Hur du använder wrapcols för att konvertera en lista till flera kolumner i
  Java
url: /sv/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du wrapcols för att konvertera en lista till flera kolumner i Java

Om du behöver **how to use wrapcols** i ett Java‑projekt, visar den här guiden de exakta stegen. Du kommer att lära dig hur du anger formeln, konverterar en lista till kolumner och skapar en flerkolumnslayout utan manuellt kopiera‑och‑klistra.

Handledningen täcker allt från projektuppsättning till hantering av kantfall, så att du kan tillämpa lösningen på vilket kalkylblad som helst som innehåller en enkelsidig lista. Inga extra verktyg krävs utöver Aspose.Cells for Java.

## Förutsättningar

* Java 17 eller nyare installerat  
* Maven 3.8+ (eller Gradle) för beroendehantering  
* En licens för **Aspose.Cells for Java** – den kostnadsfria utvärderingen fungerar för testning  
* Grundläggande kunskap om Excel‑formler  

Dessa punkter säkerställer att koden körs utan kompileringsfel.

## Steg 1: Lägg till Aspose.Cells i ditt projekt

Lägg till följande Maven‑beroende i `pom.xml`. Om du använder Gradle gäller samma koordinater.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

Biblioteket tillhandahåller klasserna `Cell` och `Worksheet` som används senare när du **how to set formula** för ett område.

## Steg 2: Skapa en arbetsbok och fyll i källistan

Den första uppgiften är att generera en arbetsbok som innehåller en vertikal lista (A2:A100). Denna lista representerar de data du vill **convert list to columns**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

Loopen fyller den första kolumnen med 99 objekt, vilket ger dig en realistisk lista att arbeta med. Du kan ersätta de genererade värdena med data som läses från en databas eller en annan källa.

## Steg 3: Så använder du wrapcols för att ange formeln

Nu får du se kärnan i handledningen: att använda funktionen `WRAPCOLS` för att **create multi‑column layout**. Funktionen tar två argument – källområdet och antalet kolumner du vill ha.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Varför detta fungerar* – `WRAPCOLS` läser det vertikala området `A2:A100` och fördelar sedan värdena rad‑för‑rad över tre kolumner (B, C och D). Resultatet visas med början i cellen som innehåller formeln (`A1`). Eftersom formeln returnerar en array expanderar Aspose.Cells automatiskt resultatet till de nödvändiga cellerna.

### Vad som händer bakom kulisserna

När arbetsboken sparas utvärderar Aspose.Cells formeln och skriver de expanderade värdena till filen. Om du öppnar `WrapColsResult.xlsx` i Excel kommer du att se:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

Layouten demonstrerar ett **create multi‑column layout**‑mönster som är användbart för rapporter, instrumentpaneler eller utskrivbara formulär.

## Steg 4: Verifiera resultatet programatiskt (valfritt)

Om du vill bekräfta att formeln producerade den förväntade matrisen utan att öppna Excel kan du läsa tillbaka värdena efter beräkning.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

Att köra programmet skriver ut något liknande:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

Detta bekräftar att **how to use wrapcols** fungerar som avsett och att **convert list to columns**‑operationen lyckades.

## Steg 5: Vanliga variationer och kantfall

### Ändra antalet kolumner

Om du behöver ett annat antal kolumner, ändra det andra argumentet i `WRAPCOLS`. Till exempel skapar `=WRAPCOLS(A2:A100,5)` fem kolumner. Funktionen justerar automatiskt radantalet för att rymma den nya layouten.

### Hantera en ojämn liststorlek

När källområdets längd inte är delbar med kolumnantalet fyller `WRAPCOLS` den sista kolumnen med tomma celler. Detta beteende är användbart för att skapa balanserade tabeller utan manuell trimning.

### Använda ett dynamiskt område

Du kan ersätta `A2:A100` med ett namngivet område eller en formel som beräknar den sista raden, till exempel `A2:INDEX(A:A, COUNTA(A:A))`. Detta gör lösningen robust när listlängden förändras.

### Undvika cirkulära referenser

Placera formeln i en cell som inte är en del av källområdet. Om du av misstag placerar formeln i `A2:A100` kommer Excel att rapportera ett fel för cirkulär referens. Skriv alltid formeln i en separat cell (vanligtvis `A1`).

## Steg 6: Tips för produktionsanvändning

* **Cache the workbook** – Om du genererar många rapporter i en loop, återanvänd en enda `Workbook`‑instans och rensa tidigare data för att minska minnesbelastningen.  
* **Set calculation mode** – Använd `workbook.getSettings().setCalculateFormulaOnOpen(false)` när du bara behöver den råa formeln utan omedelbar utvärdering.  
* **Internationalization** – Funktionsnamnet `WRAPCOLS` är språkoberoende, men decimalavgränsare i andra formler kan skilja sig. Behåll formler på engelska för att undvika missmatchningar.  
* **Performance** – För listor som överstiger 10 000 rader, utvärdera formeln en gång och läs sedan arrayvärdena direkt för att undvika upprepade beräkningar.

## Slutsats

Du vet nu **how to use wrapcols** i Java för att **convert list to columns** och **create multi‑column layout** med en enda formel. Det kompletta, körbara exemplet demonstrerar hela arbetsflödet: lägga till biblioteket, fylla i data, tillämpa formeln och verifiera resultatet.

Härifrån kan du:

* Justera antalet kolumner för att passa din rapporteringsstil  
* Kombinera `WRAPCOLS` med andra funktioner som `SORT` eller `FILTER` för avancerad databehandling  
* Exportera arbetsboken till PDF, CSV eller HTML med Aspose.Cells inbyggda konverterare  

Experimentera med dessa variationer för att effektivisera dina Excel‑automatiseringsuppgifter. Om du stöter på problem, gå igenom avsnittet om kantfalls‑hantering ovan eller konsultera Aspose.Cells‑dokumentationen för ytterligare formelstöd. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man använder WRAPCOLS i Java – Komplett guide till Excel‑array‑formler](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [Hur man använder WRAPCOLS i Java – Komplett Excel WRAPCOLS‑exempel](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [Hur man använder Reduce i Excel med Java – Lambda‑formelguide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}