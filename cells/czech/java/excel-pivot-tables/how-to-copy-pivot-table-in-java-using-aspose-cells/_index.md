---
category: general
date: 2026-07-06
description: Jak zkopírovat kontingenční tabulku v Javě s Aspose.Cells – krok za krokem
  průvodce pro programové duplikování kontingenčních tabulek v Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: cs
lastmod: 2026-07-06
og_description: Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells vám
  umožní rychle a spolehlivě duplikovat kontingenční tabulky v Excelu.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Jak zkopírovat kontingenční tabulku v Javě – kompletní průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells
url: /cs/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v Javě pomocí Aspose.Cells

Už jste se někdy zamysleli nad **jak zkopírovat pivot** tabulky v souboru Excel, aniž byste ručně otevírali sešit? Nejste v tom sami. V mnoha reportovacích pipelinech potřebujete **duplikovat Excel pivot** tabulky za běhu — možná pro vytvoření snímku, přesunutí na nový list nebo vytvoření šablony pro následné uživatele.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který přesně ukazuje, jak na to. Pomocí knihovny Aspose.Cells pro Java načteme sešit, najdeme zdrojový rozsah pivotu, zkopírujeme jej na nové místo a výsledek uložíme. Žádné vágní odkazy, jen konkrétní řešení, které můžete ještě dnes vložit do svého projektu.

---

## Požadavky

* **Java Development Kit (JDK) 8+** – kód se kompiluje s jakýmkoli aktuálním JDK.
* **Aspose.Cells for Java** verze 25.11 nebo novější – metoda `Range.copy`, která podporuje kontingenční tabulky, byla představena v tomto vydání.
* Soubor **input.xlsx**, který již obsahuje kontingenční tabulku (můžete si ji vytvořit v Excelu pro testování).
* Nástroj pro sestavení dle vašeho výběru (Maven, Gradle nebo prostý `javac`). Ukážeme Maven závislost pro rychlý start.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Krok 1: Načtení zdrojového sešitu

Prvním krokem je otevřít soubor Excel, který obsahuje původní kontingenční tabulku. Aspose.Cells zachází se sešitem jako s objektem v paměti, takže jej můžete manipulovat, aniž byste spouštěli Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Proč je to důležité:** Načtení sešitu nám poskytuje přístup k listům, buňkám a, co je zásadní, k pivotní cache, která podporuje kontingenční tabulku. Bez tohoto kroku knihovna nemá co kopírovat.

---

## Krok 2: Získání listu obsahujícího pivot

Pokud má váš sešit více listů, musíte ukázat na ten správný. Zde jednoduše získáme první list, ale můžete také použít `get("SheetName")` pro vyhledání podle názvu.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Tip:** Při práci s mnoha listy uložte index nebo název do konfiguračního souboru, abyste se vyhnuli pevně zakódovaným číslům.

---

## Krok 3: Definování zdrojového rozsahu, který zahrnuje kontingenční tabulku

Od verze 25.11 umožňuje Aspose.Cells zacházet s kontingenční tabulkou jako s běžným rozsahem buněk. Zadejte buňky v levém horním a pravém dolním rohu, které ohraničují celou tabulku.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Hraniční případ:** Pokud se váš pivot dynamicky rozšiřuje (např. jsou později přidány řádky), zvažte použití `worksheet.getPivotTables().get(0).getDataRange()` pro programové získání přesného rozsahu.

---

## Krok 4: Definování cílového rozsahu, kam bude pivot zkopírován

Vyberte libovolnou prázdnou buňku, kde chcete, aby se duplikovaný pivot objevil. V tomto demu začínáme na **F1**, čímž ponecháváme mezeru mezi originálem a kopií.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Proč ne nový list?** Můžete také vytvořit nový list (`workbook.getWorksheets().add("Copy")`) a použít jeho buňky jako cíl. Stejná metoda `copy` funguje napříč listy.

---

## Krok 5: Zkopírování kontingenční tabulky na nové místo

Nyní se děje magie. Metoda `copy` klonuje pivot, jeho cache, formátování a dokonce i související řezače (slicery) (od nejnovější verze).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Důležité:** Operace kopírování je *hluboká*; **nevytváří** odkaz zpět na původní pivot. Nový pivot můžete upravovat nezávisle, aniž byste ovlivnili zdroj.

---

## Krok 6: Uložení sešitu s duplikovaným pivotem

Nakonec zapíšeme upravený sešit zpět na disk. Můžete přepsat originál nebo vytvořit nový soubor; zde volíme druhou možnost, aby zdroj zůstal nedotčen.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Když otevřete **output.xlsx** v Excelu, uvidíte původní pivot ve sloupcích A‑D a dokonalou kopii začínající ve sloupci F. Oba pivoty lze obnovovat samostatně.

---

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní třídu Java, kterou můžete přímo zkompilovat a spustit:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Očekávaný výsledek:** Otevření `output.xlsx` ukazuje původní pivot (A1:D20) a identický pivot začínající na F1. Obě tabulky si zachovávají své filtry, styly a vypočtená pole.

---

## Řešení běžných variant

| Situace | Co upravit |
|-----------|----------------|
| **Multiple pivots** na stejném listu | Procházejte `worksheet.getPivotTables()` a zkopírujte každou s vlastním cílovým rozsahem. |
| **Dynamic data range** | Použijte `worksheet.getPivotTables().get(0).getDataRange()` pro automatické zjištění zdrojové oblasti. |
| **Copy to another workbook** | Načtěte druhou instanci `Workbook`, vytvořte cílový list a poté zavolejte `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | Od verze 25.12 jsou slicery kopírovány automaticky, pokud je rozsah zahrnuje. Ověřte v Excelu po uložení. |

---

## Pro tipy a úskalí

* **Kontrola verze:** Metoda `copy`, která podporuje pivoty, byla přidána v **Aspose.Cells 25.11**. Pokud používáte starší verzi, získáte výjimku. Vždy ověřte verzi `aspose-cells` ve vašem `pom.xml`.
* **Výkon:** Kopírování velkých pivotů může být náročné na paměť. Pokud potřebujete jen data, zvažte export pivotu do ploché tabulky místo klonování celého objektu.
* **Chování při obnově:** Duplikovaný pivot si zachovává vlastní cache. Pokud změníte podkladová data, zavolejte `pivotTable.refresh()` na novém pivotu pro přepočet.
* **Zvláštnosti formátování:** Některé vlastní číselné formáty nemusí při kopírování přetrvat ve velmi starých verzích Excelu (<2007). Otestujte na verzi Excelu, kterou používá vaše cílová skupina.

---

## Závěr

Nyní máte pevnou, end‑to‑end odpověď na **jak zkopírovat pivot** tabulky pomocí Aspose.Cells pro Java a viděli jste, jak **duplikovat Excel pivot** tabulky v několika řádcích kódu. Přístup funguje pro jediné i více pivotů, napříč listy a dokonce i mezi sešity.

Další kroky mohou zahrnovat:

* Automatizaci kopírování pro každý pivot v dávkovém úkolu.
* Přidání kódu pro přejmenování duplikovaného pivotu (např. `pivotTable.setName("Copy_of_Sales")`).
* Integraci rutiny do většího reportovacího servisu, který generuje PDF nebo CSV exporty.

Vyzkoušejte to, upravte rozsahy tak, aby odpovídaly vašim skutečným datům, a nechte knihovnu udělat těžkou práci. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}