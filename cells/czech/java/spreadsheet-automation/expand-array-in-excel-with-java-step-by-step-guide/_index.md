---
category: general
date: 2026-07-03
description: Naučte se, jak rozšířit pole v Excelu pomocí Javy. Tento tutoriál pokrývá
  rozšíření pole do řádků, jak použít expand a jak efektivně vložit vzorec.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: cs
og_description: Rozšiřte pole v Excelu pomocí Javy. Postupujte podle tohoto průvodce
  a naučte se, jak použít rozšíření, nastavit vzorec v buňce a okamžitě rozšířit pole
  do řádků.
og_title: Rozšíření pole v Excelu pomocí Javy – Kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Rozšíření pole v Excelu pomocí Javy – krok za krokem
url: /cs/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozšíření pole v Excelu pomocí Javy – Kompletní programovací průvodce

Už jste se někdy zamysleli, jak **expand array in Excel** bez ručního tahání buněk? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují programově vygenerovat dynamický rozsah – zejména když je nová funkce Excel `EXPAND` ještě čerstvá. V tomto průvodci vám přesně ukážeme **how to use EXPAND**, vložíme vzorec do listu a necháme výsledek rozlévat do požadovaných řádků. Na konci budete schopni **expand array to rows** v jedné řádce Java kódu.

Projdeme kompletním, spustitelným příkladem pomocí knihovny Aspose.Cells for Java. Žádné vágní odkazy, jen konkrétní kód, který můžete zkopírovat‑vložit, zkompilovat a spustit. Během toho probereme, proč je každý krok důležitý, pokryjeme okrajové případy jako nesouvislá pole a posypeme pár profesionálních tipů, které nenajdete v oficiální dokumentaci. Připravení? Ponořme se.

## Požadavky

* Java 17 (nebo jakýkoli aktuální JDK) nainstalována.
* Maven nebo Gradle pro správu závislostí.
* Platná licence Aspose.Cells for Java (zdarma zkušební verze funguje pro testování).
* Základní znalost Excelových vzorců – pokud jste už dříve používali `VLOOKUP` nebo `SUMIF`, jste připraveni.

Pokud vám některý z těchto bodů není známý, zastavte se a nejprve je nastavte; zbytek tutoriálu předpokládá, že jsou připravené.

## Krok 1: Nastavte svůj Maven projekt a přidejte Aspose.Cells

Aby vše bylo přehledné, vytvořte nový Maven projekt s názvem `ExpandArrayDemo`. Přidejte závislost Aspose.Cells do souboru `pom.xml`:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Pokud používáte Gradle, stejná závislost vypadá takto `implementation 'com.aspose:aspose-cells:23.12'`.

Jakmile Maven dokončí stahování, jste připraveni psát Java kód, který **sets formula in cell**.

## Krok 2: Vytvořte Workbook a přistupte k prvnímu listu

První část kódu odráží úryvek, který jste již viděli, ale přidáme několik kontrol a komentářů, abyste pochopili *proč* za každým řádkem.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Proč je to důležité:* Vytvoření instance `Workbook` alokuje interní struktury, které Aspose potřebuje pro správu buněk, vzorců a stylů. Přístup k prvnímu listu je nejčastější vstupní bod, zejména když jen experimentujete.

## Krok 3: Vložte vzorec EXPAND – “Jak vložit vzorec”

Nyní přichází jádro tutoriálu: **how to insert formula**, který rozšiřuje pole. Funkce Excel `EXPAND` přijímá tři argumenty – zdrojové pole, požadovaný počet řádků a požadovaný počet sloupců. V našem případě chceme rozšířit `{1,2,3}` na **5 řádků** a **1 sloupec**.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

Všimněte si, že jsme použili `putFormula` místo `putValue`. To říká Aspose, aby řetězec považoval za skutečný Excelový vzorec, nikoli za obyčejný text. Metoda `putFormula` automaticky parsuje řetězec a interně ukládá strom vzorce.

### Proč použít EXPAND?

`EXPAND` odstraňuje únavný krok tahání výplňové úchyty. Také funguje s dynamickými poli, což znamená, že pokud se vaše zdrojové pole změní, rozlévaný rozsah se automaticky aktualizuje. To je zvláště užitečné při programovém generování reportů.

## Krok 4: Vynutit výpočet – Materializace výsledku

