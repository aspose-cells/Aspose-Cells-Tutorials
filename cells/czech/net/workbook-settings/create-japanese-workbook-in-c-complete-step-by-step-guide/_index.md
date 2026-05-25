---
category: general
date: 2026-03-25
description: Rychle vytvořte japonský pracovní sešit v C#. Naučte se nastavit CultureInfo
  na ja-JP a povolit japonský kalendář podle panování císařů pro přesné zpracování
  dat.
draft: false
keywords:
- create japanese workbook
- set cultureinfo ja-jp
language: cs
og_description: Vytvořte japonskou pracovní knihu v C# nastavením CultureInfo na ja-JP
  a použitím japonského kalendáře císařovské éry. Postupujte podle tohoto kompletního
  tutoriálu.
og_title: Vytvořte japonskou pracovní knihu v C# – kompletní průvodce
tags:
- C#
- Aspose.Cells
- Internationalization
title: Vytvořte japonský sešit v C# – kompletní průvodce krok za krokem
url: /cs/net/workbook-settings/create-japanese-workbook-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření japonského sešitu v C# – Kompletní krok‑za‑krokem průvodce

Už jste někdy potřebovali **vytvořit japonský sešit** v C#, ale nebyli jste si jisti, jaké nastavení upravit? Nejste v tom sami; práce s daty založenými na érách může připomínat bludiště, zejména když výchozí gregoriánský kalendář prostě nevyhovuje.  
Dobrá zpráva? Pár řádků kódu vám umožní nastavit `cultureinfo ja-jp`, aktivovat kalendář japonského císařského panování a nechat sešit mluvit jazykem japonského era systému.

V tomto tutoriálu projdeme celý proces – od přidání správného NuGet balíčku až po ověření, že převod dat skutečně funguje. Na konci budete mít spustitelný příklad, který **vytváří japonský sešit** připravený pro jakoukoli obchodní logiku, která se opírá o data v érách, například fiskální výkaznictví v Japonsku nebo analýzu historických dat.

## Co se naučíte

- Jak pomocí Aspose.Cells (nebo jakékoli kompatibilní knihovny) **vytvořit japonský sešit** objekty.  
- Proč musíte **nastavit cultureinfo ja-jp** před tím, než vložíte řetězce s érou do buněk.  
- Mechaniku **japonského kalendáře císařského panování** a jak mapuje notaci éry jako `R2/5/1` na standardní `DateTime`.  
- Časté úskalí (např. nesoulad řetězců s érou) a rychlé opravy.  
- Kompletní, připravený ke zkopírování kód, který můžete dnes vložit do konzolové aplikace.

### Požadavky

- .NET 6.0 nebo novější (kód funguje i s .NET Core 3.1+, ale novější runtime poskytují hezčí async API).  
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete).  
- NuGet balíček **Aspose.Cells** (bezplatná zkušební verze stačí pro demonstraci).  
- Základní znalost C# a konceptu nastavení kultury.

Pokud máte vše připravené, pojďme na to.

## Implementace krok‑za‑krokem

Níže rozdělujeme řešení do logických částí. Každý krok má vlastní nadpis, krátký úryvek kódu a vysvětlení **proč** je důležitý.

### Krok 1: Nainstalujte Aspose.Cells a přidejte jmenné prostory

Nejprve přidejte knihovnu pro tabulky do svého projektu.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
```

*Proč?* Aspose.Cells vám poskytuje třídu `Workbook`, která respektuje .NET `CultureInfo`. Bez ní byste museli psát vlastní logiku pro parsování éry – což je děravý kanál, kterým pravděpodobně nechcete procházet.

### Krok 2: Vytvořte novou instanci Workbook

Nyní skutečně **vytvoříme japonský sešit** objekt.

```csharp
// Step 2: Initialize a fresh workbook
Workbook workbook = new Workbook();
```

Tento řádek je prázdné plátno. Představte si `Workbook` jako soubor, který nakonec uložíte jako `.xlsx`. Začíná prázdný, ale můžete okamžitě začít konfigurovat jeho globální nastavení.

### Krok 3: Nastavte CultureInfo na japonštinu (ja‑JP)

Zde **nastavíme cultureinfo ja-jp**. Toto říká .NET runtime, aby interpretoval data, čísla a další lokálně specifické informace podle japonských konvencí.

```csharp
// Step 3: Apply Japanese culture to the workbook
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Pokud tento krok přeskočíte, engine bude zacházet s jakýmikoli řetězci dat, jako by byly v invariantní kultuře, což povede k `FormatException` při pozdějším zadání data v éře jako `R2/5/1`.

### Krok 4: Povolit kalendář japonského císařského panování

Japonský era systém není jen hezký formát; mění i základní výpočty kalendáře. Přepnutím typu kalendáře může sešit automaticky rozumět notaci éry.

```csharp
// Step 4: Use the Japanese Emperor Reign calendar for date handling
workbook.Settings.CalendarType = CalendarType.JapaneseEmperorReign;
```

