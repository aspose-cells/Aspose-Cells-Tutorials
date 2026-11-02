---
category: general
date: 2026-07-03
description: Zahrňte export vzorců v Javě pro převod buněk Excelu na text pomocí Aspose.Cells.
  Naučte se, jak efektivně vytisknout oblast Excelu a získat řetězec hodnot buněk.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: cs
og_description: Zahrňte export vzorců v Javě pro převod buněk Excelu na text. Podrobný
  návod krok za krokem, jak vytisknout oblast Excelu a získat hodnoty buněk jako řetězec.
og_title: Zahrnout export vzorců v Javě – Převést buňky Excelu na text
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Zahrnout export vzorců v Javě – Převést buňky Excelu na text
url: /cs/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zahrnout export vzorců v Javě – Převést buňky Excelu na text

Už jste někdy potřebovali **include formulas export** při získávání dat z sešitu Excel? Možná vytváříte reportingovou službu, která musí zachovat původní vzorce a zároveň dodat úhledný textový blok. V takovém případě jste na správném místě. Tento průvodce vás provede převodem buněk Excelu na prostý text—*včetně* vložených vzorců—pomocí Aspose.Cells pro Java.

Také se podíváme na to, jak **print Excel range**, upravit **export table options**, a nakonec **get cell values string**, které můžete zaznamenat, poslat přes API nebo uložit do databáze. Na konci budete mít plně spustitelný úryvek a solidní pochopení důvodů za každým voláním.

## Co si odnesete

- Kompletní, připravený Java program ke zkopírování, který načte soubor `.xlsx`, vybere oblast a exportuje ji jako formátovaný řetězec.
- Pochopení třídy `ExportTableOptions` a proč má význam přepínání `setExportAsString` a `setIncludeFormula`.
- Tipy pro práci s velkými listy, zacházení s různými datovými typy a přizpůsobení výstupního formátu.
- Rychlý kontrolní seznam běžných úskalí (např. sloučené buňky, skryté řádky a lokálně specifické formáty čísel).

### Požadavky

- Java 17 nebo novější (kód se kompiluje i se staršími verzemi, ale budeme se držet nejnovější LTS).
- Aspose.Cells pro Java 23.10 (nebo jakékoli novější vydání) — můžete jej získat z Maven Central.
- Ukázkový soubor `input.xlsx` umístěný ve složce, kterou ovládáte (cesta je v příkladu pevně zakódována pro přehlednost).

Pokud už to máte, pojďme na to.

## Krok 1: Nastavte projekt a přidejte závislosti

Nejprve vytvořte Maven projekt (nebo Gradle, pokud dáváte přednost). Přidejte závislost Aspose.Cells do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Tip:** Pokud používáte firemní proxy, ujistěte se, že je repozitář dosažitelný; jinak sestavení selže s chybou „Could not resolve dependencies“.

Jakmile Maven dokončí stahování, budete připraveni psát Java kód.

## Krok 2: Načtěte sešit a získejte požadovaný list

První řádek ukázkového kódu ukazuje, jak otevřít existující sešit:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou k vašemu souboru. Konstruktor `Workbook` automaticky detekuje formát souboru (XLS, XLSX, CSV atd.), takže jej nemusíte specifikovat.

Dále získáme první list:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Proč první list? V mnoha šablonách jsou data na první kartě, ale můžete zadat libovolný index nebo dokonce použít `get("SheetName")`, pokud dáváte přednost pojmenovanému přístupu.

## Krok 3: Definujte oblast, kterou chcete exportovat

