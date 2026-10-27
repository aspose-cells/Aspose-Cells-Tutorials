---
category: general
date: 2026-10-07
description: Naučte se, jak číst data Excelu z buněk v Javě pomocí Aspose.Cells a
  také efektivně zapisovat hodnoty zpět do Excelu.
draft: false
keywords:
- how to read excel
- write value to excel
- get datetime from excel
- extract datetime from cell
- Aspose.Cells Java date parsing
lastmod: 2026-10-07
og_description: Jak číst data Excelu z buněk v Javě pomocí Aspose.Cells. Tento průvodce
  také ukazuje, jak efektivně zapisovat hodnoty do buněk Excelu.
og_image_alt: 'Developer guide: reading and writing Excel dates with Aspose.Cells
  Java'
og_title: Jak číst data Excelu z buněk v Javě pomocí Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  headline: How to read Excel dates from cells in Java using Aspose.Cells
  type: TechArticle
- description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  name: How to read Excel dates from cells in Java using Aspose.Cells
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- date parsing
- Excel automation
title: Jak číst data Excelu z buněk v Javě pomocí Aspose.Cells
url: /cs/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak číst data Excel z buněk v Javě pomocí Aspose.Cells

Pokud potřebujete **jak číst Excel** hodnoty uložené jako řetězce japonské éry, jste na správném místě. Mnoho starých sešitů obsahuje data jako „Reiwa 3/04/01“ a získání správného `java.time.LocalDateTime` může připomínat luštění kódu. Aspose.Cells pro Java rozumí těmto notacím éry a také vám umožní **zapsat hodnotu do excel** buněk bez ztráty formátování. V tomto průvodci získáte kompletní, krok‑za‑krokem návod, který můžete dnes vložit do libovolného Maven projektu.

## Rychlé odpovědi
- **Umí Aspose.Cells parsovat data japonské éry?** Ano – povolte příznak kalendáře japonské éry a přepočítejte vzorce.  
- **Musím přepočítávat vzorce ručně?** Rozhodně; bez výpočtového průchodu zůstane řetězec éry textem.  
- **Kolik formátů Excel podporuje Aspose.Cells?** Více než 50 vstupních a výstupních formátů, včetně XLSX, XLS, CSV a ODS.  
- **Je knihovna kompatibilní s Java 8+?** Ano, funguje s Java 8 a novějšími verzemi runtime.  
- **Mohu zpět zapsat gregoriánské datum do stejné buňky?** Použijte `putValue` s `LocalDateTime` a nastavte číselný formát na zobrazení ISO‑8601.

## Co je „jak číst data Excel z buněk“?
Fráze **jak číst Excel** odkazuje na extrakci obsahu buněk – zejména dat – do nativních programových typů, jako je `java.time.LocalDateTime`. Aspose.Cells abstrahuje nízkoúrovňové parsování, takže se můžete soustředit na obchodní logiku místo zvláštností sériových čísel Excelu. Tento přístup zjednodušuje údržbu kódu a snižuje riziko chyb při konverzi ve starých tabulkách.

## Proč použít Aspose.Cells pro konverzi japonské éry?
Aspose.Cells podporuje **50+** souborových formátů a dokáže zpracovat sešity s **stovkami listů** bez načítání celého souboru do paměti. Povolení kalendáře japonské éry přidává jen zanedbatelný výkonový náklad, což jej činí ideálním pro dávkové zpracování starých tabulek. Knihovna také zachovává styly buněk a vzorce během konverze, takže výstup vypadá identicky jako originální sešit.

## Předpoklady

* **Java 8+** – příklady používají moderní API `java.time`.  
* **Aspose.Cells pro Java ≥ 23.9.0** – přidejte Maven/Gradle závislost z oficiálního repozitáře.  
* Základní znalost konceptů Excelu (listy, buňky, vzorce).  

Pokud vám knihovna chybí, stáhněte ji z oficiálního Aspose repozitáře:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Jak vytvořit sešit a získat první list?
`Workbook` představuje soubor Excel načtený v paměti. `Worksheet` představuje jeden list v tomto sešitu.  
Vytvořte objekt `Workbook`, který představuje soubor Excel v paměti, a poté získejte první `Worksheet`. To vám dává plnou kontrolu před tím, než se data dotknou disku. Inicializací sešitu jako první můžete nastavit parametry – například zpracování kalendáře – před tím, než jsou buňky čteny nebo zapisovány.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

## Jak zapsat řetězec data japonské éry do buňky A1?
`Cell` je objekt, který drží hodnotu jedné buňky Excelu.  
Vložte řetězec staré éry „Reiwa 3/04/01“ do buňky A1. Toto napodobuje hodnotu zadanou uživatelem, kterou později převedete. Zapsání řetězce nejprve vám umožní demonstrovat celý workflow konverze z textu na správný objekt data.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

## Jak povolit kalendář japonské éry pro parsování dat?
`WorkbookSettings.setUseJapaneseEraCalendar(boolean)` přepíná funkci konverze éry.  
Zapněte příznak kalendáře, aby Aspose.Cells vědělo, jak převést názvy éry na gregoriánské roky. Povolení tohoto příznaku říká výpočtovému enginu, aby interpretoval řetězce jako „Reiwa“ na odpovídající gregoriánský rok, což je nezbytné pro přesné parsování dat.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

## Jak přepočítat vzorce, aby se řetězec éry převedl na gregoriánské datum?
`Workbook.calculateFormula()` vynutí výpočet všech vzorců v sešitu.  
Spusťte výpočetní engine jednou; rozpozná vzor éry, převede jej a interně uloží gregoriánský výsledek. Poté `getDateTime()` vrátí `java.util.Date`, který můžete převést na `java.time`. Tento krok je nutný, protože řetězec éry je zpočátku považován za prostý text, dokud nejsou vzorce vyhodnoceny.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

