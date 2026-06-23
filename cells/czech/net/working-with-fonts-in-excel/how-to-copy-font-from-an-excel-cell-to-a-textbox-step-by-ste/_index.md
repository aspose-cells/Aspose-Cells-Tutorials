---
category: general
date: 2026-02-15
description: jak zkopírovat font a aplikovat styl buňky v C# s jednoduchým příkladem.
  Naučte se, jak získat styl buňky a použít formátování buňky k nastavení velikosti
  písma v textovém poli.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: cs
og_description: jak zkopírovat písmo z buňky listu a použít styl buňky na TextBox.
  Tento průvodce ukazuje, jak získat styl buňky, použít formátování buňky a nastavit
  velikost písma TextBoxu.
og_title: jak zkopírovat písmo z buňky Excel – kompletní tutoriál C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Jak zkopírovat písmo z buňky v Excelu do TextBoxu – krok za krokem
url: /cs/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

kopírovat písmo z buňky Excel do TextBoxu". Keep URL unchanged.

Then closing shortcodes.

Now produce final content with same structure.

Check we didn't miss any text.

Also note the shortcodes at bottom: {{< /blocks/products/pf/tutorial-page-section >}} etc. Keep.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat písmo z buňky Excel do TextBoxu – kompletní C# tutoriál

Už jste někdy potřebovali **kopírovat písmo** z buňky tabulky a udělat, aby UI textové pole vypadalo naprosto stejně? Nejste v tom sami. V mnoha nástrojích pro reportování nebo vlastních dashboardech se setkáte s tím, že načítáte data z Excelu a snažíte se zachovat vizuální věrnost — rodinu písma, velikost a barvu — beze změny.  

Dobrou zprávou je, že s několika řádky C# můžete **získat styl buňky**, přečíst její vlastnosti písma a **použít styl buňky** na jakýkoli text‑box ovládací prvek. V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje, jak **použít formátování buňky** a dokonce **nastavit velikost písma textového pole** programově.

---

## Co se naučíte

- Jak získat objekt `TextBox` z komponenty mřížky (`gridJs` v našem příkladu)
- Jak přečíst rodinu písma, velikost a barvu z konkrétní buňky Excelu (`B2`)
- Jak zkopírovat tyto atributy písma do textového pole, aby UI odráželo tabulku
- Běžné úskalí (např. konverze barvy) a několik **pro tipů**, jak udržet kód robustní
- Připravený spustitelný úryvek kódu, který můžete vložit do konzolové aplikace nebo projektu WinForms

**Požadavky**  
Měli byste mít:

1. .NET 6+ (nebo .NET Framework 4.8) nainstalováno  
2. Balíček EPPlus NuGet (pro práci s Excelem)  
3. Řídicí prvek mřížky, který vystavuje slovník `TextBoxes` (příklad používá fiktivní `gridJs`, ale myšlenka funguje s libovolnou UI knihovnou)

Teď si uděláme praktické cvičení.

## Krok 1: Nastavení projektu a načtení listu

Nejprve vytvořte nový konzolový nebo WinForms projekt a přidejte EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Poté načtěte sešit a získejte buňku, jejíž styl chcete zkopírovat.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Proč je to důležité:** EPPlus vám poskytuje přímý přístup k objektu `Style`, který obsahuje podobjekt `Font`. Odtud můžete číst `Name`, `Size` a `Color`. To je jádro operace **získat styl buňky**.

## Krok 2: Získání cílového TextBoxu z vaší mřížky

Předpokládáme, že vaše UI mřížka (`gridJs`) ukládá textová pole do slovníku indexovaného názvem sloupce, můžete takto získat požadované:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Pokud používáte WinForms, `notesTextBox` může být ovládací prvek `TextBox`; pro WPF to může být element `TextBox` a pro web‑založenou mřížku to může být objekt JavaScript interop. Klíčové je, že máte referenci, kterou můžete manipulovat.

## Krok 3: Přenos rodiny písma

