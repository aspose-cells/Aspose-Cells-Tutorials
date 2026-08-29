---
category: general
date: 2026-07-16
description: Skapa en ny arbetsbok och kopiera en pivottabell med Aspose.Cells för
  Java. Lär dig hur du duplicerar en pivottabell och kopierar ett Excel‑område på
  några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: sv
lastmod: 2026-07-16
og_description: Skapa en ny arbetsbok och kopiera en pivottabell med Aspose.Cells
  för Java. Denna guide visar hur du duplicerar en pivottabell och kopierar ett Excel‑område
  effektivt.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Skapa ny arbetsbok & kopiera pivottabell i Java – Komplett handledning
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Skapa ny arbetsbok och kopiera pivottabell i Java – Fullständig steg‑för‑steg‑guide
url: /sv/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok och kopiera pivottabell i Java – Fullständig steg‑för‑steg‑guide

Har du någonsin undrat hur man **create new workbook** samtidigt som man bevarar en komplex pivottabell från en befintlig fil? Om du någonsin har stirrat på ett Excel‑blad, tänkt “Jag behöver den här pivottabellen i en annan arbetsbok”, och sedan kliat dig i huvudet, är du inte ensam. Den goda nyheten är att med Aspose.Cells for Java kan du duplicera en pivottabell på bara några få rader.

I den här handledningen går vi igenom de exakta stegen för att **copy pivot table**‑data, **duplicate pivot table**‑strukturer och **copy Excel range**‑innehåll — allt medan vi skapar en ny arbetsbok från grunden. När du är klar har du ett färdigt Java‑program som gör exakt det du bad om.

## Vad du kommer att lära dig

- Hur man **create new workbook** programatiskt med Aspose.Cells.
- Det exakta sättet att definiera området som innehåller en pivottabell.
- Tekniker för att **copy pivot table** och **duplicate pivot table** utan att förlora formatering eller datakopplingar.
- Hur man **copy Excel range** effektivt och sparar resultatet.
- Vanliga fallgropar och tips för att hantera större pivottabeller.

Inga externa referenser behövs — allt är självständigt, körbart och förklarat.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **Java Development Kit (JDK) 11+** – någon nyare version fungerar.
2. **Aspose.Cells for Java**‑biblioteket (den senaste versionen per 2026‑07‑16). Du kan hämta det från Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. En käll‑Excel‑fil (`SourceWithPivot.xlsx`) som redan innehåller en pivottabell du vill kopiera.
4. En IDE eller enkel textredigerare — IntelliJ IDEA, Eclipse eller VS Code räcker.

Har du allt? Bra — låt oss köra.

---

## Steg 1: **Create New Workbook** och läs in källfilen

Det första vi behöver är ett nytt arbetsboksobjekt som så småningom kommer att hålla den duplicerade pivottabellen. Samtidigt måste vi läsa in den ursprungliga arbetsboken så att vi kan referera till dess pivottabellsområde.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Varför detta är viktigt:**  
> Att läsa in källarbetsboken ger oss åtkomst till det underliggande `Range`‑objektet som kapslar pivottabellen. Om du hoppar över detta steg har du inget att kopiera, och **duplicate pivot table**‑operationen kommer att misslyckas tyst.

---

## Steg 2: Definiera **Copy Excel Range** som innehåller pivottabellen

En pivottabell är inte en enskild cell — den sträcker sig över ett rektangulärt block. Vi måste tala om för Aspose.Cells exakt vilka celler som ska kopieras.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Tips:**  
> Om du inte är säker på det exakta området, öppna källarbetsboken i Excel, markera pivottabellen och titta i namn‑rutan. Den visar något i stil med `A1:G20`. Att använda det exakta området säkerställer att alla fältinställningar, filter och beräkningar behålls när vi senare **copy pivot table**.

---

## Steg 3: **Create New Workbook** som ska ta emot den kopierade pivottabellen

Nu skapar vi en helt ny arbetsbok — här kommer vår **duplicate pivot table** att finnas.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Vad händer under huven?**  
> Standardkonstruktorn bygger en arbetsbok med ett enda tomt blad. Detta är den rena duk vi behöver för ett **create new workbook**‑scenario. Inga kvarvarande stilar eller dolda blad att oroa sig för.

---

