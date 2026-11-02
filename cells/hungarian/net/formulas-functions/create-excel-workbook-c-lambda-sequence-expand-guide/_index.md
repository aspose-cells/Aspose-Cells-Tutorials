---
category: general
date: 2026-03-30
description: Excel munkafüzet létrehozása C#-ban az Aspose.Cells használatával. Tanulja
  meg alkalmazni a lambda függvényt Excelben, a sequence függvényt Excelben, a tömb
  kibontását Excelben, és mentse a munkafüzetet xlsx formátumban.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: hu
og_description: Gyorsan hozzon létre Excel munkafüzetet C#-ban. Ez az útmutató bemutatja,
  hogyan használja a lambda függvényt Excelben, a sorozat függvényt Excelben, a tömb
  kibontását Excelben, és hogyan mentse a munkafüzetet xlsx formátumban.
og_title: Excel munkafüzet létrehozása C#-ban – Lambda, SEQUENCE és EXPAND útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel munkafüzet létrehozása C#-ban – Lambda, SEQUENCE és EXPAND útmutató
url: /hu/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása C#‑ban – Lambda, SEQUENCE és EXPAND útmutató

Valaha is szükséged volt **Excel munkafüzet C#‑ban** egy automatizált jelentéshez, de nem tudtad, melyik API‑hívásokat használd? Nem vagy egyedül – sok fejlesztő ugyanazzal a problémával szembesül, amikor először programozottan generál Excel‑t. Ebben az útmutatóban egy teljes, futtatható példát láthatsz, amely lefedi az új **SEQUENCE függvény Excel**-t, a hatékony **LAMBDA függvény Excel**-t, és még azt is, hogyan **expand array Excel** eredményeket.  

Megmutatjuk a pontos lépéseket is, hogyan **save workbook as xlsx**, hogy a fájlt átadhasd bárkinek, aki Excel‑t használ. A tutorial végére egy stabil, termelés‑kész kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz. Nincs homályos „lásd a dokumentációt” hivatkozás – csak olyan kód, ami ma működik.

## Amire szükséged lesz

- **.NET 6.0 vagy újabb** – a példa .NET 6‑ra céloz, de bármely friss verzió működik.  
- **Aspose.Cells for .NET** – telepítsd a NuGet‑en keresztül (`Install-Package Aspose.Cells`).  
- Alapvető C# szintaxis ismeret (változók, objektumok és lambda kifejezések).  
- Egy kedvedre való IDE (Visual Studio, Rider vagy VS Code).  

Ennyi. Nincs extra COM interop, nincs Office telepítve a szerveren – az Aspose.Cells mindent memóriában kezel.

## Excel munkafüzet létrehozása C#‑ban – Lépésről‑lépésre megvalósítás

Az alábbiakban a folyamatot kisebb, könnyen követhető lépésekre bontjuk. Minden lépésnek van egyértelmű címe, egy rövid kódrészlete, és magyarázata **miért** csináljuk így. Nyugodtan másold ki a teljes blokkot a végén, és futtasd konzolalkalmazásként.

### 1. lépés – Új munkafüzet inicializálása

Először is szükségünk van egy üres munkafüzet objektumra, amely a memóriában lévő Excel‑fájlt képviseli.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Miért fontos:* A `Workbook` az összes Aspose.Cells művelet belépési pontja. Az első `Worksheet` lekérésével kapunk egy vásznat, ahová képleteket, értékeket vagy formázást írhatunk.  

> **Pro tipp:** Ha több lapra van szükséged, egyszerűen hívd a `workbook.Worksheets.Add()`‑t, és tartsd meg a hivatkozást minden lapra.

### 2. lépés – SEQUENCE függvény Excel használata adatok generálásához

