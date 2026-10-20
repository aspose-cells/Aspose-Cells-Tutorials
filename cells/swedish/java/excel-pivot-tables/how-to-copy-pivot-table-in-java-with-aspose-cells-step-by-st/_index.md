---
category: general
date: 2026-10-20
description: Lär dig hur du kopierar pivottabell med Aspose.Cells i Java. Den här
  handledningen visar hur du kopierar ett område till ett nytt blad och duplicerar
  pivottabellbladet på ett säkert sätt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: sv
lastmod: 2026-10-20
og_description: Hur du kopierar pivottabell med Aspose.Cells i Java. Följ den här
  guiden för att kopiera ett område till ett nytt blad och duplicera pivottabellbladet
  utan att förlora data.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Hur man kopierar en pivottabell i Java – komplett Aspose.Cells‑handledning
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man kopierar pivottabell i Java med Aspose.Cells – steg‑för‑steg‑guide
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar pivottabell i Java med Aspose.Cells – steg‑för‑steg guide

Om du behöver **how to copy pivot table** i en Java‑applikation, guidar den här guiden dig genom de exakta stegen. Oavsett om du bygger en rapporteringsmotor eller automatiserar datamigrering, kommer du att se hur du kopierar ett område till ett nytt blad samtidigt som pivottabellens definition och data bevaras.

Att kopiera en pivottabell kan kännas riskabelt eftersom den underliggande cachen och fältinställningarna ofta går förlorade. Denna handledning visar ett pålitligt tillvägagångssätt med Aspose.Cells, visar den kompletta körbara koden och förklarar varför varje rad är viktig. I slutet kommer du att kunna duplicera pivottabellbladet på några sekunder.

## Förutsättningar

* Java 8 eller nyare installerat.
* Aspose.Cells för Java (version 23.10 eller senare) tillagd i ditt projekts classpath.
* En källarbok (`source.xlsx`) som innehåller en pivottabell i området `A1:G20`.
* Grundläggande kunskap om Java‑ och Excel‑koncept.

Inga ytterligare bibliotek krävs; Aspose.Cells hanterar alla Excel‑operationer internt.

## Så kopierar du pivottabell – övergripande strategi

Kärnidén är enkel:

1. Ladda arbetsboken som innehåller den ursprungliga pivottabellen.
2. Identifiera det exakta området som inkluderar pivottabellen.
3. Skapa ett nytt kalkylblad som ska ta emot de kopierade data.
4. Använd `Range.copy`‑metoden för att överföra området till det nya bladet.  
   Denna metod kopierar automatiskt pivottabellcachen, så pivottabellen förblir funktionell.
5. Spara arbetsboken till en ny fil.

Eftersom kopieringsoperationen fungerar på områdesnivå, behåller **duplicate pivot table sheet** alla fältkonfigurationer, filter och beräknade objekt.

## Steg 1: Ladda källarboken

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Varför detta är viktigt*: Att ladda arbetsboken ger dig åtkomst till dess kalkylblad, celler och pivottabellcachen. Aspose.Cells läser in hela filen i minnet, så efterföljande operationer är snabba och trådsäkra.

## Steg 2: Definiera källområdet som innehåller pivottabellen

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Varför detta är viktigt*: `createRange`‑anropet talar om för Aspose.Cells exakt vilka celler som ska kopieras. Att inkludera hela pivottabellområdet säkerställer att de dolda cache‑raderna också överförs. Om du utelämnar någon del av cachen blir den kopierade pivottabellen tom.

## Steg 3: Lägg till ett destinationskalkylblad för de kopierade data

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Varför detta är viktigt*: Att lägga till ett dedikerat blad isolerar den kopierade pivottabellen från originalet, vilket gör det enkelt att jämföra resultat eller använda bladet som mall för vidare bearbetning.

## Steg 4: Kopiera området till destinationskalkylbladet (pivottabellen bevaras)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Varför detta är viktigt*: `copy`‑metoden kopierar inte bara cellvärden och formatering utan även replikerar pivottabellcachen. Detta är nyckelsteget som gör att du kan **duplicate pivot table sheet** utan att förlora någon funktionalitet.

