---
category: general
date: 2026-06-21
description: Jak použít WRAPCOLS s Aspose.Cells Java k převodu pole na řádky, zápisu
  vzorce do buňky a naplnění buněk vzorcem – krok za krokem průvodce.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: cs
og_description: Jak použít WRAPCOLS v Javě s Aspose.Cells k převodu pole na řádky,
  zápisu vzorce do buňky a naplnění buněk vzorcem – vše v jednom průvodci.
og_title: Jak použít WRAPCOLS v Javě – Kompletní příklad WRAPCOLS v Excelu
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Jak použít WRAPCOLS v Javě – Kompletní příklad WRAPCOLS v Excelu
url: /cs/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít WRAPCOLS v Javě – Kompletní příklad Excel WRAPCOLS

Už jste se někdy zamysleli **jak použít WRAPCOLS**, když potřebujete převést jednoduché pole na přehlednou tabulku v Excelu? Nejste v tom sami. Mnoho vývojářů narazí na problém, když poprvé uvidí funkci `WRAPCOLS` a pomyslí si: „Jak vlastně zapíšu tento vzorec do buňky z Javy?“ Dobrá zpráva? Je to celkem jednoduché, jakmile znáte správné kroky.

V tomto tutoriálu projdeme plně spustitelný příklad Aspose.Cells pro Javu, který **převádí pole na řádky**, zapisuje vzorec přímo do buňky a ukazuje vám, jak **naplnit buňky vzorcem** pro reálné scénáře. Na konci budete mít jasnou představu o **příkladu excel wrapcols** a budete připraveni jej přizpůsobit svým projektům.

## Požadavky

- Java 17 nebo novější (kód funguje s jakýmkoli aktuálním JDK).
- Knihovna Aspose.Cells pro Java (můžete stáhnout nejnovější JAR z Maven Central).
- Základní znalost syntaxe Javy a Excelových vzorců.
- IDE nebo jednoduchý textový editor – žádné speciální nástroje nejsou potřeba.

Máte vše? Skvělé, pojďme začít.

## Krok 1: Nastavení projektu a načtení sešitu

Nejprve vytvořte nový Maven (nebo Gradle) projekt a přidejte závislost Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Nyní můžeme načíst existující sešit (nebo vytvořit nový) a získat první list:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Proč načítáme sešit** – Aspose.Cells pracuje s paměťovou reprezentací souboru Excel. Načtením (nebo vytvořením) sešitu získáme přístup k buňkám, řádkům a vzorcům, což je nezbytné pro jakoukoli operaci **zapsat vzorec do buňky**.

## Krok 2: Vložení vzorce WRAPCOLS do buňky

Jádrem tutoriálu je funkce `WRAPCOLS`. Přijímá jednorozměrné pole a „zabalí“ jej do zadaného počtu sloupců, přičemž automaticky rozlévá zbytek do nových řádků. Zde je syntaxe, kterou použijeme:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Všimněte si, že vzorec je prostý řetězec předaný metodě `setFormula`. Aspose.Cells provádí těžkou práci – parsuje vzorec, vyhodnocuje jej a rozlévá výsledky do listu. Toto je nejpřímější způsob, jak **naplnit buňky vzorcem** bez ručního procházení řádků a sloupců.

### Co vzorec dělá

- `{1,2,3}` – literální pole obsahující tři čísla.
- `2` – počet sloupců na řádek.
- Výsledek:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (prázdná)

Pokud byste chtěli tři sloupce, stačí změnit druhý argument na `3` a pole by vyplnilo jeden řádek.

## Krok 3: Uložení sešitu a ověření výstupu

Nyní, když je vzorec v **A1**, uložme sešit na disk, abyste jej mohli otevřít v Excelu a vidět rozložení:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Otevřete `output.xlsx` a uvidíte přesně to, co komentář popisoval – dva sloupce v prvním řádku a zbývající hodnotu ve druhém řádku. To je podstata **příkladu excel wrapcols**.

