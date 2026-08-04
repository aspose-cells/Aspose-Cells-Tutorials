---
category: general
date: 2026-02-09
description: Vytvořte nový sešit Excel a naučte se snadno kopírovat kontingenční tabulky.
  Tento průvodce ukazuje, jak duplikovat kontingenční tabulku a uložit sešit jako
  nový.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: cs
og_description: Vytvořte nový sešit Excel v C# a okamžitě zkopírujte kontingenční
  tabulku. Naučte se, jak duplikovat kontingenční tabulku a uložit sešit jako nový
  s kompletním ukázkovým kódem.
og_title: Vytvořit nový sešit Excel – krok po kroku kopírování kontingenční tabulky
tags:
- excel
- csharp
- aspose.cells
- automation
title: Vytvořit nový sešit Excel – kopírovat a duplikovat kontingenční tabulku
url: /cs/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit nový sešit Excel – Kopírování a duplikace kontingenční tabulky

Už jste někdy potřebovali **create new Excel workbook**, který přenese složitou kontingenční tabulku z existujícího souboru? Nejste jediní — mnoho vývojářů narazí na tento problém při automatizaci reportovacích pipeline. Dobrou zprávou je, že s několika řádky C# a knihovnou Aspose.Cells můžete **how to copy pivot** rychle, **duplicate pivot table**, a **save workbook as new** bez ručního otevírání Excelu.

V tomto průvodci projdeme celý proces, od načtení zdrojového sešitu až po uložení duplikované verze. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu. Žádné zbytečnosti, jen praktické řešení, které můžete vyzkoušet ještě dnes.

## Co tento tutoriál pokrývá

* **Prerequisites** – .NET 6+ (nebo .NET Framework 4.6+), Visual Studio a NuGet balíček Aspose.Cells pro .NET.
* Krok‑za‑krokem kód, který **creates new Excel workbook**, kopíruje kontingenční tabulku a zapíše výsledek na disk.
* Vysvětlení **why** každého řádku, ne jen **what** dělá.
* Tipy pro řešení okrajových případů, jako jsou skryté listy nebo velké datové rozsahy.
* Rychlý pohled na **how to copy worksheet**, pokud někdy potřebujete celý list místo jen kontingenční tabulky.

Připravení? Ponořme se.

![ilustrace vytvoření nového sešitu Excel](image.png "Diagram ukazující zdrojový sešit, kopii kontingenční tabulky a cílový sešit")

## Krok 1: Nastavení projektu a instalace Aspose.Cells

Než budeme moci **create new Excel workbook**, potřebujeme projekt, který odkazuje na správnou knihovnu.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Proč je to důležité:* Aspose.Cells funguje kompletně v paměti, takže nikdy nemusíte spouštět Excel na serveru. Také zachovává informace o cache kontingenční tabulky, což je nezbytné pro pravou **duplicate pivot table**.

> **Pro tip:** Pokud cílíte na .NET Core, ujistěte se, že identifikátor runtime (RID) vašeho projektu odpovídá platformě, na kterou nasazujete; jinak můžete narazit na chyby při načítání nativních knihoven.

## Krok 2: Načtení zdrojového sešitu, který obsahuje kontingenční tabulku

Nyní **how to copy pivot** z existujícího souboru. Zdrojový sešit může být kdekoliv na disku, ve streamu nebo dokonce v poli bajtů.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Proč vybíráme rozsah:* Kontingenční tabulka žije v běžném rozsahu buněk, ale má také skryté data cache připojená k listu. Kopírováním rozsahu **včetně kontingenční tabulky** Aspose.Cells zajistí, že cache s ním cestuje, což vám poskytne funkční **duplicate pivot table** v cílovém souboru.

## Krok 3: Vytvoření nového sešitu Excel pro příjem zkopírovaných dat

