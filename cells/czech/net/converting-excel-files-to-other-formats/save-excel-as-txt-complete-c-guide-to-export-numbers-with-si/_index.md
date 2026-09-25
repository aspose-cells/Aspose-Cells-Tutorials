---
category: general
date: 2026-02-21
description: Uložte Excel jako txt s přesnou kontrolou významných číslic. Exportujte
  Excel do txt v C# a snadno nastavte významné číslice.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: cs
og_description: Rychle uložte Excel jako txt. Naučte se, jak exportovat Excel do txt,
  nastavit významné číslice a řídit výstup textu pomocí C#.
og_title: Uložit Excel jako txt – Exportovat čísla s významnými číslicemi v C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Uložení Excelu jako txt – Kompletní C# průvodce exportem čísel se signifikantními
  číslicemi
url: /cs/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložit Excel jako txt – Kompletní C# průvodce exportem čísel s významnými číslicemi

Už jste někdy potřebovali **save Excel as txt**, ale obávali se, že čísla ztratí svou přesnost? Nejste v tom sami. Mnoho vývojářů narazí na problém, když se snaží exportovat Excel do txt a skončí buď s příliš mnoha desetinnými místy, nebo s zaokrouhleným nepořádkem.  

V tomto tutoriálu vám ukážeme jednoduchý způsob, jak **export Excel to txt** a zároveň **nastavit významné číslice**, aby výstup vypadal přesně tak, jak chcete. Na konci budete mít připravený C# úryvek, který uloží sešit jako text, exportuje čísla do txt a poskytne vám plnou kontrolu nad číselným formátem.

## Co se naučíte

- Jak vytvořit nový workbook a zapsat číselná data.
- Správný způsob, jak **set significant digits** pomocí `TxtSaveOptions`.
- Jak **save workbook as text** a ověřit výsledek.
- Zvládání okrajových případů (velká čísla, záporné hodnoty, problémy s locale).
- Rychlé tipy pro další úpravy výstupu (změna oddělovače, kódování).

### Předpoklady

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+).
- Balíček NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).
- Základní znalost syntaxe C# – není potřeba hluboká znalost Excel interop.

> **Pro tip:** Pokud používáte Visual Studio, povolte *nullable reference types* (`<Nullable>enable</Nullable>`), abyste včas zachytili potenciální null chyby.

---

## Krok 1: Inicializace Workbooku a zápis čísla

Nejprve potřebujeme objekt workbook. Představte si ho jako paměťovou reprezentaci souboru Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Proč je to důležité:**  
Vytvoření workbooku programově eliminuje režii COM interopu a `PutValue` automaticky detekuje datový typ, což zajišťuje, že buňka je považována za číslo – ne za řetězec.

---

## Krok 2: Konfigurace TxtSaveOptions pro řízení významných číslic

Třída `TxtSaveOptions` je místem, kde se děje magie. Nastavením `SignificantDigits` říkáte Aspose.Cells, kolik smysluplných číslic má být zachováno při zápisu souboru.  

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Proč byste to měli nastavit:**  
Když **export numbers to txt**, často potřebujete stručnou reprezentaci (např. pro reportovací systémy, které akceptují jen určitou přesnost). Vlastnost `SignificantDigits` zaručuje konzistentní zaokrouhlení bez ohledu na délku původního čísla.

---

## Krok 3: Uložení Workbooku jako textový soubor

Nyní zapíšeme workbook na disk pomocí právě definovaných možností.  

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Co uvidíte:**  
Otevřete `Numbers.txt` a získáte jeden řádek:

```
12350
```

Původní `12345.6789` byl zaokrouhlen na **čtyři významné číslice**, přesně podle požadavku.

---

## Krok 4: Ověření výstupu (volitelné, ale doporučené)

Automatizované testy jsou skvělý zvyk. Zde je rychlá kontrola, kterou můžete spustit hned po uložení:  

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Spuštěním tohoto bloku se vytiskne zelená fajfka, pokud vše souhlasí, což vám dodá jistotu, že operace **save excel as txt** proběhla podle očekávání.

---

## Běžné varianty a okrajové případy

### Export více buněk nebo oblastí

Pokud potřebujete **export excel to txt** pro celou oblast, stačí před uložením vyplnit více buněk:  

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Stejné `TxtSaveOptions` použije pravidlo 4‑ciferného zaokrouhlení na každou hodnotu, což vytvoří:  

```
12350
0.0001235
-98800
```

### Změna oddělovače

Některé downstream systémy očekávají hodnoty oddělené tabulátorem. Upravit oddělovač takto:  

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Nyní je každá buňka v řádku oddělena tabulátorem.

### Zpracování locale‑specifických desetinných oddělovačů

Pokud vaše publikum používá čárky jako desetinné oddělovače, nastavte kulturu:  

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Výstup bude respektovat locale a změní `12350` na `12 350` (mezera jako oddělovač tisíců ve francouzštině).

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Očekávaný obsah `Numbers.txt` (výchozí oddělovač, 4 významné číslice):**  

```
12350	0.0001235	-98800
```

Tabulátor (`\t`) se objeví, protože jsme v příkladu ponechali výchozí oddělovač (tabulátor); pokud dáváte přednost CSV, změňte jej na čárku.

## Závěr

Nyní přesně víte, **jak uložit Excel jako txt**, přičemž řídíte počet významných číslic. Kroky – vytvoření workbooku, nastavení `TxtSaveOptions.SignificantDigits` a uložení – jsou vše, co potřebujete k spolehlivému **export excel to txt**.

Odtud můžete:

- **Export numbers to txt** pro větší datové sady.
- Upravit oddělovače, kódování nebo nastavení kultury tak, aby odpovídaly libovolnému downstream systému.
- Kombinovat tento přístup s dalšími funkcemi Aspose.Cells (styly, vzorce) před exportem.

Vyzkoušejte to, upravte `SignificantDigits` na 2 nebo 6 a podívejte se, jak se výstup změní. Flexibilita **save workbook as text** z něj činí užitečný nástroj v jakémkoli datovém výměnném řetězci.

---

### Související témata, která můžete dále zkoumat

- **Export Excel to CSV** s vlastním pořadím sloupců.
- **Read txt files back into a workbook** (`Workbook.Load` s `LoadOptions`).
- **Batch processing** více listů a jejich konsolidace do jednoho txt souboru.
- **Performance tuning** pro rozsáhlé exporty (streamování vs. v‑paměti).

Neváhejte zanechat komentář, pokud narazíte na potíže, nebo se podělit, jak jste si export přizpůsobili pro své projekty. Šťastné programování!  

*Obrázek: Screenshot vygenerovaného souboru `Numbers.txt` zobrazujícího zaokrouhlené hodnoty.*  
*Alt text: „Soubor Numbers.txt zobrazující 12350, 0.0001235 a -98800 po uložení Excelu jako txt se 4 významnými číslicemi.“*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}