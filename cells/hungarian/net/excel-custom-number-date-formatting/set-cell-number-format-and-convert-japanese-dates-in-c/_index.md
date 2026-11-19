---
category: general
date: 2026-11-19
description: Állítsa be a cella számformátumát C#‑ban, és tanulja meg, hogyan alkalmazza
  az Excel dátumformátumot a japán korszak dátumaira, lehetővé téve a megbízható C#
  Excel dátumkonverziót.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: hu
lastmod: 2026-11-19
og_description: Állítsa be a cella számformátumát C#-ban, és alkalmazza az Excel dátumformátumot
  a japán korszak dátumaira. Kövesse ezt a teljes útmutatót a pontos C# Excel dátumkonverzióhoz.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Állítsa be a cella számformátumát és konvertálja a japán dátumokat C#‑ban
  – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Állítsa be a cella számformátumát, és konvertálja a japán dátumokat C#‑ban
url: /hu/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cellaszám formátum beállítása és japán dátumok konvertálása C#-ban

Ha egy C# Excel automatizálási projektben **cellaszám formátumot kell beállítania**, ez az útmutató megmutatja, hogyan **alkalmazzon Excel dátumformátumot**, és hogyan hajtson végre **C# Excel dátumkonvertálást** japán korszak dátumok esetén. Egy teljes, futtatható példát kap, amely a Reiwa‑korszak stringet (pl. `R3/04/01`) a gregorián `2021‑04‑01` dátummá alakítja.

## Mit fog megtanulni

* Hogyan hozzon létre egy munkafüzetet, és érje el az első munkalapját.  
* Hogyan **állítsa be a cella számformátumát**, hogy az Excel dátumként kezelje az értéket.  
* Hogyan **alkalmazzon Excel dátumformátumot**, amely felismeri a japán korszak stringeket.  
* Hogyan indítson el **C# Excel dátumkonvertálást** a képletek újraszámításával.  
* Várt kimenet és hibakeresési tippek szélhelyzetekhez.

**Előfeltételek**

* .NET 6 vagy újabb (a kód .NET Framework 4.6+‑tal is működik).  
* Aspose.Cells for .NET 2024 vagy újabb – telepítés NuGet‑en: `dotnet add package Aspose.Cells`.  
* Alapvető ismeretek C#‑ról és az Excel dátumkezelésről.

> **Pro tipp:** Az Aspose.Cells Microsoft Office telepítése nélkül is működik, így ideális szerver‑oldali automatizáláshoz.

## Cellaszám formátum beállítása Aspose.Cells‑szel C#‑ban

Az első lépés, hogy jelezzük az Excelnek, hogy a cella dátumot tartalmaz. Az Excel a dátumokat sorozatszámokként tárolja, ezért egy beépített dátum számformátumot (ID 14) kell alkalmaznunk a célcellára.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Miért működik ez

* `Style.Number = 14` az Excel *Rövid dátum* formátumához (alapértelmezés szerint `mm/dd/yyyy`) rendeli hozzá.  
* Ha a cella japán korszak stringet tartalmaz, például `R3/04/01`, az Aspose.Cells belső elemzője felismeri a korszakot, és a `CalculateFormula()` során a megfelelő gregorián sorozatszámra konvertálja.  
* A számítás után a `StringValue` a formázott gregorián dátumot adja vissza.

## Excel dátumformátum alkalmazása japán korszak dátumokhoz

