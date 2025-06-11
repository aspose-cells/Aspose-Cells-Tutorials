---
"description": "Tanuld meg, hogyan állíthatsz be alapértelmezett betűtípusokat a PDF mentési beállításaihoz az Aspose.Cells for .NET használatával, így biztosítva, hogy dokumentumaid minden alkalommal tökéletesen nézzenek ki."
"linktitle": "Alapértelmezett betűtípus beállítása PDF mentési beállításokhoz"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Alapértelmezett betűtípus beállítása PDF mentési beállításokhoz"
"url": "/id/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Alapértelmezett betűtípus beállítása PDF mentési beállításokhoz

## Bevezetés
Jelentések, számlák vagy bármilyen más PDF formátumú dokumentum létrehozásakor kiemelkedő fontosságú, hogy a tartalom megfelelően nézzen ki. A betűtípusok létfontosságú szerepet játszanak a dokumentumok vizuális megjelenésének és olvashatóságának fenntartásában. De mi történik, ha az Excel-fájlban használt betűtípus nem érhető el azon a rendszeren, ahol a PDF-et generálja? Itt jön jól az Aspose.Cells for .NET. Ez a hatékony könyvtár lehetővé teszi az alapértelmezett betűtípusok beállítását a PDF mentési beállításaihoz, biztosítva, hogy a dokumentumok professzionálisak és egységesek legyenek, függetlenül attól, hogy hol nyitják meg őket.
## Előfeltételek
Mielőtt belekezdenénk, győződjünk meg róla, hogy a következőkkel rendelkezünk:
1. Visual Studio: A kód írásához és végrehajtásához szükséged lesz egy fejlesztői környezetre, például a Visual Studio-ra.
2. Aspose.Cells .NET-hez: A legújabb verziót innen töltheti le: [ezt a linket](https://releases.aspose.com/cells/net/)Alternatív megoldásként telepítheti a Visual Studio NuGet csomagkezelőjével is.
3. C# alapismeretek: A C# alapjainak ismerete segít a kódpéldák követésében.
4. Minta Excel fájl: Készíts elő egy minta Excel fájlt tesztelésre. Létrehozhatsz egyet különböző betűtípusokkal és stílusokkal, hogy lásd, hogyan kezeli az Aspose.Cells a hiányzó betűtípusokat.
## Csomagok importálása
Mielőtt használhatnád az Aspose.Cells-t a projektedben, importálnod kell a szükséges csomagokat. Így teheted meg:
1. Nyisd meg a projekted: Indítsd el a Visual Studio-t, és nyisd meg a meglévő projektedet, vagy hozz létre egy újat.
2. Referenciák hozzáadása: Kattintson jobb gombbal a projektjére a Megoldáskezelőben, és válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Aspose.Cells telepítése: Keresse meg az „Aspose.Cells” fájlt, és kattintson a „Telepítés” gombra.
4. User Directives hozzáadása: A C# fájl tetején szerepeljenek a következő névterek:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## 1. lépés: Állítsa be a könyvtárait
fájlokkal való munka megkezdése előtt fontos meghatározni a forrás- és kimeneti könyvtárakat. Ez megkönnyíti a bemeneti Excel-fájl megtalálását és a létrehozott kimeneti fájlok mentését.
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
Csere `"Your Document Directory"` a könyvtáraid tényleges elérési útjával.
## 2. lépés: Nyissa meg az Excel-fájlt
Most, hogy beállítottuk a könyvtárainkat, nyissuk meg azt az Excel fájlt, amellyel dolgozni szeretnénk. A `Workbook` Az Aspose.Cells osztálya az Excel dokumentum betöltéséhez használatos.
```csharp
// Excel-fájl megnyitása
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Ügyelj arra, hogy a fájlnevet a tényleges fájlnevedre cseréld.
## 3. lépés: Képmegjelenítési beállítások megadása
Ezután konfigurálnunk kell a renderelési beállításokat az Excel-táblázat képformátumba konvertálásához. Létrehozunk egy példányt a következőből: `ImageOrPrintOptions`, megadva a kép típusát és az alapértelmezett betűtípust.
```csharp
// PNG fájlformátumba renderelés
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
Ebben a kódrészletben beállítottuk a `CheckWorkbookDefaultFont` ingatlan `false`ami azt jelenti, hogy ha hiányzik valamelyik betűtípus, akkor a megadott alapértelmezett betűtípus („Times New Roman”) lesz használva.
## 4. lépés: A munkalap renderelése képként
Most pedig jelenítsük meg a munkafüzet első lapját PNG képként. Használni fogjuk a `SheetRender` osztály ennek megvalósításához.
```csharp
// Az első munkalap renderelése képpé
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## 5. lépés: Képtípus módosítása és renderelés TIFF formátumra
Ha ugyanazt a munkalapot más képformátumban, például TIFF-ben szeretné megjeleníteni, egyszerűen módosíthatja a `ImageType` tulajdonságot, és ismételje meg a renderelési folyamatot.
```csharp
// TIFF formátumra állítás
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## 6. lépés: PDF mentési beállítások konfigurálása
Következő lépésként állítsuk be a PDF mentési beállításait. Létrehozunk egy példányt a következőből: `PdfSaveOptions`, állítsd be az alapértelmezett betűtípust, és add meg, hogy hiányzó betűtípusokat szeretnénk keresni.
```csharp
// PDF mentési beállítások konfigurálása
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## 7. lépés: A munkafüzet mentése PDF formátumban
A mentési beállítások konfigurálása után itt az ideje, hogy PDF fájlként mentsük el az Excel-munkafüzetünket. 
```csharp
// Munkafüzet mentése PDF formátumban
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## 8. lépés: Végrehajtás megerősítése
Végül, jó gyakorlat, ha értesítjük a felhasználót a folyamat sikeres befejezéséről. Ezt egy egyszerű konzolüzenettel teheti meg.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Következtetés
Az Aspose.Cells rugalmas és robusztus módot kínál az Excel-fájlok manipulációjának kezelésére, megkönnyítve a fejlesztők számára a vizuálisan vonzó, formázást megőrző dokumentumok létrehozását. Akár jelentéseken, pénzügyi dokumentumokon vagy bármilyen más adatmegjelenítési formában dolgozik, a betűtípus-megjelenítés feletti kontroll jelentősen javíthatja a kimeneti minőséget.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET könyvtár, amely lehetővé teszi a fejlesztők számára, hogy Excel fájlokat kezeljenek anélkül, hogy telepíteni kellene a Microsoft Excelt. Különböző fájlformátumokat támogat, és gazdag funkciókat kínál a táblázatokkal való munkához.
### Hogyan állíthatok be alapértelmezett betűtípust az Excel fájljaimhoz?
Beállíthat egy alapértelmezett betűtípust a `PdfSaveOptions` osztályt, és adja meg a kívánt betűtípus nevét. Ez biztosítja, hogy még ha egy betűtípus hiányzik is, a dokumentum a megadott alapértelmezett betűtípust fogja használni.
### Konvertálhatok Excel fájlokat PDF-től eltérő formátumba?
Abszolút! Az Aspose.Cells lehetővé teszi Excel fájlok konvertálását különféle formátumokba, beleértve a képeket (PNG, TIFF), HTML-t, CSV-t és egyebeket.
### Ingyenesen használható az Aspose.Cells?
Az Aspose.Cells egy kereskedelmi termék, de ingyenesen kipróbálható egy korlátozott próbaverzióval. A teljes funkcionalitás eléréséhez licencet kell vásárolnia.
### Hol találok támogatást az Aspose.Cells-hez?
Az Aspose.Cells támogatását a következő helyen találja: [Aspose fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehet fel és megoszthatja tapasztalatait más felhasználókkal és fejlesztőkkel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}