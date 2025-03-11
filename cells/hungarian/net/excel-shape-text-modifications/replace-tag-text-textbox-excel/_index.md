---
title: Cserélje ki a címkét szövegre az Excel TextBox-ban
linktitle: Cserélje ki a címkét szövegre az Excel TextBox-ban
second_title: Aspose.Cells .NET Excel Processing API
description: Az Aspose.Cells for .NET segítségével könnyedén cserélje ki az Excel-lapok szövegmezőiben lévő szöveget. Útmutató lépésről lépésre az Excel automatizálásához.
weight: 11
url: /hu/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cserélje ki a címkét szövegre az Excel TextBox-ban

## Bevezetés
Ebben a cikkben egy konkrét feladattal foglalkozunk: a címkék szövegmezőiben való helyettesítése egy Excel munkalapon az Aspose.Cells segítségével. Lépésről lépésre végigvezetjük a teljes folyamaton, biztosítva, hogy minden részletet megértsen. Ennek az oktatóanyagnak a végére nemcsak az Aspose.Cells megértését fogja javítani, hanem az Excelhez kapcsolódó feladatait is egyszerűsíti!
## Előfeltételek
Mielőtt elkezdené, elő kell készítenie néhány dolgot:
1. Visual Studio: Győződjön meg arról, hogy telepítve van a Visual Studio. Ez egy rugalmas IDE, amely a C# nyelvű kódolást gyerekjátékká teszi.
2.  Aspose.Cells Library: Ha még nem tette meg, töltse le a .NET Aspose.Cells könyvtárát a[oldalon](https://releases.aspose.com/cells/net/)Ingyenes próbaverziót is beszerezhet a funkcióinak megtekintéséhez.
3. Alapvető C# ismerete: A C# programozás alapvető ismerete nagyban segít abban, hogy könnyen kövesse ezt az útmutatót.
Most, hogy minden készen áll, térjünk át a szórakoztató részre – a kód megírására!
## Csomagok importálása
Először is – importáljuk a szükséges csomagokat. Ez döntő fontosságú, mert a megfelelő importálás nélkül a kód nem ismeri fel az általunk használt osztályokat és metódusokat.
## Indítsa el C# projektjét
Nyissa meg a Visual Studio-t, és hozzon létre egy új C#-projektet, lehetőleg egy konzolalkalmazást, mivel ez lehetővé teszi a kimenet egyszerű megtekintését.
## Adja hozzá az Aspose.Cells Reference hivatkozást
- Kattintson a jobb gombbal a projektre a Solution Explorerben.
- Válassza a „Hozzáadás” > „Referencia” lehetőséget.
- Keresse meg azt a helyet, ahonnan letöltötte az Aspose.Cells könyvtárat, és foglalja bele a projektbe.
## Importálja a szükséges névtereket
 Miután hozzáadta a hivatkozást, adja hozzá a következőket`using` direktíva a fő fájl tetején:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Ez hozzáférést biztosít az Aspose.Cells névtér osztályaihoz.
Most, hogy kialakítottuk környezetünket, térjünk rá a szaftos részre – a kódolásra! Célunk, hogy egy Excel-fájl szövegmezőiben meghatározott címkéket keressünk, és helyettesítsünk a megadott szöveggel.
## 1. lépés: Határozza meg a forrás- és kimeneti könyvtárat
Először is meg kell adnunk, hogy a forrás Excel fájlunk hol található, és hova szeretnénk menteni a módosított verziót.
```csharp
// Forrás és kimeneti könyvtár
string sourceDir = "Your Document Directory"; // Váltson át a címtárra
string outputDir = "Your Document Directory"; // Váltson át a címtárra
```
## 2. lépés: Töltse be a munkafüzetet
Ide töltjük be az Excel munkafüzetünket. Ha a fájl nem létezik, hibát jelez. Tehát ellenőrizze, hogy a fájl elérési útja helyes-e!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Itt egy létező Excel fájlt töltünk be`sampleReplaceTagWithText.xlsx`.
## 3. lépés: Adja meg a címkéket és a helyettesítő szöveget
Ezután meg kell határoznunk a keresett címkéket, és azt, hogy mivel akarjuk lecserélni őket.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 Ebben a példában a címkék a következővel vannak felosztva`$`. Ezt tetszőleges határolóval helyettesítheti.
## 4. lépés: Ismételje meg a címkéket és cserélje ki
Létrehozunk egy hurkot, hogy végigmenjünk minden egyes cserélni kívánt címkén. Itt történik a varázslat!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## 5. lépés: Mentse el a munkafüzetet
Most, hogy elvégeztük a cseréket, ideje elmenteni a módosított munkafüzetet a kívánt formátumba. Így konvertálhatjuk PDF formátumba.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Különféle más formátumokban is mentheti, beleértve az XLSX-et is.
## 6. lépés: Valósítsa meg a cserelogikát
 Ez az a hely, ahol funkcionalitásunk szíve található. A`sheetReplace` metódus kezeli a tényleges cserét az Excel munkalapokon.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Először a munkafüzet egyes munkalapjait körbejárjuk.
- A fő címkét nem csak a cella tartalmában cseréljük le, hanem a fejlécekben és láblécekben is (ha vannak).
- Végül bejelöljük a lap minden szövegmezőjét, és a keresett címke alapján lecseréljük a bennük lévő szöveget.
## Következtetés
És íme! Most már megtanulta, hogyan cserélheti le a címkéket szöveggel az Excel-dokumentumok szövegmezőiben az Aspose.Cells for .NET segítségével. Ez valódi időt takaríthat meg, különösen akkor, ha ismétlődő feladatokat kezel táblázatokban.
## GYIK
### Cserélhetek címkéket egyszerre több Excel-fájlban?
Igen, a fájlok listáján végignézve ugyanazt a logikát több Excel-fájlra is alkalmazhatja.
### Szükségem van fizetős licencre az Aspose.Cells használatához?
 Kezdheti egy ingyenes próbaverzióval, de a teljes funkcionalitás érdekében licencet kell vásárolnia. Nézze meg[Az Aspose vásárlási lehetőségei](https://purchase.aspose.com/buy).
### Lecserélhetem a szövegmezőkben lévő képeket az Aspose.Cells segítségével?
Az Aspose.Cells elsősorban szöveggel foglalkozik. Szükség esetén azonban a képeket külön is módosíthatja.
### Milyen formátumokba menthetem a módosított Excel fájlt?
Különféle formátumokban mentheti, beleértve az XLSX, PDF, CSV stb.
### Hol találok támogatást az Aspose.Cells számára?
 Támogatást találhat és kérdéseket tehet fel a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
