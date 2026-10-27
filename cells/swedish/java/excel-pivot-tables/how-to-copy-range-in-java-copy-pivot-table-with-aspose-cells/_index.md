---
category: general
date: 2026-06-30
description: Hur man kopierar ett område i Java med Aspose.Cells – duplicera Excel‑område,
  kopiera pivottabell och ladda Excel‑arbetsbok effektivt.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: sv
og_description: Hur man kopierar ett område i Java med Aspose.Cells. Lär dig duplicera
  Excel‑område, kopiera pivottabell och ladda Excel‑arbetsbok på några minuter.
og_title: Hur man kopierar ett intervall i Java – Steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Hur man kopierar ett område i Java – Kopiera pivottabell med Aspose.Cells
url: /sv/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du område i Java – Kopiera pivottabell med Aspose.Cells

Har du någonsin undrat **how to copy range** från en Excel-arbetsbok till en annan utan att förlora pivottabellens integritet? Du är inte ensam. I många rapporteringspipeline är behovet av att *duplicate Excel range* samtidigt som pivottabellens logik bevaras ett dagligt huvudvärk. Lyckligtvis gör Aspose.Cells för Java detta enkelt, och i den här handledningen går vi igenom ett komplett, körbart exempel som också visar hur du **load Excel workbook**, kopierar en pivottabell och sparar resultatet.

I slutet av den här guiden har du ett självständigt Java‑program som:

* Laddar en befintlig arbetsbok (`load excel workbook`);
* Definierar de exakta cellerna som innehåller en pivottabell;
* Kopierar den **pivot table to sheet** i en helt ny arbetsbok;
* Sparar den nya filen, redo för efterföljande bearbetning.

Inga externa skript, inga manuella steg—bara ren kod.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* Java 8 eller nyare (koden fungerar även med Java 11+);
* Aspose.Cells för Java‑biblioteket (du kan hämta det från Maven Central);
* Två exempel‑Excel‑filer – en källa med en pivottabell (`source.xlsx`) och en destinationsmapp där du skriver `copy-pivot.xlsx`.

Det är allt. Inga avancerade IDE‑trick behövs; vilken textredigerare som helst plus `javac` räcker.

## Steg 1: Ställ in projektet och importera Aspose.Cells

Först och främst—låt oss få biblioteket på plats. Om du använder Maven, lägg till detta beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Om du inte använder Maven, ladda ner JAR‑filen från Aspose‑webbplatsen och lägg den på din classpath. När det är gjort, skapa en ny Java‑klass som heter `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Håll din `src/main/java`‑mapp ren och ge klassen ett meningsfullt namn; det underlättar framtida underhåll.

## Steg 2: Ladda källarbetsboken (`load excel workbook`)

Nu **load excel workbook** som innehåller pivottabellen vi vill kopiera. `Workbook`‑konstruktorn tar en filsökväg, så se till att sökvägen är korrekt.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Varför väljer vi det första kalkylbladet? I de flesta enkla fall finns pivottabellen på det första bladet, men du kan ändra indexet eller använda bladnamnet om så behövs. Denna flexibilitet är en av anledningarna till att Aspose.Cells glänser.

## Steg 3: Definiera området som innehåller pivottabellen

En pivottabell sträcker sig vanligtvis över ett block av celler. Låt oss anta att den upptar `A1:G20`. Du kan justera adressen så att den matchar dina faktiska data.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Om du är osäker på den exakta adressen, öppna arbetsboken i Excel, markera hela pivottabellen och titta i namnboxen. Kom ihåg att **duplicate excel range** fungerar bäst när du riktar in dig på exakt rätt område—inga extra rader, inga saknade kolumner.

## Steg 4: Skapa en ny arbetsbok för destinationen

Vi behöver en ny arbetsbok som ska ta emot det kopierade området. Här kommer vi att **copy pivot table** till ett nytt blad.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Vid den här tidpunkten är destinationsarbetsboken tom, men Aspose.Cells lägger automatiskt till ett standardsblad, som vi kommer att använda som mål.

## Steg 5: Kopiera området – pivottabellen förblir intakt

Här är den magiska raden som **copy pivot table** samtidigt som alla dess interna kopplingar hålls levande.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

`copy`‑metoden tar två argument: käll‑`Range` och destinations‑`Range`. Genom att börja destinationen på `A1` placerar vi pivottabellen exakt där den var i källan. Aspose.Cells kopierar den underliggande pivot‑cachen, så den nya arbetsboken fortfarande vet hur den ska uppdatera pivottabellen.

## Steg 6: Spara den resulterande arbetsboken

Till sist skriver vi den nya filen till disk. Du kan välja vilket format som helst som Aspose stödjer (`.xlsx`, `.xls`, `.csv`, etc.). Vi håller oss till `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Kör programmet, så bör du se en ny arbetsbok med samma pivottabellslayout. Öppna den i Excel—om allt gick bra kan du uppdatera pivottabellen utan fel.

