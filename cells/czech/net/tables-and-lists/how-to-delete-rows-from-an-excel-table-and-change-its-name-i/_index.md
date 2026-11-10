---
category: general
date: 2026-10-01
description: Naučte se mazat řádky z tabulky Excel a měnit název tabulky Excel pomocí
  C#. Průvodce krok za krokem s kompletním kódem a osvědčenými postupy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: cs
lastmod: 2026-10-01
og_description: Odstraňte řádky z tabulky v Excelu a změňte název tabulky v Excelu
  v C#. Postupujte podle tohoto kompletního tutoriálu, který načte sešit, upraví tabulku
  a uloží výsledek.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Smazat řádky z Excel tabulky a změnit její název v C# – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak smazat řádky z tabulky Excel a změnit její název v C#
url: /cs/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odstranit řádky z tabulky v Excelu a změnit její název v C#

Pokud potřebujete **odstranit řádky z tabulky v Excelu** při práci s C#, tento návod ukazuje přesné kroky, které jsou potřeba. Uvidíte, jak **načíst sešit Excelu v C#**, odstranit konkrétní řádky z tabulky a poté **aktualizovat název tabulky v Excelu**, aby soubor zůstal konzistentní.

Tutoriál pokrývá vše, co potřebujete vědět: požadované NuGet balíčky, kompletní spustitelný kód a běžné úskalí, jako jsou porušení struktury tabulky. Na konci článku budete umět libovolnou tabulku v Excelu upravovat programově bez ručního zásahu.

## Předpoklady

Než začnete, ujistěte se, že máte:

