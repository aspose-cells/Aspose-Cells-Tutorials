---
category: general
date: 2026-06-17
description: Vytvořte sešit Excel a zapište datum do Excelu pomocí japonského kalendáře.
  Naučte se používat CultureInfo, nastavit datum a čas buňky a pracovat s formáty
  japonských érá.
draft: false
keywords:
- create excel workbook
- write date to excel
- use japanese calendar
- how to use cultureinfo
- set cell datetime
language: cs
og_description: Vytvořte sešit Excel a zapište datum do Excelu pomocí japonského kalendáře.
  Tento průvodce ukazuje, jak použít CultureInfo a správně nastavit datum a čas buňky.
og_title: Vytvořit sešit Excel – Zpracování japonských kalendářních dat
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  headline: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  type: TechArticle
- description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  name: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  steps:
  - name: What if the Japanese era changes next year?
    text: The `CultureInfo` object always references the latest era data baked into
      Windows/.NET. When a new era begins, Microsoft updates the underlying calendar
      data via Windows updates. So your code will continue to work without changes—just
      keep the OS patched.
  - name: Can I write multiple dates in a loop?
    text: Absolutely. Just move the parsing and `PutValue` logic inside a `for` loop
      or LINQ query. Remember to adjust the cell address each iteration (e.g., `"A"
      + rowNumber`).
  - name: How does this differ from using `DateTimeOffset`?
    text: '`DateTimeOffset` includes timezone information, which Excel ignores. For
      pure date values, stick with `DateTime`. If you need to preserve UTC offsets,
      store the offset in a separate column.'
  type: HowTo
tags:
- excel
- csharp
- cultureinfo
- datetime
title: Vytvořte Excel sešit s japonskými kalendářními daty – kompletní průvodce
url: /cs/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření sešitu Excel s japonskými kalendářními daty – Kompletní průvodce

Už jste někdy potřebovali **vytvořit sešit Excel**, který respektuje japonský era kalendář? Nejste sami — mnoho vývojářů narazí na problém, když se snaží parsovat data jako “令和3年5月1日” a vložit je do tabulky. Dobrá zpráva? Je to hračka, jakmile znáte správné kroky.

V tomto tutoriálu projdeme, jak **zapsat datum do Excelu** při **používání japonského kalendáře**, vysvětlíme **jak použít CultureInfo** pro parsování éry a ukážeme přesný kód pro **nastavení datum‑času buňky**. Na konci budete mít připravený příklad, který můžete vložit do libovolného .NET projektu.

## Požadavky — Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.7+). API, která používáme, jsou součástí základní knihovny, takže pro část parsování dat nejsou potřeba žádné extra NuGet balíčky.
- Odkaz na knihovnu pro práci s tabulkami, která poskytuje třídy `Workbook`, `Worksheet` a `Cell`. Níže uvedený úryvek používá **Aspose.Cells**, ale můžete ji nahradit za EPPlus, ClosedXML nebo jakoukoli knihovnu s podobným objektovým modelem.
- Základní znalost C# — nic složitého, jen dost na to, abyste šli krok za krokem.
- (Volitelné) Visual Studio 2022 nebo VS Code pro rychlé otestování.

Máte vše připravené? Skvěle — ponořme se do toho.

## Vytvoření sešitu Excel – Přehled krok za krokem

Níže je vysokou úrovní plán, který budeme následovat:

1. **Inicializovat** nový sešit a získat první list.  
2. **Definovat** japonskou kalendářní kulturu pomocí `CultureInfo`.  
3. **Parsovat** řetězec s japonskou érou na `DateTime`.  
4. **Zapsat** parsované datum do konkrétní buňky.  
5. **Uložit** sešit, abyste jej mohli otevřít v Excelu a ověřit výsledek.

Každý krok je rozdělen do vlastní sekce s kódem, vysvětlením a několika „pro tipy“, které později oceníte.

