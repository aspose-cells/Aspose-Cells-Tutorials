---
category: general
date: 2026-02-15
description: Vytvořte nový sešit v C# a zkopírujte kontingenční tabulku, aniž byste
  ztratili její definici. Naučte se, jak kopírovat řádky, zachovat kontingenční tabulku
  a snadno duplikovat kontingenční tabulku.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: cs
og_description: Vytvořte nový sešit v C# a zkopírujte kontingenční tabulku při zachování
  její definice. Průvodce krok za krokem pro vývojáře.
og_title: Vytvořit nový sešit v C# – zachovat kontingenční tabulku
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořit nový sešit v C# – zachovat kontingenční tabulku
url: /cs/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu v C# – Zachování kontingenční tabulky

Už jste někdy potřebovali **vytvořit nový sešit** v C#, který obsahuje přesnou kopii kontingenční tabulky z jiného souboru? Nejste v tom sami. V mnoha reportingových řetězcích je kontingenční tabulka srdcem analýzy a ztráta její definice při přesunu dat je noční můra.

Dobrá zpráva? Několika řádky kódu Aspose.Cells můžete zkopírovat řádky — včetně kontingenční tabulky — do nového sešitu a vše zůstane nedotčeno. Níže uvidíte **jak zkopírovat řádky**, **zachovat nastavení kontingenční tabulky** a dokonce **duplikovat kontingenční tabulku** napříč soubory, aniž by se porušily vzorce nebo cache.

## Co tento tutoriál pokrývá

1. Načtení zdrojového sešitu, který již obsahuje kontingenční tabulku.  
2. **Vytvoření nového sešitu** objektů pro cíl.  
3. Použití `CopyRows` k přenosu oblasti, která obsahuje kontingenční tabulku.  
4. Uložení výsledku s zajištěním, že kontingenční tabulka zůstane funkční.  

Žádná externí dokumentace není potřeba — pouze kód, vysvětlení a pár praktických tipů, které můžete vložit přímo do svého projektu.

> **Pro tip:** Aspose.Cells funguje s .NET Core, .NET Framework a dokonce Xamarin, takže stejný úryvek běží kdekoliv ho potřebujete.

---

![Vytvoření nového sešitu s kopírovanou kontingenční tabulkou](/images/create-new-workbook-pivot.png "vytvoření nového sešitu s kopírovanou kontingenční tabulkou")

## Krok 1 – Vytvoření nového sešitu a načtení zdrojového souboru

Prvním krokem je **vytvořit nový sešit** objekt. Jeden obsahuje původní data, druhý přijme zkopírovanou oblast.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Proč je to důležité:*  
`Workbook` je vstupní bod pro jakoukoli manipulaci s Excel v Aspose.Cells. Vytvořením nového sešitu garantujeme čistý start — žádné skryté styly nebo zbylé listy, které by později mohly způsobit problémy.

## Krok 2 – Jak zkopírovat řádky včetně kontingenční tabulky

Nyní přichází jádro problému: **jak zkopírovat řádky**, které obklopují kontingenční tabulku, aniž by se rozpadla. Metoda `CopyRows` dělá právě to.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Několik poznámek:

* `startRow` a `totalRows` definují blok, který obsahuje kontingenční tabulku.  
* Metoda kopíruje **obě** surová data i cache kontingenční tabulky, takže cílový sešit ví, jak tabulku znovu sestavit za běhu.  
* Pokud vaše kontingenční tabulka začíná hlouběji v listu, stačí změnit indexy — není potřeba jiná API volání.

> **Často kladená otázka:** *Ztratí zkopírovaná kontingenční tabulka odkaz na zdrojová data?*  
> Ne. Aspose.Cells vloží cache přímo do listu, takže kontingenční tabulka je v novém souboru samostatná.

## Krok 3 – Zachování kontingenční tabulky při ukládání cíle

Po zkopírování řádků zůstává kontingenční tabulka v cílovém sešitu přesně tak, jak byla ve zdroji. Uložení souboru je jednoduché.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Když otevřete `destination.xlsx` v Excelu, uvidíte kontingenční tabulku připravenou k obnovení. Chování **zachovat kontingenční tabulku** je automatické, protože cache cestovala spolu s řádky.

### Ověření výsledku

Otevřete soubor a:

1. Klikněte na kontingenční tabulku.  
2. Všimněte si, že se zobrazí seznam polí — to znamená, že cache je neporušená.  
3. Proveďte obnovení; data se aktualizují bez chyb.

Pokud narazíte na chybu *#REF!*, zkontrolujte, že zkopírovaná oblast zahrnuje skryté řádky cache (obvykle hned za viditelnými daty).

## Krok 4 – Duplikování kontingenční tabulky do více sešitů (volitelné)

Někdy potřebujete stejnou kontingenční tabulku v několika zprávách. Vzor, který jsme právě použili, se snadno škáluje — stačí opakovat kopírování pro každý nový sešit.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Tento úryvek **duplikuje kontingenční tabulku** třikrát v jednom cyklu. Přizpůsobte pole `targets` podle svého plánu reportování.

### Okrajové případy, na které je třeba myslet

| Situace | Na co si dát pozor | Řešení |
|-----------|-------------------|-----|
| Kontingenční tabulka používá externí zdroj dat | Cache může odkazovat na spojení, které na novém počítači neexistuje | Vložte zdrojová data nebo znovu vytvořte spojení v cílovém sešitu |
| Velmi velká kontingenční tabulka ( > 100 k řádků ) | `CopyRows` může být náročná na paměť | Používejte `CopyRows` po částech nebo zvažte `Copy` s `PasteOptions` pro omezení využití paměti |
| List má skryté řádky/sloupce | Skryté řádky cache mohou být přeskočeny, pokud kopírujete jen viditelné řádky | Vždy kopírujte přesnou oblast řádků, která obsahuje cache, ne jen viditelnou část |

## Kompletní funkční příklad

Spojením všech částí získáte samostatný program, který můžete vložit do konzolové aplikace.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Spusťte program, otevřete `destination.xlsx` a uvidíte stejnou kontingenční tabulku připravenou k analýze vašich dat. Žádná ruční rekonstrukce není potřeba.

---

## Závěr

Ukázali jsme, jak **vytvořit nový sešit** v C# a **zkopírovat kontingenční tabulku**, přičemž zachováme všechna nastavení. Použitím `CopyRows` získáte spolehlivý způsob, jak **zachovat funkčnost kontingenční tabulky**, odpovědět na starou otázku „**jak zkopírovat řádky**“ a dokonce **duplikovat kontingenční tabulku** napříč více reporty s minimálním kódem.

Další kroky? Zkuste rozšířit zkopírovanou oblast o grafy, které odkazují na stejnou kontingenční tabulku, nebo experimentujte s `PasteOptions` pro přesné zachování formátování. Stejný vzor funguje i pro jiné objekty Aspose.Cells, jako jsou tabulky a pojmenované oblasti, takže můžete rozšířit jeho využití.

Máte nějaký specifický problém — například kontingenční tabulku, která čerpá data z externí DB, nebo sešit uložený v cloudu? Zanechte komentář níže a společně to vyřešíme. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}