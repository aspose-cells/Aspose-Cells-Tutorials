---
title: Az automatikus szűrő az Excelben kezdődik
linktitle: Az automatikus szűrő az Excelben kezdődik
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből az átfogó, lépésenkénti útmutatóból megtudhatja, hogyan szűrheti meg könnyedén az Excel sorait az Aspose.Cells segítségével a .NET-ben.
weight: 10
url: /hu/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az automatikus szűrő az Excelben kezdődik

## Bevezetés

Az adatokkal való munkavégzés során az Excel számtalan iparágban és célra használható alkalmazásnak bizonyult. Egyik legerősebb funkciója az AutoFilter, amely megkönnyíti a kiterjedt adatkészletek átvizsgálását. Ha az Aspose.Cells for .NET-et használja, akkor programozottan kihasználhatja ezt a funkciót, és jelentősen javíthatja adatkezelési feladatait. Ebben az útmutatóban végigvezetjük egy olyan szolgáltatás megvalósításának folyamatán, amely szűri az Excel-sorokat az alapján, hogy azok egy bizonyos karakterlánccal kezdődnek-e.

## Előfeltételek

A merülés előtt győződjön meg arról, hogy a következő előfeltételek teljesülnek:

1. Fejlesztői környezet: Ismerkedjen meg a .NET fejlesztői környezettel. Ez lehet a Visual Studio vagy bármely más választott IDE.
2.  Aspose.Cells for .NET: Az Aspose.Cells for .NET-nek telepítve kell lennie. Ha még nem tette meg, kényelmesen letöltheti[itt](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: A C# és a .NET-könyvtárak használatának alapvető ismerete segít a zökkenőmentes követésben.
4.  Mintaadatok: rendelkeznie kell egy Excel-fájllal, lehetőleg névvel`sourseSampleCountryNames.xlsx`, amely a kijelölt forráskönyvtárban található. Ez a fájl tartalmazza majd azokat az adatokat, amelyeket szűrni fogunk.
5.  Licenc: A teljes funkcionalitás érdekében fontolja meg a licenc beszerzését ezen keresztül[link](https://purchase.aspose.com/buy) . Ha szeretné tesztelni a funkciókat, kérheti a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/).

Minden készen van? Menjünk!

## Csomagok importálása

A kezdéshez importálja a szükséges névtereket a C# fájl tetejére:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ez importálja az Aspose.Cells alapvető funkcióit, valamint az alapvető rendszerfunkciókat, amelyekre a konzolos interakció során támaszkodunk.

Most, hogy beállította a környezetet és importálta a szükséges csomagokat, bontsuk fel az Automatikus szűrő funkciót kezelhető lépésekre. Olyan szűrőt fogunk megvalósítani, amely kivonja a „Ba” betűvel kezdődő sorokat.

## 1. lépés: Forrás- és kimeneti könyvtárak meghatározása

Először is határozzuk meg, hol található a bemeneti Excel fájlunk, és hova szeretnénk menteni a szűrt kimenetünket:

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory\\";

// Kimeneti könyvtár
string outputDir = "Your Document Directory\\";
```

 Magyarázat: Tessék, cserélje ki`"Your Document Directory\\"` a könyvtárak tényleges elérési útjával. Ügyeljen arra, hogy a könyvtár elérési útjait dupla fordított perjellel (`\\`) az útvonalproblémák elkerülése érdekében.

## 2. lépés: Példányosítsa a munkafüzet objektumot

Ezután létrehozunk egy munkafüzet objektumot, amely az Excel fájlunkra mutat:

```csharp
// Mintaadatokat tartalmazó munkafüzet-objektum példányosítása
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 Magyarázat: Ez a sor inicializál egy új munkafüzet-példányt a megadott fájlútvonal használatával. A`Workbook` osztály alapvető fontosságú, mivel a teljes Excel fájlt képviseli.

## 3. lépés: Az első munkalap elérése

Most el kell érnünk azt a konkrét munkalapot, amellyel dolgozni szeretnénk:

```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```

 Magyarázat: A`Worksheets` gyűjtemény lehetővé teszi az egyes lapokhoz való hozzáférést. Használata`[0]` az Excel-fájl első munkalapjára hivatkozik, ami általában bevett gyakorlat az egylapos fájlokkal végzett munka során.

## 4. lépés: Az automatikus szűrő beállítása

Itt kezdődik a varázslat! Adatainkhoz létrehozunk egy AutoFilter tartományt:

```csharp
// Automatikus szűrő létrehozása a cellatartomány megadásával
worksheet.AutoFilter.Range = "A1:A18";
```

 Magyarázat: A`AutoFilter.Range` tulajdonság lehetővé teszi annak megadását, hogy mely sorokat szűrje. Ebben az esetben az A1–A18 tartományba eső sorokat szűrjük, amelyekről feltételezzük, hogy az adatainkat tárolják.

## 5. lépés: Alkalmazza a szűrőfeltételt

A következő lépés a szűrőfeltétel meghatározása. Csak azokat a sorokat szeretnénk megjeleníteni, amelyek első oszlopának értéke "Ba"-val kezdődik:

```csharp
// A "Ba" karakterlánccal kezdődő sorok szűrőjének inicializálása
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 Magyarázat: A`Custom` metódus határozza meg a szűrési logikánkat. Az első érv (`0` ) azt jelzi, hogy az első oszlop (A) alapján szűrünk, és a`FilterOperatorType.BeginsWith` megadja azt a feltételt, hogy a „Ba” betűvel kezdődő sorokat keressük.

## 6. lépés: Frissítse a szűrőt

Szűrési feltételünk alkalmazása után meg kell győződnünk arról, hogy az Excel frissíti a változásokat:

```csharp
// Frissítse a szűrőt a szűrt sorok megjelenítéséhez/elrejtéséhez
worksheet.AutoFilter.Refresh();
```

Magyarázat: Ez a sor az Automatikus szűrő frissítését hívja meg annak biztosítására, hogy a látható sorok megfeleljenek az alkalmazott szűrőfeltételeknek. Ez hasonló az Excel frissítési gombjának megnyomásához.

## 7. lépés: Mentse el a módosított Excel-fájlt

Itt az ideje, hogy mentsük az általunk végzett változtatásokat:

```csharp
// A módosított Excel fájl mentése
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 Magyarázat: A`Save` metódus visszaírja a módosított munkafüzetet a megadott kimeneti útvonalra. Ez a meghatározott szűrők új fájlba írása alá esik, így az eredeti adatok érintetlenek maradnak.

## 8. lépés: Kimenet megerősítése

Végül erősítsük meg, hogy műveletünk sikeres volt:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Magyarázat: Ez az egyszerű sor egy megerősítő üzenetet küld a konzolnak, jelezve, hogy a szűrési folyamat hiba nélkül fejeződött be.

## Következtetés

Egy olyan világban, ahol az adatkezelés elsöprőnek tűnik, az olyan funkciók elsajátítása, mint az AutoFilter az Excelben az Aspose.Cells for .NET segítségével, lehetővé teszi az adatok hatékony és eredményes kezelését. Megtanulta a „Ba” betűvel kezdődő Excel-sorok szűrését, lépésről lépésre valósítva meg a módszert. Gyakorlattal képes lesz ezt a módszert a folyamatban lévő projektjei során különféle adatszűrési igényekhez igazítani.

## GYIK

### Mi az AutoFilter célja az Excelben?  
Az AutoFilter lehetővé teszi a felhasználók számára, hogy gyorsan rendezzék és szűrjék az adatokat egy táblázatban, megkönnyítve az egyes adatkészletekre való összpontosítást.

### Szűrhetek több feltétel alapján az Aspose.Cells segítségével?  
Igen, az Aspose.Cells támogatja a speciális szűrési beállításokat, amelyek lehetővé teszik több feltétel beállítását.

### Szükségem van licencre az Aspose.Cells használatához?  
Bár ingyenes próbaverzióval kezdheti, licenc szükséges a teljes funkcionalitáshoz és a próbaidőszak korlátozásainak megszüntetéséhez.

### Milyen típusú szűrést végezhetek az Aspose.Cells használatával?  
Az adatokat érték, feltétel (például azzal kezdődik vagy ezzel végződik) és egyéni szűrés alapján szűrheti, hogy megfeleljen sajátos követelményeinek.

### Hol találhatok további információt az Aspose.Cells for .NET-ről?  
 Ellenőrizheti a dokumentációt[itt](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
