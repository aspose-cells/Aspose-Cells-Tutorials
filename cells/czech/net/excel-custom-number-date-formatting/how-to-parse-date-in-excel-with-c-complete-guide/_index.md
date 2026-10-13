---
category: general
date: 2026-05-23
description: Jak parsovat datum z buňky Excelu pomocí C#. Naučte se triky s vlastním
  číselným formátem v Excelu, čtěte datum z buňky a použijte vlastní formát pro přesné
  výsledky.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: cs
og_description: Jak načíst datum z buňky Excelu pomocí C#. Tento tutoriál ukazuje,
  jak použít vlastní číselný formát v Excelu, načíst datum z buňky a správně naformátovat
  datum v buňce Excelu.
og_title: Jak parsovat datum v Excelu pomocí C# – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Jak parsovat datum v Excelu pomocí C# – Kompletní průvodce
url: /cs/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsovat datum v Excelu pomocí C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak parsovat datum** uložené v listu Excelu, aniž byste museli ručně manipulovat s převody řetězců? Nejste v tom sami. Ať už získáváte japonské fiskální datum, evropské kombinace měsíc‑den, nebo jakýkoli řetězec specifický pro locale, získání spolehlivého `DateTime` v C# může připadat jako honění se za pohyblivým cílem.

V tomto tutoriálu projdeme konkrétním, end‑to‑end příkladem, který **aplikuje vlastní číselný formát v Excelu** na textovou buňku, a poté **čte datum z buňky** jako správný `DateTime`. Na konci přesně vědět, jak **formátovat datum v buňce Excelu**, **aplikovat vlastní formát**, a vyhnout se běžným úskalím, která zaskočí většinu vývojářů.

## Požadavky

- .NET 6.0 nebo novější (kód funguje s .NET Core, .NET Framework a .NET 5+)
- Odkaz na knihovnu pro práci s tabulkami, která podporuje manipulaci se styly – ve vzorku se používá **Aspose.Cells**, ale koncepty lze přenést na EPPlus, ClosedXML nebo NPOI.
- Základní znalost C# (máte to, že?)

> **Tip:** Pokud ještě nemáte Aspose.Cells, můžete si stáhnout bezplatnou zkušební verzi z jejich webu a přidat ji přes NuGet: `dotnet add package Aspose.Cells`.

## Přehled řešení

1. **Vytvořit sešit** a zaměřit se na první buňku prvního listu.  
2. **Vložit řetězec data specifický pro locale** (v našem případě japonské).  
3. **Aplikovat vlastní číselný formát**, který řekne Excelu, aby text interpretoval jako datum.  
4. **Načíst hodnotu buňky** zpět jako objekt `DateTime`.

To je celý tok – žádné ruční parsování, žádné gymnastické cvičení s `DateTime.ParseExact`. Pojďme na to.

---

## Krok 1: Nastavení sešitu a cílové buňky

Nejprve vytvořte nový sešit a získejte buňku, se kterou budeme pracovat. To odráží scénář „nový sešit“, ze kterého většina dávkových úloh začíná.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Proč je to důležité:** Programatické inicializování sešitu zajišťuje, že kontrolujeme každý aspekt souboru – žádná skrytá formátovací překvapení. Objekt `Cell` je naším vstupním bodem jak pro obsah, tak pro styl.

---

## Krok 2: Vložit japonský řetězec data

Excel často přijímá data jako prostý text, zejména když data pocházejí ze starších systémů. Zde to simulujeme vložením japonského data era přímo do buňky.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Poznámka k okrajovému případu:** Pokud buňka již obsahovala skutečné datum v Excelu (sériové číslo), můžete krok s vlastním formátem přeskočit. Tento průvodce se soustředí na cestu *text‑na‑datum*.

---

## Krok 3: Aplikovat vlastní číselný formát, který interpretuje text jako datum

Nyní přichází magie: řekneme Excelu, aby text zpracoval pomocí **vlastního číselného formátu v Excelu**, který respektuje japonské locale. Formátovací řetězec `[$-ja-JP]yyyy` získá část roku, ale můžete jej rozšířit o měsíc a den podle potřeby.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Proč vlastní formát funguje