## Steg 5: Spara arbetsboken med det kopierade området

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Varför detta är viktigt*: Spara skapar en ny Excel‑fil (`result.xlsx`) som innehåller både originalet och det duplicerade pivottabellbladet. Du kan nu öppna filen i Excel för att verifiera att pivottabellen fungerar exakt som tidigare.

## Fullt, körbart exempel

När allt sätts ihop, här är det kompletta programmet som du kan kopiera‑klistra in i din IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Förväntat resultat

* Att öppna `result.xlsx` visar två kalkylblad:
  * **Sheet1** – de ursprungliga data och pivottabellen.
  * **CopyResult** – en exakt duplicering av pivottabellen, fullt funktionell.
* Alla pivottabellfält, filter och beräknade objekt beter sig identiskt med källan.

Om du ändrar källpivottabellen efter kopieringen kommer det duplicerade bladet **inte** att återspegla dessa förändringar eftersom cachen duplicerades vid kopieringstillfället. Denna isolering är ofta önskvärd när du behöver ett ögonblicksbild av rapporten.

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Pivot table appears blank** | Det kopierade området utelämnade de dolda cache‑raderna. | Se till att området inkluderar hela cachen (vanligtvis några rader under den synliga tabellen). |
| **Destination sheet name already exists** | `add("CopyResult")` kastar ett undantag om namnet redan är upptaget. | Använd `workbook.getWorksheets().addUniqueName("CopyResult")` eller kontrollera `contains` innan du lägger till. |
| **File path errors** | Felaktig `YOUR_DIRECTORY` leder till `FileNotFoundException`. | Använd absoluta sökvägar eller Javas `Paths.get(...).toAbsolutePath()` för att lösa platser. |
| **Performance slowdown on large workbooks** | Kopiering av enorma områden kopierar onödiga celler. | Begränsa området till exakt pivottabellområde, eller använd `Range.copy` med `CopyOptions` för att hoppa över formatering om det inte behövs. |

## Proffstips: Använd `CopyOptions` för finare kontroll

Om du bara behöver pivottabellens data och vill hoppa över cellformatering, kan du skicka ett `CopyOptions`‑objekt:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Detta minskar filstorleken på det duplicerade bladet och påskyndar kopieringsoperationen, särskilt för stora arbetsböcker.

## Så kopierar du område till nytt blad utan att förlora formler

Exemplet ovan kopierar redan formler eftersom `Range.copy` bevarar dem som standard. Om du bara vill ha värden (t.ex. för att frysa det aktuella läget), sätt `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Nu innehåller destinationsbladet statiska värden, men pivottabellen kommer fortfarande att fungera eftersom dess cache är en del av området.

## Sammanfattning av lösningen

* **How to copy pivot table** – ladda arbetsboken, definiera det exakta området, lägg till ett nytt kalkylblad, kopiera området och spara.
* Processen visar också **copy range to new sheet** och hur man **duplicate pivot table sheet** på ett säkert sätt.
* Du kan finjustera kopieringen med `CopyOptions` för prestanda eller enbart värden.

## Nästa steg och relaterade ämnen

* **Refresh pivot cache programmatically** – använd `PivotTable.refreshData()` efter att ha uppdaterat källdata.
* **Export pivot table to PDF** – kombinera denna kopieringsteknik med `PdfSaveOptions` för att skapa ögonblicksrapporter.
* **Automate multi‑sheet duplication** – loopa igenom alla kalkylblad och tillämpa samma kopieringslogik.

Experimentera med dessa variationer för att anpassa mönstret till din specifika rapporteringspipeline. Om du stöter på kantfall, såsom externa datakällor eller VBA‑styrda pivoter, fungerar samma område‑kopieringsmetod, men du kan behöva kopiera de underliggande anslutningsobjekten också.

---

*Lycklig kodning! Om den här handledningen hjälpte dig att lära dig **how to copy pivot table**, dela gärna den med kollegor eller bidra med förbättringar.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man kopierar område och bevarar en pivottabell i Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Skapa ny arbetsbok i Java – Full guide för att kopiera pivottabell](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Kopiera pivottabell mellan arbetsböcker – Steg‑för‑steg Java‑guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}