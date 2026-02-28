---
category: general
date: 2026-02-28
description: Gyorsan sorokat törölni Excel táblázatban C#-ban. Tanulja meg, hogyan
  adjon hozzá névvel ellátott tartományt Excelben, hogyan érje el a munkalapot név
  szerint, és hogyan kerüljön el a duplikált név hibákat.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: hu
og_description: Sorok törlése Excel táblázatból C#-vel. Ez a bemutató azt is megmutatja,
  hogyan lehet névvel ellátott tartományt hozzáadni Excelhez, és a munkalapot név
  alapján elérni.
og_title: Sorok törlése Excel táblázatban C#-al – Teljes útmutató
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Sorok törlése Excel táblázatból C#‑val – Lépésről lépésre útmutató
url: /hu/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sorok törlése Excel táblázatból C#-al – Teljes programozási útmutató

Valaha szükséged volt **delete rows excel table** törlésére egy munkafüzetből, de nem tudtad, melyik API hívást kell használni? Nem vagy egyedül – a legtöbb fejlesztő ugyanazzal a problémával szembesül, amikor először próbál programozottan csökkenteni egy táblázatot.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely nem csak az Excel táblázat sorait távolítja el, hanem bemutatja a **how to add defined name** (más néven *named range*) használatát, a **access worksheet by name** módszert, valamint azt, hogy miért dob `InvalidOperationException`-t egy másik lapon a duplikált név hozzáadása.  

A cikk végére képes leszel:

* Lefogni egy munkalapot a lapfül neve alapján.  
* Biztonságosan törölni az adat sorokat az adott lapon lévő első táblázatból.  
* Létrehozni egy névvel ellátott tartományt, amely egy adott címre mutat.  
* Megérteni a duplikált nevek problémáit a munkalapok között.

Nincs szükség külső dokumentációra – minden, amire szükséged van, itt található.

---

## Amire szükséged lesz

* **DevExpress Spreadsheet** (vagy bármely könyvtár, amely elérhetővé teszi a `Workbook`, `Worksheet`, `ListObject` és `Names` objektumokat).  
* .NET projekt, amely a **.NET 6** vagy újabb verziót célozza (a kód .NET Framework 4.8-ra is lefordítható).  
* Alapvető ismeretek C#-ban – ha tudsz `foreach` ciklust írni, már készen állsz.

> **Pro tip:** Ha a DevExpress ingyenes Community Edition-ét használod, az alább használt API-k megegyeznek a kereskedelmi verzióval.

## 1. lépés – Munkalap elérése név alapján

Az első dolog, amit tenned kell, megtalálni azt a lapot, amelyik a módosítani kívánt táblázatot tartalmazza.  
A legtöbb fejlesztő szokásból a `Worksheets[0]`-t használja, de ez a kódot a lap sorrendjéhez köti, és hibát okoz, amint valaki átnevezi a fület.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Miért fontos:* A lap **nevének** használatával az index helyett elkerülöd, hogy a munkafüzet változásakor véletlenül a rossz lapot módosítsd.  

Ha a megadott név nem létezik, a könyvtár `KeyNotFoundException`-t dob, amelyet elkapva barátságos hibaüzenetet jeleníthetsz meg.

## 2. lépés – Sorok törlése Excel táblázatból (Biztonságos módon)

Miután megvan a megfelelő munkalap, távolítsuk el az adat sorokat az első táblázatból.  
Gyakori hiba a `DeleteRows(1, rowCount‑1)` hívása. A **DevExpress 22.2** óta ez a túlterhelés **tiltott**, és `InvalidOperationException`-t dob. A könyvtár azt várja, hogy a sorokat a **táblázat adat tartományán** belül töröld, nem pedig a fejléc sorát.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Mi van, ha a táblázat üres?** Az `if` ellenőrzés megakadályozza a `rowCount = 0` hívást, amely egyébként kivételt eredményezne.

### Vizualizáció  

![sorok törlése excel táblázat példában](image.png "Képernyőkép, amelyen látható, hogy sorok kerülnek eltávolításra egy Excel táblázatból")  