Ha azt szeretné, hogy a cella a japán korszakot jelenítse meg a gregorián dátum helyett, használhat egy egyedi számformátumot, amely tartalmazza a korszakkódot. Ez bemutatja a **apply excel date format** képességet.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` kényszeríti a japán helyi beállítást.  
* `ggg` a korszak nevét jelöli (pl. `R` a Reiwa‑hez).  
* A szó szerinti karakterek (`年`, `月`, `日`) hozzáadása egy ismerős japán dátumelrendezést hoz létre.

### Mikor használjunk egyedi formátumot

* Japán közönségnek szánt jelentések.  
* Amikor a jogi dokumentumokban meg kell őrizni az eredeti korszakinformációt.  
* Ilyen műszerfalakon, ahol a gregorián és a korszak dátumok egymás mellett jelennek meg.

## C# Excel dátumkonvertálás – japán korszakok kezelése

A **c# excel date conversion** folyamat három logikai részre bontható:

1. **A korszak string elemzése** – az Aspose.Cells automatikusan felismeri a `R` (Reiwa), `H` (Heisei), `S` (Showa) stb. karaktereket.  
2. **Sorozatszámra konvertálás** – az Excel a dátumokat 1899‑12‑30 óta eltelt napok számaként tárolja.  
3. **A sorozatszám formázása** – akár beépített formátummal (ID 14), akár egyedi japán formátummal.

### Teljes vég‑végi példa

Az alábbi önálló program mind a gregorián, mind a korszak kimenetet egy futtatásban demonstrálja.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Várt konzolkimenet**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Szélhelyzetek és gyakori buktatók

| Helyzet                                 | Mire kell figyelni                                          | Javítás / Ajánlás                                                                                              |
|-----------------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| Üres vagy hibás korszak string          | A `PutValue` a szó szerinti szöveget tárolja; a konvertálás sikertelen | Érvényesítse a bemenetet reguláris kifejezéssel, mielőtt a cellába írná.                                        |
| Helyi beállítás eltérés                 | Az egyedi formátum nyugati számjegyeket jelenít meg japán karakterek helyett | Győződjön meg róla, hogy a `Custom` formátum tartalmazza a `[$-ja-JP]` részt, vagy állítsa be a `Workbook.Settings.CultureInfo`‑t `ja-JP`‑re. |
| A munkafüzet képleteket tartalmaz, amelyek a dátumcellára hivatkoznak | Az újraszámítás felülírhatja a képlet eredményeit | Hívja meg a `CalculateFormula`‑t **a** formázási lépések **után**, vagy használja a `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`‑t, ha a hibákat ki szeretné hagyni. |
| Régebbi Aspose.Cells verziók használata | A japán korszak támogatás csak a 2022 Q3‑as verziótól érhető el | Frissítsen a legújabb NuGet csomagra.                                                                            |

## A megoldás tesztelése

1. **Futtassa a programot** a Visual Studio‑ból vagy `dotnet run`‑nal.  
2. Ellenőrizze, hogy a konzol a gregorián `2021‑04‑01` dátumot és a korszak stringet `R3年04月01日` jeleníti meg.  
3. Nyissa meg a generált munkafüzetet (ha hozzáadja a `wb.Save("Demo.xlsx");` sort) a Microsoft Excel‑ben, hogy ugyanazt a formázást lássa a cellákban.

### Automatizálási tipp

Ha nagy mennyiségű korszak dátumot kell feldolgozni (pl. az A oszlopban sok japán dátum található), csomagolja a konvertálási logikát egy ciklusba:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Ez a megközelítés gyors és memóriahatékony **cellaszám formátum beállítási** műveletet biztosít.

## Összegzés

Most már tudja, hogyan **állítsa be a cella számformátumát** C#‑ban az Aspose.Cells segítségével, hogyan **alkalmazzon Excel dátumformátumot** japán korszak stringekhez, és hogyan hajtson végre megbízható **C# Excel dátumkonvertálást** a korszakból a gregorián dátumra. A teljes, futtatható kód mindkét kimenetet demonstrálja, és kiemeli a gyakori szélhelyzeteket.  

**Következő lépések**

* Fedezze fel a további beépített formátum ID‑kat


## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsék az API további funkcióinak elsajátítását és alternatív megvalósítási megközelítések felfedezését saját projektjeiben.

- [Excel dátumformátum beállítása C#-ban – Teljes lépésről‑lépésre útmutató](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Hogyan alkalmazz számformátumot Excelben az Aspose.Cells segítségével](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Hogyan alkalmazz egyedi számformátumot Excelben C#-ban](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}