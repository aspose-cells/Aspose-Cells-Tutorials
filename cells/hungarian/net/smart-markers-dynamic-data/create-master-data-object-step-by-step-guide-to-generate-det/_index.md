---
category: general
date: 2026-02-14
description: Hozzon létre master adatobjektumot C#-ban, és generáljon részletes lapot
  könnyedén. Ismerje meg a teljes SmartMarker munkafolyamatot gyakorlati kódrészletekkel.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: hu
og_description: Hozzon létre mesteradat-objektumot C#‑ban, és generáljon részletes
  lapot a SmartMarkerrel. Kövesse részletes útmutatónkat egy azonnal futtatható megoldásért.
og_title: Mesteradat-objektum létrehozása – Teljes útmutató
tags:
- C#
- SmartMarker
- Excel Automation
title: Mesteradat-objektum létrehozása – Lépésről lépésre útmutató a részletes lap
  generálásához
url: /hu/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mesteradat-objektum létrehozása – Teljes útmutató

Szükséged volt már **mesteradat-objektum** létrehozására egy Excel munkalaphoz, de nem tudtad, hogyan kössük össze egy SmartMarker részletlapra? Nem vagy egyedül. Sok jelentéskészítési helyzetben a mesterobjektum hajt egy dinamikus részletlapot, és a helyes összekötés olyan, mintha egy képet nélküli kirakós darabjait próbálnád összeilleszteni.  

Ebben az útmutatóban végigvezetünk a teljes folyamaton – a mesteradat-objektum felépítésén, a SmartMarker beállításainak konfigurálásán a **részletlap generálásához**, majd a processzor elindításán. A végére egy futtatható kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz, amely a GrapeCity Documents for Excel (GcExcel) könyvtárat használja.

## Amire szükséged lesz

- .NET 6+ (vagy .NET Framework 4.7.2) a `GcExcel.dll` hivatkozással
- Alapvető C# ismeretek (változók, anonim típusok, objektum‑inicializálók)
- Egy Excel munkafüzet, amely már tartalmaz SmartMarker címkéket, például `{{OrderId}}`, és egy táblázatot a sorokhoz
- Visual Studio, Rider vagy bármely kedvelt szerkesztő

Ennyi – nincs szükség extra NuGet csomagokra a GcExcel alapdisztribúcióján kívül.

## 1. lépés: A mesteradat-objektum létrehozása

Az első dolog, amit meg kell tenned, hogy **mesteradat-objektumot** hozol létre, amely tükrözi a SmartMarker címkék által elvárt struktúrát. Tekintsd ezt egy kis, memóriában lévő jelentésmodellnek.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Miért használunk itt anonim típust? Mert lehetővé teszi egy könnyű tároló definiálását anélkül, hogy teljes osztályt kellene deklarálni – tökéletes gyors demókhoz vagy ha a forma valószínűleg nem változik. Ha később újrahasználható modellt szeretnél, egyszerűen cseréld le a `var`-t egy megfelelő POCO‑ra.

> **Pro tipp:** A tulajdonnév (`OrderId`, `Product`, `Quantity`) legyen pontosan megegyező a munkalapodban lévő helyőrzőkkel; a SmartMarker kis‑ és nagybetűket figyelmen kívül hagyva egyeztet.

## 2. lépés: SmartMarker beállítások konfigurálása a részletlap generálásához

Most megmondjuk a SmartMarkernek, hogy külön munkalapot szeretnénk a sor‑tétel táblázathoz. Itt jön képbe a **generate detail sheet** kulcsszó.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

A `DetailSheetNewName` minta kapcsos‑zárójelezett helyőrzőket használ, amelyeket futásidőben helyettesít. A példánkban a lap neve `Order_1` lesz. Ha később több megrendelésen iterálsz, mindegyik saját fület kap – pontosan ahogy a legtöbb könyvelő elvárja.

## 3. lépés: A SmartMarker processzor futtatása

Az adatok és a beállítások készen állnak, az utolsó lépés a processzor meghívása a célmunkalapon.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

A háttérben a SmartMarker átvizsgálja a munkalapot a címkékért, beilleszti az `orderData` értékeket, és mivel a `DetailSheet` `true`, a sablont egy új, `Order_1` nevű lapra másolja. Minden sor‑tétel megjelenik a részletterületen, megőrizve a sablonban alkalmazott formázást.

### Teljes, működő példa

Az alábbi önálló konzolprogram megnyit egy sablon‑munkafüzetet (`Template.xlsx`), végrehajtja a három lépést, és elmenti az eredményt `Result.xlsx` néven. Másold be egy új konzolprojektbe, és nyomd meg az **F5**‑öt.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Várt kimenet

- **Result.xlsx** tartalmaz egy `Order_1` nevű lapot.
- Az `A1` (vagy ahol elhelyezted a `{{OrderId}}`‑t) most `1`‑et mutat.
- Egy, a SmartMarker blokkot követő táblázat két sort listáz:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Ha megnyitod a fájlt, látni fogod, hogy a sablon formázása megmaradt – szegélyek, betűtípusok, feltételes formázás – minden érintetlen.

## Gyakori kérdések és széljegyek

### Mi van, ha több megrendelésem van?

Tedd a mesterobjektumot egy gyűjteménybe, és a SmartMarker automatikusan iterál:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Minden megrendelés saját lapot hoz létre (`Order_1`, `Order_2`, …). A processzor a külső tömböt tekinti a mestergyűjteménynek.

### Hogyan szabályozhatom a lap pozícióját?

Állítsd be a `smartMarkerOptions.DetailSheetInsertIndex = 2;`‑t, hogy az új lap a második fül után kerüljön, vagy használd a `DetailSheetInsertAfter = "Summary"`‑t, hogy egy név szerint megadott lap után szúrja be.

### Kikapcsolhatom a részletlapot egy adott futtatásnál?

Egyszerűen állítsd `DetailSheet = false;`‑ra. Ebben az esetben a SmartMarker a sor‑tétel adatokat ugyanabban a lapban írja, ahol a mestercímkék találhatók.

### Mi a helyzet a nagy adathalmazokkal?

A SmartMarker hatékonyan streameli az adatokat, de ha néhány százezrenél több sort próbálsz beilleszteni, elérheted az Excel 1 048 576 soros korlátját. Ilyenkor oszd fel az adatot több mesterrekordra, vagy fontold meg a CSV‑exportálást.

## Vizuális áttekintés

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*A diagram a folyamatot mutatja: C# mesterobjektum → SmartMarker beállítások → munkalap feldolgozás → új részletlap.*

## Összegzés

Most már tudod, hogyan **hozd létre a mesteradat-objektumot** C#‑ban, és hogyan konfiguráld a SmartMarker‑t a **részletlap automatikus generálásához**. A háromlépéses minta – adat, beállítás, processzor – lefedi a legtöbb Excel‑automatizálási szituációt a GcExcel‑el.  

Innen tovább felfedezheted:

- Fejléc/lábléc adatok hozzáadása minden részletlaphoz
- Feltételes formázás használata a megrendelés állapota alapján
- A generált munkafüzet PDF‑ként való exportálása a `workbook.SaveAsPdf(...)`‑val

Kísérletezz, törj el dolgokat, majd hozd vissza őket a helyükre. Ez a leggyorsabb út a munkalap‑automatizálás elsajátításához. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}