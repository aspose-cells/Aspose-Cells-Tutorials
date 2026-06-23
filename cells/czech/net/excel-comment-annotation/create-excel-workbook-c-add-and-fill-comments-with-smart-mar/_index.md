---
category: general
date: 2026-03-21
description: Vytvořte Excel sešit v C# a naučte se, jak přidat komentář do Excelu,
  automaticky vyplnit komentář pomocí Smart Markers. Krok za krokem průvodce pro vývojáře.
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: cs
og_description: Vytvořte Excel sešit v C# a rychle přidejte komentář do Excelu, poté
  vyplňte komentář pomocí Smart Markerů. Kompletní tutoriál s kódem.
og_title: Vytvořte Excel sešit v C# – Přidávejte a vyplňujte komentáře
tags:
- C#
- Excel automation
- Aspose.Cells
title: Vytvořit Excel sešit v C# – Přidat a vyplnit komentáře pomocí chytrých značek
url: /cs/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu C# – Přidání a vyplnění komentářů pomocí Smart Markers

Už jste někdy potřebovali **create Excel workbook C#** a přemýšleli, jak vložit komentář, který se automaticky aktualizuje? Nejste v tom sami. V mnoha scénářích reportování chcete komentář buňky, který říká *„Created by Alice on 2024‑07‑15“* bez ručního kódování jména nebo data pokaždé.

V tomto tutoriálu vám ukážeme přesně **how to add comment to Excel**, pak **how to fill comment** pomocí Smart Markers od Aspose.Cells. Na konci budete mít připravený program, který vytvoří sešit, vloží dynamický komentář a uloží soubor – vše během několika úhledných kroků.

> **Co získáte:** kompletní, kompilovatelnou C# konzolovou aplikaci, vysvětlení každého řádku, tipy na běžné úskalí a nápady, jak řešení rozšířit.

## Požadavky

- .NET 6.0 SDK nebo novější (kód funguje také s .NET Core a .NET Framework)  
- Visual Studio 2022 nebo jakékoli IDE, které preferujete  
- **Aspose.Cells for .NET** NuGet balíček (`Install-Package Aspose.Cells`) – tato knihovna poskytuje třídy `Workbook`, `Worksheet` a `SmartMarkerProcessor` použité níže.  
- Základní znalost syntaxe C# – pokud jste již použili `Console.WriteLine`, jste připraveni.

Nyní, když je základ připraven, pojďme se ponořit dovnitř.