**Očekávaný výstup**

```
2021-04-01T00:00:00.000+00:00
```

## Jak zapsat novou hodnotu zpět do stejné buňky (nebo jiné buňky)?
`Cell.putValue(Object)` zapisuje hodnotu do buňky a automaticky provádí konverzi typu.  
Přepište původní řetězec éry čistým ISO‑8601 datem při zachování stylu buňky. `putValue` rozpozná typ `LocalDateTime` a převede jej na sériové číslo Excelu. Nastavením číselného formátu zajistíte, že buňka zobrazí datum přesně tak, jak očekáváte při otevření v Excelu.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

## Kompletní funkční příklad

Všechny výše uvedené kroky jsou sloučeny do jedné Java třídy, kterou můžete zkompilovat a spustit. Vytvoří se sešit, zapíše se řetězec éry, převede se a nakonec se soubor uloží.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Spusťte třídu pomocí `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` a otevřete **output.xlsx**. Buňka A1 zobrazí převedené gregoriánské datum a konzole zaloguje hodnotu „2021‑04‑01“.

## Co když buňka již obsahuje pravé datum Excelu?
Pokud buňka již ukládá nativní datum Excelu, můžete jej přečíst přímo bez dalšího zpracování. To šetří čas, protože výpočetní engine nemusí hodnotu reinterpretovat. Stačí zkontrolovat typ buňky a získat datum.

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

## Jak zpracovat celý sloupec řetězců éry?
Když mnoho buněk obsahuje řetězce éry, iterujte přes použité rozmezí a aplikujte stejnou konverzní logiku na každou buňku. Tento dávkový přístup snižuje režii oproti zpracování buněk jednotlivě. Nezapomeňte před smyčkou povolit kalendář japonské éry a po zpracování jednou přepočítat.

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

## Můžu později vypnout zpracování japonské éry?
Po dokončení zpracování relevantních buněk můžete příznak konverze éry vypnout. Vypnutí obnoví výchozí chování parsování pro všechny následné operace. To je užitečné, pokud později v tomtéž sešitu potřebujete pracovat se standardními daty.

```java
settings.setUseJapaneseEraCalendar(false);
```

Nezapomeňte po změně nastavení znovu přepočítat, pokud po zápisu dat měníte příznak.

## Profesionální tipy a úskalí

* **Výkon:** Povolení kalendáře japonské éry přidává jen malý overhead. Přepínejte jej jen pro buňky, které vyžadují konverzi, a pak ho vypněte.  
* **Vědomí locale:** Řetězec éry musí přesně odpovídat vzoru „EraName yy/MM/dd“. Překlepy (např. „Rewa“) ponechají buňku jako prostý text.  
* **Formát ukládání:** `Workbook.save("output.xlsx")` zapíše soubor XLSX. Pro starší binární formát použijte `"output.xls"`, ale uvědomte si, že některé pokročilé funkce – jako parsování éry – mohou být omezené.

## Často kladené otázky

**Q: Funguje tento přístup i s jinými kulturními kalendáři (Thai, Hijri)?**  
A: Ano – Aspose.Cells poskytuje podobné příznaky pro thajský buddhistický a hijri kalendář; povolte příslušné nastavení a přepočítejte.

**Q: Můžu číst data z heslem chráněného sešitu?**  
A: Načtěte sešit s parametrem hesla a pak postupujte stejně; příznak kalendáře funguje beze změny.

**Q: Existuje limit na počet řádků, které mohu zpracovat?**  
A: Aspose.Cells zvládne miliony řádků; data streamuje, aby udržel nízkou spotřebu paměti, zejména když je `setUseJapaneseEraCalendar` přepínán po dávkách.

**Q: Jak zachovat existující styly buněk při přepisování data?**  
A: Před voláním `putValue` získejte objekt `Style` buňky a po zápisu jej znovu aplikujte.

**Q: Potřebuji komerční licenci pro produkční použití?**  
A: Ano, pro produkční nasazení je vyžadována platná licence Aspose.Cells; k vyzkoušení je k dispozici bezplatná zkušební verze.

## Závěr

Nyní víte **jak číst Excel** data, která používají notaci japonské éry, a jak **zapsat hodnotu do excel** buněk s odpovídajícím formátováním. Povolením `setUseJapaneseEraCalendar(true)` a vynucením přepočtu vzorců Aspose.Cells propojí staré řetězce éry s moderními gregoriánskými daty během několika řádků Javy. Vyzkoušejte rozšíření tohoto vzoru na jiné kulturní kalendáře nebo dávkové zpracování velkých sešitů – stejný workflow enable‑recalculate‑read/write funguje univerzálně.

Máte problém s formátem data, který se vám nedaří rozluštit? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné programování!

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")
[Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl ovládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [How to Implement Recursive Cell Calculation in Aspose.Cells Java for Enhanced Excel Automation](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

--- 

**Poslední aktualizace:** 2026-10-07  
**Testováno s:** Aspose.Cells 23.9.0  
**Autor:** Aspose

## Související tutoriály

- [aspose cells performance: Retrieve Excel Cell Data with Java](/cells/java/cell-operations/aspose-cells-java-data-retrieval-excel/)
- [Change Excel 1904 date system with Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Master Java File Handling with Aspose.Cells: Read, Write & Process Data Efficiently](/cells/java/workbook-operations/java-file-handling-aspose-cells-read-write-process/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}