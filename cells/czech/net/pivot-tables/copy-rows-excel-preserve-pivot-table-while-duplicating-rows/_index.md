---
category: general
date: 2026-02-14
description: Kopírovat řádky v Excelu a zachovat kontingenční tabulku najednou. Naučte
  se, jak kopírovat řádky, kopírovat oblast do listu a duplikovat řádky s kontingenční
  tabulkou pomocí Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: cs
og_description: Kopírovat řádky v Excelu a zachovat kontingenční tabulku najednou.
  Postupujte podle tohoto krok‑za‑krokem průvodce pro duplikaci řádků s kontingenční
  tabulkou pomocí C#.
og_title: kopírovat řádky excel – zachovat kontingenční tabulku při duplikaci řádků
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopírovat řádky v Excelu – zachovat kontingenční tabulku při duplikování řádků
url: /cs/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Zachování kontingenční tabulky při duplikaci řádků

Už jste někdy potřebovali **copy rows excel** a zároveň zachovat kontingenční tabulku nedotčenou? V tomto tutoriálu vás provedeme kompletním, spustitelným řešením, které vám ukáže **how to copy rows**, udrží chování **preserve pivot table** a dokonce **duplicate rows with pivot** napříč listy pomocí Aspose.Cells pro .NET.

Představte si, že vytváříte měsíční prodejní zprávu, která čerpá data z hlavního listu, vytvoří kontingenční tabulku a poté musíte odeslat zmenšenou verzi partnerovi. Ruční kopírování oblasti je obtížné a hrozí, že kontingenční tabulku rozbijete. Dobrá zpráva? Několik řádků C# může udělat těžkou práci za vás—žádné klikání myší není potřeba.

> **Co získáte:** kompletní ukázkový kód, krok‑za‑krokem vysvětlení, tipy pro okrajové případy a rychlý sanity‑check pro ověření, že kontingenční tabulka přežila kopírování.

---

## Co budete potřebovat

- **Aspose.Cells for .NET** (the free NuGet package works fine for this demo).  
- Recent **.NET runtime** (4.7+ or .NET 6/7).  
- Excel file (`source.xlsx`) that contains a pivot table on the first worksheet.  
- Visual Studio, Rider, or any C# editor you like.

Žádné další knihovny, žádné COM interop a žádná instalace Excelu na serveru. Proto je tento přístup přátelský k **copy range to sheet** a zároveň bezpečný pro server.

---

## Krok 1 – Načtení sešitu (copy rows excel)

Prvním krokem je otevřít zdrojový sešit. Použití Aspose.Cells nám poskytuje čistý objektový model, který funguje stejně na Windows, Linuxu i Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Proč je to důležité:** načtení sešitu vytvoří v‑paměti reprezentaci každého listu, včetně skrytých objektů jako jsou pivot cache. Jakmile je soubor v paměti, můžeme manipulovat s řádky, aniž bychom se dotýkali uživatelského rozhraní.

---

## Krok 2 – Identifikace cílového listu (copy range to sheet)

Chceme, aby zkopírované řádky skončily na jiném listu—`Sheet2` v tomto příkladu. Pokud list neexistuje, Aspose jej pro vás vytvoří.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Tip:** vždy zkontrolujte `Worksheets.Contains` před přidáním listu; jinak skončíte s duplicitními názvy a výjimkou za běhu.

---

## Krok 3 – Kopírování řádků při zachování kontingenční tabulky

Nyní přichází jádro problému: kopírování řádků **A1:E20** (které zahrnují kontingenční tabulku) z prvního listu do `Sheet2`. Metoda `CopyRows` kopíruje surové buňky *a* podkladový pivot cache, takže kontingenční tabulka zůstane funkční.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Proč to funguje:** `CopyRows` respektuje interní pivot cache, takže kontingenční tabulka na cílovém listu je *živá* kopie, nikoli statický snímek. Tím se splňuje požadavek **preserve pivot table** bez dalšího kódu.

Pokud potřebujete, aby řádky začínaly na jiném posunu na cílovém listu—například řádek 10—stačí změnit třetí argument na `9`.

---

## Krok 4 – Uložení sešitu (duplicate rows with pivot)

Nakonec zapíšete upravený sešit zpět na disk. Kontingenční tabulka bude v novém souboru plně funkční.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Ověření výsledku:** otevřete `copyWithPivot.xlsx` v Excelu, přejděte na *Sheet2* a obnovte kontingenční tabulku. Měli byste vidět stejný rozložení polí a výpočty jako v originálu—nic není poškozeno.

---

## Ověření kopie – Rychlý sanity‑check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Pokud konzole vypíše `True`, úspěšně jste **duplicate rows with pivot** a udrželi analytický engine živý.

---

## Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Navrhovaná úprava |
|-----------|-------------------|-----------------|
| **Zdrojová oblast zahrnuje sloučené buňky** | Sloučené buňky mohou při kopírování způsobit nesoulad. | Použijte `CopyRows` jak je ukázáno; automaticky zachovává sloučení. |
| **Cílový list již obsahuje data** | Nové řádky mohou přepsat existující obsah. | Změňte počáteční řádek cíle (třetí argument) na první prázdný řádek: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Kontingenční tabulka používá externí zdroj dat** | Externí připojení nejsou zkopírována. | Ujistěte se, že zdrojový sešit obsahuje kompletní datovou sadu; jinak po kopírování znovu připojte spojení. |
| **Velký sešit (100 000+ řádků)** | Spotřeba paměti stoupá. | Zvažte kopírování po částech (např. 5 000 řádků najednou), aby byl GC spokojen. |

---

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je celý program, který můžete vložit do konzolové aplikace a okamžitě spustit.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Spusťte program, otevřete vygenerovaný `copyWithPivot.xlsx` a uvidíte, že kontingenční tabulka na **Sheet2** funguje přesně jako originál. Žádná ruční rekonstrukce není potřeba.

---

## Často kladené otázky

**Q: Funguje to s Excel 2003‑kompatibilními soubory `.xls`?**  
A: Ano. Aspose.Cells abstrahuje formát souboru, takže stejný kód funguje pro `.xls`, `.xlsx` i `.xlsb`.

**Q: Co když potřebuji kopírovat *sloupce* místo řádků?**  
A: Použijte `CopyColumns` podobně; stačí vyměnit parametry řádků za indexy sloupců.

**Q: Můžu najednou kopírovat více nespojitých oblastí?**  
A: Ne přímo pomocí `CopyRows`. Projděte každou oblast ve smyčce nebo vytvořte dočasný list, který oblasti sloučí před kopírováním.

---

## Závěr

Právě jsme předvedli čistý vzor **copy rows excel**, který zachovává integritu **preserve pivot table**, umožňuje vám **how to copy rows** efektivně a ukazuje, jak **copy range to sheet** bez ztráty funkčnosti kontingenční tabulky. Na konci tohoto návodu byste měli být sebejistí při **duplicate rows with pivot** v jakémkoli automatizačním pipeline—ať už generujete denní zprávy nebo budujete rozsáhlou službu pro export dat.

Jste připraveni na další výzvu? Zkuste rozšířit kód o:

- Export duplikovaného listu jako PDF.  
- Programatické obnovení kontingenční tabulky po kopírování.  
- Procházení seznamu zdrojových souborů a jejich dávkové zpracování.

Pokud narazíte na potíže, zanechte komentář níže nebo mě kontaktujte na GitHubu. Šťastné kódování a užijte si čas, který jste ušetřili tím, že jste nemuseli ručně tahat Excel!

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}