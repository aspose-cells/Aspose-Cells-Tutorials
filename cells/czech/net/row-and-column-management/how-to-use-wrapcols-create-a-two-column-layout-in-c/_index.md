---
category: general
date: 2026-02-15
description: Jak použít WRAPCOLS k vytvoření dvou sloupcového rozvržení, přidat vzorec
  a vygenerovat sekvenční pole v C# listech – krok za krokem návod.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: cs
og_description: Jak použít WRAPCOLS k vytvoření dvousloupcového rozvržení, přidání
  vzorců a generování sekvenčního pole v listu C# – kompletní průvodce.
og_title: 'Jak použít WRAPCOLS: Dvou‑sloupcové rozložení v C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Jak použít WRAPCOLS: Vytvořte dvousloupcové rozložení v C#'
url: /cs/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

content.

Be careful to preserve markdown formatting, code block placeholders unchanged.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít WRAPCOLS: Vytvořit dvousloupcové rozložení v C#

Už jste se někdy ptali, **jak použít WRAPCOLS**, když potřebujete rychlý dvousloupcový pohled v listu stylu Excel? Nejste v tom sami. Mnoho vývojářů narazí na problém, když se snaží rozdělit vygenerovaný seznam do úhledných sloupců, aniž by psali smyčku pro každou buňku. Dobrá zpráva? S funkcí `WRAPCOLS` můžete vložit jediný vzorec do `A1` a nechat Excel (nebo kompatibilní engine) udělat těžkou práci.

V tomto tutoriálu si projdeme **jak přidat vzorec**, který vytvoří **dvousloupcové rozložení**, ukážeme vám **jak dynamicky vytvořit sloupce** a dokonce **vygenerovat pole sekvence** za běhu. Na konci budete mít plně spustitelný úryvek C#, který můžete vložit do svého projektu, spustit a okamžitě uvidíte úhledný dvousloupcový blok.

## Co se naučíte

- Účel funkce `WRAPCOLS` a proč je lepší alternativou k ručnímu iterování.  
- Jak **přidat vzorec** do buňky listu pomocí C#.  
- Jak vygenerovat pole sekvence pomocí `SEQUENCE` a předat jej funkci `WRAPCOLS`.  
- Tipy pro přepočítání listu, aby se vzorec vyhodnotil okamžitě.  
- Zpracování okrajových případů (např. prázdné listy, vlastní počet sloupců).

Žádné externí knihovny mimo standardní balíček pro zpracování Excelu nejsou potřeba – použijeme **ClosedXML** pro jeho přímé API, ale koncepty lze přenést i na EPPlus, SpreadsheetGear nebo dokonce Google Sheets přes jeho API.

---

## Předpoklady

- .NET 6.0 nebo novější (kód se kompiluje na .NET Core i .NET Framework).  
- Odkaz na **ClosedXML** (`dotnet add package ClosedXML`).  
- Základní znalost C# – měli byste být pohodlní s `using` příkazy a inicializací objektů.  

Pokud už máte otevřený sešit, můžete přeskočit část vytváření souboru a rovnou přejít k sekci s vzorcem.

---

## Krok 1: Nastavení listu (Jak vytvořit sloupce)

Nejprve potřebujeme objekt `Worksheet`, se kterým budeme pracovat. V ClosedXML jej získáte z `XLWorkbook`. Níže uvedený úryvek vytvoří nový sešit, přidá list pojmenovaný *Demo* a získá referenci pojmenovanou `worksheet` pro přehlednost.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Proč přejmenovat?**  
> Udržení krátkého názvu proměnné (`worksheet`) usnadňuje čtení následného kódu, zejména když řetězíte více operací. Také to odráží pojmenovací styl, který uvidíte ve většině dokumentace, a snižuje kognitivní zátěž.

---

## Krok 2: Zapsání vzorce (Jak přidat vzorec + Vytvořit pole sekvence)

Nyní přichází kouzelný řádek. Vložíme vzorec do buňky **A1**, který dělá dvě věci:

1. **Vytvoří pole sekvence** šesti čísel (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Zabalí tato čísla do dvou sloupců** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Co se děje?**  
> `SEQUENCE(6)` vytvoří vertikální pole `{1;2;3;4;5;6}`. `WRAPCOLS` pak vezme toto pole a „zabalí“ ho do zadaného počtu sloupců – v tomto případě **2**. Výsledkem je blok o 3 řádcích × 2 sloupcích, který vypadá takto:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Pokud změníte druhý argument na **3**, získáte třísloupcové rozložení. To je podstata **jak vytvořit sloupce** za běhu bez ručních smyček.

---

## Krok 3: Přepočítání listu (Zajištění vyhodnocení vzorce)

ClosedXML automaticky nevyhodnocuje vzorce, když je zapíšete. Musíte zavolat `Calculate()` na sešit (nebo na konkrétní list), aby se vynutilo vyhodnocení.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Tip:** Pokud pracujete s velkými sešity, volejte `Calculate()` jen na listech, které se skutečně změnily. Ušetříte tak paměť a zrychlíte zpracování.

Když otevřete `WrapColsDemo.xlsx`, uvidíte dvousloupcové rozložení pěkně vyplněné v **A1:B3**. Nebyl potřeba žádný další kód pro procházení řádků nebo sloupců – `WRAPCOLS` vše zvládl.

---

## Krok 4: Ověření výstupu (Co očekávat)

Po spuštění programu otevřete vygenerovaný soubor. Měli byste vidět:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Pokud se čísla objeví vertikálně (tj. všechna ve sloupci A), zkontrolujte, že jste volali `worksheet.Calculate()` **po** nastavení vzorce. Některé enginy také vyžadují `workbook.Calculate()`; úryvek výše funguje pro vestavěný evaluátor ClosedXML.

---

## Běžné varianty a okrajové případy

### Změna počtu sloupců

Pro **vytvoření dvousloupcového rozložení** s jiným počtem řádků stačí upravit velikost `SEQUENCE` nebo druhý argument funkce `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Tím vznikne blok o 4 řádcích × 3 sloupcích (12 čísel rozdělených do tří sloupců).

### Použití dynamického počtu sloupců

Pokud počet sloupců pochází z proměnné, vložte jej pomocí řetězcové interpolace:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Nyní máte **jak přidat vzorec**, který se přizpůsobí za běhu.

### Prázdné listy

Pokud je list prázdný, `Calculate()` stále funguje – vzorec naplní buňky počínaje A1. Pokud však později smažete řádky/sloupce, které protínají výstupní oblast, můžete vidět chyby `#REF!`. Aby se tomu předešlo, nejprve vymažte cílový rozsah:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Kompatibilita

`WRAPCOLS` a `SEQUENCE` jsou součástí **Dynamic Array** funkcí Excelu, zavedených v Office 365. Pokud cílíte na starší verze Excelu, tyto funkce neexistují a budete potřebovat ruční smyčku. Evaluátor ClosedXML napodobuje nejnovější chování Excelu, takže je bezpečný pro moderní prostředí.

---

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Očekávaný výsledek:** Otevřením *WrapColsDemo.xlsx* se zobrazí úhledné dvousloupcové rozložení s čísly 1‑6 uspořádanými, jak bylo popsáno výše.

---

## Závěr

Probrali jsme **jak použít WRAPCOLS** k **vytvoření dvousloupcového rozložení**, ukázali **jak přidat vzorec** programově a viděli, jak `SEQUENCE` umožňuje **vygenerovat pole sekvence** bez smyčky. Využitím dynamických polí Excelu z C# můžete udržet svůj kód stručný, čitelný a udržovatelný.

Dále můžete zkoumat:

- **Vytváření dynamického počtu řádků** pomocí `ROWS` nebo `COUNTA`.  
- **Styling výstupu** (okraje, formáty čísel) pomocí styling API ClosedXML.  
- **Export do CSV** po vytvoření rozložení, pro následné zpracování.

Vyzkoušejte to, pozměňte počet sloupců a uvidíte, jak rychle můžete prototypovat složité tabulky. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}