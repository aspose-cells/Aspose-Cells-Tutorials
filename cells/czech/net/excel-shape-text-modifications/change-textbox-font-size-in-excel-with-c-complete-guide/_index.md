---
category: general
date: 2026-05-30
description: Změňte velikost písma textového pole v Excelu pomocí C#. Naučte se rychle
  upravit písmo textového pole v Excelu pomocí kódu krok za krokem.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: cs
og_description: Změňte velikost písma textového pole v Excelu pomocí C#. Tento průvodce
  ukazuje, jak bezpečně a efektivně upravit písmo textového pole v Excelu.
og_title: Změna velikosti písma textového pole v Excelu pomocí C# – kompletní návod
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Změna velikosti písma textového pole v Excelu pomocí C# – Kompletní průvodce
url: /cs/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změna velikosti písma textového pole v Excelu pomocí C# – Kompletní průvodce

Potřebujete **změnit velikost písma textového pole** v listu Excelu z C#? Jste na správném místě. Ať už generujete reporty, stavíte dashboard nebo jen upravujete šablonu, úprava vzhledu textového pole může vašemu sešitu dodat mnohem profesionálnější vzhled.

V tomto tutoriálu také **upravit excel textbox font** nejen co se týká velikosti – myslíme font family, tučnost a dokonce i práci s více tvary. Na konci budete mít připravený útržek kódu, který pokrývá celý proces, od otevření sešitu až po úklid COM objektů. Žádné zbytečnosti, jen praktický kód, který můžete dnes vložit do svého projektu.

## Požadavky — Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte na svém počítači následující:

| Požadavek | Proč je důležitý |
|-----------|-------------------|
| **.NET 6+** (nebo .NET Framework 4.7.2+) | Poskytuje kompilátor a runtime pro C#. |
| **Microsoft.Office.Interop.Excel** NuGet balíček | Dodává potřebné COM interop typy pro komunikaci s Excelem. |
| **Excel nainstalovaný** (jakákoliv recentní verze) | Interop vrstva funguje jen když je Office aplikace přítomna. |
| **Základní znalost C#** | Snadno budete následovat, ale každou řádku vysvětlíme. |

Pokud vám něco chybí, pozastavte se nyní a nainstalujte to; zbytek průvodce předpokládá, že jsou všechny komponenty připravené.

## Krok 1: Nastavení projektu a import jmenných prostorů

Nejprve vytvořte novou konzolovou aplikaci (nebo ji zapojte do existující) a načtěte interop jmenný prostor.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Tip:** Pokud cílíte na .NET 6+, přidejte balíček `Microsoft.Office.Interop.Excel` pomocí `dotnet add package Microsoft.Office.Interop.Excel`. Tím zajistíte, že alias `Excel` bude správně rozpoznán.

## Krok 2: Otevření sešitu a získání cílového listu

Nyní musíme spustit Excel, otevřít soubor a ukázat se na list, který obsahuje textové pole. Zabalení do bloku `try/finally` zaručuje uvolnění COM objektů i v případě, že se něco pokazí.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Proč je to důležité

Otevření sešitu přes COM nám poskytuje živý objektový model – což znamená, že jakákoli změna se okamžitě projeví v souboru. Nastavení `Visible = false` urychlí proces a zabrání vyskakování oken během automatizace.

## Krok 3: Načtení tvaru textového pole

Excel zachází s textovými poli jako s objekty `Shape` v kolekci `Shapes`, nikoli jako s dedikovanou kolekcí `TextBox`. Proto kód níže vypadá trochu jinak než úryvek, který jste možná viděli online.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Pozor:** Kolekce `Shapes` je indexována od 1, takže k nule‑základnímu `textboxIndex`, který předáte, přičteme `+1`. Zapomenutí na to vede k chybám „index out of range“, které mohou být frustrující při ladění.

## Krok 4: Změna velikosti písma (a názvu) textového pole

Tady konečně **změníme velikost písma textového pole**. Vlastnost `TextFrame2` nám dává přístup k možnostem formátování bohatého textu, včetně `Font.Name` a `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Proč používáme `TextFrame2`

`TextFrame2` je novější objektový model zavedený v Office 2007. Podporuje pokročilé typografické funkce a je obecně spolehlivější než starší `TextFrame`. Použitím tohoto modelu zajistíme, že naše **change textbox font size** operace funguje napříč moderními verzemi Excelu.

## Krok 5: Uložení, úklid a ověření

Po úpravě písma musíme změny uložit a uvolnit všechny COM reference. Vynechání úklidu může zanechat osamělé procesy Excelu běžící na pozadí.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Tip:** Pokud potřebujete **modify excel textbox font** na mnoha listech, zabalte vnitřní logiku do smyčky, která iteruje přes `Workbook.Worksheets`. Jen nezapomeňte pro každý list resetovat `textboxIndex`.

## Řešení okrajových případů — Více textových polí a chybějící tvary

Reálné sešity zřídka obsahují jen jedno textové pole. Níže jsou dva rychlé přístupy, které můžete použít, aniž byste přepisovali celou metodu.

### 1. Změnit *všechna* textová pole na listu

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identifikovat textové pole podle jeho **Name** místo indexu

Pokud jste svému textovému poli přiřadili smysluplný název (např. „TitleBox“), můžete jej načíst přímo:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Oba přístupy vám umožní **modify excel textbox font** s přesností, bez ohledu na strukturu sešitu.

## Vizuální přehled (volitelné)

Pokud dáváte přednost rychlému vizuálnímu náhledu, představte si následující diagram:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Alt text:* *změna velikosti písma v Excelu – zvýrazněné textové pole připravené k úpravě písma.*

## Kompletní funkční příklad

Spojením všech částí získáte jediný soubor, který můžete zkopírovat‑vložit do konzolového projektu a spustit okamžitě (jen aktualizujte cestu k souboru a název listu).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Co byste se měli naučit dál?

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}