## Steg 4: **Copy Pivot Table** – Kopiera faktiskt det definierade Excel‑området

Med både källa och destination redo utför vi kopieringsoperationen. Detta steg löser **how to copy pivot**‑delen av pusslet.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Varför `copy` fungerar för pivottabeller:**  
> Aspose.Cells behandlar pivottabellen som en del av cellsamlingen. När du kopierar området tas pivottabellscachen, fältlistan och layouten med. Resultatet blir en fullt funktionell **duplicate pivot table** i den nya arbetsboken.

---

## Steg 5: Spara resultatet och verifiera **Copy Pivot Table**‑operationen

Slutligen sparar du destinationsarbetsboken till disk. Öppna filen i Excel för att bekräfta att pivottabellen visas exakt som i källfilen.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Förväntat resultat:**  
- `CopyPivotResult.xlsx` öppnas med ett kalkylblad som innehåller samma pivottabell som du såg i `SourceWithPivot.xlsx`.  
- Alla rad‑/kolumnetiketter, filter och beräknade fält är intakta.  
- Du kan nu redigera källdata oberoende, och den nya arbetsboken behåller sin egen pivottabellscache.

---

## Kantfall & Vanliga frågor

### Vad händer om källpivottabellen sträcker sig över mer än ett blad?
Aspose.Cells kan bara kopiera områden inom ett enda kalkylblad åt gången. Om din pivottabell sträcker sig över flera blad måste du kopiera varje relevant område separat och sedan länka dem manuellt.

### Bevarar den här metoden anpassade talformat?
Ja. `copy`‑metoden kopierar cellstilar, inklusive talformat, teckensnitt och färger. Men om du har villkorlig formatering som refererar till externa områden, dubbelkolla dessa referenser efter kopieringen.

### Hur kopierar man en pivottabell som använder en extern datakälla?
När pivottabellen hämtar data från en extern anslutning (t.ex. en SQL‑fråga) överförs inte anslutningsinformationen av `copy`. Du måste återskapa datakällan i destinationsarbetsboken eller bädda in källdata i förväg.

### Kan jag kopiera endast pivottabellens layout utan underliggande data?
Det kan du göra genom att först rensa datacellerna i källområdet och sedan kopiera endast pivottabellens layout. Detta är ett mer avancerat scenario och krävs vanligtvis inte för en enkel **duplicate pivot table**‑uppgift.

---

## Fullt fungerande exempel (alla steg kombinerade)

Nedan är den kompletta, körklara Java‑klassen. Byt bara ut `YOUR_DIRECTORY` mot den faktiska mappvägen på din maskin.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Kör programmet (`java CopyPivotTableDemo`) så ser du konsolmeddelandet som bekräftar att det lyckades.

---

## Pro‑tips & bästa praxis

- **Validate the range** before copying. Use `srcWs.getCells().maxDisplayRange` to programmatically discover the used area if you don’t want to hard‑code `"A1:G20"`.
- **Turn off calculation** temporarily for huge workbooks to speed up the copy:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) in long‑running services to avoid memory leaks.
- **Version compatibility:** The code works with Aspose.Cells 23.12 and later. Older versions may require `srcRange.copyTo` instead of `copy`.

---

## Nästa steg

Nu när du har bemästrat **create new workbook** och **copy pivot table**, kan du utforska:

- **How to copy pivot** across multiple worksheets in a batch job.
- Adding **copy excel range** for regular data tables alongside the pivot.
- Automating **duplicate pivot table** creation for each month’s report using a loop.
- Exporting the duplicated pivot to PDF or HTML with Aspose.Cells’ built‑in renderers.

Var och en av dessa ämnen bygger på grunden som lagts här, och de drar alla nytta av samma rena, programatiska tillvägagångssätt.

---

## Slutsats

Vi har gått igenom hela processen för **create new workbook**, definierat käll‑**copy excel range** och **copy pivot table** för att skapa en **duplicate pivot table** i Java med Aspose.Cells. Lösningen är kortfattad, fullt funktionell och klar för produktionsbruk. Känn dig fri att justera området, experimentera med olika källfiler eller integrera denna logik i en större rapporteringspipeline.

Om du stöter på problem eller har idéer för att utöka den här handledningen, lämna en kommentar nedan. Lycka till med kodningen!

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}