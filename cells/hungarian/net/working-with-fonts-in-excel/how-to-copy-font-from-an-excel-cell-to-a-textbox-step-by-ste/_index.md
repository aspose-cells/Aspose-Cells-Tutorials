---
category: general
date: 2026-02-15
description: Hogyan másoljuk a betűtípust és alkalmazzuk a cellastílust C#-ban egy
  egyszerű példával. Tanulja meg, hogyan szerezze meg a cellastílust, és használja
  a cellaformázást a szövegmező betűméretének beállításához.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: hu
og_description: hogyan másoljuk a betűtípust egy munkalap cellájából, és alkalmazzuk
  a cellastílust egy szövegdobozra. Ez az útmutató bemutatja, hogyan lehet lekérni
  a cellastílust, használni a cellaformázást, és beállítani a szövegdoboz betűméretét.
og_title: Hogyan másoljunk betűtípust egy Excel cellából – Teljes C# oktatóanyag
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: hogyan másoljuk a betűtípust egy Excel cellából egy szövegdobozba – lépésről‑lépésre
  útmutató
url: /hu/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan másoljuk a betűtípust egy Excel cellából egy TextBoxba – Teljes C# útmutató

Valaha is szükséged volt **copy font**-ra egy táblázat cellájából, és arra, hogy egy UI szövegdoboz pontosan ugyanúgy nézzen ki? Nem vagy egyedül. Sok jelentéskészítő eszközben vagy egyedi műszerfalakon előfordul, hogy adatot húzol ki Excelből, majd megpróbálod megőrizni a vizuális hűséget – a betűcsaládot, méretet és színt – változatlanul.  

A jó hír, hogy néhány C# sorral **get cell style**-t tudsz elérni, beolvasni a betűtípus tulajdonságait, és **apply cell style**-t bármely text‑box vezérlőre alkalmazni. Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely megmutatja, hogyan **use cell formatting**-t és akár **set textbox font size**-t programozottan.

---

## Amit megtanulsz

- Hogyan lehet lekérni egy `TextBox` objektumot egy rács komponensből (`gridJs` a példánkban)  
- Hogyan olvasható ki a betűcsalád, méret és szín egy adott Excel cellából (`B2`)  
- Hogyan másolhatók ezek a betűtípus attribútumok a szövegdobozba, hogy a UI tükrözze a táblázatot  
- Gyakori buktatók (pl. színkonverzió) és néhány **pro tip**, amely a kódod robusztusságát növeli  
- Egy kész‑futtatható kódrészlet, amelyet beilleszthetsz egy konzol‑alkalmazásba vagy WinForms projektbe  

**Prerequisites**  
Meg kell, hogy legyen:

1. .NET 6+ (vagy .NET Framework 4.8) telepítve  
2. Az EPPlus NuGet csomag (Excel kezeléshez)  
3. Egy rácsvezérlő, amely egy `TextBoxes` szótárat exponál (a példa egy fiktív `gridJs`-t használ, de az elv bármely UI könyvtárral működik)

Most pedig vágjunk bele.

---

## 1. lépés: A projekt beállítása és a munkalap betöltése

Először hozz létre egy új konzol vagy WinForms projektet, és add hozzá az EPPlus csomagot:

```bash
dotnet add package EPPlus --version 6.*
```

Ezután töltsd be a munkafüzetet, és szerezd meg azt a cellát, amelynek a stílusát másolni szeretnéd.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Miért fontos:** Az EPPlus közvetlen hozzáférést biztosít a `Style` objektumhoz, amely a `Font` alobjektumot tartalmazza. Innen kiolvashatod a `Name`, `Size` és `Color` értékeket. Ez a **get cell style** művelet magja.

---

## 2. lépés: A cél TextBox lekérése a rácsból

Feltételezve, hogy a UI rácsod (`gridJs`) a szövegdobozokat egy oszlopnév szerint kulcsként tároló szótárban tárolja, a kívánt elemet így kérheted le:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Ha WinForms-t használsz, a `notesTextBox` egy `TextBox` vezérlő lehet; WPF-ben egy `TextBox` elem, web‑alapú rácsnál pedig egy JavaScript interop objektum. A lényeg, hogy legyen egy hivatkozásod, amit manipulálhatsz.

---

## 3. lépés: A betűcsalád átvitele