V pozadí tato funkce mapuje éru „R“ (Reiwa) na rok 2019 + eraYear‑1, takže `R2/5/1` se stane 1. května 2020.

### Krok 5: Zapište řetězec data v éře do buňky

Vložme ukázkové japonské datum v éře do buňky **A1**.

```csharp
// Step 5: Write a Japanese era date string into cell A1
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].PutValue("R2/5/1"); // Reiwa 2, May 1
```

Možná se ptáte, proč používáme řetězec místo `DateTime`. Celý smysl je demonstrovat schopnost knihovny **převádět** řetězce s érou na základě nastavené kultury a kalendáře.

### Krok 6: Získejte hodnotu jako .NET DateTime

Nyní požádáme buňku, aby nám vrátila správný objekt `DateTime`.

```csharp
// Step 6: Convert the cell content to a .NET DateTime
DateTime date = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(date); // Expected output: 2020‑05‑01 00:00:00
```

Pokud je vše správně nastaveno, konzole vypíše `5/1/2020 12:00:00 AM` (nebo ISO‑8601 verzi podle lokálního nastavení konzole). To dokazuje, že pipeline **vytvoření japonského sešitu** správně interpretuje data v éře.

### Krok 7: Uložte sešit (volitelné, ale užitečné)

Většina reálných scénářů zahrnuje ukládání souboru.

```csharp
// Step 7: Persist the workbook to disk
workbook.Save("JapaneseWorkbook.xlsx");
Console.WriteLine("Workbook saved successfully.");
```

Ukládání není nutné pro test převodu dat, ale umožní vám otevřít soubor v Excelu a vidět formátované datum, čímž potvrdíte, že nastavení kultury cestuje se souborem.

## Úplný funkční příklad

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu. Obsahuje všechny výše uvedené kroky a pár obranných kontrol.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set the workbook's culture to Japanese (Japan)
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 3️⃣ Enable the Japanese Emperor Reign calendar
        workbook.Settings.CalendarType = CalendarType.JapaneseEmperorReign;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Write a Japanese era date string into cell A1
        string eraDate = "R2/5/1"; // Reiwa 2, May 1
        sheet.Cells["A1"].PutValue(eraDate);

        // 6️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime date;
        try
        {
            date = sheet.Cells["A1"].GetDateTime();
            Console.WriteLine($"Converted date: {date:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to convert era date: {ex.Message}");
            return;
        }

        // 7️⃣ Save the workbook (optional)
        workbook.Save("JapaneseWorkbook.xlsx");
        Console.WriteLine("Workbook saved as JapaneseWorkbook.xlsx");
    }
}
```

**Očekávaný výstup v konzoli**

```
Converted date: 2020-05-01
Workbook saved as JapaneseWorkbook.xlsx
```

Otevřete vygenerovaný soubor `JapaneseWorkbook.xlsx` v Excelu; buňka A1 zobrazí `2020/05/01` (nebo lokalizovaný formát) a zároveň zachová podkladová metadata vědomá éry.

## Okrajové případy a varianty

### Různé předpony éry

Japonský kalendář měl několik epoch: **M** (Meiji), **T** (Taisho), **S** (Showa), **H** (Heisei) a **R** (Reiwa). Stejný kód funguje pro kteroukoliv z nich, pokud řetězec éry odpovídá vzoru `EraYear/Month/Day`. Například:

```csharp
sheet.Cells["A2"].PutValue("H30/4/30"); // Heisei 30 = 2018‑04‑30
DateTime heiseiDate = sheet.Cells["A2"].GetDateTime(); // 2018‑04‑30
```

### Zpracování neplatných řetězců

Pokud řetězec neodpovídá požadovanému formátu (např. `X1/1/1`), `GetDateTime()` vyhodí `FormatException`. Rychlá ochrana může zvýšit robustnost:

```csharp
if (DateTime.TryParse(sheet.Cells["A1"].StringValue, out DateTime parsed))
{
    // use parsed
}
else
{
    Console.WriteLine("Invalid era format.");
}
```

### Práce bez Aspose.Cells

Pokud nemůžete použít komerční knihovnu, můžete stále **vytvořit japonský sešit**‑stylové soubory pomocí OpenXML a vlastního parseru éry, ale kód bude podstatně delší a ztratíte vestavěnou podporu kalendáře. Pro většinu vývojářů je přístup s Aspose nejjednodušší cestou.

## Praktické tipy (Pro‑Tipy)

- **Pro tip:** Nastavte `workbook.Settings.CultureInfo` **před** tím, než zapíšete jakékoli řetězce s daty. Změna později neprovádí retroaktivní reinterpretaci existujících buněk.  
- **Pozor:** Výchozí formát `DateTime` v `Console.WriteLine` respektuje aktuální kulturu vlákna. Pokud potřebujete stabilní ISO formát, použijte `date:yyyy-MM-dd`.  
- **Poznámka o výkonu:** Pokud zpracováváte tisíce řádků, nastavte kulturu a kalendář jednou na úrovni sešitu – nepřepínejte je opakovaně.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}