---
category: general
date: 2026-03-18
description: Pivot tábla másolása C#-ban az Aspose.Cells segítségével. Tanulja meg,
  hogyan másolhat Excel-tartományt, duplikálhat Excel-pivotot, másolhat tartományt
  új munkalapra, és másolhat pivotot munkalapra percek alatt.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: hu
og_description: Pivot tábla másolása C#-ban az Aspose.Cells használatával. Tanulja
  meg, hogyan duplikálja az Excel pivotot, hogyan másolja az Excel tartományt egy
  új helyre, és hogyan másolja a pivotot egy munkalapra, teljes kódrészletekkel.
og_title: Pivot tábla másolása C#‑ban – Teljes programozási útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Pivot tábla másolása C#‑ban – Lépésről lépésre útmutató
url: /hu/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla másolása C#‑ban – Teljes programozási útmutató

Volt már, hogy **pivot táblát** kellett másolni egy munkafüzet egyik részéről a másikra, de nem tudtad, hogyan tegyed ezt meg anélkül, hogy elveszítenéd a mögöttes adatkapcsolatokat? Nem vagy egyedül. Sok fejlesztő szembesül ezzel a problémával Excel jelentések automatizálásakor, különösen akkor, amikor a pivot egy nagyobb adatblokk része. A jó hír? Az Aspose.Cells segítségével a pivot táblát **pontosan úgy** másolhatod, ahogy megjelenik, és megtanulod, hogyan **excel tartományt másolj**, **excel pivotot duplikálj**, sőt, hogyan **pivotot másolj munkalapra** néhány C#‑sorral.

Ebben a tutorialban egy valós példán keresztül mutatjuk be: egy *A1:J20* tartományban lévő pivot áthelyezése egy új *M1:V20* területre ugyanazon a munkalapon. A végére egy futtatható programmal, a lépések jelentőségével és a kód más tartományokra vagy külön munkalapokra való adaptálásával fogsz rendelkezni. Nincs szükség külső dokumentumokra – minden itt van.

---

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következőkkel rendelkezel:

- **Aspose.Cells for .NET** (23.9 vagy újabb verzió). NuGet‑en keresztül telepíthető: `Install-Package Aspose.Cells`.
- Alap C# fejlesztői környezet (Visual Studio 2022, Rider vagy VS Code a C# kiegészítővel).
- Egy Excel fájl (`source.xlsx`), amelyben a pivot tábla az *A1:J20* tartományban található.

Ennyi. Ha tudsz konzolos alkalmazást létrehozni, már készen állsz.

---

## Hogyan másolj pivot táblát az Aspose.Cells‑ben

A megoldás lényege egyetlen hívás a `Worksheet.Cells.CopyRange` metódusra. Ez a metódus nem csak a nyers cellaértékeket másolja, hanem automatikusan megőrzi a pivot táblákat, diagramokat és egyéb gazdag objektumokat is. Nézzük meg lépésről lépésre.

### 1. lépés: A forrás munkafüzet betöltése

Először be kell tölteni a munkafüzetet a memóriába.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Miért fontos:** A munkafüzet betöltése egy memóriabeli reprezentációt hoz létre, amelyet az Aspose.Cells Excel indítása nélkül manipulálhat. Gyors, szálbiztos, és szervereken is működik.

### 2. lépés: Az első munkalap lekérése

A legtöbb példa az első lapot használja, de bármely indexet vagy nevet megcélozhatsz.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tipp:** Ha **pivotot szeretnél másolni munkalapra** a jelenlegi helyett, egyszerűen cseréld ki a `worksheet` hivatkozást egy másik `Worksheet` objektumra.

### 3. lépés: A forrás és a cél tartományok definiálása

A `CellArea` struktúrákat fogjuk használni a mozgatandó blokkok leírására.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Magyarázat:** A sor- és oszlopindexek nullától indulnak. 0‑s oszlop = **A**, 12‑s oszlop = **M**, stb. Igazítsd ezeket a számokat, ha a pivot máshol helyezkedik el.

### 4. lépés: A másolási művelet végrehajtása

Most jön a varázslat. Az utolsó logikai paraméter `true`‑ra állítása azt mondja az Aspose.Cells‑nek, hogy másolja az összes objektumot – beleértve a pivotot is.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Miért `true`?** A jelző azt jelzi, hogy „minden objektumot másoljon”. Ha `false`‑ra állítod, csak a sima cellaértékek kerülnek átmásolásra, a pivot elveszik.

### 5. lépés: A munkafüzet mentése

Végül írjuk vissza a módosított munkafüzetet a lemezre.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Eredmény:** A `copy-pivot.xlsx` most már tartalmazza az eredeti pivotot az *A1:J20* tartományban **és** egy azonos másolatot az *M1:V20* tartományban. Nyisd meg a fájlt Excelben, hogy ellenőrizd, mindkét pivot működik és megtartja az adatkapcsolatait.

