---
category: general
date: 2026-06-30
description: Řazení unikátních hodnot v Excelu pomocí Javy. Naučte se nastavit vzorec,
  přepočítat vzorce a vytvořit unikátní seznam v Excelu s Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: cs
og_description: Třídění unikátních hodnot v Excelu pomocí Javy. Tento návod ukazuje,
  jak nastavit vzorec, přepočítat vzorce a během několika minut vytvořit unikátní
  seznam v Excelu.
og_title: Řazení unikátních hodnot v Excelu – Java tutoriál pro pole vzorců
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Řazení unikátních hodnot v Excelu – Kompletní Java průvodce nastavením maticových
  vzorců
url: /cs/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Řazení unikátních hodnot v Excelu – Kompletní Java průvodce nastavením pole vzorců

Už jste se někdy zamysleli, jak **seřadit unikátní hodnoty v Excelu** bez tahání vzorců? Nejste v tom sami. V mnoha reportovacích scénářích potřebujete čistý, abecedně seřazený seznam jedinečných položek a provádět to ručně je obtížné.  

Dobrá zpráva? Několika řádky Java kódu můžete **nastavit pole vzorce** v listu, poté **přepočítat vzorce**, aby se rozšířený rozsah vyplnil automaticky. V tomto tutoriálu projdeme vše – od vytvoření sešitu až po generování unikátního seznamu ve stylu Excelu – takže můžete řešení vložit přímo do své aplikace.

## Co tento tutoriál pokrývá

- Nastavení Java projektu s Aspose.Cells (knihovna, která pohání ukázkový kód).  
- Použití funkcí `SORT` a `UNIQUE` společně k **vytvoření unikátního seznamu v Excelu**.  
- Programové aplikování **pole vzorce** na buňku.  
- Spuštění výpočtu, aby krok **jak přepočítat vzorce** proběhl okamžitě.  
- Ověření výstupu a ladění řešení pro okrajové případy, jako jsou prázdné buňky nebo nespojitá oblast.

Na konci tohoto průvodce budete schopni vložit připravenou metodu do libovolné Java služby, která potřebuje exportovat čisté Excel tabulky.

> **Pro tip:** Pokud už používáte Maven, přidání Aspose.Cells jako závislosti vám ušetří ruční manipulaci s JAR soubory.

---

## Požadavky

| Požadavek | Proč je důležitý |
|-----------|-------------------|
| Java 8 nebo novější | Aspose.Cells cílí na Java 8+. |
| Maven (nebo Gradle) | Zjednodušuje správu závislostí. |
| Aspose.Cells pro Java | Poskytuje třídy `Workbook`, `Worksheet` a API pro vzorce, které použijeme. |
| Základní znalost Excel funkcí | Porozumění `SORT` a `UNIQUE` vám pomůže kód přizpůsobit. |

> *Pokud ještě nemáte Aspose.Cells, přidejte následující do svého `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Krok 1: Vytvoření nového sešitu (Zde začíná nastavení vzorce)

Nejprve potřebujeme prázdný sešit. Představte si ho jako prázdné plátno, na které později **nastavíme pole vzorce** v buňce `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Proč vytvářet nový sešit?*  
> Zaručuje čisté prostředí, vyhýbá se skrytým vzorcům, které by mohly narušit naše testovací data.

---

## Krok 2: Naplnění ukázkových dat (Volitelné, ale užitečné)

Aby byl výsledek jasně viditelný, naplňme sloupec **B** několika duplicitními položkami.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Proč použít sloupec B?*  
> Vzorec, který napíšeme, odkazuje na `B1:B10`, takže umístění dat tam odpovídá klasickému Excel příkladu.

---

## Krok 3: Nastavení pole vzorce, který **seřadí unikátní hodnoty v Excelu**

Teď se děje magie. Kombinujeme `UNIQUE` (odstraní duplicity) s `SORT` (seřadí je abecedně). Výsledný výraz je **pole vzorce**, což znamená, že se automaticky rozšíří do sousedních buněk.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Jak to funguje

- `UNIQUE(B1:B10)` prohledá oblast a vrátí svislé pole odlišných řetězců.  
- `SORT(...)` vezme toto pole a seřadí jej vzestupně.  
- Zabalíme celý výraz do `=` a zavoláme `setFormulaArray`, což Aspose.Cells řekne, aby výsledek považoval za **rozšířené pole**, stejně jako v Excelu.

