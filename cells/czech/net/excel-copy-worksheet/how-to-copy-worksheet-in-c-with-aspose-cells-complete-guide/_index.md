---
category: general
date: 2026-03-30
description: Jak zkopírovat list v C# pomocí Aspose.Cells – podrobný návod krok za
  krokem zahrnující kopírování rozsahu buněk, kopírování sloupců mezi listy, kopírování
  kontingenční tabulky listu a přidání kódu pro vytvoření nového listu.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: cs
og_description: Naučte se, jak kopírovat list v C# s Aspose.Cells. Tento průvodce
  ukazuje kopírování rozsahu buněk, zachování kontingenčních tabulek, kopírování sloupců
  mezi listy a přidání kódu pro nový list.
og_title: Jak zkopírovat list v C# – Kompletní tutoriál Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak zkopírovat list v C# pomocí Aspose.Cells – kompletní průvodce
url: /cs/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat list v C# s Aspose.Cells – Kompletní průvodce

Už jste se někdy zamýšleli **jak zkopírovat list** v C# bez ztráty jediného kontingenčního tabulky nebo vzorce? Nejste sami – mnoho vývojářů narazí na problém, když potřebují duplikovat list a zachovat všechny výhody. V tomto tutoriálu vás provedeme praktickým, end‑to‑end řešením, které nejen kopíruje data, ale také zachovává **copy worksheet pivot table**, zpracovává **copy cell range** a ukazuje **add new worksheet code**, který budete potřebovat.

Probereme vše od načtení zdrojového sešitu až po uložení cílového souboru, takže můžete **copy columns between sheets**, zachovat objekty a mít čistý kód. Žádné nejasné odkazy, jen kompletní, spustitelný příklad, který můžete dnes vložit do svého projektu.

## Co tento tutoriál pokrývá

- Načtení existujícího souboru Excel pomocí Aspose.Cells  
- Použití **add new worksheet code** k vytvoření cílového listu  
- Definování **copy cell range**, který zahrnuje kontingenční tabulku  
- Nastavení **CopyOptions** pro zachování grafů, vzorců a kontingenčních tabulek  
- Provádění **copy columns between sheets** s řádkovou přesností  
- Uložení výsledku a ověření, že list byl správně zkopírován  

Na konci tohoto průvodce budete schopni sebejistě odpovědět na otázku „how to copy worksheet“, ať už automatizujete reporty nebo vytváříte UI řízené tabulkami.

---

## Jak zkopírovat list – Přehled

Než se ponoříme do kódu, načrtneme vysokou úroveň postupu. Považujte to za recept:

1. **Load** zdrojový sešit (`Source.xlsx`).  
2. **Add** nový list pro uložení kopie (`add new worksheet code`).  
3. **Define** oblast, kterou chcete duplikovat (`copy cell range`).  
4. **Configure** možnosti kopírování, aby kontingenční tabulka přežila (`copy worksheet pivot table`).  
5. **Copy** řádky a sloupce (`copy columns between sheets`).  
6. **Save** nový sešit (`Destination.xlsx`).  

A to je vše – šest kroků, žádná magie. Každý krok je vysvětlen níže s ukázkami kódu a odůvodněním.

---

## Krok 1 – Načtení zdrojového sešitu

Nejprve: potřebujete instanci `Workbook`, která ukazuje na soubor, který chcete duplikovat. Tento krok je zásadní, protože Aspose.Cells pracuje přímo se souborovým systémem, ne s UI Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Proč je to důležité:* Načtení souboru vytvoří v‑paměti reprezentaci každého listu, buňky a objektu. Bez toho není co kopírovat a jakýkoli pokus o `add new worksheet code` později selže, protože zdrojová data nejsou přítomna.

---

## Krok 2 – Přidání nového listu (add new worksheet code)

