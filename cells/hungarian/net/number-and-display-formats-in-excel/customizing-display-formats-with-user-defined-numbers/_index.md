---
title: Megjelenítési formátumok testreszabása felhasználó által megadott számokkal
linktitle: Megjelenítési formátumok testreszabása felhasználó által megadott számokkal
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg a megjelenítési formátumok testreszabását az Aspose.Cells for .NET segítségével. Formázza a dátumokat, a százalékokat és a pénznemet ennek a lépésről lépésre történő útmutatónak a segítségével.
weight: 11
url: /hu/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Megjelenítési formátumok testreszabása felhasználó által megadott számokkal

## Bevezetés
Az Excel-fájlokkal való munkavégzés gyakran megköveteli a cellák egyéni formázását az adatok értelmesebb és felhasználóbarátabb megjelenítéséhez. Képzelje el, hogy Excel-fájlt készít egy jelentéshez. Nem csak nyers számokat akarsz. Azt szeretné, hogy a dátumok, százalékok és pénznemek elegánsak és professzionálisak legyenek, igaz? Itt lépnek életbe az egyéni megjelenítési formátumok. Ebben az oktatóanyagban mélyrehatóan foglalkozunk az Aspose.Cells for .NET-szel, és bemutatjuk, hogyan szabhatja testre a számok megjelenítési formátumát a felhasználó által megadott beállításokkal.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy minden készen áll, hogy kövesse ezt az oktatóanyagot. Íme, amire szüksége lesz:
-  Aspose.Cells for .NET telepítve.[Töltse le itt](https://releases.aspose.com/cells/net/).
- C# és .NET keretrendszer alapismeretei.
-  Érvényes licenc az Aspose.Cells számára. Ha nincs ilyened, fogj egy[ingyenes próbaverzió](https://releases.aspose.com/) vagy kérjen a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
- Egy IDE, mint a Visual Studio.
- .NET Framework 4.0 vagy újabb.
 Ha hiányzik valami, ne aggódjon. Ezeket a hivatkozásokat bármikor újra meglátogathatja a szükséges fájlok letöltéséhez, vagy segítséget kérhet a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).
## Névterek importálása
Mielőtt belevágna a kódba, importálnia kell a szükséges névtereket az összes szükséges Aspose.Cells funkció eléréséhez.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ez a két névtér lesz az Ön fő eszköze ebben az oktatóanyagban. Most pedig térjünk át a szórakoztató részre:
## 1. lépés: A projektkönyvtár beállítása
Először is szüksége van egy helyre a fájlok tárolására, igaz? Hozzon létre egy könyvtárat a kimeneti Excel fájl mentéséhez. Ebben a lépésben a mentés előtt megbizonyosodunk arról is, hogy a könyvtár létezik.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Meghatározzuk a`dataDir` változó az elérési út tárolására, ahová a kimeneti Excel-fájl fog menni.
-  Ezután ellenőrizzük, hogy a könyvtár létezik-e használ`System.IO.Directory.Exists()`.
-  Ha a könyvtár nem létezik, akkor a következő használatával jön létre`System.IO.Directory.CreateDirectory()`.
## 2. lépés: Hozzon létre egy új munkafüzetet és adjon hozzá egy munkalapot
Most, hogy megvan a könyvtárunk, hozzunk létre egy új Excel-munkafüzetet, és adjunk hozzá egy munkalapot.
```csharp
// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();
// Új munkalap hozzáadása az Excel objektumhoz
int i = workbook.Worksheets.Add();
// Az újonnan hozzáadott munkalap hivatkozásának megszerzése a lapindex átadásával
Worksheet worksheet = workbook.Worksheets[i];
```
-  Először is létrehozunk egy újat`Workbook` objektum. Tekintse ezt az Ön Excel-fájljának.
-  Ehhez a munkafüzethez adunk egy új munkalapot a`Add()`módszert, és tárolja az indexet változóban`i`.
-  Erre a munkalapra hivatkozunk a`workbook.Worksheets[i]`.
## 3. lépés: Dátum hozzáadása egy cellához és a formátum testreszabása
 Most illessze be az aktuális dátumot egy cellába, és formázza azt, hogy egyéni módon jelenjen meg. Az alapértelmezett dátumformátum helyett egyéni formátumot állítunk be, mint pl`d-mmm-yy`.
```csharp
// Az aktuális rendszerdátum hozzáadása az "A1" cellához
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Az A1 cella stílusának lekérése
Style style = worksheet.Cells["A1"].GetStyle();
// Az egyéni megjelenítési formátum beállítása úgy, hogy a dátum „d-hh-éé” legyen
style.Custom = "d-mmm-yy";
// A stílus alkalmazása A1 cellára
worksheet.Cells["A1"].SetStyle(style);
```
-  Az aktuális rendszerdátumot hozzáadjuk a cellához`A1` segítségével`PutValue(DateTime.Now)`.
-  Lekérjük a cella aktuális stílusát`A1` segítségével`GetStyle()`.
-  Beállítással módosítjuk a cella stílusát`style.Custom = "d-mmm-yy"`, amely formázza a dátumot, hogy megjelenítse a napot, a hónapot és az évet.
-  Végül alkalmazzuk az új stílust a cellára`SetStyle()`.
## 4. lépés: Cella formázása százalékként
 Következő lépésként dolgozzunk a számokkal. Hozzáadunk egy numerikus értéket egy másik cellához, mondjuk`A2`, és formázza százalékban.
```csharp
//Számérték hozzáadása az "A2" cellához
worksheet.Cells["A2"].PutValue(20);
// Az A2-es cella stílusának megszerzése
style = worksheet.Cells["A2"].GetStyle();
// Az egyéni megjelenítési formátum beállítása az érték százalékos megjelenítéséhez
style.Custom = "0.0%";
// A stílus alkalmazása A2-es cellára
worksheet.Cells["A2"].SetStyle(style);
```
-  Hozzáadjuk az értéket`20` sejthez`A2`.
-  Lekérjük a cella stílusát`A2` és állítsa be az egyéni formátumot`0.0%` az érték százalékos (azaz 20%) megjelenítéséhez.
-  Végül alkalmazzuk a stílust a cellára`SetStyle()`.
## 5. lépés: Cella formázása pénznemként
 Adjunk hozzá még egy értéket, mondjuk a cellához`A3`, és formázza úgy, hogy pénznemként jelenjen meg. A dolgok érdekesebbé tétele érdekében olyan formátumot fogunk használni, amely a pozitív értékeket valutaként fontban, a negatív értékeket pedig dollárban jeleníti meg.
```csharp
// Számérték hozzáadása az "A3" cellához
worksheet.Cells["A3"].PutValue(2546);
// Az A3-as cella stílusának megszerzése
style = worksheet.Cells["A3"].GetStyle();
// Az egyéni megjelenítési formátum beállítása az érték pénznemként való megjelenítéséhez
style.Custom = "£#,##0;[Red]$-#,##0";
// A stílus alkalmazása A3-as cellára
worksheet.Cells["A3"].SetStyle(style);
```
-  Hozzáadjuk az értéket`2546` sejthez`A3`.
-  Egyedi formátumot állítunk be`£#,##0;[Red]$-#,##0`, amely a pozitív értékeket font előjellel, a negatív értékeket pedig pirossal és dollárjellel jeleníti meg.
- Alkalmazzuk a stílust a cellára a segítségével`SetStyle()`.
## 6. lépés: A munkafüzet mentése
Az utolsó lépés a munkafüzet mentése Excel fájlként. Ebben az oktatóanyagban az Excel 97-2003 formátumot fogjuk használni.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  A`Save()` metódus elmenti a munkafüzetet a megadott könyvtárba.
-  választunk`SaveFormat.Excel97To2003` hogy biztosítsa a kompatibilitást az Excel régebbi verzióival.
## Következtetés
Megvan! Létrehoztunk egy Excel-fájlt, egyedi dátum-, százalék- és pénznemformátumokat adtunk az egyes cellákhoz az Aspose.Cells for .NET segítségével, és elmentettük a fájlt. Az egyéni formázás sokkal olvashatóbbá és professzionálisabbá teszi az Excel-fájlokat. Ne felejtse el felfedezni az Aspose.Cells egyéb formázási lehetőségeit, például a feltételes formázást, hogy még jobban szabályozhassa az adatok megjelenését.
## GYIK
### Hogyan alkalmazhatok bonyolultabb formázási beállításokat az Aspose.Cells-ben?
Különféle formázási stílusokat, például betűszínt, szegélyeket és háttérszíneket kombinálhat egyéni számformátumokkal.
### Alkalmazhatok egyéni számformátumot egy cellatartományra?
Igen, az Aspose.Cells lehetővé teszi, hogy stílust alkalmazzon egy sor cellára a`Range.SetStyle()` módszer.
### Milyen más fájlformátumokba menthetem a munkafüzetet?
 Az Aspose.Cells számos formátumot támogat, beleértve az XLSX-et, a CSV-t és a PDF-t. Egyszerűen változtassa meg a`SaveFormat` a`Save()` módszer.
### Formázhatom másképp a negatív számokat?
Teljesen! Egyéni számformátumok segítségével negatív számokat jeleníthet meg különböző színekkel vagy szimbólumokkal.
### Az Aspose.Cells for .NET ingyenes?
 Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes funkcionalitás érdekében érvényes licencre lesz szüksége. Kaphatsz a[ideiglenes engedély itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