![Snímek obrazovky příkladu vytvoření Excel sešitu C#](excel-workbook.png "Příklad vytvoření Excel sešitu C#")

## Krok 1: Inicializace nového sešitu – Základy vytvoření Excel sešitu C#

Nejprve potřebujeme čistý objekt sešitu. Představte si `Workbook` jako prázdné plátno; bez něj nemůžete umístit žádné buňky, řádky ani komentáře.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**Proč je to důležité:** `Workbook` automaticky vytvoří výchozí list, takže nemusíte volat `Add`, pokud nepotřebujete další záložky. Přístup k `Worksheets[0]` je nejrychlejší způsob, jak začít naplňovat data.

## Krok 2: Vložení komentáře s Smart Marker – Jak přidat komentář pomocí tokenů

Dále umístíme komentář do buňky **B2**, který obsahuje tokeny Smart Marker (`«UserName»` a `«CreatedDate»`). Tyto tokeny budou později nahrazeny skutečnými hodnotami.

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**Vysvětlení:**  
- `CreateComment()` vytvoří objekt komentáře, pokud neexistuje; jinak vrátí existující.  
- Vlastnost `Note` obsahuje viditelný text. Zabalíme‑li zástupné symboly do `« »`, řekneme Aspose.Cells, že se jedná o **Smart Markery** – zástupné symboly, které lze nahradit najednou.

> **Pro tip:** Pokud potřebujete víceřádkový komentář, použijte `\n` uvnitř řetězce, např. `"Line1\nLine2"`.

## Krok 3: Příprava datového objektu – Jak dynamicky vyplnit komentář

Smart Markery potřebují datový zdroj. V C# je nejjednodušší způsob anonymní typ, který odpovídá názvům zástupných symbolů.

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**Proč anonymní typ?**  
Je lehký, nevyžaduje žádný další soubor třídy a přesně odpovídá názvům vlastností (`UserName`, `CreatedDate`) názvům tokenů. Pokud dáváte přednost silně typovanému modelu, stačí vytvořit třídu se stejnými vlastnostmi.

## Krok 4: Zpracování Smart Markerů – Jak vyplnit komentář pomocí datového objektu

Nyní se děje magie. `SmartMarkerProcessor` prohledá sešit na výskyt tokenů `«…»` a nahradí je hodnotami z `markerData`.

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**Co se děje pod kapotou?**  
`SmartMarkerProcessor` prochází každou buňku, komentář, záhlaví atd., hledá vzor `«Token»`. Když jej najde, použije reflexi k načtení odpovídající vlastnosti z `markerData` a zapíše hodnotu zpět. Žádné ruční smyčky nejsou potřeba.

## Krok 5: Uložení sešitu – Vyplnění Excel komentáře a uložení souboru

Nakonec zapíšeme sešit na disk. Komentář nyní vypadá například takto *„Created by Alice on 03/21/2026 10:15 AM“*.

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Ověření výsledku:** Otevřete `CommentFilled.xlsx` v Excelu, najděte buňku **B2** a uvidíte komentář se skutečným jménem uživatele a časovým razítkem. Pro další spuštění není potřeba měnit kód – stačí změnit hodnoty v `markerData`.

---

## Běžné varianty a okrajové případy

### Použití vlastního formátu data

Pokud chcete datum ve formátu `yyyy‑MM‑dd`, upravte datový objekt:

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### Přidání více komentářů

Můžete opakovat **Krok 2** pro jiné buňky. Každý komentář může mít svůj vlastní soubor tokenů, nebo sdílet stejné, pokud jsou informace univerzální.

### Práce s existujícími sešity

Místo `new Workbook()` načtěte existující soubor:

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

Zbytek kroků zůstává stejný – Smart Markery fungují jak na nových, tak na předchozích souborech.

### Zpracování nulových hodnot

Pokud může token chybět, zabalte vlastnost do nullable typu nebo poskytněte náhradní hodnotu:

```csharp
UserName = user?.Name ?? "Unknown"
```

Procesor vloží *„Unknown“* když je zdroj `null`.

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je **celý program**, který můžete vložit do projektu konzolové aplikace a spustit okamžitě (jen nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce).

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Spusťte program, otevřete vygenerovaný soubor a uvidíte dynamický komentář v buňce **B2**. Jednoduché, že?

---

## Často kladené otázky (FAQ)

**Q: Funguje to s .NET Framework 4.7?**  
A: Rozhodně. Aspose.Cells podporuje .NET Framework 4.0+ a .NET Core/5/6/7. Stačí odkazovat na příslušný DLL nebo NuGet balíček.

**Q: Mohu tento přístup použít pro validaci dat nebo podmíněné formátování?**  
A: Smart Markery slouží především k vkládání hodnot do buněk, komentářů, záhlaví a zápatí. Pro podmíněné formátování byste stále použili standardní API `Style`.

**Q: Co když potřebuji přidat komentář do **jiného** listu?**  
A: Získejte cílový list (`workbook.Worksheets["MySheet"]`) a opakujte **Krok 2** na buňkách tohoto listu.

## Další kroky a související témata

- **How to add comment to Excel** programatically pro více buněk (procházet rozsah).  
- **Fill Excel comment** s daty z databáze (použijte `DataTable` jako zdroj dat pro Smart Markery).  
- Prozkoumejte **Smart Marker arrays** pro automatické generování tabulek.  
- Naučte se o **Aspose.Cells styling** pro formátování písma, barvy a velikosti komentáře.

### Závěr

Právě jsme prošli celý proces **create excel workbook c#**, **add comment to excel**, a **fill excel comment** pomocí Smart Markerů. Řešení je kompaktní, znovupoužitelné a připravené pro produkci.  

Vyzkoušejte to, upravte zástupné symboly a nechte knihovnu udělat těžkou práci. Pokud narazíte na problémy, zanechte komentář níže – šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}