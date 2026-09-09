---
category: general
date: 2026-03-01
description: Naučte se, jak exportovat CSV z Java sešitu, přičemž nastavíte počet
  významných číslic a rozsah exportu do CSV, v jednom přehledném návodu.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: cs
og_description: Naučte se, jak exportovat CSV v Javě, nastavit významné číslice a
  exportovat rozsah do CSV s praktickým kódem a tipy.
og_title: Jak exportovat CSV v Javě – Kompletní průvodce krok za krokem
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Jak exportovat CSV v Javě – nastavit významné číslice a exportovat rozsah do
  CSV
url: /cs/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat CSV pomocí Javy – Nastavit významné číslice a exportovat oblast do CSV

Už jste se někdy zamysleli **jak exportovat csv** z Java sešitu, aniž byste ztratili číselnou přesnost? Možná jste zkusili rychlé `toString()` a skončili s nepořádkem zaokrouhlovacích chyb. To je častý problém, zejména když potřebujete **nastavit významné číslice** pro finanční data nebo vědecké výsledky.  

V tomto tutoriálu uvidíte kompletní, připravený příklad, který ukazuje **jak exportovat csv**, jak **nastavit významné číslice** a dokonce jak **exportovat oblast do csv**, přičemž data zůstávají přehledná. Projdeme každý řádek, vysvětlíme *proč* za voláními API a dáme vám tipy, jak se vyhnout běžným úskalím. Žádná další dokumentace ke sledování – jen samostatné řešení, které můžete dnes zkopírovat a vložit.

## Co se naučíte

- Vytvořit sešit a nastavit číselnou přesnost pomocí `setNumberSignificantDigits`.
- Exportovat konkrétní oblast buněk jako pěkně formátovaný řetězec CSV.
- Analyzovat japonské datumové éry pomocí `DateTimeFormatInfo`.
- Přepočítat vzorce, aby výsledky dynamických polí zůstaly aktuální.
- Vykreslit kontingenční tabulku do PNG obrázku.
- Použít Smart Marker k vložení komentářů a nakonec uložit sešit.

Všechny tyto operace jsou provedeny pomocí knihovny Aspose.Cells for Java, verze 23.12 (nejnovější v době psaní). Pokud máte JAR ve své classpath, můžete rovnou začít.

---

## Krok 1: Vytvořit sešit a **nastavit významné číslice**

Než budeme moci cokoli exportovat, potřebujeme objekt sešitu. První věc, kterou mnozí vývojáři přehlédnou, je číselná přesnost. Ve výchozím nastavení Aspose.Cells používá plnou dvojitou přesnost, což může vést k dlouhým, nešikovným řetězcům v CSV. Nastavením počtu významných číslic se výstup zkrátí a zároveň zachová nejdůležitější číslice.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Proč je to důležité?**  
Pokud exportujete buňku obsahující `12345.6789` bez omezení číslic, CSV zobrazí plnou hodnotu a znečistí reporty. S `setNumberSignificantDigits(5)` se stejná buňka stane `12346`, což je často to, co očekávají obchodní uživatelé.

> **Tip:** Pokud potřebujete různou přesnost pro jednotlivé sloupce, můžete použít vlastní `Style` místo globálního nastavení.

---

## Krok 2: **Exportovat oblast do CSV** – Formátování má význam

Nyní, když je sešit připraven, vybereme obdélníkový blok dat a převedeme jej na řetězec CSV. Navíc vynutíme formát se dvěma desetinnými místy (`0.00`), aby se každé číslo pěkně zarovnalo.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

Volání `exportDataTable` dělá těžkou práci. Protože jsme nastavili `exportAsString`, metoda vrací `String`, který můžeme vytisknout, zapsat do souboru nebo poslat přes HTTP. Krok **exportovat oblast do csv** také respektuje globální `setNumberSignificantDigits`, které jsme definovali dříve, takže čísla jsou jak zaokrouhlena na pět významných číslic, tak zobrazena se dvěma desetinnými místy.

**Očekávaný výstup (zkrácený):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Často kladená otázka:** *Co když potřebuji jiný oddělovač, například středník?*  
> Stačí zavolat `exportOptions.setSeparator(";")` před exportem.

---

## Krok 3: Analyzovat japonské datumové éry (bonusová utilita)

I když to není přímo spojeno s CSV, mnoho Excelových listů obsahuje lokálně specifická data. Zde je ukázka, jak převést japonský řetězec era jako `"R3/04/01"` na standardní objekt `DateTime`.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Výstup:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Proč to zahrnout?**  
Pokud váš CSV export napájí downstream systémy, které očekávají ISO‑8601 data, musíte nejprve normalizovat všechny lokalizované formáty. Tento úryvek ukazuje *jak* i *proč* na jednom místě.

---

## Krok 4: Přepočítat vzorce – Udržet výsledky dynamických polí čerstvé

Pokud sešit obsahuje vzorce (např. `=SUM(A1:A10)`), po změně nastavení se neaktualizují automaticky. Volání `calculateFormula` vynutí úplný přepočet, čímž zajistí, že exportované CSV odráží nejnovější hodnoty.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Pozor:** Velké sešity mohou vyžadovat znatelný čas na přepočet. Pro scénáře citlivé na výkon zvažte `calculateFormula(FormulaCalculationOptions)`, aby se omezil rozsah.

---

## Krok 5: Vykreslit první kontingenční tabulku do PNG obrázku

Někdy potřebujete vizuální snímek kontingenční tabulky vedle CSV. Následující kód vykreslí první kontingenční tabulku na prvním listu do PNG souboru.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Tip:** Pokud sešit ještě neobsahuje kontingenční tabulku, můžete ji vytvořit programově – podívejte se do dokumentace Aspose.Cells na rychlý příklad.

---

## Krok 6: Použít Smart Marker k zápisu komentáře a uložení sešitu

Smart Marker vám umožní vkládat dynamický obsah do buněk pomocí jednoduchých zástupných znaků. Zde zapíšeme komentář jako “Reviewed by QA” do určené buňky a poté sešit uložíme.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

Zástupný znak `${Comment}` můžete umístit kamkoli v listu (např. buňka `A1`). Když se spustí `apply`, zástupný znak se nahradí předanou hodnotou.

**Výsledek:** Najdete soubor `output/commented.xlsx` obsahující komentář, plus dříve vygenerovaný `pivot.png` a řetězec CSV vytištěný do konzole.

---

## Kompletní funkční příklad

Spojením všech částí získáte kompletní program, který můžete zkompilovat a spustit:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Očekávaný výstup v konzoli

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Na disku také najdete `output/pivot.png` (pokud kontingenční tabulka existovala) a `output/commented.xlsx`.

---

## Často kladené otázky a okrajové případy

- **Mohu exportovat přímo do fyzického CSV souboru?**  
  Ano. Nahraďte blok `exportAsString` voláním `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Co když můj list používá jinou lokalizaci pro čísla?**  
  Před exportem nastavte `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))`; tím se přepne

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}