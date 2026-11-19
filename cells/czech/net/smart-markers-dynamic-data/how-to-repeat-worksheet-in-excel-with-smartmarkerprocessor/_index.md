---
category: general
date: 2026-11-19
description: Jak opakovat list při naplňování Excelu daty z pole. Naučte se vytvořit
  více listů a naplnit list ze seznamu během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: cs
lastmod: 2026-11-19
og_description: Jak opakovat list pomocí SmartMarkerProcessor. Postupujte podle tohoto
  návodu k naplnění Excelu daty z pole, vytvoření více listů a naplnění listu ze seznamu.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Jak duplikovat list v Excelu – krok za krokem
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Jak opakovat list v Excelu pomocí SmartMarkerProcessor
url: /cs/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opakovat list v Excelu pomocí SmartMarkerProcessor

Pokud potřebujete **how to repeat worksheet** při generování Excel reportů, tento průvodce vám ukáže kompletní, spustitelné řešení. Na konci tutoriálu budete schopni **populate Excel with array** data, **generate multiple worksheets** a **populate worksheet from list** pomocí knihovny SmartMarkerProcessor.

Opakování listu je běžná požadavek, když každé oddělení, region nebo časové období potřebuje vlastní kartu. Níže uvedený příklad demonstruje přesné kroky, vysvětluje, proč je každé nastavení důležité, a pokrývá okrajové případy jako prázdné seznamy nebo vlastní pojmenování.

## Požadavky

- .NET 6.0 nebo novější nainstalovaný
- Odkaz na NuGet balíček **GroupDocs.Viewer** (nebo ekvivalent), který obsahuje `SmartMarkerProcessor`
- Excel šablona se sešitem (`.xlsx`) s markerem jako `${repeat:Dept}` umístěným v řádku, který chcete opakovat
- Základní znalost C# a LINQ (volitelné, ale užitečné)

Žádné další knihovny třetích stran nejsou vyžadovány.

## Krok 1: Vytvořte instanci SmartMarkerProcessor

Procesor orchestruje nahrazování markerů a duplikaci listů. Vytvoření instance bez argumentů používá výchozí nastavení.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Vytvoření procesoru brzy vám umožní nakonfigurovat globální nastavení před aplikací jakýchkoli dat. Toto je základ pro **how to repeat worksheet** správně.

## Krok 2: Povolit opakování listu

Ve výchozím nastavení procesor nahrazuje markery pouze na aktuálním listu. Nastavení `RepeatWorksheet` na `true` říká enginu, aby klonoval celý list pro každou položku v datové kolekci.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Povolení této volby je klíčem k **generate multiple worksheets** — procesor vytvoří novou kartu pro každý prvek v poli `Dept` a zachová původní formátování.

## Krok 3: Připravte zdroj dat jako pole nebo seznam

SmartMarkerProcessor pracuje s libovolným enumerable, ale použití pole dává jasný záměr, když chcete **populate worksheet from list**. Zde vytváříme anonymní objekt, který obsahuje vlastnost `Dept` držící pole řetězců.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Pokud již máte `List<string>`, můžete jej předat přímo; procesor s ním zachází stejně. Důležitá část je, aby název vlastnosti (`Dept`) odpovídal markeru `${repeat:Dept}` v šabloně.

## Krok 4: Načtěte šablonu listu

Předpokládejme, že máte `ExcelPackage` (z EPPlus) nebo objekt `Workbook`, načtěte list, který chcete opakovat. Proměnná `ws` představuje tento list.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Pokud dáváte přednost jiné knihovně (např. ClosedXML), platí stejný princip: získat objekt listu, který implementuje požadované rozhraní.

## Krok 5: Zpracujte list s daty

Nyní aplikujte data na šablonu. Procesor klonuje list pro každé oddělení, nahradí marker `${repeat:Dept}` skutečným názvem oddělení a zbytek listu ponechá nedotčený.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Po dokončení `Process` se `ws` stane prvním z několika listů — jedním pro každé oddělení. Název původního listu je zachován, zatímco duplikáty získají přírůstkové přípony (např. „Sheet1 (1)“, „Sheet1 (2)“). Můžete je přejmenovat později, pokud potřebujete vlastní pojmenování.

