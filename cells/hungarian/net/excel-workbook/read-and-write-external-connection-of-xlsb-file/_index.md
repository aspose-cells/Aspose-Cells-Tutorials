---
title: Az XLSB fájl külső kapcsolatának olvasása és írása
linktitle: Az XLSB fájl külső kapcsolatának olvasása és írása
second_title: Aspose.Cells for .NET API Reference
description: Ebből az átfogó oktatóanyagból megtudhatja, hogyan kezelheti a külső kapcsolatokat XLSB-fájlokban az Aspose.Cells for .NET használatával.
weight: 130
url: /hu/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az XLSB fájl külső kapcsolatának olvasása és írása

## Bevezetés

Sziasztok, Excel-rajongók! Készen állsz, hogy belemerülj az XLSB fájlok és külső kapcsolatok lenyűgöző világába? Ha valaha is dolgozott Excellel, tudja, milyen hatékony és sokoldalú lehet, de néha megvannak a maga furcsaságai – különösen, ha külső adatbázisokhoz való kapcsolódásról van szó. Itt jön a segítség az Aspose.Cells for .NET! Ez a remek könyvtár lehetővé teszi az Excel-fájlok egyszerű kezelését. Ebben a cikkben lépésről lépésre végigvezetjük Önt egy XLSB-fájlban lévő külső kapcsolatok olvasásához és írásához.

## Előfeltételek

Mielőtt elkezdenénk, íme néhány dolog, amire szüksége lesz:

1. Alapvető C# ismerete: Ha jól ismeri a C# programozási nyelvet, az óriási segítség. Ha kényelmesen ír C# kódot, akkor kész!
2.  Aspose.Cells for .NET: Ezt a könyvtárat telepíteni kell a fejlesztői környezetbe. Ha még nem tette meg, könnyen letöltheti[itt](https://releases.aspose.com/cells/net/). 
3. IDE: Szüksége lesz egy kódszerkesztőre vagy egy integrált fejlesztési környezetre (IDE), például a Visual Studiora. 
4. Minta XLSB fájl: Egy minta XLSB fájllal fogunk dolgozni, amely külső kapcsolatokat tartalmaz. Létrehozhat sajátot, vagy letölthet mintákat online. 

Ha mindezen előfeltételek adottak, készen állunk, hogy belevágjunk a kódba!

## Csomagok importálása

Először is importáljuk a szükséges csomagokat a projektünkbe. Győződjön meg arról, hogy hozzáadott egy hivatkozást az Aspose.Cells-re a projektben. Ezt a következőképpen teheti meg C#-ban:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ezek az importálások hozzáférést biztosítanak az Excel-fájlok és kapcsolataik kezeléséhez szükséges funkciókhoz.

## 1. lépés: Állítsa be a könyvtárakat

Mielőtt az XLSB-fájllal dolgozna, be kell állítania a forrás- és kimeneti könyvtárakat. Ez a lépés elengedhetetlen a fájlok rendszerezéséhez.

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Output Directory";
```

 Ebben a kódrészletben`"Your Document Directory"` és`"Your Document Directory"` feltételezik, hogy lekérik a megfelelő elérési utat, ahol a bemeneti és kimeneti fájlok lesznek. Ezeket a metódusokat lecserélheti keménykódolt elérési utakra, ha úgy tetszik.

## 2. lépés: Töltse be az XLSB fájlt

Itt az ideje, hogy betöltse az Excel-fájlt egy munkafüzet-objektumba. Ez lehetőséget ad a benne lévő adatok manipulálására.

```csharp
// Töltse be a forrás Excel Xlsb fájlt
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Csak győződjön meg arról, hogy az XLSB fájl a megadott helyen található`sourceDir`. Ha az elérési út helyes, a munkafüzeted készen áll a manipulációra!

## 3. lépés: Nyissa meg a külső kapcsolatokat

A munkafüzet betöltése után hozzáférhet a külső kapcsolataihoz. Esetünkben az első adatbázis-kapcsolatot fogjuk lekérni.

```csharp
// Olvassa el az első külső kapcsolatot, amely valójában egy DB-kapcsolat
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Itt,`DataConnections[0]` a munkafüzet első kapcsolatára utal. Úgy öntjük, mint a`DBConnection` írja be a további manipulációhoz.

## 4. lépés: A csatlakozási információk kibontása

Most, hogy hozzáfért az adatbázis-kapcsolathoz, bontsa ki és nyomtassa ki annak részleteit a konzolra. Ez segít nekünk látni, hogy pontosan mivel dolgozunk.

```csharp
// Nyomtassa ki a DB-Connection nevét, parancsát és csatlakozási adatait
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Ez a lépés lehetővé teszi a külső kapcsolat aktuális állapotának ellenőrzését. Látni fogja a kapcsolat nevét, a használt parancsot és a csatlakozási információkat a konzolra nyomtatva.

## 5. lépés: Módosítsa a kapcsolatot

Néha már csak névváltoztatásra van szükség a dolgok egyértelműbbé tételéhez vagy az új elnevezési konvencióknak való megfeleléshez. Változtassuk meg a meglévő kapcsolat nevét valami relevánsabbra.

```csharp
// Módosítsa a kapcsolat nevét
dbCon.Name = "NewCust";
```

Ez a kódsor gyakorlatilag átnevezi a kapcsolatot az eredeti nevéről "NewCust"-ra. Ez egy egyszerű, de hatásos változás!

## 6. lépés: Mentse el a változtatásokat

A módosítások elvégzése után a módosításokat vissza kell mentenie az XLSB fájlba. Íme, hogyan kell csinálni:

```csharp
// Mentse el az Excel Xlsb fájlt
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Ez a kódsor menti a frissített munkafüzetet, megtartva az összes módosítást, beleértve az új kapcsolatnevet is.

## 7. lépés: Erősítse meg a végrehajtást

Végül erősítsük meg, hogy minden zökkenőmentesen működött. Egy egyszerű üzenet a végén egyértelművé teszi.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Ez az üzenet megnyugtatja Önt arról, hogy a kód sikeresen lefutott, és az összes módosítást a várt módon mentettük.

## Következtetés

És megvan! Sikeresen megtanulta, hogyan kell XLSB-fájlokban olvasni és írni a külső kapcsolatokat az Aspose.Cells for .NET segítségével. Ha követi ezeket a lépéseket, hatékonyan kezelheti Excel adatkapcsolatait, így az Excellel végzett munka sokkal egyszerűbb és kevésbé frusztráló. Ne feledje, hogy akár kiterjedt adatkészleteket kezel, akár egyszerűen rendszerezi adatait, az Aspose.Cells rendelkezik a szükséges eszközökkel.

## GYIK

### Mi az XLSB fájl?  
Az XLSB-fájl egy bináris Excel-fájlformátum, amely bináris formátumban tárolja a táblázat adatait, így kompaktabbá és gyorsabbá teszi a megnyitást.

### Hogyan telepíthetem az Aspose.Cells for .NET fájlt?  
 Könnyen letöltheti az Aspose webhelyéről[itt](https://releases.aspose.com/cells/net/).

### Használhatom ingyenesen az Aspose.Cells-t?  
 Igen! Kezdheti egy ingyenes próbaverzióval, amely elérhető[itt](https://releases.aspose.com/).

### Az Aspose.Cells támogat más fájlformátumokat?  
Teljesen! Az Aspose.Cells számos fájlformátumot támogat, beleértve az XLSX-et, CSV-t és még sok mást.

### Hol kérhetek segítséget, ha problémába ütközöm?  
Támogatást kaphat az Aspose fórumain[itt](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