> **Poznámka:** Pokud používáte starší verzi Excelu, která nemá `SORT` nebo `UNIQUE`, můžete se vrátit k `SORT(UNIQUE(...))` s funkcí **LET** nebo použít starší pole vzorců (`=INDEX(...)`). Tento tutoriál se zaměřuje na moderní dynamické pole, protože je to nejčistší způsob, jak **vytvořit unikátní seznam v Excelu** dnes.

---

## Krok 4: Přepočítání vzorců, aby se rozšířený rozsah naplnil

Po vložení vzorce sešit automaticky nevyhodnotí. Zde přichází na řadu krok **jak přepočítat vzorce**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Volání `calculateFormula()` nutí Aspose.Cells spustit Excel engine a vyplnit buňky `A1`, `A2`, … seřazenými unikátními hodnotami.

> *Proč nespoléhat na líné vyhodnocování?*  
> V serverovém kontextu často potřebujete data připravená k exportu (CSV, PDF, atd.) hned po výpočtu, takže explicitní volání zaručuje konzistenci.

---

## Krok 5: Ověření výsledku (Volitelné ladění)

Vždy je dobré vytisknout rozšířené hodnoty do konzole – zejména když se učíte novému API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Spuštěním programu se vypíše:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Otevřete `SortedUniqueValues.xlsx` a uvidíte stejná data rozšířená od `A1` dolů.

---

## Řešení okrajových případů

### Prázdné buňky ve zdrojové oblasti

Pokud `B1:B10` obsahuje prázdné buňky, `UNIQUE` je bude považovat za samostatnou položku. Pro ignorování prázdných buněk obalte oblast funkcí `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Nespojitá data

Když jsou vaše data v několika sloupcích, můžete je spojit pomocí `CHOOSE` nebo `TEXTJOIN` před aplikací `UNIQUE`. Například:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Tyto úpravy ukazují flexibilitu **jak nastavit vzorec** pro složitější scénáře.

---

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je kompletní, spustitelný Java program. Zkopírujte jej do svého IDE, přidejte závislost Aspose.Cells a spusťte *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Očekávaný výstup** (zobrazený v konzoli) odpovídá seřazenému, deduplikovanému seznamu, o kterém jsme mluvili. Otevřením vygenerovaného Excel souboru uvidíte stejné hodnoty rozšířené od `A1` dolů.

---

## Často kladené otázky

**Q: Funguje to i se staršími verzemi Excelu (před Office 365)?**  
A: Funkce `SORT` a `UNIQUE` jsou součástí dynamického pole zavedeného v Excel 365. Pro starší soubory byste museli použít klasické pole vzorců jako `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells je stále dokáže vyhodnotit, ale syntaxe je podstatně verbóznější.

**Q: Můžu nastavit pole vzorce na jinou oblast než `A1`?**  
A: Samozřejmě. Stačí změnit adresu v `cells.get("A1")`. Rozšířené pole vždy začne v buňce, kterou specifikujete, a rozšíří se doprava a dolů podle potřeby.

**Q: Co když jsou moje zdrojová data větší než `B1:B10`?**  
A: Nahraďte statickou oblast dynamickou, např. `B:B` nebo pojmenovanou oblast. Vzorec pak bude `=SORT(UNIQUE(B:B))`. Buďte opatrní s odkazem na celý sloupec u velmi velkých listů; může to ovlivnit výkon.

---

## Závěr

Právě jsme probrali **jak nastavit vzorec** v Javě pro **seřazení unikátních hodnot v Excelu**, jak **přepočítat vzorce** a jak **vytvořit unikátní seznam v Excelu** pomocí výkonného API Aspose.Cells. Kroky jsou jednoduché: vytvořit sešit, naplnit data, aplikovat pole vzorce, spustit výpočet a ověřit výsledek.  

Odtud můžete rozšířit – přidat podmíněné formátování, export do PDF nebo integrovat metodu do webové služby, která poskytuje připravené reporty. Hlavní myšlenka zůstává stejná: nechte Excelové funkce udělat těžkou práci a nechte Javu orchestraci procesu.

Jste připraveni posunout svou automatizaci Excelu na vyšší úroveň? Vyzkoušejte výměnu `SORT` za `SORTBY` pro řazení podle sekundárního sloupce, nebo experimentujte s `FILTER`, abyste vyloučili řádky, které nesplňují obchodní pravidla. Možnosti jsou prakticky neomezené.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}