Zde skutečně **create new Excel workbook**, který bude obsahovat duplikovanou kontingenční tabulku.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Proč nový sešit?** Začátek s čistým listem zaručuje, že žádné zbylé formátování nebo skryté objekty nebudou rušit kopírovanou kontingenční tabulku. Také to dělá výsledný soubor menší, což je užitečné pro automatické přílohy e‑mailů.

## Krok 4: Kopírování rozsahu kontingenční tabulky do nového sešitu

Nyní provedeme skutečnou operaci **how to copy pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Ten jediný řádek provádí těžkou práci:

* Hodnoty buněk, vzorce a formátování jsou přeneseny.
* Cache kontingenční tabulky je duplikována, takže nová kontingenční tabulka zůstává plně funkční.
* Jakékoli relativní odkazy uvnitř kontingenční tabulky se automaticky přizpůsobí novému umístění.

### Řešení okrajových případů

* **Skryté listy:** Pokud je zdrojový list skrytý, kontingenční tabulka se stále dobře zkopíruje, ale možná budete chtít odkrýt cílový list pro viditelnost uživatele:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Velké datové sady:** Pro rozsahy větší než několik tisíc řádků zvažte použití `CopyTo` s `CopyOptions` pro streamování operace a snížení zatížení paměti.

## Krok 5: Uložení cílového sešitu jako nový soubor

Nakonec **save workbook as new** a ověříme výsledek.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Pokud otevřete `copied.xlsx`, uvidíte přesnou repliku původní kontingenční tabulky, připravenou k dalším úpravám nebo distribuci.

### Volitelné: Jak kopírovat list místo jen kontingenční tabulky

Někdy chcete celý list, ne jen kontingenční tabulku. Stejné API to dělá triviální:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Toto uspokojuje dotaz **how to copy worksheet** a může být užitečné, když potřebujete zachovat další nastavení na úrovni listu.

## Kompletní funkční příklad

Sestavením všeho dohromady zde máte samostatnou konzolovou aplikaci, kterou můžete zkompilovat a spustit:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Očekávaný výstup:** Konzole vypíše zprávu o úspěchu a `copied.xlsx` se objeví v `C:\Reports` s funkční kontingenční tabulkou identickou s tou v `source.xlsx`.

## Časté otázky a úskalí

* **Rozbijí se vzorce uvnitř kontingenční tabulky?** Ne — protože cache kontingenční tabulky cestuje s rozsahem, všechny vypočítané pole zůstávají nedotčeny.
* **Co když zdrojová kontingenční tabulka používá externí datová spojení?** Tato spojení *nejsou* zkopírována. Budete je muset znovu vytvořit v cílovém sešitu nebo nejprve převést kontingenční tabulku na statickou tabulku.
* **Mohu kopírovat více kontingenčních tabulek najednou?** Ano — stačí definovat větší rozsah, který zahrnuje všechny kontingenční tabulky, nebo projít každým objektem `PivotTable` v `sourceSheet.PivotTables` a kopírovat je jednotlivě.
* **Musím uvolňovat objekty `Workbook`?** Implementují `IDisposable`, takže jejich zabalení do `using` bloků je dobrý zvyk, zejména ve službách s vysokou propustností.

## Závěr

Nyní víte **how to create new Excel workbook**, jak kopírovat kontingenční tabulku, **duplicate pivot table** a **save workbook as new** pomocí C# a Aspose.Cells. Kroky jsou jednoduché: načíst, vytvořit, kopírovat a uložit. S volitelným úryvkem **how to copy worksheet** máte také záložní řešení pro duplikaci celého listu.

Další kroky, které můžete prozkoumat:

* Přidání vlastního formátování do duplikované kontingenční tabulky.
* Programové obnovení cache kontingenční tabulky po změně dat.
* Export sešitu do PDF nebo CSV pro následné systémy.

Vyzkoušejte to, upravte rozsah a nechte automatizaci odstranit těžkou práci z vašich reportovacích workflow. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}