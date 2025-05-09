---
"description": "Ismerje meg, hogyan szabhatja testre a megjelenítési formátumokat az Aspose.Cells for .NET segítségével. Formázza a dátumokat, százalékokat és pénznemeket ezzel a lépésről lépésre bemutató útmutatóval."
"linktitle": "Megjelenítési formátumok testreszabása felhasználó által definiált számokkal"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Megjelenítési formátumok testreszabása felhasználó által definiált számokkal"
"url": "/hu/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Megjelenítési formátumok testreszabása felhasználó által definiált számokkal

## Bevezetés
Az Excel-fájlokkal való munka gyakran megköveteli a cellák egyéni formázását az adatok értelmesebb és felhasználóbarátabb megjelenítése érdekében. Képzelje el, hogy egy Excel-fájlt készít egy jelentéshez. Nem csak nyers számokra van szüksége. Azt szeretné, hogy a dátumok, százalékok és pénznemek elegánsak és professzionálisak legyenek, igaz? Itt jönnek képbe az egyéni megjelenítési formátumok. Ebben az oktatóanyagban mélyrehatóan elmerülünk az Aspose.Cells for .NET programban, hogy megmutassuk, hogyan szabhatja testre a számok megjelenítési formátumát a felhasználó által definiált beállításokkal.
## Előfeltételek
Mielőtt elkezdenéd, győződj meg róla, hogy mindent előkészítettél az oktatóanyag követéséhez. Íme, amire szükséged lesz:
- Aspose.Cells for .NET telepítve. [Töltsd le itt](https://releases.aspose.com/cells/net/).
- C# és .NET keretrendszer alapismeretek.
- Érvényes Aspose.Cells licenc. Ha nincs, szerezz be egyet [ingyenes próba](https://releases.aspose.com/) vagy kérjen egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
- Egy Visual Studio-hoz hasonló IDE.
- .NET-keretrendszer 4.0 vagy újabb.
Ha bármi hiányzik, ne aggódjon. Bármikor újra megnyithatja ezeket a linkeket a szükséges fájlok letöltéséhez, vagy segítséget kérhet a [Aspose támogatói fórum](https://forum.aspose.com/c/cells/9).
## Névterek importálása
Mielőtt belevágnánk a kódba, importálnunk kell a szükséges névtereket az Aspose.Cells összes funkciójának eléréséhez.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ez a két névtér lesz a fő eszközöd ebben az oktatóanyagban. Most pedig térjünk át a szórakoztató részre:
## 1. lépés: A projektkönyvtár beállítása
Először is, kell egy hely a fájljaid tárolásához, ugye? Hozzunk létre egy könyvtárat a kimeneti Excel-fájl mentéséhez. Ebben a lépésben a mentés előtt ellenőrizzük, hogy a könyvtár létezik-e.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- Mi definiálunk egy `dataDir` változó, amely tárolja az elérési utat, ahová a kimeneti Excel fájl kerülni fog.
- Ezután ellenőrizzük, hogy létezik-e a könyvtár, a következő használatával: `System.IO.Directory.Exists()`.
- Ha a könyvtár nem létezik, akkor a következővel lesz létrehozva: `System.IO.Directory.CreateDirectory()`.
## 2. lépés: Új munkafüzet létrehozása és munkalap hozzáadása
Most, hogy megvan a könyvtárunk, hozzunk létre egy új Excel-munkafüzetet, és adjunk hozzá egy munkalapot.
```csharp
// Workbook objektum példányosítása
Workbook workbook = new Workbook();
// Új munkalap hozzáadása az Excel objektumhoz
int i = workbook.Worksheets.Add();
// Az újonnan hozzáadott munkalap hivatkozásának lekérése a munkalap indexének átadásával
Worksheet worksheet = workbook.Worksheets[i];
```
- Először is létrehozunk egy újat `Workbook` objektum. Gondolj erre úgy, mint egy Excel-fájlra.
- Új munkalapot adunk hozzá ehhez a munkafüzethez a következő használatával: `Add()` metódust és az indexet egy változóban tároljuk `i`.
- Erre a munkalapra a következőképpen hivatkozunk: `workbook.Worksheets[i]`.
## 3. lépés: Dátum hozzáadása egy cellához és a formátum testreszabása
Most illesszük be az aktuális dátumot egy cellába, és formázzuk meg egyéni megjelenítéshez. Az alapértelmezett dátumformátum helyett egyéni formátumot állítunk be, például: `d-mmm-yy`.
```csharp
// Aktuális rendszerdátum hozzáadása az "A1" cellához
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Az A1 cella stílusának lekérése
Style style = worksheet.Cells["A1"].GetStyle();
// Egyéni megjelenítési formátum beállítása a dátum megjelenítéséhez "n-hhh-éé" formátumban
style.Custom = "d-mmm-yy";
// Stílus alkalmazása az A1 cellára
worksheet.Cells["A1"].SetStyle(style);
```
- Hozzáadjuk az aktuális rendszerdátumot a cellához `A1` használva `PutValue(DateTime.Now)`.
- Lekérjük a cella aktuális stílusát `A1` használva `GetStyle()`.
- A cella stílusát a következő beállítással módosítjuk: `style.Custom = "d-mmm-yy"`, amely úgy formázza a dátumot, hogy a nap, a rövidített hónap és az év jelenjen meg.
- Végül az új stílust alkalmazzuk a cellára a következővel: `SetStyle()`.
## 4. lépés: Cella formázása százalékként
Következő lépésként dolgozzunk számokkal. Hozzáadunk egy numerikus értéket egy másik cellához, mondjuk `A2`, és formázd százalékként.
```csharp
// Numerikus érték hozzáadása az "A2" cellához
worksheet.Cells["A2"].PutValue(20);
// Az A2 cella stílusának meghatározása
style = worksheet.Cells["A2"].GetStyle();
// Egyéni megjelenítési formátum beállítása az érték százalékos megjelenítéséhez
style.Custom = "0.0%";
// Stílus alkalmazása az A2 cellára
worksheet.Cells["A2"].SetStyle(style);
```
- Mi adjuk hozzá az értéket `20` cellába `A2`.
- Lekérjük a cella stílusát `A2` és állítsd be az egyéni formátumot erre: `0.0%` az érték százalékos formában történő megjelenítéséhez (azaz 20%).
- Végül a stílust a cellára alkalmazzuk a következővel: `SetStyle()`.
## 5. lépés: Cella formázása pénznemként
Adjunk hozzá egy másik értéket, mondjuk a cellához `A3`és formázd úgy, hogy pénznemként jelenjen meg. Hogy érdekesebb legyen a dolog, egy olyan formátumot fogunk használni, amely a pozitív értékeket fontban, a negatív értékeket pedig dollárban jeleníti meg pénznemként.
```csharp
// Numerikus érték hozzáadása az "A3" cellához
worksheet.Cells["A3"].PutValue(2546);
// Az A3-as cella stílusának megismerése
style = worksheet.Cells["A3"].GetStyle();
// Egyéni megjelenítési formátum beállítása az érték pénznemként való megjelenítéséhez
style.Custom = "£#,##0;[Red]$-#,##0";
// Stílus alkalmazása A3-as cellára
worksheet.Cells["A3"].SetStyle(style);
```
- Mi adjuk hozzá az értéket `2546` cellába `A3`.
- Egyedi formátumot állítunk be `£#,##0;[Red]$-#,##0`, amely a pozitív értékeket kettőskereszttel, a negatív értékeket pedig pirossal és dollárjellel jeleníti meg.
- A stílust a következővel alkalmazzuk a cellára: `SetStyle()`.
## 6. lépés: A munkafüzet mentése
Az utolsó lépés a munkafüzet Excel-fájlként történő mentése. Ebben az oktatóanyagban az Excel 97-2003 formátumot fogjuk használni.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- A `Save()` A metódus a megadott könyvtárba menti a munkafüzetet.
- Mi választunk `SaveFormat.Excel97To2003` hogy biztosítsa a kompatibilitást az Excel régebbi verzióival.
## Következtetés
Íme, itt van! Létrehoztunk egy Excel-fájlt, egyéni dátum-, százalék- és pénznemformátumokat adtunk hozzá bizonyos cellákhoz az Aspose.Cells for .NET segítségével, majd mentettük a fájlt. Az egyéni formázás sokkal olvashatóbbá és professzionálisabbá teszi az Excel-fájlokat. Ne felejtsd el felfedezni az Aspose.Cells egyéb formázási lehetőségeit, például a feltételes formázást, hogy még jobban szabályozhasd az adatok megjelenését.
## GYIK
### Hogyan alkalmazhatok összetettebb formázási beállításokat az Aspose.Cells-ben?
Különböző formázási stílusokat, például betűszínt, szegélyeket és háttérszíneket kombinálhat egyéni számformátumokkal.
### Alkalmazhatok egyéni számformátumot egy cellatartományra?
Igen, az Aspose.Cells lehetővé teszi egy stílus alkalmazását cellatartományra a `Range.SetStyle()` módszer.
### Milyen más fájlformátumokban menthetem el a munkafüzetet?
Az Aspose.Cells számos formátumot támogat, beleértve az XLSX, CSV és PDF fájlokat. Egyszerűen módosítsa a `SaveFormat` a `Save()` módszer.
### Formázhatom másképp a negatív számokat?
Természetesen! Egyéni számformátumokat használhat a negatív számok különböző színekkel vagy szimbólumokkal történő megjelenítéséhez.
### Ingyenes az Aspose.Cells .NET-hez?
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes funkcionalitás eléréséhez érvényes licencre van szükség. Szerezhet egy [ideiglenes jogosítvány itt](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}