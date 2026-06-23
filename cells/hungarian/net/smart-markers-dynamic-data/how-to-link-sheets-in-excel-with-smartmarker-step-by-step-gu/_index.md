---
category: general
date: 2026-06-08
description: Hogyan kapcsoljuk össze az Excel munkalapokat a SmartMarkerProcessor
  segítségével mester‑részlet jelentésekhez. Töltsük fel a mester munkalapot, és könnyedén
  generáljunk mester‑részlet Excel jelentést.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: hu
og_description: Hogyan kapcsoljunk össze munkalapokat az Excelben a SmartMarkerProcessor
  használatával. Tanulja meg, hogyan töltsön fel egy főmunkalapot, és percek alatt
  készítsen egy fő‑részlet jelentést.
og_title: Hogyan kapcsoljunk össze lapokat az Excelben a SmartMarkerrel – Lépésről
  lépésre
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Hogyan kapcsoljunk össze munkalapokat az Excelben a SmartMarkerrel – Lépésről
  lépésre útmutató
url: /hu/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kapcsoljunk össze munkalapokat Excelben a SmartMarkerrel – Lépésről‑lépésre útmutató

Gondoltad már valaha, **hogyan kapcsoljunk össze munkalapokat** Excelben anélkül, hogy kézzel másolnád a sorokat vagy végtelen VBA ciklusokat írnál? Nem vagy egyedül. A legtöbb fejlesztő akadályba ütközik, amikor egy tiszta master‑detail jelentésre van szüksége, amely szinkronban marad az adatok változásával. A jó hír? A SmartMarkerProcessor elvégzi a nehéz munkát helyetted, néhány C# sorból teljes funkcionalitású master‑detail munkafüzetet készít.

Ebben a bemutatóban végigvezetünk a pontos lépéseken, hogy **feltöltsd a master munkalapot**, beállítsd a részlet munkalapot, és végül **generálj master‑detail jelentést**, amely automatikusan frissül. A végére egy újrahasználható mintát kapsz, amelyet bármely .NET projektbe beilleszthetsz.

> **Előfeltétel megjegyzés:** Szükséged van a GrapeCity Documents for Excel (GcExcel) 2024 vagy újabb verziójára, egy .NET fejlesztői környezetre (a Visual Studio 2022 remekül működik), és alapvető C# ismeretekre. A GcExcel‑en kívül nem szükséges további NuGet csomag.

---

## A megoldás áttekintése

Mielőtt a kódba merülnénk, bontsuk le, mit jelent a „munkalapok összekapcsolása” a SmartMarker kontextusában:

1. **Master sheet** – Egy sor egy entitáshoz (pl. ügyfelek listája).
2. **Detail sheet** – Sorok, amelyek egy master sorhoz tartoznak (pl. megrendelések minden ügyfélhez).
3. **SmartMarker szintaxis** – Egy apró jelölőnyelv (`{MasterSheet}#master;{DetailSheet}#detail`), amely megmondja a processzornak, hogyan kössön össze két adat táblát.
4. **Processzor beállítások** – A `MasterDetail` engedélyezése automatikusan megismétli a master sorokat, és beágyazza a kapcsolódó detail sorokat alá.

Ezeknek a részeknek a megértése segít a megközelítés későbbi finomhangolásában – lehet, hogy háromszintű beágyazásra vagy feltételes formázásra van szükséged. Tartsd ezt a mentális modellt kéznél, miközben végigvezetünk a megvalósításon.

## 1. lépés: Hierarchikus adatok előkészítése a Master‑Detail feldolgozáshoz

Az első dolog, amire szükséged van, egy adatforrás, amely tükrözi a master‑detail kapcsolatot. A legtöbb valós helyzetben ez egy adatbázisból származik, de a tisztaság kedvéért egy névtelen objektumliterált használunk.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Miért fontos ez:** A SmartMarker nem varázslatosan találja ki a kapcsolatokat; a megfelelő tulajdonnév (`MasterId` → `Id`) alapján keres. Az adatok ilyen struktúrába rendezésével egyértelmű térképet adunk a processzornak, ami a **hogyan kapcsoljunk össze munkalapokat** hatékony megvalósításának alappillére.

> **Pro tipp:** Ha az adataid `DataTable` objektumokban élnek, egyszerűen tedd elérhetővé őket azonos nevű tulajdonságokként – a SmartMarker bármely enumerálható gyűjteménnyel működik.

## 2. lépés: Munkafüzet létrehozása és sablon betöltése

A SmartMarker egy meglévő Excel munkafüzet ellen dolgozik, általában egy sablon, amely már tartalmazza a munkalap neveket és a helyőrző jelölőket. Hozzunk létre egy munkafüzetet memóriában, és adjunk hozzá két üres munkalapot *MasterSheet* és *DetailSheet* néven.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Betölthetsz egy `.xlsx` fájlt a lemezről is (`wb.Open("Template.xlsx")`), ha előbb szeretnéd megtervezni a layoutot Excelben. A fontos rész az, hogy a munkalap nevek megegyezzenek azokkal, amelyeket a SmartMarker karakterláncban hivatkozol.

