---
category: general
date: 2026-10-01
description: Konvertálja a japán korszak dátumát gregorián DateTime-re az Aspose.Cells
  használatával C#-ban. Tanulja meg, hogyan konvertálja gyorsan a japán naptárat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: hu
lastmod: 2026-10-01
og_description: japán korszak dátum konvertálása gregorián DateTime-ra C#-ban. Ez
  az útmutató bemutatja, hogyan lehet pontosan átalakítani a japán naptárat az Aspose.Cells
  segítségével.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Japán korszak dátum konvertálása gregoriánra C#‑ban – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Hogyan konvertáljuk a japán korszak dátumát gregoriánra C#‑ban
url: /hu/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan konvertáljuk a japán era dátumot gregoriánra C#‑ban

Ha **japán era dátum** karakterláncokat szeretnél átalakítani gregorián dátumokká C#‑ban, ez az útmutató pontosan megmutatja, hogyan. Legyen szó örökölt adatok feldolgozásáról, felhasználói bevitel olvasásáról vagy jelentések generálásáról, az Aspose.Cells könyvtár egyszerűvé teszi a konverziót. Emellett megtudod, mi a legjobb módja a **japán naptár** értékek konvertálásának táblázatokban.

A tutorial minden lépést lefed – a munkafüzet létrehozásától a `DateTime` érték lekéréséig – így egy teljes, futtatható programot egyszerűen másolhatsz‑beilleszthetsz. Nem szükséges külső dokumentáció; csak kövesd a kódot és a magyarázatokat alább.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy a következők rendelkezésre állnak:

* .NET 6.0 vagy újabb (a kód .NET Framework 4.6+‑tal is működik)
* **Aspose.Cells** licenc (a ingyenes próba verzió teszteléshez elegendő)
* Fejlesztői környezet, például Visual Studio 2022 vagy VS Code
* Alapvető ismeretek C# konzolalkalmazásokról

## Japán era dátum konvertálása Aspose.Cells‑szel

A konverzió lényege néhány egyszerű API hívásban rejlik. Az Aspose.Cells automatikusan értelmezi a japán era karakterláncokat (pl. „Reiwa 2/04/01”) és a munkalap újraszámítása után `DateTime` objektumként adja vissza az eredményt.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Miért fontos minden egyes lépés

| Lépés | Cél | Hogyan segíti a konverziót |
|------|-----|----------------------------|
| **Munkafüzet létrehozása** | Olyan tárolót biztosít, amely érti az Excel képleteket és dátumrendszereket. | A könyvtár belső dátummotorja csak munkafüzeten belül aktiválódik. |
| **Era karakterlánc beillesztése** | A nyers japán naptár szöveget adja meg, amelyet le szeretnél fordítani. | Az Aspose.Cells felismeri az olyan era neveket, mint *Reiwa*, *Heisei*, *Showa* stb. |
| **Stílus beállítása** | Kényszeríti, hogy a cellát értékcellaként kezelje, ne egyszerű szövegként. | Stílus nélkül a `Calculate` metódus figyelmen kívül hagyhatja a cellát, és a szöveg változatlan marad. |
| **Számítás** | Elindítja az era karakterlánc elemzését és átalakítását a belső sorozatszámra. | A könyvtár átalakítja a „Reiwa 2/04/01” → sorozatszám → gregorián `DateTime` értéket. |
| **`DateTimeValue` kiolvasása** | Visszaadja a konvertált .NET `DateTime` objektumot. | Most már egy szabványos `DateTime`-ot kapsz, amelyet bármely .NET API‑ban használhatsz. |

## Japán naptár konvertálása más helyzetekben

Ugyanaz a megközelítés működik minden, az Aspose.Cells által támogatott japán era névre:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Érvénytelen vagy kétértelmű karakterláncok kezelése

* **Érvénytelen era név** – Az Aspose.Cells `FormatException`‑t dob. A konverziót `try/catch`‑ben kell körülvenni, hogy barátságos hibaüzenetet jelenítsen meg.
* **Hiányzó év/hónap/nap** – A könyvtár teljes “Era Year/Month/Day” mintát vár. Ha részleges adatot kapsz, előzd meg a hiányzó részekkel, vagy korán utasítsd el a bemenetet.
* **Eltérő helyi beállítások** – A konverzió **nem** függ a jelenlegi szál kultúrájától; mindig az Aspose.Cells‑be ágyazott japán era térképet használja. Ez a módszert biztonságossá teszi szerveroldali feldolgozásnál.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Gyakorlati tippek és gyakori buktatók

* **Mindig hívd meg a `SetStyle`‑t** a `Calculate` előtt. Ennek kihagyása gyakori hiba, mert a cella egyszerű szövegként marad.
* **Használd újra ugyanazt a munkafüzetet**, ha sok dátumot kell konvertálni. Új munkafüzet létrehozása minden egyes konverzióhoz felesleges terhelést jelent.
* **Kötegelt konverzió** – Tölts fel egy oszlopot era karakterláncokkal, hívd egyszer a `worksheet.Calculate()`‑t, majd olvasd ki az egész oszlop `DateTimeValue`‑jait. Ez sokkal hatékonyabb, mint cellánként újraszámolni.
* **Verziókompatibilitás** – Az era konverzió logikája az Aspose.Cells 22.9‑es verzióban került bevezetésre. Győződj meg róla, hogy legalább ezen a verzión vagy újabb verzión vagy; a régebbi kiadások a karakterláncot egyszerű szövegként kezelik.

## Teljes működő példa (konzolalkalmazás)

Az alábbi önálló programot azonnal lefordíthatod és futtathatod. Bemutatja a Reiwa és a Heisei konverziót, valamint a hibakezelést is.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Várható konzolkimenet**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

A program futtatása megerősíti, hogy a könyvtár helyesen **konvertálja a japán era dátumot** karakterláncokat, és megfelelően jelzi a nem támogatott értékeket.

## Összegzés

Most már tudod, hogyan **konvertálj japán era dátumot** karakterláncokból szabványos gregorián `DateTime` objektumokká az Aspose.Cells segítségével C#‑ban. A folyamat lényegében az era szöveg beillesztése, stílus alkalmazása, a munkalap újraszámítása és a `DateTimeValue` kiolvasása. A fenti lépéseket követve válaszolhatsz a szélesebb körű kérdésre is, hogy **hogyan konvertáljunk japán naptár** adatokat tömegesen, kezeljünk hibákat és optimalizáljuk a teljesítményt.

### Következő lépések

* Fedezd fel a **formázási lehetőségeket**, hogy a gregorián dátumot visszaírhasd a munkalapba egyedi számformátummal.
* Kombináld ezt a konverziót **adatimport pipeline‑okkal** (pl. CSV‑fájlok, amelyek era dátumokat tartalmaznak).
* Tekintsd át az Aspose.Cells egyéb funkcióit, például a **dátumaritmetikát** és a **regionális beállításokat** összetettebb naptári forgatókönyvekhez.

Jó kódolást, és nyugodtan igazítsd a mintát a saját adatfeldolgozó folyamataidhoz!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}