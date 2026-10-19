---
category: general
date: 2026-07-13
description: Japán naptár konverzió C#-ban lépésről‑lépésre kóddal. Tanulja meg, hogyan
  lehet DateTime-ot kinyerni Excelből, és hatékonyan kezelni a japán érák dátumait.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- japanese calendar conversion
- extract datetime from excel
- excel date parsing c#
- aspnet excel cultureinfo
- japanese era date handling
language: hu
lastmod: 2026-07-13
og_description: A japán naptár átalakítása C#-ban részletesen. Tanulja meg, hogyan
  nyerjen ki DateTime értéket Excel cellákból, és hogyan konvertálja a japán korszakok
  sztringjeit gregorián dátumokká.
og_image_alt: Code screenshot illustrating Japanese calendar conversion in a C# console
  app
og_title: Japán naptár konverzió C#-ban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  headline: Japanese Calendar Conversion in C# – Full Guide
  type: TechArticle
- description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  name: Japanese Calendar Conversion in C# – Full Guide
  steps:
  - name: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
    text: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
  - name: Parses the year number relative to the era’s start.
    text: Parses the year number relative to the era’s start.
  - name: Constructs the corresponding Gregorian `DateTime`.
    text: Constructs the corresponding Gregorian `DateTime`.
  type: HowTo
tags:
- C#
- Excel
- DateTime
- Localization
title: Japán naptár átalakítása C#-ban – Teljes útmutató
url: /hu/net/excel-custom-number-date-formatting/japanese-calendar-conversion-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán naptár átalakítás C#-ban – Teljes útmutató

Volt már szükséged **japanese calendar conversion**-re, miközben Excel‑ből húztál adatokat? Nem vagy egyedül, aki azon kapja a fejét, hogyan alakítsa a „Reiwa 3‑04‑01” megfelelő .NET `DateTime`‑ná. Ebben az útmutatóban egy tiszta, vég‑től‑végig megoldáson vezetünk végig, amely nem csak a japán korszak dátumokat konvertálja, hanem megmutatja, hogyan **extract datetime from excel** cellákat használva az Aspose.Cells‑et. A végére egy azonnal futtatható konzolalkalmazásod lesz, és szilárd megértésed arról, miért fontosak a kultúra beállítások.

Mindent lefedünk, amire csak kíváncsi lehetsz: a megfelelő kultúra beállítása, az korszak karakterlánc elemzése, szökőévekhez hasonló széljegyek kezelése, és végül a gregorián eredmény kiírása. Nem szükséges külső dokumentáció – csak másolj, illessz be, és futtasd.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core‑on és .NET Framework‑ön is működik)
- Aspose.Cells for .NET (ingyenes próba NuGet csomag `Aspose.Cells`)
- Alapvető ismeretek C#‑ról és konzolalkalmazásokról
- Egy Excel‑fájl (vagy egy új munkafüzet), ahol a dátum japán korszak formátumban szövegként van tárolva

Ha valamelyik hiányzik, szerezd be a NuGet csomagot a következővel:

```bash
dotnet add package Aspose.Cells
```

Most merüljünk el benne.

## 1. lépés: Munkafüzet létrehozása és japán kultúra beállítása

Az első dolog, amit tenned kell, hogy megmondod az Aspose.Cells‑nek, hogy a munkafüzet a japán naptárat használja a dátumok értelmezéséhez. Itt kezdődik igazán a **japanese calendar conversion**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook instance
        Workbook workbook = new Workbook();

        // 2️⃣ Apply Japanese culture (Japanese calendar) to the workbook settings
        workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

        // The rest of the steps follow...
```

**Miért fontos:** A `CultureInfo` nem csak a nyelvet, hanem a naptárinformációt is tartalmazza. A `"ja-JP-u-ca-japanese"`‑re váltással a könyvtár képes megérteni a *Reiwa* vagy *Heisei* korszakneveket, amikor azok a cellákban jelennek meg.

## 2. lépés: Japán korszak dátum írása egy cellába

Demonstrációként egy japán korszak sztringet helyezünk közvetlenül az **A1** cellába. Valós környezetben valószínűleg egy meglévő munkafüzetet olvasnál, de az elv ugyanaz marad.

```csharp
        // 3️⃣ Write a Japanese era date string into cell A1 (row 0, column 0)
        workbook.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");