## 3. lépés: SmartMarkerProcessor példányosítása és a Master‑Detail mód engedélyezése

Most behozzuk a motort, amely beolvassa a jelölőket és beilleszti az adatokat. A `SmartMarkerProcessor` a munkafüzetet kapja konstruktorparaméterként, és a `Options.MasterDetail` jelző azt mondja meg, hogy a `#master` és `#detail` jelölőket összekapcsolt pároként kezelje.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Miért engedélyezzük a `MasterDetail`‑t?** Enélkül a jelző nélkül a processzor a `{MasterSheet}#master` és `{DetailSheet}#detail` műveleteket függetlenül kezeli, elveszítve a sorok közötti kritikus kapcsolatot. A jelző beállítása az egyetlen sor, amely a **hogyan kapcsoljunk össze munkalapokat** ténylegesen működésre képes.

## 4. lépés: SmartMarker karakterlánc definiálása és a processzor futtatása

A jelölő karakterlánc megmondja a SmartMarkernek, melyik munkalap a master és melyik a detail. A szintaxis egyszerű: `{SheetName}#master;{SheetName}#detail`. Hozzáadhatsz további jelölőket (pl. `#header`), de egy alap jelentéshez ezek nem szükségesek.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Amikor a `Process` fut, a motor:

1. Az *MasterSheet*-be ír minden master sort, a fejléc után az első üres sorból kezdve.
2. Minden master sorhoz átvizsgálja a `Details` gyűjteményt, kiválasztja azokat a sorokat, ahol a `MasterId` egyezik a master `Id`‑vel, és közvetlenül a megfelelő master bejegyzés alá írja őket a *DetailSheet*-be.

## 5. lépés: Az eredményül kapott munkafüzet mentése vagy exportálása

Ezen a ponton egy teljesen feltöltött munkafüzeted van. Mentheted lemezre, streamelheted vissza egy webkliensnek, vagy akár PDF‑re konvertálhatod is.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Nyisd meg a fájlt, és két munkalapot látsz: a *MasterSheet* listázza az `A` és `B` elemeket, míg a *DetailSheet* a `Item1`‑et a 1‑es master alatt és a `Item2`‑t a 2‑es master alatt mutatja. Ez a **master munkalap feltöltése** és a **master‑detail jelentés generálása** lényege egy lépésben.

## Visual Overview

![Diagram, amely bemutatja, hogyan kapcsoljunk össze munkalapokat Excelben a SmartMarkerProcessor használatával](https://example.com/diagram.png "Munkalapok összekapcsolásának diagramja")

A diagram (az alt szöveg tartalmazza a fő kulcsszót) a C# objektumok → SmartMarkerProcessor → összekapcsolt Excel munkalapok adatáramlását mutatja.

## Gyakori edge case‑ek kezelése

### Több részlet sor egy masterhez

Ha egy master sor több kapcsolódó részlettel rendelkezik, a SmartMarker egyszer írja a master sort, majd *az összes* egyező részlet sort alá. Nem szükséges extra kód – csak győződj meg róla, hogy a `Details` gyűjtemény tartalmazza az összes sort.

### Hiányzó részletek

Amikor egy master bejegyzésnek nincs megfelelő részlet sora, a részlet munkalap egyszerűen kihagyja azt a szekciót. Ha helyőrzőre van szükséged (pl. „Nincsenek elemek”), hozzáadhatsz egy számított oszlopot a sablonban, amely egy Excel képletet használ, például `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Nagy adathalmazok

Több tízezer sor feldolgozása memóriaigényes lehet. A teljesítmény fenntartásához:

- Használd a `processor.Options.EnableStreaming = true` beállítást (elérhető a GcExcel 2025+ verzióban).
- Törd fel az adatokat darabokra, és minden darabot külön dolgozz fel, majd egyesítsd a munkafüzeteket.

### Egyedi oszlop leképezés

Ha a tulajdonnév nem egyezik (`MasterKey` vs `Id`), a `SmartMarkerProcessor.Map` metódussal alias‑t hozhatsz létre a feldolgozás előtt.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## Teljes működő példa

Mindent összerakva, itt egy komplett, másolás‑beillesztésre kész program, amelyet azonnal futtathatsz.

```csharp
using System;
using GrapeCity.Documents.Excel;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare hierarchical data
            var sampleData = new
            {
                Master = new[]
                {
                    new { Id = 1, Name = "A" },
                    new { Id = 2, Name = "B" }
                },
                Details = new[]
                {
                    new { MasterId = 1, Item = "Item1" },
                    new { MasterId = 1, Item = "Item1‑Extra" },
                    new { MasterId = 2, Item = "Item2" }
                }
            };

            // 2️⃣ Create workbook and template sheets
            IWorkbook wb = new Workbook();

            var master = wb.Worksheets.Add("MasterSheet");
            master.Range["A1"].Value


## Mit érdemes még megtanulni?

A következő bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Mester külső hivatkozás képletek Excelben Aspose.Cells for Java használatával](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Dinamikus Excel munkalapok Java-ban az Aspose.Cells‑vel: Átfogó útmutató](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dinamikus Excel jelentések Aspose.Cells Java‑val: Névtér és összetett képletek](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}