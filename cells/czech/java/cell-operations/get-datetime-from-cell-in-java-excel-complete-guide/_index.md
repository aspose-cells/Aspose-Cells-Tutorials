---
category: general
date: 2026-06-08
description: Získejte datum a čas z buňky pomocí Aspose.Cells Java a naučte se, jak
  v několika krocích zapsat hodnotu do buňky v Excelu.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: cs
og_description: Získejte datum a čas z buňky pomocí Aspose.Cells Java. Tento tutoriál
  také ukazuje, jak efektivně zapisovat hodnotu do buňky Excelu.
og_title: Získání data a času z buňky v Java Excel – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
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
title: Získání data a času z buňky v Java Excel – kompletní průvodce
url: /cs/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání data a času z buňky v Java Excel – Kompletní průvodce

Už jste někdy potřebovali **získat datum a čas z buňky**, ale hodnota vypadá jako řetězec japonské éry? Nejste v tom sami. V mnoha starších tabulkách jsou data uložena jako „Reiwa 3/04/01“ a získání správného `java.time.LocalDateTime` z toho může připomínat dešifrování tajné zprávy.  

Naštěstí Aspose.Cells for Java dokáže konverzi provést za vás a zároveň vám ukážeme, jak **zapsat hodnotu do buňky Excelu**, abyste mohli data provádět round‑trip bez narušení logiky listu.

V tomto tutoriálu se naučíte:

* Jak vytvořit sešit a zaměřit se na konkrétní list.  
* Přesné kroky pro povolení japonského kalendáře éry při parsování.  
* Proč musíte přepočítat vzorce před načtením data.  
* Jak zapsat novou hodnotu zpět do buňky bez ztráty formátování.  

Žádné externí nástroje, žádná magie — jen čistý Java kód, který můžete dnes vložit do libovolného Maven projektu.

---

## Požadavky

* **Java 8+** (příklad používá moderní `java.time` API).  
* **Aspose.Cells for Java** ≥ 23.9.0 — přidejte závislost přes Maven nebo Gradle.  
* Základní znalost konceptů Excelu (listy, buňky, vzorce).  

Pokud vám knihovna chybí, stáhněte ji z oficiálního repozitáře Aspose:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Krok 1: Vytvořte nový sešit a přistupte k prvnímu listu

Na začátek potřebujeme čerstvý objekt `Workbook`. Představte si to jako otevření nového Excel souboru v paměti.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Proč je to důležité:*  
Programové vytvoření sešitu vám dává plnou kontrolu nad nastavením před tím, než se data dotknou souborového systému. První list (`index 0`) je místem, kde ukážeme jak čtení, tak zápis.

---

## Krok 2: Zapište řetězec japonské éry do buňky A1

Nyní **zapsáme hodnotu do buňky Excelu** A1. To odráží reálný scénář, kdy uživatel ručně zadal „Reiwa 3/04/01“.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Rychlá tip:* `putValue` je univerzální — přijímá řetězce, čísla, data i dokonce vzorce. Když předáte prostý řetězec, Aspose jej uloží přesně tak, jak je, což je pro naši ukázku ideální.

---

## Krok 3: Povolení japonského kalendáře éry pro parsování data

Ve výchozím nastavení používá Aspose.Cells gregoriánský kalendář. Abychom pochopili „Reiwa“, přepneme nastavení.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Proč to povolit?*  
Japonský kalendář mapuje názvy epoch (Reiwa, Heisei, Showa) na jejich gregoriánské ekvivalenty. Bez tohoto příznaku by knihovna řetězec považovala za prostý text a nikdy byste nedostali správný objekt `DateTime`.

---

## Krok 4: Přepočítejte vzorce, aby se řetězec éry převedl na gregoriánské datum

Aspose automaticky neparsuje řetězec na datum. Místo toho buňku po průchodu výpočtem považuje za výsledek vzorce.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Když se spustí `calculateFormula()`, engine rozpozná vzor epochy, použije japonský kalendář a interně uloží vzniklé gregoriánské datum. Volání `getDateTime()` pak vrátí `java.util.Date` (nebo jej můžete převést na `java.time`).

