---
category: general
date: 2026-10-26
description: Naučte se, jak zkopírovat kontingenční tabulku do nového sešitu pomocí
  Javy, zachovat formátování a definici kontingenční tabulky při kopírování rozsahu
  Excelu s formátováním pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: cs
lastmod: 2026-10-26
og_description: Zkopírujte kontingenční tabulku do nového sešitu v Javě s Aspose.Cells.
  Tento průvodce ukazuje, jak zkopírovat oblast v Excelu, zachovat formátování a efektivně
  vytvořit prázdný sešit.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Zkopírujte kontingenční tabulku do nového sešitu v Javě – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak zkopírovat kontingenční tabulku do nového sešitu v Javě
url: /cs/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku do nového sešitu v Javě

Pokud potřebujete **copy pivot table** z jednoho souboru Excel do druhého, tento průvodce vám ukáže kompletní, spustitelné řešení. Uvidíte, jak zachovat definici kontingenční tabulky, udržet veškeré formátování a vyhnout se běžným úskalím při kopírování rozsahu v Excelu.

Kopírování kontingenční tabulky často vyvolává otázky jako *how to copy pivot* bez poškození datového zdroje nebo ztráty stylů. Na konci tohoto tutoriálu budete mít samostatný Java program, který vytvoří prázdný sešit, zkopíruje požadovaný rozsah a uloží výsledek s neporušenou kontingenční tabulkou.

## Co dosáhnete

* Načtěte zdrojový sešit, který obsahuje kontingenční tabulku.  
* **Create empty workbook** který přijme zkopírovaná data.  
* **Copy excel range** který zahrnuje kontingenční tabulku, s použitím možností, které zachovají kontingenční tabulku a formátování.  
* Uložte cílový soubor a ověřte, že kontingenční tabulka funguje přesně jako originál.

### Předpoklady

* Java 17 nebo novější.  
* Aspose.Cells for Java (verze 23.10 nebo novější).  
* Základní znalost Java IDE (IntelliJ IDEA, Eclipse, atd.).  

> **Pro tip:** Použijte bezplatnou zkušební licenci Aspose.Cells pro rychlé testování; nahraďte ji plnou licencí před nasazením do produkce.

## Zkopírovat kontingenční tabulku do nového sešitu

Prvním krokem je nastavit zdrojové a cílové sešity. Cíl začíná jako volání **create empty workbook**, což vám poskytne čistý soubor s jedním listem.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Proč to funguje

* `new Workbook()` **creates empty workbook** s výchozím listem, čímž se vyhnete nutnosti mazat existující data.  
* `CopyOptions` říká Aspose.Cells, aby kopíroval metadata **pivot table**, ne jen surové hodnoty. Režim `PASTE_ALL` také přenáší styly buněk, formáty čísel a podmíněné formátování — splňuje požadavek **copy range with formatting**.  
* `copyRange` provádí operaci **copy excel range**, která respektuje interní struktury zdroje, takže kontingenční tabulka zůstane po kopírování funkční.

## Jak zkopírovat kontingenční tabulku bez ztráty formátování

Pokud použijete pouze výchozí `CopyOptions`, některé informace o stylu mohou být ve starších verzích Aspose.Cells vynechány. Výslovné nastavení typu vložení zaručuje, že **copy range with formatting** bude respektováno.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Přidání `setPasteSpecialType` zajišťuje, že šířky sloupců, výšky řádků a dokonce pravidla ověření dat se přenesou spolu s rozsahem. To je zvláště užitečné, když kontingenční tabulka zasahuje do více sloupců s vlastními šířkami.

## Vytvořit prázdný sešit před kopírováním

Někdy se vývojáři pokusí kopírovat do existujícího sešitu, který již obsahuje data. To může způsobit překrývající se rozsahy nebo neočekávané přepsání. Začátek s voláním **create empty workbook** izoluje operaci:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Pokud potřebujete v cíli více než jeden list, můžete je přidat po kopírování:

```java
destWb.getWorksheets().add("Summary");
```

## Kopírovat excel rozsah s formátováním pomocí CopyOptions

Mimo kontingenčních tabulek funguje stejný vzor pro jakýkoli **copy excel range**, který vyžaduje zachování formátování — grafy, tabulky nebo podmíněné formáty.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Instance `CopyOptions` zůstává stejná, takže získáte konzistentní chování napříč různými rozsahy.

### Okrajové případy k úvaze

| Situation                              | Recommended handling |
|----------------------------------------|----------------------|
| Source workbook has multiple pivots   | Copy each pivot’s range separately or copy the whole sheet. |
| Destination already contains data      | Choose a non‑conflicting start cell (e.g., "H1") when calling `copyRange`. |
| Pivot data source is external (e.g., DB) | Ensure the destination workbook points to the same external data source, or refresh the pivot after copy. |
| Large workbook ( > 10 MB )             | Increase Java heap size (`-Xmx2g`) to avoid `OutOfMemoryError`. |

## Ověřte výsledek

Po spuštění programu otevřete `destination.xlsx`. Měli byste vidět:

* Stejný rozvrh kontingenční tabulky jako v `source.xlsx`.  
* Všechny barvy buněk, formáty čísel a šířky sloupců jsou zachovány.  
* Datový zdroj kontingenční tabulky stále ukazuje na původní rozsah dat v novém souboru, takže obnovení kontingenční tabulky aktualizuje hodnoty správně.

Pokud se kontingenční tabulka zobrazí jako statická tabulka, dvojitě zkontrolujte, že je nastaveno `CopyOptions.setPasteType(PasteType.PASTE_ALL)`. Bez této možnosti Aspose.Cells zachází s kontingenční tabulkou jako s obyčejnými daty.

## Závěr

Nyní víte, jak **copy pivot table** do nového sešitu v Javě při zachování formátování, datových spojení a rozvržení listu. Kompletní řešení ukazuje načtení zdrojového souboru, **create empty workbook**, konfiguraci možností **copy excel range** a uložení výsledku.  

Odtud můžete zkoumat související témata, jako je **how to copy pivot** mezi různými listy, vložit grafy vedle kontingenčních tabulek nebo automatizovat hromadné zpracování více sešitů. Experimentujte s nastavením `CopyOptions`, aby vyhovovalo vašim konkrétním potřebám automatizace, a budete mít robustní sadu nástrojů pro manipulaci s Excelem na dosah ruky.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit nový sešit v Javě – Kompletní průvodce kopírováním kontingenční tabulky](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Kopírovat kontingenční tabulku mezi sešity – Krok za krokem Java průvodce](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Jak zkopírovat rozsah a zachovat kontingenční tabulku v Javě](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}