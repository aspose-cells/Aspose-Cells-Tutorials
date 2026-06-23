---
category: general
date: 2026-03-18
description: Kopírování kontingenční tabulky v C# s Aspose.Cells. Naučte se, jak kopírovat
  rozsah v Excelu, duplikovat kontingenční tabulku, kopírovat rozsah do nového listu
  a kopírovat kontingenční tabulku do listu během několika minut.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: cs
og_description: Kopírování kontingenční tabulky v C# pomocí Aspose.Cells. Naučte se
  duplikovat kontingenční tabulku v Excelu, kopírovat oblast Excelu na nové místo
  a kopírovat kontingenční tabulku do listu s kompletními příklady kódu.
og_title: Kopírování kontingenční tabulky v C# – Kompletní programovací průvodce
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopírování kontingenční tabulky v C# – krok za krokem
url: /cs/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopírování kontingenční tabulky v C# – Kompletní programovací průvodce

Už jste někdy potřebovali **kopírovat kontingenční tabulku** z jedné části sešitu do druhé, ale nebyli jste si jisti, jak to udělat, aniž byste ztratili podkladová datová připojení? Nejste v tom sami. Mnoho vývojářů narazí na tento problém při automatizaci Excelových reportů, zejména když kontingenční tabulka žije uvnitř většího datového bloku. Dobrá zpráva? S Aspose.Cells můžete kopírovat kontingenční tabulku **přesně tak, jak vypadá**, a zároveň se naučíte, jak **kopírovat excelový rozsah**, **duplikovat excelovou kontingenční tabulku** a dokonce **kopírovat kontingenční tabulku do listu** pomocí několika řádků C#.

V tomto tutoriálu projdeme reálný scénář: přesunout kontingenční tabulku, která zabírá *A1:J20*, do nové oblasti *M1:V20* ve stejném listu. Na konci budete mít spustitelný program, pochopíte, proč je každý krok důležitý, a budete vědět, jak kód přizpůsobit pro jiné rozsahy nebo dokonce pro samostatné listy. Žádná externí dokumentace není potřeba — vše je zde.

---

## Požadavky

Než se pustíme do práce, ujistěte se, že máte:

- **Aspose.Cells pro .NET** (verze 23.9 nebo novější). Můžete jej získat přes NuGet: `Install-Package Aspose.Cells`.
- Základní vývojové prostředí pro C# (Visual Studio 2022, Rider nebo VS Code s rozšířením C#).
- Excelový soubor (`source.xlsx`) obsahující kontingenční tabulku v rozsahu *A1:J20*.

To je vše. Pokud umíte vytvořit konzolovou aplikaci, můžete začít.

---

## Jak kopírovat kontingenční tabulku v Aspose.Cells

Jádrem řešení je jediný volání `Worksheet.Cells.CopyRange`. Tato metoda nejen kopíruje surové hodnoty buněk, ale také automaticky zachovává kontingenční tabulky, grafy a další bohaté objekty. Rozložme si to.

### Krok 1: Načtení zdrojového sešitu

Nejprve musíme načíst sešit do paměti.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Proč je to důležité:** Načtení sešitu vytvoří jeho in‑memory reprezentaci, kterou může Aspose.Cells manipulovat bez spouštění Excelu. Je to rychlé, vlákny‑bezpečné a funguje na serverech.

### Krok 2: Získání prvního listu

Většina příkladů používá první list, ale můžete cílit na libovolný index nebo název.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** Pokud potřebujete **kopírovat kontingenční tabulku do listu** místo stejného listu, stačí změnit odkaz `worksheet` na jiný objekt `Worksheet`.

### Krok 3: Definování zdrojového a cílového rozsahu

Použijeme struktury `CellArea` k popisu bloků, které přesouváme.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Vysvětlení:** Indexy řádků a sloupců jsou nulové. Sloupec 0 = **A**, sloupec 12 = **M** atd. Upravit tato čísla podle toho, kde se vaše kontingenční tabulka nachází.

### Krok 4: Provedení kopírovací operace

Nyní se děje magie. Nastavení posledního boolean parametru na `true` říká Aspose.Cells, aby kopíroval všechny objekty — včetně kontingenční tabulky.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Proč `true`?** Příznak označuje „kopírovat všechny objekty“. Pokud jej nastavíte na `false`, přesunou se jen prosté hodnoty buněk a kontingenční tabulka bude ztracena.

### Krok 5: Uložení sešitu

Nakonec zapíšeme upravený sešit zpět na disk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Výsledek:** `copy-pivot.xlsx` nyní obsahuje původní kontingenční tabulku na *A1:J20* **i** identickou kopii na *M1:V20*. Otevřete soubor v Excelu a ověřte, že obě kontingenční tabulky fungují a zachovávají svá datová připojení.

