---
category: general
date: 2026-03-30
description: Miként másolhatunk munkalapot C#-ban az Aspose.Cells használatával –
  lépésről‑lépésre útmutató, amely bemutatja a cellatartomány másolását, oszlopok
  másolását munkalapok között, a munkalap pivot táblájának másolását és új munkalap
  hozzáadásának kódját.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: hu
og_description: Tudja meg, hogyan másolhat munkalapot C#-ban az Aspose.Cells segítségével.
  Ez az útmutató bemutatja a cellatartomány másolását, a pivot táblák megőrzését,
  az oszlopok másolását lapok között, valamint az új munkalap hozzáadásának kódját.
og_title: Munkalap másolása C#-ban – Teljes Aspose.Cells útmutató
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hogyan másoljunk munkalapot C#-ban az Aspose.Cells segítségével – Teljes útmutató
url: /hu/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljuk a munkalapot C#-ban az Aspose.Cells segítségével – Teljes útmutató

Gondolkodtál már azon, **hogyan másoljunk munkalapot** C#-ban anélkül, hogy egyetlen pivot tábla vagy képlet is elveszne? Nem vagy egyedül – sok fejlesztő akad el, amikor egy lapot kell megkettőzni, miközben minden funkciót meg akar tartani. Ebben az útmutatóban egy gyakorlati, vég‑től‑végig megoldást mutatunk be, amely nem csak az adatokat másolja, hanem megőrzi a **copy worksheet pivot table**-t, kezeli a **copy cell range**-t, és bemutatja a szükséges **add new worksheet code**-ot.

Mindent lefedünk a forrás munkafüzet betöltésétől a célfájl mentéséig, így másolhatsz oszlopokat lapok között, megőrizheted az objektumokat, és tisztán tarthatod a kódod. Nincs homályos hivatkozás, csak egy teljes, futtatható példa, amelyet ma beilleszthetsz a projektedbe.

## Amit ez az útmutató lefed

- Létező Excel fájl betöltése az Aspose.Cells segítségével  
- A **add new worksheet code** használata a céllap létrehozásához  
- **copy cell range** definiálása, amely tartalmaz egy pivot táblát  
- **CopyOptions** beállítása a diagramok, képletek és pivot táblák érintetlenül tartásához  
- **copy columns between sheets** végrehajtása soronkénti pontossággal  
- Az eredmény mentése és annak ellenőrzése, hogy a munkalap helyesen másolódott-e  

A útmutató végére magabiztosan tudod majd megválaszolni a “how to copy worksheet” kérdést, legyen szó jelentések automatizálásáról vagy táblázat‑alapú felhasználói felület építéséről.

## Munkalap másolása – Áttekintés

Mielőtt a kódba merülnénk, vázoljuk fel a magas szintű folyamatot. Tekintsd úgy, mint egy receptet:

1. **Load** a forrás munkafüzet (`Source.xlsx`).  
2. **Add** egy új munkalapot a másolat tárolásához (`add new worksheet code`).  
3. **Define** a területet, amelyet meg szeretnél duplikálni (`copy cell range`).  
4. **Configure** a másolási beállításokat, hogy a pivot tábla megmaradjon (`copy worksheet pivot table`).  
5. **Copy** sorokat és oszlopokat (`copy columns between sheets`).  
6. **Save** az új munkafüzetet (`Destination.xlsx`).  

Ennyi—hat lépés, semmi varázslat. Minden lépést alább részletezünk kódrészletekkel és a mögöttes indoklással.

## 1. lépés – A forrás munkafüzet betöltése

Először is: szükséged van egy `Workbook` példányra, amely a másolni kívánt fájlra mutat. Ez a lépés elengedhetetlen, mivel az Aspose.Cells közvetlenül a fájlrendszerrel dolgozik, nem az Office felhasználói felületével.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Miért fontos:* A fájl betöltése egy memóriában létező reprezentációt hoz létre minden munkalapról, celláról és objektumról. Enélkül nincs mit másolni, és bármely későbbi `add new worksheet code` próbálkozás sikertelen lesz, mivel a forrásadatok nem állnak rendelkezésre.

## 2. lépés – Új munkalap hozzáadása (add new worksheet code)