Nyní přichází jádro operace **convert excel cells text**. Řeknete Aspose.Cells, které buňky získat, vytvořením objektu `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Řetězec `"A1:C3"` je klasická adresa ve stylu A1. Může být také vytvořen programově:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Tato flexibilita pomáhá, když je velikost oblasti dynamická – například když načtete poslední použitý řádek pomocí `ws.getCells().getMaxDataRow()`.

## Krok 4: Nakonfigurujte ExportTableOptions pro zahrnutí vzorců

Zde se skrývá kouzlo **include formulas export**. Ve výchozím nastavení Aspose.Cells vrací *zobrazené* hodnoty. Pokud buňka obsahuje `=SUM(A1:A3)`, získáte vypočtené číslo, nikoli text vzorce. Pro změnu to nastavte pomocí `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Proč oba příznaky? `setExportAsString(true)` říká API, aby spojilo buňky pomocí výchozího oddělovače (tabulátor pro sloupce, nový řádek pro řádky). `setIncludeFormula(true)` přepíná zdroj hodnoty z „zobrazené hodnoty“ na „surový vzorec“. Pokud chcete jen hodnoty, nechte jej `false`.

### Volitelné úpravy

- `eto.setExportHiddenRows(true);` – zahrnout řádky skryté v Excelu.  
- `eto.setExportHiddenColumns(true);` – totéž pro sloupce.  
- `eto.setExportAsHTML(true);` – získat HTML místo prostého textu.

Klidně experimentujte; třída options je hřiště pro **export table options**.

## Krok 5: Získejte oblast jako formátovaný řetězec

Nyní získáme data:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Vrácený `txt` vypadá zhruba takto (předpokládáme, že A1:C3 obsahuje směs hodnot a vzorců):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Všimněte si tabulátoru (`\t`) oddělujícího sloupce a nového řádku (`\n`) oddělujícího řádky. Řetězec můžete později rozdělit, pokud potřebujete 2‑D pole:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Krok 6: Vytiskněte výsledek – „Print Excel Range“ zjednodušeno

Nakonec vypíšeme řetězec do konzole:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Spuštěním programu se vytiskne přesně výstup uvedený výše. Odtud můžete řetězec zapsat do log souboru, poslat přes HTTP nebo uložit do NoSQL dokumentu.

## Úplný, připravený k spuštění příklad

Sestavením všeho dohromady získáte kompletní program. Zkopírujte, vložte a stiskněte **Run** – žádné chybějící importy.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Očekávaný výstup (ukázka)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Pokud váš sešit obsahuje čísla formátovaná jako data, zobrazí se v lokálně specifickém formátu (např. `2026‑07‑03`). Pro vynucení ISO formátu dat můžete upravit `ExportTableOptions` pomocí vlastního `NumberFormat`.

## Řešení okrajových případů a častých otázek

### Co když oblast obsahuje sloučené buňky?

Sloučené buňky jsou považovány za hodnotu levé horní buňky. Zbytek sloučené oblasti se zobrazí jako prázdné řetězce. Pokud potřebujete adresu sloučené oblasti, dotazujte se na `Cell.getMergedRange()` před exportem.

### Mohu exportovat obrovský list (stovky tisíc řádků)?

Ano, ale dejte pozor na spotřebu paměti. Použijte `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby Aspose.Cells streamovalo data na disk. Také zvažte export po částech (např. 10 000 řádků najednou), aby byl řetězec zvládnutelný.

### Jak změním oddělovač sloupců?

`ExportTableOptions` nabízí metodu `setSeparator(char separator)`. Pro výstup ve stylu CSV nastavte na `','`:

```java
eto.setSeparator(',');
```

### Respektují vzorce externí odkazy?

Pokud vzorec odkazuje na jiný sešit, Aspose.Cells zachová text odkazu (`='[Other.xlsx]Sheet1'!A1`). Nevypočítá externí hodnotu, pokud nenačtete i ten sešit.

## Profesionální tipy pro produkční kód

- **Cache the workbook** pokud čtete the

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi se sešitem](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Jak převést Excel do PDF v Javě pomocí Aspose.Cells&#58; krok za krokem](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Exportovat Excel sešit jako obrázek pomocí Aspose.Cells pro Java&#58; krok za krokem](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}