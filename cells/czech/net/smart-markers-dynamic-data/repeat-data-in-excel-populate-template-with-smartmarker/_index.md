---
category: general
date: 2026-02-21
description: Opakujte data v Excelu rychle pomocí SmartMarkeru — naučte se, jak naplnit
  šablonu Excelu a snadno opakovat řádky.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: cs
og_description: Opakujte data v Excelu pomocí SmartMarkeru. Naučte se, jak vyplnit
  šablonu Excelu, opakovat řádky a automatizovat své tabulky.
og_title: opakovat data v Excelu – Vyplnit šablonu pomocí SmartMarkeru
tags:
- excel
- csharp
- smartmarker
- automation
title: opakovat data v Excelu – vyplnit šablonu pomocí SmartMarkeru
url: /cs/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# opakování dat v Excelu – Vyplnění šablony pomocí SmartMarker

Už jste někdy potřebovali **opakovat data v Excelu**, ale nevedeli jste, jak se vyhnout ručnímu kopírování‑vkládání? Nejste v tom sami. V mnoha reportovacích scénářích máte seznam položek, který se musí automaticky rozšířit do řádků, a ruční provedení je recept na chyby.

Jde o to, že použití **SmartMarkerProcessor** z knihovny **GemBox.Spreadsheet** vám umožní **vyplnit Excel šablonu** jediným řádkem C# a nechat řádky opakovat pro každou položku ve vaší kolekci. V tomto průvodci projdeme přesné kroky, ukážeme kompletní kód a vysvětlíme, proč je každá část důležitá, abyste mohli sebejistě opakovat řádky v Excelu bez potíží.

## Co se naučíte

* Jak definovat datovou strukturu, která řídí operaci opakování.  
* Jak připojit `SmartMarkerProcessor` k sešitu, který obsahuje skrytou šablonu.  
* Jak se marker `${Repeat:Item}` automaticky rozšíří do více řádků.  
* Tipy pro řešení okrajových případů, jako jsou prázdné kolekce nebo vlastní formátování.  

Na konci tohoto tutoriálu budete schopni **vyplnit Excel z dat** způsobem, který škáluje, je snadno udržovatelný a funguje v jakémkoli .NET projektu.

---

## Požadavky

