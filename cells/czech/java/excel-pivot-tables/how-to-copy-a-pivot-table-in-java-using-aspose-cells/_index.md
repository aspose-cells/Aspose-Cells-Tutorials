---
category: general
date: 2026-09-27
description: Kopírování kontingenční tabulky v Javě s Aspose.Cells – krok za krokem
  průvodce, který ukazuje, jak zkopírovat oblast a zachovat definice kontingenční
  tabulky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: cs
lastmod: 2026-09-27
og_description: Zkopírujte kontingenční tabulku v Javě pomocí Aspose.Cells. Sledujte
  tento kompletní návod, jak zkopírovat oblast v Aspose.Cells a zachovat definice
  kontingenční tabulky beze změny.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Zkopírujte kontingenční tabulku v Javě – rychlý průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells
url: /cs/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells

Pokud potřebujete **copy pivot table** z jednoho sešitu do druhého, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells pro Javu. Řešení funguje pro jakýkoli kontingenční tabulku, kterou jste vytvořili, a zachovává definici kontingenční tabulky bez ručního přetvoření.

Naučíte se, jak načíst zdrojový soubor, definovat oblast, která obsahuje kontingenční tabulku, zkopírovat tuto oblast do nového sešitu a nakonec výsledek uložit. Tutoriál také pokrývá běžné úskalí, jako je zachování zdrojových dat a práce s velkými sešity.

## Co budete potřebovat

* Java 17 nebo novější (kód se také kompiluje s JDK 8+)
* Aspose.Cells for Java 23.9 nebo novější – nejnovější verze nabízí nejspolehlivější podporu **copy range aspose cells**
* Zdrojový soubor Excel, který obsahuje kontingenční tabulku (např. `SourceWithPivot.xlsx`)
* IDE nebo nástroj pro sestavení (Maven/Gradle), který může odkazovat na Aspose.Cells JAR

## Krok 1: Načtěte zdrojový sešit, který obsahuje kontingenční tabulku

Prvním krokem je otevřít sešit, který obsahuje kontingenční tabulku, kterou chcete duplikovat. Načtení souboru vytvoří v‑paměti reprezentaci všech listů, buněk a mezipamětí kontingenčních tabulek.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Proč je to důležité:**  
Aspose.Cells načte celý sešit, včetně skrytých listů mezipaměti kontingenčních tabulek. Pokud tento krok přeskočíte, následná operace **copy pivot table** ztratí podkladový zdroj dat.

## Krok 2: Vytvořte prázdný cílový sešit

Dále vytvořte nový sešit, který přijme zkopírovanou kontingenční tabulku. Začátek s čistým sešitem zabraňuje nechtěnému přepsání.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tip:** Výchozí sešit obsahuje jeden prázdný list, což je ideální pro jednoduché kopírování. Pokud potřebujete kopírovat do konkrétního názvu listu, přejmenujte `destWs` pomocí `destWs.setName("TargetSheet")`.

## Krok 3: Definujte zdrojovou oblast, která zahrnuje kontingenční tabulku

Kontingenční tabulka zabírá obdélníkový blok buněk. Musíte zadat přesnou oblast; jinak bude zkopírována jen surová data. V tomto příkladu předpokládáme, že kontingenční tabulka zabírá **A1:G20**, ale můžete adresu upravit podle svého souboru.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Proč to funguje:**  
Když zavoláte `createRange` na kolekci `Cells` listu, Aspose.Cells zahrne definici kontingenční tabulky, její mezipaměť a veškeré formátování. Toto je jádro **how to copy pivot table** správně.

## Krok 4: Zkopírujte definovanou oblast do cílového listu

Nyní použijte metodu `copy` k duplikaci oblasti. Metoda zkopíruje vše uvnitř oblasti, včetně definice kontingenční tabulky, vzorců a stylů.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Důležitá poznámka:**  
Pokud potřebujete jen data bez kontingenční tabulky, můžete použít `srcRange.copyData`. Pro skutečnou **copy pivot table** však musíte zkopírovat celou oblast, jak je uvedeno výše.

## Krok 5: Uložte cílový sešit

Nakonec zapište nový sešit na disk. Výsledný soubor bude obsahovat plně funkční kontingenční tabulku identickou se zdrojem.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Spuštěním programu vznikne `CopyPivotResult.xlsx` se stejným rozložením kontingenční tabulky, filtry a výpočty jako v původním souboru.

## Očekávaný výstup

Když otevřete `CopyPivotResult.xlsx` v Excelu:

* Kontingenční tabulka se zobrazí v **A1:G20** na prvním listu.
* Všechna pole řádků/sloupců, filtry a hodnotová pole jsou zachována.
* Aktualizace kontingenční tabulky obnoví stejný zdroj dat jako zdrojový sešit (pokud jsou zdrojová data vložena).

## Okrajové případy a praktické tipy

| Situace | Jak to řešit |
|-----------|------------------|
| **Kontingenční tabulka zasahuje do více sloupců, než se očekávalo** | Použijte `srcWs.getPivotTables().get(0).getPivotTableArea()` k získání přesné adresy programově. |
| **Zdrojový sešit obsahuje více kontingenčních tabulek** | Procházejte `srcWs.getPivotTables()` a zkopírujte každou oblast samostatně, přičemž upravíte cílové adresy. |
| **Velké sešity způsobují tlak na paměť** | Povolte `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` před načtením zdroje. |
| **Potřebujete zkopírovat jen definici kontingenční tabulky, ne data** | Po kopírování odstraňte řádky se zdrojovými daty v cíli pomocí `destWs.getCells().deleteRows(startRow, count)`. |
| **Cílový soubor musí zachovat původní formátování** | Nastavte `CopyOptions` s `options.setPasteType(PasteType.ALL)` pro plnohodnotné kopírování. |

**Pro tip:** Vždy ověřte zkopírovanou kontingenční tabulku voláním `destWs.getPivotTables().get(0).refresh()` programově. Tím zajistíte, že mezipaměť je aktuální, zejména pokud jsou zdrojová data v externím připojení.

## Kompletní spustitelný příklad

Níže je celý program, který můžete zkopírovat a vložit do svého IDE. Nahraďte `YOUR_DIRECTORY` skutečnou cestou na vašem počítači.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Spuštěním tohoto kódu **copy pivot table** přesně podle popisu, a ukazuje nejjednodušší způsob, jak **copy range aspose cells** při zachování funkčnosti kontingenční tabulky.

## Závěr

Nyní víte, jak **copy pivot table** v Javě pomocí Aspose.Cells, od načtení zdrojového sešitu až po uložení cílového souboru. Průvodce pokryl nezbytné kroky, vysvětlil, proč je každý krok důležitý, a zabýval se běžnými okrajovými případy.

Dále můžete zkoumat:

* **how to copy pivot table** napříč různými listy ve stejném sešitu
* Použití **copy range aspose cells** ke kopírování grafů nebo podmíněného formátování
* Automatizace aktualizace kontingenční tabulky po kopírování pro udržení aktuálnosti dat

Neváhejte experimentovat s většími oblastmi, více kontingenčními tabulkami nebo integrovat tuto logiku do rozsáhlejšího zpracování Excelu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}