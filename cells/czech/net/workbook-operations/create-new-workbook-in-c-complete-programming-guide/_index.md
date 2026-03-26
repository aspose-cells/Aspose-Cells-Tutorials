---
category: general
date: 2026-03-25
description: Vytvořte nový sešit v C# a naučte se používat funkci EXPAND, vypočítat
  kotangens a uložit sešit do souboru pomocí krok‑za‑krokem kódu.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: cs
og_description: Vytvořte nový sešit v C# a okamžitě zjistěte, jak použít funkci EXPAND,
  vypočítat kotangens a uložit sešit do souboru.
og_title: Vytvořte nový sešit v C# – Kompletní průvodce programováním
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Vytvořte nový sešit v C# – Kompletní programovací průvodce
url: /cs/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu v C# – Kompletní programovací průvodce

Už jste někdy potřebovali **vytvořit nový sešit** v C#, ale nebyli jste si jisti, kde začít? Nejste v tom sami. Ať už automatizujete reportingový kanál nebo jen experimentujete s Excelovými vzorci v kódu, schopnost vytvořit sešit, vložit vzorce jako `EXPAND` nebo `COT` a následně **uložit sešit do souboru** je základní dovedností pro každého .NET vývojáře.

V tomto tutoriálu projdeme reálným příkladem, který přesně to dělá: vytvoříme čerstvý sešit, použijeme funkci `EXPAND` k převodu statického pole na dynamický sloupec, vypočítáme kotangens pomocí funkce `COT` a nakonec **uložíme sešit do souboru** jako `.xlsx`. Na konci budete mít připravený úryvek kódu, pochopíte *proč* je každé volání důležité, a uvidíte několik užitečných variant pro okrajové případy.

> **Pro tip:** Veškerý kód níže funguje s nejnovější verzí Aspose.Cells pro .NET (k březnu 2026). Pokud používáte starší verzi, rozhraní API je převážně stejné, ale zkontrolujte importy jmenných prostorů.

## Co budete potřebovat

- .NET 6.0 nebo novější (ukázka cílí na .NET 6, ale .NET 5 také funguje)  
- Aspose.Cells pro .NET nainstalovaný přes NuGet (`Install-Package Aspose.Cells`)  
- Základní znalost C# (to zvládnete)  

To je vše — žádné extra DLL, žádná COM interop a rozhodně žádný Excel nainstalovaný na stroji. Připravení? Ponořme se do toho.