---

## Excel tartomány másolása új helyre – gyors variáció

Néha csak a **excel tartományt** kell másolni, a pivotok nélkül. Ugyanez a `CopyRange` metódus megteszi a dolgot; csak az utolsó argumentumot állítsd `false`‑ra.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Mikor használjuk:** Ha nyers adatot mozgatunk egy ideiglenes számítási lapra, az objektummásolás letiltása memóriát takarít meg és felgyorsítja a műveletet.

---

## Excel pivot duplikálása több munkalapon

Mi van, ha **excel pivotot szeretnél duplikálni** egy másik munkalapon? A minta ugyanaz; csak a cél `Worksheet`‑et kell megadni.

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

> **Szélhelyzet:** Ha a forrás pivot egy olyan táblát használ, amely az eredeti lapon él, az Aspose.Cells másolja a tábladefiníciót is, így az új pivot azonnal működni fog.

---

## Gyakori hibák és elkerülésük

| Hiba | Miért fordul elő | Megoldás |
|------|------------------|----------|
| **A pivot elveszíti a gyorsítótárát** | `CopyRange` `false`‑val vagy egy egyedi másolási rutin használata, amely figyelmen kívül hagyja az objektumokat. | Mindig `true`‑t adj meg, ha a pivotra is szükséged van. |
| **A célcellák már tartalmaznak adatot** | Csendes felülírás, ami meglévő képleteket romolhat. | Először töröld a célterületet: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **A forrás tartomány nem fedi le a teljes pivotot** | A pivot táblák több sort/oszlopot is lefednek, mint amire számítasz (pl. rejtett sorok). | Használd a `worksheet.PivotTables[0].DataRange`‑t a pontos határok programozott lekéréséhez. |
| **Másolás munkafüzetek között** | A `CopyRange` csak ugyanabban a munkafüzetben működik. | Használd a `sourceWorksheet.Cells.CopyRange`‑t egy ideiglenes tartományra, majd `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Várt kimenet és ellenőrzés

A program futtatása után:

1. Nyisd meg a `copy-pivot.xlsx` fájlt.
2. Két azonos pivot táblát látsz – egyet **A1:J20**, egyet **M1:V20** tartományban.
3. Frissíts bármely pivotot; mindkettőnek ugyanazt az adatot kell mutatnia.
4. Ha egy másik lapra duplikáltad, az új lap is tartalmaz egy működő másolatot.

Egy gyors ellenőrzés kóddal:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro tipp: Tartományok automatikus felismerése

A `CellArea` kézi megadása statikus jelentésekhez működik, de a termelési kódban gyakran szükség van a pivot dinamikus megtalálására.

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

> **Miért érdemes?** Ez a megoldás rugalmasabbá teszi a kódot a layout‑változásokkal szemben – többé nem lesz „Hoppá, a pivot B2‑re mozdult” hiba.

---

![copy pivot table example](copy-pivot.png){alt="pivot tábla másolása példája"}

*Az (helyőrző) képernyőképen látható az eredeti pivot bal oldalon, a duplikált pedig jobb oldalon.*

---

## Összefoglalás

Most már tudod, hogyan **másolj pivot táblát** C#‑ban az Aspose.Cells‑szel, megismerkedtél a **excel tartomány másolásával**, a **excel pivot duplikálásával**, sőt, a **pivot munkalapra másolásával** is. A legfontosabb tanulságok:

- Használd a `Worksheet.Cells.CopyRange`‑t a `true` jelzővel a gazdag objektumok megőrzéséhez.
- Definiáld a forrás és cél `CellArea` objektumokat nullától induló indexekkel.
- Állítsd be a cél munkalapot, ha **pivotot szeretnél másolni munkalapra**.
- Vedd figyelembe az olyan szélhelyzeteket, mint a meglévő adatok, rejtett sorok és a munkafüzetek közti másolás.

---

## Mi a következő?

- **Dinamikus pivot felfedezés**: Készíts egy segédfüggvényt, amely bejárja a munkafüzetet, megtalálja az összes pivotot és automatikusan replikálja őket.
- **Export PDF/HTML‑re**: Másolás után érdemes lehet a lapot jelentésformátumba renderelni – az Aspose.Cells ezt is támogatja.
- **Teljesítmény optimalizálás**: Nagy munkafüzeteknél fontold meg a számítás letiltását a másolás előtt, majd újbóli engedélyezését utána.

Kísérletezz nyugodtan: változtasd meg a célkoordinátákat, másolj egy teljesen új munkafüzetbe, vagy akár több munkalapon keresztül ciklusba foglald a másolást egy konszolidált jelentés létrehozásához. A lehetőségek végtelenek, és a most megszerzett alapokkal szinte bármilyen Excel‑automatizálási feladatot meg tudsz oldani.

Boldog kódolást, és legyenek a pivotjaid mindig tökéletesen szinkronban!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}