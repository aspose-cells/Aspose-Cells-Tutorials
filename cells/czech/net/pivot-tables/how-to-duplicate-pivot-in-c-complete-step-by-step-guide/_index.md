---
category: general
date: 2026-03-22
description: Naučte se, jak duplikovat kontingenční tabulku v C# pomocí Aspose.Cells.
  Tento průvodce také ukazuje, jak kopírovat řádky a načíst Excel sešit v C# pro plynulou
  automatizaci Excelu a kopírování řádků.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: cs
og_description: Jak duplikovat pivot v C#? Postupujte podle tohoto stručného tutoriálu,
  jak načíst Excel sešit v C#, kopírovat řádky a zvládnout automatizaci Excelu při
  kopírování řádků.
og_title: Jak duplikovat pivot v C# – kompletní průvodce
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Jak duplikovat Pivot v C# – Kompletní průvodce krok za krokem
url: /cs/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikovat kontingenční tabulku v C# – Kompletní průvodce krok za krokem

Už jste se někdy zamýšleli **jak duplikovat kontingenční tabulky** programově, aniž byste je museli ručně přetahovat v Excelu? Nejste v tom sami. V mnoha reportovacích pipelinech je potřeba stejný rozvrh kontingenční tabulky na novém souboru řádků a ruční provedení je ztráta času.  

Dobrá zpráva? S několika řádky C# můžete načíst Excel sešit, definovat oblast, která obsahuje kontingenční tabulku, a **jak kopírovat řádky**, aby se kontingenční tabulka objevila na novém místě – vše v jednom automatizovaném běhu. V tomto tutoriálu také pokryjeme základy **load excel workbook c#** a poskytneme vám pevný základ pro úkoly **excel automation copy rows**.

> **Co si odnesete**  
> • Kompletní, spustitelný příklad, který duplikuje kontingenční tabulku.  
> • Vysvětlení, proč je každý řádek důležitý.  
> • Tipy pro řešení okrajových případů, jako jsou skryté listy nebo více kontingenčních tabulek.

---

## Prerequisites

Než se ponoříme dál, ujistěte se, že máte:

- **.NET 6.0** (nebo jakoukoli novější verzi .NET) nainstalovanou.  
- **Aspose.Cells for .NET** – knihovna, kterou použijeme k manipulaci se soubory Excel. Můžete ji získat přes NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Zdrojový sešit (`Source.xlsx`), který již obsahuje kontingenční tabulku v rozsahu **A1:J20** (rozsah, který budeme duplikovat).  
- Základní znalost syntaxe C# – nic složitého, jen běžné `using` příkazy a metoda `Main`.

Pokud vám některá z těchto věcí není známá, zastavte se na chvíli a nainstalujte balíček; zbytek průvodce předpokládá, že knihovna je připravena k použití.

