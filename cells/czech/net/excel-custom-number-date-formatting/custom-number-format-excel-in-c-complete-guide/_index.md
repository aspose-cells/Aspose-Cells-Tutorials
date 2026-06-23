---
category: general
date: 2026-03-22
description: Návod na vlastní číselný formát v Excelu, ukazující, jak importovat datovou
  tabulku do Excelu, nastavit barvu pozadí sloupce, formátovat sloupec jako měnu a
  uložit sešit jako xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: cs
og_description: Tutoriál Excelu o vlastním formátu čísel, který vás provede importem
  DataTable, nastavením barvy pozadí sloupce, formátováním sloupce jako měny a uložením
  sešitu jako xlsx.
og_title: Vlastní číselný formát v Excelu v C# – průvodce krok za krokem
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Vlastní formát čísel v Excelu v C# – Kompletní průvodce
url: /cs/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní formát čísel v Excelu – Full‑Stack C# tutoriál

Už jste se někdy zamýšleli, jak aplikovat **custom number format excel** styl přímo z C#? Možná jste zkoušeli vypsat DataTable do tabulky a viděli jen prostá čísla, žádné barvy a žádné formátování měny. To je častý problém – zejména když potřebujete vylepšenou zprávu pro zainteresované strany.

V tomto průvodci tento problém vyřešíme společně: naučíte se **import datatable to excel**, **set column background color**, **format column as currency** a nakonec **save workbook as xlsx** s vlastním formátem čísel, který vaše čísla zvýrazní. Žádné vágní odkazy, jen kompletní, spustitelný řešení, které můžete zkopírovat a vložit do svého projektu.

---

## Co vytvoříte

Na konci tohoto tutoriálu budete mít samostatnou C# konzolovou aplikaci, která:

1. Načte `DataTable` (můžete nahradit ukázkový kód vlastním dotazem).  
2. Vytvoří nový Excel workbook pomocí Aspose.Cells (nebo jakékoli kompatibilní knihovny).  
3. Použije modré, tučné písmo na první sloupec, světle žluté pozadí na druhý a formát měny (`$#,##0.00`) na třetí.  
4. Uloží soubor jako `DataTableWithStyleArray.xlsx` do vámi zvoleného adresáře.

Uvidíte přesně, jak každý řádek přispívá k finálnímu Excel souboru, a probereme, proč jsou tyto volby důležité pro udržitelnost a výkon.

---

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+).  
- Aspose.Cells pro .NET (zdarma zkušební verze nebo licencovaná). Instalace přes NuGet:

```bash
dotnet add package Aspose.Cells
```

- Základní znalost `DataTable` a C# konzolových aplikací.

---

## Krok 1: Načtení zdrojových dat jako DataTable

Nejprve potřebujeme nějaká data k exportu. Ve skutečném scénáři byste pravděpodobně volali repozitář nebo spustili SQL dotaz. Pro ilustraci vytvoříme jednoduchou tabulku v paměti.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** Použití `DataTable` vám poskytuje tabulární, schématem‑uvědomělý zdroj, který se čistě mapuje na řádky a sloupce v Excelu. Navíc vám umožní znovu použít stejnou logiku exportu pro jakýkoli dataset bez přepisování kódu.

---

## Krok 2: Vytvoření nového workbooku a získání první listu

Nyní spustíme Excel workbook. Třída `Workbook` představuje celý soubor; její `Worksheets[0]` je výchozí list, kam vložíme naše data.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Pokud potřebujete více listů, stačí zavolat `workbook.Worksheets.Add("SheetName")` a opakovat kroky stylování pro každý z nich.

---

## Krok 3: Definice stylů sloupců – písmo, pozadí a formát čísla

Styling v Aspose.Cells se provádí pomocí objektů `Style`. Vytvoříme pole, kde každý prvek odpovídá sloupci v DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** Předání pole do `ImportDataTable` vám umožní aplikovat odlišný styl na každý sloupec v jediném volání, což je jak stručné, tak výkonné. Navíc zaručuje, že formátování zůstane synchronizováno s pořadím dat.

---

## Krok 4: Import DataTable s aplikací stylů