### Očekávaný výstup

Když otevřete výsledný sešit, měli byste vidět:

- **Sheet1** – původní šablona (často prázdná nebo použita jako hlavní)
- **Sheet1 (1)** – vyplněno „HR“
- **Sheet1 (2)** – vyplněno „IT“
- **Sheet1 (3)** – vyplněno „Finance“

Každý list obsahuje stejné rozložení, ale s názvem oddělení dosazeným tam, kde se objevil `${repeat:Dept}`.

## Řešení okrajových případů

### Prázdná nebo null pole

Pokud je `Dept` null nebo prázdné, procesor nevytvoří žádné další listy. Aby se předešlo zcela prázdnému sešitu, můžete přidat ochranu:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Vlastní názvy listů

Výchozí schéma pojmenování nemusí vyhovovat každému požadavku na reportování. Po zpracování přejmenujte každý list pomocí smyčky:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Vyplnění dalších sloupců

Pokud potřebujete **populate excel with array** hodnoty nad rámec jednoho markeru, rozšiřte datový objekt:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Poté upravte markery v šabloně na `${repeat:Dept.Name}` a `${repeat:Dept.Headcount}`. Procesor opakuje řádek pro každé oddělení a vyplní oba sloupce.

## Kompletní funkční příklad

Níže je samostatná konzolová aplikace, která demonstruje celý tok od načtení šablony po uložení finálního sešitu.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Vysvětlení klíčových částí**

- **Processor creation** – vytváří engine, který bude interpretovat markery.
- **RepeatWorksheet option** – aktivuje hlavní funkci, která odpovídá na *how to repeat worksheet*.
- **Data source** – používá pole (`new[]`) k naplnění **populate excel with array**.
- **Template loading** – ukazuje běžný způsob získání objektu listu.
- **Processing** – provádí duplikaci a vložení dat v jednom volání.
- **Renaming** – ukazuje, jak převést generické názvy “(1)”, “(2)” na smysluplné titulky, typický požadavek po **generate multiple worksheets**.

Spuštěním tohoto programu se vytvoří `Result.xlsx` se třemi listy specifickými pro oddělení, každý vyplněný z pole.

## Časté úskalí a tipy pro profesionály

- **Marker spelling** – marker musí přesně odpovídat názvu vlastnosti (`${repeat:Dept}`). překlep zabraňuje opakování.
- **Worksheet index** – po zpracování zůstává původní list na indexu 0; generované listy následují sekvenčně. Špatné indexování může vést k přejmenování špatné karty.
- **Large data sets** – generování stovek listů může dramaticky zvýšit velikost souboru. Zvažte rozdělení reportů nebo použití jednoho listu se seskupenými sekcemi, pokud se objeví problémy s výkonem.
- **Thread safety** – `SmartMarkerProcessor` není thread‑safe. Vytvořte samostatnou instanci pro každý vlákno, pokud zpracováváte více sešitů paralelně.

## Závěr

Nyní víte, jak **how to repeat worksheet** v Excelu pomocí SmartMarkerProcessor, jak **populate excel with array** data, jak **generate multiple worksheets**, a jak **populate worksheet from list** efektivně. Kompletní příklad spojuje všechny koncepty dohromady a volitelný krok přejmenování vám umožní vytvořit čisté, uživatelsky přívětivé názvy karet.

Dále můžete prozkoumat:

- Použití **populate worksheet from list** s komplexními objekty (vnořené kolekce)
- Aplikace podmíněného formátování po duplikaci listu
- Export vygenerovaného sešitu do PDF nebo CSV pro následnou konzumaci

Neváhejte přizpůsobit kód vašim vlastním scénářům reportování a užívejte si automatizaci Excel sešitů s jistotou!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak opakovat listy – Kompletní průvodce pro automatizaci Excelu](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Vytvořit list pro položku – Jak opakovat list v C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Jak rozšířit pole v Excelu a naplnit šablonu](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}