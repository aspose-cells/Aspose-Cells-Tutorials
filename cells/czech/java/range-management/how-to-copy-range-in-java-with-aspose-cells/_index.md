---
category: general
date: 2026-09-08
description: Jak kopírovat oblast v Javě pomocí Aspose.Cells – naučte se kopírovat
  kontingenční tabulku, duplikovat kontingenční tabulku a exportovat kontingenční
  tabulku při zachování formátování.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: cs
lastmod: 2026-09-08
og_description: Jak kopírovat oblast v Javě pomocí Aspose.Cells. Tento tutoriál vám
  ukáže, jak kopírovat kontingenční tabulku, duplikovat kontingenční tabulku a exportovat
  kontingenční tabulku při zachování formátování.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Jak zkopírovat rozsah v Javě – kompletní průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak zkopírovat rozsah v Javě pomocí Aspose.Cells
url: /cs/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat oblast v Javě s Aspose.Cells

Pokud potřebujete **jak zkopírovat oblast** v Javě, Aspose.Cells úkol zjednodušuje. Ať už přesouváte běžný blok buněk nebo plnohodnotnou kontingenční tabulku, knihovna provádí operaci kopírování a zachovává vzorce, styly i mezipaměť kontingenční tabulky. V tomto průvodci se naučíte **kopírovat kontingenční tabulku**, **duplikovat kontingenční tabulku** a dokonce **exportovat kontingenční tabulku** do nového sešitu s kompletním formátováním.

Tutoriál pokrývá vše od nastavení projektu až po poslední ověřovací krok, takže můžete kód spustit ihned po přečtení. Kromě JAR souboru Aspose.Cells pro Javu nejsou potřeba žádné externí nástroje.

## Požadavky

- Java 17 (nebo jakýkoli podporovaný JDK) nainstalovaná a nakonfigurovaná ve vašem IDE.
- Maven nebo Gradle pro správu závislostí (příklady používají Maven).
- Zdrojový Excel soubor (`source.xlsx`) obsahující kontingenční tabulku v rozsahu `A1:H20`.
- Základní znalost programování v Javě.

## Krok 1: Přidání Aspose.Cells do vašeho projektu

Aspose.Cells je komerční knihovna, ale je k dispozici bezplatná evaluační verze. Přidejte závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Tip:** Pokud dáváte přednost Gradlu, ekvivalentní zápis je:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Přidání JAR souboru vám poskytne přístup ke třídám `Workbook`, `Worksheet`, `Range` a `CopyOptions`, které jsou v tomto průvodci používány.

## Krok 2: Načtení zdrojového sešitu a výběr první listu

Prvním krokem **jak zkopírovat oblast** je otevřít sešit, který obsahuje data, jež chcete přesunout.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Proč je to důležité:** Otevření sešitu vytvoří v‑paměti reprezentaci, kterou API může manipulovat, aniž by se dotýkalo původního souboru na disku.

## Krok 3: Definování rozsahu, který obsahuje kontingenční tabulku

Kontingenční tabulka se nachází uvnitř obdélníkového bloku. Musíte tento blok specifikovat, aby Aspose.Cells vědělo, co má kopírovat.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Poznámka:** Metoda `createRange` **ne**kopíruje nic; pouze vytváří objekt `Range`, který ukazuje na buňky, jež chcete duplikovat.

## Krok 4: Vytvoření nového sešitu a získání jeho prvního listu

Nyní vytvořte cílový sešit, ve kterém bude zkopírovaný rozsah umístěn.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Proč nový sešit?** Použití nového souboru zaručuje, že žádné skryté styly nebo pojmenované rozsahy nebudou zasahovat do operace kopírování, což je zvláště důležité, když **exportujete kontingenční tabulku** do samostatného souboru.

## Krok 5: Zkopírování rozsahu (včetně kontingenční tabulky) do cílového listu

