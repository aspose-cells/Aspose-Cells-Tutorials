---
category: general
date: 2026-09-21
description: Naučte se, jak v Javě kopírovat oblast při zachování kontingenční tabulky.
  Tento krok‑za‑krokem průvodce vám ukáže, jak bezpečně exportovat kontingenční tabulku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: cs
lastmod: 2026-09-21
og_description: Jak zkopírovat rozsah v Javě při zachování kontingenční tabulky. Následujte
  tento kompletní průvodce, abyste bezpečně exportovali kontingenční tabulky.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Jak zkopírovat oblast a zachovat kontingenční tabulku v Javě
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Jak zkopírovat oblast a zachovat kontingenční tabulku v Javě
url: /cs/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat oblast a zachovat kontingenční tabulku v Javě

Pokud potřebujete **how to copy range** obsahující kontingenční tabulku, tento průvodce vám ukáže spolehlivý způsob, jak zachovat kontingenční tabulku neporušenou. Mnoho vývojářů má problém se ztrátou kontingenční tabulky při exportu dat, ale níže uvedený přístup vám umožní **copy pivot table** data bez narušení její funkčnosti. Na konci tohoto tutoriálu budete schopni **preserve pivot table** strukturu, **export pivot table** soubory a pochopit **how to preserve pivot** v různých scénářích.

Příklad používá Aspose.Cells pro Java, populární knihovnu pro automatizaci Excelu. Žádné další nástroje nejsou potřeba kromě standardního vývojového prostředí Java.

## Požadavky

* Nainstalovaný Java 17 (nebo novější).
* Maven nebo Gradle pro správu závislostí.
* Aspose.Cells pro Java (verze 23.9 nebo novější). Přidejte následující Maven závislost:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Zdrojový sešit (`Source.xlsx`) obsahující kontingenční tabulku, kterou chcete zkopírovat.

## Jak zkopírovat oblast a zachovat kontingenční tabulku neporušenou

Hlavní myšlenkou je zkopírovat **range**, která obklopuje celou kontingenční tabulku — včetně jejího zdroje dat — pomocí `copyRange`. Tato metoda kopíruje jak surová data, tak definici kontingenční tabulky, čímž zajistí, že cílový sešit získá plně funkční kontingenční tabulku.

### Krok 1: Načtěte zdrojový sešit

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Proč tento krok?*  
Načtení sešitu vám poskytuje přístup k listu, který obsahuje kontingenční tabulku. Třída `Workbook` abstrahuje celý soubor Excel, zatímco `Worksheet` poskytuje operace na úrovni buněk.

### Krok 2: Definujte oblast, která zahrnuje kontingenční tabulku

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Proč tento krok?*  
Kontingenční tabulka není jediná buňka; rozprostírá se přes blok, který zahrnuje záhlaví, řádky s daty a cache kontingenční tabulky. Zadáním oblasti, která plně obsahuje kontingenční tabulku, zajistíte, že `copyRange` také zkopíruje podkladovou cache, což je nezbytné pro chování **preserve pivot table**.

### Krok 3: Vytvořte prázdný cílový sešit

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Proč tento krok?*  
Začátek s čistým sešitem zabraňuje nechtěným konfliktům s existujícími listy nebo pojmenovanými oblastmi. Cílový sešit přijme zkopírovanou oblast, čímž efektivně **export pivot table** obsah.

### Krok 4: Zkopírujte oblast — kontingenční tabulka je zachována

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Proč tento krok?*  
`copyRange` provádí hlubokou kopii: hodnoty buněk, formátování a metadata kontingenční tabulky jsou přeneseny. Toto je klíčová operace, která umožňuje **copy pivot table** bez ztráty její funkčnosti. Objekt `CellArea` určuje, kam oblast dopadne v cílovém listu.

### Krok 5: Uložte cílový sešit

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Proč tento krok?*  
Uložení dokončuje proces **export pivot table**. Výsledný soubor (`DestWithPivot.xlsx`) obsahuje plně funkční kontingenční tabulku, kterou můžete otevřít v Excelu, Google Sheets nebo jakémkoli jiném prohlížeči tabulek.

## Ověření, že kontingenční tabulka byla zachována

