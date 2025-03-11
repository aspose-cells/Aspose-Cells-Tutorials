---
title: A VBAMacro User Form Designer Storage másolása a munkafüzetbe az Aspose.Cells használatával
linktitle: A VBAMacro User Form Designer Storage másolása a munkafüzetbe az Aspose.Cells használatával
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan másolhatja hatékonyan a VBA Macro User Form Designer alkalmazást az Aspose.Cells for .NET-ben az átfogó, lépésről lépésre bemutató oktatóanyagunkkal! Oldja fel az Excelben rejlő lehetőségeket.
weight: 11
url: /hu/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A VBAMacro User Form Designer Storage másolása a munkafüzetbe az Aspose.Cells használatával

## Bevezetés
Üdvözöljük! Ha szeretné javítani az Excel-élményt VBA makrók és felhasználói űrlapok segítségével, akkor jó helyen jár! Ebben az útmutatóban belemerülünk abba, hogyan másolhat zökkenőmentesen egy VBA Macro UserForm Designert egyik munkafüzetből a másikba az Aspose.Cells for .NET használatával. Akár tapasztalt fejlesztő vagy, akár csak kezdő, mi végigvezetünk minden döntő lépésen. Tekintse ezt az útmutatót az Excel-fájlok programozott kezelésének elsajátításához. Készen állsz a merülésre? Menjünk!
## Előfeltételek
Mielőtt belevágnánk a kódolás finomságába, győződjünk meg arról, hogy mindennel rendelkezünk, amire szükségünk van:
1. C# fejlesztői környezet: rendelkeznie kell egy munkakörnyezettel, amely készen áll a C# fejlesztésre. A Visual Studio erősen ajánlott.
2.  Aspose.Cells for .NET Library: Győződjön meg arról, hogy az Aspose.Cells könyvtár integrálva van a projektbe. Könnyen lehet[töltse le itt](https://releases.aspose.com/cells/net/).
3. A VBA és az Excel makrók alapismeretei: A VBA és az Excel makrók működésének alapos ismerete segít abban, hogy könnyedén navigáljon ezen az oktatóanyagon.
4. Felhasználói űrlapot tartalmazó Excel-fájl: Kísérletezni, létrehozni vagy beszerezni egy felhasználói űrlapot tartalmazó Excel-munkafüzetet, lehetőleg engedélyezett makróval (pl.`.xlsm` fájlok).
## Csomagok importálása
A C# projektben importálnia kell bizonyos névtereket a fájl tetején az Aspose.Cells funkciók használatához. Íme, hogyan kell csinálni:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Ezeknek a névtereknek a használata lehetővé teszi az Aspose.Cells könyvtárba ágyazott összes hatékony eszköz elérését. 
Most, hogy az előfeltételeink és a csomagjaink megvannak, ideje rátérni a szórakoztató részre: a kódolásra! Bontsuk le lépésről lépésre.
## 1. lépés: Határozza meg a forrás- és kimeneti könyvtárait
Először is meg kell határoznia, hol találhatók a fájlok:
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
 Tessék, cserélje ki`"Your Document Directory"` a fájlok tárolási útvonalával. Ez az a hely, ahonnan a forrásmunkafüzetünk (a UserForm-mal) lekerül, és az új munkafüzet mentésre kerül.
## 2. lépés: Hozzon létre egy üres célmunkafüzetet
Ezután hozzuk létre a célmunkafüzetünket, amelybe a felhasználói űrlapot és a makrókat másoljuk:
```csharp
// Hozzon létre üres célmunkafüzetet
Workbook target = new Workbook();
```
Ez a kódsor inicializál egy új, üres munkafüzetet, amelyet adatokkal tölthetünk meg. Gondoljon rá, mint egy üres vászonra remekműve számára!
## 3. lépés: Töltse be a sablon munkafüzetet
Be kell töltenünk a felhasználói űrlapot és a makrókat tartalmazó munkafüzetet:
```csharp
// Töltse be a VBA-Macro Designer felhasználói űrlapot tartalmazó Excel-fájlt
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Ügyeljen arra, hogy változtasson`"sampleDesignerForm.xlsm"` a tényleges fájl nevére. Ez a munkafüzet olyan, mint a receptkönyved – ebből fogjuk az alapanyagokat!
## 4. lépés: Másolja a munkalapokat a célmunkafüzetbe
Most kezdjük el a munkalapok másolását a sablonunkból a célmunkafüzetbe:
```csharp
// Másolja az összes sablonmunkalapot a célmunkafüzetbe
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Helyezze az üzenetet a célmunkalap A2 cellájába
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
Ebben a lépésben végigpörgetjük a sablonban lévő egyes munkalapokat, és átmásoljuk őket a célmunkafüzetünkbe. Ha belegondolsz, az olyan, mintha a legjobb receptjeidet áthelyeznéd egyik szakácskönyvből a másikba!
## 5. lépés: Másolja ki a VBA-makrókat a sablonból
Ezután átmásoljuk a VBA makrókat, beleértve a UserForm Designer modulokat is, az új munkafüzetünkbe:
```csharp
// Másolja a VBA-Macro Designer felhasználói űrlapot a sablonból a célba
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Másolja ki ezt a munkafüzet modul kódját
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Másolja a többi modul kódját és adatait
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Szerezze be a felhasználói űrlap adatait, azaz a tervezői tárhelyet
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Adja hozzá a tervezői tárhelyet a cél Vba Projecthez
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Ez a tetemes kódcsomag kezeli a sablonfájlban lévő VBA-modulok ellenőrzését. Átmásoljuk a UserForm dizájnt és a hozzá tartozó kódokat. Ez olyan, mintha nem csak a nagymama híres pite receptjét, hanem a pontos sütési technikáit is megkapnád!
## 6. lépés: Mentse el a cél munkafüzetet
Miután az összes példányt elértük, ideje megtakarítani a kemény munkánkat:
```csharp
// Mentse el a célmunkafüzetet
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Győződjön meg arról, hogy szükség szerint módosítja a kimeneti fájl nevét. Mentés után hatékonyan létrehozhatja a munkafüzet saját testreszabott verzióját, amely tele van makróval és felhasználói űrlapokkal. Ez mennyire izgalmas?
## 7. lépés: Erősítse meg a sikert
Végül nyomtassunk egy sikerüzenetet a konzolra:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Ez a kis vonal megnyugtat, hogy a folyamat zökkenőmentesen ment. Ez a cseresznye a kódoló krémed tetején!
## Következtetés
Gratulálok! Elkészítette a VBA makró felhasználói űrlaptervezőjének egyik munkafüzetből a másikba való másolásához szükséges lépésenkénti útmutatót az Aspose.Cells for .NET használatával. Lehet, hogy elsőre kissé elsöprőnek tűnik, de gyakorlással profiként fogod kezelni a munkafüzet-manipulációkat. Ne feledje, a kódolás a gyakorlatról szól, ezért ne riadjon vissza attól, hogy különféle dolgokat próbáljon ki Excel-fájljaiban. Ha bármilyen kérdése van, vagy bármilyen problémába ütközik, bátran nézze meg az Aspose fórumait vagy a dokumentációt támogatásért!
## GYIK
### Az Excel mely verzióit támogatja az Aspose.Cells?
Az Aspose.Cells az Excel formátumok széles skáláját támogatja, beleértve az XLSX, XLSM, CSV és sok más formátumot.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen! Kezdheti egy ingyenes próbaverzióval, amely lehetővé teszi a könyvtár értékelését:[Ingyenes próbaverzió](https://releases.aspose.com/).
### Kell-e a Visual Studio a kód futtatásához?
Bár felhasználóbarát funkciói miatt erősen ajánlott, bármely C# IDE megteszi, ha támogatja a .NET fejlesztést.
### Hol találok további példákat és dokumentációt?
 Feltárhatod a[Aspose.Cells Documentation](https://reference.aspose.com/cells/net/) további példákért és mélyreható magyarázatokért.
### Hogyan oldhatom meg a problémákat az Aspose.Cells használata közben?
 Meg kell látogatnia a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9) segítségért a közösségtől és az Aspose támogató személyzetétől.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
