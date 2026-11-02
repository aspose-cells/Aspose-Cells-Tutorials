---
category: general
date: 2026-02-21
description: Naučte se, jak nastavit text v TextBoxu tučně, změnit velikost písma
  v TextBoxu a načíst sešit Excel v C# pomocí Aspose.Cells v kompletním, spustitelném
  příkladu.
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: cs
og_description: Ztučte text v TextBoxu v souboru Excel pomocí C#. Tento tutoriál také
  ukazuje, jak změnit velikost písma v TextBoxu a načíst sešit Excel v C# pomocí Aspose.Cells.
og_title: Ztučte text v TextBoxu v Excelu pomocí C# – Kompletní průvodce
tags:
- C#
- Aspose.Cells
- Excel automation
title: Ztučte text v TextBoxu v Excelu pomocí C# – krok za krokem
url: /cs/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ztučněte text v TextBoxu v Excelu pomocí C# – krok za krokem průvodce

Potřebujete **ztučnit text v TextBoxu** v souboru Excel pomocí C#? V tomto tutoriálu vám přesně ukážeme, jak *načíst Excel sešit*, **změnit velikost písma v TextBoxu** a formátovat text tvaru pomocí Aspose.Cells.  
Pokud jste někdy zírali na nudnou tabulku a pomysleli si „můj textbox by měl vyniknout“, jste na správném místě.

Projdeme každý řádek kódu, vysvětlíme, proč je každé volání důležité, a dokonce se podíváme, co dělat, když list neobsahuje žádné textové boxy. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu – bez tajemných odkazů typu „viz dokumentace“.

## Co budete potřebovat

- **Aspose.Cells for .NET** (free trial or licensed version) – API, které používáme k práci s tvary v Excelu.  
- .NET 6 nebo novější (kód funguje také s .NET Framework 4.7+).  
- Jednoduchý Excel soubor (`input.xlsx`), který již obsahuje alespoň jeden textbox na prvním listu.  

## Ztučněte text v TextBoxu – načtení sešitu a přístup k tvaru

Prvním krokem je otevřít sešit a získat textbox, který chceme upravit.  
Také provádíme rychlou kontrolu, aby kód nezhavaroval, pokud je list prázdný.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**Proč je to důležité:**  
*Načtení sešitu* nám poskytuje objekt `Workbook`, který představuje celý soubor v paměti. Přístup k `Worksheets[0]` je bezpečný, protože každý Excel soubor má alespoň jeden list. Ochranná podmínka (`if (worksheet.TextBoxes.Count == 0)`) zabraňuje `IndexOutOfRangeException` – častému úskalí při automatizaci existujících souborů.

## Změna velikosti písma v TextBoxu

Než ztučnime text, ujistěte se, že velikost je přesně taková, jakou potřebujete.  
Změna velikosti je tak jednoduchá jako úprava vlastnosti `Font.Size`.

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**Pro tip:**  
Pokud potřebujete dynamickou velikost na základě vstupu uživatele, stačí nahradit `12` proměnnou. Objekt `Font` je sdílený napříč celým tvarem, takže změna velikosti okamžitě ovlivní každý znak uvnitř textboxu.

## Ztučněte text v TextBoxu – hlavní akce

Nyní k hlavní funkci: ztučnění textu.  
Příznak `IsBold` mění tloušťku písma, aniž by měnil jakékoli jiné stylování.

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**Co se děje pod kapotou?**  
Aspose.Cells ukládá formátování textu v objektu `Font`, který je připojený k tvaru. Nastavením `IsBold = true` aktualizuje podkladové XML (`<b>1</b>`), které Excel čte při vykreslování listu. Jedná se o **nedestruktivní** operaci – pokud později nastavíte `IsBold = false`, text se vrátí k normální tloušťce.

## Uložení upraveného sešitu

Po dokončení formátování zapíšeme změny zpět na disk.  
Můžete přepsat původní soubor nebo, jak je zde ukázáno, vytvořit nový, aby zdroj zůstal nedotčený.

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**Očekávaný výsledek:**  
Otevřete `output.xlsx` v Excelu. První textbox na prvním listu by měl zobrazovat text ve **Calibri 12 pt, tučně**. Ostatní tvary nejsou ovlivněny.

## Formátování textu tvaru v Excelu – další možnosti stylování (volitelné)

Zatímco hlavním cílem je **ztučnit text v TextBoxu**, můžete také chtít:

| Možnost | Ukázka kódu | Kdy použít |
|--------|--------------|-------------|
| Kurzíva | `textBox.Font.IsItalic = true;` | Zdůraznění podtitulku |
| Barva textu | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | Barvy značky |
| Zarovnání | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | Centrované nadpisy |
| Více TextBoxů | Loop through `worksheet.TextBoxes` | Dávkové formátování |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

Tyto další úpravy ukazují, jak *formátovat text tvaru v Excelu* může být rozšířeno nad rámec pouhého ztučnění.

## Okrajové případy a časté úskalí

1. **Žádné TextBoxy na listu** – Přidaná ochranná podmínka (`if (worksheet.TextBoxes.Count == 0)`) se elegantně ukončí a informuje uživatele.  
2. **Skryté listy** – Skryté listy jsou stále přístupné přes kolekci `Worksheets`; jen se ujistěte, že odkazujete na správný index.  
3. **Velké soubory** – Načtení obrovského sešitu může spotřebovat paměť. Zvažte použití `Workbook.LoadOptions` k načtení jen potřebných částí.  
4. **Různé verze Excelu** – Aspose.Cells funguje s `.xls`, `.xlsx` a dokonce i `.xlsb`. Stejný kód funguje napříč verzemi, ale starší Excel může ignorovat některé novější funkce písma.

## Úplný funkční příklad (připravený ke zkopírování a vložení)

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

Spusťte program, otevřete vygenerovaný `output.xlsx` a uvidíte ztučněný text ve 12‑pt Calibri uvnitř textboxu. Jednoduché, že?

## Závěr

Nyní víte, **jak ztučnit text v TextBoxu** v Excel sešitu pomocí C#, **jak změnit velikost písma v TextBoxu**, a základy **načítání Excel sešitu v C#** s Aspose.Cells. Výše uvedený kompletní příklad je připravený k vložení do libovolného projektu a také jste viděli způsoby, jak **formátovat text tvaru v Excelu** pro bohatší stylování.  
Co dál? Zkuste projít všechny listy a ztučnit všechny textboxy, nebo zkombinujte toto s generováním obsahu řízeným daty – například naplněním textboxu hodnotami z databáze. Stejné principy platí a kód zůstává čistý.  
Máte nějaký tip, který byste chtěli sdílet, nebo narazili na neočekávanou chybu? Zanechte komentář a pojďme konverzaci udržet. Šťastné programování!

![make textbox text bold in Excel using C#](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}