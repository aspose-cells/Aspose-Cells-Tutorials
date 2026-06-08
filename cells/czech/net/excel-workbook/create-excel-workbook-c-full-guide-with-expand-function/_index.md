---
category: general
date: 2026-06-08
description: Vytvořte Excel sešit v C# krok za krokem a naučte se používat funkci
  EXPAND v Excelu pro dynamické rozsahy. Ideální pro vývojáře .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: cs
og_description: Vytvořte Excel sešit v C# s jasným příkladem a objevte, jak použít
  funkci EXPAND v Excelu k vytvoření dynamických polí.
og_title: Vytvořte Excel sešit v C# – Kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Vytvoření Excel sešitu v C# – Kompletní průvodce s funkcí Expand
url: /cs/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu C# – Kompletní průvodce s funkcí EXPAND

Už jste se někdy zamýšleli, jak **vytvořit Excel sešit C#** bez boje s COM interop nebo manipulací s XML? Nejste v tom sami. V mnoha .NET projektech potřebujeme vygenerovat tabulku, naplnit ji vzorci a předat ji netechnickým uživatelům. Dobrá zpráva? S moderní knihovnou jako **Aspose.Cells** je celý proces hračka.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **vytvoří Excel sešit C#**, vloží několik vzorců – včetně toho, **jak použít funkci EXPAND v Excelu** – a uloží soubor, takže jej můžete okamžitě otevřít v Excelu. Na konci budete vědět nejen *co* napsat, ale i *proč* je každý řádek důležitý, a získáte šablonu, kterou můžete zkopírovat do libovolného projektu.

## Požadavky

Než se pustíme do práce, ujistěte se, že máte:

- .NET 6 SDK (nebo jakoukoli novější verzi .NET) nainstalovanou.
- IDE kompatibilní s NuGet (Visual Studio, VS Code, Rider atd.).
- NuGet balíček **Aspose.Cells** – poskytuje třídy `Workbook` a `Worksheet` používané v kódu.
- Základní znalost C#; není potřeba žádná předchozí zkušenost s Excelem.

Máte vše připravené? Skvěle – pojďme na to.

## Krok 1: Nastavení projektu a přidání Aspose.Cells

Nejprve vytvořte konzolovou aplikaci a přidejte knihovnu.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Tip:** Pokud jste v korporátní síti, možná budete muset nastavit proxy pro NuGet. Balíček Aspose.Cells je lehký, takže instalace proběhne během několika sekund.

Otevřete `Program.cs`. Uvidíte výchozí metodu `Main` – nahraďte ji následujícím kostrou.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

Řádek `using Aspose.Cells;` přináší třídy pro práci s tabulkami do dosahu. Pokud jej zapomenete, kompilátor si bude stěžovat, že `Workbook` není definován – což později chceme předejít.

## Krok 2: Vytvoření Excel sešitu C# a přístup k prvnímu listu

S připraveným projektem můžeme konečně **vytvořit Excel sešit C#**. Konstruktor `Workbook` nám poskytne nový, prázdný sešit a index `Worksheets[0]` vrátí výchozí list (nazvaný „Sheet1“).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Proč si explicitně bereme první list? Protože mnoho následných API (např. nastavení vzorců) vyžaduje objekt `Worksheet`, ne jen `Workbook`. To také činí kód přehlednějším pro každého, kdo jej bude později číst.

## Krok 3: Použití funkce EXPAND v Excelu pro vyplnění dynamického rozsahu

Nyní přichází hvězda show: **použít funkci EXPAND v Excelu**. Funkce `EXPAND` (dostupná od Excel 365) vezme zdrojové pole a rozšíří jej na požadovanou velikost. V našem příkladu začneme s 3‑řádkovým vertikálním polem vytvořeným pomocí `SEQUENCE(3)` a rozšíříme jej na blok 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Co se vlastně děje?

1. `SEQUENCE(3)` vytvoří vertikální pole `{1;2;3}`.
2. `EXPAND(...,5,5)` řekne Excelu, aby toto pole zvětšil na 5 řádků a 5 sloupců.
3. Výsledkem je mřížka 5 × 5, kde první tři řádky obsahují čísla 1‑3 opakovaná napříč sloupci a zbývající dva řádky jsou prázdné.

Protože vzorec zapisujeme jako řetězec, Excel jej vyhodnotí *při otevření souboru*, ne během běhu programu. To znamená, že sešit zůstane lehký a jakékoli změny ve zdrojovém poli se automaticky projeví.

> **Okrajový případ:** Pokud uživatel otevře sešit ve starší verzi Excelu, která funkci `EXPAND` nepodporuje, buňka zobrazí `#NAME?`. Pro ochranu můžete vzorec zabalit do `IFERROR`, ale v moderních prostředích je bezpečné spoléhat se na tuto funkci.