Most szükségünk van egy helyre, ahová beilleszthetjük a másolt adatokat. Itt jön képbe a **add new worksheet code**. A lapot bármire elnevezheted; itt `"Copy"`-nek hívjuk.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tipp:* Ha több lapot szeretnél másolni, hívd meg a `Worksheets.Add`-ot egy ciklusban, és adj minden lapnak egyedi nevet. Így elkerülöd a névütközéseket, és rendezett marad a munkafüzet.

## 3. lépés – A másolási cellatartomány meghatározása

A **copy cell range** pontosan megmondja az Aspose.Cells-nek, mely sorokat és oszlopokat kell duplikálni. Sok valós esetben a tartomány pivot táblát is tartalmaz, ezért precíznek kell lennünk.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Miért szükséges:* A tartomány explicit megadásával elkerülöd a teljes lap másolását (ami pazarló lehet), és biztosítod, hogy a pivot tábla a másolt területen belül legyen. Ez a **how to copy worksheet** lényege, ha csak a lap egy részére van szükséged.

## 4. lépés – Másolási beállítások megadása (preserve copy worksheet pivot table)

Az Aspose.Cells egy `CopyOptions` objektumot biztosít, amely szabályozza, mi kerül beillesztésre. A pivot tábla, diagramok és képletek megőrzéséhez beállítjuk a `PasteType.All`-t és engedélyezzük a `PasteSpecial`-t.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Magyarázat:* A `PasteType.All` a legátfogóbb opció, míg a `PasteSpecial` azt mondja a motornak, hogy megfelelően kezelje a komplex objektumokat – például a pivot táblákat. Ennek a lépésnek a kihagyása gyakori hibaforrás; a másolt lap elveszíti interaktív funkcióit.

## 5. lépés – Sorok és oszlopok másolása (copy columns between sheets)

Most jön a nehéz munka: az adatok tényleges áthelyezése. A `CopyRows` és `CopyColumns` metódusokat fogjuk használni a **copy columns between sheets** kezelésére. Mindkettő alkalmazása biztosítja, hogy az egyesített cellák és oszlopszélességek megmaradjanak.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Mi történik:* A `CopyRows` soronként mozgatja az adatokat, míg a `CopyColumns` oszloponként. Mindkettő futtatása garantálja, hogy az egész téglalap alakú blokk duplikálva legyen, ami elengedhetetlen, ha **copy columns between sheets** kell, ahol a oszlopszélességek vagy rejtett oszlopok eltérnek.

## 6. lépés – A munkafüzet mentése

Végül írjuk vissza a változásokat a lemezre. Ez a lépés fejezi be a **how to copy worksheet** folyamatot.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Ellenőrzési tipp:* Nyisd meg a `Destination.xlsx`-t, és ellenőrizd, hogy a `"Copy"` lap azonosnak tűnik-e az eredetivel, a pivot táblák működnek-e, és az oszlopszélességek egyeznek-e. Ha valami nem stimmel, nézd át a `CopyOptions` beállításokat.

## Szélsőséges esetek és gyakori variációk

### Több munkalap másolása

Ha több lapot kell duplikálnod, csomagold be a fenti logikát egy `foreach` ciklusba:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Képletek megőrzése különböző munkafüzetek között

Ha a forrás és a cél munkafüzetek különböző névvel ellátott tartományokkal rendelkeznek, állítsd be a `copyOptions`-t `PasteType.Formulas`-ra az `All` mellett:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Nagy tartományok és teljesítmény

Nagy adathalmazok (több százezer sor) esetén fontold meg csak a `CopyRows` használatát, és hagyd ki a `CopyColumns`-t, ha az oszlopszélességek nem kritikusak. Ez néhány másodpercet takaríthat meg.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható program található, amely magában foglalja a megbeszélteket. Illeszd be egy konzolos alkalmazásba, állítsd be a fájlutakat, és nyomd meg az **F5**-öt.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Várható eredmény:** A `Destination.xlsx` megnyitása egy **Copy** nevű lapot mutat, amely tükrözi a `Source.xlsx` első lapját – beleértve a pivot táblákat, a formázást és az oszlopszélességeket. Az eredeti fájl érintetlen marad.

## Gyakran Ismételt Kérdések

**Q: Működik ez a .xlsx fájlokkal, amelyeket az Excel 2019 hozott létre?**  
A: Teljesen. Az Aspose.Cells támogatja az összes modern Excel formátumot, így ugyanaz a kód működik `.xlsx`, `.xlsm`, és még a régebbi `.xls` fájlok esetén is.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}