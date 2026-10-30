---
category: general
date: 2026-07-16
description: Nastavte vlastní oddělovač buněk při exportu tabulky Excel do TXT pomocí
  Aspose.Cells. Naučte se, jak exportovat vzorce Excelu do textu a uložit list jako
  soubor txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: cs
lastmod: 2026-07-16
og_description: Nastavení vlastního oddělovače buněk v Aspose.Cells vám umožní exportovat
  tabulku Excel do TXT s přesným formátováním. Exportujte vzorce Excelu do textu a
  snadno uložte list jako soubor txt.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Nastavit vlastní oddělovač buněk – Exportovat tabulku Excel do TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Nastavit vlastní oddělovač buněk – Exportovat tabulku Excel do TXT
url: /cs/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte vlastní oddělovač buněk – Export tabulky Excel do TXT

Nastavení vlastního oddělovače buněk je tajná ingredience, kterou potřebujete, když chcete čistý textový výpis z listu Excel. Už jste se někdy ptali, jak **export excel table to txt** bez toho, aby výsledek byl chaotický zmatek čárek a konců řádků? V tomto tutoriálu projdeme celý proces pomocí Aspose.Cells pro Java, od načtení sešitu až po **save worksheet as txt file** s oddělovačem, který si zvolíte.

## Co se naučíte

- Jak **set custom cell separator** pro export textu.
- Přesné kroky k **export excel formulas to text**, aby se s vámi přenesly vyhodnocené hodnoty.
- Způsoby, jak **export excel data as plain text** při zachování rozvržení.
- Kompletní, připravený k běhu ukázkový kód, který můžete zkopírovat a vložit do svého projektu.

Na konci tohoto průvodce budete schopni vzít libovolný sešit Excel, vybrat rouru (`|`), tabulátor (`\t`) nebo jakýkoli jiný znak, a vytvořit čistý, oddělený textový soubor, který milují downstream systémy.

### Požadavky

- Nainstalovaný Java 8 nebo novější.
- Maven (nebo jakýkoli build nástroj) pro stažení knihovny Aspose.Cells pro Java.
- Vzorek sešitu (`TableDemo.xlsx`), který obsahuje tabulku s formuláři.

Pokud je máte, pojďme na to – žádné zbytečné okázalosti, jen praktické kroky.

## Krok 1: Přidejte Aspose.Cells do svého projektu

Než budete moci **set custom cell separator**, potřebujete mít Aspose.Cells JAR na classpathu. Nejjednodušší způsob je pomocí Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Pokud dáváte přednost Gradle, vyměňte XML za ekvivalentní `implementation 'com.aspose:aspose-cells:24.10'`. Jakmile je závislost vyřešena, jste připraveni psát Java kód, který pracuje s Excel soubory.

## Krok 2: Načtěte sešit – Příprava na export tabulky Excel do TXT

První skutečný řádek kódu je vždy stejný: otevřít sešit, který obsahuje tabulku, kterou chcete exportovat.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Zde získáme první list (`get(0)`). Pokud jsou vaše data na jiném listu, stačí změnit index nebo použít `get("SheetName")`. Tato část je nezbytná pro **export excel table to txt**, protože exportér pracuje na úrovni listu.

## Krok 3: Nastavte vlastní oddělovač buněk – Jádro exportu

Nyní přichází hvězda představení: konfigurace `ExportTableOptions`. Tento objekt vám umožní přesně rozhodnout, jak se každá buňka zobrazí ve výsledném textovém souboru.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Proč **set custom cell separator**? Protože výchozí oddělovač je tabulátor, který může kolidovat s daty, jež již tabulátory obsahují. Výběrem roury (`|`) nebo středníku zajistíte, že každá sloupec zůstane odlišný, když downstream parser soubor čte.

### Export Excel Formulí do Textu

Řádek `setFormulaValueInCell(true)` říká Aspose.Cells, aby zapisoval **export excel formulas to text** jako *výsledek* vzorce, nikoli samotný řetězec vzorce. Pokud byste to vynechali, buňka obsahující `=SUM(A1:A5)` by se v TXT objevila jako `=SUM(A1:A5)`, což zřídka chcete.

## Krok 4: Připojte exportní možnosti k TXT Save Options

Nyní svážeme tyto tabulkové možnosti s celkovou konfigurací exportu TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` je hlavní objekt, který řídí, jak se celý list zapíše. Vložením `exportTableOptions` do něj zajistíte, že každá tabulka na listu respektuje pravidlo **set custom cell separator**.

## Krok 5: Uložte list jako TXT soubor – Dokončení exportu

Nakonec zapíšeme soubor na disk.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Spuštěním tohoto programu se vytvoří `TableExported.txt`. Každý řádek původní tabulky Excel se nyní zobrazí jako řádek hodnot oddělených rourou, například:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Všimněte si, že vzorec ve sloupci **Total** byl vyhodnocen před zápisem – díky `setFormulaValueInCell(true)`. To je podstata **export excel data as plain text**, přičemž se zachovávají vypočtené výsledky.

## Krok 6: Ověřte výstup – Vypadá to správně?

Otevřete vygenerovaný `TableExported.txt` v libovolném textovém editoru. Měli byste vidět:

- Jeden řádek na každý řádek v Excelu.
- Sloupce oddělené znakem roury, který jste nastavili pomocí `setCellValueSeparator`.
- Žádné zbytečné čárky nebo tabulátory, pokud nebyly součástí původních hodnot buněk.
- Výsledky vzorců, nikoli samotné vzorce.

Pokud narazíte na neočekávané znaky, zkontrolujte zvolený oddělovač. Některé znaky (jako roura) jsou bezpečné pro většinu CSV‑stylových parserů, ale pokud vaše data již roury obsahují, zvažte jiný oddělovač, například `~` nebo tabulátor (`\t`).

## Tipy, okrajové případy a osvědčené postupy – Export Excel dat jako prostý text

| Situace | Co udělat |
|-----------|------------|
| **Data již obsahují vámi zvolený oddělovač** | Přepněte na méně běžný znak (`^`, `~` nebo Unicode ne‑tisknutelné znaky). |
| **Potřebujete kódování UTF‑8** |  |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Uložit Excel jako textový soubor s vlastním oddělovačem pomocí Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Uložit Excel Text Vlastní Oddělovač Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Uložit Excel Text Vlastní Oddělovač Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}