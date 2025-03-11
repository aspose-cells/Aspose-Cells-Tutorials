---
title: Decimális adatok érvényesítése Excelben
linktitle: Decimális adatok érvényesítése Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel, hogyan valósíthatja meg a decimális adatok érvényesítését az Excelben az Aspose.Cells for .NET segítségével az egyszerűen követhető útmutatónkkal. Fokozatmentesen fokozza az adatok integritását.
weight: 11
url: /hu/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Decimális adatok érvényesítése Excelben

## Bevezetés

A pontos adatokat tartalmazó táblázatok készítése elengedhetetlen az egyértelmű kommunikációhoz bármely vállalkozásban. Az adatok pontosságának biztosításának egyik módja az adatellenőrzés az Excelben. Ebben az oktatóanyagban az Aspose.Cells for .NET erejét fogjuk hasznosítani egy decimális adatellenőrzési mechanizmus létrehozásához, amely megbízhatóan és tisztán tartja adatait. Ha Excel játékot keres, jó helyen jár!

## Előfeltételek

Mielőtt belemerülne a kódba, győződjön meg arról, hogy mindent beállított a zökkenőmentes vitorlázás élményéhez:

1. Visual Studio: Töltse le és telepítse a Visual Studio alkalmazást, ha még nem tette meg. Ez a tökéletes környezet .NET alkalmazások fejlesztéséhez.
2.  Aspose.Cells for .NET: Aspose.Cells könyvtárat kell hozzáadnia a projekthez. keresztül töltheti le[ezt a linket](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismeretek: Bár mindent lépésről lépésre elmagyarázunk, a C# programozás alapvető ismeretei jobban megértik a fogalmakat.
4. .NET-keretrendszer: Győződjön meg arról, hogy telepítve van a szükséges .NET-keretrendszer, amely kompatibilis az Aspose.Cells-szel.
5. Könyvtárak: A fordítási hibák elkerülése érdekében hivatkozzon az Aspose.Cells könyvtárra a projektben.

Most, hogy áttekintettük az alapokat, ugorjunk az izgalmas részre: a kódolásra.

## Csomagok importálása

A kezdéshez importálnia kell a szükséges csomagokat a C# fájlba. Ez lehetővé teszi az Aspose.Cells funkciók elérését.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ha ezt a sort a fájl tetejére helyezi, akkor azt mondja a C#-nak, hogy keresse az Aspose.Cells funkciót, amely lehetővé teszi az Excel-fájlok kezelését.

Most, hogy készen állunk, menjünk végig a decimális adatok érvényesítésének Excel-munkalapon történő létrehozásához szükséges lépéseken.

## 1. lépés: Állítsa be a dokumentumkönyvtárat

A fájlok mentése előtt meg kell győződnie arról, hogy a dokumentumkönyvtár megfelelően van beállítva:

```csharp
string dataDir = "Your Document Directory";
```

 Cserélje ki`"Your Document Directory"` azzal az elérési úttal, ahová menteni szeretné az Excel fájljait.

## 2. lépés: Ellenőrizze a címtár meglétét

Ez a kódrészlet ellenőrzi, hogy létezik-e a könyvtár, és létrehozza, ha nem:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Ez a lépés olyan, mintha egy új projekt elindítása előtt megbizonyosodna arról, hogy a munkaterülete készen áll. Nincs rendetlenség, nincs stressz!

## 3. lépés: Hozzon létre egy munkafüzet-objektumot

Ezután hozzunk létre egy új munkafüzet objektumot, amely lényegében egy Excel fájl:

```csharp
Workbook workbook = new Workbook();
```

Gondoljon a munkafüzetre úgy, mint egy üres vászonra az adatok számára. Jelenleg nincs tartalom, de készen áll a festésre.

## 4. lépés: A munkalap létrehozása és elérése


Most hozzunk létre egy munkalapot, és érjük el a munkafüzet első lapját:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Ahogy egy könyvnek több oldala van, a munkafüzetnek is több munkalapja lehet. Jelenleg az elsőre koncentrálunk.

## 5. lépés: Szerezze be az érvényesítési gyűjteményt

Most húzzuk ki az érvényesítési gyűjteményt a munkalapról, mivel itt kezeljük az adatérvényesítési szabályokat:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Ez a lépés hasonló az eszköztár ellenőrzéséhez a projekt elindítása előtt.

## 6. lépés: Határozza meg az érvényesítéshez szükséges cellaterületet

Meg kell határoznunk azt a területet, ahol az érvényesítés vonatkozik:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Itt azt írjuk elő, hogy az adatellenőrzés egyetlen cellára vonatkozik – pontosabban a munkalap első cellájára (A1).

## 7. lépés: Érvényesítés létrehozása és hozzáadása

Hozzuk létre az érvényesítési objektumunkat, és adjuk hozzá az érvényesítési gyűjteményhez:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Most van egy érvényesítési objektum, amelyet úgy fogunk konfigurálni, hogy érvényesítse a decimális feltételeinket.

## 8. lépés: Állítsa be az érvényesítés típusát

Ezután meghatározzuk a kívánt érvényesítés típusát:

```csharp
validation.Type = ValidationType.Decimal;
```

A típus Decimális értékre állításával arra utasítjuk az Excelt, hogy decimális értékeket várjon az ellenőrzött cellában.

## 9. lépés: Adja meg a kezelőt

Most megadjuk a megengedett értékek feltételét. Biztosítani szeretnénk, hogy a megadott adatok két tartomány közé esjenek:

```csharp
validation.Operator = OperatorType.Between;
```

Tekintsd úgy, mint egy határvonalat. Az ezen a tartományon kívül eső számokat a rendszer elutasítja, így az adatok tisztán maradnak!

## 10. lépés: Határozzon meg korlátokat az érvényesítéshez

Ezután beállítjuk az érvényesítés alsó és felső határát:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Ezekkel a korlátokkal minden tizedes számot elfogadunk, legyen az kicsi vagy nagy, mindaddig, amíg érvényes!

## 11. lépés: A hibaüzenet testreszabása

Egy hibaüzenet hozzáadásával biztosítsuk, hogy a felhasználók tudják, miért utasították el bevitelüket:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Ez felhasználóbarát élményhez vezet, mivel útmutatást ad a bevitelhez.

## 12. lépés: Határozza meg az érvényesítési területet

Most határozzuk meg azokat a cellákat, amelyek ezt az érvényesítést viselik:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Ebben a konfigurációban azt mondjuk, hogy az érvényesítés az A1-től A10-ig terjed.

## 13. lépés: Adja hozzá az érvényesítési területet

Most, hogy meghatároztuk az érvényesítési területünket, alkalmazzuk:

```csharp
validation.AddArea(area);
```

Az érvényesítés most már szilárdan a helyén van, készen áll a nem megfelelő bevitelek észlelésére!

## 14. lépés: Mentse el a munkafüzetet

Végül mentsük el a munkafüzetet a decimális adatok érvényesítésével:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

És megvan! Sikeresen létrehozott egy munkafüzetet decimális adatok érvényesítésével az Aspose.Cells for .NET használatával.

## Következtetés

A decimális adatok érvényesítésének végrehajtása Excelben az Aspose.Cells for .NET használatával gyerekjáték, ha követi ezeket az egyszerű lépéseket. Nemcsak arról gondoskodik, hogy az adatok tiszták és strukturáltak maradjanak, hanem javítja a táblázatok általános adatintegritását is, így azok megbízhatóak és felhasználóbarátok.
Legyen szó pénzügyről, projektmenedzsmentről vagy bármilyen adatjelentést használó területről, ezen készségek elsajátítása jelentősen növeli termelékenységét. Szóval hajrá, próbáld ki! A táblázatai hálásak lesznek érte.

## GYIK

### Mi az adatellenőrzés az Excelben?
Az adatellenőrzés az Excelben egy olyan szolgáltatás, amely korlátozza az adott cellába vagy tartományba beírható adatok típusát, így biztosítva az adatok integritását.

### Testreszabhatom a hibaüzenetet az adatellenőrzés során?
Igen! Egyéni hibaüzeneteket biztosíthat, amelyek útmutatást nyújtanak a felhasználók számára, ha helytelen adatbevitelt végeznek.

### Az Aspose.Cells ingyenesen használható?
 Az Aspose.Cells ingyenes próbaverziót kínál, de a hosszú távú használathoz licencre lesz szüksége. Az ideiglenes engedély megszerzéséről további információkat talál[itt](https://purchase.aspose.com/temporary-license/).

### Milyen adattípusokat ellenőrizhetek Excelben?
Az Aspose.Cells segítségével különféle adattípusokat ellenőrizhet, beleértve az egész számokat, a tizedesjegyeket, a dátumokat, a listákat és az egyéni képleteket.

### Hol találok további Aspose.Cells dokumentációt?
 Megtekintheti a kiterjedt dokumentációt[itt](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
