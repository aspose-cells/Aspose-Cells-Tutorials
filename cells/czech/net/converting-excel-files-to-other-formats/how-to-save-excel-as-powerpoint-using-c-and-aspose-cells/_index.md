---
category: general
date: 2026-08-17
description: Uložte Excel jako PowerPoint pomocí C# – krok za krokem průvodce převodem
  souborů XLSX, úpravou textových polí a generováním výstupu PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: cs
lastmod: 2026-08-17
og_description: Uložte Excel jako PowerPoint v C# s kompletním příkladem kódu. Naučte
  se, jak převést XLSX, udělat textová pole editovatelná a exportovat do PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Uložte Excel jako PowerPoint v C# – kompletní průvodce převodem
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Jak uložit Excel jako PowerPoint pomocí C# a Aspose.Cells
url: /cs/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit Excel jako PowerPoint pomocí C# a Aspose.Cells

Pokud potřebujete **uložit Excel jako PowerPoint** v .NET projektu, tento průvodce vám ukáže kompletní, připravené řešení. Uvidíte, jak načíst sešit XLSX, učinit každé textové pole na listu editovatelným a exportovat výsledek do souboru PPTX – vše pomocí několika řádků C#.

Převod Excelu do PowerPointu je častý požadavek pro reportovací dashboardy, prezentace nebo automatické generování snímků. Tento tutoriál také pokrývá **jak programově upravovat textová pole**, takže můžete přizpůsobit obsah snímku před uložením.

## Požadavky

* .NET 6.0 (nebo novější) SDK nainstalováno  
* Vývojové prostředí jako Visual Studio 2022 nebo VS Code  
* Licence Aspose.Cells pro .NET (nebo bezplatný evaluační klíč) – stáhněte z [Aspose webu](https://products.aspose.com/cells/net/)  
* Soubor `input.xlsx`, který chcete převést  

> **Pro tip:** Pokud používáte bezplatnou evaluační verzi, výstupní PPTX bude obsahovat vodoznak. Licencovaná verze jej odstraní.

## Krok 1: Instalace NuGet balíčku Aspose.Cells

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Cells
```

## Krok 2: Vytvoření kostry konzolové aplikace

Vytvořte nový konzolový projekt (pokud ještě nemáte):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Nahraďte vygenerovaný soubor `Program.cs` kódem uvedeným v následujících krocích.

## Krok 3: Načtení sešitu a výběr prvního listu

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Proč je to důležité:**  
`Workbook` načte soubor Excel do paměti, zatímco `Worksheet` poskytuje přístup k buňkám, grafům a tvarům listu. První list je často výchozí zpráva, kterou chcete prezentovat.

## Krok 4: Učinit každé textové pole na listu editovatelným

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Proč to potřebujete:**  
Ve výchozím nastavení jsou textová pole importovaná z Excelu v PowerPointu pouze pro čtení. Nastavením `IsEditable = true` umožníte sobě (nebo pozdějším uživatelům PowerPointu) upravovat text přímo na snímku.

## Krok 5: Uložení sešitu jako PowerPoint prezentaci

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Co se děje pod kapotou:**  
`Workbook.Save` rozpozná hodnotu výčtu `SaveFormat.Pptx` a převede rozvržení listu Excelu – včetně řádků, sloupců, grafů a nyní editovatelných textových polí – na objekty snímků v PowerPointu.

## Kompletní zdrojový kód (spustitelný)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Očekávaný výstup

Když spustíte program (`dotnet run`), měli byste vidět:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Otevření `output.pptx` v Microsoft PowerPoint zobrazí snímek, který odráží původní list Excelu. Všechna textová pole lze upravovat přímo dvojitým kliknutím.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Mohu převést konkrétní list místo prvního?** | Ano. Nahraďte `workbook.Worksheets[0]` výrazem `workbook.Worksheets["SheetName"]` nebo libovolným požadovaným indexem. |
| **Co když sešit obsahuje více listů?** | Zavolejte `workbook.Save` pro každý list zvlášť, přičemž pro každý použijete odlišný název souboru PPTX, nebo je spojte do jedné prezentace pomocí objektů `Presentation` z Aspose.Slides. |
| **Zůstanou grafy zachovány?** | Aspose.Cells automaticky převádí grafy z Excelu na objekty grafů v PowerPointu. Není potřeba žádný další kód. |
| **Jak změním velikost snímku?** | Po `workbook.Save` můžete načíst vygenerovaný PPTX pomocí Aspose.Slides a upravit `Presentation.SlideSize`. |
| **Co když potřebuji před uložením upravit text v textovém poli?** | Přistupujte k `shapeItem.TextBox.Text` uvnitř smyčky, upravte jej a poté nastavte `IsEditable = true`. Příklad: `shapeItem.TextBox.Text = "New title";` |

## Tipy pro řešení problémů

* **„ShapeType.TextBox“ nenalezen** – Ujistěte se, že používáte Aspose.Cells verze 25.11 nebo novější; starší verze nemají vlastnost `IsEditable`.  
* **Chyby „Soubor nenalezen“** – Ověřte, že `YOUR_DIRECTORY` je absolutní cesta nebo že relativní cesta ukazuje na správné umístění.  
* **Licence není použita** – Zavolejte `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` před načtením sešitu, aby se odstranily evaluační vodoznaky.

## Závěr

Nyní víte, jak **uložit Excel jako PowerPoint** pomocí C# načtením sešitu XLSX, učiněním každého textového pole editovatelným a exportem do PPTX. Tato metoda automaticky zpracuje grafy, obrázky a formátování buněk, čímž vám poskytne připravenou prezentaci.

Dále prozkoumejte související témata, jako **převod Excelu do PowerPointu s Aspose.Slides**, **jak programově upravovat textová pole po převodu**, nebo **hromadné zpracování více sešitů**. Každé z nich staví na základních krocích zde popsaných a může dále automatizovat váš reportingový workflow.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak převést Excel do PowerPointu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak zkopírovat kontingenční tabulku v C# – Převod Excelu do PPTX, kopírování rozsahu a vytvoření textového pole](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Jak uložit soubory Excel v různých formátech pomocí Aspose.Cells .NET (průvodce 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}