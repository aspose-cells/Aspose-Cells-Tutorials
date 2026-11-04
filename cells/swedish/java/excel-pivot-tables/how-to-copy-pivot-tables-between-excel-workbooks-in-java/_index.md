---
category: general
date: 2026-10-01
description: Lär dig hur du kopierar pivottabeller mellan Excel‑arbetsböcker med Java.
  Denna steg‑för‑steg‑guide visar också hur du kopierar områden mellan arbetsböcker
  och duplicerar Excel‑områden på ett säkert sätt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: sv
lastmod: 2026-10-01
og_description: Hur du kopierar pivottabeller mellan Excel‑arbetsböcker med Java.
  Följ den här guiden för att kopiera ett område till en arbetsbok, duplicera Excel‑områden
  och bevara pivottabellsdata.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Hur man kopierar pivottabeller mellan Excel‑arbetsböcker i Java – komplett
  guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Hur man kopierar pivottabeller mellan Excel‑arbetsböcker i Java
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du pivottabeller mellan Excel‑arbetsböcker i Java

Om du behöver **how to copy pivot** tabeller från en Excel‑fil till en annan, ger den här guiden dig en färdig‑att‑köra‑lösning. Efter de två första meningarna vet du exakt vilka API‑anrop som bevarar pivottabellens definition när du kopierar dataområdet.

Du kommer också att lära dig hur du **copy range between workbooks**, **duplicate Excel range**‑objekt, och säkert **copy range to workbook** utan att förlora formler eller formatering. Inga externa skript behövs—bara ett enda Java‑projekt som använder Aspose.Cells for Java.

## Förutsättningar

* Java Development Kit 17 eller senare.
* Maven eller Gradle för att hantera beroenden.
* En giltig Aspose.Cells for Java‑licens (den kostnadsfria utvärderingen fungerar för testning).
* Två Excel‑filer: `source.xlsx` (innehåller pivottabellen) och en tom `destination.xlsx` (eller låt koden skapa den).

## Steg 1: Ställ in Maven‑projektet

Skapa en `pom.xml` som inkluderar Aspose.Cells. Detta beroende ger dig klasserna `Workbook`, `Worksheet` och `Range` som används i exemplet.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Håll Aspose.Cells‑versionen uppdaterad; nyare versioner ger bättre stöd för komplexa pivot‑cache‑strukturer.

## Steg 2: Ladda källarboken som innehåller pivottabellen

Det första kodblocket demonstrerar **how to copy excel** data genom att ladda källfilen. `Workbook`‑konstruktorn läser in hela filen i minnet och bevarar alla bladobjekt, inklusive pivottabeller.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Varför detta är viktigt:* Aspose.Cells lagrar pivottabeller som en del av kalkylbladets interna modell. Att ladda arbetsboken säkerställer att pivot‑cachen är tillgänglig för senare kopiering.

## Steg 3: Definiera området som inkluderar pivottabellen

En pivottabell kan sträcka sig över flera rader och kolumner. I de flesta fall kan du kopiera hela det använda området på bladet. Metoden `createRange` bygger ett `Range`‑objekt som kopieringsoperationen hanterar.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Om pivottabellen sträcker sig bortom `H20`, ändra helt enkelt adresssträngen. Detta steg är kärnan i **duplicate excel range**‑hanteringen; område‑objektet känner till formler, stilar och dolda rader.

## Steg 4: Skapa en ny arbetsbok som ska ta emot det kopierade området

Du kan antingen börja med en tom arbetsbok eller ladda en befintlig destinationsfil. Här skapar vi en ny arbetsbok, vilket är det renaste sättet att **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Obs:** Om du behöver kopiera pivottabellen till ett specifikt bladnamn, byt namn på `destWs` med `destWs.setName("Report")` innan du klistrar in.

## Steg 5: Kopiera området – Aspose.Cells bevarar automatiskt pivottabellen

`copy`‑metoden överför allt inom källområdet, inklusive pivottabellens definition, cache och formatering. Ingen extra kod behövs för att hålla pivottabellen funktionell.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Varför det fungerar:* Aspose.Cells behandlar pivottabellen som en samling dolda celler och metadata som är knutna till området. När du anropar `copy` replikerar biblioteket den metadata i mål‑arbetsboken.

## Steg 6: Spara destinationsarboken

Slutligen skriver du resultatet till disk. Den sparade filen innehåller en identisk pivottabell som du kan uppdatera eller ändra precis som originalet.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

När programmet körs skrivs en bekräftelse ut och `destination.xlsx` skapas med en fullt funktionell pivottabell.

## Fullt, körbart exempel

När alla steg sätts ihop ser den kompletta Java‑klassen ut så här:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Förväntad output

* Konsol: `Pivot table copied successfully.`
* `destination.xlsx` öppnas i Excel med en pivottabell som är identisk med den i `source.xlsx`. Att uppdatera pivottabellen visar samma datakälla, vilket bevisar att **how to copy pivot** fungerar som avsett.

## Hantera vanliga variationer

### Kopiera flera kalkylblad

Om ditt projekt kräver att kopiera flera blad, loopa igenom arbetsbokens kalkylblad och upprepa steg 2‑4 för varje blad. Pivottabellen i varje blad bevaras oberoende.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Bevara externa datakopplingar

Pivottabeller som förlitar sig på externa datakällor behåller anslutningssträngen efter kopiering. Destinationen måste dock ha åtkomst till samma datakälla. Verifiera anslutningen genom att öppna pivottabellen och kontrollera fliken **Data**.

### Hantera sammanslagna celler

Om källområdet innehåller sammanslagna celler kopierar Aspose.Cells automatiskt sammanslagningslayouten. Kontrollera ändå resultatet om destinationsarboken använder en annan standardkolumnbredd.

## Bästa praxis för pålitlig kopiering

| Praxis | Orsak |
|----------|--------|
| Använd det exakta använda området (`srcWs.getCells().getMaxDisplayRange()`) istället för en hårdkodad adress | Säkerställer att hela pivottabellen och dess källdata inkluderas. |
| Applicera en licens innan tunga operationer | Förhindrar utvärderingsvattenstämpeln och förbättrar prestanda. |
| Uppdatera pivottabellen efter kopiering (`pivotTable.refresh()`) om källdatan har ändrats | Säkerställer att destinationen visar de senaste värdena. |
| Skriv enhetstester som öppnar destinationsarboken och påstår att `pivotTable.getPivotFields().size()` matchar källan | Upptäcker oavsiktlig förlust av fält vid framtida kodändringar. |

## Slutsats

Du vet nu **how to copy pivot** tabeller mellan Excel‑arbetsböcker i Java, samt hur du **copy range between workbooks**, **duplicate excel range** och **copy range to workbook** samtidigt som du bevarar all formatering och formler. Exemplet använder Aspose.Cells, som abstraherar bort den lågnivå‑XML‑hantering som krävs av OpenXML SDK.

Nästa steg är att utforska relaterade ämnen som **updating pivot cache programmatically**, **exporting pivot data to CSV** eller **creating pivot tables from scratch**. Alla dessa bygger på samma koncept som demonstrerats här.

Lycka till med kodandet, och var gärna experimentera med större områden, flera pivottabeller eller anpassad styling – samma mönster gäller i alla scenarier.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}