![Snímek obrazovky vytvoření sešitu Excel](https://example.com/create-excel-workbook.png "Snímek obrazovky nově vytvořeného sešitu Excel")

## Krok 1: Vytvoření sešitu Excel a přístup k prvnímu listu

První věc, kterou potřebujeme, je čerstvý objekt sešitu. Představte si ho jako prázdné plátno, na které se postupně kreslí všechny operace.

```csharp
using Aspose.Cells;          // Replace with your library's namespace
using System;
using System.Globalization;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0)
Worksheet ws = workbook.Worksheets[0];
```

**Proč je to důležité:**  
Vytvoření sešitu programově vám umožní vyhnout se zbytečnému otevírání existujícího souboru jen kvůli přidání data. Navíc zaručuje, že sešit začne ve známém, čistém stavu — ideální pro automatizovanou tvorbu reportů.

> **Tip:** Pokud používáte EPPlus, ekvivalentní kód by byl `var package = new ExcelPackage(); var ws = package.Workbook.Worksheets.Add("Sheet1");`.

## Krok 2: Použití japonského kalendáře – Definování CultureInfo

Japonská data jsou vyjádřena pomocí epoch (např. “令和” pro Reiwa). .NET to dokáže zpracovat pomocí *kultury*, která zahrnuje japonský kalendář.

```csharp
// Step 2: Define the Japanese era culture
CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");
```

**Co se zde děje?**  
Identifikátor `"ja-JP-u-ca-japanese"` říká .NETu, aby použil japonské locale **a** japonský kalendář (`ca-japanese`). To znamená, že jakékoli parsování nebo formátování data automaticky rozpozná symboly epoch.

> **Častý úskalí:** Zapomenutí přípony `-u-ca-japanese` způsobí, že parser bude řetězec zpracovávat jako standardní gregoriánské datum, což vyústí v `FormatException`.

## Krok 3: Parsování řetězce s japonskou érou

Nyní převádíme lidsky čitelné japonské datum na objekt `DateTime`, který Excel může uložit.

```csharp
// Step 3: Parse the Japanese era date string
DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);
```

**Proč parsovat tímto způsobem?**  
`DateTime.Parse` respektuje předanou kulturu, takže `"令和3年5月1日"` se stane **1. května 2021** v gregoriánském kalendáři (Reiwa 3 odpovídá roku 2021). Výsledný `DateTime` je nezávislý na časovém pásmu, což je přesně to, co Excel očekává jako hodnotu buňky.

> **Okrajový případ:** Pokud řetězec obsahuje měsíc nebo den bez úvodní nuly (např. “5月1日”), parser stále funguje — jen se ujistěte, že název éry odpovídá aktuální éře, jinak dojde k chybě.

## Krok 4: Zapsání data do Excelu – Nastavení datum‑času buňky

S `DateTime` v ruce jej můžeme vložit do libovolné buňky. Zde cílíme na **A1**, ale můžete použít jakoukoliv adresu.

```csharp
// Step 4: Write the parsed date into cell A1
Cell cell = ws.Cells["A1"];
cell.PutValue(eraDate);               // Aspose.Cells method
cell.Style.Number = 14;               // Apply a date format (e.g., mm/dd/yyyy)
```

**Vysvětlení:**  
- `PutValue` automaticky rozpozná .NET typ a uloží jej jako Excel *Date* (číslo s plovoucí desetinnou čárkou pod kapotou).  
- Nastavení `cell.Style.Number = 14` použije vestavěný krátký formát data v Excelu, což zajistí, že se hodnota zobrazí jako čitelné datum po otevření souboru.

> **Alternativní knihovny:** S EPPlus byste napsali `cell.Value = eraDate; cell.Style.Numberformat.Format = "mm/dd/yyyy";`.

## Krok 5: Uložení sešitu – Zobrazení výsledku

Nakonec zapíšeme sešit na disk, abyste jej mohli otevřít v Excelu a ověřit, že datum je zobrazeno správně.

```csharp
// Step 5: Save the workbook (adjust the path as needed)
string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Po spuštění souboru by buňka **A1** měla zobrazovat **5/1/2021** (nebo formát, který jste zvolili). Pokud změníte kulturu na jinou — např. `"ja-JP-u-ca-japanese"` s jinou érou — uvidíte automatickou konverzi.

> **Tip:** Pokud potřebujete, aby buňka zachovala japonský formát éry při otevření v Excelu, můžete použít vlastní číselný formát jako `[$-ja-JP]ggge"年"M"月"d"日"` — ale to už přesahuje rámec tohoto základního návodu.

## Časté otázky a úskalí

### Co když se japonská era změní příští rok?

Objekt `CultureInfo` vždy odkazuje na nejnovější data epoch, která jsou zabudována ve Windows/.NET. Když nastane nová era, Microsoft aktualizuje podkladová kalendářní data prostřednictvím Windows aktualizací. Váš kód tak bude nadále fungovat bez změn — stačí mít OS aktualizovaný.

### Můžu zapisovat více dat v cyklu?

Určitě. Stačí přesunout logiku parsování a `PutValue` dovnitř `for` smyčky nebo LINQ dotazu. Nezapomeňte při každé iteraci upravit adresu buňky (např. `"A" + rowNumber`).

### Jaký je rozdíl oproti použití `DateTimeOffset`?

`DateTimeOffset` obsahuje informaci o časovém pásmu, kterou Excel ignoruje. Pro čisté datumové hodnoty používejte `DateTime`. Pokud potřebujete zachovat UTC offset, uložte jej do samostatného sloupce.

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je jednorázový program připravený ke zkopírování, který spojuje všechny kroky. Kompiluje se s .NET 6 a Aspose.Cells, ale můžete nahradit volání knihovny podle dříve uvedených poznámek.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class JapaneseDateExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Define the Japanese calendar culture (Japanese era)
        CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");

        // 3️⃣ Parse a date string that uses the Japanese era format
        //    Example: Reiwa 3 (2021) May 1st
        DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);

        // 4️⃣ Write the parsed date into cell A1
        Cell cell = ws.Cells["A1"];
        cell.PutValue(eraDate);
        cell.Style.Number = 14; // Short date format

        // 5️⃣ (Optional) Save the workbook to see the result
        string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Očekávaný výstup:**  
Po spuštění programu se vypíše `Workbook saved to C:\Temp\JapaneseDateDemo.xlsx`. Otevřením souboru uvidíte **5/1/2021** (nebo krátký datumový formát vašeho locale) v buňce **A1**.

## Shrnutí – Co jsme probrali

- **Vytvoření sešitu Excel** od nuly pomocí .NET knihovny pro tabulky.  
- **Zapsání data do Excelu** parsováním japonského řetězce s `CultureInfo`.  
- **Použití japonského kalendáře** (`ja-JP-u-ca-japanese`) pro automatické rozpoznání symbolů epoch.  
- **Jak použít CultureInfo** pro vlastní kalendáře a locale‑specifické parsování.  
- **Nastavení datum‑času buňky** a aplikace číselného formátu pro správné zobrazení.

## Další kroky a související témata

Nyní, když ovládáte vkládání japonských dat, můžete zkusit:

- **Formátování buněk pomocí vlastních japonských formátů epoch** (`ggge"年"M"月"d"日"`).  
- **Generování vícejazykových reportů** přepínáním `CultureInfo` za běhu.  
- **Hromadný import dat z CSV**, kde každý řádek používá jiný kalendářní systém.  
- **Automatizaci tvorby sešitu** pomocí šablon — ideální pro fakturaci nebo výplaty.

Pokud vás zajímá práce s jinými ne‑gregoriánskými kalendáři (např. hebrejským, islámským), stejný vzor `CultureInfo` funguje — stačí jen vyměnit identifikátor kultury.

Klidně experimentujte: změňte řetězec data, vyzkoušejte jinou buňku nebo dokonce přidejte graf, který odkazuje na sloupec s daty. Flexibilita .NET `CultureInfo` v kombinaci se spolehlivou Excel knihovnou umožňuje vše.

Šťastné kódování a ať vaše tabulky vždy ukazují správnou éru!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Automatizace Excelu s Aspose.Cells .NET&#58; Vytvoření sešitu a nastavení externích odkazů](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Jak vytvořit a uložit sešit Excel jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Jak načíst sešit Excel a nastavit velikosti tiskárny pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}