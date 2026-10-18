---
category: general
date: 2026-06-08
description: Olvassa be a japán korszak dátumát C#‑ban az Aspose.Cells segítségével.
  Ismerje meg, hogyan teszi lehetővé a ja-JP CultureInfo és a japán korszak formátum
  a pontos Excel dátumkonverziót.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: hu
og_description: Gyorsan dolgozzon fel japán korszak dátumot C#-ban. Ez az útmutató
  bemutatja, hogyan alakítja a CultureInfo ja-JP és az Aspose.Cells a korszak karakterláncokat
  megfelelő DateTime objektumokká.
og_title: Japán korszak dátum feldolgozása C#-ban – Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Japán korszak dátumának feldolgozása C#‑ban az Aspose.Cells segítségével –
  Teljes útmutató
url: /hu/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán era dátum feldolgozása C#-ban az Aspose.Cells segítségével – Teljes útmutató

Valaha is szükséged volt **parse japanese era date** karakterláncok közvetlenül egy Excel‑lapból történő feldolgozására? Lehet, hogy egy örökölt rendszerből húzod az adatokat, amely még mindig a “令和3年5月12日” formátumot használja, és egy tiszta `DateTime`‑ra van szükséged a jelentésekhez. Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan alakíthatók ezek az era‑stílusú karakterláncok megfelelő C# dátumokká – találgatás nélkül.

A **Aspose.Cells**‑t fogjuk használni, a hatékony .NET könyvtárat az Excel manipulációhoz, együtt a **CultureInfo ja-JP** beállítással, amely tudja olvasni a japán era‑kat. A végére egy újrahasználható kódrészletet kapsz, amely kezeli a “令和”, “平成” és még a régebbi era‑kat is gond nélkül.

## Előkövetelmények

- .NET 6.0 vagy újabb (a kód .NET Framework 4.6+‑on is működik)  
- Aspose.Cells for .NET (letöltheted a ingyenes próba NuGet csomagot: `Install-Package Aspose.Cells`)  
- Alap C# ismeretek – semmi bonyolult, egy konzolos alkalmazás elegendő  
- A választott IDE (Visual Studio, Rider, VS Code, stb.)

Ennyi. Nincs extra szolgáltatás, nincs rejtélyes harmadik fél által biztosított parser.

## 1. lépés: A projekt beállítása és az Aspose.Cells hozzáadása

Először hozz létre egy új konzolos projektet:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Ezután nyisd meg a **Program.cs**‑t, és add hozzá a szükséges névtereket:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tipp:** Ha Visual Studio‑t használsz, az IDE automatikusan felajánlja a `using` nyilatkozatok hozzáadását, miután beírod az osztályneveket.

## 2. lépés: Munkafüzet létrehozása és a japán kultúra alkalmazása

A **parse japanese era date** helyes feldolgozásának kulcsa, hogy megmondjuk az Aspose.Cells‑nek, melyik kultúrát használja. A `CultureInfo` `ja-JP`‑re állítása aktiválja az era‑érzékeny feldolgozást.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Miért fontos ez? A japán naptár több era‑t tartalmaz (pl. *Reiwa* (令和), *Heisei* (平成)). A `CultureInfo` objektum egy `JapaneseCalendar`‑t tartalmaz, amely ismeri minden era kezdődátumát, így bármely, a japán era formátumot követő karakterlánc helyesen értelmezhető.

## 3. lépés: Japán era dátum karakterlánc írása egy cellába

Tegyük be egy minta era dátumot az **A1** cellába. Nyugodtan módosítsd a karakterláncot, hogy különböző era‑kat tesztelj.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Ha meglévő munkafüzetet szeretnél használni, betöltheted a `new Workbook("path/to/file.xlsx")`‑vel, és kihagyhatod a létrehozási lépést.

## 4. lépés: Az érték lekérése C# DateTime objektumként

