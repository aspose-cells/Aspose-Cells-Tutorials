---
category: general
date: 2026-08-20
description: Skapa en Excel-arbetsbok i Java med Aspose.Cells, ange valutformat, lägg
  till fet stil och importera stilarray för formaterade celler.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: sv
lastmod: 2026-08-20
og_description: Skapa Excel-arbetsbok i Java, ställ in valutformat, lägg till fet
  stil och lär dig hur du importerar stil med Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Skapa Excel-arbetsbok med formaterade valutaceller i Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Hur man skapar en Excel-arbetsbok med valutaformat och fet stil i Java
url: /sv/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du en Excel-arbetsbok med valutformat och fet stil i Java

Om du behöver **skapa en Excel-arbetsbok** programatiskt visar den här guiden exakt hur. Vi går igenom hur du bygger en arbetsbok, applicerar ett valutformat, lägger till fet stil och använder **how to import style**‑funktionen i Aspose.Cells så att varje importerad cell ser enhetlig ut.

Du får en färdig **`DataTableWithStyleArray.xlsx`**‑fil som visar siffror som dollar och markerar dem i fet stil. Ingen manuell formatering i Excel behövs.

## Förutsättningar

Innan du börjar, se till att du har:

- Java 17 eller senare installerat.
- En Aspose.Cells för Java‑licens (eller en gratis utvärderingsnyckel).
- Maven eller Gradle för att hantera `aspose-cells`‑beroendet.
- Grundläggande kunskap om Java‑samlingar och `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Proffstips:** Om du får ett `LicenseException`, placera licensfilen i classpath och anropa `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` innan du skapar arbetsboken.

## Så skapar du en Excel-arbetsbok med formaterade valutaceller

Detta avsnitt innehåller kärnstegen. Varje steg förklarar **varför** det är viktigt, inte bara **vad** du ska skriva.

### Steg 1: Initiera arbetsboken och kalkylbladet

Att skapa en ny arbetsbok ger dig en ren behållare för all efterföljande formatering.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Varför:** `Workbook`‑objektet representerar hela Excel‑filen. Genom att komma åt det första `Worksheet` kan du börja fylla i data omedelbart.

### Steg 2: Bygg en DataTable med numeriska data

En `DataTable` efterliknar en databastabell, vilket gör det enkelt att importera rader i bulk.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Varför:** Genom att använda `DOUBLE` garanteras att värdena behåller sin decimalprecision, vilket är avgörande när du senare **formaterar celler som valuta**.

### Steg 3: Definiera en stil – valutformat och fet stil

Här **sätter vi valutformat** och **lägger till fet stil** på ett `Style`‑objekt.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Varför:** Formatsträngen `$#,##0.00` i `Number` talar om för Excel att behandla cellen som ett monetärt värde, medan `setBold(true)` framhäver siffrorna. Att placera stilen i en array förbereder oss för **how to import style**‑steget.

### Steg 4: Konfigurera importalternativ för att använda stil‑arrayen

Aspose.Cells låter dig skicka en `Style[]` via `ImportTableOptions`. Detta är den officiella **how to import style**‑metoden.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Varför:** Utan `ImportTableOptions` skulle importerade celler ärva standardstilen, vilket skulle förlora valutformateringen och fetstil som vi definierade.

### Steg 5: Importera DataTable till kalkylbladet

Nu för vi in data i bladet på cell `A1`, och applicerar stil‑arrayen automatiskt.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indikerar att den första raden i `DataTable` innehåller kolumnrubriker.
- `"A1"` är den övre vänstra hörnet där importen börjar.

> **Varför:** Import med stil‑arrayen garanterar att varje importerad cell får den **format cells currency**‑stil vi förberedde tidigare.

### Steg 6: Spara arbetsboken till disk

Till sist skriver du den minnesbaserade arbetsboken till en fysisk fil.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Varför:** Genom att spara bevaras formateringen, så att du eller efterföljande processer kan öppna filen i Excel med önskat utseende.

## Fullständig källkod

Nedan är den kompletta, körklara Java‑klassen. Kopiera den till din IDE, ersätt `YOUR_DIRECTORY` med en befintlig mapp och kör.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Förväntad output

När du öppnar `DataTableWithStyleArray.xlsx` i Microsoft Excel bör du se:

| Belopp |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Siffrorna visas med ett **valutformat** (`$`‑tecken, två decimaler).
- Teckensnittet för båda cellerna är **fet**, vilket får dem att sticka ut.

## Vanliga variationer och kantfall

| Scenario | Vad som ska ändras | Orsak |
|----------|--------------------|-------|
| **Different currency** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Använd Euro‑symbolen eller ett valfritt lokalanpassat format. |
| **Multiple columns with different styles** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Varje kolumn kan ha sitt eget talformat, teckensnitt, bakgrund osv. |
| **Large data sets** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Förbättrar prestanda genom att hoppa över rubrikrader eller onödig metadata. |
| **Applying style after import** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Användbart när endast en delmängd av raderna behöver speciell formatering. |

## Tips för produktionsanvändning

- **Licensiera tidigt**: Registrera din Aspose.Cells‑licens innan du skapar arbetsboken för att undvika utvärderingsvattenstämpeln.
- **Trådsäkerhet**: `Workbook`‑instanser är **inte** trådsäkra. Skapa en separat instans per tråd om du genererar många filer samtidigt.
- **Minneshantering**: För mycket stora blad, överväg att använda `Workbook`‑s streaming‑API (`Workbook` → `WorkbookDesigner`) för att hålla minnesanvändningen låg.
- **Testning**: Inkludera ett enhetstest som öppnar den sparade filen med Apache POI och verifierar att cellstils talformat matchar `"$#,##0.00"`.

## Slutsats

Du vet nu hur du **skapar en Excel-arbetsbok** i Java, **sätter valutformat**, **lägger till fet stil**, och korrekt **how to import style** med Aspose.Cells `ImportTableOptions`. Denna helhetslösning eliminerar manuella Excel‑steg och garanterar att varje importerad cell följer samma **format cells currency**‑stil.

Redo för nästa utmaning? Prova att lägga till villkorsstyrd formatering, bädda in diagram eller exportera arbetsboken till PDF – allt medan du återanvänder samma stil‑array‑teknik. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}