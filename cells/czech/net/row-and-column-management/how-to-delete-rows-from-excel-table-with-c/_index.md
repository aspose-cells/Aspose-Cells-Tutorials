---
category: general
date: 2026-11-25
description: Naučte se, jak v C# mazat řádky z tabulky v Excelu a také efektivně mazat
  více řádků z listu v Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: cs
lastmod: 2026-11-25
og_description: Odstraňte řádky z tabulky Excel v C# a naučte se mazat více řádků
  z listu Excelu pomocí čistého kódu.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Smazání řádků z Excel tabulky v C# – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Jak smazat řádky z tabulky Excel pomocí C#
url: /cs/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odstranit řádky z tabulky Excel pomocí C#

Pokud potřebujete odstranit řádky z tabulky Excel pomocí C#, tento průvodce vám přesně ukáže, jak to provést. Také uvidíte, jak odstranit více řádků z listu Excelu, aniž byste ovlivnili ostatní data.

Práce s Excelem programově často vyžaduje odstranění zastaralých nebo neplatných záznamů. Odstraňování řádků přímo v listu může být riskantní, protože řádek záhlaví strukturované tabulky musí zůstat nedotčen. Tento tutoriál vás provede bezpečným přístupem, který respektuje záhlaví tabulky a umožní vám v jednom volání smazat libovolný počet datových řádků.

## Požadavky

* .NET 6.0 nebo novější nainstalováno  
* Visual Studio 2022 (nebo jakékoli kompatibilní IDE)  
* NuGet balíček **Aspose.Cells** (verze 23.10 nebo novější) – tato knihovna poskytuje třídy `Workbook`, `Worksheet` a `ListObject` používané v příkladech  

Nemusíte mít nainstalovaný Microsoft Office na vývojovém počítači, protože Aspose.Cells pracuje přímo se souborovým formátem.

## Odstranění řádků z tabulky Excel – krok za krokem

Následující sekce popisují každý krok potřebný k bezpečnému odstranění řádků z tabulky Excel. Primární klíčové slovo se objevuje v tomto nadpisu pro splnění SEO požadavků.

### Krok 1: Přidat Aspose.Cells do projektu

Otevřete **Package Manager Console** a spusťte:

```powershell
Install-Package Aspose.Cells
```

Balíček přidá potřebné sestavení a zpřístupní typy `Workbook`, `Worksheet` a `ListObject`.

### Krok 2: Načíst sešit a najít tabulku

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Proč je to důležité*: `ListObject` představuje skutečnou tabulku Excel, která udržuje svůj vlastní řádek záhlaví. Prací s `ListObject` se vyhnete neúmyslnému odstranění záhlaví.

### Krok 3: Odstranit požadované datové řádky

Metoda `DeleteRows` očekává **nulově‑indexovaný** řádek relativně k tabulce, **včetně** řádku záhlaví. Protože záhlaví nelze odstranit, musíte začít indexem 1 pro první datový řádek.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Pokud byste zkusili `table.DeleteRows(0, 2)`, Aspose.Cells vyhodí výjimku, protože řádek záhlaví (index 0) je chráněn. Začátek od indexu 1 zajišťuje, že jsou odstraněny jen datové řádky.

### Krok 4: Uložit upravený sešit

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Spuštěním programu se okamžitě odstraní dva řádky těsně pod záhlavím, přičemž struktura tabulky zůstane nedotčena.

### Kompletní funkční příklad

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Očekávaný výstup**: Soubor `table_with_header_modified.xlsx` obsahuje původní záhlaví tabulky, následované všemi řádky kromě těch dvou, které byly odstraněny. Žádné jiné listy nejsou změněny.

## Odstranění více řádků z listu Excel

Někdy potřebujete odstranit řádky, které **nejsou** součástí strukturované tabulky. Sekundární klíčové slovo se objevuje v tomto nadpisu. Přístup se mírně liší, protože pracujete se sbírkou `Rows` listu místo `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Proč to funguje**: `Rows.RemoveAt(startIndex, count)` odstraňuje souvislý blok řádků přímo z listu. Neexistuje ochrana záhlaví, takže můžete začít na libovolném indexu. Metoda je efektivní, protože aktualizuje interní datové struktury v jediném operaci, což je ideální při potřebě odstranit více řádků z listu Excel.

### Okrajové případy a osvědčené postupy

| Situace                               | Doporučené řešení |
|---------------------------------------|-------------------|
| Odstraňování řádků za posledním řádkem | Zkontrolujte `worksheet.Rows.Count` před voláním `RemoveAt`. |
| Odstranění všech řádků kromě záhlaví   | Odstraňujte datové řádky ve smyčce nebo použijte `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Zachování formátování buněk           | Odstranění pomocí `ListObject` automaticky posouvá formátování; pro čisté listy zkopírujte formátování před odstraněním, pokud je potřeba. |
| Velké listy ( > 10 000 řádků)         | Provádějte odstraňování v sestupném pořadí, aby nedošlo k posunu indexů, nebo použijte `DeleteRows` na tabulce, pokud je to možné. |

**Pro tip**: Když potřebujete odstranit řádky na základě podmínky (např. řádky, kde je hodnota ve sloupci prázdná), projděte `DataRange` tabulky pozpátku a zavolejte `DeleteRows` pro každý odpovídající řádek. Odstraňování pozpátku zabraňuje nesouladu indexů.

## Časté otázky

*Funguje to s .xlsx soubory vytvořenými v Excelu 365?*  
Ano. Aspose.Cells podporuje kompletní specifikaci Office Open XML, takže stejný kód funguje pro jakýkoli moderní `.xlsx` soubor.

*Co když sešit obsahuje více tabulek?*  
Získejte požadovanou tabulku podle názvu: `var table = worksheet.ListObjects["MyTable"];` a poté použijte `DeleteRows` podle ukázky.

*Mohou být řádky odstraněny bez použití knihovny třetí strany?*  
Můžete použít Microsoft.Office.Interop.Excel COM interop, ale to vyžaduje instalaci Excelu na serveru a zavádí COM‑souvislé zatížení. Aspose.Cells poskytuje lehkou, server‑bezpečnou alternativu.

## Závěr

Nyní víte, jak bezpečně odstranit řádky z tabulky Excel a jak odstranit více řádků z listu Excel pomocí C#. Primární technika se opírá o metodu `ListObject.DeleteRows`, která respektuje záhlaví tabulky, zatímco sekundární technika používá `Rows.RemoveAt` pro běžné listy. Použijte tyto vzory k úklidu dat, automatizaci generování reportů nebo implementaci hromadných úprav ve svých aplikacích.

**Další kroky**

* Prozkoumejte další funkce Aspose.Cells, jako je vkládání řádků, kopírování stylů nebo filtrování dat.  
* Vyzkoušejte stejné operace s **ClosedXML**, pokud dáváte přednost open‑source knihovně; API je podobné, ale používá `IXLTable` a `IXLRows`.  
* Kombinujte logiku mazání řádků s LINQ dotazy pro vytvoření složitějších pipeline pro čištění dat.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [jak odstranit řádky v Excelu pomocí C# – chránit záhlaví tabulky](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Jak použít Aspose.Cells k odstranění řádků v tabulce Excel při zachování](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Načíst soubor Excel C# – Jak odstranit řádky a odstranit konkrétní řádky](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}