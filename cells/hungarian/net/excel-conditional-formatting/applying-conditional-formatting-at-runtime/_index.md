---
title: Feltételes formázás alkalmazása futásidőben az Excelben
linktitle: Feltételes formázás alkalmazása futásidőben az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből az átfogó, lépésenkénti útmutatóból megtudhatja, hogyan alkalmazhat feltételes formázást futás közben az Excelben az Aspose.Cells for .NET segítségével.
weight: 11
url: /hu/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Feltételes formázás alkalmazása futásidőben az Excelben

## Bevezetés

hatékony eszközök az adatok elemzéséhez és megjelenítéséhez. Az Excel egyik kiemelkedő funkciója a feltételes formázás, amely lehetővé teszi a felhasználók számára, hogy az értékek alapján meghatározott formázási stílusokat alkalmazzanak a cellákban. Ez megkönnyítheti a trendek azonosítását, a fontos adatpontok kiemelését, vagy egyszerűen olvashatóbbá teheti az adatokat. Ha programozottan szeretné megvalósítani a feltételes formázást Excel-fájljaiban, akkor jó helyen jár! Ebben az útmutatóban bemutatjuk, hogyan alkalmazhat feltételes formázást futás közben az Aspose.Cells for .NET használatával.

## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjünk meg arról, hogy mindennel rendelkezünk, ami a kezdéshez szükséges:

1. Visual Studio: Győződjön meg arról, hogy a Visual Studio telepítve van a gépen. Bármilyen verziót használhat, amely támogatja a .NET fejlesztést.
2.  Aspose.Cells for .NET: telepíteni kell az Aspose.Cells for .NET programot. Letöltheti a[Aspose honlapja](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: A C# programozás ismerete segít jobban megérteni a kódrészleteket.
4. .NET-keretrendszer: Győződjön meg arról, hogy projektje a .NET-keretrendszer kompatibilis verzióját célozza meg.

Most, hogy megvannak az előfeltételek, ugorjunk a szórakoztató részre!

## Csomagok importálása
Az Aspose.Cells használatának megkezdéséhez importálnia kell a szükséges névtereket a C#-projektbe. Ezt a következőképpen teheti meg:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ezek a névterek hozzáférést biztosítanak az Excel-fájlok kezeléséhez és a feltételes formázás alkalmazásához szükséges osztályokhoz és metódusokhoz.

Most bontsuk fel a feltételes formázás alkalmazásának folyamatát kezelhető lépésekre.

## 1. lépés: Állítsa be projektjét
Először is létre kell hoznia egy új C#-projektet a Visual Studióban. Íme, hogyan:

1. Nyissa meg a Visual Studio-t, és válassza a Fájl > Új > Projekt lehetőséget.
2. Válassza a Konzolalkalmazást (.NET-keretrendszer), és adjon nevet a projektnek.
3. Kattintson a Létrehozás gombra.

## 2. lépés: Adja hozzá az Aspose.Cells Reference fájlt
A projekt beállítása után hozzá kell adni egy hivatkozást az Aspose.Cells könyvtárhoz:

1. Kattintson a jobb gombbal a projektre a Solution Explorerben.
2. Válassza a NuGet-csomagok kezelése lehetőséget.
3. Keresse meg az Aspose.Cells elemet, és telepítse.

Ez lehetővé teszi az Aspose.Cells könyvtár által biztosított összes funkció használatát.

## 3. lépés: Hozzon létre egy munkafüzet-objektumot
Ezután hozzunk létre egy új munkafüzetet és egy munkalapot. Itt történik minden varázslat:

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Ebben a lépésben meghatározzuk azt a könyvtárat, ahová az Excel-fájlunk mentésre kerül, létrehozunk egy új munkafüzetet, és elérjük az első munkalapot.

## 4. lépés: Feltételes formázás hozzáadása
Most adjunk hozzá néhány feltételes formázást. Kezdjük egy üres feltételes formázási objektum létrehozásával:

```csharp
// Üres feltételes formázást ad hozzá
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Itt egy új feltételes formázási gyűjteményt adunk a munkalapunkhoz, amely tartalmazza a formázási szabályainkat.

## 5. lépés: Határozza meg a formátumtartományt
Ezután meg kell adnunk a cellák tartományát, amelyekre a feltételes formázás vonatkozik. Tegyük fel, hogy formázni szeretnénk az első sort és a második oszlopot:

```csharp
// Beállítja a feltételes formátumtartományt.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Ebben a kódban két területet határozunk meg a feltételes formázáshoz. Az első terület a (0,0), a második pedig az (1,1) cellához tartozik. Nyugodtan állítsa be ezeket a tartományokat egyedi igényei szerint!

## 6. lépés: Adjon hozzá feltételes formázási feltételeket
Itt az ideje, hogy meghatározzuk a formázás feltételeit. Tegyük fel, hogy értékeik alapján szeretnénk kiemelni a cellákat:

```csharp
// Feltételt ad hozzá.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Feltételt ad hozzá.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 Ebben a lépésben két feltételt adunk hozzá: egyet a közötti értékekhez`A2` és`100` , egy másik pedig a közötti értékekhez`50` és`100`. Ez lehetővé teszi a cellák dinamikus kiemelését azok értékei alapján.

## 7. lépés: Állítsa be a formázási stílusokat
Feltételeinkkel most már beállíthatjuk a formázási stílusokat. Változtassuk meg a háttérszínt a feltételeinknek megfelelően:

```csharp
// Beállítja a háttérszínt.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Itt az első feltétel háttérszínét pirosra állítjuk. Ezt tovább szabhatja a betűszín, a szegélyek és más stílusok szükség szerinti módosításával!

## 8. lépés: Mentse el az Excel fájlt
Végre itt az ideje megmenteni a munkánkat! A munkafüzetet a megadott könyvtárba mentjük:

```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```

Ez a kódsor menti az Excel-fájlt az alkalmazott feltételes formázással. Ügyeljen arra, hogy ellenőrizze a kimeneti fájl megadott könyvtárát!

## Következtetés
És megvan! Sikeresen alkalmazta a feltételes formázást futás közben az Excelben az Aspose.Cells for .NET használatával. Ez a nagy teljesítményű könyvtár megkönnyíti az Excel-fájlok programozott kezelését, lehetővé téve az unalmas feladatok automatizálását és az adatbemutatók javítását. Akár egy kis projekten, akár egy nagyszabású alkalmazáson dolgozik, az Aspose.Cells segíthet a munkafolyamat egyszerűsítésében és a termelékenység javításában.

## GYIK

### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok programozott létrehozását, kezelését és konvertálását.

### Használhatom az Aspose.Cells-t más programozási nyelvekkel?
Igen, az Aspose.Cells több programozási nyelvhez is elérhető, beleértve a Java, Python és sok más nyelvet.

### Létezik ingyenes próbaverzió az Aspose.Cells számára?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[Aspose honlapja](https://releases.aspose.com/).

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Támogatást kaphat, ha ellátogat a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).

### Szükségem van engedélyre az Aspose.Cells használatához?
 Igen, kereskedelmi használatra engedély szükséges, de kérhet ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
