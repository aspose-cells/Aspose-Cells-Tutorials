---
category: general
date: 2026-04-07
description: Írj dátumot és időt Excelbe C#-val. Tanuld meg, hogyan illessz be dátumot
  a munkalapra, kezeld az Excel cella dátumértékét, és néhány lépésben konvertáld
  a japán naptár dátumát.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: hu
og_description: Írj dátumot és időt gyorsan az Excelbe. Ez az útmutató bemutatja,
  hogyan illessz be dátumot a munkalapra, kezeld az Excel cella dátumértékét, és konvertáld
  a japán naptár dátumát C#-ban.
og_title: Dátum és idő írása Excelbe – Lépésről lépésre C# útmutató
tags:
- C#
- Excel automation
- Aspose.Cells
title: Dátum és idő írása Excelbe – Teljes útmutató C# fejlesztőknek
url: /hu/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum és idő írása Excelbe – Teljes útmutató C# fejlesztőknek

Valaha is szükséged volt **write datetime to Excel**-re, de nem tudtad, melyik API hívás tárolja valóban az Excel dátumot? Nem vagy egyedül. Sok vállalati eszközben egy C# `DateTime`-ot kell egy táblázatba helyezni, és az eredménynek úgy kell viselkednie, mint egy valódi Excel dátum – rendezhető, szűrhető, és készen áll a pivot táblákra.  

Ebben az útmutatóban lépésről lépésre bemutatjuk, hogyan *insert date into worksheet* Aspose.Cells segítségével, miért fontos a kultúra beállítása, és még azt is megmutatjuk, hogyan **convert Japanese calendar date** egy szabványos `DateTime`-ra, mielőtt írnád. A végére egy önálló kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz.

## Amire szükséged lesz

- **.NET 6+** (vagy bármely friss .NET verzió; a kód .NET Frameworkön is működik)  
- **Aspose.Cells for .NET** – egy NuGet csomag, amely lehetővé teszi Excel fájlok manipulálását Office telepítése nélkül.  
- Alapvető ismeretek a C# `DateTime`-ról és a kultúrákról.  

Nincs szükség extra könyvtárakra, COM interopra, és Excel telepítésre sem. Ha már rendelkezel egy worksheet példánnyal (`ws`), akkor készen állsz.

## 1. lépés: A japán kultúra beállítása (Convert Japanese Calendar Date)

Amikor egy olyan dátumot kapsz, mint a `"R02/05/01"` (Reiwa 2, május 1.), meg kell mondanod a .NET-nek, hogyan értelmezze az era szimbólumokat. A japán naptár nem az alapértelmezett gregorián naptár, ezért létrehozunk egy `CultureInfo`-t, amely a naptárát a `JapaneseCalendar`-ra cseréli.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Miért fontos ez:**  
Ha az alapértelmezett kultúrával próbálod meg a karakterláncot elemezni, a .NET formátum kivételt dob, mert nem tudja a `R` (a Reiwa era) szimbólumot évhez rendelni. A `JapaneseCalendar` használatával a parser megérti az era szimbólumokat, és a megfelelő gregorián évre konvertálja őket.

## 2. lépés: Az era‑alapú karakterlánc elemzése `DateTime`‑ra

Most, hogy a kultúra készen áll, biztonságosan meghívhatjuk a `DateTime.ParseExact`-ot. A formátum string `"ggyy/MM/dd"` a parsernek a következőket jelenti:

- `gg` – era jelölő (pl. `R` a Reiwa-hoz)  
- `yy` – kétjegyű év az erában  
- `MM/dd` – hónap és nap.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Pro tipp:** Ha más formátumú dátumokat is kaphatsz (pl. `"Heisei 30/12/31"`), tedd a parse-olást egy `try/catch` blokkba, és használj visszaesést `DateTime.TryParseExact`-re. Ez megakadályozza, hogy egyetlen hibás sor miatt az egész import feladat összeomoljon.

## 3. lépés: `DateTime` írása Excel cellába (Excel cella dátumérték)

