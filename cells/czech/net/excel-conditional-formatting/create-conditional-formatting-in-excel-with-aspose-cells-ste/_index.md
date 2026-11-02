---
category: general
date: 2026-06-30
description: Vytvořte podmíněné formátování v sešitu Excel pomocí Aspose.Cells. Naučte
  se, jak nastavit pozadí buňky, řadit buňky a programově vytvořit soubor.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: cs
og_description: Vytvořte podmíněné formátování v sešitu Excel pomocí Aspose.Cells.
  Postupujte podle tohoto kompletního tutoriálu, abyste nastavili pozadí buňky, seřadili
  buňky a automatizovali Excel.
og_title: Vytvořte podmíněné formátování v Excelu pomocí Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořte podmíněné formátování v Excelu pomocí Aspose.Cells – krok za krokem
url: /cs/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření podmíněného formátování v Excelu pomocí Aspose.Cells – krok za krokem

Už jste se někdy zamýšleli, jak **vytvořit podmíněné formátování** v souboru Excel, aniž byste otevírali uživatelské rozhraní? Nejste v tom sami. Mnoho vývojářů potřebuje **vytvořit excel workbook** soubory za běhu a provedení toho programově ušetří hodiny ruční práce. V tomto tutoriálu vám ukážeme přesně, jak **vytvořit podmíněné formátování**, stylovat buňky a dokonce ohodnotit nejvyšší hodnoty – vše pomocí výkonné knihovny Aspose.Cells pro .NET.

Provedeme vás reálným příkladem: generování seznamu skóre, zvýraznění vysokých skóre světle zelenou a nastavení zlatého pozadí pro tři nejlepší výkonnostní výsledky. Na konci budete vědět **jak nastavit pozadí buňky**, **jak ohodnotit buňky** a **jak použít Aspose** pro sofistikovanou automatizaci Excelu. Žádné zbytečnosti, jen kompletní, spustitelný kód, který můžete vložit do libovolného C# projektu.

## Co se naučíte

- Jak **vytvořit excel workbook** pomocí Aspose.Cells  
- Jak naplnit oblast náhodnými daty (skóry)  
- Jak **nastavit pozadí buňky** pomocí plných barev  
- Jak použít pravidlo založené na vzorci k **ohodnocení buněk** a zvýraznit nejlepší tři  
- Jak uložit výsledek jako soubor .xlsx  

