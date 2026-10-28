---
category: general
date: 2026-08-17
description: Jak duplikovat list v Javě pomocí Aspose.Cells, zachovat kontingenční
  tabulku, kopírovat kontingenční tabulku do nového sešitu a vytvořit sešit z listu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: cs
lastmod: 2026-08-17
og_description: Jak duplikovat list v Javě pomocí Aspose.Cells, zachovat kontingenční
  tabulku, zkopírovat kontingenční tabulku do nového sešitu a vytvořit sešit z listu
  – všechny kroky vysvětleny.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Jak duplikovat list a zachovat kontingenční tabulky – Java průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Jak duplikovat list a zachovat kontingenční tabulky v Javě
url: /cs/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikovat list a zachovat kontingenční tabulky v Javě

Duplikovat list při zachování jeho kontingenční tabulky je častá potřeba při automatizaci reportování v Excelu. Tento průvodce vám ukáže, jak zkopírovat kontingenční tabulku do nového sešitu pomocí Aspose.Cells pro Java a také jak zachovat kontingenční tabulku při vytváření sešitu z listu.

Naučíte se, jak načíst existující sešit, duplikovat list, který obsahuje kontingenční tabulku, a uložit výsledek jako nový soubor. Tutoriál předpokládá, že máte základní vývojové prostředí Java a platnou licenci Aspose.Cells (bezplatná zkušební verze funguje pro testování). Kromě JAR souboru Aspose.Cells nejsou vyžadovány žádné externí nástroje.

## Požadavky

* Java Development Kit (JDK) 8 nebo novější.
* Maven nebo Gradle pro správu závislosti Aspose.Cells.
* Excel soubor (`source.xlsx`) obsahující alespoň jednu kontingenční tabulku na prvním listu.
* Adresář, ve kterém můžete číst zdrojový soubor a zapisovat duplikovaný sešit.

Přidejte závislost Aspose.Cells do svého `pom.xml` (Maven) nebo `build.gradle` (Gradle). Pro Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Jak duplikovat list s kontingenční tabulkou

Základní operace je tříkrokový proces: načtení, kopírování a uložení. Každý krok je vysvětlen níže.

### Krok 1 – Načtení sešitu, který obsahuje kontingenční tabulku

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Proč je tento krok důležitý*: Objekt `Workbook` představuje celý Excel soubor. Získáním prvního listu (`get(0)`) cílíte na list, který obsahuje kontingenční tabulku, kterou chcete duplikovat.

### Krok 2 – Vytvoření nového sešitu a duplikace celého listu

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` klonuje list **včetně** všech vložených objektů, vzorců a pivot cache. Toto je doporučený způsob, jak **how to copy pivot**, protože definice kontingenční tabulky a její zdrojová data jsou přeneseny společně.

### Krok 3 – Uložení nového sešitu

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Po provedení obsahuje `copy_with_pivot.xlsx` přesnou kopii původního listu a kontingenční tabulka funguje bez další konfigurace.

**Očekávaný výsledek**: Otevření `copy_with_pivot.xlsx` v Excelu zobrazí duplikovaný list se stejným rozvržením kontingenční tabulky, filtry a vypočtenými poli jako ve zdrojovém souboru.

## Jak zkopírovat kontingenční tabulku do jiného sešitu

Pokud potřebujete přesunout kontingenční tabulku bez kopírování celého listu, můžete extrahovat pivot cache a připojit ji k novému listu. Následující úryvek demonstruje tento přístup:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Tento kód odpovídá na **how to copy pivot** tím, že kopíruje pouze objekt kontingenční tabulky, nikoli celý list. Metoda `addCopy` na kolekci `PivotTables` zajišťuje duplikaci pivot cache, což splňuje požadavky **how to preserve pivot**.

## Jak zachovat kontingenční tabulku při vytváření sešitu z listu

Někdy začnete s listem, který nepatří k žádnému sešitu (například generujete list v paměti). Pro **create workbook from sheet** při zachování kontingenční tabulky postupujte podle těchto kroků:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Přidáním listu do nového `Workbook` po úplném definování kontingenční tabulky zajistíte, že **how to preserve pivot** funguje i v případě, že list vznikl mimo existující soubor.

## Praktické tipy a běžné úskalí

| Tip | Proč je to důležité |
|-----|----------------------|
| Použijte `addCopy` místo `copy` | `addCopy` klonuje podkladovou pivot cache; jednoduchý `copy` může ztratit spojení se zdrojem dat. |
| Uchovávejte zdrojové i cílové soubory na stejném souborovém systému | Relativní cesty v datovém zdroji kontingenční tabulky se správně vyřeší, což snižuje chyby „source not found“. |
| Ověřte pivot cache po kopírování | Zavolejte `pivot.refresh()`, pokud se zdrojová data změnila mezi kopírováním a uložením. |
| Uvolněte sešity po dokončení | `sourceWorkbook.dispose();` uvolní nativní zdroje, což je důležité u velkých souborů. |

## Okrajové případy, na které můžete narazit

* **Více listů s navzájem závislými kontingenčními tabulkami** – Kopírujte každý list samostatně; sdílené cache se automaticky duplikují, ale může být nutné znovu přiřadit externí datová připojení.
* **Kontingenční tabulky založené na externích SQL dotazech** – Ujistěte se, že cílové prostředí má přístup ke stejné databázi; jinak se v kontingenční tabulce zobrazí chyby „#REF!“.
* **Velké sešity (>100 MB)** – Použijte `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, abyste snížili zatížení paměti během operace kopírování.

## Kompletní, spustitelný příklad

Níže je kompletní program, který zahrnuje všechny diskutované kroky. Uložte jej jako `CopyPivotTable.java`, upravte cesty k souborům a spusťte jej ve svém preferovaném IDE nebo pomocí `javac`/`java`.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak aktualizovat zdroj kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak implementovat řezače (Slicers) v kontingenčních tabulkách pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}