* .NET 6.0 SDK nebo novější nainstalovaný.
* Visual Studio 2022 (nebo jakékoli C# IDE) nastavené pro vývoj v .NET.
* Knihovnu **Aspose.Cells for .NET** přidanou přes NuGet (`Install-Package Aspose.Cells`).
* Existující sešit Excel (`Table.xlsx`), který obsahuje alespoň jeden list s tabulkou.

Tyto položky poskytují prostředí potřebné k **load Excel workbook c#** kódu a spolehlivému provedení operací.

## Krok 1: Načtení sešitu obsahujícího tabulku

Prvním krokem je otevření souboru sešitu. Aspose.Cells načte celý sešit do paměti a dává vám plnou kontrolu nad listy, tabulkami a daty buněk.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Proč je to důležité*: Načtení sešitu je základem pro jakoukoli následnou manipulaci s tabulkou. Objekt `Workbook` vystavuje kolekci `Worksheets`, kterou použijete k nalezení cílové tabulky.

## Krok 2: Přístup k prvnímu listu a jeho první tabulce

Většina souborů Excel ukládá tabulky do prvního listu, ale můžete upravit index podle potřeby. Následující kód získá první objekt `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Pokud list neobsahuje žádnou tabulku, `sheet.Tables.Count` bude nula a měli byste tento případ ošetřit. Pokus o přístup k `sheet.Tables[0]`, když žádné tabulky neexistují, vyvolá výjimku, proto se v produkčním kódu doporučuje použít guard clause.

## Krok 3: Odstranění řádků z tabulky v Excelu

Pro **odstranění řádků z tabulky v Excelu** zavolejte `DeleteRows(startRow, totalRows)`. Parametr `startRow` je nulově indexovaný relativně k první datové řádce tabulky (řádka za záhlavím).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Proč použít `DeleteRows` místo mazání řádků listu?

`DeleteRows` aktualizuje interní rozsah tabulky, zachovává vzorce, styly a definované názvy, které patří k tabulce. Přímé mazání řádků listu by mohlo narušit strukturu tabulky a vyvolat výjimku.

**Hraniční případ**: Pokud by smazání zanechalo tabulku bez datových řádků, Aspose.Cells vyhodí `ArgumentException`. Ochráníte se tím, že před smazáním zkontrolujete `table.RowCount`.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Krok 4: Změna názvu tabulky v Excelu

Po odstranění řádků možná budete chtít tabulce přiřadit popisnější identifikátor. Vlastnost `Name` nastavuje definovaný název tabulky, který se používá ve vzorcích a VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Proč přejmenovávat?* Jasný název tabulky zlepšuje čitelnost ve vzorcích (`=SUM(SalesData2026[Amount])`) a zabraňuje kolizím názvů, když více tabulek slouží podobným účelům.

## Krok 5: Uložení upraveného sešitu (volitelné)

Uložte změny buď do nového souboru, nebo přepište originál. Ukládání na nové místo je během vývoje bezpečnější.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Metoda `Save` zapíše aktualizovaný sešit, včetně změněného rozsahu tabulky a nového názvu tabulky, na disk.

## Kompletní funkční příklad

Spojením všech kroků získáte samostatný program, který můžete spustit okamžitě.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Očekávaný výstup** (za předpokladu, že soubor a tabulka existují):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Spuštěním programu se soubor Excel aktualizuje přesně podle popisu: řádky jsou odstraněny, název tabulky se změní a výsledek se uloží bez ruční úpravy.

## Často kladené otázky a řešení problémů

| Otázka | Odpověď |
|----------|--------|
| *Co se stane, pokud tabulka zasahuje sloučené buňky?* | `DeleteRows` respektuje sloučené oblasti. Pokud sloučená buňka překračuje hranici mazání, Aspose.Cells automaticky upraví sloučení. Výsledek vizuálně zkontrolujte, pokud spoléháte na složité sloučení. |
| *Mohu mazat řádky z tabulky, která je součástí pivot cache?* | Mazání řádků ze zdrojové tabulky, která napájí kontingenční tabulku, **ne**obnoví pivot cache automaticky. Po úpravě zdrojové tabulky zavolejte `pivotTable.RefreshData()`. |
| *Je možné mazat řádky na základě podmínky (např. hodnota < 0)?* | Ano. Projděte `table.ListObjects` nebo `table.Rows`, najděte odpovídající řádky, shromážděte jejich indexy a pro každý rozsah zavolejte `DeleteRows`. |
| *Musím uvolnit objekt `Workbook`?* | `Workbook` implementuje `IDisposable`. Zabalte jej do bloku `using` pro deterministické uvolnění prostředků, zejména při zpracování velkých souborů. |
| *Jak se to liší od použití EPPlus?* | EPPlus také podporuje manipulaci s tabulkami, ale používá odlišné API (`ExcelTable`). Koncepty načtení sešitu, mazání řádků a přejmenování tabulky jsou analogické. Vyberte knihovnu, která odpovídá vašim licenčním požadavkům. |

## Nejlepší postupy při úpravě tabulek v Excelu v C#

* **Validujte indexy** – Indexy řádků tabulky jsou nulově indexované; chyby typu off‑by‑one způsobí nečekané mazání.
* **Kontrolujte kolize názvů** – Excel neumožňuje duplicitní definované názvy; před přiřazením nového názvu vždy ověřte jedinečnost.
* **Zálohujte originální soubory** – Automatizované skripty mohou data poškodit; uchovejte si kopii zdrojového sešitu.
* **Používejte `using` bloky** – Zajišťují včasné uvolnění souborových handle:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Testujte hraniční případy** – Tabulky s jediným datovým řádkem, tabulky, které zabírají celý list, a tabulky propojené s grafy by měly být po změnách ověřeny.

## Závěr

Nyní víte, jak **odstranit řádky z tabulky v Excelu** a **změnit název tabulky v Excelu** pomocí C#. Kompletní řešení načte sešit, získá cílovou tabulku, odstraní požadované řádky, přejmenuje tabulku a výsledek uloží. Použijte tyto techniky k automatizaci generování reportů, čištění dat nebo jakéhokoli workflow, který vyžaduje programovou správu tabulek v Excelu.

Dále prozkoumejte související témata, jako je **aktualizace hodnot buněk v tabulce Excel**, **přidávání nových řádků programově** a **export dat tabulky do CSV**. Ovládnutí těchto operací vám poskytne plnou kontrolu nad soubory Excel z vašich C# aplikací.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Table in C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Get First Table from Excel Workbook in C# – Complete Guide](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}