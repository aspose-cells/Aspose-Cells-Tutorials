---
category: general
date: 2026-09-24
description: Parsoljon DateTime értékeket a japán császár uralkodása szerint az Aspose.Cells
  C#-ban. Engedélyezze a japán korszak naptárát, írjon korszak karakterláncokat, és
  szerezzen pontos DateTime értékeket.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: hu
lastmod: 2026-09-24
og_description: Dátum és idő (DateTime) feldolgozása a japán császári uralkodás szerint
  az Aspose.Cells segítségével C#-ban. Ez az útmutató bemutatja, hogyan lehet engedélyezni
  a japán korszaknaptárat, korszak karakterláncokat írni, és helyes DateTime értéket
  visszaolvasni.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: DateTime feldolgozása japán császár uralkodásával az Aspose.Cells segítségével
  – C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Dátum és idő feldolgozása japán császári uralkodás szerint az Aspose.Cells
  használatával
url: /hu/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum és idő elemzése japán császári uralkodás alapján az Aspose.Cells használatával

Ha egy .NET alkalmazásban **dátum és idő elemzésére japán császári uralkodás alapján** van szükséged, ez az útmutató pontosan megmutatja, hogyan teheted ezt meg az Aspose.Cells segítségével. A japán era naptár engedélyezésével, egy era‑alapú karakterlánc írásával és a kapott `DateTime` érték kiolvasásával megbízható, kultúrára érzékeny dátumokat kapsz manuális karakterlánc‑manipuláció nélkül.

A japán era dátumok kezelése gyakori a pénzügyekben, a kormányzati szektorban és a régi rendszerekben, amelyek még mindig olyan formátumban tárolják a dátumokat, mint a “令和3年5月10日”. Ez a tutorial lefedi a teljes munkafolyamatot, a projekt beállításától a `DateTime` objektum lekéréséig, amelyet számításokban, naplózásban vagy felhasználói felületen való megjelenítésben használhatsz.

## Mit fogsz megtanulni

- Hogyan add hozzá az Aspose.Cells NuGet csomagot egy C# projekthez.  
- Hogyan kapcsolod be a **Japanese era calendar**-t a `Workbook.Settings` segítségével.  
- Hogyan írsz japán era dátum karakterláncot egy cellába, és hagyod, hogy az Aspose.Cells automatikusan értelmezze.  
- Hogyan olvasod ki a feldolgozott `DateTime`-t a `DateTimeValue` tulajdonság használatával.  

**Előfeltételek**  
- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik).  
- Alapvető ismeretek a C#‑ról és a Visual Studio‑ról (vagy bármely IDE‑ról).  
- Internetkapcsolat az Aspose.Cells csomag letöltéséhez.

---

## 1. lépés: Aspose.Cells telepítése

Nyisd meg a projekt mappádat egy terminálban vagy a NuGet Package Manager Console‑ban, és futtasd a következőt:

```bash
dotnet add package Aspose.Cells
```

Vagy a Visual Studio‑ban kattints jobb‑gombbal a projektre → **Manage NuGet Packages** → keresd meg a **Aspose.Cells**‑t, és kattints a **Install** gombra.  
Ez hozzáadja az `Aspose.Cells` assembly‑t, amely biztosítja a szükséges `Workbook`, `Worksheet` és a feldolgozási képességeket.

## 2. lépés: A japán era naptár engedélyezése

Az Aspose.Cells alapértelmezés szerint letiltja a japán era feldolgozást. Engedélyezned kell a `Workbook.Settings.UseJapaneseEraCalendar` kapcsolón keresztül.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

A `UseJapaneseEraCalendar` `true`‑ra állítása azt mondja a könyvtárnak, hogy a karakterláncokat, amelyek era neveket tartalmaznak (`令和`, `平成`, `昭和`, stb.), a hivatalos japán naptár szabályai szerint értelmezze.

## 3. lépés: Japán era dátum karakterlánc írása egy cellába

