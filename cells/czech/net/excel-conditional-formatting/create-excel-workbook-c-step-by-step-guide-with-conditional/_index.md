---
category: general
date: 2026-03-27
description: Vytvořte Excel sešit v C# pomocí Aspose.Cells, aplikujte podmíněné formátování,
  importujte datovou tabulku do Excelu a uložte sešit jako xlsx – vše v jednom tutoriálu.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: cs
og_description: Vytvořte Excel sešit v C# pomocí Aspose.Cells, aplikujte podmíněné
  formátování, importujte datovou tabulku do Excelu a uložte sešit jako xlsx během
  několika minut.
og_title: Vytvoření Excel sešitu v C# – Kompletní průvodce s podmíněným formátováním
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvoření Excel sešitu v C# – krok za krokem průvodce s podmíněným formátováním
url: /cs/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v C# – Kompletní programovací tutoriál

Už jste někdy potřebovali **create excel workbook c#** za běhu, ale nevedeli ste, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když poprvé automatizují reporty. V tomto průvodci vám ukážeme přesně, jak vytvořit excel workbook c# pomocí Aspose.Cells, aplikovat podmíněné formátování, importovat datatable do Excelu a nakonec uložit sešit jako xlsx.  

Co z tohoto tutoriálu získáte, je připravená konzolová aplikace, která vytvoří barevný Excel soubor, plus jasné vysvětlení každého řádku, abyste jej mohli přizpůsobit svým projektům. Žádná externí dokumentace není potřeba; stačí zkopírovat, vložit a spustit.  

### Požadavky

- .NET 6+ (nebo .NET Framework 4.7.2+) nainstalovaný  
- Visual Studio 2022 nebo jakýkoli C# editor, který máte rádi  
- Aspose.Cells pro .NET (můžete si stáhnout bezplatnou zkušební NuGet balíček)  

Pokud máte vše připravené, pojďme na to.

## Vytvoření Excel sešitu v C# – Inicializace sešitu

První věc, kterou musíte udělat, je **create excel workbook c#** vytvořením instance třídy `Workbook`. Tento objekt představuje celý Excel soubor v paměti.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Proč je to důležité:** Třída `Workbook` abstrahuje formát souboru, takže se nemusíte starat o nízkoúrovňové XML nebo COM interop. Navíc vám poskytuje přístup ke stylům, tabulkám a smart markerům přímo z krabice.

## Aplikace podmíněného formátování

Nyní, když sešit existuje, **apply conditional formatting** pro zvýraznění řádků, kde množství přesahuje 100. Podmíněné formátování žije na listu, ne na buňce, což ho činí znovupoužitelným.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Tip:** Pokud potřebujete složitější pravidla (např. mezi dvěma hodnotami), stačí znovu zavolat `AddCondition` s `OperatorType.Between`.

## Zápis hlaviček a smart markerů

Než **import datatable to excel**, potřebujeme zástupné buňky — smart markery, které knihovna nahradí skutečnými daty. Přemýšlejte o nich jako o šablonových značkách.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Proč smart markery?** Umožňují vám udržet rozvržení Excelu oddělené od kódu. Navrhnete list jednou, pak jen předáte `DataTable` a knihovna udělá zbytek.

## Import DataTable do Excelu

Zde je jádro **import datatable to excel**. Vytvoříme `DataTable`, která odpovídá polím smart markerů, a předáme ji metodě `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Hraniční případ:** Pokud má vaše tabulka více sloupců, než potřebujete, stačí vynechat přebytečné sloupce ve smart markerech; budou ignorovány.

## Uložení sešitu jako XLSX

Nakonec **save workbook as xlsx** na disk. Metoda `Save` automaticky určí formát podle přípony souboru.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

To je celý program. Po jeho spuštění uvidíte soubor pojmenovaný `SmartMarkersConditional.xlsx` ve výstupní složce.

### Očekávaný výstup

| Produkt | Množství | Stav |
|---------|----------|------|
| Apple   | 120      | High |
| Banana  | 80       | Low  |
| Cherry  | 150      | High |

Řádky s **Quantity > 100** (Apple a Cherry) budou mít červený text na žlutém pozadí díky podmíněnému formátování, které jsme přidali dříve.

## Vytvoření Excel souboru programově – Kompletní zdrojový výpis

Níže je kompletní, připravený ke zkopírování zdrojový kód. Obsahuje všechny části, o kterých jsme mluvili, plus několik doplňujících komentářů pro přehlednost.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** Pokud potřebujete vytvořit více listů, stačí opakovat kroky 2‑6 na nové instanci `Worksheet`, získané pomocí `workbook.Worksheets.Add()`.

## Proč použít Aspose.Cells pro C# Excel automatizaci?

- **Výkon:** Pracuje zcela v paměti, bez COM interopu, takže je rychlý i u velkých datových sad.  
- **Bohaté funkce:** Podporuje smart markery, podmíněné formátování, grafy, kontingenční tabulky a další.  
- **Cross‑platform:** Funguje na Windows, Linuxu i macOS s .NET Core/5/6+.  

Pokud uvíznete na konkrétní funkci — např. přidání grafu nebo ochrana listu — stačí vyhledat “asp​ose.cells add chart c#” a najdete podobný vzor.

## Další kroky a související témata

- **Export do PDF:** Po tom, co **create excel workbook c#**, můžete okamžitě exportovat do PDF pomocí `workbook.Save("output.pdf")`.  
- **Čtení existujících Excel souborů:** Použijte `new Workbook("ExistingFile.xlsx")` pro úpravu šablony.  
- **Hromadný import:** Pro masivní data zvažte `ImportArray` nebo `ImportDataTable` s `ImportOptions` pro zvýšení rychlosti.  

Klidně experimentujte s různými podmíněnými pravidly, barvami nebo dokonce přidejte řádek součtu pomocí vzorců. Možnosti jsou neomezené, když **create excel file programmatically**.

---

*Připravený to vyzkoušet? Vezměte si kód, spusťte ho a otevřete vygenerovaný `SmartMarkersConditional.xlsx`. Pokud narazíte na problémy, zanechte komentář níže — šťastné kódování!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}