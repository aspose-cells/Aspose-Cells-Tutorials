---
category: general
date: 2026-03-30
description: Naučte se, jak v C# použít WRAPCOLS k vytvoření sešitu Excel, přidání
  dat do Excelu a vynucení výpočtu vzorců, a zároveň použít WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: cs
og_description: Objevte, jak použít WRAPCOLS v C# k vytvoření sešitu Excel, přidání
  dat, vynucení výpočtu vzorců a využití WRAPROWS pro maticové vzorce.
og_title: Jak používat WRAPCOLS v C# – kompletní průvodce
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak použít WRAPCOLS v C# – Vytvořte Excel sešit s funkcemi pro zalamování
url: /cs/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat WRAPCOLS v C# – Vytvořit Excel sešit s funkcemi Wrap

Už jste se někdy zamysleli **jak používat WRAPCOLS**, když automatizujete Excel pomocí C#? Nejste sami – mnoho vývojářů narazí na problém, když potřebují převést vodorovný rozsah na vertikální pole, aniž by museli psát spoustu kódu. Dobrou zprávou je, že Aspose.Cells to dělá hračkou.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje **jak používat WRAPCOLS**, jak **vytvořit Excel sešit v C# stylu**, jak **přidat data do Excelu** a dokonce jak **vynutit výpočet vzorců**, aby se výsledky objevily okamžitě. Také přidáme **jak používat WRAPROWS** pro opačnou transformaci. Na konci budete mít připravený program k spuštění a jasné pochopení, proč je každý krok důležitý.

---

