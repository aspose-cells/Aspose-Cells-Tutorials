---
category: general
date: 2026-03-22
description: Tanulja meg, hogyan formázhatja a dátum‑idő értéket ISO formátumba, miközben
  Excelből kinyeri a dátumot, és hogyan jelenítheti meg az ISO dátumot az Aspose.Cells
  segítségével C#‑ban.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: hu
og_description: A dátum és idő ISO formátumba konvertálása egyszerű. Ez az útmutató
  bemutatja, hogyan lehet kinyerni a dátumot az Excelből, és megjeleníteni az ISO
  dátumot az Aspose.Cells segítségével.
og_title: Dátum és idő formázása ISO formátumba C#-ban – Lépésről lépésre útmutató
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Dátum és idő formázása ISO formátumba C#-ban – Teljes útmutató
url: /hu/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum és idő formázása ISO formátumba C#‑ban – Teljes útmutató

Valaha szükséged volt **format datetime to iso**-ra, de a forrás egy Excel munkafüzetben van? Lehet, hogy a cella egy japán korszakot tartalmaz, például “令和3年5月1日”, és azon kapkodod a fejed, hogy hogyan alakítsd át egy tiszta `2021‑05‑01` karakterlánccá. Nem vagy egyedül. Ebben az útmutatóban **extract date from excel**‑t fogunk végrehajtani, feldolgozzuk a japán korszakot, majd **display iso date**-t jelenítünk meg a konzolon – mindezt néhány C# és Aspose.Cells sorral.

Végigvezetünk minden szükséges lépésen: a szükséges NuGet csomagon, a pontos kódrészleten, amelyet egyszerűen másolhatsz‑beilleszthetsz, hogy miért fontos minden sor, és néhány edge‑case tippel. A végére egy újrahasználható kódrészletet kapsz, amely **formats datetime to iso**, függetlenül attól, milyen furcsa az eredeti Excel érték.

## Amire szükséged lesz

- .NET 6.0 vagy újabb (a kód .NET Framework 4.6+‑on is fordul)
- Visual Studio 2022 (vagy bármelyik kedvenc szerkesztő)
- **Aspose.Cells for .NET** NuGet csomag – `Install-Package Aspose.Cells`
- Egy Excel fájl (vagy egy új munkafüzet), amely japán korszak formátumú dátumot tartalmaz

Ennyi. Nincs extra könyvtár, nincs COM interop, csak egyetlen, jól dokumentált metódus.

## 1. lépés: Munkafüzet létrehozása és japán korszak dátum írása  

Először is szükségünk van egy munkafüzetre, amivel dolgozhatunk. Ha már van egy Excel fájlod, betöltheted a `new Workbook("path")`‑vel. Ebben a példában egy új munkafüzetet hozunk létre a memóriában, és egy japán korszak szöveget helyezünk a **A1** cellába.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Miért csináljuk ezt:** Aspose.Cells alapértelmezés szerint a cellaértékeket karakterláncként kezeli. A nyers korszak szöveg beillesztésével egy valós helyzetet szimulálunk, ahol egy japán ügyfél a saját naptáruk szerint adta meg a dátumokat.

## 2. lépés: Japán korszak feldolgozás engedélyezése és a dátum kinyerése  

Az Aspose.Cells automatikusan le tudja fordítani a japán korszak karakterláncokat .NET `DateTime` objektumokká – ha ezt engedélyezed. A `DateTimeParseOptions.EnableJapaneseEra` jelző végzi a nehéz munkát.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tipp:** Ha elfelejted az `EnableJapaneseEra` opciót, a könyvtár az eredeti karakterláncot adja vissza, és a későbbi konverzió hibára fut. Mindig ellenőrizd a `parsed.Type`‑t, ha vegyes tartalommal dolgozol.

## 3. lépés: A feldolgozott DateTime konvertálása ISO 8601‑re  

Most, hogy már van egy megfelelő `DateTime` objektumunk, az ISO‑formátumú karakterlánccá alakítása gyerekjáték. A `"yyyy-MM-dd"` minta megfelel az ISO 8601 dátum résznek, amit a legtöbb API elvár.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Running the program prints:

```
ISO date: 2021-05-01
```

Ez a **display iso date**, amit kerestél.

## Teljes, futtatható példa  

Az alábbi teljes kódrészletet közvetlenül beillesztheted egy konzolos projektbe. Nincs rejtett függőség, nincs extra konfiguráció.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Várható kimenet:** `ISO date: 2021-05-01`