Otevřete `DestWithPivot.xlsx` v Excelu a zkontrolujte následující:

1. Kontingenční tabulka se zobrazuje na stejném místě (A1:G20) jako ve zdroji.
2. Aktualizace kontingenční tabulky (Refresh) správně aktualizuje data, což dokazuje, že cache byla zkopírována.
3. Veškeré formátování (šířky sloupců, formáty čísel) odpovídá originálu.

Pokud některá z těchto kontrol selže, ověřte, že zdrojová oblast plně zahrnuje kontingenční tabulku a její zdroj dat. Častou chybou je výběr oblasti, která nezasahuje až k datové cache, což vede k poškozené kontingenční tabulce.

## Další úvahy

### Kopírování kontingenční tabulky mezi různými verzemi sešitu

Aspose.Cells podporuje starší soubory `.xls` i novější formát `.xlsx`. Stejný kód funguje bez ohledu na příponu souboru, což z něj činí univerzální řešení pro **how to preserve pivot** napříč verzemi.

### Zachování kontingenční tabulky při použití filtrovaného zdroje

Pokud je zdrojová kontingenční tabulka filtrována, stav filtru je také zkopírován. Pokud potřebujete v cíli resetovat filtry, zavolejte po kopírování `PivotTable.refreshData()`:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Export kontingenční tabulky jako statického snímku

Někdy můžete chtít statickou kopii (pouze hodnoty) místo živé kontingenční tabulky. Nahraďte `copyRange` voláním `copyRange` následovaným `pt.setEnableRefresh(false)`, čímž zakážete další výpočty.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Práce s velkými sešity

U sešitů s mnoha listy omezte operaci kopírování na konkrétní list, aby se snížila spotřeba paměti. Použijte `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` pro jemné ladění výkonu.

## Kompletní spustitelný příklad

Níže je celý program, který můžete zkopírovat, vložit a spustit. Přizpůsobte cesty k souborům tak, aby odpovídaly vašemu prostředí.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Očekávaný výstup**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Když otevřete `DestWithPivot.xlsx`, měli byste vidět původní kontingenční tabulku plně funkční, což potvrzuje, že jste úspěšně **how to copy range** při **preserve pivot table**.

## Časté úskalí a tipy pro profesionály

| Problém | Proč k tomu dochází | Řešení |
|---------|---------------------|--------|
| Kontingenční tabulka se zobrazí, ale ukazuje chyby `#REF!` | Zkopírovaná oblast vynechala skrytý list s cache | Rozšiřte zdrojovou oblast tak, aby zahrnovala celou cache (obvykle řádky pod kontingenční tabulkou) |
| Cílový sešit je větší, než se očekávalo | `copyRange` také kopíruje formátování | Použijte `CopyOptions` k vyloučení formátování, pokud je velikost problémem |
| Obnovení selže s chybou „Data source not found“ | Zdrojový sešit použil externí datová připojení | Zreplikujte připojení v cíli nebo nejprve zkopírujte list se zdrojem dat |

**Pro tip:** Vždy po kopírování proveďte rychlou kontrolu `destWs.getPivotTables().size()`. Pokud je počet nula, oblast neobsahovala definici kontingenční tabulky a je třeba ji rozšířit.

## Závěr

V tomto tutoriálu jsme ukázali **how to copy range**, která obsahuje kontingenční tabulku, a zajistili, že chování **preserve pivot table** zůstane neporušené. Načtením zdrojového sešitu, definováním komplexní oblasti, použitím `copyRange` a uložením cílového souboru můžete spolehlivě **export pivot table** data a odpovědět na otázku **how to preserve pivot** v Java projektech.

Další kroky, které můžete prozkoumat, zahrnují:

* Automatizaci kopírování pro více listů (použijte sekundární klíčové slovo **copy pivot table** ve smyčce).
* Převod exportovaného sešitu do CSV při zachování surových dat (stále logika **preserve pivot table** pro zdroj).

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Kopírovat kontingenční tabulku v Javě – Zachovat ji, Exportovat do PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Jak aktualizovat zdroj kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak exportovat kontingenční tabulku jako obrázek v C# – Krok za krokem](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}