## Krok 4: Přidání vzorce pro kotangens jako doplněk

Přidejme ještě jeden vzorec, abychom ukázali, jak snadno lze vkládat matematické výrazy. Vypočítáme kotangens π/4, což je přesně `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Funkce `COT` v Excelu není tak často používaná jako `SIN` nebo `COS`, ale je ideální pro trigonometrické workflow. Po otevření sešitu buňka **B1** zobrazí `1`.

## Krok 5: Uložení sešitu a ověření výsledku

Všechen ten výstup by byl zbytečný, kdybychom soubor neuložili. Metoda `Save` zapíše sešit z paměti na disk. Vyberte složku, do které máte právo zápisu, a dejte souboru přátelské jméno.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Spusťte program:

```bash
dotnet run
```

Měli byste vidět zprávu v konzoli potvrzující uložení. Otevřete `output.xlsx` v Excelu a všimněte si:

- Buňky **A1:E5** jsou vyplněny rozšířenou sekvencí (1,2,3 v prvních třech řádcích, prázdné v řádcích 4‑5).
- Buňka **B1** zobrazuje hodnotu `1` z kotangensového vzorce.

To je kompletní cyklus: **vytvořit excel sešit c#**, vložit vzorce a získat použitelnou tabulku.

![Snímek obrazovky vygenerovaného Excel sešitu zobrazující rozšířené pole a výsledek kotangensu](/images/create-excel-workbook-csharp.png "příklad vytvoření excel sešitu c#")

*Alt text obrázku: vytvořit excel sešit c# – pohled na vyplněnou tabulku.*

## Krok 6: Volitelné – automatické přizpůsobení šířky sloupců pro profesionální vzhled

Pokud plánujete soubor distribuovat koncovým uživatelům, rychlé automatické přizpůsobení sloupců mu dodá profesionální vzhled.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Tento řádek projde každý sloupec, který obsahuje data, a upraví jeho šířku podle nejdelší položky. Je to malý detail, ale zabraňuje otravnému přetečení „…###“, když jsou čísla širší než výchozí šířka sloupce.

## Krok 7: Závěr a další kroky

Gratulujeme – právě jste se naučili, jak **vytvořit excel sešit c#** od nuly a jak **použít funkci EXPAND v excelu** k vytvoření dynamických polí. Kód je úmyslně minimalistický, abyste jej mohli zkopírovat do libovolného projektu, ale koncepty jsou škálovatelné:

- **Dynamické zdroje dat:** Nahraďte `SEQUENCE(3)` odkazem na jiný rozsah nebo pojmenovanou tabulku.
- **Podmíněné formátování:** Použijte `ws.Cells["A1:E5"].Style` k přidání barev na základě hodnot.
- **Grafy a obrázky:** Aspose.Cells dokáže vkládat grafy, obrázky a dokonce kontingenční tabulky.

Nebojte se experimentovat – měňte rozměry `EXPAND`, vyzkoušejte `FILTER` nebo `SORT`, nebo řetězte více vzorců dohromady. Knihovna se postará o vše, aniž byste se museli dotýkat nízkoúrovňového formátu OpenXML.

---

### Často kladené otázky

**Q: Funguje to s .NET Framework 4.8?**  
A: Ano. Aspose.Cells cílí na .NET Standard 2.0, který je kompatibilní jak s .NET Core, tak s klasickým Frameworkem.

**Q: Co když potřebuji list chránit?**  
A: Použijte `ws.Protect(ProtectionType.All, "yourPassword");` před uložením.

**Q: Můžu zapisovat sešit přímo do `MemoryStream`?**  
A: Ano – `workbook.Save(stream, SaveFormat.Xlsx);` je užitečné pro webová API, která vrací soubor ke stažení.

---

## TL;DR

Vytvořili jsme **kompletní C# konzolovou aplikaci**, která:

1. **Vytvoří Excel sešit C#** pomocí Aspose.Cells.  
2. **Použije funkci EXPAND v Excelu** k převodu 3‑řádkového pole na blok 5 × 5.  
3. Přidá vzorec pro kotangens (`COT(PI()/4)`).  
4. Uloží soubor a volitelně automaticky přizpůsobí šířku sloupců.

Nyní máte pevný základ pro jakýkoli automatizační úkol, který zahrnuje generování Excel souborů z .NET. Šťastné kódování a ať vaše tabulky zůstávají vždy bez chyb!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak vytvořit pojmenované rozsahy omezené na sešit v Excelu pomocí Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Jak vytvořit a použít sjednocené rozsahy v Excelu s Aspose.Cells .NET (průvodce pro C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Vytvoření Excel sešitu s grafy pomocí Aspose.Cells .NET | Krok za krokem](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}