## Krok 4: Rozšíření příkladu – převod větších polí

Skutečné projekty zřídka pracují jen se třemi čísly. Předpokládejme, že máte větší kolekci, např. `{10,20,30,40,50,60,70}` a chcete tři sloupce na řádek. Zde je, jak byste upravili kód:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Nyní se rozložení začne v **C5**, což vytvoří:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

To ukazuje, jak můžete **převést pole na řádky** dynamicky, pouhým úpravou řetězce vzorce. Žádné smyčky, žádné ruční přiřazování buněk – Aspose.Cells se postará o zbytek.

## Krok 5: Řešení hraničních případů a běžných úskalí

### 1. Prázdná pole

Pokud je literál pole prázdný (`{}`), `WRAPCOLS` vrátí chybu `#VALUE!`. Aby nedošlo k poškození listu, chraňte generování vzorce:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Není‑číslicová data

`WRAPCOLS` funguje také s textem. Například `WRAPCOLS({"A","B","C","D"},2)` vytvoří dvousloupcové rozložení řetězců. Jen nezapomeňte uzavřít řetězce do uvozovek uvnitř literálu pole.

### 3. Kompatibilita

Funkce `WRAPCOLS` je dostupná v Excelu 365 a Excelu 2019+ (Office 2019, Excel pro web). Pokud potřebujete podporovat starší verze, budete muset přejít na ruční smyčkování nebo použít jinou funkci kompatibilní se spill.

## Krok 6: Praktické tipy a profesionální triky

- **Pro tip:** Použijte `Cell.setFormulaLocal`, pokud potřebujete lokálně specifický oddělovač (čárka vs středník) podle regionálního nastavení uživatele.
- **Dejte pozor na:** Přepisování existujících dat. Oblast spill přepíše jakýkoli obsah, který již v cílovém rozsahu existuje.
- **Poznámka k výkonu:** Nastavení vzorce je levné; těžká práce nastává při **ukládání** nebo **přepočítávání** sešitu. Pokud generujete tisíce vzorců, zvažte vypnutí automatického výpočtu (`wb.calculateFormula()` později) pro zrychlení zpracování.

## Kompletní funkční příklad

Níže je kompletní, připravená ke spuštění třída Java, která zahrnuje vše, o čem jsme mluvili:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Očekávaný výstup:** Otevřete `output.xlsx` a uvidíte tři odlišné spill oblasti:

- **A1:B2** – čísla 1‑3 zabalená do dvou sloupců.
- **C5:E7** – čísla 10‑70 zabalená do tří sloupců.
- **G1:H2** – názvy ovoce zabalené do dvou sloupců.

## Závěr

Právě jsme probrali **jak použít WRAPCOLS** s Aspose.Cells pro Javu, ukázali vám, jak **převést pole na řádky**, **zapsat vzorec do buňky** a **naplnit buňky vzorcem** čistým, opakovatelným způsobem. Tento přístup eliminuje nudné smyčkování, využívá nativní spill chování Excelu a udržuje váš kód stručný.

Jste připraveni na další výzvu? Zkuste kombinovat `WRAPCOLS` s dynamickými zdroji dat – třeba načíst hodnoty z databáze, vytvořit řetězec pole za běhu a nechat Excel provést rozložení. Můžete také experimentovat s dalšími spill funkcemi jako `SEQUENCE` nebo `FILTER` a vytvořit tak ještě bohatší reporty.

Pokud narazíte na problémy, zanechte komentář níže nebo prozkoumejte rozsáhlou dokumentaci Aspose. Šťastné programování a užívejte si sílu moderních Excelových vzorců přímo z Javy! 

![příklad použití wrapcols](/images/wrapcols-demo.png "jak použít wrapcols v Javě – screenshot rozložených dat")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vybrat rozsahy buněk v Excelu pomocí Aspose.Cells pro Java (průvodce 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [Jak nastavit aktivní buňku v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Jak vložit řádky do Excel sešitů pomocí Aspose.Cells pro Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}