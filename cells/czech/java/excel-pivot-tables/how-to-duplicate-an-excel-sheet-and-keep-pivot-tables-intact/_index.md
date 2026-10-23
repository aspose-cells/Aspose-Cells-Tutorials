---
category: general
date: 2026-10-23
description: Naučte se, jak duplikovat list v Excelu v Javě při zachování kontingenčních
  tabulek. Tento průvodce také ukazuje, jak kopírovat kontingenční tabulky, kopírovat
  rozsahy v Excelu a kopírovat list s kontingenčními daty.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: cs
lastmod: 2026-10-23
og_description: Duplikujte list Excel v Javě a zachovejte kontingenční tabulky. Sledujte
  tento kompletní návod, jak kopírovat kontingenční tabulky, kopírovat oblasti v Excelu
  a kopírovat list s kontingenčními daty.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplikovat list Excel s kontingenčními tabulkami v Javě – průvodce krok
  za krokem
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Jak duplikovat list v Excelu a zachovat kontingenční tabulky v neporušeném
  stavu v Javě
url: /cs/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikovat list v Excelu a zachovat kontingenční tabulky v Java

Pokud potřebujete **duplikovat list v Excelu** a zachovat všechny kontingenční tabulky, tento průvodce vám přesně ukáže, jak na to. Uvidíte stručné řešení, které kopíruje list, kopíruje konkrétní oblast a dokonce kopíruje kontingenční tabulku do jiného sešitu – vše v čisté Javě pomocí Aspose.Cells.

Duplikování listu v Excelu je běžný úkol, když generujete měsíční zprávy ze šablony nebo když potřebujete sandboxovou kopii pro testování. Níže uvedený kód funguje s Aspose.Cells 25.11 nebo novějším, který zavedl možnost `setCopyPivotTable(true)`.

## Co budete potřebovat

- Java 17 (nebo jakýkoli aktuální JDK) nainstalována
- Aspose.Cells for Java 25.11 nebo novější ve vašem projektu (Maven koordináta `com.aspose:aspose-cells:25.11`)
- Zdrojový sešit (`SourceWithPivot.xlsx`), který již obsahuje kontingenční tabulku
- IDE nebo nástroj pro sestavení dle vašeho výběru (IntelliJ IDEA, Eclipse, Maven, Gradle, atd.)

## Krok 1: Načtěte zdrojový sešit, který obsahuje kontingenční tabulku

Prvním krokem je otevřít sešit, který obsahuje kontingenční tabulku, kterou chcete zachovat.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Proč je tento krok důležitý:** Načtení zdrojového sešitu vám poskytuje přístup k objektům listů, buňkám a vloženým kontingenčním tabulkám. Bez toho nemůžete odkazovat na data kontingenční tabulky, kterou plánujete kopírovat.

## Krok 2: Vytvořte prázdný cílový sešit (nebo načtěte existující)

Můžete buď začít s prázdným sešitem, nebo otevřít existující soubor, který přijme duplikovaný list.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tip:** Pokud již máte sešit s reporty, nahraďte řádek výše `new Workbook("ExistingReport.xlsx")`, aby se duplikovaný list přidal do něj.

## Krok 3: Zkopírujte celý list – kontingenční tabulka se zachová automaticky

Kopírování celého listu je nejjednodušší způsob, jak **kopírovat list s kontingenční tabulkou**. Aspose.Cells automaticky kopíruje definici kontingenční tabulky a její mezipaměť.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Proč to funguje:** `addCopy` klonuje strukturu listu, hodnoty buněk, styly a všechny vložené kontingenční tabulky. Nový list v `dstWb` bude vypadat identicky jako originál, včetně mezipaměti kontingenční tabulky.

## Krok 4: (Volitelné) Zkopírujte pouze konkrétní oblast, která zahrnuje kontingenční tabulku

Někdy nechcete celý list – možná potřebujete jen část, která obsahuje kontingenční tabulku. Zde použijete **kopírování oblasti v Excelu** a explicitně požádáte o kopírování kontingenční tabulky.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Jak to pomáhá:** `setCopyPivotTable(true)` nutí engine duplikovat definici kontingenční tabulky i při kopírování omezené oblasti. Bez tohoto příznaku by se zkopírovala jen surová data a kontingenční tabulka by byla ztracena.

## Krok 5: Uložte cílový sešit

Nakonec zapište duplikovaný obsah do nového souboru.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vytvoří `DuplicatedWithPivot.xlsx` v cílovém adresáři. Otevřete soubor v Excelu a uvidíte:

- Nový list pojmenovaný `Sheet1 (Copy)` (nebo původní název s připojeným „Copy“)
- Kontingenční tabulka se objeví přesně jako ve zdrojovém listu, plně funkční
- Pokud jste použili volitelné kopírování oblasti, jsou přítomny jen buňky A1:G30, ale kontingenční tabulka stále funguje, protože její mezipaměť byla zkopírována

## Časté otázky a okrajové případy

### Jak zkopírovat kontingenční tabulku do jiného sešitu bez kopírování celého listu?

Pokud potřebujete jen kontingenční tabulku a její podkladová data, zkopírujte oblast, která obsahuje jak zdrojová data, tak kontingenční tabulku, a poté použijte `setCopyPivotTable(true)`. Použije se stejný kód jako v **Kroku 4**; jen se ujistěte, že oblast zahrnuje zdroj dat.

### Co když má zdrojový sešit více listů s kontingenčními tabulkami?

Opakujte **Krok 3** pro každý list, který chcete duplikovat:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Funguje to s chráněnými listy?

Aspose.Cells může kopírovat chráněné listy, ale musíte je nejprve odemknout, pokud potřebujete po kopírování upravit kontingenční tabulku:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Mohu zkopírovat kontingenční tabulku do existujícího sešitu, který již obsahuje list se stejným názvem?

Ano. Použijte `addCopy` s unikátním názvem:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro tip: ověřte mezipaměť kontingenční tabulky

Po kopírování můžete programově potvrdit, že mezipaměť kontingenční tabulky existuje:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Pokud ID mezipaměti vypíše nezáporné číslo, kontingenční tabulka byla úspěšně duplikována.

## Závěr

Nyní víte, jak **duplikovat list v Excelu** v Javě při zachování všech kontingenčních tabulek, jak přímo **kopírovat kontingenční** tabulky, jak **kopírovat oblast v Excelu**, která zahrnuje kontingenční tabulku, a jak **kopírovat list s kontingenční tabulkou** nebo **kopírovat kontingenční tabulku do sešitu** pomocí Aspose.Cells 25.11+. Použijte tyto vzory k automatizaci tvorby reportů, vytvoření kopií šablon nebo budování testovacích prostředí, která potřebují identické analýzy založené na kontingenčních tabulkách.

Jste připraveni na další průzkum? Zkuste exportovat duplikovaný sešit do PDF nebo programově obnovit mezipaměť kontingenční tabulky po kopírování, aby se zajistilo, že jsou zobrazeny nejnovější data. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}