---
category: general
date: 2026-10-07
description: Naučte se, jak duplikovat kontingenční tabulky v Excelu pomocí Javy a
  Aspose.Cells. Rychle zkopírujte kontingenční tabulku kopírováním jejího rozsahu
  mezi sešity.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: cs
lastmod: 2026-10-07
og_description: Jak duplikovat kontingenční tabulky v Excelu pomocí Javy a Aspose.Cells.
  Postupujte podle tohoto návodu, abyste zkopírovali kontingenční tabulku kopírováním
  jejího rozsahu mezi sešity.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Jak duplikovat kontingenční tabulky v Excelu pomocí Javy – kompletní návod
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Jak duplikovat kontingenční tabulky v Excelu pomocí Java – krok za krokem
url: /cs/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikovat kontingenční tabulky v Excelu pomocí Javy – krok za krokem průvodce

Pokud potřebujete **jak duplikovat pivot** tabulky v sešitu Excel, tento tutoriál vám ukáže kompletní, připravené řešení. Pomocí Aspose.Cells pro Javu můžete zkopírovat kontingenční tabulku spolu s jejími zdrojovými daty zkopírováním podkladového rozsahu a následným uložením výsledku jako nový sešit.

Duplikování kontingenční tabulky se často zdá obtížné, protože pivot cache je skrytý uvnitř listu. Zkopírováním celého rozsahu, který obsahuje pivot, Aspose.Cells automaticky vytvoří cache v cílovém sešitu, takže získáte plně funkční kopii bez ručního manipulování s XML.

V tomto průvodci:

* Načtete zdrojový sešit, který obsahuje kontingenční tabulku.  
* Definujete přesný rozsah, který pivot obsahuje.  
* Zkopírujete tento rozsah do nového sešitu, přičemž zachováte definici pivotu.  
* Uložíte nový soubor a ověříte, že pivot funguje.  

Kroky fungují s libovolnou verzí Excelu podporovanou Aspose.Cells (2007‑2024) a vyžadují jen několik řádků Java kódu.

## Prerequisites

| Požadavek | Proč je to důležité |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells je postaven na Java 8+. |
| **Aspose.Cells for Java** (latest version) | Poskytuje API `Workbook`, `Range` a `CopyRange` použité v příkladu. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Zdrojový sešit obsahující kontingenční tabulku (např. `Source.xlsx`). |
| **Write permission** to the target directory | Oprávnění k zápisu do cílového adresáře. |
| | Potřebné pro uložení `CopyWithPivot.xlsx`. |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Jak duplikovat kontingenční tabulky – kompletní implementace

Níže je samostatný Java program, který demonstruje **jak duplikovat pivot** tabulky kopírováním rozsahu, který obsahuje pivot. Kód zahrnuje ošetření chyb, komentáře a ověřovací krok.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Vysvětlení každého kroku

| Krok | Co kód dělá | Proč je to důležité pro **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` načte `Source.xlsx`. | Zdrojový soubor je jediným místem, kde existuje originální pivot. |
| **2️⃣ Define the range** | `createRange("A1:G20")` vytvoří objekt `Range`, který pokrývá pivot a jeho data. | Kontingenční tabulka je uložena spolu s cache; kopírováním celého rozsahu se zajistí, že cache je také přesunuta. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` zapíše rozsah do cílového listu. | Toto je jádro **copy range between workbooks** – API automaticky zpracovává skryté objekty. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` vynutí přepočet pivotu. | Zaručuje, že duplikovaný pivot zobrazuje stejné hodnoty jako originál, zejména po úpravách. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` zapíše soubor na disk. | Vytvoří finální výsledek **copy excel range**, který můžete otevřít v Excelu. |

#### Očekávaný výstup

Po spuštění programu otevřete `CopyWithPivot.xlsx`. Uvidíte list, který vypadá identicky jako zdrojový list, a kontingenční tabulka funguje přesně jako originál – můžete rozbalovat řádky, filtrovat pole a obnovovat data bez chyb.

## Běžné varianty a okrajové případy

### 1️⃣ Kopírování pivotu, který se rozprostírá na více listech

Pokud zdrojová data pivotu jsou na jiném listu než samotný pivot, zahrňte oba listy do operace kopírování. Nejjednodušší přístup je nejprve zkopírovat celý zdrojový list a poté zkopírovat list s pivotem:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Práce s pojmenovanými rozsahy

Aspose.Cells zachovává pojmenované rozsahy při kopírování rozsahu. Pokud však cílový sešit již obsahuje název se stejným identifikátorem, je vyvolána `CellsException`. Vyřešte to přejmenováním konfliktního názvu před kopírováním:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Velké sešity a výkon

Kopírování velmi velkých rozsahů (stovky tisíc řádků) může být náročné na paměť. Povolit **optimalizaci paměti**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Zachování vzorců beze změny

Pokud zdrojový rozsah obsahuje vzorce, které odkazují na buňky mimo kopírovanou oblast, tyto odkazy se po kopírování rozbijí. Aby se tomu předešlo, rozšiřte rozsah tak, aby zahrnoval všechny závislé buňky, nebo použijte `copyRange` s příznakem `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Profesionální tipy pro spolehlivé **copy range between workbooks**

* **Vždy používejte absolutní adresy** (`$A$1:$G$20`), pokud může být zdrojový list přejmenován.  
* **Obnovte po kopírování** – i když Aspose.Cells přestaví cache, volání `refresh()` eliminuje občasná varování o zastaralé cache v Excelu.  
* **Ověřte pivot**: po uložení otevřete soubor programově a zavolejte `pivotTable.validate()`, aby se zajistilo, že neexistují poškozené odkazy.  
* **Kompatibilita verzí**: kód funguje se soubory Excel 2007‑2024 (`.xlsx`, `.xlsm`). Pro starší soubory `.xls` nastavte `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Kompletní výpis zdrojového kódu (připravený ke kompilaci)



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s krok za krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak zkopírovat kontingenční tabulku v Javě – Kompletní průvodce Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Jak vytvořit kontingenční tabulky v Excelu pomocí Aspose.Cells pro Javu: Kompletní průvodce](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak aktualizovat zdroj kontingenční tabulky v Excelu s Aspose.Cells pro Javu: Kompletní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}