Toto je jádro **jak zkopírovat oblast s formátováním**. Objekt `CopyOptions` říká Aspose.Cells, aby zachovalo vše: hodnoty, vzorce, styly a mezipaměť kontingenční tabulky.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Kopírovat kontingenční tabulku:** Protože zdrojový rozsah zahrnuje kontingenční tabulku, API automaticky duplikuje mezipaměť kontingenční tabulky, takže nový list obsahuje plně funkční kontingenční tabulku, která se chová přesně jako originál.

## Krok 6: Uložení cílového sešitu

Nakonec výsledek zapíšete na disk.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Když otevřete `dest.xlsx`, uvidíte přesnou repliku původní kontingenční tabulky, včetně jejího formátování, filtrů a vypočtených polí.

## Očekávaný výstup

- `dest.xlsx` obsahuje list pojmenovaný **Sheet1**.
- Buňky `A1:H20` obsahují stejná data a kontingenční tabulku jako zdroj.
- Všechny styly buněk (písma, barvy, ohraničení) jsou zachovány.
- Kontingenční tabulka je plně interaktivní; její obnovení odráží podkladová data ve zkopírovaném rozsahu.

## Jak zkopírovat oblast s formátováním – podrobnější pohled

Předchozí příklad ukazuje nejjednodušší scénář, ale můžete narazit na varianty, které vyžadují mírně odlišný přístup.

### Kopírování kontingenční tabulky do existujícího sešitu

Pokud potřebujete **duplikovat kontingenční tabulku** v sešitu, který již obsahuje data, použijte stejný volání `copyRange`, ale nasměrujte jej na jinou cílovou adresu:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Exportovat pouze kontingenční tabulku (bez okolních dat)

Někdy chcete jen kontingenční tabulku, ne zdrojová data. Identifikujte zobrazovací rozsah kontingenční tabulky pomocí její metody `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Zachování podmíněného formátování

Pravidla podmíněného formátování jsou součástí kolekce stylů. Příznak `PasteType.ALL` je již kopíruje, ale můžete být explicitní:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Okrajové případy a řešení problémů

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|-------------------|-----------------|
| Zdrojové a cílové sešity používají různé verze Excelu | Některé novější funkce kontingenční tabulky (např. datový model) se nemusí správně zobrazit | Použijte nejnovější verzi Aspose.Cells a nastavte `Workbook.setFileFormatType(FileFormatType.XLSX)` pro oba sešity |
| Velmi velké kontingenční tabulky ( > 10 000 řádků) způsobují tlak na paměť | Chyby nedostatku paměti během kopírování | Povolte `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` před načtením |
| Cílový list již obsahuje pojmenovaný rozsah se stejným názvem jako zdroj | Kolize názvů vede k selhání `CopyOptions` | Zavolejte `copyOptions.setIgnoreNameConflicts(true)` |

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do třídy Java. Obsahuje všechny importy, ošetření chyb a komentáře.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Spusťte program a poté otevřete `dest.xlsx`, abyste ověřili, že kontingenční tabulka funguje přesně jako originál.

## Závěr

Nyní víte **jak zkopírovat oblast** v Javě pomocí Aspose.Cells, včetně toho, jak **kopírovat kontingenční tabulku**, **duplikovat kontingenční tabulku** a **exportovat kontingenční tabulku** při zachování veškerého formátování. Knihovna abstrahuje nízkoúrovňové detaily XML struktury Excelu, což vám umožní soustředit se na obchodní logiku.

### Další kroky

- Prozkoumejte **kopírování oblasti s formátováním** pro grafy a obrázky (použijte `PasteType.PICTURES`).
- Automatizujte dávkové zpracování: procházejte více zdrojových souborů a konsolidujte jejich kontingenční tabulky do souhrnného sešitu.
- Kombinujte tuto techniku s Aspose.Slides pro generování PowerPoint reportů, které vkládají zkopírovanou kontingenční tabulku

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak aktualizovat zdroj kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: komplexní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimalizace načítání kontingenční tabulky v Javě pomocí Aspose.Cells – komplexní průvodce](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Jak zkopírovat kontingenční tabulku v C# – převod Excelu na PPTX, kopírování oblasti a vytvoření textového pole](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}