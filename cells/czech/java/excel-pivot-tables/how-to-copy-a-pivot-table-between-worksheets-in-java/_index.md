---
category: general
date: 2026-10-16
description: Jak zkopírovat kontingenční tabulku v Javě s Aspose.Cells – naučte se
  kopírovat oblast do jiného listu a efektivně kopírovat oblast mezi listy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: cs
lastmod: 2026-10-16
og_description: Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells. Tento
  tutoriál vám ukáže, jak zkopírovat oblast do jiného listu a jak zkopírovat oblast
  mezi listy s kompletním kódem.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Jak zkopírovat kontingenční tabulku mezi listy v Javě – průvodce krok za
  krokem
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Jak zkopírovat kontingenční tabulku mezi listy v Javě
url: /cs/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku mezi listy v Javě

Pokud potřebujete **jak zkopírovat kontingenční tabulku** z jednoho listu do druhého ve stejném sešitu, tento průvodce poskytuje kompletní, připravené řešení. Uvidíte, jak zkopírovat zdrojový rozsah, který obsahuje kontingenční tabulku, zachovat její funkčnost a ověřit výsledek — vše pomocí Aspose.Cells pro Java.

Kopírování kontingenční tabulky je běžný úkol při programovém generování reportů a jeho správné provedení zabraňuje ztrátě pivot cache nebo poškození vzorců. Na konci tohoto tutoriálu budete schopni **kopírovat rozsah do jiného listu** a **kopírovat rozsah mezi listy** bez jakýchkoli ručních kroků.

## Co se naučíte

* Načíst existující soubor Excel s kontingenční tabulkou.
* Definovat zdrojový rozsah, který obsahuje kontingenční tabulku.
* Definovat cílový rozsah na jiném listu.
* Použít `CopyOptions` k zachování kontingenční tabulky.
* Ověřit, že zkopírovaná kontingenční tabulka funguje podle očekávání.

**Požadavky**

* Java 17 nebo novější.
* Aspose.Cells pro Java (verze 23.12 nebo novější).  
* Soubor Excel (`input.xlsx`) obsahující kontingenční tabulku na prvním listu.

---

## Jak zkopírovat kontingenční tabulku pomocí Aspose.Cells

Jádrem operace je čtyřkrokový proces: načíst sešit, najít zdrojový rozsah, nastavit cílový rozsah a provést kopírování. Níže je každý krok podrobně vysvětlen.

### Krok 1: Načíst sešit

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Proč tento krok?*  
Načtení sešitu načte celý soubor do paměti, což vám poskytne přístup k listům, buňkám a pivot cache. Aspose.Cells automaticky čte formát souboru, takže se nemusíte starat o rozdíl mezi `.xls` a `.xlsx`.

### Krok 2: Najít zdrojový rozsah, který obsahuje kontingenční tabulku

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Proč tento krok?*  
Kontingenční tabulka je uložena v bloku buněk, který také odkazuje na skrytou cache. Výběrem přesného rozsahu (`A1:G20` v tomto příkladu) zajistíte, že cache zůstane propojena při kopírování rozsahu.

### Krok 3: Definovat cílový rozsah na jiném listu

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Proč tento krok?*  
Výběr cíle na jiném listu vám umožní **kopírovat rozsah do jiného listu**. Buňka v levém horním rohu (`A1`) je běžný výchozí bod, ale můžete ji umístit kamkoli změnou adresy.

### Krok 4: Zkopírovat zdrojový rozsah při zachování kontingenční tabulky

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Proč tento krok?*  
`CopyOptions` řídí, co se přenáší. Použití `PasteType.PASTE_ALL` zaručuje, že kontingenční tabulka, její formátování a podkladové vzorce jsou duplikovány. Bez těchto možností se mohou zkopírovat jen surové hodnoty, což naruší funkčnost kontingenční tabulky.

### Krok 5: Uložit sešit a ověřit výsledek

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Otevřete `output.xlsx` v Excelu a potvrďte, že:

* Druhý list obsahuje plně funkční kontingenční tabulku identickou s originálem.
* Obnovení kontingenční tabulky aktualizuje data, což dokazuje, že cache je neporušená.

---

## Kopírovat rozsah do jiného listu pomocí Javy

Pokud je vaším cílem jednoduše **kopírovat rozsah do jiného listu** bez kontingenční tabulky, stejný kód funguje i s běžným rozsahem buněk. Jedinou změnou je adresa zdroje. Konfigurace `CopyOptions` zůstává stejná, což zajišťuje zachování vzorců a formátování.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Tento úryvek demonstruje flexibilitu API pro scénáře s kontingenční tabulkou i bez ní.

---

## Kopírovat rozsah mezi listy bez ztráty vzorců

Když **kopírujete rozsah mezi listy**, vzorce odkazující na jiné listy se mohou rozbít, pokud se změní relativní odkazy. Aby se tomu předešlo:

1. Použijte `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`, pokud potřebujete jen vzorce.
2. Uchovejte cílový list ve stejném sešitu, aby interní odkazy zůstaly platné.
3. Po kopírování zavolejte `workbook.calculateFormula();`, aby se vynutila přepočet.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Tyto dodatečné kroky zajišťují, že zkopírovaný rozsah se chová přesně jako originál, i když se rozprostírá na více listech.

---

## Profesionální tipy a běžné úskalí

| Situace | Tip |
|-----------|-----|
| **Pivot cache se neaktualizuje** | Po kopírování zavolejte `destSheet.getPivotTables().get(0).refresh();`, aby se cache aktualizovala. |
| **Kopírování do jiného sešitu** | Použijte `Workbook destWorkbook = new Workbook();` a poté `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Nezapomeňte v případě potřeby zkopírovat pivot cache samostatně. |
| **Velké kontingenční tabulky** | Zvyšte velikost haldy Java (`-Xmx2g`), aby nedošlo k `OutOfMemoryError` během kopírování. |
| **Zachování stylů** | Nastavte `copyOptions.setPasteType(PasteType.PASTE_ALL)`; jinak se kopírují jen hodnoty. |

---

## Očekávaný výstup

Spuštěním celého programu se vytvoří `output.xlsx`. Po otevření v Excelu:

* **Sheet2!A1:G20** zobrazuje stejnou kontingenční tabulku jako **Sheet1!A1:G20**.
* Seznam polí kontingenční tabulky, řádkové/sloupcové štítky a datové hodnoty odpovídají zdroji.
* Obnovení kontingenční tabulky aktualizuje čísla, což potvrzuje funkčnost cache.

Konzole vypíše:

```
Pivot table copied successfully.
```

---

## Závěr

V tomto tutoriálu jste se naučili **jak zkopírovat kontingenční tabulku** z jednoho listu do druhého pomocí Aspose.Cells pro Java. Načtením sešitu, výběrem správného zdrojového rozsahu, definováním cíle a konfigurací `CopyOptions` můžete spolehlivě **kopírovat rozsah do jiného listu** a **kopírovat rozsah mezi listy**, přičemž zachováte veškerou funkčnost kontingenční tabulky.  

Dále můžete zkoumat:

* Export zkopírované kontingenční tabulky do PDF nebo HTML.
* Automatizaci obnovení kontingenčních tabulek napříč více sešity.
* Použití `CopyOptions` k kopírování jen konkrétních prvků (např. hodnot, formátů).

Neváhejte experimentovat s různými adresami rozsahů, strukturami sešitů nebo dokonce s kopiemi mezi sešity. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copy Pivot Table Excel – Step‑by‑Step Guide Using Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}