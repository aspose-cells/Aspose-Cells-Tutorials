---
category: general
date: 2026-02-21
description: Készítsen cellastílust C#-ban gyorsan. Tanulja meg, hogyan alkalmazzon
  stílust egy cellára, középre helyezze a szöveget a cellában, állítsa be a cella
  igazítását, és sajátítsa el a cella formázását.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: hu
og_description: Hozzon létre cellastílust C#‑ban, és tanulja meg, hogyan alkalmazzon
  stílust egy cellára, középre helyezze a szöveget a cellában, valamint állítsa be
  a cella igazítását egy világos, lépésről‑lépésre útmutatóval.
og_title: Cellastílus létrehozása C#‑ban – Stílus alkalmazása egy cellára és a szöveg
  középre igazítása
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cellastílus létrehozása C#‑ban – Hogyan alkalmazz stílust egy cellára és középre
  igazítsd a szöveget
url: /hu/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cellastílus létrehozása C#‑ban – Teljes útmutató a stílusok alkalmazásához és a szöveg középre helyezéséhez

Valaha szükséged volt már **create cell style** létrehozására egy Excel munkalapon, de nem tudtad, hol kezdj? Nem vagy egyedül. Sok automatizálási projektben a **apply style to cell** objektumok alkalmazásának képessége a közönséges táblázat és a kifinomult jelentés közötti különbség.

Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely megmutatja, hogyan **how to center text** egy cellán belül, beállítja az igazítást, és hozzáad egy vékony szegélyt – mindezt csak néhány C#‑os sorban. A végére pontosan tudni fogod, miért fontos minden rész, és hogyan finomíthatod a saját eseteidhez.

## Amit elsajátítasz

- A **create cell style** munkafolyamat világos megértése az Aspose.Cells (vagy bármely hasonló könyvtár) használatával.
- A pontos kód, amelyet beilleszthetsz egy konzolalkalmazásba a **apply style to cell** elvégzéséhez.
- Rálátás a **center text in cell**, **set cell alignment** műveletekre, valamint a széljegyek kezelése, mint például az egyesített cellák vagy egyedi számformátumok.
- Tippek a stílus kiterjesztéséhez – különböző betűtípusok, háttérszínek vagy feltételes formázás.

