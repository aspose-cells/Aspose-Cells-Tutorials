---
category: general
date: 2026-02-15
description: Jak vytvořit sešit, převést řetězec na datum a formátovat buňku jako
  datum pomocí Aspose.Cells. Naučte se nastavit formát čísla buňky a snadno číst datum
  v Excelu.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: cs
og_description: Jak vytvořit sešit, převést řetězec na datum a formátovat buňku jako
  datum. Kompletní krok‑za‑krokem průvodce čtením dat v Excelu.
og_title: Jak vytvořit sešit a převést řetězec na datum v C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak vytvořit sešit a převést řetězec na datum v C#
url: /cs/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit sešit a převést řetězec na datum v C#

Už jste se někdy zamýšleli **jak vytvořit sešit**, který změní prostý text jako `"R3-04-01"` na skutečnou hodnotu `DateTime`? Nejste v tom sami — mnoho vývojářů narazí na tento problém při načítání dat ze starých systémů nebo uživatelského vstupu. Dobrá zpráva? S několika řádky C# a Aspose.Cells to zvládnete během chvilky, bez ručního parsování.

V tomto tutoriálu projdeme celý proces: vytvoříme sešit, vložíme řetězec s datem, použijeme **formát buňky jako datum**, vynutíme **nastavení číselného formátu buňky** a nakonec **přečteme datum z Excelu** zpět jako `DateTime`. Na konci budete mít funkční úryvek, který můžete vložit do libovolného .NET projektu.

## Požadavky

- .NET 6+ (nebo .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** NuGet balíček (`Install-Package Aspose.Cells`)
- Základní znalost syntaxe C#
- IDE jako Visual Studio nebo VS Code (kterýkoliv vyhovuje)

Žádná další konfigurace není potřeba — Aspose.Cells se postará o veškeré těžké operace interně.

## Krok 1: Jak vytvořit sešit — inicializace Excel souboru

Nejprve potřebujeme čerstvý objekt sešitu. Představte si ho jako prázdný zápisník, kde každá list je stránka.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Proč je to důležité:* Vytvoření sešitu nám poskytuje kontejner pro buňky, styly a vzorce. Bez něj není kam vložit řetězec s datem.

## Krok 2: Převést řetězec na datum — vložit surový text

Nyní vložíme surový řetězec s datem do buňky **A1** prvního listu. Řetězec používá vlastní formát (`R3-04-01`), který Excel standardně nepozná.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Proč to děláme:* `PutValue` uloží doslovný text. Kdybychom se pokusili nastavit `DateTime` přímo, vlastní formát by se ztratil. Uchování jako text nám umožní později použít **nastavení číselného formátu buňky**, který Excelu řekne, jak text interpretovat.

## Krok 3: Formát buňky jako datum — aplikovat styl číslo 14

Vestavěný styl Excelu číslo 14 odpovídá `mm-dd-yy`. Přiřazením tohoto stylu řekneme enginu: „Treat the content of this cell as a date.“

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*Co se děje pod kapotou:* Vlastnost `Number` mapuje na interní ID číselných formátů v Excelu. Když sešit přepočítá, Excel se pokusí převést text na sériové datum pomocí zadaného formátu.

## Krok 4: Nastavit číselný formát buňky — vynutit přepočet

Excel text automaticky nepřevádí, dokud nepožádáme o vyhodnocení vzorců (nebo v tomto případě o reinterpretaci buňky). Volání `CalculateFormula` tento převod spustí.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Tip:* Pokud pracujete s mnoha buňkami, můžete `CalculateFormula` zavolat jednou po dokončení všech formátovacích úprav — ušetříte tak několik milisekund.

## Krok 5: Přečíst datum z Excelu — získat hodnotu DateTime

Nakonec vyčteme reprezentaci `DateTime` z buňky. Aspose.Cells ji poskytuje přes `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Očekávaný výstup (při výchozím gregoriánském kalendáři):**

```
2023-04-01 00:00:00
```

Všimněte si, že předpona `"R3-"` je ignorována, protože Excelův parser dat se soustředí na číselnou část, pokud je styl nastaven jako datum. Pokud vaše řetězce obsahují jiné předpony, možná bude nutné je předzpracovat, ale pro mnoho starých formátů tento přístup funguje perfektně.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravený program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Uložte jej jako `Program.cs`, obnovte balíček Aspose.Cells a spusťte `dotnet run`. V konzoli by se měl zobrazit formátovaný `DateTime`.

## Časté varianty a okrajové případy

### Různé řetězce s daty

Pokud vaše vstupní data vypadají jako `"2023/04/01"` nebo `"01‑Apr‑2023"`, můžete použít stejný postup — jen změňte vlastnost **Number** na formát odpovídající vzoru (např. `Number = 15` pro `d-mmm-yy`).  

### Formáty specifické pro locale

Excel respektuje nastavení locale sešitu. Pro vynucení US‑stylu parsování nastavte kulturu sešitu:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### Když řetězec není rozpoznán

Někdy Excel nedokáže datum odvodit (např. `"R3-13-40"`). V takových případech předzpracujte řetězec:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Pak aplikujte stejný číselný formát.

## Profesionální tipy a úskalí

- **Pro tip:** Použijte `StyleFlag` k úpravě jen číselného formátu, aniž byste zasahovali do ostatních stylových atributů.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Dejte si pozor na:** Přepisování existujících stylů v buňce, která už má ohraničení nebo písmo. Přístup se `StyleFlag` tomu předchází.
- **Poznámka o výkonu:** Pokud zpracováváte tisíce řádků, seskupte volání `CalculateFormula` po dokončení všech aktualizací; volání po každém řádku přidává zbytečnou režii.

## Závěr

Nyní víte **jak vytvořit sešit**, **převést řetězec na datum**, **formátovat buňku jako datum**, **nastavit číselný formát buňky** a nakonec **přečíst datum z Excelu** zpět do `DateTime`. Vzorec je jednoduchý: vložíte surový text, použijete datumový styl, vynutíte přepočet a pak odečtete hodnotu.  

Odtud můžete logiku rozšířit na celé sloupce, importovat CSV data nebo dokonce generovat reporty, které automaticky převádějí staré řetězce s daty na správná Excelová data.  

Jste připraveni posunout se dál? Vyzkoušejte vlastní číselný formát (`Number = 22`) pro zobrazení dat jako `yyyy-mm-dd`, nebo prozkoumejte utilitu `DateTimeConversion` v Aspose.Cells pro složitější scénáře.

Šťastné programování! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}