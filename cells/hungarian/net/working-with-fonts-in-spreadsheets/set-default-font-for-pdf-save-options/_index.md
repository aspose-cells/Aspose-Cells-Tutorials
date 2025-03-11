---
title: Állítsa be az alapértelmezett betűtípust a PDF-mentési beállításokhoz
linktitle: Állítsa be az alapértelmezett betűtípust a PDF-mentési beállításokhoz
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan állíthat be alapértelmezett betűtípusokat a PDF-mentési beállításokhoz az Aspose.Cells for .NET segítségével, így biztosítva, hogy a dokumentumok minden alkalommal tökéletesek legyenek.
weight: 11
url: /hu/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be az alapértelmezett betűtípust a PDF-mentési beállításokhoz

## Bevezetés
Ha jelentések, számlák vagy bármely más PDF formátumú dokumentum létrehozásáról van szó, a legfontosabb annak biztosítása, hogy a tartalom megfelelően nézzen ki. A betűtípusok létfontosságú szerepet játszanak a dokumentumok vizuális vonzerejének és olvashatóságának megőrzésében. Mi történik azonban, ha az Excel-fájlban használt betűtípus nem érhető el azon a rendszeren, ahol a PDF-fájlt generálja? Itt jön jól az Aspose.Cells for .NET. Ez a nagy teljesítményű könyvtár lehetővé teszi, hogy alapértelmezett betűtípusokat állítson be a PDF-mentési beállításokhoz, így biztosítva, hogy a dokumentumok professzionális és egységes megjelenésűek legyenek, függetlenül attól, hogy hol nyitják meg őket.
## Előfeltételek
Mielőtt elkezdenénk, győződjön meg arról, hogy rendelkezik a következőkkel:
1. Visual Studio: A kód írásához és végrehajtásához olyan fejlesztői környezetre lesz szüksége, mint a Visual Studio.
2.  Aspose.Cells for .NET: Letöltheti a legújabb verziót innen[ezt a linket](https://releases.aspose.com/cells/net/). Alternatív megoldásként telepítheti a Visual Studio NuGet Package Manager segítségével.
3. Alapvető C# ismerete: A C# alapjainak megértése segít a kódpéldák követésében.
4. Minta Excel-fájl: Készítsen egy Excel-mintafájlt tesztelésre. Létrehozhat egyet különféle betűtípusokkal és stílusokkal, hogy megtudja, hogyan kezeli az Aspose.Cells a hiányzó betűtípusokat.
## Csomagok importálása
Mielőtt használhatná az Aspose.Cells-t a projektben, importálnia kell a szükséges csomagokat. Íme, hogyan kell csinálni:
1. Nyissa meg projektjét: Indítsa el a Visual Studio programot, és nyissa meg a meglévő projektet, vagy hozzon létre egy újat.
2. Referenciák hozzáadása: Kattintson jobb gombbal a projektre a Solution Explorerben, és válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Az Aspose.Cells telepítése: Keresse meg az "Aspose.Cells" kifejezést, és kattintson az "Install" gombra.
4. Irányelvek hozzáadása: A C# fájl tetején adja meg a következő névtereket:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## 1. lépés: Állítsa be a címtárakat
A fájlokkal való munka előtt fontos meghatározni a forrás- és kimeneti könyvtárakat. Ez megkönnyíti a bemeneti Excel-fájl megkeresését és a generált kimeneti fájlok mentését.
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` a könyvtárak tényleges elérési útjával.
## 2. lépés: Nyissa meg az Excel fájlt
 Most, hogy beállítottuk a könyvtárainkat, nyissuk meg azt az Excel-fájlt, amellyel dolgozni szeretne. A`Workbook` osztály az Aspose.Cellsben az Excel dokumentum betöltésére szolgál.
```csharp
// Nyisson meg egy Excel fájlt
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Ügyeljen arra, hogy a fájlnevet a tényleges fájlnévre cserélje.
## 3. lépés: Állítsa be a képmegjelenítési beállításokat
Ezután konfigurálnunk kell az Excel-lap képformátumra konvertálásához szükséges renderelési beállításokat. Létrehozunk egy példányt`ImageOrPrintOptions`, amely megadja a kép típusát és az alapértelmezett betűtípust.
```csharp
// Renderelés PNG fájlformátumba
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Ebben a kódrészletben beállítjuk a`CheckWorkbookDefaultFont` tulajdonát`false`, ami azt jelenti, hogy ha valamelyik betűtípus hiányzik, a rendszer a megadott alapértelmezett betűtípust („Times New Roman”) használja helyette.
## 4. lépés: Rendelje meg a lapot képként
 Most jelenítsük meg a munkafüzet első lapját PNG-képként. Használjuk a`SheetRender` osztályban ennek megvalósításához.
```csharp
// Az első munkalapot rendereli képpé
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## 5. lépés: Változtassa meg a képtípust és a renderelést TIFF-re
 Ha ugyanazt a lapot egy másik képformátumra, például TIFF-re szeretné renderelni, egyszerűen módosíthatja a`ImageType` tulajdonságot, és ismételje meg a renderelési folyamatot.
```csharp
// Állítsa TIFF formátumra
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## 6. lépés: Konfigurálja a PDF mentési beállításokat
 Következő lépésként állítsuk be a PDF mentési beállításokat. Létrehozunk egy példányt`PdfSaveOptions`állítsa be az alapértelmezett betűtípust, és adja meg, hogy ellenőrizni akarjuk a hiányzó betűtípusokat.
```csharp
// Konfigurálja a PDF mentési beállításokat
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## 7. lépés: Mentse el a munkafüzetet PDF formátumban
A konfigurált mentési beállításokkal ideje PDF-fájlként menteni Excel-munkafüzetünket. 
```csharp
// Mentse el a munkafüzetet PDF-be
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## 8. lépés: Erősítse meg a végrehajtást
Végül jó gyakorlat, ha tudatja a felhasználóval, hogy a folyamat sikeresen befejeződött. Ezt egy egyszerű konzolüzenet használatával érheti el.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Következtetés
Az Aspose.Cells rugalmas és robusztus módot biztosít az Excel-fájlok kezelésének kezelésére, megkönnyítve a fejlesztők számára, hogy tetszetős, formázásukat megőrző dokumentumokat hozzanak létre. Akár jelentésekkel, pénzügyi dokumentumokkal vagy bármilyen más adatmegjelenítési formával dolgozik, a betűkészlet-megjelenítés ellenőrzése jelentősen javíthatja a kimeneti minőséget.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-fájlok kezelését a Microsoft Excel telepítése nélkül. Különféle fájlformátumokat támogat, és gazdag funkciókat kínál a táblázatokkal való munkavégzéshez.
### Hogyan állíthatok be alapértelmezett betűtípust az Excel-fájljaimhoz?
 Beállíthat egy alapértelmezett betűtípust a`PdfSaveOptions` osztályt, és adja meg a kívánt betűtípus nevét. Ez biztosítja, hogy a dokumentum a megadott alapértelmezett betűtípust használja még akkor is, ha hiányzik egy betűtípus.
### Átalakíthatom az Excel fájlokat PDF-től eltérő formátumba?
Teljesen! Az Aspose.Cells lehetővé teszi az Excel-fájlok különféle formátumokká konvertálását, beleértve a képeket (PNG, TIFF), HTML-t, CSV-t stb.
### Az Aspose.Cells ingyenesen használható?
Az Aspose.Cells kereskedelmi termék, de egy korlátozott próbaverzióval ingyenesen kipróbálhatod. A teljes funkcionalitás érdekében licencet kell vásárolnia.
### Hol találok támogatást az Aspose.Cells számára?
 Az Aspose.Cells támogatásához keresse fel a[Aspose fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehet fel, és megoszthatja tapasztalatait más felhasználókkal és fejlesztőkkel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
