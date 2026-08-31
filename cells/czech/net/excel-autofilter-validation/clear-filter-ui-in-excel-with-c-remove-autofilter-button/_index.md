---
category: general
date: 2026-02-09
description: Vymažte uživatelské rozhraní filtru v Excelu pomocí C# odstraněním tlačítka
  AutoFilter. Naučte se, jak skrýt tlačítko filtru, zobrazit řádek záhlaví a udržet
  své listy přehledné.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: cs
og_description: Vymazání UI filtru v Excelu pomocí C#. Tento návod ukazuje, jak skrýt
  tlačítko filtru, zobrazit řádek záhlaví a udržet listy čisté.
og_title: Vymazat UI filtru v Excelu pomocí C# – Odebrat tlačítko AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Vymazat UI filtru v Excelu pomocí C# – Odebrat tlačítko AutoFilter
url: /cs/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vymazání UI filtru v Excelu pomocí C# – Odstranění tlačítka AutoFilter

Už jste někdy potřebovali **vymazat UI filtru** v listu Excel, ale nebyli jste si jisti, která řádka kódu skutečně skryje tu malou rozbalovací šipku? Nejste v tom jediní. Tlačítko filtru může být otravné, když odesíláte zprávu koncovým uživatelům, kteří nikdy nemusí měnit zobrazení.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **odstraňuje tlačítko AutoFilter** z tabulky, zajistí, že řádek záhlaví zůstane viditelný, a dokonce se dotkne toho, jak *trvale skrýt tlačítko filtru*. Na konci budete přesně vědět **jak odstranit AutoFilter** v C# a proč je každý krok důležitý.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.7.2+) – funguje jakékoli moderní runtime.
- Balíček **EPPlus** z NuGet (verze 6.x nebo novější) – poskytuje nám `ExcelWorksheet`, `ExcelTable` atd.
- Jednoduchý soubor Excel s tabulkou pojmenovanou **SalesTable** (klidně si ji vytvořte během několika kliknutí).

To je vše. Žádný COM interop, žádné extra DLL, jen pár `using` direktiv a několik řádků kódu.

## Vymazání UI filtru: Odstranění tlačítka AutoFilter

Jádro řešení spočívá ve třech malých příkazech. Rozložme je, abyste pochopili *proč* jsou potřeba, ne jen *co* dělají.

### Krok 1 – Získání reference na tabulku

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Proč je to důležité: EPPlus pracuje s **tabulkami** (`ExcelTable`), ne s čistými oblastmi. Získáním objektu tabulky získáme přístup k vlastnosti `AutoFilter`, která řídí UI prvek, který vidíte na listu. Pokud se pokusíte manipulovat přímo s listem, ovlivníte jen hodnoty, ne tlačítko filtru.

### Krok 2 – Odstranění řádku tlačítka AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Nastavením `AutoFilter` na `null` řeknete EPPlus, aby smazal podkladový řádek filtru. Toto je operace *vymazání UI filtru*, kterou většina vývojářů hledá, když se ptá „**jak odstranit autofilter**“. Jedná se o čistý jednorázový přístup, který funguje v jakékoli verzi Excelu, kterou EPPlus podporuje.

### Krok 3 – Zachování viditelnosti řádku záhlaví

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Když odstraníte UI filtru, Excel může někdy skrýt řádek záhlaví, pokud je příznak `ShowHeader` tabulky nastaven na false. Explicitním nastavením na `true` zajistíme, že názvy sloupců zůstanou na obrazovce – jemný, ale důležitý detail pro vyladěnou finální zprávu.

### Kompletní, spustitelný příklad

Níže je minimální konzolová aplikace, která otevře existující sešit, provede tři kroky a výsledek uloží. Zkopírujte‑vložit, stiskněte **F5** a sledujte, jak tlačítko filtru zmizí.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Očekávaný výsledek:** Otevřete *SalesReport_NoFilter.xlsx* – šipky filtru jsou pryč, ale záhlaví sloupců zůstává. Už žádný „klik‑na‑filtr“ UI nepořádek.

> **Tip:** Pokud máte **více tabulek** a chcete skrýt tlačítko filtru pro všechny, projděte `worksheet.Tables` a použijte stejné tři řádky uvnitř smyčky.

## Jak odstranit AutoFilter v Excelu pomocí C# – podrobnější pohled

Možná se ptáte, „Co když už je v sešitu filtr aplikován? Vymaže nastavení `AutoFilter = null` také filtrované řádky?“ Odpověď je **ano**. EPPlus vymaže jak UI, tak podkladová kritéria filtru, takže data zůstávají v původním pořadí.

Pokud chcete pouze *skrýt* tlačítko, ale zachovat filtr aktivní, můžete místo toho nastavit vlastnost `AutoFilter` na **nový prázdný filtr**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Tato varianta je užitečná, když chcete *skrýt tlačítko filtru* pro vylepšený vzhled, ale stále umožnit pokročilým uživatelům přepínat filtry pomocí VBA nebo pásu karet.

### Okrajový případ: Tabulky bez řádku záhlaví

Některé starší zprávy používají obyčejné oblasti místo tabulek. V takovém případě EPPlus neukáže objekt `ExcelTable`, takže výše uvedený kód selže. Řešením je **převést oblast na tabulku** nejprve:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Nyní jste *odstranili UI ve stylu autofilter excel* i na oblasti, která původně neměla formální tabulku.

## Zobrazení řádku záhlaví po skrytí tlačítka filtru – proč je to důležité

Častá stížnost je, že po skrytí UI filtru řádek záhlaví někdy zmizí, zejména když byl sešit původně vytvořen s nastaveným „Skrýt záhlaví“. Explicitním nastavením `salesTable.ShowHeader = true;` tomu předcházíme.

Pokud někdy potřebujete **skrýt tlačítko filtru**, ale zachovat záhlaví skryté (třeba generujete surový výpis dat), jednoduše po vymazání filtru nastavte `salesTable.ShowHeader = false;`. Kód je symetrický, což usnadňuje přepínání na základě konfiguračního příznaku.

## Skrýt tlačítko filtru – praktické tipy a úskalí

- **Kompatibilita verzí:** EPPlus 6+ funguje pouze s soubory `.xlsx`. Pokud pracujete se starším formátem `.xls`, budete potřebovat jinou knihovnu (např. NPOI), protože API *clear filter UI* není k dispozici.
- **Výkon:** Načtení obrovského sešitu jen kvůli skrytí jednoho tlačítka může být pomalé. Zvažte použití `ExcelPackage.Load(stream, true)` pro otevření v režimu **read‑only**, aplikujte změnu a poté uložte.
- **Testování:** Vždy první výstupní soubor ověřte ručně. Automatizované UI testy mohou ověřit, že šipky filtru jsou skutečně pryč (`worksheet.Tables[0].AutoFilter == null`).
- **Licencování:** EPPlus přešel na dvojitou licenci ve verzi 5. Pro komerční projekty budete potřebovat placenou licenci nebo přejít na alternativní knihovnu.

## Kompletní zdrojový soubor pro kopírování‑vkládání

Níže je přesný soubor, který můžete vložit do nového konzolového projektu. Žádné skryté závislosti, vše je samostatné.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Spusťte `dotnet add package EPPlus --version 6.0.8` (nebo nejnovější) před sestavením a budete mít čistý list připravený k distribuci.

## Závěr

Právě jsme vám ukázali **jak odstranit AutoFilter** a **vymazat UI filtru** v sešitu Excel pomocí C#. Třířádkové jádro (`AutoFilter = null;`, `ShowHeader = true;`) provádí těžkou práci, zatímco okolní boilerplate dělá řešení

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}