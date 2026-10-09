---
category: general
date: 2026-04-07
description: Použijte vlastní formát čísla na buňku v tabulce a naučte se, jak formátovat
  číslo v tabulce při exportu hodnoty buňky pomocí C#. Rychlý, kompletní návod.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: cs
og_description: Aplikujte vlastní číselný formát na buňku v tabulce a exportujte ji
  jako formátovaný řetězec. Naučte se, jak formátovat číslo v tabulce a exportovat
  hodnotu buňky.
og_title: Použít vlastní formát čísel – Kompletní tutoriál exportu v C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Použít vlastní číselný formát při exportu tabulky v C# – průvodce krok za krokem
url: /cs/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití vlastního formátu čísel v exportu tabulky v C# – Kompletní tutoriál

Už jste někdy potřebovali **aplikovat vlastní formát čísel** na buňku a poté získat ten formátovaný řetězec z tabulky? Nejste sami. Mnoho vývojářů narazí na problém, když zjistí, že místo hezkého, lokalizovaného řetězce se vrací surová hodnota. V tomto průvodci vám ukážeme přesně, jak formátovat čísla v buňkách tabulky a jak exportovat hodnotu buňky jako formátovaný řetězec pomocí populární knihovny pro tabulky v C#.

Do konce tohoto návodu budete schopni **aplikovat vlastní formát čísel** na libovolnou číselnou buňku, exportovat výsledek pomocí `ExportTable` a vidět přesně ten výstup, který byste očekávali zobrazit v UI nebo v reportu. Žádná externí dokumentace není potřeba – vše je zde.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+)
- Odkaz na knihovnu pro tabulky, která poskytuje `Workbook`, `Worksheet` a `ExportTableOptions` (např. **Aspose.Cells** nebo **GemBox.Spreadsheet**; ukázané API odpovídá Aspose.Cells)
- Základní znalost C# – pokud umíte napsat `Console.WriteLine`, jste připraveni

> **Pro tip:** Pokud používáte jinou knihovnu, názvy vlastností jsou obvykle podobné (`NumberFormat`, `ExportAsString`). Stačí je podle toho namapovat.

## Co tutoriál pokrývá

1. Vytvoření sešitu a výběr první listu.  
2. Vložení číselné hodnoty do buňky.  
3. Nastavení `ExportTableOptions` pro **aplikaci vlastního formátu čísel** a vrácení řetězce.  
4. Export buňky a vytištění formátovaného výsledku.  
5. Zvládání okrajových případů – co když buňka obsahuje vzorec nebo null hodnotu?

Pojďme na to.

