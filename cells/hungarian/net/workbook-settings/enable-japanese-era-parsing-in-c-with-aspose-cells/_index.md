---
category: general
date: 2026-05-30
description: Engedélyezze a japán korszakok feldolgozását C#-ban az Aspose.Cells használatával.
  Tanulja meg, hogyan állítsa be a munkafüzet kultúráját, hogyan dolgozza fel a korszak
  dátumokat, és hogyan kezelje a japán naptárat az Excel munkalapokon.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: hu
og_description: Engedélyezze a japán korszakok feldolgozását C#-ban az Aspose.Cells
  használatával. Ez az útmutató bemutatja, hogyan állítható be a munkafüzet kultúrája,
  hogyan engedélyezhető a korszak támogatása, és hogyan dolgozhatunk japán dátumokkal.
og_title: Japán korszakok feldolgozásának engedélyezése C#‑ban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Japán korszakok feldolgozásának engedélyezése C#-ban az Aspose.Cells segítségével
url: /hu/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán Era Parszolás Engedélyezése C#-ban az Aspose.Cells segítségével

Valaha szükséged volt **enable japanese era parsing** engedélyezésére Excel fájlok generálásakor egy japán ügyfél számára? Nem vagy egyedül — sok fejlesztő akad el, amikor a régi japán naptár (令和, 平成, stb.) megjelenik az adatokban. A jó hír, hogy az Aspose.Cells gyerekjáték, hogy felismerje ezeket az era dátumokat és szabványos gregorián értékekké alakítsa őket.

Ebben az útmutatóban lépésről‑lépésre bemutatjuk, hogyan **enable japanese era parsing** használható az Aspose.Cells‑szel, hogyan állítsuk be a munkafüzet kultúráját japánra, és hogyan illesszünk be egy era‑formázott dátumot egy cellába. A végére egy futtatható C# kódrészletet kapsz, amely a „令和3年5月1日” szöveget a megfelelő `2021‑05‑01` dátumobjektummá alakítja. Külső dokumentáció nélkül — csak másold, illeszd be és futtasd.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód működik .NET Core, .NET Framework és .NET 5+ környezetben is)
- Aspose.Cells for .NET (NuGet csomag `Aspose.Cells`)
- Alap C# ismeretek — ha tudsz egy `Console.WriteLine`‑ot írni, rendben vagy
- A kedvenc IDE‑d (Visual Studio, VS Code, Rider…)

> **Pro tipp:** Tartsd naprakészen az Aspose.Cells verziódat; a 24.10+ verzió már tartalmazza a legújabb japán era definíciókat.

## Miért érdemes engedélyezni a japán era parszt?

A japán naptárak uralkodói korszakokhoz kötődnek. A legtöbb modern alkalmazásban a dátumokat a jól ismert gregorián formátumban szeretnéd tárolni, de a forrásadatok még mindig „令和3年5月1日” formában érkezhetnek. Ha kihagyod a **enable japanese era parsing** lépést, a karakterlánc egyszerű szövegként lesz kezelve, ami hibás számításokhoz, rendezéshez és diagramokhoz vezet. Az era‑támogatás bekapcsolásával az Aspose.Cells automatikusan a megfelelő `DateTime` értékekre konvertálja ezeket a karakterláncokat, megőrizve a japán felhasználók számára olvasható formátumot és a numerikus pontosságot a további feldolgozáshoz.

## 1. lépés: A munkafüzet kultúrájának beállítása japánra

Az első dolog, amit meg kell tenned, hogy elmondod az Aspose.Cells‑nek, hogy a munkafüzet alapértelmezett nyelve japán (`ja-JP`). Ez biztosítja, hogy minden kultúrára specifikus feldolgozás (beleértve az era neveket) a japán szabályok szerint történjen.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Miért fontos:** A `CultureInfo` objektum szabályozza a számformátumokat, a dátumelválasztókat, és legfőképpen számunkra a karakterláncok feldolgozásakor használt naptárrendszert.

## 2. lépés: Japán era parszt engedélyezése

Miután a kultúra be van állítva, fel kell kapcsolnod azt a kapcsolót, amely azt mondja az Aspose.Cells‑nek, hogy ismerje fel az era dátumokat. Ez a **enable japanese era parsing** lényege.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Gyakori hiba:** Ennek a flagnek a kihagyása azt eredményezi, hogy a „令和3年5月1日” egyszerű szöveg marad. Bekapcsolva az Aspose.Cells automatikusan a helyes gregorián évre térképezi az era nevet.

