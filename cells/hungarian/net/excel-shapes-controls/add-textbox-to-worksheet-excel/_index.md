---
title: Szövegdoboz hozzáadása az Excel munkalapjához
linktitle: Szövegdoboz hozzáadása az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Ebben a lépésenkénti oktatóanyagban megtudhatja, hogyan adhat hozzá testreszabható szövegdobozokat az Excelhez az Aspose.Cells for .NET használatával.
weight: 14
url: /hu/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szövegdoboz hozzáadása az Excel munkalapjához

## Bevezetés
Szeretné Excel-táblázatait egyedi látványelemekkel bővíteni, amelyek lekötik a közönséget? Szövegdobozok hozzáadása nagyszerű módja ennek elérésére! Az Aspose.Cells for .NET segítségével egyszerűen integrálhat szövegdobozokat Excel-munkalapjaiba, így dokumentumait informatívabbá és látványosabbá teheti. Ez a részletes útmutató végigvezeti Önt az Aspose.Cells segítségével szövegdobozok hozzáadásának egyszerű folyamatán, bemutatva, hogyan lehet őket személyre szabni szöveggel, színekkel, hiperhivatkozásokkal és egyebekkel!
## Előfeltételek
Mielőtt belemerülnénk a kódolási csodába, íme, a zökkenőmentes vitorlázási élmény biztosításának alapvető előfeltételei:
1. .NET fejlesztői környezet: Szüksége lesz egy működő .NET-keretrendszerre, valamint egy olyan IDE-re, mint a Visual Studio. Győződjön meg róla, hogy frissítve van a legújabb verzióra!
2.  Aspose.Cells for .NET: Győződjön meg arról, hogy letöltötte az Aspose.Cells könyvtárat. A legújabb verziót letöltheti innen[itt](https://releases.aspose.com/cells/net/).
3. Alapvető programozási ismeretek: A C# ismerete és az Excel fájlok kezelésének néhány általános fogalma megkönnyíti ezt az oktatóanyagot!
## Csomagok importálása
Ügyeljen arra, hogy a szükséges csomagokat a C# fájl elején importálja. Ezt a következőképpen teheti meg:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Telepítse az Aspose.Cells programot
Ha még nem tette meg, hozzáadhatja az Aspose.Cells fájlt a Visual Studio NuGet Package Manager segítségével:
1. Nyissa meg a Visual Studio-t.
2.  Menj ide`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Keresse meg az „Aspose.Cells” kifejezést, és telepítse a projekthez.
Most, hogy leraktuk az alapokat, ugorjunk a szórakoztató részre!
## 1. lépés: A dokumentumkönyvtár beállítása
Először is állítsuk be azt a könyvtárat, ahol az összes Excel dokumentumot tárolni fogja. A munkafüzet létrehozásának megkezdése előtt elengedhetetlen annak biztosítása, hogy ez a könyvtár létezik.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory"; 
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a kódrészlet létrehoz egy nevű könyvtárat`Your Document Directory` (Kérjük, cserélje ki a tényleges elérési útjával), ha még nem létezik. Könnyű peasy, igaz?
## 2. lépés: Új munkafüzet példányosítása
Ezután létre kell hoznunk egy új munkafüzetet, amelyhez hozzáadjuk a szövegdobozainkat. Ez könnyen megtehető néhány sornyi kóddal:
```csharp
// Példányosítson egy új munkafüzetet.
Workbook workbook = new Workbook();
```
Ez a kódsor egy új Excel-munkafüzetet hoz létre. Egyszerű és egyértelmű!
## 3. lépés: Az első munkalap elérése
Most, hogy elkészült a munkafüzetünk, szerezzük be az első munkalapot, amelyhez hozzáadjuk a szövegdobozunkat:
```csharp
// Szerezd meg a könyv első feladatlapját.
Worksheet worksheet = workbook.Worksheets[0];
```
 Így most már hozzáférhet az első nevű munkalaphoz`worksheet`. Itt az ideje, hogy ragyogjon!
## 4. lépés: Szövegdoboz hozzáadása
Rendben, itt az ideje, hogy hozzáadjuk az első szövegdobozunkat! Íme, hogyan kell csinálni:
```csharp
// Új szövegdoboz hozzáadása a gyűjteményhez.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Ebben a sorban megadjuk azt a sort és oszlopot, ahová a szövegdoboz kerül, valamint beállítjuk a szélességét és magasságát (160, illetve 200). Nyugodtan módosíthatja ezeket a számokat az elrendezése alapján!
## 5. lépés: A TextBox objektum beszerzése
szövegmező hozzáadása után hivatkozást kell kapnunk rá, hogy testreszabhassuk a tartalmát:
```csharp
// Szerezze be a szövegdoboz objektumot.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Jelenleg,`textbox0` az Ön aranyjegye ennek a szövegmezőnek a módosításához!
## 6. lépés: A szövegmező kitöltése tartalommal
Ezután adjunk meg szöveget a szövegdobozhoz:
```csharp
// Töltse ki a szöveget.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Szöveg beszúrása a szövegdobozba ilyen egyszerű! 
## 7. lépés: A szövegdoboz megjelenésének testreszabása
Mit szólnál, ha feldobnánk egy kicsit? Beállíthatja a betűtípusok színét, stílusát és még sok mást!
```csharp
// Állítsa be a betűtípus színét.
textbox0.Font.Color = Color.Blue;
// Állítsa a betűtípust félkövérre.
textbox0.Font.IsBold = true;
// Állítsa be a betűméretet.
textbox0.Font.Size = 14;
// A font attribútumot állítsa dőltre.
textbox0.Font.IsItalic = true;
```
Nyugodtan játssz a különböző színekkel és stílusokkal, hogy megtudd, mi tűnik fel a legjobban vizuálisan!
## 8. lépés: Hiperhivatkozás hozzáadása
Szeretnéd a szövegmezőt kattintható hivatkozássá alakítani? Tegyük ezt:
```csharp
// Adjon hozzá egy hiperhivatkozást a szövegdobozhoz.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Mostantól bárki, aki a szövegdobozra kattint, az Aspose webhelyére kerül. Ez olyan, mint a varázslat!
## 9. lépés: A TextBox elhelyezési típusának beállítása
Különböző választási lehetőségek közül választhat, hogy a szövegdoboz hogyan viselkedjen a munkalappal kapcsolatban. Íme egy példa arra, hogyan állíthatja be szabadon lebegővé:
```csharp
// Állítsa be az elhelyezést.
textbox0.Placement = PlacementType.FreeFloating;
```
Alternatív megoldásként, ha szeretné átméretezni és cellákkal együtt mozgatni, a következőképpen állíthatja be:
```csharp
// Állítsa be az elhelyezés típusát, mivel a szövegmező a cellákkal együtt mozog és átméreteződik.
textbox1.Placement = PlacementType.MoveAndSize;
```
## 10. lépés: A vonal- és kitöltési formátumok testreszabása
A következőképpen módosíthatja a szövegmező szegélyének és kitöltésének megjelenését:
```csharp
// Szerezze meg a szövegdoboz kitöltési formátumát.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Szerezze be a szövegdoboz sorformátumának típusát.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Állítsa be a vonalvastagságot.
lineformat.Weight = 6;
// Állítsa a kötőjelstílust négyzetpontra.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Ezzel tovább testreszabhatja szövegdobozát, és stílusának megfelelő látványelemeket ad hozzá.
## 11. lépés: Újabb szövegdoboz hozzáadása
Senki nem mondta, hogy csak egy szövegdobozt adhatunk hozzá! Tegyünk egy másikat más szöveggel:
```csharp
// Adjon hozzá egy másik szövegdobozt.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Szerezd meg a második szövegdobozt.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Írjon be hozzá szöveget.
textbox1.Text = "This is another simple text box";
```
Most igazán feldobja az Excel-lapot több szövegdobozsal!
## 12. lépés: Mentse el a munkafüzetet
Végre itt az ideje megmenteni remekművünket! Íme a nap utolsó kódsora:
```csharp
// Mentse el az excel fájlt.
workbook.Save(dataDir + "book1.out.xls");
```
Ezzel az egyetlen kódsorral létrehozott és módosított egy Excel-fájlt testreszabható szövegmezőkkel!
## Következtetés
Gratulálok! Sikeresen navigált az Excel szövegdobozainak világában az Aspose.Cells for .NET használatával. Nem csak azt tanulta meg, hogyan kell szövegdobozt hozzáadni, hanem azt is, hogyan szabhatja személyre, hogy vonzóbbá tegye a táblázatokat. A színek és stílusok megváltoztatásától a hiperhivatkozások hozzáadásáig a lehetőségek gyakorlatilag végtelenek! 
Készen áll az Excel-dokumentumok átalakítására? Engedje ki kreativitását, és kísérletezzen különböző elrendezésekkel!
## GYIK
### Mi az Aspose.Cells a .NET számára?
Az Aspose.Cells for .NET egy hatékony könyvtár, amellyel a fejlesztők könnyedén hozhatnak létre, kezelhetnek és konvertálhatnak Excel-fájlokat.
### Kipróbálhatom az Aspose.Cells-t vásárlás előtt?
 Igen! Letöltheti és használhatja az ingyenes próbaverziót[itt](https://releases.aspose.com/).
### Hol találom az Aspose.Cells dokumentációját?
 Az átfogó dokumentációt a címen érheti el[Aspose.Cells Documentation](https://reference.aspose.com/cells/net/).
### Van-e támogatás, ha problémákba ütközöm?
 Teljesen! Ha segítségre van szüksége, menjen a[Aspose fórum](https://forum.aspose.com/c/cells/9) segítségért.
### Használhatom az Aspose.Cells-t licenc nélkül?
 Bár használhat ingyenes próbaverziót, a teljes funkcionalitás eléréséhez licencet kell vásárolnia. Nézze meg az árképzést[itt](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