![Screenshot showing how to create new workbook in C#](assets/create-new-workbook.png){alt="Snímek obrazovky ukazující, jak vytvořit nový sešit v C#"}

## Krok 1: Vytvoření nového sešitu

První věc, kterou musíte udělat, je vytvořit instanci třídy `Workbook`. Představte si to jako otevření prázdného Excel souboru v paměti. Tento objekt obsahuje kolekci listů, stylů a všeho ostatního, co budete později potřebovat.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Proč hned získat první list? Většina rychlých příkladů pracuje s jediným listem a přístup `Worksheets[0]` je nejrychlejší způsob, jak získat referenci bez iterace. Pokud budete později potřebovat více listů, můžete je přidat pomocí `workbook.Worksheets.Add()`.

## Krok 2: Jak použít funkci EXPAND k vytvoření dynamických oblastí

`EXPAND` je novější Excel funkce, která vezme pole a doplní jej na zadanou velikost. V našem kódu rozšíříme literál pole `{1,2,3}` na **sloupec o 5 řádcích** počínaje buňkou `A1`. Syntaxe uvnitř řetězce je přesně taková, jakou byste napsali do Excelu, takže ji můžete později jednoduše zkopírovat a vložit do buňky.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### Co se děje pod kapotou?

- `{1,2,3}` je horizontální literál pole.  
- Druhý argument (`5`) říká Excelu, aby pole rozšířil na **5 řádků**.  
- Třetí argument (`1`) vynutí výstup **jednoho sloupce**.  

Pokud třetí argument vynecháte, Excel se pokusí zachovat původní tvar, což by vám mohlo dát blok 5×3 místo jednoho sloupce. To je častá chyba při prvním experimentování s `EXPAND`.

#### Varianty, které můžete potřebovat

| Požadovaný tvar | Příklad vzorce |
|-----------------|----------------|
| 3‑řádkový, 2‑sloupcový blok | `=EXPAND({1,2,3},3,2)` |
| Vyplnit pouze dolů (stejný sloupec) | `=EXPAND({10,20},10,1)` |
| Rozšířit na větší počet sloupců | `=EXPAND({5},5,4)` |

Klidně zaměňte literály nebo rozměry, aby odpovídaly vaší logice generování dat.

## Krok 3: Jak vypočítat kotangens pomocí funkce COT

Funkce `COT` vrací kotangens úhlu vyjádřeného v radiánech. V našem příkladu vypočítáme kotangens 45° (π/4 radiánů). Výsledek, `1`, se objeví v buňce `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Proč použít COT místo ručního výpočtu?

Excel už umí provádět trigonometrické převody, takže se vyhnete chybám zaokrouhlování v plovoucí řádové čárce, které mohou vzniknout při pokusu o `1 / TAN(angle)`. Navíc vzorec zůstává čitelný pro každého, kdo bude tabulku později kontrolovat.

#### Okrajový případ: úhly mimo 0‑360°

Pokud zadáte úhel větší než `2*PI()` (nebo záporný), Excel jej automaticky zabalí, ale výsledek může být překvapivý. Pro jistotu můžete úhel nejprve normalizovat:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Tento úryvek ukazuje, jak kombinovat `MOD` s `COT` pro robustní výpočty.

## Krok 4: Jak uložit sešit do souboru (Excel)

Nyní, když jsou vzorce na svém místě, posledním krokem je **uložit sešit do souboru**. Můžete zvolit libovolnou cestu – jen se ujistěte, že adresář existuje a máte oprávnění k zápisu.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Co se ve skutečnosti uloží?

Když otevřete `output.xlsx` v Excelu, uvidíte:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- Sloupec **A** obsahuje rozšířené pole `{1,2,3}` následované dvěma prázdnými buňkami (protože jsme požadovali 5 řádků).  
- Buňka **B1** zobrazuje `1`, kotangens 45°.  

Pokud sešit obnovíte (stiskněte `F9` nebo povolte automatické přepočítávání), Excel vyhodnotí vzorce a zobrazí výsledky. Aspose.Cells také nabízí metodu `CalculateFormula`, pokud potřebujete hodnoty bez otevření Excelu:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Často kladené otázky a úskalí

| Otázka | Odpověď |
|--------|---------|
| **Musím povolit výpočet ručně?** | Ne. Ve výchozím nastavení Aspose.Cells ukládá vzorce tak, jak jsou; Excel je vypočítá při otevření. Pro předběžný výpočet použijte `workbook.CalculateFormula()`. |
| **Mohu zapisovat vzorce do více buněk najednou?** | Ano. Použijte `ws.Cells["D1:D5"].Formula = "=RAND()"` k vyplnění oblasti náhodnými čísly. |
| **Co když cílová složka neexistuje?** | Nejprve ji vytvořte: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **Je `EXPAND` podporováno ve starších verzích Excelu?** | `EXPAND` se objevilo v Excel 365/2019. Pokud potřebujete kompatibilitu se staršími soubory, zvažte kombinace `INDEX`/`SEQUENCE`. |
| **Jak skrýt zobrazení vzorce?** | Nastavte `ws.Cells["A1"].FormulaHidden = true;` a list ochraňte, pokud nechcete, aby uživatelé viděli podkladový vzorec. |

## Shrnutí

Nyní víte, **jak vytvořit nový sešit** v C#, využít sílu funkce `EXPAND` k generování dynamických polí, vypočítat kotangens pomocí `COT` a **uložit sešit do souboru** jako přehledný Excel dokument. Kompletní, spustitelný příklad najdete v úryvcích kódu výše — zkopírujte jej do konzolové aplikace, stiskněte `F5` a otevřete vzniklý `output.xlsx`, abyste viděli magii.

### Co dál?

- **Prozkoumejte další dynamické pole funkce** jako `SEQUENCE`, `FILTER` a `SORT`.  
- **Automatizujte tvorbu grafů** pomocí bohatého grafického API Aspose.Cells.  
- **Integrujte s datovými zdroji** (SQL, CSV) a programově předávejte tyto hodnoty do vzorců.  
- **Naučte se ukládat Excel jako PDF** nebo jiné formáty — ideální pro reportingové kanály.  

Klidně experimentujte: změňte hodnoty pole, upravte úhel nebo výsledek zapište do jiného listu. Možnosti jsou neomezené, když spojíte C# s moderním vzorcem Excelu.

Šťastné programování a ať vaše tabulky vždy správně počítají!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}