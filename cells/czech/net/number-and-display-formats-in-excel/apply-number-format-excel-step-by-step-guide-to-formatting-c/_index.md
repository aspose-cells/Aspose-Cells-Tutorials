---
category: general
date: 2026-02-26
description: Rychle použijte formát čísel v Excelu a naučte se, jak formátovat sloupec
  jako měnu, nastavit formát čísel sloupce a nastavit barvu písma sloupce během několika
  řádků C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: cs
og_description: aplikujte formát čísel v Excelu v C# pomocí snadných kroků. Naučte
  se formátovat sloupec jako měnu, nastavit číselný formát sloupce a nastavit barvu
  písma sloupce pro profesionální tabulky.
og_title: Použití formátu čísel v Excelu – Kompletní průvodce stylováním sloupců
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Použití číselného formátu v Excelu – krok za krokem průvodce formátováním sloupců
url: /cs/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

Produkt", "Price" to "Cena", "Apple" "Banán"? Actually "Apple", "Banana", "Cherry" are fruit names; could translate to "Jablko", "Banán", "Třešeň". Probably we should translate.

But the table header also includes "(blue font)" etc. Should translate.

Let's translate accordingly.

Also bullet points at the end: "What’s Next?" etc.

Make sure to keep markdown formatting.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Jak stylovat sloupce v Excelu v C#

Už jste se někdy zamýšleli, jak **apply number format excel** během procházení `DataTable`? Nejste v tom sami. Většina vývojářů narazí na problém, když potřebují mít záhlaví s modrým písmem *a* sloupec formátovaný jako měna ve stejné importní operaci. Dobrá zpráva? S několika řádky C# a správnými objekty stylů to můžete udělat bez následného zpracování listu.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **format column as currency**, **set column number format** pro libovolný jiný sloupec a dokonce **set column font color** pro záhlaví. Na konci budete mít znovupoužitelný vzor, který můžete vložit do libovolného projektu Aspose.Cells (nebo podobného).

## Co se naučíte

- Jak získat `DataTable` a přiřadit každému sloupci konkrétní `Style`.
- Přesné kroky k **apply number format excel** pomocí `Worksheet.Cells.ImportDataTable`.
- Proč je vytváření stylů předem efektivnější než formátování buněk po jedné.
- Jak zacházet s okrajovými případy, když má zdrojová tabulka více sloupců, než jste stylovali.
- Kompletní, připravený k zkopírování a vložení kód, který můžete spustit ještě dnes.

> **Prerequisite:** Tento průvodce předpokládá, že máte v projektu odkaz na Aspose.Cells pro .NET (nebo jakoukoli knihovnu poskytující API `Workbook`, `Worksheet`, `Style`). Pokud používáte jinou knihovnu, koncepty se přenášejí přímo – stačí nahradit názvy typů.

---

## Krok 1: Získání zdrojových dat jako DataTable

Než může dojít k jakémukoli stylování, potřebujete surová data. Ve většině reálných scénářů data žijí v databázi, CSV nebo API. Pro přehlednost si vytvoříme jednoduchý `DataTable` se dvěma sloupci: *Product* (string) a *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** Načtení dat do `DataTable` vám poskytne tabulární, paměťovou reprezentaci, kterou `ImportDataTable` může přímo konzumovat, čímž se eliminuje potřeba ručního vkládání buněk po jedné.

## Krok 2: Vytvoření pole stylů – jeden pro každý sloupec

Přetížení `ImportDataTable`, které použijeme, přijímá pole objektů `Style`. Každý prvek odpovídá indexu sloupce. Pokud ponecháte prvek jako `null`, sloupec zdědí výchozí styl sešitu.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** Deklarace pole *po* získání `DataTable` zajišťuje, že velikost přesně odpovídá, čímž se později předejde `IndexOutOfRangeException`.

## Krok 3: Nastavení barvy písma (modrá) pro první sloupec

Častý požadavek je zvýraznit záhlaví nebo klíčové sloupce odlišnou barvou písma. Zde nastavíme text prvního sloupce na modrou.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** Styly jsou znovupoužitelné a aplikují se hromadně, což je mnohem rychlejší než iterovat přes každou buňku po importu. Sešit si styl načte jednou a poté jej znovu použije pro každou buňku v daném sloupci.

