---
category: general
date: 2026-03-25
description: Naučte se, jak v Excelu opakovat položky pomocí C#. Tento průvodce ukazuje,
  jak dynamicky generovat řádky v Excelu a naplnit Excel šablonu v C# pro libovolnou
  kolekci.
draft: false
keywords:
- how to repeat items in excel
- generate excel rows dynamically
- populate excel template c#
language: cs
og_description: Jak opakovat položky v Excelu pomocí C#? Postupujte podle tohoto kompletního
  tutoriálu, který vám umožní dynamicky generovat řádky v Excelu a snadno naplnit
  Excel šablonu pomocí C#.
og_title: Jak opakovat položky v Excelu – krok za krokem průvodce C#
tags:
- C#
- Excel automation
- Aspose.Cells
title: Jak opakovat položky v Excelu – Dynamické generování řádků pomocí C#
url: /cs/net/row-and-column-management/how-to-repeat-items-in-excel-dynamic-row-generation-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opakovat položky v Excelu – Dynamické generování řádků pomocí C#

Už jste se někdy zamysleli **jak opakovat položky v Excelu** bez ručního kopírování řádků? Možná máte seznam objednávek, každou s několika položkami, a potřebujete přehledný list, který se automaticky rozšiřuje. V tomto tutoriálu uvidíte přesně to: budeme dynamicky generovat řádky v Excelu a **naplnit šablonu Excelu C#** pomocí výkonné funkce Smart Marker knihovny Aspose.Cells.

Provedeme vás reálným scénářem, vytvoříme malý datový model a uvidíme, jak knihovna převádí naši šablonu na plně vyplněný list. Na konci budete schopni opakovat položky v Excelu pro jakoukoli kolekci, ať už jde o jednu objednávku nebo obrovský katalog. Žádné zbytečnosti – jen funkční řešení, které můžete zkopírovat a vložit do svého projektu.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+)
- Visual Studio 2022 (nebo jakékoli IDE dle vašeho výběru)
- **Aspose.Cells for .NET** NuGet balíček (`Install-Package Aspose.Cells`)
- Základní pochopení anonymních typů v C#

Pokud vám něco chybí, stačí přidat NuGet balíček a můžete začít. Knihovna je plně spravovaná, takže není potřeba žádná COM interop nebo instalace Office.

---

## Krok 1: Definujte šablonu Smart Marker – jádro „opakování položek v Excelu“

Prvním, co potřebujeme, je buňka šablony, která říká Aspose.Cells, jak iterovat přes naši kolekci. Smart Markery používají jednoduchou syntaxi zástupných znaků, která je umístěna přímo v listu.

```csharp
// Put the template into cell A1
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +          // Start repeating the Orders collection
    "   ${Item:Repeat}\n" +        // For each Order, repeat the Item collection
    "      ${Item.Name}\n" +       // Insert the Name of each Item
    "   ${/Item}\n" +              // End Item repeat block
    "${/Orders}");                 // End Orders repeat block
```

**Proč je to důležité:** Značka `${Orders:Repeat}` říká procesoru, aby prošel pole `Orders`. Uvnitř tohoto cyklu spustíme další opakovací blok pro `Item`. Při každém průchodu vnitřního cyklu se `${Item.Name}` nahradí skutečným názvem, jako je „Apple“ nebo „Banana“. Když procesor skončí, šablona se rozšíří na tolik řádků, kolik je potřeba – přesně to, co potřebujete k **generování řádků v Excelu dynamicky**.

> **Tip:** Zachovejte odsazení uvnitř řetězce; překládá se to na správné zarovnání řádků v konečném listu.

## Krok 2: Vytvořte odpovídající datový model – „populate excel template c#“ zjednodušeně

Naše šablona očekává objekt s vlastností `Orders`, přičemž každá objednávka obsahuje pole `Item`. Vytvoříme anonymní objekt, který tuto strukturu odráží:

```csharp
// Create a simple data model that matches the template
var dataModel = new
{
    Orders = new[]
    {
        new
        {
            Item = new[]
            {
                new { Name = "Apple" },
                new { Name = "Banana" }
            }
        },
        // You can add more orders here – the template will repeat automatically
        new
        {
            Item = new[]
            {
                new { Name = "Orange" },
                new { Name = "Grape" },
                new { Name = "Mango" }
            }
        }
    }
};
```

**Proč je to důležité:** Struktura anonymního objektu musí přesně odpovídat značkám. Pokud chybí nějaká vlastnost nebo ji pojmenujete jinak, engine Smart Marker ji tiše přeskočí a zůstane prázdný řádek. To je častá chyba při prvním pokusu **populate excel template c#**.

## Krok 3: Spusťte procesor Smart Marker – motor, který opakuje položky

Nyní, když máme šablonu a datový model, předáme je obě Aspose.Cells. Procesor prochází list, rozšiřuje opakovací bloky a zapisuje hodnoty.

```csharp
// Process the template with the data model
worksheet.SmartMarkerProcessor.Process(dataModel);
```

