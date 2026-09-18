---
category: general
date: 2026-02-23
description: Automaticky pojmenovávejte listy v Excelu a naučte se, jak generovat
  listy automaticky pomocí SmartMarkers. Krok za krokem průvodce v C# pro dynamické
  sešity.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: cs
og_description: Automaticky pojmenujte listy v Excelu okamžitě. Naučte se, jak generovat
  listy pomocí SmartMarkers v C# – kompletní, spustitelný příklad.
og_title: Automatické pojmenování listů Excel – Rychlý tutoriál C#
tags:
- C#
- Excel
- Aspose.Cells
title: Automatické pojmenování listů v Excelu – Jednoduchý způsob, jak generovat listy
url: /cs/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatické pojmenování listů Excel – Kompletní C# tutoriál

Už jste se někdy zamysleli, jak **automaticky pojmenovat listy Excel** bez psaní smyčky, která ručně přejmenuje každý list? Nejste v tom sami. V mnoha projektech reportování se počet listů během běhu zvyšuje a udržování názvů v pořádku se stává problémem. Dobrá zpráva? S **SmartMarkers** od Aspose.Cells můžete nechat knihovnu, aby se postarala o pojmenování za vás, a dokonce vám umožní **jak generovat listy** za běhu.

V tomto průvodci projdeme reálným scénářem: vytvoříme sešit, nakonfigurujeme možnosti SmartMarker tak, aby detailní listy byly automaticky pojmenovány *Detail*, *Detail1*, *Detail2*, …, a poté ověříme, že listy se zobrazují podle očekávání. Na konci budete mít samostatné, připravené k zkopírování řešení, které můžete přizpůsobit libovolnému projektu, který potřebuje dynamické vytváření listů.

---

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6.2+). Kód funguje na jakémkoli moderním runtime.
- **Aspose.Cells for .NET** NuGet balíček – `Install-Package Aspose.Cells`.
- Základní projekt C# (Console App, WinForms nebo ASP.NET – stejný kód funguje všude).
- Visual Studio, VS Code nebo vaše oblíbené IDE.

Žádné extra Excel interop, žádné COM, jen čistý spravovaný kód.

## Krok 1: Automatické pojmenování listů Excel pomocí SmartMarkers

První věc, kterou musíte udělat, je říct Aspose.Cells, jaký základní název chcete pro automaticky vytvořené detailní listy. To se provádí pomocí třídy `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Proč je to důležité:** Nastavením `DetailSheetNewName` předáte logiku pojmenování knihovně. Není potřeba psát `for` smyčku, která kontroluje existující názvy listů a zvyšuje čítač – API to udělá za vás a zajistí jedinečné názvy i když zdrojová data obsahují desítky řádků.

## Krok 2: Připravte zdrojová data

SmartMarkers fungují s libovolnou kolekcí `IEnumerable`, `DataTable` nebo i s obyčejným seznamem objektů. Pro tuto ukázku použijeme jednoduchý seznam objektů, které představují podrobnosti objednávek.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Proč je to důležité:** Zdrojová data určují, kolik detailních listů bude vygenerováno. Každý prvek v kolekci vytvoří nový list na základě SmartMarker šablony, kterou přidáme dále.

## Krok 3: Vložte SmartMarker šablonu do hlavního listu

SmartMarker šablona je jen buňka (nebo oblast), která obsahuje zástupné symboly. Když se spustí metoda `Apply`, zástupné symboly jsou nahrazeny skutečnými daty a pro každý řádek je vytvořen nový list.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Proč je to důležité:** Syntaxe `&=` říká SmartMarkers „vezmi hodnotu ze zdrojových dat“. Když se spustí `Apply`, Aspose.Cells zkopíruje tento řádek do nového listu pro každou položku v `orders` a automaticky pojmenuje list podle předtím nastavené možnosti.

## Krok 4: Použijte SmartMarker možnosti – zde se listy automaticky pojmenují

Nyní přichází okamžik, kdy knihovna udělá těžkou práci. Volání `Apply` načte šablonu, vytvoří detailní listy a pojmenuje je podle `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Proč je to důležité:** Metoda `Apply` nejen naplní data, ale také respektuje názevový vzor, který jsme zadali. Pokud otevřete *AutoNamedSheets.xlsx*, uvidíte:

- **Detail** – obsahuje první objednávku.
- **Detail1** – druhá objednávka.
- **Detail2** – třetí objednávka.

Žádné ruční přejmenovávání není potřeba.

## Krok 5: Ověřte výsledek – Jak správně generovat listy

Po spuštění programu otevřete vygenerovaný soubor. Měli byste vidět tři nové listy pojmenované přesně tak, jak je popsáno výše. To dokazuje, že jste úspěšně zvládli **jak automaticky generovat listy**.

> **Tip:** Pokud potřebujete vlastní příponu (např. „_Report“), stačí nastavit `DetailSheetNewName = "Detail_Report"` a knihovna přidá čísla za základní řetězec.

## Okrajové případy a časté otázky

### Co když základní název již existuje?

Aspose.Cells kontroluje existující názvy listů a přidává inkrementální číslo, dokud nenajde jedinečný název. Takže i když v sešitu již existuje list nazvaný *Detail*, další vygenerovaný list bude *Detail1*.

### Můžu ovlivnit pořadí generovaných listů?

Ano. Pořadí následuje sekvenci zdrojových dat. Pokud potřebujete konkrétní pořadí, setřiďte kolekci před předáním do `Apply`.

### Je možné generovat listy v jiném sešitu?

Rozhodně. Vytvořte druhou instanci `Workbook`, přidejte list s placeholderem a zavolejte `Apply` na tomto listu. Stejná logika pojmenování se použije.

### Jak to funguje s velkými datovými sadami?

SmartMarkers jsou optimalizovány pro výkon. I při tisících řádků knihovna efektivně streamuje data. Jen se ujistěte, že máte dostatek paměti pro konečnou velikost sešitu.

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, který můžete vložit do nového konzolového projektu. Nechybí žádná část – vše od `using` direktiv po finální volání `Save` je zahrnuto.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Spusťte program, otevřete vzniklý soubor *AutoNamedSheets.xlsx* a uvidíte funkci **automatického pojmenování listů Excel** v akci.

## Často kladené doplňující otázky

- **Mohu to použít s existujícím souborem šablony?**  
  Ano. Načtěte sešit pomocí `new Workbook("Template.xlsx")` a nasměrujte `master` na list, který obsahuje vaše SmartMarker placeholdery.

- **Co když potřebuji různé konvence pojmenování pro různé typy listů?**  
  Vytvořte několik objektů `SmartMarkerOptions`, každý s vlastní `DetailSheetNewName`, a použijte je na různé hlavní listy.

- **Existuje způsob, jak potlačit základní list (ten, který obsahuje šablonu)?**  
  Po `Apply` můžete jednoduše odstranit hlavní list: `workbook.Worksheets.RemoveAt(0);` – detailní listy zůstanou nedotčeny.

## Závěr

Nyní víte **jak automaticky pojmenovat listy Excel** pomocí Aspose.Cells SmartMarkers a také jste viděli osvědčený vzor pro **jak dynamicky generovat listy** v C#. Hlavní myšlenka je jednoduchá: nakonfigurujte `SmartMarkerOptions.DetailSheetNewName`, předáte kolekci a nechte knihovnu udělat zbytek. Tento přístup eliminuje boilerplate smyčky, zaručuje jedinečné názvy a škáluje se plynule.

Připraven na další krok? Zkuste vyměnit zdrojová data za `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}