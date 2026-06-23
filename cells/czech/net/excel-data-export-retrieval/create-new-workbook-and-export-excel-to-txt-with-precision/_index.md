---
category: general
date: 2026-02-15
description: Vytvořte nový sešit a exportujte Excel do TXT při nastavení číselné přesnosti.
  Naučte se nastavit významné číslice a omezit počet významných číslic v C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: cs
og_description: Vytvořte nový sešit a exportujte Excel do TXT, nastavte významné číslice
  pro číselnou přesnost. Krok za krokem průvodce v C#.
og_title: Vytvořit nový sešit – Exportovat Excel do TXT s přesností
tags:
- C#
- Aspose.Cells
- Excel automation
title: Vytvořit nový sešit a exportovat Excel do TXT s přesností
url: /cs/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu – Export Excel do TXT s přesným číselným formátováním

Už jste se někdy zamýšleli, jak **vytvořit nový sešit** (new workbook) v C# a okamžitě jej uložit do prostého textového souboru? Nejste jediní. V mnoha scénářích datových pipeline potřebujeme **exportovat Excel do TXT**, přičemž čísla musí zůstat čitelná, což znamená omezit počet číslic za desetinnou čárkou.

V tomto tutoriálu projdeme celý proces: od vytvoření nového sešitu, přes nastavení exportu tak, aby **nastavil významné číslice** (tj. omezil počet významných číslic), až po zápis souboru na disk. Na konci budete mít připravený úryvek kódu, který respektuje vaše požadavky na **číselnou přesnost** – bez dalších knihoven, bez kouzel.

> **Pro tip:** Pokud už používáte Aspose.Cells, třídy uvedené níže jsou součástí této knihovny. Pokud pracujete na jiné platformě, koncepty jsou stále použitelné; stačí jen vyměnit volání API.

---

## Co budete potřebovat

- .NET 6+ (kód se kompiluje jak na .NET Core, tak na .NET Framework)  
- Aspose.Cells pro .NET (zdarma zkušební verze nebo licencovaná) – instalace přes NuGet: `dotnet add package Aspose.Cells`  
- Jakékoliv IDE, které máte rádi (Visual Studio, Rider, VS Code)  

To je vše. Žádné extra konfigurační soubory, žádné skryté kroky.

---

## Krok 1: Vytvoření nového sešitu

Prvním krokem je **vytvořit nový sešit**. Třídu `Workbook` si můžete představit jako prázdný Excel soubor čekající na listy, buňky a data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Proč je to důležité:** Začínáte-li s čistým sešitem, vyhnete se skrytému formátování, které by později mohlo narušit nastavení přesnosti.

---

## Krok 2: Nastavení Text Save Options – Definování významných číslic

Nyní řekneme Aspose.Cells, kolik **významných číslic** chceme při zápisu do souboru `.txt`. Třída `TxtSaveOptions` poskytuje vlastnost `SignificantDigits`, která přesně to umožňuje.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Vysvětlení:** `SignificantDigits = 5` znamená, že exportér zachová nejdůležitějších pět číslic libovolného čísla, bez ohledu na umístění desetinné čárky. Jedná se o praktický způsob, jak **nastavit číselnou přesnost** bez ručního formátování každé buňky.

---

## Krok 3: Uložení sešitu jako prostého textového souboru

S připraveným sešitem a nastavením můžeme konečně **exportovat Excel do txt**. Metoda `Save` přijímá cestu k souboru a objekt s nastavením, který jsme právě nakonfigurovali.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Spuštěním programu vznikne soubor, který vypadá takto:

```
12346
0.00012346
3.1416
```

Všimněte si, že každé číslo dodržuje pravidlo **omezení významných číslic**, které jsme nastavili dříve.

---

## Krok 4: Ověření výsledku (volitelné, ale doporučené)

Soubor `numbers.txt` můžete snadno otevřít v libovolném editoru, ale možná budete chtít automatizovat ověření, zejména v CI pipeline.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Pokud konzole zobrazí tři řádky výše, úspěšně jste **nastavili významné číslice** a export funguje podle očekávání.

---

## Časté problémy a jak se jim vyhnout

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| Čísla se zobrazují s příliš mnoha desetinnými místy | `SignificantDigits` zůstalo na výchozí hodnotě (0) | Explicitně nastavte `SignificantDigits` na požadovaný počet |
| Vytvořený soubor je prázdný | Sešit nebyl naplněn daty před uložením | Naplňte buňky **před** voláním `Save` |
| Cesta k souboru vrací `UnauthorizedAccessException` | Pokus o zápis do chráněné složky | Použijte složku, do které máte právo zapisovat (např. `C:\Temp` nebo `%USERPROFILE%\Documents`) |
| Přesnost se zdá být špatná u velmi malých čísel | Počet významných číslic zahrnuje úvodní nuly za desetinnou čárkou | Pamatujte, že „významné“ ignoruje úvodní nuly; 0.000123456 s 5 číslicemi se stane `0.00012346` |

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je kompletní, samostatný program. Vložte jej do nového konzolového projektu a spusťte **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Očekávaný výstup v konzoli**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

A soubor `numbers.txt` bude obsahovat tři řádky uvedené výše.

---

## Další kroky: Přesah základů

- **Export dalších formátů** – Aspose.Cells také podporuje CSV, HTML a PDF. Vyměňte `TxtSaveOptions` za `CsvSaveOptions` nebo `PdfSaveOptions` podle potřeby.  
- **Dynamická přesnost** – můžete počítat `SignificantDigits` za běhu na základě vstupu uživatele nebo konfiguračních souborů.  
- **Více listů** – iterujte přes `workbook.Worksheets` a exportujte každý do vlastního souboru `.txt`.  
- **Lokalizace** – ovládejte desetinný oddělovač (`.` vs `,`) pomocí `CultureInfo`, pokud potřebujete odpovídat regionálním nastavením.  

Všechny tyto rozšíření stále vycházejí z jádra, které jsme probrali: **vytvořit nový sešit**, nakonfigurovat export a **nastavit číselnou přesnost** podle požadavků na reportování.

---

## Shrnutí

Ukázali jsme si, jak vytvořit čerstvou instanci **create new workbook**, naplnit ji daty a demonstrovat, jak **exportovat Excel do TXT** při **nastavení významných číslic** pro omezení výstupní přesnosti. Kompletní příklad funguje hned po stažení a vysvětlení popisuje *proč* každého řádku, takže jej můžete snadno přizpůsobit vlastním projektům.

Nebojte se experimentovat – změňte hodnotu `SignificantDigits`, přidejte další listy nebo přepněte výstupní formát. Pokud narazíte na problém, podívejte se do dokumentace Aspose.Cells nebo zanechte komentář níže. Šťastné programování!

---

![Vytvoření nového sešitu – příklad](/images/create-new-workbook.png "Snímek obrazovky ukazující C# IDE s kódem pro vytvoření nového sešitu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}