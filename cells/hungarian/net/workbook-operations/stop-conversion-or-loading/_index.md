---
"description": "Tanuld meg, hogyan állíthatod le a munkafüzet-konvertálást az Aspose.Cells for .NET-ben az Interrupt Monitor használatával, részletes, lépésről lépésre szóló útmutatóval."
"linktitle": "Konverzió vagy betöltés leállítása az Interrupt Monitor használatával"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Konverzió vagy betöltés leállítása az Interrupt Monitor használatával"
"url": "/hu/net/workbook-operations/stop-conversion-or-loading/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Konverzió vagy betöltés leállítása az Interrupt Monitor használatával

## Bevezetés
A nagyméretű Excel-fájlokkal való munka gyakran hosszadalmas folyamatokkal jár, amelyek időt és erőforrásokat emészthetnek fel. De mi lenne, ha félúton leállíthatná a konvertálási folyamatot, amikor rájön, hogy valamit módosítani kell? Az Aspose.Cells for .NET rendelkezik egy Megszakításfigyelő nevű funkcióval, amely lehetővé teszi, hogy megszakítsa egy munkafüzet más formátumra, például PDF-re konvertálását. Ez életmentő lehet, különösen nagy adatfájlok esetén. Ebben az útmutatóban bemutatjuk, hogyan szakíthatja meg a konvertálási folyamatot az Aspose.Cells for .NET Megszakításfigyelőjével.
## Előfeltételek
Mielőtt belevágna, győződjön meg arról, hogy a következők a helyén vannak:
1. Aspose.Cells .NET-hez - Töltsd le [itt](https://releases.aspose.com/cells/net/).
2. .NET fejlesztői környezet – például a Visual Studio.
3. C# programozási alapismeretek – A C# szintaxis ismerete segít majd a haladásban.
## Csomagok importálása
Kezdésként importáljuk a szükséges csomagokat. Ezek az importálások a következőket tartalmazzák:
- Aspose.Cells: Az Excel fájlok kezelésének fő könyvtára.
- System.Threading: Szálak kezelésére, mivel ebben a példában két párhuzamos folyamat fog futni.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Bontsuk le a folyamatot részletes lépésekre. Minden egyes lépés segít megérteni az Interrupt Monitor beállításának és használatának fontosságát az Excel-munkafüzetek konvertálásának kezeléséhez.
## 1. lépés: Az osztály létrehozása és a kimeneti könyvtár beállítása
Először is szükségünk van egy osztályra, amelybe beágyazzuk a függvényeinket, valamint egy könyvtárra, ahová a kimeneti fájlt menteni fogjuk.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
Csere `"Your Document Directory"` a PDF fájl mentésének tényleges elérési útjával.
## 2. lépés: A megszakításfigyelő példányosítása
Ezután hozz létre egy InterruptMonitor objektumot. Ez a monitor segít a folyamat vezérlésében azáltal, hogy beállítja a folyamat bármely ponton történő megszakításának lehetőségét.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Ez a megszakításfigyelő csatolva lesz a munkafüzetünkhöz, lehetővé téve számunkra az átalakítási folyamat kezelését.
## 3. lépés: A munkafüzet beállítása az átalakításhoz
Most hozzunk létre egy munkafüzet-objektumot, rendeljük hozzá az InterruptMonitor objektumot, majd nyissuk meg az első munkalapot, hogy beszúrjunk néhány mintaszöveget.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
A fenti kód létrehoz egy munkafüzetet, beállítja hozzá az InterruptMonitort, és szöveget helyez el egy távoli cellában (`J1000000`). Ha szöveget helyezünk erre a cellapozícióra, az biztosítja, hogy a munkafüzet feldolgozása időigényesebb legyen, így az InterruptMonitornak elegendő ideje lesz beavatkozni.
## 4. lépés: Munkafüzet mentése PDF formátumban és a megszakítás kezelése
Most próbáljuk meg PDF formátumban menteni a munkafüzetet. Ehhez egy `try-catch` blokk az esetlegesen felmerülő megszakítások kezelésére.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Ha a folyamat megszakad, a kivétel észleli azt, és egy megfelelő üzenetet jelenít meg. Ellenkező esetben a munkafüzet PDF formátumban kerül mentésre.
## 5. lépés: A konverziós folyamat megszakítása
fő funkció itt a folyamat megszakításának lehetősége. Hozzáadunk egy késleltetést a következővel: `Thread.Sleep` és akkor hívd fel a `Interrupt()` módszer a konverzió leállítására 10 másodperc után.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Ez a késleltetés időt ad a munkafüzetnek a PDF-be konvertálás megkezdésére, mielőtt a megszakításjel elküldésre kerülne.
## 6. lépés: A szálak egyidejű végrehajtása
Ahhoz, hogy mindent összefogjunk, mindkét függvényt külön szálon kell elindítanunk. Így a munkafüzet-konverzió és a megszakításvárakozás egyszerre történhet.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
A fenti kód lefut `CreateWorkbookAndConvertItToPdfFormat` és `WaitForWhileAndThenInterrupt` párhuzamos szálakban, majd miután mindkét folyamat befejeződött, összekapcsoljuk őket.
## 7. lépés: Végső végrehajtás
Végül hozzáadunk egy `Run()` metódus a kód végrehajtásához.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
Ez `Run` A módszer a belépési pont a megszakítás működés közbeni elindításához és megfigyeléséhez.
## Következtetés
Ebben az oktatóanyagban azt vizsgáltuk meg, hogyan szakítható meg a konverziós folyamat az Aspose.Cells for .NET-ben. Az Interrupt Monitor hasznos eszköz nagyméretű Excel-fájlok kezelésekor, lehetővé téve a folyamatok leállítását anélkül, hogy meg kellene várni a befejezésüket. Ez különösen hasznos olyan helyzetekben, amikor az idő és az erőforrások értékesek, és gyors visszajelzésre van szükség.
## GYIK
### Mi az az Interrupt Monitor az Aspose.Cells for .NET-ben?  
A Megszakításfigyelő lehetővé teszi a munkafüzet konvertálásának vagy betöltésének folyamatának félbeszakítását.
### Használhatom az Interrupt Monitort a PDF-en kívül más formátumokhoz is?  
Igen, megszakíthatja a konverziókat más támogatott formátumokba is.
### Hogyan befolyásolja a Thread.Sleep() a megszakítás időzítését?  
A Thread.Sleep() függvény késleltetést hoz létre a megszakítás kiváltása előtt, időt adva a konverzió megkezdésére.
### Megszakíthatom a folyamatot 10 másodperc előtt?  
Igen, módosítsa a késleltetést `WaitForWhileAndThenInterrupt()` rövidebb időre.
### A megszakítási folyamat hatással lesz a teljesítményre?  
hatás minimális, és rendkívül előnyös a hosszan futó folyamatok kezeléséhez.
További információkért lásd a [Aspose.Cells .NET dokumentációhoz](https://reference.aspose.com/cells/net/)Ha segítségre van szüksége, tekintse meg a [Támogatási fórum](https://forum.aspose.com/c/cells/9) vagy szerezz egy [Ingyenes próbaverzió](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}