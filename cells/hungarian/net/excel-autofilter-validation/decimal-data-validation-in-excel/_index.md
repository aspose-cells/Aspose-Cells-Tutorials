---
"description": "Ismerje meg, hogyan valósíthat meg decimális adatellenőrzést Excelben az Aspose.Cells for .NET használatával könnyen követhető útmutatónkkal. Növelje az adatok integritását erőfeszítés nélkül."
"linktitle": "Decimális adatérvényesítés Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Decimális adatérvényesítés Excelben"
"url": "/hu/net/excel-autofilter-validation/decimal-data-validation-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Decimális adatérvényesítés Excelben

## Bevezetés

A pontos adatokat tartalmazó táblázatok létrehozása elengedhetetlen a világos kommunikációhoz minden vállalkozásban. Az adatok pontosságának biztosításának egyik módja az adatérvényesítés használata az Excelben. Ebben az oktatóanyagban az Aspose.Cells for .NET erejét fogjuk kihasználni egy decimális adatérvényesítési mechanizmus létrehozásához, amely megbízhatóan és tisztán tartja az adatait. Ha szeretné fejleszteni Excel-tudását, jó helyen jár!

## Előfeltételek

Mielőtt belemerülnénk a kódba, győződjünk meg róla, hogy mindent beállítottunk a zökkenőmentes működéshez:

1. Visual Studio: Töltsd le és telepítsd a Visual Studio alkalmazást, ha még nem tetted meg. Ez a tökéletes környezet .NET alkalmazások fejlesztéséhez.
2. Aspose.Cells .NET-hez: A projektedhez hozzá kell adni az Aspose.Cells könyvtárat. Letöltheted innen: [ezt a linket](https://releases.aspose.com/cells/net/).
3. C# alapismeretek: Bár mindent lépésről lépésre elmagyarázunk, a C# programozás alapvető ismerete jobb megértést biztosít a fogalmak terén.
4. .NET-keretrendszer: Győződjön meg arról, hogy telepítve van a szükséges, az Aspose.Cells-szel kompatibilis .NET-keretrendszer.
5. Könyvtárak: A fordítási hibák elkerülése érdekében hivatkozz az Aspose.Cells könyvtárra a projektedben.

Most, hogy az alapokkal tisztában vagyunk, térjünk át az izgalmas részre: a kódolásra.

## Csomagok importálása

Kezdéshez importálnod kell a szükséges csomagokat a C# fájlodba. Ez lehetővé teszi az Aspose.Cells funkcióinak elérését.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ha ezt a sort a fájl elejére illeszted, azzal arra utasítod a C#-ot, hogy keresse meg az Aspose.Cells funkciót, amely lehetővé teszi az Excel fájlok kezelését.

Most, hogy előkészítettük a terepet, nézzük meg a decimális adatellenőrzés Excel-munkalapban történő létrehozásához szükséges lépéseket.

## 1. lépés: Dokumentumkönyvtár beállítása

Mielőtt bármilyen fájlt mentene, győződjön meg arról, hogy a dokumentumkönyvtár megfelelően van beállítva:

```csharp
string dataDir = "Your Document Directory";
```

Csere `"Your Document Directory"` azzal az elérési úttal, ahová menteni szeretné az Excel-fájlokat.

## 2. lépés: A címtár létezésének ellenőrzése

Ez a kódrészlet ellenőrzi, hogy létezik-e a könyvtár, és létrehozza, ha nem:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Ez a lépés olyan, mintha egy új projekt elkezdése előtt ellenőriznéd, hogy a munkaterületed készen áll-e. Nincs rendetlenség, nincs stressz!

## 3. lépés: Munkafüzet-objektum létrehozása

Következő lépésként hozzunk létre egy új munkafüzet-objektumot, amely lényegében egy Excel-fájl:

```csharp
Workbook workbook = new Workbook();
```

Gondoljon a munkafüzetre úgy, mint egy üres vászonra az adatai számára. Ezen a ponton még nincs tartalma, de készen áll a festésre.

## 4. lépés: A munkalap létrehozása és elérése


Most hozzunk létre egy munkalapot, és nyissuk meg a munkafüzet első lapját:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Ahogy egy könyvnek is több oldala van, úgy egy munkafüzetnek is lehet több munkalapja. Jelenleg az elsővel foglalkozunk.

## 5. lépés: A validációs gyűjtemény beszerzése

Most hívjuk elő az érvényesítési gyűjteményt a munkalapról, mivel itt fogjuk kezelni az adatérvényesítési szabályainkat:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Ez a lépés ahhoz hasonlít, mintha a projekt megkezdése előtt átnéznéd az eszköztárat.

## 6. lépés: Az érvényesítéshez tartozó cellaterület meghatározása

Meg kell határoznunk azt a területet, ahol az érvényesítés érvényes:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Itt azt adjuk meg, hogy az adatérvényesítést egyetlen cellára alkalmazzuk – konkrétan a munkalap első cellájára (A1).

## 7. lépés: Érvényesítés létrehozása és hozzáadása

Hozzuk létre a validációs objektumunkat, és adjuk hozzá a validációs gyűjteményhez:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Most van egy validációs objektumunk, amelyet úgy fogunk konfigurálni, hogy érvényesítse a decimális feltételeket.

## 8. lépés: Az érvényesítési típus beállítása

Ezután meghatározzuk a kívánt validáció típusát:

```csharp
validation.Type = ValidationType.Decimal;
```

típus Decimálisra állításával arra utasítjuk az Excelt, hogy decimális értékeket várjon az érvényesített cellában.

## 9. lépés: Az operátor megadása

Most megadjuk a megengedett értékek feltételét. Biztosítani szeretnénk, hogy a beírt adatok két tartomány közé essenek:

```csharp
validation.Operator = OperatorType.Between;
```

Gondolj rá úgy, mintha egy határvonalat húznál. Minden, ezen a tartományon kívül eső számot elutasít a rendszer, így az adatod tiszta marad!

## 10. lépés: Határozza meg az érvényesítés határait

Ezután beállítjuk az érvényesítés alsó és felső határértékeit:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Ezekkel a korlátokkal minden tizedesjegy, függetlenül attól, hogy milyen nagy vagy kicsi, elfogadott, feltéve, hogy érvényes!

## 11. lépés: A hibaüzenet testreszabása

Biztosítsuk a felhasználókat arról, hogy miért utasították el a bemenetüket egy hibaüzenet hozzáadásával:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Ez felhasználóbarát élményt nyújt, mivel útmutatást nyújt a bevitelhez.

## 12. lépés: Az érvényesítési terület meghatározása

Most határozzuk meg azokat a cellákat, amelyek ezt az érvényesítést tartalmazni fogják:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Ebben a konfigurációban azt mondjuk, hogy az érvényesítés az A1-től az A10-es celláig érvényes.

## 13. lépés: Adja hozzá az érvényesítési területet

Most, hogy definiáltuk az érvényesítési területet, alkalmazzuk is:

```csharp
validation.AddArea(area);
```

Az érvényesítésed most már szilárdan a helyén van, készen áll a nem megfelelő bevitelek kiszűrésére!

## 14. lépés: A munkafüzet mentése

Végül mentsük el a munkafüzetet a decimális adatellenőrzéssel:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

És íme! Sikeresen létrehoztál egy decimális adatérvényesítéssel rendelkező munkafüzetet az Aspose.Cells for .NET használatával.

## Következtetés

Az Aspose.Cells for .NET használatával az Excelben a decimális adatérvényesítés megvalósítása gyerekjáték, ha követi ezeket az egyszerű lépéseket. Nemcsak azt biztosítja, hogy az adatok tiszták és strukturáltak maradjanak, hanem javítja a táblázatok általános adatintegritását is, így azok megbízhatóak és felhasználóbarátak lesznek.
Akár pénzügyben, projektmenedzsmentben vagy bármilyen olyan területen dolgozol, amely adatelemzést alkalmaz, ezeknek a készségeknek az elsajátítása jelentősen növelni fogja a termelékenységedet. Szóval próbáld ki! A táblázataid hálásak lesznek érte.

## GYIK

### Mi az adatérvényesítés az Excelben?
Az Excelben az adatérvényesítés egy olyan funkció, amely korlátozza az adott cellába vagy tartományba beírható adatok típusát, biztosítva az adatok integritását.

### Testreszabhatom a hibaüzenetet az adatellenőrzés során?
Igen! Egyéni hibaüzeneteket adhat meg, amelyek segítenek a felhasználóknak helytelen adatbevitel esetén.

### Ingyenesen használható az Aspose.Cells?
Az Aspose.Cells ingyenes próbaverziót kínál, de hosszú távú használathoz licencre lesz szükséged. További információt az ideiglenes licenc beszerzéséről itt találsz. [itt](https://purchase.aspose.com/temporary-license/).

### Milyen adattípusokat tudok validálni az Excelben?
Az Aspose.Cells segítségével különféle adattípusokat validálhatsz, beleértve az egész számokat, tizedesjegyeket, dátumokat, listákat és egyéni képleteket.

### Hol találok további Aspose.Cells dokumentációt?
Böngészheted a kiterjedt dokumentációt [itt](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}