```

> **Pro tipp:** Ha a forrás Excel már megfelelő Excel sorozatszámként tárolja a dátumokat, kihagyhatod a `PutValue` lépést, és közvetlenül az kinyeréshez léphetsz. A konverziós logika mindkét esetben működik.

## 3. lépés: DateTime kinyerése Excel‑ből – a “extract datetime from excel” magja

Most jön az a rész, ahol **extract datetime from excel**. Az Aspose.Cells egy kényelmes `GetDateTime` metódust biztosít, amely tiszteletben tartja a munkafüzet kultúra beállításait.

```csharp
        // 4️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime gregorianDate = workbook.Worksheets[0].Cells[0, 0].GetDateTime();
```

A háttérben az Aspose a korábban beállított kultúrát nézi, értelmezi a „Reiwa 3‑04‑01” sztringet, és visszaadja a megfelelő gregorián dátumot (`2021‑04‑01`).

## 4. lépés: Az eredmény megjelenítése

Végül írassuk ki a konvertált dátumot a konzolra, hogy ellenőrizhesd, a **japanese calendar conversion** sikeres volt-e.

```csharp
        // 5️⃣ Show the converted Gregorian date
        Console.WriteLine(gregorianDate.ToString("yyyy‑MM‑dd"));
        // Expected output: 2021‑04‑01
    }
}
```

Futtasd a programot (`dotnet run`), és a következőt kell látnod:

```
2021‑04‑01
```

Ez a teljes ciklus: munkafüzet létrehozása, japán kultúra beállítása, korszak dátum írása, `DateTime` kinyerése és megjelenítése.

---

## Mélyebb betekintés: Hogyan működik a japán naptár .NET‑ben

A japán naptár egy *hold‑nap* rendszer, amely az uralkodó császár nevére szóló korszakokba sorolja az éveket. A .NET `JapaneseCalendar` osztály minden korszakot egy gregorián évintervallumhoz rendel. Amikor egy `-u-ca-japanese`‑t tartalmazó `CultureInfo`‑t kérsz, a futtatókörnyezet automatikusan:

1. Felismeri a korszakneveket (pl. *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
2. Az évszámot a korszak kezdetéhez viszonyítva értelmezi.
3. Létrehozza a megfelelő gregorián `DateTime`‑ot.

Ha valaha a másik irányba kell konvertálni – gregoriánról japán korszakra –, használhatod a következőt:

```csharp
var japaneseCal = new System.Globalization.JapaneseCalendar();
int era = japaneseCal.GetEra(gregorianDate);
string eraName = japaneseCal.Eras[era - 1]; // .Eras is zero‑based
int yearInEra = japaneseCal.GetYear(gregorianDate);
Console.WriteLine($"{eraName} {yearInEra:D2}-{gregorianDate:MM-dd}");
```

### Széljegyek kezelése

| Helyzet | Mit kell figyelni | Javasolt megoldás |
|-----------|-------------------|---------------|
| **Hiányzó korszak név** (pl. “03‑04‑01”) | `GetDateTime` `FormatException`‑t dob. | Előre ellenőrizd a sztringet, vagy térj vissza a `DateTime.ParseExact`‑hez egy egyedi mintával. |
| **Jövőbeli korszak** (új császár) | Az aktuális `JapaneseCalendar` nem ismeri a új korszakot, amíg az operációs rendszer frissül. | Frissítsd a .NET futtatókörnyezetet, vagy használj egy egyedi leképezési táblát, amíg az OS fel nem frissül. |
| **Vegyes naptárak egy munkafüzetben** | Néhány cella a gregorián, míg mások a japán naptárat használhatják. | Szükség esetén állítsd be a `CultureInfo`‑t cellánként a `cell.Style.CultureInfo` használatával. |

## Létező Excel fájlokból DateTime kinyerése

Ha már van egy `.xlsx` fájlod japán dátumokkal, a kinyerő kód majdnem azonos – csak cseréld le a munkafüzet létrehozását egy betöltési hívásra:

```csharp
Workbook workbook = new Workbook("Path/To/YourFile.xlsx");
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

