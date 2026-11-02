---
category: general
date: 2026-06-21
description: Jak aplikovat styly při převodu DataTable do Excelu v Javě. Naučte se
  importovat datovou tabulku do Excelu, přidat vlastní styly do Excelu a uložit sešit
  do souboru během několika minut.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: cs
og_description: Jak aplikovat styly při převodu DataTable do Excelu v Javě. Tento
  návod vám ukáže, jak importovat datovou tabulku do Excelu, přidat vlastní styly
  do Excelu a uložit sešit do souboru.
og_title: Jak aplikovat styly při převodu DataTable do Excelu – Java tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: Jak použít styly při převodu DataTable do Excelu – Kompletní Java průvodce
url: /cs/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít styly při převodu DataTable do Excelu – Kompletní průvodce pro Javu

Už jste se někdy zamysleli **jak použít styly**, když potřebujete **převést DataTable do Excelu**? Nejste jediní. V mnoha interních nástrojích načítáme data z databází, vložíme je do `DataTable` a pak očekáváme hezky vypadající tabulku bez dalšího úsilí. Spoiler: musíte knihovně *přesně* říct, co “hezké” znamená.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který ukazuje **jak použít styly** pomocí Aspose.Cells pro Java, importuje `DataTable` do Excelu, **přidá vlastní styly excel**‑style a nakonec **uloží sešit do souboru**. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného projektu.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli recentní JDK) – kód funguje také na Java 8+.
- **Aspose.Cells for Java** JAR (bezplatná zkušební verze stačí pro testování).
- Zdroj `DataTable` – vytvoříme jednoduchý mock, ale můžete dosadit jakýkoli skutečný výsledek dotazu.
- IDE podle vašeho výběru (IntelliJ, Eclipse, VS Code…).

Žádné další nástroje pro sestavení nejsou potřeba; stačí prostý Maven `pom.xml`, ale můžete JAR také přidat ručně.

## Krok 1: Nastavení projektu a závislostí

Nejprve – pojďme získat knihovnu na classpath.

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

Pokud nepoužíváte Maven, stačí vložit `aspose-cells-24.9.jar` do složky `libs` a přidat ji do cesty sestavení.

> **Tip:** Aspose dodává třídu `License`. Zaregistrujte licenci brzy, jinak se ve výstupním souboru objeví vodoznaky.

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

Nyní jsme připraveni mluvit o **jak použít styly**.

## Krok 2: Vytvoření vlastních stylů pro Excel

Magie upravené tabulky spočívá v stylech buněk. Aspose vám umožní definovat objekt `Style`, upravit písma, barvy, okraje a pak jej znovu použít kdekoliv chcete. Níže je kompaktní způsob, jak **přidat vlastní styly excel**‑wide.

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

Všimněte si, že jsme vytvořili **dvě odlišné styly** – jeden pro záhlaví sloupců a jeden pro řádky s daty. Můžete rozšířit toto pole o libovolný počet stylů; Aspose je použije v pořadí, ve kterém je předáte metodě `importDataTable`.

## Krok 3: Import DataTable do listu

Nyní přichází část, která skutečně **importuje datatable do excelu**. Metoda `importDataTable` přijímá zdrojový `DataTable`, příznak pro záhlaví sloupců, počáteční řádek/sloupec a pole stylů, které jsme právě vytvořili.

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

Rychlá poznámka: argument `true` říká Aspose, aby **zachoval záhlaví sloupců** – to je typický případ, když chcete čitelnou zprávu. Pokud ho nastavíte na `false`, první řádek dat se stane záhlavím.

## Krok 4: Spojení všeho dohromady – minimální funkční příklad

Níže je samostatná metoda `main`, která vytvoří ukázkový `DataTable`, zavolá exportní rutinu a zapíše `output.xlsx` do složky `./results`.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**Očekávaný výstup:** Otevřete `output.xlsx` a uvidíte tučný, šedý řádek záhlaví, buňky s tenkými okraji a sloupce automaticky nastavené na šířku podle obsahu. To je přesně **jak použít styly**, aby tabulka vypadala profesionálně.

![Jak použít styly v Excel sešitu](/images/excel-styles.png){alt="Jak použít styly v Excel sešitu"}

*(Na snímku je záhlaví tučné šedé a řádky s daty mají tenké okraje.)*

## Krok 5: Pokročilé tipy a okrajové případy

### 5.1 Podmíněné formátování místo pevných stylů  
Pokud potřebujete zvýraznit řádky, kde `Score > 90`, můžete po importu přidat `ConditionalFormattingCollection`. To vám poskytne dynamické barvení bez nutnosti pevně kódovat další styly.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Sloučení buněk pro nadpisy  
Někdy zpráva potřebuje velký nadpis přes několik sloupců. Použijte `worksheet.getCells().merge(0, 0, 1, 3)` a poté aplikujte odlišný styl na tuto sloučenou oblast.

### 5.3 Velké datové sady – výkonnostní úvahy  
Při práci s >100 000 řádky nastavte `ImportDataTableOptions` na `ImportDataTableOptions.NO_FORMATTING` nejprve, pak aplikujte styly v druhém průchodu. Tím se vyhnete režii stylování každé buňky během importu.

### 5.4 Export více listů  
Pokud máte několik `DataTable`ů, stačí vytvořit další listy pomocí `workbook.getWorksheets().add("Sheet2")` a zopakovat krok **import datatable do excelu** pro každý list.

## Závěr

Probrali jsme **jak použít styly** od začátku do konce: nastavení Aspose.Cells, tvorbu **vlastních stylů excel**, **import datatable do excelu** a nakonec **uložení sešitu do souboru**. Kompletní ukázkový kód je připraven ke zkopírování a vložení a další tipy vám poskytují plán pro složitější zprávy.

Dále můžete zkoumat **přidání vlastních stylů excel** pro grafy nebo experimentovat s **převodem datatable do excelu** v REST endpointu Spring Boot. V každém případě máte nyní pevný základ pro převod surových tabulek na upravené tabulky – bez ručního formátování.

Máte otázky

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Jak použít styly na buňky v Excelu pomocí Aspose.Cells pro Java – Kompletní průvodce](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Sloučit buňky a použít styly v Excelu pomocí Aspose.Cells pro Java – Kompletní průvodce](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Jak importovat DataTable do Excelu pomocí Aspose.Cells pro .NET (Krok za krokem průvodce)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}