> **Prerequisite:** Visual Studio 2022 (vagy bármely C# IDE) és az Aspose.Cells for .NET NuGet csomag. Egyéb függőségek nem szükségesek.

## 1. lépés: A projekt beállítása és a névterek importálása

Mielőtt **create cell style**-t tudnánk, szükségünk van egy olyan projektre, amely hivatkozik az Excel könyvtárra.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Miért fontos ez:* Az `Aspose.Cells` importálása hozzáférést biztosít a `Workbook`, `Worksheet`, `Style` és `Border` osztályokhoz. Ha más könyvtárat használsz (pl. EPPlus), az osztálynevek változnak, de a koncepció ugyanaz marad.

## 2. lépés: Workbook létrehozása és az első cella lekérése

Most **create cell style**-t hajtunk végre, először a formázni kívánt cellára hivatkozást lekérve.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Vedd észre, hogy a `Cell`-t használtuk a generikus `var` helyett – az explicit típusmegadás átláthatóbbá teszi a kódot a kezdők számára. A `PutValue` hívás egy karakterláncot ír, így később láthatjuk a stílus hatását.

## 3. lépés: A stílus meghatározása – Szöveg középre helyezése, vékony szegély hozzáadása

Itt van a **create cell style** művelet szíve. Beállítjuk a vízszintes igazítást, egy vékony szegélyt, és néhány opcionális finomságot.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Miért csináljuk ezt:*  
- **HorizontalAlignment** és **VerticalAlignment** együtt válaszolják a “**how to center text** a cellában?” kérdést.  
- Az összes négy szegély hozzáadása biztosítja, hogy a cella doboz címkeként jelenjen meg, ami a fejlécekhez hasznos.  
- A háttérszín nem kötelező, de bemutatja, hogyan bővítheted a stílust később.

## 4. lépés: A meghatározott stílus alkalmazása a kiválasztott cellára

Most, hogy a stílus létezik, egyetlen metódushívással **apply style to cell**-t hajtunk végre.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Ennyi—az Aspose.Cells gondoskodik a stílus másolásáról a cella belső stílusgyűjteményébe. Ha ugyanazt a formázást egy tartományra is szükséged van, használhatod a `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` kifejezést.

## 5. lépés: A Workbook mentése és az eredmény ellenőrzése

Egy gyors mentés lehetővé teszi, hogy megnyisd a fájlt Excelben, és megerősítsd, hogy a szöveg valóban középre van igazítva, és a szegély megjelenik.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Expected output:* Amikor megnyitod a **StyledCell.xlsx** fájlt, az **A1** cella tartalmazza a “Hello, styled world!” szöveget, amely vízszintesen és függőlegesen egyaránt középre van igazítva, egy vékony szürke szegéllyel körülvéve, és egy világosszürke háttérrel.

## Gyakori variációk és széljegyek

### 1. Szöveg középre helyezése egy egyesített tartományban

Ha egyesíted a **A1:C1** cellákat, és továbbra is középre szeretnéd a szöveget, a stílust az egyesítés **után** a bal‑felső cellára kell alkalmazni:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Numerikus formátum használata

Néha szükség van a **set cell alignment** *és* a számok egy adott formátummal való megjelenítésére:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Az igazítás középre marad, míg a szám `12,345.68` formában jelenik meg.

### 3. Stílusok hatékony újrahasználata

Új `Style` létrehozása minden cellához ronthatja a teljesítményt. Ehelyett hozz létre egy stílusobjektumot, és használd újra sok cellán vagy tartományon. A `StyleFlag` osztály lehetővé teszi, hogy csak a szükséges részeket alkalmazd, ezzel memóriát takarítva meg.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

## Pro tippek és figyelni való buktatók

- **Don’t forget vertical alignment** – csak vízszintesen középre helyezni gyakran hibásan néz ki, különösen a magasabb soroknál.  
- **Border types**: `CellBorderType.Thin` a legtöbb jelentésnél működik, de a vizuális hierarchiához válthatsz `Medium` vagy `Dashed` típusra.  
- **Color handling**: .NET Core célzásakor használd a `System.Drawing.Color`-t a `System.Drawing.Common` csomagból; egyébként futásidejű hibát kapsz.  
- **Saving format**: Ha régebbi Excel verziókkal való kompatibilitásra van szükséged, változtasd a `SaveFormat.Xlsx`-t `SaveFormat.Xls`-re.

![Cellastílus példa](https://example.com/images/create-cell-style.png "Cellastílus C#‑ban")

*Alt text: képernyőkép, amely egy középre igazított szöveggel és vékony szegéllyel rendelkező cellát mutat, amelyet a create cell style útmutató hozott létre.*

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Futtasd ezt a programot, nyisd meg a **StyledCell.xlsx** fájlt, és láthatod a korábban leírt pontos eredményt. Nyugodtan módosítsd a szöveget, a szegély stílusát vagy a háttérszínt, hogy illeszkedjen a márkádhoz.

## Következtetés

Most **created cell style**-t hoztunk létre a semmiből, **apply style to cell**-t alkalmaztuk, és bemutattuk, hogyan **how to center text** vízszintesen és függőlegesen. Ezeknek az építőelemeknek a elsajátításával most már formázhatsz fejléceket, kiemelheted az összegeket, vagy építhetsz teljes jelentés sablonokat anélkül, hogy elhagynád a C#-ot.

Ha kíváncsi vagy a következő lépésekre, próbáld ki:

- **Ugyanazon stílus alkalmazása egy teljes sorra** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Feltételes formázás hozzáadása** a háttér megváltoztatásához a cellaértékek alapján.
- **Exportálás PDF‑be** a stílus megőrzése mellett.

Ne feledd, a formázás ugyanolyan mértékben a olvashatóságról szól, mint az esztétikáról. Kísérletezz, iterálj, és hamarosan a táblázataid olyan professzionálisak lesznek, mint a kódod.

*Boldog kódolást!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}