A **sequence function excel** dinamikus számtömböt hoz létre VBA nélkül. Az `A1` cellába helyezzük, és hagyjuk, hogy az Excel automatikusan kibővítse.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Miért fontos:* A `SEQUENCE(3)` `[1,2,3]` tömböt ad. Az `EXPAND`‑el kényszerítjük, hogy az eredmény egy 5 soros tartományba kerüljön, a felesleges sorok pedig üresek maradnak. Ez egyszerre mutatja be a **sequence function excel**‑t és a **expand array excel**‑t.

### 3. lépés – Számok aggregálása LAMBDA függvény Excel segítségével

Most mutassuk be a **lambda function excel** képességét. Az `REDUCE` függvényt használjuk, amely belsőleg egy lambda‑ra támaszkodik, hogy összegezzük az 1‑5 számokat.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Miért fontos:* A `REDUCE` végigiterál a `SEQUENCE(5)` által előállított tömbön, minden elemet (`b`) a lambda‑ba adva a felhalmozóval (`a`). A `a+b` lambda összeadja őket, így a `B1` cellában `15` lesz. Ez egy tiszta, csak képleteket használó módja a redukcióknak, anélkül, hogy C#‑ban ciklusokat írnánk.

### 4. lépés – Trigonometrikus függvények közvetlen alkalmazása cellákban

Az Excel beépített matematikai függvényei gyors számításokra alkalmasak. Egy kotangenset és egy hiperbolikus kotangenset helyezünk el szomszédos cellákban.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Miért fontos:* Bemutatja, hogy a klasszikus matematikai függvényeket keverheted az új dinamikus‑tömb képletekkel. Nincs szükség ezeknek az értékeknek a C#‑ban való kiszámítására, hacsak nem áll fenn speciális teljesítményigény.

### 5. lépés – Minden képlet kiszámítása

Az Aspose.Cells nem számolja ki automatikusan a képleteket, amikor beállítod őket. Kérned kell, hogy elvégezze a számítást.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Miért fontos:* Ez a hívás után minden cella `Value` tulajdonsága a kiértékelt eredményt tartalmazza, készen áll a mentésre vagy a visszaolvasásra.

### 6. lépés – Munkafüzet mentése Xlsx‑ként

Végül a **save workbook as xlsx** mintát használva mentjük a munkafüzetet a lemezre.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Miért fontos:* A `Save` metódus automatikusan felismeri a fájlkiterjesztést. A „.xlsx” használatával biztosítjuk, hogy a fájl kompatibilis legyen a modern Excel verziókkal. Az útvonal az asztalra mutat, hogy könnyen elérhető legyen a tesztelés során.

### Teljes működő példa

Az alábbi teljes programot beillesztheted egy új konzolprojektbe. Tartalmazza a fenti lépéseket, valamint egy kis ellenőrző blokkot, amely kiírja a számított értékeket a konzolra.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Várható kimenet a konzolon**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

És amikor megnyitod a *NewFunctions.xlsx* fájlt, ugyanazokat a számokat láthatod az első négy oszlopban.

![create excel workbook c# screenshot of the resulting spreadsheet](/images/create-excel-workbook-csharp.png)

## Széljegyek, tippek és gyakori kérdések

- **Mi van, ha több lapra van szükségem?**  
  Egyszerűen hívd a `workbook.Worksheets.Add()`‑t, és ismételd meg a képlet‑hozzárendeléseket minden új `Worksheet` objektumon.  

- **Használhatók-e régebbi Excel verziók?**  
  A dinamikus‑tömb függvények (`SEQUENCE`, `EXPAND`, `REDUCE`) Excel 365‑öt vagy Excel 2021‑et igényelnek. Régebbi verziók esetén maradj a klasszikus képleteknél, vagy számold ki az értékeket C#‑ban, mielőtt beírnád őket.  

- **Teljesítménybeli aggályok?**  
  Több ezer sor esetén a képletek egy tartományra való beállítása, majd a `CalculateFormula` meghívása általában gyorsabb, mint egyesével értékeket hozzárendelni.  

- **Mentés stream‑be fájl helyett?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}