Excel interně ukládá data jako sériová čísla. Aplikací formátu, který je citlivý na locale, se Excel pokusí *interpretovat* podkladový text podle vzoru. Předpona `[$-ja-JP]` vynutí japonská kalendářní pravidla, zatímco zbytek vzoru mapuje znaky na rok, měsíc a den.

> **Alternativa:** Pokud potřebujete obecnější přístup, můžete použít `[$-en-US]mm/dd/yyyy` pro americký styl dat, nebo jakýkoli jiný kód kultury podporovaný Windows.

---

## Krok 4: Získat parsované datum jako objekt `DateTime`

Nakonec požádáme buňku o její `DateTimeValue`. Aspose.Cells automaticky převádí formátovaný text na správnou instanci `DateTime`.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Očekávaný výstup do konzole**

```
Parsed date: 2021-05-12
```

> **Co když vrátí `DateTime.MinValue`?** To obvykle znamená, že formát neodpovídá obsahu buňky. Zkontrolujte znovu vlastní formátovací řetězec a ujistěte se, že kód locale odpovídá zdrojovému jazyku.

---

## Bonus: Zpracování dalších locale a reálných variant

### 1. Parsování evropských dat (např. „12/05/2021“ ve francouzštině)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Když buňka již obsahuje sériové datum

Pokud zdrojový soubor Excel již ukládá skutečnou hodnotu data, můžete vlastní formát úplně přeskočit:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Náhradní řešení – ruční parsování

Někdy jsou data nečistá (přebytečné mezery, skryté znaky). Bezpečná náhrada je:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Ale přístup **aplikovat vlastní formát** je obvykle rychlejší a méně náchylný k chybám, protože využívá parsovací engine Excelu.

---

## Běžné úskalí a jak se jim vyhnout

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Chybný kód locale (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` zůstává na `1/1/1900` | Ověřte přesný řetězec LCID; použijte `CultureInfo.GetCultureInfo("ja-JP").LCID` pro jistotu. |
| Chybějící uvozovky kolem statického textu | Excel interpretuje `"年"` jako zástupný znak formátu a selže | Obalte statické znaky do dvojitých uvozovek, např. `\"年\"`. |
| Buňka je již formátována jako *Text* | Vlastní formát je ignorován | Nejprve vymažte `NumberFormat` buňky: `firstCell.SetStyle(workbook.CreateStyle());` |
| Použití knihovny, která nepodporuje vlastnost `Custom` | Chyba při kompilaci | Přepněte na knihovnu, která umožňuje vlastní číselné formáty (Aspose.Cells, EPPlus, ClosedXML). |

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Spusťte program, otevřete `ParsedDateExample.xlsx` a uvidíte, že buňka **A1** zobrazuje `2021年5月12日`, zatímco podkladová hodnota je správné datum v Excelu.

---

## Závěr

Probrali jsme **jak parsovat datum** řetězce v Excelu pomocí C# tím, že **aplikujeme vlastní číselný formát v Excelu** a poté **čteme datum z buňky** jako nativní `DateTime`. Hlavní poznatky:

- Použijte vlastní formát citlivý na locale (`[$-ja-JP]…`), aby Excel udělal těžkou práci.  
- Přistupujte k `Cell.DateTimeValue`, abyste získali čistý `DateTime` bez ručního parsování.  
- Přizpůsobte formátovací řetězec pro jiné kultury a vždy to ověřte rychlým výpisem do konzole.

Od tady můžete **formátovat datum v buňce Excelu** pro reporty, vložit `DateTime` do databází nebo provádět výpočty přímo ve vaší C# aplikaci. Experimentujte s různými locale, kombinujte více buněk nebo dokonce dávkově zpracovávejte celé listy – stejné principy platí.

Máte podivný formát data, který se vám nedaří rozluštit? Zanechte komentář a společně to vyřešíme. Šťastné programování!

## Související tutoriály

- [Excel vlastní číselné a datumové formátování](/cells/english/net/excel-custom-number-date-formatting/)
- [Mistrovství prezentace dat v Excelu: číselné a vlastní datumové formátování s Aspose.Cells pro Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel vlastní číselné datumové formátování](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}