## 3. lépés: Era‑formázott dátum beillesztése egy cellába

A kultúra és az era‑támogatás beállítása után egy japán era karakterlánc beillesztése egyszerű. A könyvtár feldolgozza és egy valódi `DateTime` értéket tárol.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Várható Kimenet

- **A1 cella** a generált `JapaneseEraDemo.xlsx` fájlban **2021‑05‑01**‑et (vagy a lokalizált japán dátumformátumot, ha japán nyelvű Excel‑ben nyitod meg) jeleníti meg.
- A mögöttes érték egy valódi `DateTime`, így biztonságosan használható képletekben, pivot‑táblákban vagy további C# számításokban.

## 4. lépés: A feldolgozott dátum programozott ellenőrzése (opcionális)

Ha szeretnéd megerősíteni, hogy a parszt sikeres volt a mentés előtt, visszaolvashatod a cellát:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Ez a kis ellenőrzési lépés hasznos egységtesztekben vagy felhasználók által feltöltött Excel‑fájlok feldolgozásakor.

## Szélsőséges esetek és variációk

| Szenárió | Mit kell tenni |
|----------|----------------|
| **Több era egy munkafüzetben** | Hagyd beállítva a `UseJapaneseEra = true`‑t; az Aspose.Cells felismeri az összes támogatott era‑t (令和, 平成, 昭和, 大正, 明治). |
| **Vegyes gregorián és era karakterláncok** | A parser automatikusan megkülönbözteti őket; a gregorián karakterláncok változatlanul maradnak. |
| **Egyedi naptár igények** | Továbbra is beállíthatod a `Workbook.Settings.Calendar`‑t egy konkrét `Calendar` példányra, ha nagyobb kontrollra van szükséged. |
| **Régebbi .NET verziók** | Ugyanez a kód működik a .NET Framework 4.6+ verziókon; csak győződj meg róla, hogy a `System.Globalization.CultureInfo` konstruktor elérhető. |

## Gyakorlati tippek valós projektekhez

- **Cache‑eld a CultureInfo‑t**, ha egy ciklusban sok munkafüzetet hozol létre; a többszöri újrapéldányosítás felesleges terhet jelent.
- **Érvényesítsd a bemenetet** a `PutValue` hívása előtt; a hibás era karakterláncok kivételt dobnak.
- **Kapcsold ki az era parszt** (`UseJapaneseEra = false`), ha biztos vagy benne, hogy az adatok soha nem tartalmaznak era dátumokat — ez enyhén javíthatja a teljesítményt.
- **Használd a `Workbook.SaveOptions`‑t** a kimeneti formátum (XLSX, XLS, CSV) szabályozásához, miközben megőrzöd a feldolgozott dátumot.

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Futtasd a programot, nyisd meg a generált fájlt, és az A1 cellában **2021‑05‑01**‑et látsz — bizonyíték arra, hogy sikeresen **enable japanese era parsing**‑t hajtottunk végre.

## Összegzés

Most bemutattuk, hogyan **enable japanese era parsing** C#‑ban az Aspose.Cells segítségével, hogyan állítsuk be a munkafüzet kultúráját, és hogyan konvertáljunk zökkenőmentesen olyan era‑dátumokat, mint a „令和3年5月1日”, szabványos gregorián értékekké. A lépések minimálisak, a kód önálló, és az eredmény hibátlanul működik Excelben.

Készen állsz a következő kihívásra? Próbáld meg kombinálni a **set workbook culture**‑t a japán jen számformázással, vagy generálj több‑lapos jelentést, amely vegyesen tartalmaz gregorián és era dátumokat. Most már megvan az alapod, hogy bármilyen japán naptár‑különlegességet kezelj .NET Excel automatizálási projektjeidben.

---

*Ha ez az útmutató hasznos volt, fontold meg az Aspose.Cells GitHub repó csillagozását vagy saját tippek megosztását a megjegyzésekben. Boldog kódolást!*

## Mit érdemes legközelebb megtanulni?

- [Excel munkafüzetek betöltése kultúraspecifikus dátumokkal az Aspose.Cells for .NET használatával](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Hogyan állíts be nyelvet Excel fájlokban az Aspose.Cells .NET többnyelvű támogatásához](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Munkafüzet kultúraspecifikus dátumok betöltése Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}