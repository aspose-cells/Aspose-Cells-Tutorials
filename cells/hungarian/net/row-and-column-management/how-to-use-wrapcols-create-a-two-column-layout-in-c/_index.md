---
category: general
date: 2026-02-15
description: Hogyan használjuk a WRAPCOLS‑t kétoszlopos elrendezés létrehozásához,
  képlet hozzáadásához és sorozat tömb generálásához C# munkalapokon – lépésről‑lépésre
  útmutató.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: hu
og_description: Hogyan használjuk a WRAPCOLS-t kétoszlopos elrendezés létrehozásához,
  képletek hozzáadásához és sorozattömb generálásához egy C# munkalapon – teljes útmutató.
og_title: 'Hogyan használjuk a WRAPCOLS-t: Kétoszlopos elrendezés C#‑ban'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'A WRAPCOLS használata: Kétoszlopos elrendezés létrehozása C#‑ban'
url: /hu/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a WRAPCOLS‑t: Kétoszlopos elrendezés létrehozása C#‑ban

Valaha is elgondolkodtál **hogyan használjuk a WRAPCOLS‑t**, amikor gyors kétoszlopos nézetre van szükséged egy Excel‑stílusú munkalapon? Nem vagy egyedül. Sok fejlesztő elakad, amikor megpróbálja egy generált listát szép oszlopokra bontani anélkül, hogy minden cellához ciklust írna. A jó hír? A `WRAPCOLS` függvénnyel egyetlen képletet helyezhetsz el az `A1`‑ben, és hagyhatod, hogy az Excel (vagy egy kompatibilis motor) elvégezze a nehéz munkát.

Ebben az útmutatóban végigvezetünk **hogyan adjunk képletet**, amely **kétoszlopos elrendezést hoz létre**, megmutatjuk **hogyan hozzunk létre oszlopokat** dinamikusan, és még **szekvencia tömb** értékeket is generálunk menet közben. A végére egy teljesen futtatható C# kódrészletet kapsz, amelyet beilleszthetsz a projektedbe, futtathatsz, és azonnal megjelenik egy rendezett kétoszlopos blokk.

## Amit megtanulsz

- A `WRAPCOLS` célja és miért jobb alternatíva a kézi ciklusoknál.  
- **Hogyan adjunk képletet** egy munkalap cellájához C#‑ban.  
- Hogyan generáljunk szekvencia tömböt a `SEQUENCE`‑el, és adjuk át a `WRAPCOLS`‑nek.  
- Tippek a munkalap újraszámításához, hogy a képlet azonnal feloldódjon.  
- Szélső esetek kezelése (pl. üres munkalapok, egyedi oszlopszámok).

Nem szükséges külső könyvtár a standard Excel‑feldolgozó csomagon kívül – a példában **ClosedXML**‑t használunk egyszerű API‑jával, de a koncepciók alkalmazhatók EPPlus, SpreadsheetGear vagy akár a Google Sheets API‑jával is.

---

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core‑on és .NET Framework‑ön is lefordul).  
- Hivatkozás a **ClosedXML**‑re (`dotnet add package ClosedXML`).  
- Alapvető C# ismeretek – kényelmesen kell tudnod `using` utasításokat és objektum‑inicializálást használni.  

Ha már nyitott egy munkafüzet, kihagyhatod a fájl‑létrehozási részt, és egyenesen a képlet szakaszra ugorhatsz.

---

## 1. lépés: A munkalap előkészítése (Hogyan hozzunk létre oszlopokat)

Először szükségünk van egy `Worksheet` objektumra. ClosedXML‑ben egy `XLWorkbook`‑ból kapjuk meg. Az alábbi kódrészlet egy új munkafüzetet hoz létre, egy *Demo* nevű lapot ad hozzá, és egy `worksheet` nevű változóba menti a hivatkozást a tisztább kód érdekében.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Miért nevezünk át?**  
> A változó nevének rövidnek (`worksheet`) tartása megkönnyíti a későbbi kód olvasását, különösen több művelet láncolásakor. Emellett tükrözi a legtöbb dokumentációban látható elnevezési stílust, csökkentve a kognitív terhet.

---

## 2. lépés: A képlet írása (Hogyan adjunk képletet + szekvencia tömb generálása)

Most jön a varázslatos sor. Egy képletet helyezünk el az **A1** cellában, amely két dolgot csinál:

1. **Szekvencia tömböt generál** hat számra (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Az számokat két oszlopba csomagolja** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Mi történik?**  
> `SEQUENCE(6)` egy függőleges tömböt hoz létre `{1;2;3;4;5;6}`. A `WRAPCOLS` ezt a tömböt a megadott oszlopszámra „csomagolja” – ebben az esetben **2**. Az eredmény egy 3‑soros × 2‑oszlopos blokk, amely így néz ki:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Ha a második argumentumot **3**‑ra változtatod, háromoszlopos elrendezést kapsz. Ez a **hogyan hozzunk létre oszlopokat** lényege anélkül, hogy kézi ciklusokat írnál.

---

## 3. lépés: A munkalap újraszámítása (A képlet kiértékelésének biztosítása)

A ClosedXML nem értékeli ki automatikusan a képleteket, amikor beírod őket. Hívnod kell a `Calculate()`‑t a munkafüzeten (vagy a konkrét munkalapon), hogy kényszerítsd a kiértékelést.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro tipp:** Nagy munkafüzetek esetén csak azokon a lapokon hívd meg a `Calculate()`‑t, amelyek ténylegesen változtak. Ez memóriát takarít meg és felgyorsítja a feldolgozást.

Amikor megnyitod a `WrapColsDemo.xlsx`‑t, a kétoszlopos elrendezés rendezett módon megjelenik az **A1:B3** tartományban. Nem volt szükség további kódra a sorok vagy oszlopok bejárásához – a `WRAPCOLS` mindent elintézett.

---

## 4. lépés: Az eredmény ellenőrzése (Mit várhatsz)

A program futtatása után nyisd meg a generált fájlt. A következőt kell látnod:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Ha a számok függőlegesen (azaz csak az A oszlopban) jelennek meg, ellenőrizd, hogy a `worksheet.Calculate()`‑t **a képlet beállítása után** hívtad‑e. Néhány motorhoz szükséges a `workbook.Calculate()` is; a fenti kódrészlet a ClosedXML beépített értékelőjével működik.

---

## Gyakori variációk és szélső esetek

### Az oszlopszám módosítása

**Kétoszlopos elrendezés** más sorok számával egyszerűen a `SEQUENCE` méretét vagy a `WRAPCOLS` második argumentumát állítva érheted el:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Ez egy 4‑soros × 3‑oszlopos blokkot (12 számot három oszlopra osztva) hoz létre.

### Dinamikus oszlopszám használata

Ha az oszlopszám egy változóból származik, szúrj be string interpolációval:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Most már **hogyan adjunk képletet**, amely futásidőben alkalmazkodik.

### Üres munkalapok

Ha a munkalap üres, a `Calculate()` továbbra is működik – a képlet az A1‑től kezdve tölti ki a cellákat. Azonban ha később törölsz sorokat/oszlopokat, amelyek átfedésben vannak a kimeneti tartománnyal, `#REF!` hibákat kaphatsz. Ennek elkerülése érdekében először töröld a célterületet:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Kompatibilitás

A `WRAPCOLS` és a `SEQUENCE` az Excel **Dinamikus Tömb** függvényei, amelyek az Office 365‑ben jelentek meg. Régebbi Excel‑verziók esetén ezek a függvények nem léteznek, és manuális ciklusra lesz szükség. A ClosedXML értékelője a legújabb Excel viselkedését tükrözi, így biztonságosan használható modern környezetekben.

---

## Teljes működő példa (Másolás‑beillesztés kész)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Várt eredmény:** A *WrapColsDemo.xlsx* megnyitásakor egy rendezett kétoszlopos elrendezést látsz, ahol az 1‑6 számok a korábban leírt módon vannak elrendezve.

---

## Összegzés

Áttekintettük, **hogyan használjuk a WRAPCOLS‑t** egy **kétoszlopos elrendezés** létrehozásához, bemutattuk, **hogyan adjunk képletet** programozottan, és láttuk, hogy a `SEQUENCE` segítségével **szekvencia tömböt** generálhatunk ciklus nélkül. Az Excel dinamikus tömb függvényeinek C#‑beli kihasználásával a kódod tömör, olvasható és karbantartható marad.

A következő lépések lehetnek:

- **Dinamikus sorok** létrehozása a `ROWS` vagy `COUNTA` segítségével.  
- **A kimenet formázása** (szegélyek, számformátumok) a ClosedXML stílus API‑jával.  
- **CSV‑be exportálás** az elrendezés felépítése után, további feldolgozáshoz.

Próbáld ki, változtasd meg az oszlopszámot, és nézd meg, milyen gyorsan tudsz összetett táblázatokat prototípusolni. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}