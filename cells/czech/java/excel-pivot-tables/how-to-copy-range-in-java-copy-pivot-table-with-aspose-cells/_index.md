---
category: general
date: 2026-06-30
description: Jak zkopírovat oblast v Javě pomocí Aspose.Cells – duplikovat oblast
  v Excelu, zkopírovat kontingenční tabulku a efektivně načíst Excel sešit.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: cs
og_description: Jak kopírovat oblast v Javě pomocí Aspose.Cells. Naučte se duplikovat
  oblast v Excelu, kopírovat kontingenční tabulku a načíst sešit Excel během několika
  minut.
og_title: Jak zkopírovat rozsah v Javě – krok za krokem
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
title: Jak zkopírovat oblast v Javě – Kopírování kontingenční tabulky pomocí Aspose.Cells
url: /cs/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat oblast v Javě – Kopírování kontingenční tabulky pomocí Aspose.Cells

Už jste se někdy zamýšleli, **jak zkopírovat oblast** z jednoho sešitu Excel do druhého, aniž byste ztratili integritu kontingenční tabulky? Nejste v tom sami. V mnoha reportovacích řetězcích je potřeba *duplikovat oblast Excel* a zachovat logiku kontingenční tabulky, což je každodenní problém. Naštěstí Aspose.Cells pro Javu to dělá hračkou a v tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám také ukáže, jak **načíst sešit Excel**, zkopírovat kontingenční tabulku a uložit výsledek.

Na konci tohoto průvodce budete mít samostatný Java program, který:

* Načte existující sešit (`load excel workbook`);
* Definuje přesné buňky, které obsahují kontingenční tabulku;
* Zkopíruje tuto **kontingenční tabulku na list** do zcela nového sešitu;
* Uloží nový soubor, připravený pro další zpracování.

Žádné externí skripty, žádné ruční kroky – jen čistý kód.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte:

* Java 8 nebo novější (kód funguje také s Java 11+);
* knihovnu Aspose.Cells pro Javu (můžete ji získat z Maven Central);
* Dva ukázkové soubory Excel – jeden zdrojový s kontingenční tabulkou (`source.xlsx`) a cílovou složku, kam zapíšete `copy-pivot.xlsx`.

To je vše. Není potřeba žádné složité triky v IDE; stačí jakýkoli textový editor a `javac`.

## Krok 1: Nastavení projektu a import Aspose.Cells

Nejprve – přidejme knihovnu do projektu. Pokud používáte Maven, přidejte tuto závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Pokud Maven nepoužíváte, stáhněte JAR z webu Aspose a přidejte jej do classpath. Jakmile je to hotovo, vytvořte novou Java třídu s názvem `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Udržujte složku `src/main/java` čistou a dejte třídě výstižný název; usnadní to budoucí údržbu.

## Krok 2: Načtení zdrojového sešitu (`load excel workbook`)

Nyní skutečně **načteme sešit Excel**, který obsahuje kontingenční tabulku, kterou chceme zkopírovat. Konstruktor `Workbook` přijímá cestu k souboru, takže se ujistěte, že cesta je správná.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Proč vybíráme první list? Ve většině jednoduchých případů je kontingenční tabulka na prvním listu, ale můžete změnit index nebo použít název listu, pokud je to potřeba. Tato flexibilita je jedním z důvodů, proč Aspose.Cells vyniká.

## Krok 3: Definování oblasti, která obsahuje kontingenční tabulku

Kontingenční tabulka obvykle zabírá blok buněk. Předpokládejme, že se nachází v rozsahu `A1:G20`. Adresu můžete upravit podle svých skutečných dat.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Pokud si nejste jisti přesnou adresou, otevřete sešit v Excelu, vyberte celou kontingenční tabulku a podívejte se do pole názvu. Pamatujte, že **duplicate excel range** funguje nejlépe, když cílíte na přesnou oblast – žádné nadbytečné řádky, žádné chybějící sloupce.

## Krok 4: Vytvoření nového sešitu pro cíl

Potřebujeme nový sešit, který přijme zkopírovanou oblast. Zde **copy pivot table** na nový list.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

V tuto chvíli je cílový sešit prázdný, ale Aspose.Cells automaticky přidá výchozí list, který použijeme jako cíl.

## Krok 5: Kopírování oblasti – Kontingenční tabulka zůstává nedotčena

Tady je kouzelný řádek, který **copy pivot table** a zároveň zachová všechny vnitřní propojení.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

Metoda `copy` přijímá dva argumenty: zdrojový `Range` a cílový `Range`. Začínáme cílový rozsah na `A1`, takže umístíme kontingenční tabulku přesně tam, kde byla ve zdroji. Aspose.Cells kopíruje podkladovou pivot cache, takže nový sešit stále ví, jak kontingenční tabulku obnovit.

## Krok 6: Uložení výsledného sešitu

Na závěr zapíšeme nový soubor na disk. Můžete zvolit libovolný formát, který Aspose podporuje (`.xlsx`, `.xls`, `.csv`, atd.). Zůstaneme u `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Spusťte program a měli byste vidět nový sešit se stejným rozvržením kontingenční tabulky. Otevřete jej v Excelu – pokud vše proběhlo v pořádku, budete moci kontingenční tabulku obnovit bez chyb.