Ezután szerezd meg az első munkalapot, és helyezz egy japán era dátum karakterláncot az **A1** cellába.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Miért működik ez:**  
Amikor a `UseJapaneseEraCalendar` aktív, a `PutValue` megvizsgálja a karakterláncot, felismeri az era előtagot (`令和`), és belsőleg átalakítja a megfelelő gergelyi évre (2021). A könyvtár ezután a értéket valódi `DateTime` objektumként tárolja, nem csak szövegként.

## 4. lépés: A feldolgozott `DateTime` érték lekérése

Most olvasd ki a cella `DateTimeValue`‑ját. Az Aspose.Cells automatikusan visszaadja a gergelyi dátumot.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

A program futtatása a következőt írja ki:

```
Parsed Gregorian date: 2021-05-10
```

A kimenet megerősíti, hogy a **Parse DateTime with Japanese Emperor Reign** helyesen átalakította a “令和3年5月10日” értéket 2021. május 10‑re.

## 5. lépés: Szélsőséges esetek és gyakori változatok kezelése

### Többféle era formátum
Az Aspose.Cells több era ábrázolást is felismer:

| Era (Japanese) | Gergelyi év tartomány |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

Ha a forrásadatok keverik a teljes szélességű karaktereket, szóközöket, vagy a kanji „年”, „月”, „日” karaktereket használják, a parser még mindig sikeres. Például a `"平成31年4月30日"` `2019-04-30`‑ra alakul.

### Érvénytelen karakterláncok
Ha a karakterláncot nem lehet feldolgozni (pl. `"令和99年13月40日"`), a `DateTimeValue` `DateTime.MinValue`‑t ad vissza. Ezt a feltételt ellenőrizheted:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### A funkció letiltása
Ha később nyers era karakterláncokat szeretnél tárolni konverzió nélkül, állítsd vissza a kapcsolót `false`‑ra:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Teljesítmény tipp
Az era naptár engedélyezése kis teljesítménybeli többletet ad minden olyan `PutValue` híváshoz, amely karakterláncokat érint. Ha csak néhány cellát kell feldolgozni, engedélyezd a kapcsolót közvetlenül a művelet előtt, és a művelet után tiltsd le, hogy minimalizáld a hatást.

## Teljes, futtatható példa

Az alábbiakban a teljes programot találod, amelyet másolhatsz, beilleszthetsz és azonnal futtathatsz.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Várható kimenet**

```
Parsed Gregorian date: 2021-05-10
```

A program bemutatja a **Parse DateTime with Japanese Emperor Reign** végponttól végpontig tartó folyamatát az Aspose.Cells használatával, a munkafüzet létrehozásától egy felhasználható `DateTime` objektum megszerzéséig.

---

## Következtetés

Most már tudod, hogyan **Parse DateTime with Japanese Emperor Reign** C#‑ban a következők szerint:

1. Az **Aspose.Cells** telepítése.  
2. A **Japanese era calendar** engedélyezése a `Workbook.Settings`‑en keresztül.  
3. Era‑alapú karakterláncok írása cellákba.  
4. A kapott `DateTimeValue` kiolvasása.  

Ez a megközelítés megszünteti a manuális feldolgozási logikát, tiszteletben tartja a hivatalos era határokat, és zökkenőmentesen integrálódik a meglévő .NET dátumkezelő kódba.

**Következő lépések**  
- Fedezd fel az Aspose.Cells egyéb kultúra‑specifikus funkcióit, például a **C# date parsing**‑t a hidzsri vagy a thai buddhista naptárakhoz.  
- Kombináld ezt a technikát **Workbook Settings**‑ekkel, mint a `CalcEngine`, hogy kiértékeld az era dátumokra hivatkozó képleteket.  
- Használd a feldolgozott `DateTime`‑t jelentésekben, adatbázis tárolásban vagy UI komponensekben, amelyek gergelyi dátumokat igényelnek.

Nyugodtan kísérletezz különböző era karakterláncokkal, kezeld az érvénytelen bemenetet, és integráld a megoldást nagyobb adat‑import csővezetékekbe. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Japán era dátumok elemzése Excelben – Teljes útmutató C# fejlesztőknek](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Hogyan elemezzünk japán dátumokat C#‑ban – Teljes útmutató](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Hogyan valósítsunk meg dátumvalidációt .NET‑ben az Aspose.Cells használatával: Átfogó útmutató](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}