Když *set formula in cell* pomocí API, sešit se automaticky nepřepočítá. Musíte spustit výpočet, aby se pole **expanded to rows** a hodnoty se objevily v listu.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Pokud tento krok přeskočíte, otevření vygenerovaného `.xlsx` v Excelu zobrazí vzorec, ale ne rozlévané hodnoty, dokud nestisknete **F9**. Voláním `calculate()` zajistíte, že je sešit připraven k okamžitému použití.

## Krok 5: Uložte sešit a ověřte výstup

Nakonec zapište sešit do souboru a případně vytiskněte rozlévané hodnoty do konzole pro ověření.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Když spustíte program, měli byste vidět výstup v konzoli:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel vyplní zbývající řádky nulami, protože zdrojové pole mělo jen tři prvky. To je výchozí chování `EXPAND`. Pokud dáváte přednost prázdným buňkám místo nul, můžete pole zabalit do `IFERROR` nebo použít triky s `CHOOSE` – více o tom v sekci „Advanced Variations“ níže.

## Pokročilé varianty a okrajové případy

### 1. Rozšíření horizontálního pole na více sloupců

Pokud potřebujete **expand array to rows** *a* sloupce, stačí změnit třetí argument:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Nyní se rozsah rozlévá do bloku 5 × 3, chybějící buňky jsou vyplněny nulami.

### 2. Použití pojmenovaného rozsahu jako zdroje

Místo doslovného `{1,2,3}` můžete odkazovat na pojmenovaný rozsah, který se může měnit za běhu:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

Ujistěte se, že `MySourceRange` existuje (můžete jej vytvořit pomocí `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")`).

### 3. Zpracování nečíselných dat

`EXPAND` funguje také s textem. Například:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

### 4. Vyhnutí se vyplňování nulami pomocí `IFERROR`

Pokud raději vidíte prázdné buňky místo nul, zabalte `EXPAND` do `IFERROR`:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Nyní řádky 4 a 5 budou skutečně prázdné.

## Běžné úskalí a jak se jim vyhnout

| Úskalí | Proč k tomu dochází | Řešení |
|---------|----------------|-----|
| **Vzorec není přepočítán** | Zapomenutí volání `ws.getCells().calculate()` | Vždy volejte `calculate()` po `putFormula`. |
| **Nuly místo prázdných buněk** | `EXPAND` ve výchozím nastavení doplňuje nuly | Použijte `IFERROR(..., "")` nebo zabalte do `CHOOSE`. |
| **Nesprávná adresa buňky** | Použití `"A0"` nebo `"1A"` | Adresy v Excelu začínají od 1; Aspose očekává styl `"A1"`. |
| **Neshoda verzí knihovny** | Použití staré verze Aspose.Cells, která nepodporuje `EXPAND` | Aktualizujte na nejnovější verzi (23.12 v době psaní). |

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program připravený ke kopírování a vložení. Uložte jej jako `ExpandArrayDemo.java`, zkompilujte a spusťte.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Spuštěním tohoto programu vznikne soubor Excel, kde **buňka A1** nyní obsahuje vzorec `EXPAND` a řádky 1‑5 sloupce A zobrazují `1, 2, 3, 0, 0`. Otevřete soubor v Excelu a okamžitě uvidíte stejný výsledek – žádné ruční tahání není potřeba.

## Závěr

Právě jste se naučili, jak **expand array in Excel** pomocí Javy, **how to use EXPAND**, a přesné kroky k **set formula in cell** a **expand array to rows** programově. Využitím Aspose.Cells se vyhnete nešikovným UI trikům a necháte kód udělat těžkou práci. Ať už budujete reportingový engine, automatizovaný nástroj pro zadávání dat, nebo vlastní generátor tabulek, tato technika vám ušetří nespočet hodin.

Co dál? Zkuste nahradit statické pole dynamickým rozsahem načteným z jiného listu, experimentujte s rozléváním do více sloupců, nebo zkombinujte `EXPAND` s `FILTER` pro výkonné transformace dat. Možnosti jsou neomezené a nyní máte pevný základ, na kterém můžete stavět.

Máte otázky nebo chcete sdílet zajímavý případ použití? Napište

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vložit řádky do Excel sešitů pomocí Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [Jak vložit sloupec v Excelu pomocí Aspose.Cells for Java – komplexní průvodce](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [Jak vybrat rozsahy buněk v Excelu pomocí Aspose.Cells for Java (průvodce 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}