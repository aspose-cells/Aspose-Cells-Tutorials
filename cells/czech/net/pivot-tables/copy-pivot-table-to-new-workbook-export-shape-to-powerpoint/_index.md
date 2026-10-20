---
category: general
date: 2026-10-20
description: Zkopírujte kontingenční tabulku do nového sešitu pomocí Aspose.Cells
  a naučte se, jak exportovat editovatelný tvar do PowerPointu v jednom průvodci.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: cs
lastmod: 2026-10-20
og_description: Zkopírujte kontingenční tabulku do nového sešitu pomocí Aspose.Cells
  a exportujte editovatelný tvar do PowerPointu — krok za krokem kód, který můžete
  spustit ještě dnes.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Zkopírovat kontingenční tabulku do nového sešitu, exportovat tvar do PowerPointu
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Zkopírovat kontingenční tabulku do nového sešitu, exportovat tvar do PowerPointu
url: /cs/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopírování kontingenční tabulky do nového sešitu, export tvaru do PowerPointu

Pokud potřebujete **copy pivot table to new workbook** a zachovat jeho funkčnost, tento průvodce vám ukáže přesně, jak to provést pomocí Aspose.Cells. Také uvidíte nejrychlejší způsob, jak **export an editable shape to PowerPoint**, takže textové pole zůstane po konverzi editovatelné.

Mnoho vývojářů předpokládá, že kopírování oblasti, která obsahuje kontingenční tabulku, ztratí logiku kontingenční tabulky, nebo že tvary se při uložení jako PPTX změní na statické obrázky. Tento tutoriál tyto mýty vyvrací a poskytuje spolehlivé, produkčně připravené řešení.

V následujících sekcích:

* Načtete zdrojový sešit a zkopírujete oblast, která zahrnuje kontingenční tabulku.
* Vytvoříte cílový sešit, který obsahuje stejnou kontingenční tabulku.
* Přidáte textové pole, upravíte jeho text a uložíte sešit jako prezentaci PowerPoint, kde textové pole zůstane editovatelné.
* Pochopíte, proč je každé volání API nutné a jak se vyhnout běžným úskalím.

**Požadavky**

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+).
* Aspose.Cells pro .NET nainstalovaný (`Install-Package Aspose.Cells`).
* Základní znalost C# a Visual Studio (nebo libovolného IDE, které preferujete).

---

## Kopírování kontingenční tabulky do nového sešitu

Tato krok‑za‑krokem sekce ukazuje, jak zkopírovat oblast, která obsahuje kontingenční tabulku, a zachovat definici kontingenční tabulky v novém souboru.

### Krok 1 – Načtěte zdrojový sešit a vyberte první list

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Proč?*  
`Workbook` je vstupní bod pro jakoukoli manipulaci s Excel soubory v Aspose.Cells. Výběrem správného listu zajistíme, že pracujeme s přesnou polohou kontingenční tabulky.

### Krok 2 – Definujte oblast buněk, která zahrnuje kontingenční tabulku

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Proč?*  
Kontingenční tabulka sídlí v konkrétním bloku buněk. Zadáním `CellArea`, který plně obklopuje kontingenční tabulku, Aspose.Cells ví, že má zkopírovat i podkladovou kontingenční cache.

### Krok 3 – Vytvořte cílový sešit a získejte jeho první list

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Proč?*  
Čerstvý sešit zaručuje, že nebudou kolidovat pojmenované oblasti ani existující kontingenční tabulky, což činí operaci kopírování čistou.

### Krok 4 – Zkopírujte řádky ze zdrojové oblasti do cílového listu

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Proč?*  
`CopyRows` je součástí **Aspose.Cells copy rows** API. Kopíruje jak hodnoty buněk, tak skrytou kontingenční cache, takže kontingenční tabulka zůstane po přesunu funkční.

### Krok 5 – Uložte nový sešit

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Výsledek*  
Otevřete `CopyWithPivot.xlsx` v Excelu. Kontingenční tabulka se zobrazí přesně tak, jako v původním souboru, a můžete ji normálně obnovovat nebo upravovat.

---

## Export editovatelného tvaru do PowerPointu

Nyní přidáme textové pole, změníme jeho obsah a uložíme sešit jako soubor PPTX. Tvar zůstane po otevření v PowerPointu plně editovatelný.

### Krok 1 – Vytvořte nový sešit a přistupte k jeho prvnímu listu

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Krok 2 – Přidejte textové pole do listu

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Proč?*  
`AddTextBox` vytváří **editable textbox in PowerPoint**‑compatible shape. Souřadnice jsou v bodech; upravte je tak, aby odpovídaly vašemu rozvržení.

### Krok 3 – Získejte tvar a upravte jeho text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Proč?*  
Přímý přístup k objektu `Shape` vám umožní měnit vlastnosti jako `Text`, `Font` nebo `Fill`. Tento krok demonstruje, jak programově nastavit počáteční obsah.

### Krok 4 – Uložte sešit jako prezentaci PowerPoint

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Výsledek*  
Otevřete `Presentation.pptx` v Microsoft PowerPoint. Textové pole se objeví na první snímku a můžete na něj dvojklikem upravit text stejně jako u jakéhokoli nativního tvaru PowerPointu.

---

## Očekávaný výstup

| Soubor | Co uvidíte |
|--------|------------|
| `CopyWithPivot.xlsx` | List obsahující původní kontingenční tabulku, plně funkční (obnovení funguje). |
| `Presentation.pptx` | Jeden snímek s editovatelným textovým polem, které zobrazuje „Change me in PowerPoint“. |

---

## Běžná úskalí a tipy pro nejlepší praxi

* **Ztráta kontingenční cache** – Pokud kopírujete jen hodnoty buněk (např. pomocí `CopyRows` s příznakem `PasteOptions` nastaveným na `PasteValues`), kontingenční cache se vynechá a tabulka se stane statickou. Vždy používejte výchozí přetížení `CopyRows`, jak je ukázáno.
* **Umístění tvaru** – `AddTextBox` používá jednotky v bodech, nikoli indexy buněk v Excelu. Otestujte souřadnice na ukázkovém souboru, abyste předešli umístění mimo snímek.
* **Neshoda formátu souboru** – Uložení sešitu jako PPTX pomocí `SaveFormat.Pptx` automaticky převede všechny podporované tvary. Pokus o uložení jako `Pdf` rastrování tvaru, čímž se stane needitovatelným.

---

## Závěr

Nyní víte, jak **copy pivot table to new workbook** a jak **export an editable shape to PowerPoint** pomocí Aspose.Cells pro .NET. Kompletní, spustitelné ukázky kódu pokrývají všechna potřebná volání API, vysvětlují, proč je každý krok důležitý, a ukazují očekávané výsledky.

Dále můžete zkoumat:

* **Práce s grafy** – kopírování grafů společně s kontingenčními tabulkami (`Aspose.Cells copy rows between worksheets`).
* 

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}