Nyní potřebujeme místo, kam vložit zkopírovaná data. Zde se uplatní **add new worksheet code**. List můžete pojmenovat libovolně; zde jej nazýváme `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Tip:* Pokud plánujete kopírovat více listů, volejte `Worksheets.Add` uvnitř smyčky a každému listu dejte jedinečný název. Tím předejdete kolizím názvů a udržíte sešit přehledný.

---

## Krok 3 – Definování oblasti pro kopírování buněk

**copy cell range** říká Aspose.Cells přesně, které řádky a sloupce duplikovat. V mnoha reálných scénářích oblast zahrnuje kontingenční tabulku, takže musíme být přesní.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Proč to potřebujeme:* Explicitním určením oblasti se vyhnete kopírování celého listu (což může být zbytečné) a zajistíte, že kontingenční tabulka bude uvnitř kopírované oblasti. To je podstata **how to copy worksheet**, když potřebujete jen část listu.

---

## Krok 4 – Nastavení možností kopírování (preserve copy worksheet pivot table)

Aspose.Cells poskytuje objekt `CopyOptions`, který řídí, co se vloží. Pro zachování kontingenční tabulky, grafů a vzorců nastavíme `PasteType.All` a povolíme `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Vysvětlení:* `PasteType.All` je nejobsáhlejší volba, zatímco `PasteSpecial` říká enginu, aby správně zacházel s komplexními objekty – jako jsou kontingenční tabulky. Přeskočení tohoto kroku je častá chyba; zkopírovaný list by ztratil své interaktivní funkce.

---

## Krok 5 – Kopírování řádků a sloupců (copy columns between sheets)

Nyní přichází těžká část: skutečný přesun dat. Použijeme `CopyRows` a `CopyColumns` k řešení **copy columns between sheets**. Použití obojího zajišťuje zachování sloučených buněk a šířek sloupců.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Co se děje:* `CopyRows` přesouvá data řádek po řádku, zatímco `CopyColumns` dělá totéž sloupec po sloupci. Spuštění obojího zaručuje, že celý obdélníkový blok je duplikován, což je nezbytné, když potřebujete **copy columns between sheets**, které mají různé šířky sloupců nebo skryté sloupce.

---

## Krok 6 – Uložení sešitu

Nakonec zapíšete změny zpět na disk. Tento krok dokončuje proces **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Tip pro ověření:* Otevřete `Destination.xlsx` a zkontrolujte, že list `"Copy"` vypadá identicky jako originál, kontingenční tabulky fungují a šířky sloupců odpovídají. Pokud něco vypadá špatně, vraťte se k nastavení `CopyOptions`.

---

## Okrajové případy a běžné varianty

### Kopírování více listů

Pokud potřebujete duplikovat několik listů, zabalte výše uvedenou logiku do smyčky `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Zachování vzorců mezi různými sešity

Když mají zdrojový a cílový sešit různé pojmenované oblasti, nastavte `copyOptions` na `PasteType.Formulas` kromě `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Velké oblasti a výkon

Pro masivní datové sady (stovky tisíc řádků) zvažte použití pouze `CopyRows` a vynechání `CopyColumns`, pokud šířky sloupců nejsou kritické. To může ušetřit několik sekund.

---

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program, který zahrnuje vše, o čem jsme mluvili. Vložte jej do konzolové aplikace, upravte cesty k souborům a stiskněte **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Očekávaný výsledek:** Otevřením `Destination.xlsx` se zobrazí list pojmenovaný **Copy**, který zrcadlí první list `Source.xlsx` – včetně všech kontingenčních tabulek, formátování a šířek sloupců. Originální soubor zůstane nedotčen.

---

## Často kladené otázky

**Q: Funguje to s .xlsx soubory vytvořenými v Excelu 2019?**  
A: Naprosto. Aspose.Cells podporuje všechny moderní formáty Excelu, takže stejný kód funguje pro `.xlsx`, `.xlsm` a dokonce i starší soubory `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}