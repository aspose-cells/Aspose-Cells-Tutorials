---
category: general
date: 2026-06-21
description: Programově kopírovat rozsah listu v Javě pomocí Aspose.Cells. Naučte
  se, jak efektivně kopírovat rozsah Excelu do jiného sešitu.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: cs
og_description: Programově kopírovat oblast listu v Javě. Tento průvodce ukazuje,
  jak zkopírovat oblast Excelu do jiného sešitu s kompletním kódem a tipy.
og_title: Programaticky kopírovat rozsah listu – Java krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Programově kopírovat rozsah listu – kompletní průvodce Java
url: /cs/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programově kopírovat oblast listu – Kompletní průvodce v Javě

Už jste se někdy zamysleli, jak **programově kopírovat oblast listu** bez ručního otevírání Excelu? Nejste v tom sami. Ať už potřebujete duplikovat zprávu, klonovat dashboard založený na kontingenční tabulce, nebo jen přesunout data mezi soubory, provedení toho v kódu šetří čas a eliminuje lidské chyby.

V tomto tutoriálu projdeme čistým, end‑to‑end řešením, které ukazuje **jak kopírovat oblast Excelu do jiného sešitu** pomocí Javy a knihovny Aspose.Cells. Na konci budete mít připravený spustitelný program, pochopíte důvody za jednotlivými kroky a budete znát úskalí, na která si dát pozor.

---

## Co budete potřebovat

- **Java Development Kit (JDK) 11+** – kód se kompiluje s jakýmkoli moderním JDK.
- **Aspose.Cells for Java** (bezplatná zkušební verze nebo licencovaná). Přidejte Maven závislost nebo stáhněte JAR.
- Dva soubory Excel: `input.xlsx`, který obsahuje zdrojovou oblast (včetně kontingenční tabulky) a prázdný `output.xlsx`, kam bude oblast umístěna.
- Jakékoliv IDE, které máte rádi – IntelliJ IDEA, Eclipse nebo i jednoduchý textový editor.

To je vše. Žádné extra služby, žádné COM rozhraní, jen čistá Java.

![Diagram ilustrující programové kopírování oblasti listu mezi dvěma sešity](image.png)

*Alt text obrázku: ilustrace programového kopírování oblasti listu*

## Krok 1: Nastavení projektu a import Aspose.Cells

Nejprve potřebujeme knihovnu na classpath. Pokud používáte Maven, přidejte:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Pokud dáváte přednost ručnímu JAR souboru, vložte jej do složky `libs` a přidejte jej do cesty sestavení.

Proč je to důležité: Aspose.Cells poskytuje bohatý objektový model (`Workbook`, `Worksheet`, `Range`), který nám umožňuje kopírovat data **včetně kontingenčních tabulek, vzorců a formátování** jedním voláním – něco, co čistá knihovna Apache POI nedokáže tak čistě.

## Krok 2: Načtení zdrojového sešitu

Otevřeme sešit, který obsahuje data, jež chceme klonovat. Konstruktor `Workbook` přijímá cestu k souboru a Aspose načte celý soubor do paměti.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Tip:* Zabalte načítání do try‑catch bloku, pokud by soubor mohl chybět; jinak program skončí s jasnou chybou.

## Krok 3: Vytvoření prázdného cílového sešitu

Čerstvý sešit nám poskytuje čisté plátno. Nemusíme předem naplňovat žádné listy; Aspose přidá jeden za nás.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Proč nepoužít zdrojový sešit znovu? Udržení oddělených souborů zabraňuje nechtěnému přepsání a činí kód znovu použitelným pro dávkové operace.

## Krok 4: Definování přesné oblasti ke kopírování

Zde začíná kouzlo **programového kopírování oblasti listu**. Vybereme buňky `A1:D20` z prvního listu zdrojového souboru. Metoda `createRange` vrací objekt `Range`, který přesně představuje tyto buňky, včetně kontingenčních tabulek.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Pokud potřebujete dynamickou oblast (např. „poslední použitý řádek“), můžete nahradit pevně zadanou adresu pomocí `Cells.maxDisplayRange` nebo ji vypočítat pomocí `Cells.getMaxDataColumn()` a `Cells.getMaxDataRow()`.

## Krok 5: Přidání cílového listu do cílového sešitu

Aspose vytvoří výchozí list s názvem „Sheet1“, když vytvoříte instanci `Workbook`. Přidáme nový, aby vše bylo přehledné, zejména pokud později plánujete kopírovat více oblastí.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Můžete listu přiřadit přátelský název:

```java
        targetWorksheet.setName("CopiedData");
```

## Krok 6: Provedení kopírování – včetně kontingenčních tabulek

Nyní hlavní operace: `copyRange`. Tato metoda kopíruje **hodnoty, vzorce, formátování a vložené objekty** (např. kontingenční tabulky) ze zdrojové oblasti do cílové buňky (`A1` v našem novém listu). Je to nejjednodušší způsob, jak dosáhnout **jak kopírovat oblast Excelu do jiného sešitu** bez manipulace s nízkoúrovňovými smyčkami buněk.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Za scénou Aspose serializuje zdrojovou oblast do meziformátu a poté ji deserializuje do cílového listu – takže vše zůstane nedotčeno.

## Krok 7: Uložení cílového sešitu a ověření

Nakonec zapíšeme cílový sešit na disk. Otevřete `output.xlsx` v Excelu a uvidíte zkopírovanou oblast, kontingenční tabulku a veškeré zachované formátování.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Když otevřete `output.xlsx`, měli byste vidět list pojmenovaný „CopiedData“ se stejným rozvržením jako `A1:D20` ze zdroje, včetně kontingenční tabulky, která nyní ukazuje na zkopírovaná data.

## Řešení běžných okrajových případů

### 1. Kopírování mezi různými verzemi Excelu

Aspose.Cells funguje s `.xls`, `.xlsx`, `.xlsb` a dokonce i `.csv`. Pokud zdroj a cíl používají různé formáty, knihovna je automaticky převede. Stačí zajistit, aby přípony souborů odpovídaly požadovanému výstupu.

### 2. Zachování externích datových zdrojů v kontingenčních tabulkách

Pokud kontingenční tabulka ve zdroji odkazuje na externí datový zdroj (např. databázové připojení), zkopírovaná tabulka zachová řetězec připojení, ale **se neobnoví automaticky**. Po kopírování zavolejte `pivotTable.refreshData()`, pokud potřebujete aktuální výsledky.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Velké oblasti a spotřeba paměti

Kopírování obrovských oblastí (stovky tisíc řádků) může zvýšit spotřebu paměti. Před načtením velkých souborů použijte `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby se snížila paměťová stopa.

### 4. Více listů nebo oblastí

Pokud potřebujete kopírovat několik nesouvislých oblastí, opakujte kroky 4‑6 pro každou oblast, nebo použijte `copyRange` s unijní oblastí (`Cells.createRange("A1:B10,C1:D10")`).

## Pro tipy pro robustní automatizaci

- **Ověřte zdrojovou oblast** před kopírováním. Použijte `sourceRange.isValid()`, abyste se vyhnuli chybám za běhu.
- **Uzamkněte cílový soubor** pomocí `FileInfo.setReadOnly(false)`, pokud přepisujete existující sešit.
- **Logujte akce** pomocí lehkého loggeru (SLF4J) – zvláště užitečné při zpracování dávkových úloh.
- **Uvolněte sešity** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) v dlouho běžících službách, aby se uvolnily nativní zdroje.

## Kompletní funkční příklad – shrnutí

Níže je kompletní, samostatná třída Java, kterou můžete vložit do svého IDE a spustit. Nezapomeňte nahradit `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Očekávaný výstup:** Soubor `output.xlsx` s listem pojmenovaným „CopiedData“. Buňky `A1:D20` budou odrážet zdroj a jakákoli kontingenční tabulka v tomto bloku bude plně funkční a bude ukazovat na zkopírovaná data.

## Závěr

Právě jsme předvedli čisté řešení **programového kopírování oblasti listu** v Javě, které odpovídá na častou otázku **jak kopírovat oblast Excelu do jiného sešitu**. Využitím vysoké úrovně API Aspose.Cells jsme se vyhnuli nízkoúrovňovým smyčkám buněk, zachovali kontingenční tabulky a udrželi kód čitelný.

Co dál? Zkuste rozšířit tento vzor na:

- Kopírování celých listů místo jedné oblasti.
- Dávkové zpracování desítek sešitů ve složce.
- Export zkopírované oblasti do CSV nebo PDF pro reportingové pipeline.

Klidně experimentujte a pokud narazíte na problém, zanechte komentář. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak kopírovat více sloupců v Excelu pomocí Aspose.Cells Java&#58; Kompletní průvodce](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Efektivní kopírování sloupců v Excelu pomocí Aspose.Cells pro Java&#58; Komplexní průvodce](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Kopírování obrázků mezi listy v Excelu pomocí Aspose.Cells pro Java&#58; Komplexní průvodce](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}