---
title: Lehetővé teszi a felhasználók számára a tartományok szerkesztését a munkalapon az Aspose.Cells használatával
linktitle: Lehetővé teszi a felhasználók számára a tartományok szerkesztését a munkalapon az Aspose.Cells használatával
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan hozhat létre szerkeszthető tartományokat Excel-munkalapokon az Aspose.Cells for .NET használatával, lehetővé téve az egyes cellák szerkeszthetőségét, míg a többit munkalapvédelemmel védi.
weight: 10
url: /hu/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lehetővé teszi a felhasználók számára a tartományok szerkesztését a munkalapon az Aspose.Cells használatával

## Bevezetés
Az Excel-dokumentumok gyakran tartalmaznak bizalmas adatokat vagy strukturált tartalmat, amelyet meg kíván védeni a nem kívánt szerkesztéstől. Előfordulhat azonban, hogy bizonyos cellákat vagy tartományokat szeretne szerkeszthetővé tenni bizonyos felhasználók számára. Itt lép be az Aspose.Cells for .NET hatékony eszközként, amely lehetővé teszi a teljes munkalap védelmét, miközben továbbra is szerkesztési engedélyeket ad a kijelölt tartományoknak. Képzeljen el egy olyan költségvetési táblázat megosztását, ahol csak bizonyos cellák szerkeszthetők, mások pedig biztonságban maradnak – az Aspose.Cells ezt egyszerűvé és hatékonysá teszi.
## Előfeltételek
Mielőtt belemerülnénk a kódolási részbe, győződjünk meg arról, hogy mindennel rendelkezünk, amire szükségünk van:
-  Aspose.Cells for .NET: Győződjön meg arról, hogy telepítette az Aspose.Cells for .NET könyvtárat. Letöltheti[itt](https://releases.aspose.com/cells/net/).
- Fejlesztői környezet: Visual Studio vagy bármely C#-kompatibilis IDE.
- .NET-keretrendszer: 4.0 vagy újabb verzió.
- Licenc: A próbaidőszaki korlátozások elkerülése érdekében fontolja meg licenc beszerzését. Megszerezheti a[ideiglenes engedély itt](https://purchase.aspose.com/temporary-license/).
## Csomagok importálása
Ügyeljen arra, hogy a kód elején szerepeljen a szükséges Aspose.Cells névtér:
```csharp
using System.IO;
using Aspose.Cells;
```
Ez biztosítja, hogy hozzáférjen minden osztályhoz és metódushoz, amely a védett tartományok beállításához szükséges az Excel-fájlokban.
Most, hogy az alapok megvannak, nézzük végig a kódot részletesen, lépésenként.
## 1. lépés: Állítsa be a könyvtárat
Mielőtt a fájlokkal dolgozna, be kell állítania azt a könyvtárat, ahová az Excel-fájlt menteni fogja. Ez biztosítja a fájlok jól szervezett és biztonságos tárolását.
```csharp
// Határozza meg a dokumentumkönyvtár elérési útját
string dataDir = "Your Document Directory";
// Ellenőrizze, hogy létezik-e a könyvtár, ha nem, hozza létre
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
A kód ezen része biztosítja, hogy a könyvtár készen álljon a fájlműveletekre. Tekintsd úgy, hogy lefekteti az alapot mindennek, ami ezután következik.
## 2. lépés: Inicializálja a munkafüzetet és a munkalapot
Most lépjünk tovább egy új munkafüzet létrehozásával, és nyissa meg az alapértelmezett munkalapot.
```csharp
// Új munkafüzet inicializálása
Workbook book = new Workbook();
// Nyissa meg a munkafüzet első munkalapját
Worksheet sheet = book.Worksheets[0];
```
Itt inicializálunk egy Excel-munkafüzetet, és kiválasztjuk benne az első munkalapot. Ez a munkalap lesz az a vászon, ahol alkalmazzuk a védelmi beállításainkat és meghatározzuk a szerkeszthető tartományokat.
## 3. lépés: Nyissa meg a Tartományok szerkesztésének engedélyezése gyűjteményt
 Az Aspose.Cells rendelkezik egy ún`AllowEditRanges`, amely tartományok gyűjteménye, amelyek akkor is szerkeszthetők, ha a munkalap védett.
```csharp
// Nyissa meg a Tartományok szerkesztésének engedélyezése gyűjteményt
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Ez a sor hozzáférést biztosít a tartományok egy speciális gyűjteményéhez, amely szerkeszthető lesz. Tekintse úgy, mint egy „VIP” területet a munkalapon, ahol csak meghatározott tartományok léphetnek át a védelemből.
## 4. lépés: Védett tartomány meghatározása és létrehozása
Most határozzunk meg és hozzunk létre egy védett tartományt a munkalapunkon. Megadjuk a tartomány kezdő és záró celláját.
```csharp
// Adjon meg egy ProtectedRange változót
ProtectedRange protectedRange;
// Adjon hozzá egy új tartományt a gyűjteményhez adott névvel és cellapozíciókkal
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
Ebben a kódblokkban:
- `EditableRange` a tartományhoz rendelt név.
- számok (1, 1, 3, 3) határozzák meg a tartomány koordinátáit, vagyis a B2 cellától (1. sor, 1. oszlop) a D4 celláig (3. sor, 3. oszlop) kezdődik.
## 5. lépés: Állítson be jelszót a védett tartományhoz
A fokozott biztonság érdekében jelszót állíthat be a védett tartományhoz. Ez a lépés egy további védelmi réteget ad, hogy csak a jogosult felhasználók szerkeszthessék a tartományt.
```csharp
// Állítson be jelszót a szerkeszthető tartományhoz
protectedRange.Password = "123";
```
Itt adtunk hozzá egy jelszót (`"123"`) a védett tartományba. Ez a jelszókövetelmény további szabályozási szintet biztosít afelől, hogy ki végezhet változtatásokat.
## 6. lépés: Védje meg a munkalapot
A szerkeszthető tartomány létrehozásával a következő lépés a teljes munkalap védelme. Ez a védelmi beállítás biztosítja, hogy a meghatározott tartományon kívül eső összes cella zárolva legyen és ne szerkeszthető legyen.
```csharp
// Alkalmazzon védelmet a munkalapra, így az összes többi cella nem szerkeszthető
sheet.Protect(ProtectionType.All);
```
 A`Protect`metódus zárolja a teljes munkalapot, kivéve a szerkeszthetőként meghatározott tartományokat. Ez a lépés lényegében egy biztonságos „csak olvasható” környezetet hoz létre, amely szükség szerint hozzáfér bizonyos cellákhoz.
## 7. lépés: Mentse el a munkafüzetet
Az utolsó lépés a munkafüzet mentése, így a beállítások alkalmazása és tárolása megtörténik.
```csharp
// Mentse az Excel fájlt a megadott könyvtárba
book.Save(dataDir + "protectedrange.out.xls");
```
Ebben a lépésben a munkafüzetünket „protectedrange.out.xls” néven mentjük az 1. lépésben beállított könyvtárba. Most már van egy teljesen működőképes, biztonságos Excel-fájlja, amelyben csak bizonyos tartományok szerkeszthetők!
## Következtetés
Az Aspose.Cells for .NET kiváló módot biztosít az Excel-fájlok védelmének és engedélyeinek kezelésére. Szerkeszthető tartományok létrehozásával biztonságossá teheti munkalapjait, miközben bizonyos területek továbbra is elérhetők maradnak. Ez a funkció különösen hasznos az együttműködési dokumentumoknál, ahol csak néhány cella legyen nyitva szerkesztésre, míg mások zárva maradnak.
## GYIK
### Hozzáadhatok több szerkeszthető tartományt egy munkalaphoz?
Igen, több tartományt is hozzáadhat, ha egyszerűen megismétli a`allowRanges.Add()` módszer minden új tartományhoz.
### Mi a teendő, ha később el akarok távolítani egy védett tartományt?
 Használja a`allowRanges.RemoveAt()` módszert az eltávolítani kívánt tartomány indexével.
### Beállíthatok különböző jelszavakat az egyes tartományokhoz?
 Teljesen. Minden`ProtectedRange` saját egyedi jelszóval rendelkezhet, amely részletes szabályozást biztosít.
### Mi történik, ha szerkeszthető tartományok nélkül védem le a munkalapot?
Ha nem ad meg szerkeszthető tartományokat, a teljes munkalap nem szerkeszthető, miután védetté válik.
### Látható a védett tartomány más felhasználók számára?
Nem, a védelem belső. A felhasználók csak akkor kérik a jelszó megadását, ha megpróbálják szerkeszteni a védett területet.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