![Ilustrace, jak duplikovat kontingenční tabulku v C# pomocí Aspose.Cells](https://example.com/duplicate-pivot.png "ilustrace, jak duplikovat kontingenční tabulku v C#")

*Text alternativního obrázku: "příklad, jak duplikovat kontingenční tabulku v C# ukazující zdrojové a duplikované řádky kontingenční tabulky".*

---

## Krok 1: Načtení Excel sešitu C# – Otevření souboru

První věc, kterou musíte udělat, když chcete **load excel workbook c#**, je vytvořit instanci `Workbook`, která ukazuje na váš soubor. Tento objekt vám poskytuje přístup ke každému listu, buňce a kontingenční tabulce v souboru.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Proč je to důležité:**  
`Workbook` abstrahuje celý Excel soubor do modelu v paměti. Bez předchozího načtení nemůžete zkontrolovat umístění kontingenční tabulky ani kopírovat řádky. Konstruktor také automaticky detekuje formát souboru (XLS, XLSX, CSV atd.), takže není potřeba další kód pro detekci formátu.

---

## Krok 2: Jak kopírovat řádky – Definování oblasti kontingenční tabulky

Nyní, když je sešit v paměti, musíme Aspose.Cells říct, které řádky obsahují kontingenční tabulku. V našem příkladu kontingenční tabulka leží v **A1:J20**, což odpovídá řádkům **0‑19** (indexování od nuly). Zabalíme to do struktury `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Proč používáme `CellArea`:**  
Je to lehký způsob, jak popsat obdélníkový blok. Když později zavoláte `CopyRows`, metoda čte tento objekt a přesně ví, které řádky má duplikovat. Pokud budete muset upravit rozsah (např. kontingenční tabulka se rozroste do sloupce K), stačí změnit hodnotu `endColumn`.

---

## Krok 3: Přístup k cílovému listu

Většina sešitů má jediný list, ale API funguje stejně i pro více listů. Získejte první list (index 0) – tam je umístěna původní kontingenční tabulka.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro tip:**  
Pokud máte pojmenované listy, můžete je také získat podle názvu: `workbook.Worksheets["Sheet1"]`. To pomáhá vyhnout se pevně zakódovaným indexům, když se struktura sešitu změní.

---

## Krok 4: Jak kopírovat řádky – Duplikování kontingenční tabulky

Zde je jádro **how to duplicate pivot**: kopírujeme řádky obsahující kontingenční tabulku na nové místo. V našem případě začínáme na řádku 31 (index 30). Metoda `CopyRows` kopíruje *obojí* – data i podkladovou pivot cache, takže nové řádky se chovají přesně jako originál.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Co se děje pod kapotou?**  
`CopyRows` klonuje každý řádek, zachovává vzorce, styly i definice kontingenčních tabulek. Protože cache kontingenční tabulky žije na úrovni sešitu, duplikovaná tabulka automaticky odkazuje na stejný zdroj dat – není potřeba žádná další konfigurace.

**Okrajový případ – skryté řádky:**  
Pokud jsou některé řádky ve zdrojovém rozsahu skryté, zůstanou skryté i po kopírování. Pokud je chcete odkrýt, zavolejte po kopírování `worksheet.Rows[destRow].IsHidden = false`.

---

## Krok 5: Uložení sešitu – Ověření duplikátu

Nakonec zapíšeme změny zpět na disk. Můžete přepsat původní soubor nebo, bezpečněji, uložit pod novým názvem, abyste mohli porovnat před a po.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Výsledek, který byste měli vidět:**  
Otevřete `CopyWithPivot.xlsx`. Najdete původní kontingenční tabulku v **A1:J20** a identickou kopii začínající na **A31:J50**. Obě tabulky lze nezávisle obnovit a jakékoli řezače (slicery) připojené k originálu budou fungovat i pro kopii, protože sdílejí stejnou cache.

---

## Časté otázky a varianty

### Můžu duplikovat více kontingenčních tabulek najednou?

Ano. Projděte všechny kontingenční tabulky (`worksheet.PivotTables`) a každou jejich oblast zkopírujte na jiné cílové místo. Jen se ujistěte, že cílové oblasti se nepřekrývají.

### Co když je zdrojový sešit chráněn heslem?

Aspose.Cells vám umožní otevřít chráněný soubor předáním hesla do konstruktoru `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Jak kopírovat řádky bez ovlivnění vzorců?

Pokud potřebujete jen *hodnoty* (bez vzorců), použijte `CopyRows` s příznakem `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Existuje způsob, jak kopírovat řádky do *jiného* sešitu?

Ano. Po zkopírování řádků v původním listu můžete list klonovat do jiného `Workbook` pomocí `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Pro tipy pro spolehlivou automatizaci Excelu při kopírování řádků

- **Ověřte rozsah** před kopírováním. Rychlá podmínka `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` zabraňuje chybám mimo rozsah.  
- **Vypněte výpočty** při kopírování velkých oblastí: `workbook.Settings.CalcMode = CalcMode.Manual;` – to výrazně zrychlí operaci.  
- **Uvolněte objekty** (`workbook.Dispose()`), pokud zpracováváte mnoho souborů ve smyčce, aby se uvolnily nativní zdroje.  
- **Zaznamenávejte operaci** – zejména v produkčních pipelinech – abyste mohli sledovat, které soubory byly zpracovány, a včas zachytit selhání.

---

## Závěr

Nyní už víte **how to duplicate pivot** tabulky v C# pomocí Aspose.Cells a viděli jste celý workflow od **load excel workbook c#** po **excel automation copy rows** až po uložení výsledku. Příklad je samostatný, funguje ihned a lze jej rozšířit pro zpracování více kontingenčních tabulek, chráněných souborů nebo kopírování mezi sešity.

Další kroky? Zkuste upravit skript tak, aby:

- Obnovil duplikovanou kontingenční tabulku programově (`pivotTable.RefreshData();`).  
- Exportoval duplikovanou oblast do CSV pro následné zpracování.  
- Integroval kód do ASP.NET Core API, aby uživatelé mohli nahrát soubor a okamžitě získat verzi s duplikovanou kontingenční tabulkou.

Šťastné programování a ať je vaše automatizace Excelu vždy plynulá!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}