---
category: general
date: 2026-03-18
description: Vytvořte nový sešit a exportujte Excel do TXT při zachování číselné přesnosti.
  Naučte se, jak uložit list jako TXT a efektivně převést list do TXT.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: cs
og_description: Vytvořte nový sešit a exportujte Excel do TXT s přesností. Tento tutoriál
  ukazuje, jak uložit list jako TXT a převést list do TXT pomocí C#.
og_title: Vytvořit nový sešit – Průvodce exportem Excel do TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořit nový sešit – Exportovat Excel do TXT s plnou přesností
url: /cs/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit nový sešit – Exportovat Excel do TXT s plnou přesností

Už jste někdy potřebovali **create new workbook** v C# jen proto, abyste vypsali nějaká data do prostého textového souboru? Možná taháte report ze starého systému a následný nástroj přijímá jen vstup ve formátu `.txt`. Dobrá zpráva? Nemusíte obětovat číselnou přesnost a rozhodně nemusíte ručně skládat řetězce CSV.

V tomto průvodci projdeme celý proces **export excel to txt**, od inicializace sešitu až po zachování koncových nul při **save worksheet as txt**. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu – bez dalších utilit.

## Co budete potřebovat

- **ASP.NET/ .NET 6+** (kód funguje také na .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – knihovna, která poskytuje třídy `Workbook`, `Worksheet` a `TxtSaveOptions`. Můžete ji získat z NuGet pomocí `Install-Package Aspose.Cells`.  
- Základní znalost C# (pokud vám vyhovují `using` příkazy, jste připraveni).  

To je vše – žádné Excel interop, žádné COM objekty a rozhodně žádné ruční spojování řetězců.

---

## Krok 1: Inicializace nového sešitu (Primary Keyword)

První věc, kterou musíte udělat, je **create new workbook**. Představte si sešit jako prázdné plátno, kam později vložíte čísla, text nebo vzorce.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Proč je to důležité:** Vytvoření instance `Workbook` bez načtení souboru vám poskytne čistý list. Pak můžete přidávat data programově, což je ideální pro scénáře **convert worksheet to txt**, kde nemáte existující `.xlsx`.

## Krok 2: Naplnění buněk – zachovat koncové nuly

Běžnou pastkou při převodu čísel do textu je ztráta koncových nul (`123.45000` se stane `123.45`). Pokud následné systémy spoléhají na pole pevné šířky, může tato ztráta vše rozbít.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Tip:** `PutValue` automaticky určuje datový typ. Pokud potřebujete řetězec, který vypadá jako číslo, použijte místo toho `PutValue("123.45000")`.

## Krok 3: Nastavení možností uložení TXT – zachovat číselnou přesnost

Zde se děje kouzlo. Přepnutím `PreserveNumericPrecision` řeknete Aspose.Cells, aby zapsal přesně hodnotu, kterou jste zadali, včetně nevýznamných koncových nul.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Proč to povolit?** Když **save excel as txt**, výchozí chování ořízne zbytečné desetinné místa. Nastavení `PreserveNumericPrecision = true` zaručuje, že výstup bude odpovídat zobrazené hodnotě buňky, což je klíčové pro finanční zprávy nebo vědecká data.

## Krok 4: Uložení listu jako TXT – finální export

Nyní skutečně **save worksheet as txt**. Můžete zadat cestu kamkoli, kde máte právo zápisu; příklad používá relativní složku nazvanou `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Očekávaný výstup** (`num-preserve.txt`):

```
123.45000
```

Všimněte si, že koncové nuly jsou zachovány – přesně to, co jste požadovali.

## Krok 5: Ověření výsledku – rychlá kontrola

Po spuštění programu otevřete `num-preserve.txt` v libovolném textovém editoru. Měli byste vidět jediný řádek `123.45000`. Pokud místo toho uvidíte `123.45`, zkontrolujte, že `PreserveNumericPrecision` je nastaveno na `true` a že používáte aktuální verzi Aspose.Cells (v23.10+).

## Běžné varianty a okrajové případy

### Export více buněk nebo rozsahů

Pokud potřebujete **export excel to txt** pro celý rozsah, jednoduše před uložením vyplňte více buněk:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose ve výchozím nastavení zapíše každou buňku na nový řádek. Můžete také změnit oddělovač (tabulátor, čárka) pomocí `txtSaveOptions.Separator`.

### Převod listu do TXT s různými kódováními

Někdy následné systémy vyžadují UTF‑8 BOM nebo ASCII. Nastavte kódování takto:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Práce s velkými sešity

Při práci s obrovskými listy (stovky tisíc řádků) zvažte streamování výstupu:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Tipy a úskalí

- **Nezapomeňte vytvořit výstupní adresář** před voláním `Save`, jinak získáte `DirectoryNotFoundException`.  
- **Dejte pozor na lokálně specifické desetinné oddělovače**. Pokud vaše prostředí používá čárky (`1,23`), nastavte `txtSaveOptions.DecimalSeparator = '.'`, aby se vynutil tečka.  
- **Kompatibilita verzí**: Příznak `PreserveNumericPrecision` byl zaveden v Aspose.Cells 20.6. Pokud používáte starší verzi, příznak neexistuje a budete muset před uložením buňku naformátovat jako text.

![Příklad vytvoření nového sešitu](excel-to-txt.png "Vytvořit nový sešit")

*Text obrázku: "Vytvořit nový sešit a exportovat Excel do TXT s zachovanou číselnou přesností"*

## Shrnutí – Co jsme probrali

- **Create new workbook** pomocí Aspose.Cells.  
- Naplnit buňku číslem, které obsahuje koncové nuly.  
- Nastavit `TxtSaveOptions.PreserveNumericPrecision = true` pro **save excel as txt** bez ztráty přesnosti.  
- Zapsat soubor na disk a ověřit, že výstup odpovídá původní hodnotě.  

To je kompletní workflow **convert worksheet to txt** v méně než 50 řádcích C#.

## Další kroky a související témata

Nyní, když můžete **export excel to txt** s dokonalou přesností, můžete chtít prozkoumat:

- **Export do CSV** s vlastním oddělovačem (`TxtSaveOptions.Separator`).  
- **Ukládání do jiných prostých textových formátů** jako TSV (`SaveFormat.TabDelimited`).  
- **Dávkové zpracování** více sešitů ve složce pomocí `Directory.GetFiles`.  
- **Integrace s Azure Functions** pro konverzi na vyžádání v cloudu.

Každý z nich staví na stejném vzoru `Workbook` → `Worksheet` → `TxtSaveOptions`, takže se v tom budete cítit jako doma.

### Závěrečná myšlenka

Pokud jste šli krok za krokem, nyní přesně víte, jak **create new workbook**, naplnit jej a **save worksheet as txt**, přičemž zachováte každou desetinnou číslici, na které vám záleží. Je to malý úsek kódu, ale řeší překvapivě častý problém, když staré pipeline vyžadují vstupy v prostém textu.

Vyzkoušejte to, pohrávejte si s nastavením a nechte data proudit přesně tak, jak potřebujete. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}