Požadavky: .NET 6+ (nebo .NET Framework 4.6+), Visual Studio (nebo jakékoli C# IDE) a odkaz na NuGet balíček Aspose.Cells. Pokud jste s Aspose ještě nepracovali, nebojte se – ukážeme vám **jak používat Aspose** od základů.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*Image alt text: create conditional formatting example in an Excel workbook generated with Aspose.Cells.*

## Jak vytvořit Excel Workbook pomocí Aspose.Cells

Nejprve potřebujete objekt workbook, se kterým budete pracovat. Aspose.Cells to zvládne jedním řádkem.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Proč přejmenováváme list? Jasný název (např. **Scores**) usnadňuje pozdější odkazování, zejména když soubor sdílíte s netechnickými uživateli.  

Nyní, když workbook existuje, naplníme sloupec A náhodnými skóry.

## Jak naplnit data – vytvoření náhodných skóre

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Rychlá poznámka: `PutValue` automaticky detekuje datový typ, takže nemusíte přetypovávat na `int`. Smyčka začíná na `i = 0`, ale zapisuje do řádku `i + 1`, protože řádky v Excelu jsou číslovány od 1, zatímco kolekce `Cells` je číslována od 0.

## Jak nastavit pozadí buňky pro vysoká skóre

Nyní **vytvoříme podmíněné formátování**, které obarví jakékoli skóre ≥ 80 světle zeleným odstínem.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Vlastnost `ForegroundColor` určuje barvu výplně, zatímco `Pattern = BackgroundType.Solid` říká Excelu, aby použil plnou výplň místo gradientu nebo vzoru. Toto je jádro **jak nastavit pozadí buňky** na základě číselného prahu.

## Jak ohodnotit buňky a zvýraznit top‑3

Ohodnocení je o něco složitější, protože potřebujeme vzorec, který vyhodnotí každou buňku vůči celé oblasti. Aspose.Cells vám umožní použít stejnou syntaxi Excelových vzorců, jakou byste zadali do UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Proč `A2` ve vzorci? Aspose vyhodnocuje vzorec relativně k každé buňce v oblasti, takže `A2` se automaticky posune na `A3`, `A4` atd., jak se pravidlo aplikuje řádek po řádku. Funkce `RANK` vrací pozici hodnoty v určeném rozsahu a část `<=3` zajistí, že jen tři nejvyšší skóre získají zlatou výplň.

## Jak uložit workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou, do které může vaše aplikace zapisovat. Po spuštění metody otevřete soubor v Excelu a uvidíte:

- Světle zelené buňky pro jakékoli skóre ≥ 80  
- Zlaté buňky pro tři nejvyšší skóre, ať už jsou také ≥ 80 nebo ne  

To je kompletní **vytvořit podmíněné formátování** pipeline.

---

## Kompletní, spustitelný příklad

Zde je celá metoda znovu, připravená ke zkopírování a vložení do konzolové aplikace nebo libovolné C# třídy:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Očekávaný výsledek

Po otevření `Scores_ConditionalFormatting.xlsx`:

- Buňky s hodnotou **80** nebo vyšší svítí světle zeleně.  
- Tři nejvyšší čísla (i když jsou pod 80) mají **zlaté** pozadí.  
- Všechny ostatní buňky si ponechají výchozí bílé pozadí.

Tento vizuální podnět okamžitě ukáže manažerovi, kdo jsou nejlepší výkonnostní výsledky, bez nutnosti ručního řazení.

---

## Často kladené otázky a okrajové případy

**Co když potřebuji více než tři nejlepší skóre?**  
Stačí změnit část vzorce `<=3` na `<=5` (nebo jakékoliv jiné číslo). Pravidlo se automaticky přizpůsobí.

**Mohu použít více oblastí formátování?**  
Ano. Zavolejte `sheet.ConditionalFormattings.Add` znovu s jiným rozsahem a poté přidejte podmínky k tomuto novému objektu `ConditionalFormatting`.

**Co s staršími verzemi Excelu?**  
Aspose.Cells ve výchozím nastavení ukládá do moderního formátu `.xlsx`, který je kompatibilní s Excel 2007 a novějšími. Pokud potřebujete `.xls`, předávejte `SaveFormat.Excel97To2003` metodě `Save`.

**Má to dopad na výkon u velkých listů?**  
Podmíněné formátování je uloženo jako metadata, takže významně neovlivňuje velikost souboru. Přesto generování stovek tisíc řádků může zvýšit spotřebu paměti – zvažte zpracování po dávkách.

---

## Další kroky

Nyní, když ovládáte **jak vytvořit podmíněné formátování**, můžete zkusit:

- **Jak vytvořit Excel grafy** programově (další perla Aspose.Cells)  
- **Jak nastavit pozadí buňky** na základě textových hodnot (např. „Pass/Fail“)  
- **Jak použít Aspose.Cells pro datovou validaci** a rozbalovací seznamy  

Každé z těchto témat staví na stejných základech, které jste právě získali, takže se budete cítit jako doma.

---

## Závěr

Prošli jsme kompletním, end‑to‑end příkladem, jak **vytvořit podmíněné formátování** v Excel workbooku pomocí Aspose.Cells. Od inicializace workbooku, naplnění dat, **nastavení pozadí buňky**, ohodnocení nejlepších výkonů až po finální uložení souboru – každý krok byl pokryt s ohledem na **jak ohodnotit buňky** i **jak používat Aspose**.  

Vyzkoušejte kód, upravte prahy a sledujte, jak rychle můžete generovat profesionální reporty pro jakýkoli obchodní scénář. Máte vlastní tip nebo trik, který chcete sdílet? Zanechte komentář níže – šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}