### Förväntad output

När du kör `CopyPivotDemo` skriver konsolen ut:

```
Pivot table successfully copied to copy-pivot.xlsx
```

När du öppnar `copy-pivot.xlsx` visas ett blad som ser identiskt ut med källans pivottabellområde, och **pivot table to sheet** fungerar precis som originalet.

## Fullt fungerande exempel

Nedan är den kompletta, körklara Java‑klassen som binder ihop alla steg. Kopiera‑klistra in den i din IDE, justera filsökvägarna och kör.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Note:** Om din pivottabell sträcker sig över mer än ett kalkylblad, upprepa kopieringssteget för varje relevant blad, eller använd `Workbook.copy` för att klona hela kalkylblad.

## Vanliga frågor & edge‑cases

### Vad händer om källarbetsboken har flera kalkylblad?

Du kan loopa igenom `sourceWorkbook.getWorksheets()` och kopiera varje relevant område. Var bara försiktig så att du behåller samma bladnamn i destinationen om du behöver bevara referenser.

### Behåller den kopierade pivottabellen sin datakälla?

Ja. Aspose.Cells kopierar pivot‑cachen tillsammans med området, så destinationsarbetsboken fortfarande pekar på den ursprungliga datakällan i samma fil. Om du senare flyttar data till ett annat blad kan du behöva uppdatera pivottabellen manuellt.

### Hur kopierar man en pivottabell som använder en extern datakälla?

När pivottabellens datakälla är en extern fil måste du först bädda in den datan i destinationsarbetsboken (t.ex. kopiera källdataområdet) innan du kopierar pivottabellen. Annars kommer pivottabellen att visa “#REF!”‑fel.

### Kan jag kopiera pivottabellen utan den omgivande datan?

Absolut. Justera bara `pivotRange` så att den bara täcker pivottabellens celler (vanligtvis det övre vänstra hörnet plus dataområdet). Du kan också använda `sourceSheet.getPivotTables().get(0).getPivotTableArea()` för att programatiskt hämta det exakta området.

## Tips för verkliga projekt

* **Batch processing:** Om du behöver *duplicate* ett dussintal arbetsböcker, paketera koden ovan i en metod och anropa den i en loop som itererar över en katalog.
* **Performance:** För stora filer, återanvänd en enda `Workbook`‑instans och anropa `Workbook.calculateFormula()` först när alla kopieringar är klara.
* **Error handling:** Omge kopieringslogiken med try‑catch‑block och logga `Exception.getMessage()`; Aspose kastar `CellsException` för ogiltiga områden.

## Slutsats

Vi har precis gått igenom **how to copy range** i Java med Aspose.Cells, och visat hur du **duplicate excel range**, **copy pivot table** och **load excel workbook** i ett enda snyggt program. Stegen är enkla, koden är fullt körbar, och metoden skalar från en enkelsidig demo till batch‑jobb på företagsnivå.

Redo för nästa utmaning? Prova att exportera den kopierade pivottabellen till PDF, eller programatiskt uppdatera den efter att ny data lagts till. Båda uppgifterna bygger på samma grund som vi lagt upp här, så du är väl rustad att ta dig an dem.

Har du frågor eller vill dela dina egna justeringar? Lägg en kommentar nedan—lycka till med kodandet! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man implementerar ett namngivet område med arbetsboksscope i Aspose.Cells Java för förbättrad Excel‑datamanagement](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Hur man kopierar flera kolumner i Excel med Aspose.Cells Java: En komplett guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Kopiera områdesdata](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}