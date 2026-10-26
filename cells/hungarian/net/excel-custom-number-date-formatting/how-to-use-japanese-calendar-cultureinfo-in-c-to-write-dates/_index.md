---
category: general
date: 2026-10-26
description: Tanulja meg, hogyan használja a japán naptár CultureInfo-ot C#-ban korszakdátumok
  feldolgozásához, és hogyan illessze be őket NPOI-val egy Excel munkalapba.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: hu
lastmod: 2026-10-26
og_description: Használja a japán naptár CultureInfo-ot C#-ban a Reiwa korszak dátumainak
  feldolgozásához, és írja őket egy Excel munkalapra. Teljes, futtatható kód magyarázatokkal.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Japán naptár CultureInfo használata C#‑ban – teljes Excel példa
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Hogyan használjuk a japán naptár CultureInfo-ot C#-ban a dátumok Excelbe írásához
url: /hu/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a japán naptár CultureInfo‑t C#‑ban dátumok Excel‑be írásához

Ha **a japán naptár CultureInfo‑t** kell használnod a C#‑ban dátumok kezelése közben, ez az útmutató pontosan megmutatja, hogyan. Megtanulod, hogyan kell egy olyan dátumkarakterláncot elemezni, amely japán korszaknevet tartalmaz (például *Reiwa 2/5/1*), majd az eredményül kapott `DateTime`‑ot beírni egy Excel munkalap első cellájába a NPOI könyvtár segítségével.

Az era‑alapú dátumok helytelen `CultureInfo` nélkül történő elemzése `FormatException`‑t vagy helytelen hónap/nap értékeket eredményez. A `CultureInfo` japán naptárra való beállításával garantálod, hogy a .NET futtatókörnyezet helyesen értelmezi az korszakot, és hogy az Excel‑be mentett érték megegyezik az eredeti japán jelöléssel.

Ebben az oktatóanyagban:

* Létrehozol egy `CultureInfo` objektumot, amely a japán naptárat használja.
* Elemzel egy japán korszak dátumkarakterláncot a `DateTime.Parse`‑szal.
* Beszúrod a feldolgozott `DateTime`‑t egy NPOI munkalap cellájába.
* Megtekinted a teljes, futtatható programot és a várt kimenetet.

> **Előfeltételek** – .NET 6.0+ (vagy .NET Core 3.1+), a **NPOI** NuGet csomag, valamint alapvető C# és Excel‑fájlkezelési ismeretek.

---

## Amire szükséged lesz

| Elem | Indok |
|------|-------|
| **.NET SDK** (6.0 vagy újabb) | Biztosítja a futtatókörnyezetet és a `CultureInfo`‑hez szükséges könyvtárakat. |
| **NPOI** (`NPOI` NuGet csomag) | Lehetővé teszi Excel fájlok létrehozását és manipulálását Office telepítése nélkül. |
| **Visual Studio Code**, **Visual Studio**, vagy bármely C# IDE | A minta lefordításához és futtatásához. |
| **Japanese era date string** (pl. `"Reiwa 2/5/1"`) | A japán naptár használatának bemutatása. |

---

## 1. lépés: NPOI telepítése

Nyiss egy terminált a projekt mappádban, és futtasd:

```bash
dotnet add package NPOI --version 2.6.1
```

A csomag biztosítja a később használt `IWorkbook`, `ISheet` és `ICell` típusokat.

---

## 2. lépés: CultureInfo létrehozása, amely a japán naptárat használja

A japán naptár egy era‑alapú naptár. Kérned kell a *Japanese* változatot a `ja-JP` helyi beállításból, és kifejezetten be kell állítanod a naptárat `JapaneseCalendar`‑ra.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Miért fontos** – Az alapértelmezett `ja-JP` kultúra a Gergelyi naptárat használja. A `Calendar` tulajdonság újra‑rendelése biztosítja, hogy az olyan korszakneveket, mint a *Reiwa*, felismerje az elemzés során.

---

## 3. lépés: Japán korszak dátumkarakterlánc elemzése

Most, hogy a `CultureInfo` be van állítva, biztonságosan elemezhetsz egy korszaknevet tartalmazó karakterláncot.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Kimenet**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

