---
category: general
date: 2026-08-20
description: Vytvořte excelový sešit v Javě pomocí Aspose.Cells, nastavte formát měny,
  přidejte tučné písmo a importujte pole stylů pro stylované buňky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: cs
lastmod: 2026-08-20
og_description: Vytvořte excelový sešit v Javě, nastavte formát měny, přidejte tučné
  písmo a naučte se, jak importovat styl pomocí Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Vytvořte excelový sešit se stylizovanými buňkami měny v Javě
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
title: Jak vytvořit excelový sešit s formátem měny a tučným písmem v Javě
url: /cs/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit s formátem měny a tučným písmem v Javě

Pokud potřebujete **create excel workbook** programově, tento návod vám přesně ukáže, jak na to. Provedeme vás tvorbou sešitu, aplikací formátu měny, přidáním tučného písma a použitím funkce **how to import style** v Aspose.Cells, aby každá importovaná buňka vypadala konzistentně.

Na konci budete mít připravený soubor `DataTableWithStyleArray.xlsx`, který zobrazuje čísla v dolarech a zvýrazňuje je tučným písmem. Žádné ruční formátování v Excelu není potřeba.

## Požadavky

- Java 17 nebo novější nainstalována.
- Licence Aspose.Cells pro Java (nebo bezplatný evaluační klíč).
- Maven nebo Gradle pro správu závislosti `aspose-cells`.
- Základní znalost Java kolekcí a `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** Pokud narazíte na `LicenseException`, umístěte soubor licence do classpath a před vytvořením sešitu zavolejte `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.

## Jak vytvořit excel workbook se stylovanými buňkami měny

Tato sekce obsahuje hlavní kroky. Každý krok vysvětluje **proč** je důležitý, nejen **co** napsat.

### Krok 1: Inicializace sešitu a listu

Vytvoření nového sešitu vám poskytne čistý kontejner pro veškeré následné formátování.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Proč:** Objekt `Workbook` představuje celý Excel soubor. Přístup k prvnímu `Worksheet` vám umožní okamžitě začít naplňovat data.

### Krok 2: Vytvoření DataTable s číselnými daty

`DataTable` napodobuje databázovou tabulku, což usnadňuje hromadný import řádků.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Proč:** Použití `DOUBLE` zaručuje, že hodnoty zachovají desetinnou přesnost, což je nezbytné, když později **format cells currency**.

### Krok 3: Definování stylu – formát měny a tučné písmo

Zde **nastavíme formát měny** a **přidáme tučné písmo** do objektu `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Proč:** Formátovací řetězec `Number` `$#,##0.00` říká Excelu, aby buňku považoval za peněžní hodnotu, zatímco `setBold(true)` upoutá pozornost na čísla. Umístění stylu do pole nás připraví na krok **how to import style**.

### Krok 4: Konfigurace možností importu pro použití pole stylů

Aspose.Cells vám umožňuje předat `Style[]` pomocí `ImportTableOptions`. Toto je oficiální metoda **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Proč:** Bez `ImportTableOptions` by importované buňky zdědily výchozí styl, čímž by ztratily formát měny a tučnost, které jsme definovali.

### Krok 5: Import DataTable do listu

Nyní přeneseme data do listu do buňky `A1`, přičemž se automaticky použije pole stylů.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` označuje, že první řádek `DataTable` obsahuje záhlaví sloupců.
- `"A1"` je levý horní roh, kde import začíná.

> **Proč:** Import s polem stylů zaručuje, že každá importovaná buňka získá styl **format cells currency**, který jsme připravili dříve.

### Krok 6: Uložení sešitu na disk

Nakonec zapíšeme sešit v paměti do fyzického souboru.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Proč:** Uložení zachová formátování, což vám nebo následným procesům umožní otevřít soubor v Excelu s požadovaným vzhledem.

## Kompletní zdrojový kód

Níže je kompletní, připravená ke spuštění třída v Javě. Zkopírujte ji do svého IDE, nahraďte `YOUR_DIRECTORY` existujícím adresářem a spusťte.

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

### Očekávaný výstup

Když otevřete `DataTableWithStyleArray.xlsx` v Microsoft Excelu, měli byste vidět:

| Částka |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Čísla jsou zobrazena s **currency format** (`$` znak, dvě desetinná místa).
- Písmo pro obě buňky je **bold**, což je zvýrazní.

## Běžné varianty a okrajové případy

| Scénář | Co změnit | Důvod |
|----------|----------------|--------|
| **Různá měna** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Použijte symbol eura nebo jakýkoli formát specifický pro locale. |
| **Více sloupců s různými styly** | Vytvořte více objektů `Style`, naplňte `styleArray` ve stejném pořadí jako sloupce. | Každý sloupec může mít vlastní formát čísla, písmo, pozadí atd. |
| **Velké datové sady** | `cells.importDataTable(dataTable, false, "A1", importOptions);` a nastavte `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Zlepšuje výkon vynecháním řádků záhlaví nebo zbytečných metadat. |
| **Aplikace stylu po importu** | `cells.get("A2").setStyle(currencyStyle);` pro jednotlivé buňky. | Užitečné, když jen podmnožina řádků potřebuje speciální formátování. |

## Tipy pro produkční použití

- **License early**: Zaregistrujte svou licenci Aspose.Cells před vytvořením sešitu, abyste se vyhnuli vodoznaku hodnocení.
- **Thread safety**: Instance `Workbook` **nejsou** thread‑safe. Vytvořte samostatnou instanci pro každý vlákný, pokud generujete mnoho souborů současně.
- **Memory management**: Pro velmi velké listy zvažte použití streaming API `Workbook` (`Workbook` → `WorkbookDesigner`), aby byl nízký odběr paměti.
- **Testing**: Zahrňte unit test, který otevře uložený soubor pomocí Apache POI a ověří, že formát čísla stylu buňky odpovídá `"$#,##0.00"`.

## Závěr

Nyní víte, jak **create excel workbook** v Javě, **set currency format**, **add bold font**, a správně **how to import style** pomocí `ImportTableOptions` v Aspose.Cells. Toto end‑to‑end řešení eliminuje ruční kroky v Excelu a zaručuje, že každá importovaná buňka používá stejný styl **format cells currency**.

Jste připraveni na další výzvu? Zkuste přidat podmíněné formátování, vložit grafy nebo exportovat sešit do PDF — vše při opakovaném použití techniky style‑array. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvoření Excel sešitu pomocí Aspose.Cells v Javě: krok za krokem](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Jak vytvořit a formátovat buňky Excel pomocí Aspose.Cells pro Java: krok za krokem](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Jak stylovat buňky Excel a přidávat hypertextové odkazy pomocí Aspose.Cells pro Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}