Nyní, když máme jak zdrojový styl, tak cílový ovládací prvek, zkopírujeme rodinu písma.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Ne všechny UI frameworky exponují vlastnost `FontFamily`, která přijímá prostý řetězec. Ve WinForms byste nastavili `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Přizpůsobte podle potřeby.

## Krok 4: Přenos velikosti písma

Velikost písma je v EPPlus uložena jako `float`. Použijte ji přímo:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Pokud váš ovládací prvek používá body (což většina dělá), můžete hodnotu přiřadit bez konverze. Pro CSS‑založené mřížky možná budete muset připojit `"pt"`.

## Krok 5: Přenos barvy písma

Konverze barvy je nejnáročnější část, protože EPPlus ukládá barvy jako ARGB celá čísla, zatímco mnoho UI frameworků očekává `System.Drawing.Color` nebo CSS hex řetězec.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Proč to funguje:** `GetColor()` rozřeší barvy založené na tématu a vrátí konkrétní `System.Drawing.Color`. Pokud buňka používá výchozí barvu (žádné explicitní nastavení), použijeme černou jako výchozí, aby se předešlo výjimkám null reference.

## Kompletní funkční příklad

Spojením všeho dohromady, zde je minimální konzolová aplikace, která načte soubor Excel, získá písmo z **B2** a použije jej na simulované textové pole.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Očekávaný výstup (předpokládejme, že B2 používá Arial, 12 pt, modrá):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Spusťte program, otevřete své UI a uvidíte, že textové pole „Notes“ nyní odráží přesné stylování písma buňky **B2**. Žádné ruční úpravy nejsou potřeba.

## Často kladené otázky a okrajové případy

### Co když buňka používá barvu tématu místo explicitní RGB hodnoty?

EPPlus `GetColor()` automaticky rozřeší barvy tématu na konkrétní `System.Drawing.Color`. Pokud však používáte starší knihovnu, která vrací jen index tématu, budete muset tento index mapovat na paletu barev sami.

### Mohu kopírovat i jiné atributy stylu (např. tučné, kurzíva)?

Určitě. Objekt `ExcelStyle.Font` také poskytuje `Bold`, `Italic`, `Underline` a `Strike`. Stačí nastavit odpovídající vlastnosti na vašem UI ovládacím prvku:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Co když řídicí prvek mřížky neexponuje vlastnost `FontColor`?

Většina moderních UI frameworků to má, ale pokud ten váš přijímá jen CSS řetězec, převěďte `Color` na hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Jak zvládnout více buněk najednou?

Projděte požadovaný rozsah, načtěte styl každé buňky a aplikujte jej na odpovídající textové pole. Pamatujte na cachování objektů stylu, pokud zpracováváte mnoho řádků, abyste se vyhnuli výkonovým propadům.

## Pro tipy a běžné úskalí

- **Ukládejte ExcelPackage do cache** – otevírání a zavírání souboru pro každou buňku je nákladné. Načtěte sešit jednou a poté znovu použijte objekt `ExcelWorksheet`.
- **Dejte pozor na null barvy** – buňka, která dědí výchozí barvu, vrací `null`. Vždy poskytněte náhradní hodnotu (černá nebo výchozí barva ovládacího prvku).
- **Mějte na paměti DPI škálování** – pokud cílíte na monitory s vysokým DPI, velikosti písma se mohou jevit o něco větší. V případě potřeby upravte pomocí `Graphics.DpiX`.
- **Bezpečnost vláken** – EPPlus není thread‑safe. Pokud zpracováváte mnoho listů paralelně, vytvořte samostatný `ExcelPackage` pro každé vlákno.

## Závěr

Nyní víte, **jak zkopírovat písmo** z buňky Excel a **použít styl buňky** na jakýkoli text‑box ovládací prvek pomocí C#. Získáním `Style` buňky, vytažením jejích `Font` vlastností a přiřazením k UI elementu zachováte vizuální konzistenci bez ručního kopírování.  

Kompletní řešení — načtení sešitu, získání stylu buňky a nastavení rodiny písma, velikosti a barvy textového pole — pokrývá jádro **použití formátování buňky** a ukazuje, jak správně **nastavit velikost písma textového pole**.  

Dále zkuste rozšířit příklad o kopírování barev pozadí, okrajů nebo dokonce celého obsahu buňky. Pokud pracujete s knihovnou datové mřížky, která podporuje bohaté vykreslování buněk, můžete jí nyní předat přesně stejné informace o stylování, které jste získali z Excelu, a udržet tak UI a reporty dokonale synchronizované.  

Máte další otázky? Zanechte komentář nebo prozkoumejte související témata jako „dynamické vazby Excel‑na‑UI“ a „konverze barev s ohledem na téma“. Šťastné programování!

---

![příklad kopírování písma](placeholder-image.jpg "jak kopírovat písmo z buňky Excel do TextBoxu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}