---
category: general
date: 2026-08-08
description: Jak zkopírovat kontingenční tabulku v Aspose.Cells a zkopírovat oblast
  do sešitu pomocí Javy. Naučte se přesné kroky k duplikaci kontingenční tabulky s
  CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: cs
lastmod: 2026-08-08
og_description: Jak zkopírovat kontingenční tabulku v Aspose.Cells a zkopírovat oblast
  do sešitu pomocí Javy. Sledujte tento kompletní průvodce, jak duplikovat kontingenční
  tabulku pomocí CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Jak zkopírovat kontingenční tabulku v Aspose.Cells – zkopírovat oblast do
  sešitu
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Jak zkopírovat kontingenční tabulku v Aspose.Cells – zkopírovat oblast do sešitu
url: /cs/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v Aspose.Cells – kopírovat oblast do sešitu

Pokud potřebujete **jak zkopírovat kontingenční tabulku** v souboru Excel pomocí Aspose.Cells, tento návod vám ukáže přesný postup. Na konci tutoriálu budete schopni **kopírovat oblast do sešitu** při zachování definice kontingenční tabulky.

Příklad používá Java, ale stejné koncepty platí pro jakýkoli .NET jazyk, který pracuje s Aspose.Cells. Není potřeba žádné externí nástroje – stačí knihovna Aspose.Cells pro Java a základní vývojové prostředí.

## Požadavky

* Java Development Kit (JDK) 8 nebo novější.
* Maven nebo Gradle pro správu závislostí (příklad používá Maven).
* Aspose.Cells pro Java 23.9 (nebo nejnovější verze) přidaná do vašeho projektu.
* Vstupní sešit (`input.xlsx`), který obsahuje alespoň jednu kontingenční tabulku na prvním listu.

Mít tyto položky připravené zabraňuje chybám za běhu, když kód přistupuje k sešitu.

## Jak zkopírovat kontingenční tabulku pomocí Aspose.Cells

Tato sekce vás provede každým krokem potřebným k **jak zkopírovat kontingenční tabulku** z jedné části listu na druhou pomocí třídy `CopyOptions`.

### Krok 1: Přidat Aspose.Cells do projektu

Pokud používáte Maven, přidejte následující závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Proč je tento krok důležitý*: Knihovna poskytuje třídy `Workbook`, `CopyOptions` a další, které jsou potřeba pro operace **aspose.cells copy range**. Bez této závislosti kompilátor nemůže tyto typy rozpoznat.

### Krok 2: Načíst zdrojový sešit

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Načtení souboru vytvoří v‑paměti reprezentaci tabulky. Objekt `Workbook` vám poskytuje přístup k listům, buňkám a kontingenčním tabulkám.

### Krok 3: Nastavit možnosti kopírování tak, aby zahrnovaly kontingenční tabulku

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` říká Aspose.Cells, že operace má zachovat metadata kontingenční tabulky. Pokud tento příznak vynecháte, kontingenční tabulka bude převedena na statická data a ztratí svou interaktivitu.

### Krok 4: Zkopírovat požadovanou oblast s kontingenční tabulkou

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Metoda `copyRange` kopíruje buňky, formátování a — díky nastavením v předchozím kroku — všechny kontingenční tabulky, které se překrývají s oblastí. Toto je jádro funkčnosti **kopírovat oblast do sešitu**.

### Krok 5: Uložit upravený sešit

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Uložení zapíše změny do nového souboru (`output.xlsx`). Nyní můžete tento soubor otevřít v Excelu a vidět, že kontingenční tabulka byla přesně zduplikována tam, kam byla oblast zkopírována.

## Kompletní, spustitelný příklad

Připojením všech částí dohromady získáte kompletní program, který můžete zkompilovat a spustit:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Očekávaný výsledek

* `output.xlsx` obsahuje stejná data jako `input.xlsx`.
* Kontingenční tabulka, která původně obsazovala zdrojovou oblast, se objeví v cílových buňkách, plně funkční (filtry, možnost obnovy atd.).
* Veškeré formátování buněk, vzorce a šířky sloupců jsou zachovány, protože `copyRange` kopíruje celý blok buněk.

## Časté otázky a okrajové případy

**Co když cílová oblast překrývá existující kontingenční tabulku?**  
Aspose.Cells přepíše cílové buňky. Aby nedošlo ke ztrátě dat, ujistěte se, že cílová oblast je prázdná, nebo nejprve přesuňte existující kontingenční tabulku.

**Mohu zkopírovat kontingenční tabulku mezi listy?**  
Ano. Použijte `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`, kde `targetSheetIndex` odkazuje na cílový list.

**Kopíruje `setCopyPivotTable(true)` podkladový zdroj dat?**  
Metoda kopíruje pouze odkaz na pivot cache. Pokud jsou zdrojová data ve stejném sešitu, cílová kontingenční tabulka bude odkazovat na stejný cache. Pro duplikaci cache musíte vytvořit nový pivot cache ručně.

**Jak efektivně zkopírovat velkou oblast?**  
Při kopírování velmi velkých oblastí zvažte použití `CopyOptions.setCopyFormula(true)` a `setCopyDataValidation(true)` pouze pokud je to potřeba. Snížením počtu aktivních možností můžete zlepšit výkon.

## Tipy pro spolehlivé používání **aspose.cells copy range**

* **Pro tip:** Vždy po kopírování zavolejte `workbook.calculateFormula()`, pokud oblast obsahuje vzorce závislé na pivot cache.
* **Dejte pozor na:** Skryté listy. `copyRange` funguje pouze na viditelných listech, pokud výslovně neodkazujete na skrytý list podle indexu.
* **Kontrola verze:** Příznak `setCopyPivotTable` je k dispozici od Aspose.Cells 20.9. Ujistěte se, že vaše verze knihovny jej podporuje.

## Závěr

Nyní víte **jak zkopírovat kontingenční tabulku** v Aspose.Cells a jak **kopírovat oblast do sešitu** při zachování plné funkčnosti kontingenční tabulky. Kroky – přidání knihovny, načtení sešitu, nastavení `CopyOptions`, provedení kopírování a uložení – tvoří opakovatelný vzor, který můžete použít i v dalších scénářích kopírování‑vkládání.

Dále prozkoumejte související témata, jako je **aspose.cells copy range** pro grafy, podmíněné formátování a validaci dat. Experimentujte s kopírováním mezi různými formáty souborů (XLSX → XLS), abyste rozšířili své automatizační možnosti. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}