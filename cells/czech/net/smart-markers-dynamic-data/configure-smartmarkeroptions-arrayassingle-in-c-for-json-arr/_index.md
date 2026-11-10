---
category: general
date: 2026-09-21
description: V C# nakonfigurujte SmartMarkerOptions ArrayAsSingle tak, aby exportoval
  JSON pole jako jedinou hodnotu buňky v sešitu Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: cs
lastmod: 2026-09-21
og_description: Nastavte SmartMarkerOptions ArrayAsSingle v C# pro export JSON polí
  jako jediné hodnoty buňky. Získejte kompletní řešení krok za krokem.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Konfigurace SmartMarkerOptions ArrayAsSingle v C# – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Nastavte SmartMarkerOptions ArrayAsSingle v C# pro JSON pole
url: /cs/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konfigurace SmartMarkerOptions ArrayAsSingle v C# pro JSON pole

Pokud potřebujete **konfigurovat SmartMarkerOptions ArrayAsSingle** při generování Excel souborů pomocí Aspose.Cells, tento průvodce vám přesně ukáže, jak na to. Uvidíte, jak zachovat JSON pole v jednom buňce místo rozdělení jeho prvků do několika řádků.

Práce s JSON daty v tabulkách často znamená volbu mezi rozbaleným pohledem a kompaktní reprezentací. V mnoha scénářích reportování — například při ukládání seznamu štítků nebo sady identifikátorů — chcete, aby celý JSON řetězec zůstal v jedné buňce. Příznak **ArrayAsSingle** v `SmartMarkerOptions` to umožňuje.

V tomto tutoriálu se naučíte:

* Vytvořit `DataTable`, který v jednom sloupci obsahuje JSON pole.
* Umístit Smart Markery do listu Excelu.
* **Konfigurovat SmartMarkerOptions ArrayAsSingle**, aby byl JSON pole zpracován jako jediná hodnota buňky.
* Zpracovat markery a uložit sešit.
* Ověřit výstup.

> **Předpoklady** – Potřebujete knihovnu Aspose.Cells pro .NET (v13.12 nebo novější) a vývojové prostředí .NET (doporučeno Visual Studio 2022). Předpokládá se základní znalost C# a DataTables.

---

## Krok 1: Připravte zdroj dat s JSON polem

Nejprve vytvořte `DataTable`, který napodobuje data, jež byste získali ze služby nebo databáze. Sloupec **Names** obsahuje JSON‑kódovaný řetězec představující pole jmen.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Proč tento krok?*  
Smart Markery čtou data přímo z .NET objektů. Umístěním JSON pole do sloupce typu string zachováte přesnou syntaxi JSON, která pak může být nezměněna zapsána do buňky.

---

## Krok 2: Vložte Smart Markery do nového sešitu

Vytvořte nový sešit, vyberte první list a zapište Smart Markery, které odkazují na celou tabulku a konkrétní sloupec **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Marker `&=dataTable.Names` říká Aspose.Cells, aby nahradil buňku hodnotou sloupce **Names** pro každý řádek v `dataTable`. Protože máme jen jeden řádek, marker bude zpracován jednou.

---

## Krok 3: **Konfigurovat SmartMarkerOptions ArrayAsSingle**

Ve výchozím nastavení Aspose.Cells rozbalí řetězec podobný poli do samostatných řádků. Nastavením `ArrayAsSingle` na `true` přepíšete toto chování a vynutíte, aby celý JSON řetězec zůstal v jedné buňce.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Proč povolit `ArrayAsSingle`?*  
Když je `ArrayAsSingle` nastaveno na `false`, engine interpretuje `["Alice","Bob"]` jako dvě samostatné hodnoty a zapíše je do sousedních řádků. Nastavením na `true` se řetězec zachází jako atomická hodnota, což je nezbytné pro zachování JSON formátu v Excelu.

---

## Krok 4: Zpracujte Smart Markery s nakonfigurovanými možnostmi

Nyní spusťte engine Smart Marker a předávejte objekt možností, který jste právě nakonfigurovali.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Během zpracování Aspose.Cells načte `dataTable`, aplikuje markery a respektuje příznak `ArrayAsSingle`, takže JSON pole zůstane nedotčeno.

---

## Krok 5: Uložte sešit a ověřte výsledek

Nakonec zapište sešit na disk. Otevřete vygenerovaný soubor v Excelu nebo jiném prohlížeči tabulek a potvrďte, že buňka **A2** obsahuje přesně ten JSON řetězec.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Očekávaný výstup

| A   |
|-----|
| **["Alice","Bob"]** |

Buňka **A2** zobrazuje JSON pole jako jedinou textovou hodnotu, přesně tak, jak je uloženo v `DataTable`. Žádné další řádky nejsou vytvořeny.

---

## Běžné varianty a řešení okrajových případů

| Situace | Jak přizpůsobit |
|-----------|--------------|
| **Více řádků s JSON poli** | Stejné nastavení `ArrayAsSingle` funguje; JSON pole každého řádku zůstane ve své buňce. |
| **Různé JSON struktury (objekty, vnořená pole)** | Dokud je JSON uložen jako řetězec, `ArrayAsSingle` jej zachová beze změny. U složitějších objektů může být potřeba escapovat uvozovky. |
| **Použití jiného zdroje dat (např. List\<T\>)** | Nahraďte `DataTable` libovolnou kolekcí implementující IEnumerable; syntax markeru (`&=myList.Property`) zůstane stejná. |
| **Export do CSV místo XLSX** | `ArrayAsSingle` stále platí, ale pamatujte, že CSV neuchovává formátování buněk; může být nutné JSON zabalit do uvozovek. |

**Tip:** Vždy nastavte `ArrayAsSingle` *před* voláním `ProcessSmartMarkers`. Změna příznaku po zpracování nemá vliv na již vygenerované buňky.

---

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny `using` direktivy a komentáře pro přehlednost.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Spusťte program, otevřete `SmartMarkerJson.xlsx` a uvidíte, že JSON pole je zachováno v buňce **A2**.

---

## Závěr

Nyní víte, jak **konfigurovat SmartMarkerOptions ArrayAsSingle** v C# pro zachování JSON pole jako jediné buňky při použití smart markerů Aspose.Cells. Kroky — příprava `DataTable`, vložení markerů, nastavení příznaku `ArrayAsSingle`, zpracování a uložení — tvoří opakovatelný vzor, který můžete aplikovat na jakýkoli scénář, kde je potřeba kompaktní JSON reprezentace v Excelu.

Dále můžete zkusit:

* **Smart markery Aspose.Cells** pro iteraci přes kolekce.
* Export **vnořených JSON objektů** úpravou formátování buněk.
* Kombinaci **podmíněného formátování** se smart markery pro bohatší reporty.

Neváhejte experimentovat s různými datovými strukturami a sdílet své poznatky. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Vytvoření Excel sešitu z JSON – Kompletní průvodce Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Vytvoření a konfigurace Excel sešitu Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Vytvoření a konfigurace Excel sešitu Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}