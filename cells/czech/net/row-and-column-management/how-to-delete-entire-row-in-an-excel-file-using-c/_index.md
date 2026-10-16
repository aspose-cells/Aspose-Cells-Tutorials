---
category: general
date: 2026-10-10
description: Naučte se, jak smazat celý řádek v sešitu Excel pomocí C#. Tento krok‑za‑krokem
  průvodce také popisuje, jak smazat řádek podle indexu a odstranit řádek podle indexu
  pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: cs
lastmod: 2026-10-10
og_description: Odstraňte celý řádek v sešitu Excel pomocí C#. Postupujte podle tohoto
  návodu, abyste se naučili, jak smazat řádek podle indexu, odstranit řádek podle
  indexu a bezpečně uložit soubor.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Odstraňte celý řádek v Excelu pomocí C# – kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Jak smazat celý řádek v souboru Excel pomocí C#
url: /cs/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Smazat celý řádek v souboru Excel pomocí C#

Pokud potřebujete **smazat celý řádek** v sešitu Excel, tento průvodce vám přesně ukáže, jak to provést pomocí C#. Ať už čistíte importovaná data nebo vytváříte nástroj pro reportování, níže uvedené kroky vám umožní odstranit řádek podle jeho indexu a uložit výsledek bez ztráty ostatních dat.

Také uvidíte, jak stejný přístup odpovídá na otázku **how to delete row** podle indexu, jak **remove row by index**, a proč to funguje pro scénáře **delete row excel** v C#.

## Požadavky

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+)  
* Knihovna **Aspose.Cells for .NET** (k dispozici přes NuGet: `Install-Package Aspose.Cells`)  
* Základní znalost C# konzolových nebo desktopových projektů  

Žádné další komponenty Excel interop nebo COM nejsou vyžadovány, což udržuje řešení lehké a bezpečné pro server‑side provádění.

## Krok 1: Nastavení projektu a importování jmenných prostorů

Vytvořte novou konzolovou aplikaci (nebo přidejte kód do existujícího projektu) a přidejte požadované `using` direktivy:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Proč je to důležité*: Importování `Aspose.Cells` vám poskytuje přístup k `Workbook`, `Worksheet` a metodě `DeleteRows`, která provádí skutečné odstranění řádku.

## Krok 2: Načtení sešitu a výběr listu

Musíte načíst zdrojový soubor (`input.xlsx`) a získat list, který chcete upravit. První list je přístupný pomocí indexu `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: Pokud potřebujete pracovat s konkrétním listem, nahraďte index názvem listu: `workbook.Worksheets["Data"]`.

## Krok 3: Smazání celého řádku podle jeho nul‑základního indexu

Aspose.Cells používá nul‑základní indexování, takže první řádek má index `0`. Pro smazání řádku 5 (šestý vizuální řádek) zavolejte `DeleteRows` s parametrem `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Vysvětlení*:

* `ws.Cells[5, 0]` ukazuje na první buňku řádku, který chcete smazat.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` říká Aspose.Cells, aby odstranil **1** řádek, a příznak `DeleteEntireRow` zajišťuje, že **celý řádek** zmizí a řádky pod ním se posunou nahoru.

### Jak smazat řádek podle indexu v jiných scénářích

* **Smazat více po sobě jdoucích řádků** – změňte první argument na počet řádků, které chcete odstranit:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Smazat poslední řádek** – použijte `ws.Cells.MaxDataRow` k získání indexu nejspodnějšího vyplněného řádku:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Tyto úryvky odpovídají požadavku **remove row by index**, přičemž kód zůstává snadno čitelný.

## Krok 4: Uložení sešitu s odstraněným řádkem

Po odstranění zapište upravený sešit zpět na disk. Můžete přepsat původní soubor nebo vytvořit nový.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Pokud potřebujete zachovat původní soubor beze změny, stačí změnit výstupní cestu. Metoda `Save` podporuje mnoho formátů (`.xls`, `.csv`, `.pdf`, atd.) – stačí změnit příponu souboru.

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní, připravený k spuštění program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Očekávaný výstup**: Po spuštění programu bude `output.xlsx` obsahovat všechny původní řádky kromě toho, který začínal na vizuálním řádku 6. Všechna data pod odstraněným řádkem se automaticky posunou nahoru, přičemž zachovají vzorce a formátování.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Oprava |
|-------|----------------|-----|
| **Index mimo rozsah** | Pokus o smazání řádku s indexem, který neexistuje (např. `ws.Cells[1000,0]` v listu s 200 řádky) | Použijte `ws.Cells.MaxDataRow` k ověření nejvyššího platného indexu před voláním `DeleteRows`. |
| **Částečné smazání řádku** | Vynechání `DeleteOptions.DeleteEntireRow` vede k vymazání pouze obsahu buněk | Vždy předávejte `DeleteOptions.DeleteEntireRow`, když potřebujete odstranit celý řádek. |
| **Neočekávané změny ve vzorcích** | Mazání řádků, které jsou součástí rozsahu ve vzorci, může narušit odkazy | Po smazání přepočítejte vzorce (`workbook.CalculateFormula()`), pokud se váš sešit spoléhá na dynamické rozsahy. |
| **Ukládání na chráněné místo** | Volání `Save` vyhodí výjimku, pokud je složka chráněna | Ujistěte se, že cílový adresář je zapisovatelný, nebo spusťte program s odpovídajícími oprávněními. |

Řešením těchto problémů se řešení stane robustním pro produkční nasazení a splní dotazy **delete row excel** a **delete row c#**.

## Pokročilé: Mazání řádků na základě podmínky

Někdy potřebujete odstranit řádky, které splňují určitý kritérium (např. řádky, kde je sloupec A prázdný). Následující smyčka ukazuje bezpečný způsob, jak procházet odspodu nahoru a mazat odpovídající řádky:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Procházení směrem nahoru zabraňuje problému s posunem indexu, který nastává při mazání řádků během iterace dopředu.

## Závěr

Nyní víte, jak **delete entire row** v sešitu Excel pomocí C#. Průvodce pokryl:

* Načtení sešitu a výběr listu  
* Použití `DeleteRows` s `DeleteOptions.DeleteEntireRow` k **how to delete row** podle indexu  
* Bezpečné uložení upraveného souboru  
* Řešení okrajových případů, tipy na výkon a příklad podmíněného mazání  

S tímto znalostmi můžete sebejistě implementovat funkci **remove row by index**, automatizovat čištění dat a integrovat manipulaci s Excelem do jakékoli C# aplikace.  

**Další kroky**: prozkoumejte další funkce Aspose.Cells, jako je vkládání řádků, kopírování oblastí nebo převod sešitu do PDF — každá z nich staví na stejných objektech `Workbook` a `Worksheet`, které jste právě zvládli. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak smazat řádek v Excelu pomocí Aspose.Cells .NET: Kompletní průvodce](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Ochrana hlavičkového řádku v Excelu](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efektivní správa řádků v Excelu pomocí Aspose.Cells pro Java: Vkládání a mazání řádků](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}