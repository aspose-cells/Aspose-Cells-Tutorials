---
category: general
date: 2026-07-03
description: Jak exportovat soubory Excel do PowerPointu s editovatelnými textovými
  poli pomocí Aspose.Cells – krok za krokem průvodce převodem XLSX na PPTX.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: cs
og_description: Jak exportovat Excel do PowerPointu s editovatelnými textovými poli.
  Naučte se převést XLSX na PPTX pomocí PresentationExportOptions v C#.
og_title: Jak exportovat Excel do PowerPointu – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: Jak exportovat Excel do PowerPointu – kompletní průvodce
url: /cs/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel do PowerPointu – Kompletní průvodce

Už jste se někdy zamýšleli, **jak exportovat excel** data přímo do prezentace PowerPoint, aniž byste ztratili možnost úprav? Nejste v tom sami. V tomto tutoriálu vám ukážeme praktický způsob, jak **vytvořit PowerPoint z Excelu**, přičemž textová pole a tvary zůstanou plně upravitelná.

Projdeme každý řádek kódu, vysvětlíme, proč je každé nastavení důležité, a nakonec získáte soubor PowerPoint, který můžete okamžitě otevřít a upravit. Na konci budete schopni **převést XLSX na PPTX** jedním voláním metody a pochopíte, jak **prezentační exportní možnosti** řídí výsledek.

## Co budete potřebovat

- **.NET 6.0** (nebo jakákoli novější verze .NET) nainstalovaná na vašem počítači.  
- **Licence** pro **Aspose.Cells for .NET** (zdarma zkušební verze funguje pro testování).  
- Základní znalost C# — nic složitého, jen schopnost vytvořit konzolovou aplikaci nebo malou knihovnu.  
- Excel sešit (`input.xlsx`), který chcete převést na sadu snímků.

To je vše. Žádné další nástroje, žádné COM interop, jen čistý spravovaný kód.

![Jak exportovat excel do PowerPoint diagram](https://example.com/placeholder.png "Diagram ukazující tok, jak exportovat excel data do PowerPointu")

## Krok 1: Nainstalujte Aspose.Cells a nastavte projekt

Pro **jak exportovat excel** nejprve potřebujete knihovnu, která to umožňuje. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Cells
```

Tím se stáhne nejnovější balíček Aspose.Cells z NuGet. Knihovna obsahuje vše, co potřebujete pro **presentation export options**, takže nebudete muset odkazovat na sestavy Office Interop.

> **Tip:** Pokud cílíte na .NET Framework, použijte odpovídající verzi NuGet (např. `Aspose.Cells.NET`), abyste se vyhnuli překvapením s kompatibilitou.

## Krok 2: Načtěte Excel sešit

Nyní, když je knihovna na místě, načtěme zdrojový soubor. Třída `Workbook` představuje celý Excel dokument.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Proč je to důležité:* Načtení sešitu je prvním krokem v jakémkoli workflow **convert XLSX to PPTX**. Objekt `Workbook` obsahuje listy, grafy a formátování buněk, které lze později mapovat na objekty PowerPointu.

## Krok 3: Nakonfigurujte Presentation Export Options (Upravitelné textové pole)

Zde se děje kouzlo. Ve výchozím nastavení Aspose.Cells exportuje tvary jako statické obrázky. Aby zůstaly **editable text boxes**, musíte povolit správný příznak.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **Proč povolit `ExportEditableObjects`?**  
> Když je tato vlastnost `true`, Aspose.Cells převádí každý Excel tvar na nativní tvar PowerPointu. To znamená, že můžete otevřít výsledný `.pptx` v PowerPointu a upravit text, změnit velikost pole nebo barvy — přesně to, co očekáváte při **create PowerPoint from Excel**.

## Krok 4: Exportujte sešit do PowerPointu

Po načtení sešitu a nastavení možností poslední řádek uloží soubor jako prezentaci PowerPoint.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*Co uvidíte:* Soubor `output.pptx` bude obsahovat jeden snímek na každý list (ve výchozím nastavení). Každý snímek odráží rozvržení původního listu a každé textové pole, které jste umístili v Excelu, bude nyní **editable text box** v PowerPointu.

## Krok 5: Ověřte výsledek a upravte podle potřeby

Otevřete `output.pptx` v Microsoft PowerPoint:

1. Přejděte na snímek, který vznikl z listu.  
2. Klikněte na textové pole — všimněte si, že můžete text upravovat přímo.  
3. Upravte velikost nebo barvu tvaru; změny zůstanou.

Pokud něco vypadá špatně, zvažte následující úpravy:

- **Exportovat pouze konkrétní listy:** Použijte `workbook.Worksheets.RemoveAt(index)` před uložením.  
- **Řídit rozvržení snímků:** Nastavte `exportOptions.ExportAllSheetsAsSlide = false` a ručně přidejte snímky.  
- **Zachovat formátování grafu:** Ujistěte se, že grafy jsou umístěny na listu před exportem; automaticky se stanou grafy PowerPointu.

## Časté problémy a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| Tvary se stávají obrázky | `ExportEditableObjects` ponecháno na výchozí (`false`) | Nastavte `ExportEditableObjects = true` jak je ukázáno v kroku 3. |
| Chybějící listy | `Save` zavoláno před odstraněním nežádoucích listů | Odstraňte nebo skryjte listy, které nepotřebujete, před exportem. |
| Velká velikost souboru | Vysoké rozlišení obrázků vložených spolu s tvary | Použijte `exportOptions.ImageResolution = 150` pro snížení DPI, pokud je potřeba. |
| Varování o kompatibilitě v PowerPointu | Použití staré verze Aspose.Cells | Aktualizujte na nejnovější balíček NuGet (podporuje PPTX 2016+). |

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny kroky, zpracování chyb a komentáře.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**Očekávaný výstup v konzoli:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

Otevřete vygenerovaný `output.pptx` — uvidíte, že každý list byl převeden na snímek a každý tvar, který jste přidali v Excelu, je nyní **editable text box**, který můžete okamžitě upravit.

## Shrnutí: Jak rychle a čistě exportovat Excel

Prošli jsme celý proces **how to export excel** — od instalace Aspose.Cells, přes konfiguraci **presentation export options**, až po finální **convert XLSX to PPTX** s plně upravitelným obsahem. Hlavní body jsou:

- Použijte `PresentationExportOptions.ExportEditableObjects = true` pro zachování upravitelných tvarů.  
- Metoda `Workbook.Save` provádí těžkou práci; nepotřebujete žádný COM interop.  
- Upravit volitelné nastavení (rozlišení obrázku, výběr listů) pro doladění výsledku.

## Co dál?

Pokud vás baví převádět tabulky na snímky, možná budete chtít také prozkoumat:

- **Vkládání grafů** jako nativní grafy PowerPointu (`exportOptions.ExportChartAsShape = false`).  
- **Použití vlastního master slide** po exportu pro sladění s firemní identitou.  
- **Automatizace hromadných konverzí** pro desítky souborů pomocí jednoduché smyčky `foreach`.  

Všechny tyto témata staví na stejných základech, které jsme právě probrali, takže už máte pevný základ.

---

Neváhejte zanechat komentář, pokud narazíte na potíže, nebo se podělit, jak jste tento vzor rozšířili ve svých projektech. Šťastné programování a užívejte si bezproblémové propojení mezi Excelem a PowerPointem!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak převést Excel na PowerPoint pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak přidat a přistupovat k textovým polím v Excelu pomocí Aspose.Cells .NET | Průvodce krok za krokem](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Jak exportovat Excel soubory v .NET pomocí Aspose.Cells: Kompletní průvodce](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}