---

## Kopírování excelového rozsahu na nové místo – rychlá varianta

Někdy potřebujete jen **kopírovat excelový rozsah** bez ohledu na kontingenční tabulky. Stejná metoda `CopyRange` to zvládne; jen poslední argument nastavte na `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Kdy použít:** Pokud přesouváte surová data pro dočasný výpočetní list, vypnutí kopírování objektů šetří paměť a zrychluje operaci.

---

## Duplikování excelové kontingenční tabulky napříč více listy

Co když chcete **duplikovat excelovou kontingenční tabulku** na jiném listu? Princip zůstává stejný; jen jako cíl odkazujete na jiný `Worksheet`.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Hraniční případ:** Pokud zdrojová kontingenční tabulka používá tabulku, která leží na původním listu, Aspose.Cells také zkopíruje definici podkladové tabulky, takže nová kontingenční tabulka funguje hned po vytvoření.

---

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| **Kontingenční tabulka ztrácí cache** | Použití `CopyRange` s `false` nebo vlastní kopírovací rutina, která ignoruje objekty. | Vždy předávejte `true`, když potřebujete samotnou kontingenční tabulku. |
| **Cílové buňky již obsahují data** | Přepisuje se tiše, což může poškodit existující vzorce. | Nejprve vymažte cílovou oblast: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Zdrojový rozsah neobsahuje celou kontingenční tabulku** | Kontingenční tabulky zasahují do více řádků/sloupců, než očekáváte (např. skryté řádky). | Použijte `worksheet.PivotTables[0].DataRange` k programovému získání přesných hranic. |
| **Kopírování mezi sešity** | `CopyRange` funguje jen v rámci jednoho sešitu. | Použijte `sourceWorksheet.Cells.CopyRange` do dočasného rozsahu, pak `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Očekávaný výstup a ověření

Po spuštění programu:

1. Otevřete `copy-pivot.xlsx`.
2. Uvidíte dvě identické kontingenční tabulky — jednu na **A1:J20**, druhou na **M1:V20**.
3. Obnovte libovolnou kontingenční tabulku; obě by měly odrážet stejná podkladová data.
4. Pokud jste duplikovali na jiný list, nový list bude také obsahovat funkční kopii.

Rychlý způsob, jak to ověřit pomocí kódu:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Profi tip: Automatické zjišťování rozsahu

Hard‑coding `CellArea` funguje pro statické reporty, ale produkční kód často potřebuje najít kontingenční tabulku dynamicky.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Proč to dělat?** Tím učiníte řešení odolným vůči změnám rozvržení — už žádné chyby typu „Oops, kontingenční tabulka se přesunula na B2“.

---

![copy pivot table example](copy-pivot.png){alt="příklad kopírování kontingenční tabulky"}

*Screenshot (placeholder) ukazuje původní kontingenční tabulku vlevo a duplikovanou vpravo.*

---

## Shrnutí

Právě jsme probrali, jak **kopírovat kontingenční tabulku** v C# pomocí Aspose.Cells, prozkoumali způsoby **kopírování excelového rozsahu**, **duplikování excelové kontingenční tabulky** a dokonce **kopírování kontingenční tabulky do listu** napříč listy. Hlavní poznatky jsou:

- Použijte `Worksheet.Cells.CopyRange` s příznakem `true` pro zachování bohatých objektů.
- Definujte zdrojové a cílové objekty `CellArea` s nulovými indexy.
- Změňte cílový list, pokud potřebujete **kopírovat kontingenční tabulku do listu**.
- Dbejte na hraniční případy, jako jsou existující data, skryté řádky a scénáře napříč sešity.

---

## Co dál?

- **Dynamické vyhledávání kontingenčních tabulek**: Vytvořte pomocnou funkci, která prohledá sešit a automaticky replikuje všechny kontingenční tabulky.
- **Export do PDF/HTML**: Po kopírování můžete list převést do reportového formátu — Aspose.Cells to také zvládne.
- **Ladění výkonu**: U velkých sešitů zvažte vypnutí výpočtů před kopírováním a opětovné zapnutí po dokončení.

Nebojte se experimentovat: změňte cílové souřadnice, kopírujte do zcela nového sešitu nebo dokonce projděte více listů a vytvořte konsolidovaný report. Možnosti jsou neomezené a s tímto základem budete schopni přizpůsobit kód téměř pro jakýkoli úkol automatizace Excelu.

Šťastné programování a ať vaše kontingenční tabulky vždy zůstávají dokonale synchronizované!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}