---
category: general
date: 2026-10-01
description: Ismerje meg, hogyan adhat hozzá egyéni tulajdonságokat egy Excel munkafüzethez
  az Aspose.Cells használatával. Ez az útmutató bemutatja, hogyan adhat hozzá projektazonosítót,
  és hogyan olvashatja az egyéni tulajdonságokat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: hu
lastmod: 2026-10-01
og_description: Egyéni tulajdonságok hozzáadása egy Excel munkafüzethez az Aspose.Cells
  segítségével. Kövesse ezt a teljes útmutatót, hogy projektazonosítót adjon hozzá,
  beállítsa a lektor adatait, és programozottan olvassa ki az egyéni tulajdonságokat.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Egyéni tulajdonságok hozzáadása az Excel munkafüzethez – lépésről lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan adjunk hozzá egyéni tulajdonságokat egy Excel munkafüzethez
url: /hu/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan adjunk hozzá egyéni tulajdonságokat egy Excel munkafüzethez

Ha **egyéni tulajdonságokat** kell hozzáadni egy Excel munkafüzethez, ez az útmutató pontosan megmutatja, hogyan teheted meg az Aspose.Cells for .NET segítségével. Emellett megtanulod, hogyan adj hozzá egy projektazonosítót, állíts be egy ellenőrző nevet, és később **visszaolvasd az egyéni tulajdonságokat** a fájlból.

Az egyéni metaadatok használatával üzleti szempontból specifikus információkat ágyazhatsz be közvetlenül a táblázatba, így egyszerűen nyomon követheted a tulajdonjogot, verziót vagy bármilyen más kontextust anélkül, hogy külön adatbázist kellene fenntartani. Az alábbi lépések a teljes vég‑től‑végig munkafolyamatot fedik le, a munkafüzet létrehozásától az új tulajdonságok mentéséig.

## Előkövetelmények

Mielőtt elkezdenéd, győződj meg róla, hogy rendelkezel:

* .NET 6.0 vagy újabb telepítve  
* Érvényes Aspose.Cells for .NET licenc (vagy ingyenes próba)  
* Visual Studio 2022 (vagy bármely C# IDE)  

Nem szükséges további NuGet csomag a `Aspose.Cells`-en kívül.

## 1. lépés: A projekt beállítása és névterek importálása

Create a new console application and add the Aspose.Cells reference:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Az `Aspose.Cells` névtér tartalmazza a `Workbook`, `Worksheet` és `CustomPropertyCollection` osztályokat, amelyeket használni fogunk.

## 2. lépés: Létező munkafüzet betöltése (vagy új létrehozása)

Kezdhetsz egy meglévő `.xlsb` fájllal, vagy létrehozhatsz egy új munkafüzetet. Az alábbi példa betölt egy **Data.xlsb** nevű fájlt, amely a `YOUR_DIRECTORY` mappában található.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Ha a fájl nem létezik, cseréld le a kódot `new Workbook();`-ra egy üres munkafüzet létrehozásához.

## 3. lépés: Egyéni tulajdonságok hozzáadása az első munkalaphoz

Az elsődleges művelet a **egyéni tulajdonságok** hozzáadása egy munkalaphoz. Az Aspose.Cells egy gyűjteményben tárolja az egyéni tulajdonságokat, amely úgy viselkedik, mint egy szótár.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Azért használjuk a `CustomProperties.Add`-t a `CustomProperties["Name"] = value` helyett, mert az `Add` metódus létrehozza a bejegyzést, ha az nem létezik, és garantálja, hogy a megfelelő adat típus kerül tárolásra. Ez a megközelítés megakadályozza a véletlen típuseltéréseket, amelyek később futásidejű hibákat okozhatnak az értékek olvasásakor.

## 4. lépés: A munkafüzet mentése az új tulajdonságokkal

Miután beillesztetted a metaadatokat, mentse el a változásokat egy új fájlba, hogy az eredeti érintetlen maradjon.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Ekkor az Excel fájl tartalmazza a definiált egyéni metaadatokat. A tulajdonságokat a következő szakaszban leírt lépésekkel ellenőrizheted.

## 5. lépés: Egyéni tulajdonságok olvasása egy munkafüzetből

Az **excel egyéni tulajdonságok** olvasása ugyanazt a gyűjtemény mintát követi. Ez a kódrészlet bemutatja, hogyan lehet lekérni a most tárolt értékeket.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

A `CustomPropertyCollection` indexelő egy `CustomProperty` objektumot ad vissza; a `Value` tulajdonság elérése az eredeti típusban tárolt adatot adja. A `null` ellenőrzése átalakítás előtt elkerüli a `NullReferenceException`-t, ha egy tulajdonság hiányzik.

### Várt konzolkimenet

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Az időbélyeg a 3. lépésben meghívott `Add` pontos időpontját fogja mutatni.

## Pro tipp: Létező egyéni tulajdonság frissítése

Ha később **egyéni információt szeretnél hozzáadni** (például a felülvizsgáló megváltoztatása), használd a `CustomPropertyCollection` beállítót:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Ez a minta biztosítja, hogy a tulajdonság frissítve vagy létrehozva legyen, ami hasznos iteratív munkafolyamatokban, például automatizált jelentéskészítésnél.

## 6. lépés: A tulajdonságok ellenőrzése Excelben (opcionális)

1. Nyisd meg a mentett `DataWithProps.xlsb` fájlt a Microsoft Excelben.  
2. Lépj a **Fájl → Info → Tulajdonságok → Speciális tulajdonságok** menüpontra.  
3. Válaszd ki a **Egyéni** fület.  

Láthatod a `ProjectId`, `Reviewer` és `CreatedOn` bejegyzéseket a megfelelő értékekkel.

## Teljes működő példa

Az alábbiakban a teljes, önálló program látható, amely egyesíti az összes korábbi kódrészletet. Másold be a `Program.cs` fájlba és futtasd; a konzol megjeleníti a lekért értékeket.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

A program futtatása előállítja a korábban bemutatott konzolkimenetet, és létrehozza a `DataWithProps.xlsb` fájlt, amely a beágyazott metaadatokat tartalmazza.

## Gyakori kérdések és szélhelyzetek

| Question | Answer |
|---|---|
| **Tárolhatok nem primitív típusokat?** | Az Aspose.Cells támogatja a `string`, `int`, `double`, `DateTime` és `bool` típusokat. Összetett objektumok esetén először sorosítsd őket JSON vagy XML formátumba, majd tárold a stringet. |
| **Mi van, ha a munkafüzet jelszóval védett?** | Nyisd meg a munkafüzetet jelszóval (`new Workbook(path, password)`) a `CustomProperties` elérése előtt. A tulajdonságok a feloldás után is elérhetők. |
| **Megmaradnak az egyéni tulajdonságok formátumkonverzió során?** | Különböző formátumba (például `.xlsx`) mentéskor az Aspose.Cells megőrzi az egyéni tulajdonságokat, amennyiben a célformátum támogatja őket. |
| **Hogyan töröljek egy egyéni tulajdonságot?** | Használd a `worksheet.CustomProperties.Remove("PropertyName");` metódust. Ez eltávolítja a bejegyzést a gyűjteményből. |

## Következő lépések

Most, hogy ismered az **egyéni tulajdonságok hozzáadását**, érdemes megismerned a kapcsolódó témákat, például:

* **excel custom properties** a dokumentum verziókezeléshez  
* **read custom properties** több munkalapról egyetlen munkafüzetben  
* **Aspose.Cells** használata pivot táblák létrehozásához, amelyek az egyéni metaadatokra hivatkoznak  
* A munkafüzet PDF‑be exportálása az egyéni tulajdonságok megőrzése mellett  

Kísérletezz különböző adat típusokkal, kombináld az egyéni tulajdonságokat a cella megjegyzésekkel, vagy integráld a metaadatokat egy nagyobb dokumentumkezelő rendszerbe.

---

**Készen állsz az Excel jelentésed automatizálására?** Add hozzá a fenti kódot a projektedhez, igazítsd a tulajdonságneveket az üzleti igényeidhez, és egy önleíró táblázatod lesz, amely készen áll a további feldolgozásra.

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel munkafüzet létrehozása – Egyéni tulajdonságok hozzáadása és mentés XLSB‑ként](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Hogyan érhetők el egyéni dokumentumtulajdonságok Excelben az Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Excel egyéni tulajdonságok elsajátítása az Aspose.Cells .NET segítségével a fejlett adatkezeléshez](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}