* .NET 6.0 nebo novější (kód používá moderní funkce C#).  
* NuGet balíček **GemBox.Spreadsheet** (volná verze funguje až pro 150 řádků).  
* Základní Excel šablona (`Template.xlsx`) se skrytým listem pojmenovaným `HiddenTemplate`.  
* Základní znalost objektů C# a LINQ je výhodou, ale není podmínkou.

---

## Krok 1 – Definice struktury dat pro opakování

Nejprve potřebujete zdroj dat, přes který může SmartMarker engine iterovat. Ve většině reálných aplikací pochází z databáze, API nebo CSV souboru. Pro přehlednost použijeme anonymní typ s jedinou vlastností `Item`, která obsahuje pole řetězců.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Proč je to důležité:** Marker `${Repeat:Item}` v Excel šabloně hledá vlastnost pojmenovanou `Item`. Pokud vlastnost přejmenujete, aktualizujte marker odpovídajícím způsobem. Toto úzké propojení zajišťuje, že šablona zůstane synchronizovaná s kódem, což usnadňuje **vyplnění Excel šablony** bez hádání názvů sloupců.

### Běžné varianty

* **Komplexní objekty:** Místo jednoduchého pole řetězců můžete předat seznam objektů (`new[] { new { Name = "A", Qty = 10 } }`). Marker opakuje řádky a můžete v listu odkazovat na `${Item.Name}` a `${Item.Qty}`.  
* **Prázdné kolekce:** Pokud je `Item` prázdný, SmartMarker jednoduše odstraní blok opakování a šablona zůstane nedotčena – ideální pro volitelné sekce.

---

## Krok 2 – Vytvoření SmartMarkerProcessor pro skrytý list šablony

Dále načtěte svůj sešit a vytvořte instanci `SmartMarkerProcessor`. Ukazujte na sešit, který obsahuje skrytý list šablony; SmartMarker zkopíruje tento list na viditelný a rozšíří markery opakování.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** Pokud máte v jednom souboru více šablon, můžete při volání `processor.Process` specifikovat název zdrojového listu. To pomáhá, když potřebujete **opakovat řádky v Excelu** pro různé části reportu.

### Řešení okrajových případů

* **Chybějící list šablony:** Zabalte načítání do `try/catch` a zaznamenejte jasnou chybu – tím předejdete tichým selháním, když je špatná cesta k souboru.  
* **Velké datové sady:** Pro tisíce řádků zvažte streamování výstupu do souboru (`processor.Save`) místo držení všeho v paměti.

---

## Krok 3 – Aplikace dat a rozšíření markeru `${Repeat:Item}`

Nyní přichází magický řádek, který skutečně opakuje řádky. Předávejte objekt vytvořený v Kroku 1 metodě `processor.Process`. SmartMarker najde každý marker `${Repeat:Item}`, duplikuje řádek pro každý prvek a nahradí zástupné symboly skutečnými hodnotami.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Co byste měli vidět

Po otevření `Result.xlsx` byl skrytý list šablony zkopírován na nový viditelný list (standardně pojmenovaný `Sheet1`). Řádek, který obsahoval `${Repeat:Item}`, se nyní objeví třikrát, přičemž buňky zobrazí **A**, **B** a **C**.

| Item |
|------|
| A    |
| B    |
| C    |

Pokud byste přidali další sloupce jako `${Item.Price}`, byly by automaticky vyplněny z datového zdroje.

---

## Jak opakovat řádky v Excelu bez SmartMarker (rychlé srovnání)

| Přístup                | Složitost kódu | Údržba | Výkon |
|------------------------|----------------|--------|-------|
| Manuální kopírování‑vkládání | Vysoká         | Nízká   | Špatný |
| VBA makro              | Střední        | Střední | Dobrý |
| **SmartMarkerProcessor**| Nízká          | Vysoká  | Výborný |

Jak vidíte, použití SmartMarker k **opakování dat v Excelu** poskytuje nejčistší oddělení mezi návrhem šablony a obchodní logikou. Navíc je jazykově neutrální – podobné koncepty existují v knihovnách pro Java, Python a JavaScript.

---

## Pokročilé tipy a časté úskalí

### 1. Formátování opakovaných řádků

SmartMarker kopíruje celý řádek – včetně stylů buněk, ohraničení a podmíněného formátování. Pokud potřebujete odlišný styl pro první nebo poslední řádek, přidejte extra markery jako `${If:Item.IsFirst}` a použijte podmíněné vzorce přímo v Excelu.

### 2. Práce s velkými datovými sadami

Při zpracování > 10 000 řádků vypněte automatické přepočítávání v Excelu před zpracováním:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Po uložení jej opět zapněte, aby výkon zůstal svižný.

### 3. Vyplňování Excelu z reálné databáze

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Pak v šabloně použijte `${Repeat:Order}` k výpisu každé objednávky. Tento vzor ukazuje, jak snadno lze **vyplnit Excel z dat** přímo z Entity Framework.

### 4. Použití více bloků opakování

Můžete mít několik markerů `${Repeat:...}` na stejném listu nebo na různých listech. SmartMarker je zpracuje sekvenčně, takže pořadí má význam jen tehdy, když jeden blok závisí na výstupu druhého.

---

## Kompletní spustitelný příklad

Níže je samostatná konzolová aplikace, kterou můžete vložit do Visual Studia a okamžitě spustit. Demonstruje všechny tři kroky plus uložení souboru.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Očekávaný výstup:** `Result.xlsx` obsahuje list, kde se řádek s `${Repeat:Item}` objeví třikrát a zobrazí A, B a C. Žádné ruční úpravy nejsou potřeba.

---

## Závěr

Nyní víte, jak **efektivně opakovat data v Excelu** pomocí SmartMarkerProcessor. Definováním jednoduchého datového objektu, načtením šablony sešitu a voláním `Process` můžete **vyplnit Excel šablonu**, **opakovat řádky v Excelu** a obecně **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}