Az Aspose.Cells egy .NET `DateTime`-ot natív Excel dátumként kezel, ha a `PutValue`-t használod. A könyvtár automatikusan átalakítja a tick-eket az Excel sorozatszámává (a napok száma 1900‑01‑00 óta). Ez azt jelenti, hogy a cella megfelelő **excel cell date value**-t jelenít meg, és később formázhatod az Excel beépített dátumstílusaival.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Mit fogsz látni Excelben:**  
A C1 cella most a `44796` sorozatszámot tartalmazza, amelyet az Excel `2020‑05‑01`‑ként jelenít meg (vagy bármilyen általad alkalmazott formátumban). A mögöttes érték valódi dátum, nem szöveg, így a rendezés a várt módon működik.

## 4. lépés: A munkafüzet mentése (Wrap‑Up)

Ha még nem mentetted a munkafüzetet, most tedd meg. Ez a lépés nem kifejezetten a dátum írásáról szól, de befejezi a munkafolyamatot.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Ennyi—négy tömör lépés, és sikeresen **write datetime to Excel**, közben kezelve egy japán era dátumot.

---

![dátum és idő írása Excel példája](/images/write-datetime-to-excel.png "Képernyőkép, amely egy C# projektet mutat, amely DateTime-ot ír az Excel C1 cellájába")

*A fenti kép illusztrálja a végső Excel fájlt, ahol a dátum helyesen jelenik meg a C1 cellában.*

## Gyakori kérdések és széljegyek

### Mi van, ha a worksheet változó még nincs készen?

Létrehozhatsz egy új munkafüzetet a futás közben:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Hogyan őrizhetem meg az eredeti japán era karakterláncot a lapon?

Ha mind az eredeti karakterláncra, mind a feldolgozott dátumra szükséged van, írd őket szomszédos cellákba:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Működik ez régebbi .NET verziókkal is?

Igen. A `JapaneseCalendar` már a .NET 2.0 óta létezik, és az Aspose.Cells támogatja a .NET Framework 4.5+. Csak győződj meg róla, hogy a megfelelő assembly-re hivatkozol.

### Mi a helyzet az időzónákkal?

`DateTime.ParseExact` **Kind** értéke `Unspecified`. Ha a forrásdátumok UTC-ben vannak, előbb konvertáld őket:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Beállíthatok egyedi dátumformátumot (pl. “yyyy年MM月dd日”)?

Természetesen. Használd a `Style.Custom` tulajdonságot:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Most az Excel `2020年05月01日`-et fog mutatni, miközben továbbra is egy valódi dátumértéket tárol.

## Összefoglaló

Áttekintettük mindazt, amire szükséged van a **write datetime to Excel** C#-ból:

1. **Configure** egy japán kultúrát a `JapaneseCalendar`-ral, hogy **convert Japanese calendar date** karakterláncokat alakítsa át.  
2. **Parse** az era‑alapú karakterláncot a `DateTime.ParseExact` segítségével.  
3. **Insert** a kapott `DateTime`-ot egy cellába, biztosítva a megfelelő **excel cell date value**-t.  
4. **Save** a munkafüzetet, hogy az adatok megmaradjanak.

Ezekkel a négy lépéssel biztonságosan **insert date into worksheet** tudsz végrehajtani, függetlenül a forrás formátumától. A kód teljesen futtatható, csak az Aspose.Cells-re van szükség, és bármely modern .NET futtatókörnyezetben működik.

## Mi a következő?

- **Bulk import:** Sorok bejárása egy CSV-ben, minden japán dátum elemzése, és egymás utáni cellákba írása.  
- **Styling:** Feltételes formázás alkalmazása a lejárt határidőkkel rendelkező dátumok kiemeléséhez.  
- **Performance:** `WorkbookDesigner` vagy `CellStyle` gyorsítótár használata, ha több ezer sorral dolgozol.  

Nyugodtan kísérletezz—cseréld le a japán erát a gregorián naptárra, módosítsd a célcellát, vagy exportálj más fájlformátumba (CSV, ODS). A lényeg ugyanaz: elemezd, konvertáld, és **write datetime to Excel** magabiztosan.

Boldog kódolást, és legyenek a táblázataid mindig helyesen rendezhetők!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}