---
category: general
date: 2026-09-11
description: Vytvořte nový list a zkopírujte oblast v Excelu pomocí Aspose.Cells.
  Naučte se, jak kopírovat oblast mezi listy při zachování kontingenčních tabulek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: cs
lastmod: 2026-09-11
og_description: Vytvořte nový list a zkopírujte oblast v Excelu pomocí Aspose.Cells.
  Tento tutoriál ukazuje přesné kroky, jak zkopírovat oblast mezi listy a zachovat
  kontingenční tabulky nedotčené.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Vytvořte nový list a zkopírujte oblast v Excelu – průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Vytvořte nový list a zkopírujte oblast v Excelu pomocí Aspose.Cells
url: /cs/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte nový list a zkopírujte oblast Excelu pomocí Aspose.Cells

Pokud potřebujete **vytvořit nový list** a přesouvat data v souboru Excel, Aspose.Cells to usnadňuje. Tento průvodce ukazuje přesně, jak zkopírovat oblast Excelu z jednoho listu do druhého při zachování všech kontingenčních tabulek v oblasti.

Naučíte se, jak **zkopírovat oblast Excelu**, jak **zkopírovat oblast mezi listy**, a proč metoda `copy` v Aspose.Cells zachovává definice kontingenčních tabulek. Není potřeba žádné externí nástroje – stačí Java projekt s knihovnou Aspose.Cells.

## Požadavky

- Java 17 nebo novější nainstalováno
- Aspose.Cells pro Java (verze 23.12 nebo novější) přidáno do classpath vašeho projektu
- Zdrojová sešit (`input.xlsx`) obsahující kontingenční tabulku v oblasti, kterou chcete zkopírovat
- Základní znalost syntaxe Java a správy závislostí Maven/Gradle

## Krok 1: Nastavte projekt a importujte Aspose.Cells

Vytvořte jednoduchý Maven projekt (nebo Gradle, pokud dáváte přednost) a přidejte závislost Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Poté importujte požadované třídy ve vašem Java souboru:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Proč je tento krok důležitý*: Importování správných tříd vám poskytuje přístup k `Workbook`, `Worksheet`, `Range` a metodě `copy`, která provede přenos oblasti.

## Krok 2: Načtěte zdrojový sešit

Otevřete sešit, který obsahuje data, jež chcete zkopírovat. Následující kód načte `input.xlsx` z adresáře, který zadáte:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Vysvětlení*: `Workbook` představuje celý soubor Excel. Jednorázové načtení vám poskytuje přístup pro čtení i zápis ke všem listům a kolekcím buněk.

## Krok 3: Identifikujte zdrojovou oblast, která obsahuje kontingenční tabulku

Vyberte list, který obsahuje kontingenční tabulku, a definujte přesný blok buněk, který chcete zkopírovat. V tomto příkladu kopírujeme buňky A1 až D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Proč je to důležité*: Vytvořením objektu `Range` řeknete Aspose.Cells přesně, které buňky (včetně vložených objektů, jako jsou kontingenční tabulky) mají být duplikovány.

## Krok 4: **Vytvořte nový list**, který přijme zkopírovaná data

Nyní přidáme nový list do stejného sešitu. Toto je místo, kde se objeví hlavní klíčové slovo:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Vysvětlení*: Přidání nového listu izoluje zkopírovaná data, což usnadňuje ověření, že operace **zkopírovat oblast Excelu** byla úspěšná, aniž by ovlivnila původní list.

## Krok 5: Zkopírujte oblast – kontingenční tabulka je automaticky zachována

Použijte metodu `copy` k přesunu oblasti ze zdrojového listu do cílového listu. Aspose.Cells kopíruje vzorce, formátování a definice kontingenčních tabulek:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Proč to funguje*: Metoda `copy` provádí hlubokou kopii zdrojových buněk. Nekopíruje jen hodnoty; replikuje celou strukturu buněk, včetně pivot cache. Proto můžete **zkopírovat oblast aspose.cells** a stále vidět funkční kontingenční tabulku na novém listu.

## Krok 6: Uložte sešit s novým listem

Nakonec zapište upravený sešit na disk:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Výsledek*: `output.xlsx` nyní obsahuje původní list plus nový list nazvaný **Copy**, který obsahuje přesně stejnou oblast, včetně kontingenční tabulky.

## Kompletní funkční příklad

Spojením všech částí dohromady získáte kompletní, spustitelný program:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Očekávaný výstup**: Otevřete `output.xlsx` v Excelu. Uvidíte list pojmenovaný **Copy**, jehož buňky A1:D20 obsahují stejná data, formátování a aktivní kontingenční tabulku identickou s originálem.

## Časté otázky a okrajové případy

- **Co když zdrojová oblast obsahuje sloučené buňky?**  
  Metoda `copy` také kopíruje informace o sloučení, takže sloučené buňky zůstávají nezměněny na cílovém listu.

- **Mohu kopírovat do jiného sešitu?**  
  Ano. Načtěte druhou instanci `Workbook`, vytvořte cílovou oblast v tomto sešitu a zavolejte `sourceRange.copy(destinationRange)`. Metoda automaticky zvládá kopírování mezi sešity.

- **Co když cílový list již obsahuje data?**  
  Operace kopírování přepíše všechny existující buňky, které se překrývají s cílovou oblastí. Aby nedošlo ke ztrátě dat, ujistěte se, že cílová oblast je prázdná, nebo použijte jinou počáteční buňku (např. `"B2"`).

- **Je pivot cache duplikována?**  
  Aspose.Cells znovu používá původní pivot cache, což znamená, že nová kontingenční tabulka zůstává propojena se stejnými zdrojovými daty. Pokud potřebujete nezávislou cache, musíte po kopírování kontingenční tabulku znovu vytvořit.

## Tipy a osvědčené postupy

- **Pro tip**: Použijte `Workbook.setForceFormulaRecalculation(true)` před uložením, pokud vaše oblast obsahuje vzorce, které závisí na datech mimo zkopírovaný blok.
- **Dejte si pozor na** velké oblasti: kopírování obrovských listů může spotřebovat značné množství paměti. Zvažte kopírování v menších částech, pokud narazíte na `OutOfMemoryError`.
- **Tip pro výkon**: Vypněte aktualizaci obrazovky (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) při práci s velmi velkými soubory, aby se proces kopírování urychlil.

## Závěr

Nyní víte, jak **vytvořit nový list** a **zkopírovat oblast Excelu** mezi listy pomocí Aspose.Cells, přičemž zachováte kontingenční tabulky a všechny atributy buněk. Tato technika vám umožní programově duplikovat datové bloky, vytvářet šablony reportů nebo přestrukturovat sešity bez ručního kopírování a vkládání.

Dále prozkoumejte související témata, jako je **zkopírovat oblast aspose.cells** pro operace mezi sešity, automatizaci aktualizací kontingenčních tabulek nebo export zkopírovaného listu do PDF. Experimentujte s různými zdrojovými oblastmi a názvy listů, aby vyhovovaly vašemu konkrétnímu scénáři automatizace. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}