Most, hogy megvan a forrás stílus és a célvezérlő is, másold át a betűcsaládot.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Nem minden UI keretrendszer rendelkezik `FontFamily` tulajdonsággal, amely egyszerű karakterláncot fogad. WinForms‑ban például így állítanád be: `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Igazítsd a saját környezetedhez.

---

## 4. lépés: A betűméret átvitele

A betűméret EPPlus‑ban `float` típusú. Alkalmazd közvetlenül:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Ha a vezérlőd pontokban (pt) dolgozik (ami a legtöbb esetben így van), a konverzió nélkül is beállítható. CSS‑alapú rácsoknál esetleg a `"pt"` kiegészítést kell hozzáadni.

---

## 5. lépés: A betűszín átvitele

A színkonverzió a legbonyolultabb rész, mivel az EPPlus a színeket ARGB egész számokként tárolja, míg sok UI keretrendszer `System.Drawing.Color`‑t vagy CSS hex stringet vár.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Miért működik:** A `GetColor()` feloldja a téma‑alapú színeket, és konkrét `System.Drawing.Color`‑t ad vissza. Ha a cella az alapértelmezett színt használja (nincs explicit beállítás), alapértelmezettként feketét adunk, hogy elkerüljük a null referencia hibákat.

---

## Teljes működő példa

Mindent összegezve, itt egy minimális konzolalkalmazás, amely beolvas egy Excel fájlt, kinyeri a **B2** betűtípusát, és egy mock szövegdobozra alkalmazza.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Várt kimenet (feltételezve, hogy B2 Arial, 12 pt, kék):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Futtasd a programot, nyisd meg a UI‑t, és láthatod, hogy a „Notes” szövegdoboz most már pontosan tükrözi a **B2** cella betűstílusát. Nincs szükség kézi beállításra.

---

## Gyakran ismételt kérdések és széljegyek

### Mi van, ha a cella egy téma‑színt használ az explicit RGB érték helyett?

Az EPPlus `GetColor()` automatikusan feloldja a téma‑színeket egy konkrét `System.Drawing.Color`‑ra. Ha egy régebbi könyvtárat használsz, amely csak a téma‑indexet adja vissza, neked kell a saját színpalettáddal leképezni azt az indexet.

### Másolhatok más stílusattribútumokat (pl. félkövér, dőlt)?

Természetesen. Az `ExcelStyle.Font` objektum továbbá tartalmazza a `Bold`, `Italic`, `Underline` és `Strike` tulajdonságokat. Egyszerűen állítsd be a megfelelő UI‑vezérlő tulajdonságait:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Mi van, ha a rácsvezérlő nem rendelkezik `FontColor` tulajdonsággal?

A legtöbb modern UI keretrendszer igen, de ha csak CSS‑stringet fogad, konvertáld a `Color`‑t hex formátumba:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Hogyan kezeljek egyszerre több cellát?

Iterálj a kívánt tartományon, minden cellához kérd le a stílust, és alkalmazd a megfelelő szövegdobozra. Nagy mennyiségű sor feldolgozásakor cache‑eld a stílusobjektumokat a teljesítmény érdekében.

---

## Pro tippek és gyakori buktatók

- **Cache‑eld az ExcelPackage‑t** – a fájl minden cellához való újra‑megnyitása drága. Töltsd be egyszer a munkafüzetet, majd használd újra az `ExcelWorksheet` objektumot.  
- **Figyelj a null színekre** – egy alapértelmezett színt örökölő cella `null`‑t ad vissza. Mindig biztosíts tartalékot (fekete vagy a vezérlő alapértelmezettje).  
- **DPI‑skálázás** – magas DPI‑monitorok esetén a betűméretek kissé nagyobbnak tűnhetnek. Szükség esetén állítsd a `Graphics.DpiX`‑et.  
- **Szálbiztonság** – az EPPlus nem szálbiztos. Ha több munkalapot dolgozol párhuzamosan, minden szálnak külön `ExcelPackage`‑t hozz létre.

---

## Összegzés

Most már tudod, **hogyan másold a betűtípust** egy Excel cellából, és **hogyan alkalmazd a cella stílusát** bármely szövegdoboz‑vezérlőre C#‑ban. A cella `Style`‑jának lekérdezésével, a `Font` tulajdonságok kinyerésével és azok UI‑elemekhez való hozzárendelésével vizuális konzisztenciát érhetsz el manuális másolás nélkül.  

A teljes megoldás – a munkafüzet betöltése, a cella stílus lekérése, majd a textbox betűcsaládjának, méretének és színének beállítása – lefedi a **use cell formatting** alapjait, és bemutatja, hogyan **set textbox font size**‑t helyesen állítsuk be.  

Most próbáld meg kiterjeszteni a példát háttérszínek, szegélyek vagy akár a cella teljes tartalmának másolására. Ha egy olyan adat‑rácskönyvtárral dolgozol, amely támogatja a gazdag cella‑renderelést, már most be tudod táplálni a pontosan ugyanazt a stílusinformációt, amit az Excel‑ből nyertél, így UI‑d és jelentéseid tökéletesen szinkronban lesznek.

Van még kérdésed? Hagyj kommentet, vagy nézd meg a kapcsolódó témákat, például a „dinamikus Excel‑to‑UI binding” és a „téma‑érzékeny színkonverzió” cikkeket. Boldog kódolást!

---

![betűtípus másolás példája](placeholder-image.jpg "betűtípust másolni Excel cellából TextBoxba")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}