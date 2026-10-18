---
category: general
date: 2026-10-10
description: Rychle aplikujte formát čísel v Excelu importováním DataTable, nastavením
  formátů data a měny a zachováním řádku s hlavičkou v jediném kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: cs
lastmod: 2026-10-10
og_description: aplikovat formát čísel v Excelu v C# pomocí Aspose.Cells. Naučte se
  nastavit formát data v Excelu, nastavit formát měny v Excelu a zachovat řádek záhlaví
  v Excelu při importu DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Použít formát čísel v Excelu v C# – průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Jak použít číselný formát v Excelu s Aspose.Cells
url: /cs/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít formát čísel v Excelu s Aspose.Cells

Pokud potřebujete **apply number format excel** při načítání dat z `DataTable`, tento průvodce vám přesně ukáže, jak na to. Také se naučíte, jak **set date format excel**, **set currency format excel** a **preserve header row excel** během importu, takže výsledný list vypadá profesionálně bez dalšího post‑processingu.

Provedeme vše od instalace knihovny až po napsání kompletního spustitelného úryvku. Na konci budete schopni importovat libovolný `DataTable` do Excel sešitu, automaticky formátovat číselné sloupce a zachovat řádek záhlaví neporušený — vše během několika řádků C#.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.6+)
* Visual Studio 2022 (nebo jakékoli C# IDE, které preferujete)
* **Aspose.Cells for .NET** – instalace přes NuGet:

```bash
dotnet add package Aspose.Cells
```

* Zdroj `DataTable` – příklad používá pomocnou metodu `GetTable()`, která vrací ukázková data.

> **Tip:** Aspose.Cells je komerční knihovna, ale nabízí bezplatný evaluační režim, který vypne vodoznak až na 30 dní.

## Krok 1: Vytvořte sešit a přistupte k prvnímu listu

Objekt workbook je vstupním bodem pro všechny operace v Excelu. Vytvořením nového sešitu získáte výchozí list na indexu 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Proč tento krok?*  
`Workbook` spravuje formát souboru, výpočetní engine a úložiště stylů. Včasný přístup k `Worksheet` nám umožní později předat cílový list metodě importu.

## Krok 2: Získejte zdrojová data jako DataTable

V reálných projektech data často pocházejí z databázového dotazu, CSV parseru nebo odpovědi API. Pro ilustraci vygenerujeme jednoduchý `DataTable` se třemi sloupci: **Product**, **Price** a **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Proč tento krok?*  
`DataTable` poskytuje tabulární reprezentaci v paměti, kterou Aspose.Cells může importovat přímo, zachovávající pořadí sloupců a datové typy.

## Krok 3: Připravte pole `Style` – jeden styl na sloupec

Aspose.Cells vám umožňuje aplikovat odlišný styl na každý sloupec během importu předáním pole objektů `Style`. Délka pole musí odpovídat počtu sloupců ve zdrojové tabulce.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Proč tento krok?*  
Pokud vynecháte explicitní vytvoření (`CreateStyle()`), pokus o nastavení `Number` vyvolá `NullReferenceException`. Inicializace každého `Style` zajišťuje, že pozdější přiřazení uspějí.

## Krok 4: Přiřaďte formáty čísel – měna a datum

Excel rozpoznává vestavěné formáty čísel podle ID.

* **14** – Měna (např. `$1,234.00`)  
* **22** – Krátký datum (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Poznámka:** Pokud potřebujete vlastní formát (např. `"¥#,##0.00"`), použijte `Style.Custom = "¥#,##0.00"` místo vestavěného ID.

*Proč tento krok?*  
Aplikace správného **number format** při importu eliminuje potřebu druhého průchodu, který by procházel buňky a měnil formátování. Také to zaručuje, že **format excel cells date** a **set currency format excel** jsou konzistentní ve všech řádcích.

## Krok 5: Importujte DataTable při zachování řádku záhlaví

Metoda `ImportDataTable` může kopírovat data, zachovat první řádek jako záhlaví a aplikovat připravené styly sloupců.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Očekávaný výstup** – Otevřete `FormattedReport.xlsx` a uvidíte:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

Řádek záhlaví je neporušený, sloupec **Price** zobrazuje symbol měny a sloupec **ReleaseDate** ukazuje formát krátkého data — vše bez dalšího kódu pro stylování.

### Řešení běžných okrajových případů

| Situace                               | Řešení |
|----------------------------------------|----------|
| **Více sloupců než stylů**           | Ujistěte se, že `columnStyles.Length` se rovná `sourceTable.Columns.Count`. Chybějící položky použijí výchozí styl sešitu. |
| **Null hodnoty v číselných sloupcích**     | Excel zachází s `null` jako s prázdnou buňkou; formát čísla se stále použije, když je hodnota později zadána. |
| **Vlastní měna specifická pro locale**    | Použijte `columnStyles[i].Custom = "\"€\"#,##0.00"` a nastavte `columnStyles[i].Number = -1`, aby se zakázalo vestavěné ID. |
| **Velké tabulky ( > 100 000 řádků )**    | Zvažte použití přetížení `ImportDataTable` s `ImportTableOptions` pro streamování dat a snížení zatížení paměti. |
| **Aplikace stejného stylu na více sloupců** | Znovu použijte stejnou instanci `Style` v poli (např. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Použití vlastního řetězce formátu

Pokud vestavěná ID nevyhovují vašim potřebám, můžete definovat vlastní formát čísla:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Tento přístup vám dává plnou kontrolu nad **format excel cells date** a **set currency format excel** nad rámec předdefinovaných ID.

## Závěr

Nyní víte, jak efektivně **apply number format excel** při importu `DataTable` s Aspose.Cells. Vytvořením pole `Style` pro každý sloupec, přiřazením vestavěných nebo vlastních číselných ID a použitím přetížení `ImportDataTable`, které **preserve header row excel**, můžete v jedné operaci vytvořit listy připravené k publikaci.

### Co dál?

* Prozkoumejte **set date format excel** s vlastními vzory jako `"dddd, mmmm dd, yyyy"`.
* Kombinujte tuto techniku s **conditional formatting** pro zvýraznění hodnot mimo rozsah.
* Použijte **format excel cells date** v kontingenčních tabulkách nebo grafech pro dynamické reportování.

Neváhejte experimentovat s různými ID čísel nebo vlastními řetězci, aby odpovídaly stylovému průvodci vaší organizace. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}