## Lépésről‑lépésre magyarázat (Miért fontos minden részlet)

| Lépés | Mi történik | Miért fontos |
|------|--------------|--------------------|
| **Munkafüzet létrehozása** | Inicializál egy memóriában lévő Excel konténert. | Egy sandboxot biztosít a teszteléshez, anélkül, hogy a fájlrendszert érintenéd. |
| **PutValue** | Elhelyezi a nyers japán korszak karakterláncot a **A1** cellában. | Utánozza a valós adatbevitelt; biztosítja, hogy a parser a pontos szöveget lássa. |
| **GetValue with `EnableJapaneseEra`** | Átalakítja a korszak karakterláncot .NET `DateTime` objektummá. | Automatikusan kezeli a naptárkonverziót – manuális keresőtáblákra nincs szükség. |
| **`ToString("yyyy-MM-dd")`** | Formázza a `DateTime`-ot ISO 8601‑re. | Garantál egy kultúra‑független, rendezhető dátumkarakterláncot, amelyet a REST API‑k, adatbázisok stb. elfogadnak. |
| **Console.WriteLine** | Megjeleníti a végső ISO dátumot. | Megerősíti, hogy az egész folyamat vég‑től‑végig működik. |

## Gyakori változatok kezelése  

### 1. Különböző cellahelyek  

Ha a dátumod a **B2** cellában vagy egy névvel ellátott tartományban van, egyszerűen cseréld le az `"A1"`‑t a megfelelő címre:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Több dátum egy oszlopban  

Ha sok sorban kell **extract date from excel**‑t végrehajtani, iterálj a használt tartományon:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Tartalék nem‑korszak dátumokhoz  

Ha egy cella már egy szabványos dátumkarakterláncot tartalmaz, a parser továbbra is működik, de érdemes egy biztonsági hálót beépíteni:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

A `TryParse` jelző megakadályozza a kivételeket, és ha a konverzió sikertelen, az eredeti értéket adja vissza.

### 4. Idő komponens  

Ha szükséged van az idő részre is, használd a `"yyyy-MM-ddTHH:mm:ss"` formátumot:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Ez egy teljes ISO 8601 időbélyeget eredményez (`2021-05-01T00:00:00`).

## Vizuális segédlet  

![dátum és idő formázása ISO példája](image.png "Példa a dátum és idő ISO formátumba történő formázására C#‑ban")

*Alt szöveg:* *dátum és idő formázása ISO példája a konzol kimenetén*

## Gyakran Ismételt Kérdések  

- **Használhatom ezt .xls fájlokkal?**  
  Igen. Az Aspose.Cells alapból támogatja a `.xls`, `.xlsx`, `.csv` és számos más formátumot.

- **Mi van, ha a munkafüzet jelszóval védett?**  
  Töltsd be a `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`‑vel.

- **Az ISO formátum helyi beállítástól függ?**  
  Nem. A `"yyyy-MM-dd"` minta kultúra‑független, garantálva ugyanazt a karakterláncot minden gépen.

- **Működik ez .NET Core‑on?**  
  Teljesen – az Aspose.Cells .NET Standard 2.0‑nak megfelelő.

## Összegzés  

Áttekintettük, hogyan **format datetime to iso** **extract date from excel**‑vel, a japán korszak karakterláncok feldolgozásával, és végül **display iso date** megjelenítésével a konzolon. A fő lépések – munkafüzet létrehozása, a korszak szöveg írása vagy betöltése, a japán korszak feldolgozás engedélyezése, és a `ToString("yyyy-MM-dd")` formázás – mindent tartalmaznak a legtöbb esethez.

Ezután esetleg szeretnéd:

- Visszaírni az ISO dátumokat egy másik oszlopba a további feldolgozáshoz.
- Exportálni a módosított munkafüzetet CSV‑be tömeges importáláshoz.
- Összevonni ezt a logikát egy web API‑val, amely Excel feltöltéseket fogad, és JSON‑kódolt ISO dátumokat ad vissza.

Nyugodtan kísérletezz különböző dátumformátumokkal, időzónákkal vagy akár egyedi naptárakkal. Az Aspose.Cells rugalmassága miatt ritkán ütközöl akadályba.

Boldog kódolást, és legyenek a dátumaid mindig tökéletesen ISO‑kompatibilisek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}