**Očekávaný výstup**

```
2021-04-01T00:00:00.000+00:00
```

---

## Krok 5: Zapište novou hodnotu zpět do stejné buňky (nebo do jiné buňky)

Předpokládejme, že potřebujete přepsat původní řetězec čistým ISO‑8601 datem. Zde je, jak **zapsat hodnotu do buňky Excelu** bezpečně, přičemž zachováte styl buňky.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Co se děje?*  
`putValue` rozpozná typ `LocalDateTime` a převede jej na sériové číslo Excelu. Nastavení formátu čísla zajistí, že buňka zobrazí datum přesně tak, jak očekáváte při otevření v Excelu.

---

## Kompletní funkční příklad

Spojením všech částí získáte jedinou Java třídu, kterou můžete zkompilovat a spustit. Vytvoří se sešit, zapíše se řetězec éry, převede se a nakonec se soubor uloží.

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

Spusťte to pomocí `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` a otevřete **output.xlsx**. Uvidíte, že buňka A1 zobrazuje aktuální datum, zatímco konzole vypíše převedenou hodnotu „2021‑04‑01“.

---

## Řešení okrajových případů a časté otázky

### Co když buňka již obsahuje skutečné datum Excelu?

Pokud `cell.getType()` vrátí `CellValueType.IS_DATE_TIME`, můžete krok přepočítání přeskočit a hodnotu načíst přímo:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Jak zpracovat celý sloupec řetězců éry?

Projděte použité rozmezí a jednou aplikujte stejná nastavení:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Můžu později vypnout zpracování japonské éry?

Ano — stačí přepnout příznak zpět:

```java
settings.setUseJapaneseEraCalendar(false);
```

Nezapomeňte znovu přepočítat, pokud po zápisu dat změníte nastavení.

---

## Profesionální tipy a úskalí

* **Výkon:** Povolení japonského kalendáře éry přidává malé zatížení. Pokud jej potřebujete jen pro několik buněk, zvažte nastavení zapnout, provést zpracování a pak jej vypnout.  
* **Vědomí lokality:** Řetězec éry musí přesně odpovídat vzoru „EraName yy/MM/dd“. Nesprávný pravopis „Reiwa“ (např. „Rewa“) zůstane buňkou jako prostý text.  
* **Formát ukládání:** `Workbook.save("output.xlsx")` zapisuje soubor XLSX. Použijte `"output.xls"` pokud potřebujete starší binární formát, ale uvědomte si, že některé funkce (např. parsování éry) mohou být omezené.

---

## Závěr

Nyní už víte, jak **získat datum a čas z buňky**, když zdroj používá zápis japonské éry, a také jste viděli čistý způsob, jak **zapsat hodnotu do buňky Excelu** s správným formátováním. Přepnutím `setUseJapaneseEraCalendar(true)` a vynucením přepočtu vzorců Aspose.Cells překonává propast mezi starými řetězci epoch a moderními gregoriánskými daty — vše s několika řádky Java kódu.

Co dál? Zkuste rozšířit tento vzor na další kulturní kalendáře (thajský, hijri) nebo hromadně zpracovávat velké sešity stejným přístupem. Stejné principy — povolit správný kalendář, přepočítat, pak číst/zapisovat — platí napříč všemi scénáři.

Máte problém s formátem data, který se vám nedaří rozluštit? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné kódování!  

![Příklad získání data a času z buňky](https://example.com/images/get-datetime-from-cell.png "Příklad získání data a času z buňky")


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, které vám pomůže ovládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Ovládněte datumový systém 1904 v Excelu pomocí Aspose.Cells Java pro efektivní operace s buňkami](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Jak implementovat rekurzivní výpočet buněk v Aspose.Cells Java pro vylepšenou automatizaci Excelu](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Jak převést názvy buněk Excelu na indexy pomocí Aspose.Cells pro Java: průvodce krok za krokem](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}