*Alt szöveg: delete rows excel table example in C# code*

## 3. lépés – Hogyan adjunk hozzá definiált nevet (Névvel ellátott tartomány létrehozása)

A táblázat megtisztítása után később egy adott tartományra szeretnél hivatkozni – például egy diagramhoz vagy adatérvényesítési listához. Itt jön képbe a **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

A `Names.Add` metódus két paramétert vár: az azonosítót és az A1‑stílusú címet.  
Mivel korábban **access worksheet by name**-t használtunk, a cím karakterlánc biztonságosan hivatkozhat bármely lapra anélkül, hogy az indexváltozások miatt aggódnunk kellene.

## 4. lépés – Névvel ellátott tartomány egy másik lapon – Duplikált név hibák elkerülése

Azt gondolhatod, hogy ugyanazt az azonosítót újra felhasználhatod egy másik lapon, például így:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Sajnos az Excel névterének hatóköre **munkafüzet‑szintű**, nem laponkénti. A fenti hívás `InvalidOperationException`-t vált ki a *„A name with the same identifier already exists.”* üzenettel.

### Hogyan kerülhetjük el

1. **Válassz egy egyedi nevet** (`MyTable_Sheet2`).  
2. **Töröld a meglévő nevet** a újbóli hozzáadás előtt (csak ha valóban fel akarod cserélni).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

## Teljes, futtatható példa

Mindent összerakva, itt egy önálló konzolalkalmazás, amelyet beilleszthetsz a Visual Studio-ba, és futtathatsz egy `sample.xlsx` mintafájl ellen.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Várható eredmény**

* Az első táblázat összes adat sora a **Sheet1**-en eltűnik, csak a fejléc sor marad.  
* A **MyTable** név most a `Sheet1!$A$1:$C$5` címre mutat.  
* A második név, **MyTable_Sheet2**, biztonságosan hivatkozik egy tartományra a **Sheet2**-n, anélkül, hogy kivételt dobna.

## Gyakori kérdések és szélhelyzetek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a munkafüzetnek több táblázata van?* | Szerezd meg a megfelelő `ListObject`-et index szerint (`worksheet.ListObjects[1]`) vagy név szerint (`worksheet.ListObjects["MyTable"]`). |
| *Törölhetek sorokat egy olyan táblázatból, amely több munkalapot is átfog?* | Nem – a táblázatok egyetlen munkalapra korlátozódnak. A törlési logikát minden lapra újra kell alkalmazni. |
| *Van mód csak egy részhalmaz sorok törlésére?* | Igen – használd a `table.DeleteRows(startRow, count)` metódust, ahol a `startRow` a táblázat adat területén belül nullától indul. |
| *Megmaradnak a névvel ellátott tartományok mentés után?* | Természetesen. Miután meghívod a `SaveDocument`-ot, a nevek a munkafüzet XML részévé válnak. |
| *Hogyan listázhatom ki az összes definiált nevet a munkafüzetben?* | Iteráld a `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`-t. |

## Összegzés

Áttekintettük a **delete rows excel table** használatát C#-ban, bemutattuk a **add named range excel**-t, és megmutattuk a helyes **access worksheet by name** módszert, miközben elkerültük a rettegett duplikált név kivételt.  

A teljes megoldás a fenti kódrészletben található – másold, illeszd be, és futtasd a saját fájljaidon. Innen tovább bővítheted a logikát több táblázat kezelésére, dinamikus tartomány számításokra, vagy akár UI-val való integrálásra.  

**Következő lépések**, amelyeket érdemes felfedezni:

* **named range on another sheet** használata diagram sorozatok meghajtásához.  
* A törlési logikát kombináld a **ExcelDataReader**-rel, hogy adatot importálj a tisztítás előtt.  
* Automatizáld a tucatnyi munkafüzet tömeges frissítését egy egyszerű `foreach (var file in Directory.GetFiles(...))` ciklussal.

Van még kérdésed az Excel automatizálásról C#-ban? Hagyj megjegyzést, és folytassuk a beszélgetést. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}