Zde je jádro operace: předáme `DataTable` do listu, řekneme Aspose, aby zahrnul řádek hlavičky, a předáme naše pole `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose prochází každý sloupec, zapíše hlavičku a pak zapíše hodnoty řádků. Při tom aplikuje odpovídající `Style` z pole, takže získáte modrou hlavičku pro „Product“, žlutě odstíněný „Quantity“ a pěkně formátovaný sloupec „Revenue“.

---

## Krok 5: Uložení workbooku jako soubor XLSX

Nakonec workbook uložíme na disk. Metoda `Save` automaticky zvolí formát XLSX podle přípony souboru.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** Pokud potřebujete soubor streamovat (např. pro webové API), použijte `workbook.Save(stream, SaveFormat.Xlsx)` místo cesty k souboru.

---

## Kompletní funkční příklad

Níže je celý program, který můžete vložit do nového konzolového projektu. Překompiluje se a spustí tak, jak je, a vytvoří stylovaný Excel soubor.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Očekávaný výsledek

Když otevřete `DataTableWithStyleArray.xlsx`, uvidíte:

| **Produkt** (modré, tučné) | **Množství** (světle žluté) | **Příjem** (měna) |
|----------------------------|-----------------------------|-------------------|
| Widget A                   | 120                         | $3,450.75         |
| Widget B                   | 85                          | $2,190.00         |
| Widget C                   | 60                          | $1,580.40         |

**custom number format excel**, který jste zadali (`$#,##0.00`), zajišťuje, že každá buňka s příjmem zobrazí dolarový znak, oddělovač tisíců a dvě desetinná místa – přesně to, co očekávají finanční týmy.

---

## Často kladené otázky a okrajové případy

### Můžu to použít s jinou Excel knihovnou?

Ano. Koncept – vytvoření stylu pro každý sloupec a jeho aplikace během importu – se přenáší na EPPlus, ClosedXML nebo NPOI. API volání se liší, ale vzor zůstává stejný.

### Co když má moje DataTable více sloupců než stylů?

Aspose použije výchozí styl na jakýkoli sloupec, který nemá odpovídající položku v poli `columnStyles`. Aby nedošlo k překvapením, buď nastavte velikost pole na `dataTable.Columns.Count`, nebo generujte styly dynamicky ve smyčce.

### Jak nastavit vlastní formát čísla pro datumy?

Jednoduše nastavte `style.Custom = "dd‑mm‑yyyy"` (nebo jakýkoli platný Excel formátovací řetězec). Stejný přístup založený na poli funguje i pro datumy, procenta nebo vědeckou notaci.

### Existuje způsob, jak automaticky nastavit šířku sloupců po importu?

Ano – zavolejte `worksheet.AutoFitColumns();` po importu. Provede rychlý výpočet šířky na základě obsahu buněk.

### Co s velkými datovými sadami (100 000+ řádků)?

`ImportDataTable` je optimalizováno pro hromadné operace, ale můžete narazit na limity paměti. V takovém případě zvažte streamování řádků ručně pomocí `Cells[i, j].PutValue(...)` a opakované používání jednoho objektu `Style` ke snížení režie.

---

## Pro tipy a běžné úskalí

- **Avoid hard‑coding paths** v produkčním kódu; použijte `Environment.GetFolderPath` nebo konfigurační nastavení.  
- **Dispose of the workbook** pokud běžíte v dlouhoživé službě – zabalte jej do `using` bloku, aby se uvolnily nativní zdroje.  
- **Watch out for culture‑specific separators**. Vlastní formát `$#,##0.00` vynutí tečku jako desetinný oddělovač bez ohledu na locale OS, což je obvykle požadováno u finančních reportů.  
- **Remember to reference System.Drawing** (nebo `System.Drawing.Common` na .NET Core) pro struktury barev používané ve stylování.  
- **Test the output on different Excel versions**; starší verze mohou interpretovat některé vlastní formáty mírně odlišně.

---

## Závěr

Probrali jsme vše, co potřebujete k **custom number format excel** souborům z C#: načtení dat z `DataTable`, **import datatable to excel**, aplikaci **set column background color**, použití **format column as currency** a nakonec **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}