![Jak používat WRAPCOLS v C# příklad](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## Co tento průvodce pokrývá

* Nastavení nového sešitu pomocí Aspose.Cells.
* Programové naplnění buněk (**add data to Excel**).
* Použití funkce `WRAPCOLS` k převodu řádku na sloupec.
* Použití `WRAPROWS` k převodu sloupce zpět na řádek (**how to use wraprows**).
* Vynucení výpočtu vzorců okamžitě (**force formula calculation**).
* Uložení souboru a kontrola výstupu.

Není potřeba žádná externí dokumentace – vše, co potřebujete, je zde.

---

## Jak používat WRAPCOLS v C# – Krok za krokem implementace

Níže je celý zdrojový soubor. Klidně jej zkopírujte a vložte do nového konzolového projektu, přidejte NuGet balíček Aspose.Cells a stiskněte **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Proč je každý řádek důležitý

| Krok | Vysvětlení |
|------|------------|
| **1️⃣ Vytvořit nový sešit** | Toto je základ. Aspose.Cells zachází s objektem `Workbook` jako s celým Excel souborem, takže v podstatě **vytváříte Excel sešit v C# stylu**. |
| **2️⃣ Získat první list** | Nový sešit vždy obsahuje alespoň jeden list (`Worksheets[0]`). Přístup k němu brzy zabraňuje překvapením s null‑referencí. |
| **3️⃣ Přidat data do Excelu** | Pomocí `PutValue` **přidáváme data do Excelu** bez starostí o formátování buněk. Čísla `1` a `2` jsou naše testovací data pro wrap funkce. |
| **4️⃣ Jak používat WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` říká Excelu, aby vzal rozsah `A1:B1` a rozlil jeho hodnoty vertikálně, po jedné na řádek. Výsledek končí v `C1` a rozlije se dolů (`C1`, `C2`, …). |
| **5️⃣ Jak používat WRAPROWS** | `WRAPROWS(A1:B1, 2)` dělá opak: vytvoří horizontální rozlití, umístí dvě hodnoty do jednoho řádku začínajícího v `C2`. |
| **6️⃣ Vynutit výpočet vzorce** | Ve výchozím nastavení může Aspose.Cells odložit výpočet až do otevření souboru v Excelu. Volání `CalculateFormula()` **vynutí výpočet vzorce**, takže můžete okamžitě po uložení přečíst výsledky. |
| **7️⃣ Uložit sešit** | Poslední krok zapíše vše na disk. Otevřete vzniklý soubor `WrapFunctions.xlsx` a podívejte se na výsledek. |

---

## Vytvořit Excel sešit v C# – Nastavení prostředí

Než spustíte kód, ujistěte se, že máte správné nástroje:

1. **.NET 6.0+** – Nejnovější LTS verze funguje nejlépe.
2. **Visual Studio 2022** (nebo VS Code s rozšířením C#).
3. **Aspose.Cells for .NET** – Instalace přes NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. Zapisovatelná složka pro výstupní soubor.

Tyto předpoklady jsou minimální; není vyžadována žádná COM interop nebo instalace Office, což je důvod, proč je Aspose.Cells oblíbenou volbou pro server‑side generování Excelu.

---

## Přidat data do Excelu – Nejlepší postupy

Když **přidáváte data do Excelu** programově, zvažte následující tipy:

* **Použijte `PutValue`** pro surová čísla nebo řetězce; automaticky detekuje datový typ.
* **Vyhněte se pevně zakódovaným adresám buněk** ve velkých projektech – používejte smyčky nebo pojmenované oblasti pro škálovatelnost.
* **Nastavujte styly buněk střídmě**; každá změna stylu přináší režii. Pokud potřebujete formátování, vytvořte jeden objekt stylu a aplikujte jej na více buněk.

V našem malém příkladu vkládáme jen dvě čísla, ale stejný vzor se dá rozšířit na tisíce řádků.

---

## Jak používat WRAPROWS – Příklad horizontálního pole

Pokud potřebujete opak `WRAPCOLS`, `WRAPROWS` je vaše volba. Syntaxe je:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – rozsah, který chcete transformovat.
* `rows_per_item` – volitelný; určuje, kolik řádků každá položka zabírá. V našem demu jsme použili `2`, aby se obě hodnoty umístily do jednoho řádku.

Můžete experimentovat změnou druhého argumentu:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Otevřete sešit a uvidíte, že hodnoty se rozlévají přes tři sloupce, přičemž každý sloupec obsahuje původní čísla opakovaná podle potřeby.

---

## Vynutit výpočet vzorce – Kdy a proč

Můžete se ptát, „Opravdu potřebuji volat `CalculateFormula()`?“ Odpověď je **ano**, pokud:

* Plánujete číst vypočtené hodnoty **programově** po uložení.
* Chcete zajistit, aby se soubor v Excelu otevřel se správnými výsledky již zobrazenými.
* Běžíte v **headless prostředí** (např. webové API), kde žádný uživatel manuálně nevyvolá přepočet.

Přeskočení tohoto kroku nepoškodí sešit, ale buňky budou zobrazovat text vzorce (`=WRAPCOLS(...)`) místo vypočtených hodnot, dokud Excel neprovedete přepočet.

---

## Očekávaný výstup – Co hledat

Po spuštění programu a otevření `WrapFunctions.xlsx`:

| Cell | Formula | Displayed Value |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (v C1) a `2` (v C2) – vertikální seznam |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` v C2 a `2` v D2 – horizontální seznam |

Tak uvidíte sloupec hodnot začínající v **C1** a řádek hodnot začínající v **C2**. To potvrzuje, že obě wrap funkce fungovaly podle očekávání.

---

## Okrajové případy a varianty

| Scénář | Co se mění? | Navrhovaná úprava |
|--------|-------------|-------------------|
| **Velký rozsah (A1:Z1)** | Více hodnot k rozlití vertikálně | Zvyšte druhý argument `WRAPCOLS`, pokud chcete více sloupců na skupinu. |
| **Není‑číselná data** | Řetězce jsou zpracovány stejným způsobem | Žádná změna kódu; `PutValue` přijímá libovolný objekt. |
| **Dynamický rozsah** | Velikost neznáte při kompilaci | Použijte `sheet.Cells.MaxDataColumn` a `MaxDataRow` k vytvoření řetězce adresy. |
| **Více listů** | Potřeba použít wrap funkce na různých listech | Odkazujte na správný list (`workbook.Worksheets["Sheet2"]`). |

---

## Profesionální tipy z praxe

* **Pro tip:** Zabalte vytvoření sešitu do `using` bloku, pokud cílíte na .NET Core 3.1+, aby byly všechny prostředky uvolněny okamžitě.
* **Watch out for:** Nastavení stejného vzorce v rozsáhlém rozsahu bez volání `CalculateFormula()` může způsobit úzká místa ve výkonu. Kde je to možné, zpracovávejte vzorce po dávkách.
* **Tip:** Pokud potřebujete načíst vypočtené hodnoty zpět v kódu, zavolejte `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}