Most jön a varázslat. A `GetDateTime()` hívásával az Aspose.Cells a korábban beállított `CultureInfo` alapján olvassa a cellát, és egy megfelelő `DateTime`‑t ad vissza.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Várható kimenet**

```
Parsed DateTime: 2021-05-12
```

Ez a teljes **parse japanese era date** folyamat – négy tömör kódsor.

## 5. lépés: Szélsőséges esetek és alternatív era‑k kezelése

A valós adatok nem mindig tiszták. Íme néhány szituáció, amellyel találkozhatsz, és hogyan kezelheted őket.

### 5.1 Érvénytelen vagy üres karakterláncok

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Régebbi era‑k (Showa, Taisho)

Ugyanez a `CultureInfo ja-JP` automatikusan működik a régebbi era‑k esetén is:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 `DateTime.ParseExact` használata szigorú validáláshoz

Ha a pontos japán era mintát szeretnéd kikényszeríteni, használj egy egyedi formátum karakterláncot:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Ez a megközelítés `FormatException`‑t dob, ha a karakterlánc eltér, ami hasznos lehet az adatminőség ellenőrzésénél.

## Teljes működő példa

Az alábbiakban a teljes programot találod, amelyet beilleszthetsz a **Program.cs**‑be és futtathatsz.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Futtasd a `dotnet run` paranccsal, és a következőt kell látnod:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

![Japán era dátum feldolgozási munkafolyamat – mutatja a munkafüzet létrehozását, a kultúra beállítását, a cella írását és a GetDateTime hívást](parse-japanese-era-date.png "Diagram, amely bemutatja, hogyan kell a japán era dátumot feldolgozni az Aspose.Cells és a CultureInfo ja-JP segítségével")

## Gyakran feltett kérdések megválaszolva

- **Működik ez .xlsx fájlokkal, amelyek már tartalmaznak era dátumokat?**  
  Igen. Amíg a munkafüzet `Settings.CultureInfo`‑ja `ja-JP`‑re van állítva *mielőtt* meghívod a `GetDateTime()`‑t, az Aspose.Cells helyesen értelmezi a meglévő karakterláncokat.

- **Mi a helyzet az időzónákkal?**  
  A feldolgozás egy `DateTime`‑t ad vissza `Kind = Unspecified` értékkel. Ha UTC‑t vagy helyi időt szeretnél, alkalmazd a `DateTime.SpecifyKind`‑t vagy konvertálj a feldolgozás után.

- **Több cellát is feldolgozhatok egyszerre?**  
  Természetesen. Iterálj a kívánt tartományon, és hívd meg a `GetDateTime()`‑t minden cellán – csak ne felejtsd el kezelni a hibákat a rosszul formázott bejegyzéseknél.

## Összegzés

Áttekintettük mindent, amire szükséged van a **parse japanese era date** karakterláncok C#‑ban történő feldolgozásához az Aspose.Cells és a beépített `CultureInfo ja-JP` használatával. A munkafüzet beállításától, az era‑formátumú karakterláncok írásán, a tiszta `DateTime` lekérésén át a szélsőséges esetek, például régi era‑k és szigorú validálás kezeléséig – ez az útmutató egy termelés‑kész megoldást nyújt.

Ezután érdemes lehet **Excel dátum konverziót** felfedezni numerikus sorozat dátumokhoz, vagy belemerülni a **C# DateTime parsing**‑be egyedi naptárakkal más helyi beállításokhoz. Ugyanez a minta működik a thai buddhista naptár, a héber naptár és mások esetén is – csak cseréld ki a `CultureInfo`‑t.

Van egy sajátos problémád? Írj egy megjegyzést, és együtt megoldjuk. Boldog kódolást!

## Mit érdemes legközelebb tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan valósíts meg dátumvalidációt .NET‑ben az Aspose.Cells használatával: Átfogó útmutató](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel dátumrendszer 1904‑re módosítása Aspose.Cells .NET‑tel](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Hatékony Excel‑PDF konvertálás egyedi dátumformátumokkal az Aspose.Cells for Java segítségével](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}