## Krok 4: Formátování druhého sloupce jako měna

Vestavěné formáty čísel v Excelu jsou identifikovány indexem. `14` odpovídá výchozímu formátu měny (např. `$1,234.00`). Pokud potřebujete vlastní formát, můžete přiřadit formátovací řetězec.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** Pokud váš sešit používá locale, kde není měnový symbol `$`, stejný index se automaticky přizpůsobí (např. `€` pro německé locale).

## Krok 5: Import DataTable s definovanými styly

Nyní spojíme vše dohromady. Metoda `ImportDataTable` vloží data počínaje buňkou `A1` (řádek 0, sloupec 0) a použije připravené styly.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Druhý parametr `true` říká Aspose.Cells, aby považoval první řádek `DataTable` za záhlaví sloupců.
- Souřadnice `0, 0` určují levý horní roh, kde import začíná.
- `columnStyles` mapuje každý sloupec na jeho odpovídající styl.

## Krok 6: Uložení sešitu (volitelné, ale užitečné pro ověření)

Pokud chcete výsledek vidět v Excelu, stačí sešit uložit na disk. Tento krok není nutný pro samotnou logiku stylování, ale hodí se při ladění.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Očekávaný výstup

| **Produkt** (modré písmo) | **Cena** (měna) |
|----------------------------|-----------------|
| Jablko                     | $1.25           |
| Banán                      | $0.75           |
| Třešeň                     | $2.10           |

- Sloupec *Produkt* se zobrazuje modře, čímž vyniká.
- Sloupec *Cena* zobrazuje hodnoty s výchozím měnovým symbolem a dvěma desetinnými místy.

---

## Často kladené otázky a varianty

### Jak **set column number format** pro více než dva sloupce?

Stačí rozšířit pole `columnStyles`. Například pro zobrazení procent ve třetím sloupci:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Co když potřebuji *vlastní* formát měny, např. “USD 1,234.00”?

Nahraďte vlastnost `Number` formátovacím řetězcem:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Můžu použít **set column font color** na číselný sloupec, aniž by to ovlivnilo jeho formát čísla?

Ano. Styly jsou kombinovatelné. Na stejném objektu `Style` můžete nastavit jak `Font.Color`, tak `Number`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Co se stane, když má `DataTable` více sloupců než stylů?

Každý sloupec bez explicitního stylu (`null` položka) zdědí výchozí styl sešitu. Abyste se vyhnuli nechtěným `null`, můžete nejprve inicializovat celé pole základním stylem:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Pak přepíšete jen sloupce, na kterých vám záleží.

### Funguje tento přístup u velkých datových sad (10 000+ řádků)?

Ano. Protože stylování se aplikuje *jednou na sloupec* před importem, operace zůstává O(N) vzhledem k počtu řádků a paměťová náročnost zůstává nízká. Vyhněte se iteraci přes každou buňku po importu – tam výkon klesá.

---

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Spusťte program, otevřete `StyledReport.xlsx` a okamžitě uvidíte výsledek **apply number format excel**.

---

## Závěr

Ukázali jsme čistý a efektivní způsob, jak **apply number format excel** na importovaný `DataTable`. Připravením pole `Style[]` předem můžete **format column as currency**, **set column number format** i **set column font color** v jediném volání – bez nutnosti následného zpracování.

Neváhejte rozšířit tento vzor: přidat podmíněné stylování, sloučit buňky pro nadpisy nebo dokonce vložit vzorce. Stejné principy platí, udržují kód přehledný a vaše tabulky profesionální.

---

### Co dál?

- Prozkoumejte **conditional formatting** pro zvýraznění hodnot přesahujících prahovou hodnotu.
- Kombinujte tuto techniku s **pivot table generation** pro dynamické reportování.
- Vyzkoušejte **setting column number format** pro data, procenta nebo vlastní vědeckou notaci.

Zkusili jste nějaký vlastní obrat? Podělte se o něj v komentářích – pojďme společně rozšiřovat

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}