To je doslova veškerý kód, který potřebujete k **opakování položek v Excelu**. Po dokončení volání bude list obsahovat:

| A (generated) |
|---------------|
| Apple         |
| Banana        |
| Orange        |
| Grape         |
| Mango         |

Každá položka se objeví na vlastním řádku, bez ohledu na to, kolik objednávek nebo položek jste do modelu přidali.

## Kompletní funkční příklad – od začátku do konce

Níže je kompletní, připravená ke spuštění konzolová aplikace, která demonstruje celý tok. Zkopírujte ji do nového C# projektu, přidejte NuGet balíček Aspose.Cells a spusťte. Soubor `Output.xlsx` se objeví ve složce bin.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // 2️⃣ Define the Smart Marker template (Step 1)
            worksheet.Cells["A1"].PutValue(
                "${Orders:Repeat}\n" +
                "   ${Item:Repeat}\n" +
                "      ${Item.Name}\n" +
                "   ${/Item}\n" +
                "${/Orders}");

            // 3️⃣ Build the data model (Step 2)
            var dataModel = new
            {
                Orders = new[]
                {
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Apple" },
                            new { Name = "Banana" }
                        }
                    },
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Orange" },
                            new { Name = "Grape" },
                            new { Name = "Mango" }
                        }
                    }
                }
            };

            // 4️⃣ Process the template (Step 3)
            worksheet.SmartMarkerProcessor.Process(dataModel);

            // 5️⃣ Save the result
            workbook.Save("Output.xlsx");
            Console.WriteLine("Excel file generated! Open Output.xlsx to see the repeated items.");
        }
    }
}
```

**Očekávaný výstup:** Otevřete `Output.xlsx` a uvidíte sloupec s pěti názvy ovoce, každý na vlastním řádku. Žádné ruční kopírování není potřeba.

### Co když je moje kolekce prázdná?

Pokud je `Orders` nebo jakékoli pole `Item` prázdné, engine Smart Marker jednoduše přeskočí blok a nezanechá žádné řádky. To je užitečné, když potřebujete **generovat řádky v Excelu dynamicky** na základě volitelných dat – nic navíc se neobjeví.

### Zpracování velkých datových sad

Pro tisíce řádků je procesor stále rychlý, protože pracuje v paměti a zapisuje přímo do sešitu. Přesto můžete chtít:

- Vypnout výpočty (`workbook.CalculateFormula = false`) před zpracováním.
- Použít `MemoryStream`, pokud potřebujete vrátit soubor přes webové API, aniž byste se dotkli souborového systému.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Oprava |
|-------|----------------|-----|
| Značky se neexpandují | Špatně napsané jméno vlastnosti nebo nesprávná velikost písmen | Zajistěte, aby názvy vlastností anonymního objektu přesně odpovídaly značkám (`Orders`, `Item`, `Name`). |
| Objevují se prázdné řádky | Přebytečné znaky nového řádku uvnitř řetězce šablony | Ořízněte koncové `\n` nebo udržujte šablonu stručnou. |
| Procesor vyhodí `NullReferenceException` | Datový model obsahuje `null` pro kolekci | Ochráníte před `null` inicializací prázdných polí (`new object[0]`). |
| Výstupní soubor je poškozený | Sešit není správně uložen (např. použitím špatného formátu) | Použijte `workbook.Save("file.xlsx")` s příponou `.xlsx`. |

## Rozšíření šablony – víc než jen názvy

Smart Markery podporují jakoukoli vlastnost, vzorce a dokonce i podmíněné bloky. Například pro přidání sloupce s cenou:

```csharp
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +
    "   ${Item:Repeat}\n" +
    "      ${Item.Name}\t${Item.Price}\n" +
    "   ${/Item}\n" +
    "${/Orders}");
```

A aktualizujte datový model:

```csharp
new { Name = "Apple", Price = 0.99M },
new { Name = "Banana", Price = 0.59M }
```

Výsledek budou dva sloupce – jeden pro název, druhý pro cenu – opět generované **dynamicky**.

## Závěr

Nyní máte kompletní, samostatné řešení pro **jak opakovat položky v Excelu** pomocí C#. Definováním šablony Smart Marker, vytvořením odpovídajícího datového modelu a voláním `SmartMarkerProcessor.Process` můžete **generovat řádky v Excelu dynamicky** pro jakoukoli kolekci a snadno **populate excel template c#** projekty.

Co dál? Zkuste přidat součty, podmíněné formátování nebo exportovat stejná data do CSV. Stejný vzor funguje s vnořenými kolekcemi, seskupováním i s vlastními objekty – tak neváhejte experimentovat.

Pokud se vám tento návod líbil, dejte mu hvězdičku na GitHubu, sdílejte ho s kolegy nebo zanechte komentář níže. Šťastné programování a užívejte si sílu automatizovaného generování Excelu! 

![Snímek obrazovky vygenerovaných řádků v Excelu ukazující, jak opakovat položky v Excelu](/images/repeat-items-excel.png "jak opakovat položky v Excelu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}