// Assuming the date is in B2 (row 1, column 1)
DateTime dateFromFile = workbook.Worksheets[0].Cells[1, 1].GetDateTime();
Console.WriteLine(dateFromFile);
```

Vedd észre, hogy a **extract datetime from excel** ugyanaz a metódushívás marad; az egyetlen extra lépés a fájl betöltése.

---

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes programot találod, amelyet egy konzolprojektbe illeszthetsz. Tartalmazza az összes szükséges `using` direktívát, megjegyzéseket és hibakezelést a produkciós szintű érzetért.

```csharp
using System;
using Aspose.Cells;

class JapaneseCalendarDemo
{
    static void Main()
    {
        try
        {
            // Initialize workbook
            Workbook wb = new Workbook();

            // Apply Japanese calendar culture
            wb.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

            // Insert a Japanese era date string (could be read from an existing file)
            wb.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");

            // Extract as .NET DateTime – this is the core of "extract datetime from excel"
            DateTime gregDate = wb.Worksheets[0].Cells[0, 0].GetDateTime();

            // Output in ISO format
            Console.WriteLine(gregDate.ToString("yyyy-MM-dd"));
        }
        catch (Exception ex)
        {
            // Simple error handling – in real apps you might log this
            Console.Error.WriteLine($"Error during conversion: {ex.Message}");
        }
    }
}
```

**Várható konzol kimenet**

```
2021-04-01
```

Futtasd, és látni fogod a japán korszak bemenetnek megfelelő gregorián dátumot.

## Gyakran Ismételt Kérdések

**Q: Működik ez régebbi Excel fájlokkal (.xls)?**  
Igen. Az Aspose.Cells elrejti a fájlformátumot, így ugyanaz a `GetDateTime` hívás működik mind `.xls`, mind `.xlsx` esetén.

**Q: Mi van, ha a cella valódi Excel dátumot (sorozatszámot) tartalmaz szöveg helyett?**  
Az Aspose továbbra is tiszteletben tartja a munkafüzet kultúráját, és a helyes gregorián `DateTime`‑ot adja vissza. Nem szükséges extra elemzés.

**Q: Átalakíthatok egy egész oszlop japán dátumot egyszerre?**  
Természetesen. Iterálj a sorokon:

```csharp
for (int i = 0; i < worksheet.Cells.MaxDataRow + 1; i++)
{
    DateTime dt = worksheet.Cells[i, 0].GetDateTime();
    // Do something with dt
}
```

**Q: Van teljesítménybeli hatása a kultúra beállításának?**  
Elhanyagolható a tipikus adathalmazoknál. A kultúra egyszer kerül alkalmazásra egy munkafüzetre, nem cellánként.

## Összegzés

Most befejeztük a **japanese calendar conversion** útmutatót, amely pontosan bemutatja, hogyan **extract datetime from excel** az Aspose.Cells segítségével. A munkafüzet `CultureInfo`‑jának `"ja-JP-u-ca-japanese"`‑re állításával zökkenőmentes elemzést kapsz a *Reiwa 3‑04‑01* korszak sztringekre, standard .NET `DateTime` objektumokká. A kód kompakt, robusztus, és készen áll a produkcióra.

Mi a következő? Próbáld meg betölteni egy valós munkafüzetet, konvertálj egy teljes oszlopot, vagy akár írd vissza a gregorián dátumokat egy új lapra. Továbbá felfedezheted más helyi beállításokat – francia köztársasági naptár, iszlám hijri naptár – a kultúra string cseréjével. A minta változatlan.

Van egy saját trükköd, amit megosztanál? Írj kommentet, és jó kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Excel Cell Reference Conversion Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/cell-operations/excel-cell-reference-conversion-aspose-cells-net/)
- [Master HTML to Excel Conversion Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/aspose-cells-net-html-layout-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}