### Očekávaný výstup

Když spustíte `CopyPivotDemo`, konzole vypíše:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Otevření `copy-pivot.xlsx` ukáže list, který vypadá identicky jako oblast kontingenční tabulky ve zdroji, a **pivot table to sheet** funguje stejně jako originál.

## Kompletní funkční příklad

Níže je kompletní, připravená ke spuštění Java třída, která spojuje všechny kroky. Zkopírujte a vložte ji do svého IDE, upravte cesty k souborům a spusťte.

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

> **Poznámka:** Pokud vaše kontingenční tabulka zasahuje do více listů, opakujte krok kopírování pro každý relevantní list, nebo použijte `Workbook.copy` k klonování celých listů.

## Časté otázky a okrajové případy

### Co když má zdrojový sešit více listů?

Můžete projít `sourceWorkbook.getWorksheets()` a zkopírovat každý relevantní rozsah. Jen buďte opatrní, aby názvy listů v cíli zůstaly stejné, pokud potřebujete zachovat odkazy.

### Zachovává zkopírovaná kontingenční tabulka svůj zdroj dat?

Ano. Aspose.Cells kopíruje pivot cache spolu s rozsahem, takže cílový sešit stále odkazuje na původní zdroj dat ve stejném souboru. Pokud později přesunete data na jiný list, možná budete muset kontingenční tabulku ručně obnovit.

### Jak zkopírovat kontingenční tabulku, která používá externí zdroj dat?

Když je zdroj dat kontingenční tabulky externí soubor, musíte nejprve vložit tato data do cílového sešitu (např. zkopírovat zdrojový datový rozsah) před samotným kopírováním kontingenční tabulky. Jinak se zobrazí chyby “#REF!”.

### Můžu zkopírovat kontingenční tabulku bez okolních dat?

Určitě. Stačí upravit `pivotRange`, aby zahrnoval jen buňky kontingenční tabulky (obvykle levý horní roh plus datová oblast). Můžete také použít `sourceSheet.getPivotTables().get(0).getPivotTableArea()` k získání přesného rozsahu programově.

## Tipy pro reálné projekty

* **Dávkové zpracování:** Pokud potřebujete duplikovat desítky sešitů, zabalte výše uvedený kód do metody a zavolejte ji v cyklu, který prochází adresář.
* **Výkon:** U velkých souborů znovu použijte jedinou instanci `Workbook` a zavolejte `Workbook.calculateFormula()` až po dokončení všech kopií.
* **Zpracování chyb:** Obalte logiku kopírování bloky try‑catch a zaznamenávejte `Exception.getMessage()`; Aspose vyhazuje `CellsException` pro neplatné rozsahy.

## Závěr

Právě jsme probrali **jak zkopírovat oblast** v Javě pomocí Aspose.Cells, ukázali vám, jak **duplicate excel range**, **copy pivot table** a **load excel workbook** v jednom přehledném programu. Kroky jsou jednoduché, kód je plně spustitelný a přístup se škáluje od jednosheetového demu po podnikovou dávkovou úlohu.

Jste připraveni na další výzvu? Zkuste exportovat zkopírovanou kontingenční tabulku do PDF, nebo ji programově obnovit po přidání nových dat. Obě úlohy staví na stejném základu, který jsme zde vytvořili, takže budete dobře vybaveni je zvládnout.

Máte otázky nebo chcete sdílet své úpravy? Zanechte komentář níže – šťastné programování! 

![Diagram ukazující, jak je oblast s kontingenční tabulkou zkopírována z jednoho sešitu do druhého](https://example.com/images/how-to-copy-range-diagram.png "diagram jak zkopírovat oblast")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak implementovat pojmenovanou oblast s rozsahem sešitu v Aspose.Cells Java pro pokročilou správu dat v Excelu](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Jak zkopírovat více sloupců v Excelu pomocí Aspose.Cells Java: Kompletní průvodce](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Kopírování dat v rozsahu](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}