A `Parse` metódus a *Reiwa 2*‑t a Gergelyi 2020. év, 5. hónap, 1. nap értékként értelmezi.

### Szélsőséges eset: érvénytelen korszakok kezelése

Ha egy felhasználó nem támogatott korszakot ad meg (például `"Heisei 31/4/30"` a Heisei korszak vége után), a `DateTime.Parse` `FormatException`‑t dob. Tedd a hívást try‑catch blokkba, hogy barátságos hibaüzenetet biztosíts:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## 4. lépés: A feldolgozott DateTime írása egy Excel munkalapba

A `DateTime` objektum készen áll, így tárolhatod egy Excel cellában. A NPOI automatikusan a `DateTime` értékeket Excel‑dátumként formázza.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Eredmény** – A *JapaneseEraDate.xlsx* megnyitásakor a **2020‑05‑01** dátum látható az A1 cellában.

### Miért használjuk a NPOI‑t?

*Works on any platform* (Windows, Linux, macOS) és **nem** igényel Microsoft Office‑t. Ez a megoldás alkalmas CI pipeline‑okra, Docker konténerekre vagy szerver‑oldali feldolgozásra.

---

## 5. lépés: Teljes, futtatható program

Az összes lépést egyesítve itt egy komplett konzolalkalmazás, amely bemutatja a teljes folyamatot:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Hogyan futtassuk**

```bash
dotnet run
```

A futtatás után a `JapaneseEraDate.xlsx` fájlt a projekt mappájában fogod megtalálni, a helyesen feldolgozott dátummal.

---

## Gyakori buktatók és legjobb gyakorlatok

| Hiba | Javítás / Ajánlás |
|------|-------------------|
| Elfelejtetted beállítani a `japaneseCulture.DateTimeFormat.Calendar`‑t | Mindig rendelj hozzá egy `JapaneseCalendar` példányt; különben a korszak neve nem lesz felismert. |
| `DateTime.TryParse` használata a saját `CultureInfo` nélkül | Add át ugyanazt a `japaneseCulture`‑t a `TryParse`‑nak, hogy a viselkedés konzisztens legyen. |
| Azt várod, hogy az Excel megjelenítse a korszaknevet | Az Excel beépített dátumformátumai csak Gergelyi naptárat támogatnak. Ha a korszakot is meg akarod jeleníteni, tárold az eredeti karakterláncot egy külön oszlopban vagy hozz létre egy egyedi szövegformátumot. |
| Nem zárod le a `FileStream`‑et | Használj `using` blokkot (ahogy a példában látható), hogy a fájlkezelő azonnal felszabaduljon. |
| `CultureInfo` objektumok keverése szálak között | A `CultureInfo` csak olvasásra szál‑biztonságos; kerüld a `Calendar` tulajdonság módosítását az inicializálás után. |

---

## Következtetés

Most már tudod, hogyan **használjuk a japán naptár CultureInfo‑t** C#‑ban a japán korszak dátumok pontos elemzéséhez, és hogyan írjuk a kapott `DateTime`‑t egy Excel munkalapba a NPOI‑val. A teljes példa lefedi a konfigurációt, az elemzést, a hibakezelést és az Excel‑kimenetet, így szilárd alapot ad bármilyen nemzetközi jelentéshez vagy adatcseréhez.

A következőket is felfedezheted:

* **Dátumok formázása egyedi szöveggel**, hogy az era‑nevet is megtartsuk az Excelben.
* **Dátumok olvasása Excel‑ből** a `cell.DateCellValue`‑val, miközben tiszteletben tartjuk a japán naptárat.
* **Ugyanazon technika alkalmazása** más era‑alapú naptárakra (például a thai buddhista naptár) a `JapaneseCalendar` helyettesítésével a megfelelő `Calendar` alosztállyal.

Nyugodtan kísérletezz különböző korszakkarakterláncokkal, nagyobb adatállományokkal, vagy integráld ezt a logikát ASP.NET Core API‑kba, amelyek valós időben generálnak Excel‑jelentéseket. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel munkafüzet létrehozása japán naptári dátumokkal – Teljes útmutató](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Japán korszak dátumok elemzése Excelben – Teljes útmutató C# fejlesztőknek](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Excel munkafüzet létrehozása és japán dátumok elemzése C#‑ban](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}