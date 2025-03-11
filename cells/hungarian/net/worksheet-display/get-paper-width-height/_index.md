---
title: Papírszélesség és -magasság munkalapnyomtatáshoz
linktitle: Papírszélesség és -magasság munkalapnyomtatáshoz
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan állíthatja be a papír szélességét és magasságát munkalapnyomtatáshoz az Aspose.Cells for .NET alkalmazásban.
weight: 16
url: /hu/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Papírszélesség és -magasság munkalapnyomtatáshoz

## Bevezetés
A dokumentumok pontos nyomtatásához ismerni kell a papír méretét. Ha Ön fejlesztő, vagy olyan alkalmazáson dolgozik, amely Excel-fájlokkal foglalkozik, akkor lehet, hogy tudnia kell, hogyan tudja meghatározni a papír szélességét és magasságát a munkalapok nyomtatásakor. Szerencsére az Aspose.Cells for .NET robusztus módot biztosít az Excel-dokumentumok programozott kezelésére. Ebben a cikkben végigvezetjük Önt a papírméret sajátosságainak meghatározásának folyamatán, egyszerű példákon keresztül az alapvető fogalmak illusztrálására. 
## Előfeltételek
Mielőtt belemerülnénk a technikai részletekbe, tegyünk egy kis alapmunkát. Az oktatóanyag sikeres követéséhez a következőkre lesz szüksége:
### 1. C# alapismeretek
Jól ismernie kell a C# programozást, mivel .NET környezetben fogunk dolgozni.
### 2. Aspose.Cells Library
Győződjön meg arról, hogy az Aspose.Cells könyvtár telepítve van a projektben. Ha még nem tette meg, letöltheti a legújabb verziót a[Aspose.Cells letöltési oldal](https://releases.aspose.com/cells/net/).
### 3. Visual Studio IDE
C#-projektjei futtatásához és kezeléséhez előnyös a Visual Studio. Minden olyan verzió, amely támogatja a .NET-et, kiválóan működik.
### 4. Érvényes Aspose Licenc
 Míg az Aspose.Cells kipróbálható, fontolja meg a licenc vásárlását, ha hosszú távú projektekhez használja. keresztül meg lehet vásárolni[ezt a linket](https://purchase.aspose.com/buy) vagy fedezze fel a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) rövid tesztelési fázisokhoz.
Ha minden készen van, térjünk rá a kódra!
## Csomagok importálása
Utunk első lépése az alapvető névterek importálása. Ez kulcsfontosságú, mivel lehetővé teszi számunkra, hogy hozzáférjünk azokhoz az osztályokhoz és metódusokhoz, amelyeket az Excel-fájlok kezeléséhez fogunk használni. Íme, hogyan kell csinálni:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Ügyeljen arra, hogy ezt a sort helyezze el a .cs fájl tetején. Most, hogy elkészült az importálás, folytassuk a munkafüzet létrehozását és a munkalap elérését.
## 1. lépés: A munkafüzet létrehozása
Kezdjük azzal, hogy létrehozunk egy példányt a`Workbook` osztály. Ez képezi az Excel fájlkezelés alapját.
```csharp
Workbook wb = new Workbook();
```
Ez a sor azt mondja a programnak, hogy inicializáljon egy új munkafüzetet, és beállítson bennünket, hogy belemerüljünk a munkalapjainkba.
## 2. lépés: Nyissa meg az első munkalapot
Ezután elérjük az újonnan létrehozott munkafüzetünk első munkalapját. Ez elég egyértelmű:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Itt elérjük a munkafüzetünk első (0-val indexelt) lapját. Itt állítjuk be a papírméreteket.
## A papírméret beállítása és a méretek visszakeresése
Most belépünk a művelet lényegébe – a papírméret beállításához és a méretek visszakereséséhez! Bontsuk ezt le lépésről lépésre.
## 3. lépés: Állítsa a Papírméretet A2-re
Először állítsuk be a papírméretünket A2-re, és nyomtassuk ki a méreteit.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Ezt a beállítást követően használjuk`Console.WriteLine` a méretek megjelenítéséhez. Amikor ezt futtatja, az A2-es papír szélessége és magassága hüvelykben jelenik meg.
## 4. lépés: Állítsa a Papírméretet A3-ra
Itt az ideje az A3-nak! Egyszerűen megismételjük a folyamatot:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Voila! A nyilatkozat kinyomtatja az A3-as papír adott magasságát és szélességét.
## 5. lépés: Állítsa a Papírméretet A4-re
Ugyanezt a mintát követve nézzük meg az A4 méretét:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Így megkapjuk az A4-es méreteket – ez az egyik leggyakrabban használt papírméret.
## 6. lépés: Állítsa a Papírméretet Letter értékre
A papírméret-feltárás teljessé tételéhez állítsa Letter méretre:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Ismét látni fogjuk a Letter méret konkrét szélességét és magasságát.
## Következtetés
És megvan! Most tanulta meg, hogyan állíthatja be a különböző méretű papír szélességét és magasságát, amikor munkalapokat készít nyomtatásra az Aspose.Cells for .NET segítségével. Ez a segédprogram hihetetlenül hasznos lehet, különösen akkor, ha a nyomtatási elrendezéseket tervezi, vagy a nyomtatási beállításokat programozottan kezeli. A hüvelykben megadott méretek pontos ismeretével elkerülheti a gyakori buktatókat, és biztosíthatja, hogy dokumentumait a rendeltetésszerűen nyomtatja ki.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amely számos szolgáltatást biztosít az Excel-fájlok programozott kezeléséhez.
### Hogyan kezdhetem el az Aspose.Cells-t?
Kezdje a könyvtár letöltésével a[Aspose honlapja](https://releases.aspose.com/cells/net/) és kövesse a dokumentációt a projektben való beállításához.
### Használhatom ingyenesen az Aspose.Cells-t?
Az Aspose.Cells próbaverziót kínál, amellyel felfedezheti funkcióit. A hosszú távú használathoz licencet kell vásárolnia.
### Milyen papírméreteket támogat az Aspose.Cells?
Az Aspose.Cells különféle papírméreteket támogat, beleértve az A2, A3, A4, Letter és sok más papírméretet.
### Hol találhatok további forrásokat vagy támogatást az Aspose.Cells számára?
 Ellenőrizheti a[Aspose fórum](https://forum.aspose.com/c/cells/9) közösségi segítségért és a[dokumentáció](https://reference.aspose.com/cells/net/) oktatóanyagokhoz és referenciaanyagokhoz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
