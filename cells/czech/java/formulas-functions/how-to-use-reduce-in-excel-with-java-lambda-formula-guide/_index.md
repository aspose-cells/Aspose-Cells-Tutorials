---
category: general
date: 2026-06-08
description: Jak použít reduce v Excelu s Javou pomocí Aspose.Cells. Naučte se lambda
  vzorce v Excelu, dynamické pole v Javě, jak psát lambda výrazy a součet pomocí reduce
  v přehledném krok‑za‑krokem tutoriálu.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: cs
og_description: Jak používat reduce v Excelu s Javou. Ovládněte lambda vzorce v Excelu,
  dynamické pole v Javě a součet pomocí reduce pomocí kompletního, spustitelného příkladu.
og_title: Jak použít Reduce v Excelu s Javou – Průvodce lambda vzorci
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Jak použít Reduce v Excelu s Javou – Průvodce lambda vzorci
url: /cs/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít Reduce v Excelu s Javou – Průvodce lambda vzorci

Už jste se někdy zamýšleli **jak použít reduce** v Excelu při psaní kódu v Javě? Nejste sami. Mnoho vývojářů narazilo na problém při kombinaci nových dynamických pole funkcí Excelu s automatizací založenou na Javě a odpověď není tak kryptická, jak se na první pohled zdá.

V tomto tutoriálu projdeme konkrétním příkladem, který ukazuje **jak použít reduce** spolu s **lambda vzorcem Excel** výrazem, vše poháněno knihovnou Aspose.Cells pro Java. Na konci budete schopni generovat dynamické pole v Javě, psát lambda funkce a vypočítat **součet pomocí reduce** — bez ručního manipulování s tabulkou.

---

## Co vytvoříte

- Čerstvý sešit vytvořený kompletně v Javě.  
- Dynamické pole **EXPAND**, které vyplní buňky A1:A5 čísly 1‑5.  
- Vzorec **REDUCE**, který sečte tato čísla pomocí **lambda vzorce Excel**.  
- Uložený soubor `.xlsx`, který můžete otevřít v libovolném tabulkovém programu a ověřit výsledek.

Žádné externí makra, žádné VBA — jen čistý Java kód a moderní funkce Excelu.

## Požadavky

- Java 17 (nebo jakýkoli recentní JDK) – starší verze fungují, ale chybí vám cukr `var`.  
- Aspose.Cells pro Java (bezplatná zkušební verze funguje pro tento demo).  
- Základní znalost syntaxe Java a vzorců v Excelu.

Pokud jste noví v **dynamic arrays java**, nebojte se — tento průvodce vysvětluje každý krok.

## Krok 1: Nastavte svůj projekt a importujte Aspose.Cells

Nejprve přidejte Maven závislost Aspose.Cells do svého `pom.xml` (nebo si ručně stáhněte JAR).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Tip:** Udržujte své závislosti aktuální; novější verze zlepšují rychlost vyhodnocování vzorců, což je důležité, když **jak použít reduce** ve velkých listech.

## Krok 2: Vytvořte sešit a přistupte k prvnímu listu

Nyní vytvoříme zcela nový sešit. To je základ pro učení **jak použít reduce**, protože objekt sešitu nám poskytuje sandbox pro vkládání vzorců.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Proč je to důležité:* Třída `Workbook` abstrahuje celý soubor Excel, zatímco `Worksheet` představuje jeden list. Později uvidíte, jak **dynamic arrays java** může vyplnit mnoho buněk jedním vzorcem umístěným v A1.

## Krok 3: Vytvořte vertikální pole pomocí EXPAND

Funkce Excelu `EXPAND` může rozlévat hodnoty do rozsahu. Použijeme ji k vytvoření čísel 1 až 5 ve sloupci A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Pokud otevřete výsledný sešit, buňky A1:A5 budou obsahovat 1, 2, 3, 4, 5. To je část **dynamic arrays java** — jeden vzorec naplní celý rozsah.

## Krok 4: Napište REDUCE lambda pro součet pole

Zde odpovídáme na hlavní otázku: **jak použít reduce** v Excelu z Javy. Funkce `REDUCE` iteruje přes pole a aplikuje vámi poskytnutou lambda funkci. V našem případě sečteme čísla.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Rozložme to:

- `0` – počáteční hodnota akumulátoru (`acc`).  
- `A1:A5` – pole, které jsme vygenerovali pomocí **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – **lambda vzorec Excel**, který přidá každý prvek (`x`) k akumulátoru (`acc`).  

Když se vzorec spustí, `B1` bude obsahovat **15**, **součet pomocí reduce** čísel 1‑5.

> **Jak napsat lambda** v Excelu? Považujte ji za anonymní funkci, kde první argumenty jsou parametry a poslední výraz je návratová hodnota. V Javě jen vložíme text; Excel engine provádí těžkou práci.

## Krok 5: Uložte sešit

Nakonec uložíme sešit na disk, abyste jej mohli otevřít v Excelu, Google Sheets nebo jakémkoli prohlížeči podporujícím `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Otevřete soubor a uvidíte:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**Součet pomocí reduce** se objeví v B1, což potvrzuje, že jsme úspěšně předvedli **jak použít reduce** spolu s **lambda vzorcem Excel** z Javy.

## Kompletní funkční příklad

Níže je kompletní, připravený Java program. Zkopírujte jej do svého IDE, upravte výstupní adresář a stiskněte **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Očekávaný výstup** po otevření `new-functions.xlsx`:

- Buňky **A1:A5** obsahují `1, 2, 3, 4, 5`.  
- Buňka **B1** zobrazuje `15`, což potvrzuje **součet pomocí reduce**.

## Časté otázky a okrajové případy

### Co když potřebuji horizontální pole místo vertikálního?

Swap the column/row arguments in `EXPAND`. For a horizontal spill across B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Můžu použít REDUCE k násobení místo součtu?

Absolutely. Just change the lambda body:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Nyní B1 zobrazí `120` (5 ! = 120).

### Podporuje Aspose.Cells vlastní LAMBDA funkce?

Ano, můžete definovat pojmenované LAMBDA funkce pomocí kolekce `Names` v sešitu a poté je volat jako jakýkoli vestavěný vzorec. To je podrobnější téma pro pozdější tutoriál o **jak napsat lambda** funkcích, které existují mimo jedinou buňku.

### Co s staršími verzemi Excelu, které nepoznávají REDUCE?

If you target Excel 2019 or earlier, the engine will return `#NAME?`. In such cases

## Co byste se měli učit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Mistrovství v Aspose.Cells Java: Jak přerušit výpočet vzorců v sešitech Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Jak převést názvy buněk Excel na indexy pomocí Aspose.Cells pro Java: krok za krokem](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Jak vytvořit a formátovat buňky Excel pomocí Aspose.Cells pro Java: krok za krokem](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}