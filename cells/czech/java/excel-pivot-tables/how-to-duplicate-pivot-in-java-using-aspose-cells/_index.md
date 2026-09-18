---
category: general
date: 2026-09-18
description: jak duplikovat kontingenční tabulku v Javě s Aspose.Cells – rychle a
  spolehlivě zkopírovat kontingenční tabulku mezi sešity
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: cs
lastmod: 2026-09-18
og_description: Jak duplikovat kontingenční tabulku v Javě pomocí Aspose.Cells. Sledujte
  tento kompletní tutoriál, jak zkopírovat kontingenční tabulku mezi sešity s čistým
  Java kódem.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplikovat kontingenční tabulku v Javě – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak duplikovat kontingenční tabulku v Javě pomocí Aspose.Cells
url: /cs/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikovat kontingenční tabulku v Javě pomocí Aspose.Cells

Pokud potřebujete **jak duplikovat kontingenční tabulku** v Java aplikaci, tento průvodce vám ukáže přesné kroky. Načtením Excel sešitu, definováním oblasti buněk kontingenční tabulky a zkopírováním této oblasti do nového sešitu můžete přesunout kontingenční tabulku, aniž byste ztratili její definici nebo data.

Kopírování kontingenční tabulky je běžná potřeba při generování reportů, archivaci analýz nebo rozdělení velkého sešitu na modulární části. V tomto tutoriálu se naučíte, jak **kopírovat oblast mezi sešity**, jak **načíst Excel sešit v Javě** a nuance **jak bezpečně kopírovat kontingenční tabulku**.

Na konci budete mít připravený spustitelný Java program, který duplikuje kontingenční tabulku z `Source.xlsx` do `PivotCopied.xlsx` pomocí Aspose.Cells pro Java.

## Požadavky

* Nainstalovaný JDK 8 nebo novější.
* Maven (nebo jiný nástroj pro sestavení) pro správu závislostí.
* Aspose.Cells pro Java verze 23.10 nebo novější. Přidejte následující Maven závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Zdrojový sešit (`Source.xlsx`) obsahující kontingenční tabulku v oblasti **A1:H30**.

## Jak duplikovat kontingenční tabulku v Javě

Základní myšlenka je jednoduchá:

1. **Načtěte zdrojový sešit** – získáte tak přístup k listu, který obsahuje kontingenční tabulku.
2. **Definujte oblast buněk**, která obklopuje kontingenční tabulku.
3. **Vytvořte cílový sešit** – prázdný soubor, který přijme zkopírovanou oblast.
4. **Zkopírujte oblast** – Aspose.Cells automaticky duplikuje definici kontingenční tabulky.
5. **Uložte cílový sešit** – nyní máte samostatný soubor se stejnou kontingenční tabulkou.

Níže je kompletní spustitelný Java program, který tyto kroky provádí.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Proč to funguje

* **Aspose.Cells** považuje kontingenční tabulku za součást kolekce buněk listu. Když zavoláte `copyRange`, knihovna kopíruje nejen hodnoty buněk, ale také podkladovou pivot cache a definici, takže nový sešit obsahuje plně funkční duplikát.
* Objekt `CopyOptions` ve výchozím nastavení zachovává vzorce, formáty a vložené objekty. Můžete jej přizpůsobit (např. `setCopyColumnWidths(true)`), pokud potřebujete větší kontrolu.

## Kopírování oblasti mezi sešity – podrobnější pohled

Zatímco výše uvedený příklad kopíruje jeden souvislý blok, `copyRange` dokáže zpracovat libovolnou obdélníkovou oblast. Pokud vaše kontingenční tabulka zasahuje do nesouvislých oblastí, můžete `copyRange` volat vícekrát nebo použít `Worksheet.copy` pro duplikaci celého listu.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** Při kopírování velkých sešitů povolte `CopyOptions.setPreserveCellStyle(true)`, aby se předešlo zbytečnému duplikování stylů, což může zlepšit výkon.

## Jak kopírovat kontingenční tabulku do sešitu – práce s více kontingenčními tabulkami

Pokud zdrojový list obsahuje více než jednu kontingenční tabulku, můžete iterovat přes pivot tabulky listu a každou z nich zkopírovat samostatně:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Tento přístup zajišťuje, že každá kontingenční tabulka si zachová svůj původní název a datový zdroj.

## Načtení Excel sešitu v Javě – běžné úskalí

* **Oddělovače cest k souborům:** Používejte lomítka (`/`) nebo `File.separator`, aby byl kód nezávislý na platformě.
* **Chybějící licence:** Aspose.Cells funguje v evaluačním režimu, ale výstup bude obsahovat vodoznak. Zaregistrujte licenci pomocí `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` před načtením sešitu, aby se vodoznak odstranil.
* **Velké soubory:** Pro sešity větší než 100 MB zvažte použití `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` s možnostmi streamování, aby se snížila spotřeba paměti.

## Kompletní end‑to‑end příklad – shrnutí

Sestavením všech částí dohromady získáte finální program, který můžete zkopírovat a vložit do svého IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Očekávaný výstup:** Po spuštění se v určeném adresáři objeví `PivotCopied.xlsx`. Po otevření v Excelu zobrazí stejný rozvrh kontingenční tabulky, filtry a data jako v `Source.xlsx`. Všechny vypočítané pole a formátování jsou zachovány.

## Často kladené otázky

* **Funguje to se staršími formáty Excelu (.xls)?**  
  Ano. Aspose.Cells automaticky detekuje formát. Použijte `new Workbook("file.xls")` a stejná logika kopírování platí.

* **Co když kontingenční tabulka odkazuje na externí datové zdroje?**  
  Kopie zachová původní odkaz na datový zdroj. Pokud cílové prostředí nemůže tento zdroj dosáhnout, kontingenční tabulka zobrazí chyby `#REF!`. Pro zamezení tomu obnovte kontingenční tabulku po kopírování nebo změňte její datový zdroj pomocí `PivotTable.setDataSource(...)`.

* **Mohu kopírovat kontingenční tabulku na konkrétní název listu?**  
  Samozřejmě. Po vytvoření cílového listu jej přejmenujte:

```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Závěr

Nyní víte, **jak duplikovat kontingenční tabulky** v Javě pomocí Aspose.Cells, **jak kopírovat oblast mezi sešity** a osvědčené postupy pro **načtení Excel sešitu v Javě**. Dodržením pětikrokového procesu – načtení, definice, vytvoření cíle, kopírování a uložení – můžete automatizovat generování reportů, archivovat analýzy nebo rozdělit složité sešity, aniž byste ztratili funkčnost kontingenčních tabulek.

Dále prozkoumejte související témata, jako je **kopírování kontingenční tabulky do sešitu** s více listy, nebo integrujte duplikovanou kontingenční tabulku do většího datového zpracovatelského řetězce pomocí Apache POI pro scénáře mimo Aspose. Experimentujte s různými nastaveními `CopyOptions`, abyste doladili výkon pro obrovské sešity.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Komplexní průvodce](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak aktualizovat zdroj kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Komplexní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Skupinování polí kontingenční tabulky v Excel sešitech pomocí Aspose.Cells pro Java – Komplexní průvodce](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}