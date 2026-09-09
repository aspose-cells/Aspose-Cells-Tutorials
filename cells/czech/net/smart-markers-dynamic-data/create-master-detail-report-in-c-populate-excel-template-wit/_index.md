---
category: general
date: 2026-02-28
description: Vytvořte master‑detail report v C# a naučte se, jak naplnit šablonu Excelu,
  sloučit data do Excelu a načíst sešit Excel v C# během několika kroků.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: cs
og_description: Vytvořte master‑detail report v C# pomocí Aspose.Cells SmartMarker.
  Naučte se načíst Excel sešit v C#, sloučit data do Excelu a naplnit Excel šablonu.
og_title: Vytvořte master‑detail report v C# – Vyplňte šablonu Excelu
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Vytvořte master‑detail report v C# – Naplňte šablonu Excelu pomocí SmartMarkeru
url: /cs/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření master‑detail reportu v C# – Naplnění šablony Excel pomocí SmartMarker

Už jste někdy potřebovali **vytvořit master detail report** v C#, ale nebyli jste si jisti, jak dostat data do souboru Excel? Nejste v tom sami. V tomto průvodci projdeme přesně kroky k **naplnění šablony Excel**, **sloučení dat do Excelu** a **načtení sešitu Excel C#**‑stylu, abyste získali vyladěný master‑detail report připravený k distribuci.

Použijeme Aspose.Cells SmartMarker, výkonný engine, který rozumí vztahům master‑detail hned z krabice. Na konci tutoriálu budete mít kompletní, spustitelný příklad, který můžete vložit do libovolného .NET projektu. Žádné vágní zkratky typu „viz dokumentace“ – jen samostatné řešení, které můžete zkopírovat a spustit.

## Co se naučíte

- Jak **vytvořit master detail** datové struktury v C#, které se přímo mapují na šablonu Excel.
- Přesný způsob, jak **načíst sešit Excel C#** kód, který otevře soubor `.xlsx` obsahující SmartMarker tagy.
- Postup k **naplnění šablony Excel** spuštěním `SmartMarkerProcessor`.
- Tipy pro řešení okrajových případů, jako chybějící tagy nebo velké datové sady.
- Jak ověřit výsledek a jak vypadá finální **master detail report**.

### Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.8).
- Aspose.Cells pro .NET (můžete si stáhnout bezplatnou zkušební NuGet balíček: `Install-Package Aspose.Cells`).
- Základní soubor Excel (`template.xlsx`) obsahující SmartMarker tagy (ukážeme minimální značkování, které potřebujete).

Pokud máte vše připravené, pojďme na to.

## Krok 1 – Vytvoření master‑detail datového zdroje *(jak vytvořit master detail)*

Prvním, co potřebujete, je objekt v C#, který představuje řádky master (objednávky) a jejich podřazené řádky (položky objednávek). SmartMarker tuto hierarchii načte automaticky, když je `MasterDetail` nastaveno na `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Proč je to důležité:**  
SmartMarker hledá vlastnost pojmenovanou `Orders` (master) a poté pro každou objednávku hledá kolekci nazvanou `Items`. Shodou těchto názvů automaticky získáte **master‑detail report** bez nutnosti psát smyčky.

> **Tip:** Udržujte názvy vlastností krátké a výstižné; stávají se zástupnými symboly ve vaší šabloně Excel.

## Krok 2 – Konfigurace možností SmartMarker pro zpracování master‑detail

Řekněte engine, že pracujete se scénářem master‑detail, a zadejte mu název listu detailu, který přijme podřazené řádky.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Proč je to důležité:**  
Pokud vynecháte `MasterDetail = true`, SmartMarker bude data považovat za plochý seznam a řádky detailu se nikdy neobjeví. `DetailSheetName` musí odpovídat názvu listu, který jste vytvořili v šabloně (rozlišuje velká a malá písmena).

## Krok 3 – Načtení sešitu Excel ve stylu C#

Nyní otevřeme šablonu, která obsahuje SmartMarker tagy. Toto je krok **load Excel workbook C#**, nad kterým mnozí vývojáři zakopnou, protože zapomenou použít správnou cestu k souboru nebo řádně uvolnit sešit.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Proč je to důležité:**  
Aspose.Cells načte celý sešit do paměti, takže soubor může být na disku, vložený jako zdroj nebo dokonce streamovaný z webové služby. Jen se ujistěte, že cesta ukazuje na platný soubor `.xlsx`, který obsahuje tagy, o kterých budeme hovořit dále.

## Krok 4 – Vložení SmartMarker tagů do šablony (naplnění šablony Excel)

Pokud nyní otevřete `template.xlsx`, uvidíte dva listy:

- **Orders** – master list s řádkem jako `&=Orders.Id`.
- **OrderDetail** – detailní list s řádky jako `&=Items.Sku` a `&=Items.Qty`.

Zde je minimální pohled na značkování:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Není potřeba psát žádný kód pro tagy – žijí v souboru Excel. Krok **populate Excel template** je jednoduše volání procesoru:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Proč je to důležité:**  
Procesor prohledá každý list, nahradí `&=` zástupce skutečnými hodnotami a rozšíří řádky pro každý master a detailní záznam. Protože je `MasterDetail` zapnuté, automaticky vytvoří nový řádek pro každou položku pod příslušnou objednávkou.

## Krok 5 – Uložení master detail reportu

Na závěr zapíšete naplněný sešit na disk. To je okamžik, kdy získáte připravený ke sdílení **master detail report**.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Očekávaný výstup:**  

- List **Orders** ukazuje dva řádky: `1` a `2` (ID objednávek).  
- List **OrderDetail** ukazuje tři řádky:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Toto je plně funkční **create master detail report**, který můžete poslat e-mailem, vytisknout nebo předat jinému systému.

## Okrajové případy a časté otázky

### Co když šablona postrádá tag?
SmartMarker tiše ignoruje neznámé tagy, ale skončíte s prázdnými buňkami. Zkontrolujte pravopis tagu a ujistěte se, že názvy vlastností ve vašem C# objektu přesně odpovídají.

### Jak to zvládá velké datové sady?
Procesor streamuje řádky, takže i tisíce detailních záznamů nevyčerpají paměť. Pro extrémně velké soubory však můžete chtít zvýšit `MemorySetting` v `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Můžu použít jiný název listu pro master?
Ano – stačí přejmenovat list v šabloně a upravit `DetailSheetName`, pokud máte detailní list. Název master listu je odvozen ze zástupce (`&=Orders.Id`).

### Co když potřebuji přidat řádek s celkovým součtem?
Přidejte běžný Excel vzorec do šablony (např. `=SUM(B2:B{#})`). SmartMarker po vložení dat zachová vzorec.

## Kompletní spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny `using` direktivy, datový model, možnosti a práci se soubory.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Spusťte program, otevřete `output.xlsx` a uvidíte master‑detail data krásně naplněné.

## Vizuální reference

![Snímek výstupu master detail reportu](https://example.com/images/master-detail-report.png "Příklad master detail reportu")

*Obrázek zobrazuje list Orders s ID 1 a 2 a list OrderDetail se třemi řádky SKU‑Qty.*

## Závěr

Nyní víte **jak vytvořit master detail report** v C# pomocí Aspose.Cells SmartMarker, od vytvoření datového zdroje po **loading Excel workbook C#**, **populating Excel template**, a nakonec

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}