![příklad aplikace vlastního formátu čísel](https://example.com/image.png "aplikace vlastního formátu čísel")

## Krok 1 – Vytvořte sešit a získejte první list

Prvním, co potřebujete, je objekt sešitu. Představte si ho jako soubor Excel, který otevřete v aplikaci Office. Jakmile jej máte, vezměte první list – většina tutoriálů začíná zde, protože to udržuje příklad stručný.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Proč je to důležité:** Čerstvý sešit vám poskytuje čistý start, což zajišťuje, že žádné skryté formátování nezasahuje do našeho vlastního formátu čísel později.

## Krok 2 – Vložte číselnou hodnotu do buňky B2 (buňka, kterou budeme exportovat)

Nyní potřebujeme něco, co můžeme formátovat. Buňka **B2** je pohodlné místo – snadno se na ni odkazuje a je dostatečně daleko od výchozího rohu A1, aby nedošlo k nechtěnému přepsání.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Co když je hodnota vzorec?**  
Pokud později nahradíte surovou hodnotu vzorcem (např. `=SUM(A1:A10)`), exportní rutina i tak respektuje formát čísla, který aplikujeme v dalším kroku, protože formátování je přiřazeno buňce, nikoli typu hodnoty.

## Krok 3 – Nakonfigurujte možnosti exportu, aby vracely hodnotu jako formátovaný řetězec

Zde je jádro tutoriálu: řekneme knihovně, aby **aplikovala vlastní formát čísel** během exportu. Řetězec `NumberFormat` následuje stejný vzor, jaký použijete v Excelu v kategorii „Vlastní“.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` zajistí, že metoda vrátí `string` místo surového `double`.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` napodobuje vzor v Excelu: čárky pro tisíce, dvě desetinná místa a závorky pro záporná čísla.

> **Proč použít vlastní formát?** Zaručuje konzistenci napříč kulturami (např. US vs. evropské oddělovače čísel) a umožňuje vložit firemně specifické stylování, jako jsou účetní závorky.

## Krok 4 – Exportujte buňku pomocí nakonfigurovaných možností

Nyní skutečně vytáhneme hodnotu z listu a necháme knihovnu udělat těžkou práci – aplikovat definovaný formát.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Okrajový případ – prázdná buňka:** Pokud by `B2` byla prázdná, `formattedResult` by byl `null`. Můžete to ošetřit jednoduchou kontrolou na null před výpisem.

## Krok 5 – Zobrazte formátovaný řetězec

Nakonec výsledek zapíšeme do konzole. Ve skutečné aplikaci můžete tento řetězec poslat do PDF, e‑mailu nebo do UI štítku.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Očekávaný výstup**

```
1,234.56
```

Pokud změníte surovou hodnotu na `-9876.54`, stejný formát vám dá `(9,876.54)` – přesně to, co vyžadují mnohé účetní reporty.

## Kompletní, spustitelný příklad

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu. Překládá se a běží tak, jak je, pokud jste přidali odpovídající NuGet balíček pro knihovnu tabulek.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Rychlá kontrola

- **Komplikuje se?** Ano – jen se ujistěte, že je referencována knihovna `Aspose.Cells` (nebo ekvivalentní) DLL.  
- **Bude fungovat s jinými kulturami?** Formátovací řetězec je kultuře nezávislý; knihovna respektuje vzor, který zadáte. Pokud potřebujete lokálně specifické oddělovače, můžete před export přidat zpracování `CultureInfo`.

## Časté otázky a varianty

### Jak **formátovat číslo v tabulce** pomocí jiného vzoru?

Nahraďte řetězec `NumberFormat`. Například pro zobrazení procenta s jedním desetinným místem:

```csharp
NumberFormat = "0.0%";
```

### Co když potřebuji **exportovat hodnotu buňky** jako HTML místo prostého textu?

Většina knihoven má přetížení, které přijímá typ exportu. Nastavíte `ExportAsString = true` a přidáte `ExportHtml = true` (nebo podobně). Princip zůstává stejný: definujete formát a pak zvolíte reprezentaci výstupu.

### Mohu aplikovat formát na celý rozsah, ne jen na jednu buňku?

Určitě. Můžete přiřadit `NumberFormat` objektu `Style` a poté tento styl aplikovat na `Range`. Volání exportu zůstane beze změny; automaticky použije přiřazený styl.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Co se stane, když buňka obsahuje vzorec?

Exportní rutina nejprve vyhodnotí vzorec a pak formátuje vzniklou číselnou hodnotu. Žádný další kód není potřeba – jen se ujistěte, že byla zavolána metoda `Calculate`, pokud jste vypnuli automatické počítání.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Závěr

Nyní víte, jak **aplikovat vlastní formát čísel** na buňku v tabulce, **formátovat číslo v tabulce** v různých kontextech a **exportovat hodnotu buňky** jako připravený řetězec k zobrazení. Stručný ukázkový kód výše pokrývá každý krok – od vytvoření sešitu po finální výstup – takže jej můžete rovnou vložit do produkčního projektu.

Jste připraveni na další výzvu? Zkuste kombinovat tuto techniku s **formátováním číselné buňky** pro data, měnové symboly nebo podmíněné formátování. Nebo prozkoumejte export více buněk jako CSV při zachování vlastního formátu každé buňky. Možnosti jsou neomezené a s těmito základy máte pevný základ.

Šťastné programování a nezapomeňte experimentovat – někdy se nejlepší odpovědi objeví, když trochu pozměníte formátovací řetězec!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}