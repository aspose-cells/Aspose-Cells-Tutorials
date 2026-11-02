---
category: general
date: 2026-08-04
description: jak použít wrapcols s kompletním příkladem v Javě, přetvořit pole v Excelu
  a uložit sešit do souboru pomocí Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: cs
lastmod: 2026-08-04
og_description: jak použít wrapcols k přetvoření pole v Excelu pomocí Javy. Naučte
  se kompletní příklad excel wrapcols, vytvořte excelový sešit v Javě a uložte sešit
  do souboru.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: Jak používat wrapcols v Javě – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: jak použít wrapcols v Javě – přetvořit pole v Excelu
url: /cs/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít wrapcols v Javě – přetvořit pole v Excelu

Pokud potřebujete **how to use wrapcols** převést plochý seznam hodnot na víceřádkový rozsah, tento průvodce vám ukáže přesné kroky. Uvidíte **excel wrapcols example**, který přetvoří 1‑D pole na blok 3 řádky × 2 sloupce, a naučíte se, jak **save workbook to file** s Aspose.Cells.

Na konci tohoto tutoriálu budete schopni vytvořit kód **create excel workbook java**, který:

* Inicializuje nový sešit a vybere buňku A1.  
* Použije funkci `WRAPCOLS` k přetvoření dat.  
* Vynutí výpočet vzorce, aby se výsledek zobrazil okamžitě.  
* Načte hodnotu z vypočteného pole.  
* Uloží sešit na disk.

Jedinou podmínkou je vývojové prostředí Java (JDK 8 nebo novější) a knihovna Aspose.Cells pro Java.

---

## Požadavky

* JDK 8 + (nebo jakákoli novější verze).  
* Maven nebo Gradle pro správu závislosti Aspose.Cells.  
* Základní znalost syntaxe Javy a Excelových vzorců.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Pokud používáte Gradle, nahraďte XML úryvek odpovídajícím řádkem `implementation`.

---

## Krok 1: Vytvořit Excel sešit v Javě

Prvním krokem je **create excel workbook java** kód, který otevře nový sešit a získá první list a buňku A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

Vytvoření sešitu tímto způsobem vám poskytne čistý start, což zajišťuje, že příklad funguje na jakémkoli počítači bez existujícího souboru.

---

## Krok 2: Použít funkci WRAPCOLS – příklad excel wrapcols

`WRAPCOLS` přijímá jednorozměrné pole a počet sloupců, poté vrací rozsah, který nejprve vyplňuje řádky. To je jádro **reshape array in excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

Proč to funguje:

* Literální pole `{1,2,3,4,5,6}` poskytuje šest čísel.  
* `WRAPCOLS(..., 2)` říká Excelu, aby hodnoty zabalil do 2 sloupců a automaticky vytvořil dostatek řádků (v tomto případě 3) pro všechny položky.  
* Výsledný rozsah zabírá buňky **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## Krok 3: Vynutit výpočet, aby sešit odrážel ve vzorci

Aspose.Cells nevyhodnocuje vzorce automaticky při jejich nastavení. Musíte zavolat `calculateFormula()`, aby se výsledek materializoval.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

Volání této metody zajistí, že pole vytvořené pomocí `WRAPCOLS` bude zapsáno do buněk, což vám umožní okamžitě číst hodnoty.

---

## Krok 4: Načíst hodnotu z přetvořeného pole

Abychom dokázali, že vzorec funguje, přečtěte řetězcovou reprezentaci cílové buňky. Protože `WRAPCOLS` vrací pole, Excel v buňce, kde je vzorec, zobrazí **první prvek** (hodnota `1`).

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**Očekávaný výstup v konzoli**

```
First element: 1
```

Pokud si prohlédnete list v Excelu, uvidíte celý blok 3 × 2 vyplněný, jak bylo popsáno výše.

---

## Krok 5: Uložit sešit do souboru – jak uložit sešit do souboru

Uložení sešitu vám umožní jej později otevřít v Excelu nebo sdílet s kolegy. Použijte metodu `save` s úplnou cestou.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Spuštěním programu se v pracovním adresáři vytvoří `WrapFunctions.xlsx`. Otevřením souboru se zobrazí přetvořené pole v buňkách A1:B3, což potvrzuje úspěšné **save workbook to file**.

---

## Kompletní, spustitelný příklad

Spojením všech částí dohromady zde máte kompletní program, který můžete zkopírovat a vložit do IDE a spustit:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**Ověření výsledku**

1. Konzole vypíše `First element: 1`.  
2. Vygenerovaný `WrapFunctions.xlsx` obsahuje:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Pokud potřebujete odkazovat na pole jinde, můžete například přečíst libovolnou vyplněnou buňku pomocí `worksheet.getCells().get("B2").getIntValue()`.

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Může WRAPCOLS zpracovat nenumerické pole?* | Ano. Můžete předat řetězce, data nebo logické hodnoty uvnitř složených závorek a Excel je podle toho zabalí. |
| *Co když potřebuji více řádků, než Excel může zobrazit?* | WRAPCOLS bude pokračovat v rozšiřování do dalších řádků, dokud není zdrojové pole vyčerpáno. Ujistěte se, že list má dostatek řádků (výchozí limit je 1 048 576). |
| *Jak změním počet sloupců?* | Upravte druhý argument funkce `WRAPCOLS`. Pro tři sloupce použijte `=WRAPCOLS({1,2,3,4,5,6}, 3)`, což vytvoří blok 2 × 3. |
| *Je možné zapsat výsledek do jiné počáteční buňky?* | Ano. Nastavte vzorec na libovolnou buňku (např. `C5`) a zabalený rozsah se rozšíří relativně k této buňce. |
| *Musím volat `calculateFormula` pokaždé, když změníme vzorec?* | Kdykoli programově upravíte vzorec, zavolejte `calculateFormula` nebo `calculateFormula(true)`, aby se obnovily závislé buňky. |

---

## Závěr

Tento tutoriál ukázal **how to use wrapcols** v Javě k **reshape array in excel**, poskytl jasný **excel wrapcols example** a ukázal správný způsob, jak **save workbook to file**. Nyní máte pevný základ pro projekty **create excel workbook java**, které potřebují dynamické transformace polí.

Dále prozkoumejte související témata, jako je **using other array functions** (`TRANSPOSE`, `SEQUENCE`) nebo **writing large data sets** s streaming API Aspose.Cells. Experimentujte s různými zdrojovými poli, počty sloupců a počátečními pozicemi, abyste přizpůsobili vzor svým vlastním reportovacím nebo datovým procesům. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak otevřít Excel soubor pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [Jak vytvořit a sloučit Excel sešity pomocí Aspose.Cells pro Java | Kompletní průvodce](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [Jak renderovat listy Excelu jako obrázky pomocí Aspose.Cells pro Java (Operace sešitu)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}