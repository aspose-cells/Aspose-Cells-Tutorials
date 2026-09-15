---
category: general
date: 2026-02-28
description: Rychle odstraňte řádky v tabulce Excel v C#. Naučte se, jak přidat pojmenovaný
  rozsah v Excelu, přistupovat k listu podle názvu a vyhnout se chybám duplicitních
  názvů.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: cs
og_description: Smažte řádky v tabulce Excel pomocí C#. Tento tutoriál také ukazuje,
  jak přidat pojmenovaný rozsah v Excelu a přistupovat k listu podle názvu.
og_title: Odstranění řádků v Excelové tabulce pomocí C# – Kompletní průvodce
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Smazání řádků v tabulce Excel pomocí C# – krok za krokem
url: /cs/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odstranění řádků v Excel tabulce pomocí C# – Kompletní programovací tutoriál

Už jste někdy potřebovali **delete rows excel table** z sešitu, ale nebyli jste si jisti, kterou API volání použít? Nejste jediní – většina vývojářů narazí na stejnou překážku, když poprvé zkusí programově zmenšit tabulku.  

V tomto průvodci projdeme kompletním, spustitelným příkladem, který nejen odstraňuje řádky z Excel tabulky, ale také ukazuje **how to add defined name** (aka *named range*), jak **access worksheet by name**, a proč přidání duplicitního názvu na jiný list vyvolá `InvalidOperationException`.  

Do konce článku budete schopni:

* Získat list pomocí jeho názvu karty.  
* Bezpečně odstranit datové řádky z první tabulky na tomto listu.  
* Vytvořit pojmenovaný rozsah, který ukazuje na konkrétní adresu.  
* Pochopit úskalí duplicitních názvů napříč listy.

Žádná externí dokumentace není potřeba – vše, co potřebujete, je zde.

---

## Co budete potřebovat

* **DevExpress Spreadsheet** (nebo libovolná knihovna, která vystavuje objekty `Workbook`, `Worksheet`, `ListObject` a `Names`).  
* Projekt .NET cílící na **.NET 6** nebo novější (kód také kompiluje s .NET Framework 4.8).  
* Základní znalost C# – pokud umíte napsat `foreach` smyčku, jste připraveni.

> **Pro tip:** Pokud používáte bezplatnou Community Edition od DevExpress, API použité níže jsou identické s komerční verzí.

---

## Krok 1 – Přístup k listu podle názvu

Prvním krokem je najít list, který obsahuje tabulku, kterou chcete upravit.  
Většina vývojářů zvyklostně používá `Worksheets[0]`, což však svazuje váš kód s pořadím listů a selže, jakmile někdo přejmenuje kartu.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Proč je to důležité:* Použitím **name** listu místo jeho indexu se vyhnete nechtěným úpravám špatného listu, když se sešit změní.  

Pokud zadaný název neexistuje, knihovna vyhodí `KeyNotFoundException`, kterou můžete zachytit a zobrazit uživatelsky přívětivou chybovou zprávu.

---

## Krok 2 – Odstranění řádků v Excel tabulce (bezpečný způsob)

Nyní, když máte správný list, odebereme datové řádky z první tabulky.  
Častá chyba je volat `DeleteRows(1, rowCount‑1)`. Od **DevExpress 22.2** je tato přetížení **zakázáno** a vyvolá `InvalidOperationException`. Knihovna očekává, že řádky smažete **v rámci datové oblasti tabulky**, nikoli v hlavičce.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Co když je tabulka prázdná?** Ochranná podmínka `if` zabraňuje volání s `rowCount = 0`, což by jinak vyvolalo výjimku.

### Vizuální přehled  

![delete rows excel table example](image.png "Screenshot showing rows being removed from an Excel table")  

*Alt text: příklad odstranění řádků v Excel tabulce v C# kódu*

---

## Krok 3 – Jak přidat definovaný název (vytvořit pojmenovaný rozsah)

Po vyčištění tabulky můžete později chtít odkazovat na konkrétní oblast – například pro graf nebo seznam pro ověření dat. To je místo, kde přichází **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Metoda `Names.Add` přijímá dva parametry: identifikátor a adresu ve stylu A1.  
Protože jsme dříve použili **access worksheet by name**, může řetězec adresy bezpečně odkazovat na libovolný list, aniž byste se museli starat o změny indexů.

---

## Krok 4 – Pojmenovaný rozsah na jiném listu – Vyhněte se chybám duplicitního názvu

Možná si myslíte, že můžete stejný identifikátor použít na jiném listu, například takto:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Bohužel, rozsah pojmenování v Excelu je **celoprvkový** (workbook‑wide), nikoli na úrovni listu. Výše uvedené volání spustí `InvalidOperationException` s zprávou *„A name with the same identifier already exists.“*  

### Jak to obejít

1. **Zvolte jedinečný název** (`MyTable_Sheet2`).  
2. **Odstraňte existující název** před jeho opětovným přidáním (pouze pokud jej skutečně chcete nahradit).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Kompletní, spustitelný příklad

Spojením všech částí získáte samostatnou konzolovou aplikaci, kterou můžete vložit do Visual Studia a spustit proti ukázkovému souboru `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Očekávaný výsledek**

* Všechny datové řádky z první tabulky na **Sheet1** zmizí, zůstane jen hlavičkový řádek.  
* Název **MyTable** nyní ukazuje na `Sheet1!$A$1:$C$5`.  
* Druhý název **MyTable_Sheet2** bezpečně odkazuje na oblast na **Sheet2** bez vyhození výjimky.

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | Grab the correct `ListObject` by index (`worksheet.ListObjects[1]`) or by name (`worksheet.ListObjects["MyTable"]`). |
| *Can I delete rows from a table that spans multiple worksheets?* | No—tables are confined to a single sheet. You must repeat the delete logic for each sheet. |
| *Is there a way to delete only a subset of rows?* | Yes—use `table.DeleteRows(startRow, count)` where `startRow` is zero‑based within the table’s data area. |
| *Do named ranges survive after saving?* | Absolutely. Once you call `SaveDocument`, the names become part of the workbook’s XML. |
| *How do I list all defined names in the workbook?* | Iterate `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Závěr

Probrali jsme **delete rows excel table** pomocí C#, předvedli **add named range excel** a ukázali správný způsob **access worksheet by name**, který zabraňuje otravné výjimce duplicitního názvu.  

Kompletní řešení je v kódu výše – zkopírujte, vložte a spusťte ho na svých souborech. Odtud můžete rozšířit logiku pro práci s více tabulkami, dynamické výpočty rozsahů nebo dokonce integraci s UI.

**Další kroky**, které můžete prozkoumat:

* Použít **named range on another sheet** k napájení sérií grafu.  
* Kombinovat logiku mazání s **ExcelDataReader** pro import dat před jejich vyčištěním.  
* Automatizovat hromadné aktualizace napříč desítkami sešitů pomocí jednoduché smyčky `foreach (var file in Directory.GetFiles(...))`.

Máte další otázky ohledně automatizace Excelu v C#? Zanechte komentář a pojďme konverzaci posunout dál. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}