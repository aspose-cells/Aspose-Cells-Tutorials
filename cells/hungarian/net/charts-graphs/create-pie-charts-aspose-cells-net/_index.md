---
"date": "2025-04-05"
"description": "Tanuld meg, hogyan hozhatsz létre dinamikus kördiagramokat vezető vonalakkal az Aspose.Cells for .NET segítségével. Kövesd ezt az útmutatót az adatvizualizációs készségeid fejlesztéséhez."
"title": "Kördiagramok létrehozása vezető vonalakkal az Aspose.Cells .NET-ben&#58; Átfogó útmutató"
"url": "/hu/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Kördiagramok létrehozása vezető vonalakkal az Aspose.Cells .NET használatával

## Bevezetés
Fejleszd adatvizualizációdat informatívabb kördiagramok létrehozásával az Aspose.Cells for .NET segítségével. Ez a lépésről lépésre bemutatja, hogyan adhatsz hozzá vezető vonalakat a kördiagram szegmenseihez, így könnyebben azonosíthatod a megfelelő adatkategóriákat egy pillantással. Az oktatóanyag követésével a vizualizációid vizuálisan vonzóak és rendkívül funkcionálisak lesznek.

**Amit tanulni fogsz:**
- Az Aspose.Cells .NET-hez való beállítása a környezetedben
- Egyéni vezetővonal-kördiagramok létrehozása C#-ban
- Diagram mentése képként vagy Excel-munkafüzetben

Győződj meg róla, hogy minden készen áll a hatékony követés érdekében.

## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy megfelel a következő előfeltételeknek:

- **Könyvtárak és verziók**Telepítse az Aspose.Cells for .NET programot. Győződjön meg róla, hogy a projekt a legújabb verzióval van beállítva.
- **Környezet beállítása**Ez az útmutató feltételezi az Aspose.Cells kompatibilis .NET környezetét.
- **Ismereti előfeltételek**Előnyt jelent a C# programozás és az Excel műveletek alapvető ismerete.

## Az Aspose.Cells beállítása .NET-hez
Kezdésként telepítsd az Aspose.Cells-t a projektedbe a következőképpen:

**.NET parancssori felület**
```bash
dotnet add package Aspose.Cells
```

**Csomagkezelő**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

A teljes funkcionalitás eléréséhez a következő lehetőségek közül választva szerezzen be licencet:
- **Ingyenes próbaverzió**: Kezdje el az ingyenes próbaidőszakot a következőn: [Aspose letöltési oldal](https://releases.aspose.com/cells/net/).
- **Ideiglenes engedély**: Ideiglenes jogosítvány beszerzése [itt](https://purchase.aspose.com/temporary-license/).
- **Vásárlás**A teljes funkciók eléréséhez vásároljon licencet [itt](https://purchase.aspose.com/buy).

Inicializáld az Aspose.Cells függvényt a projektedben a következő egy példányának létrehozásával: `Workbook` osztály.

## Megvalósítási útmutató

### Munkafüzet és munkalap létrehozása
1. **A munkafüzet inicializálása**
   Hozz létre egy új munkafüzetet XLSX formátumban:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Az első munkalap elérése**
   Az első munkalapon adjuk meg az adatokat:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Adatok hozzáadása kördiagramhoz**
   Töltsd ki a munkalapot kategóriákkal és értékekkel:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Add hozzá a fennmaradó kategórianeveket...
   worksheet.Cells["B1"].PutValue(10.4);
   // Adja hozzá a megfelelő értékeket...
   ```

### Kördiagram hozzáadása a munkalaphoz
1. **A kördiagram létrehozása**
   Kördiagram létrehozása és hozzáadása a munkalap diagramgyűjteményéhez:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Sorozat- és kategóriaadatok konfigurálása**
   Kapcsolja össze az adatokat a sorozatokhoz és a kategóriákhoz:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Adatcímkék testreszabása**
   Jelmagyarázat megjelenítésének kikapcsolása, adatfeliratok beállítása a kategórianevek és százalékok megjelenítéséhez:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Vezető vonalak megvalósítása
1. **Vezetővonalak bekapcsolása**
   Vezetővonalak engedélyezése a tisztább vizuális kapcsolatok érdekében:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Adatcímkék pozíciójának beállítása**
   A láthatóság biztosítása a címkepozíciók beállításával:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### A diagram és a munkafüzet mentése
1. **Mentés képként**
   A diagram renderelése képfájlba:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Munkafüzet mentése**
   Mentse el a munkafüzetet a diagram Excelben való megtekintéséhez:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Gyakorlati alkalmazások
- **Pénzügyi jelentések**Egyértelműen mutassák be a költségvetési elosztásokat.
- **Marketinganalitika**: A piaci részesedési adatok hatékony vizualizálása prezentációkban vagy jelentésekben.
- **Értékesítési elemzés**Könnyedén megjelenítheti az értékesítés megoszlását a különböző régiók/termékek között.

Az integrációs lehetőségek közé tartozik ezen vizualizációk webes alkalmazásokba exportálása vagy automatizált jelentéskészítő eszközökbe való beágyazásuk.

## Teljesítménybeli szempontok
Az Aspose.Cells használatakor az optimális teljesítmény érdekében vegye figyelembe a következőket:
- Minimalizálja a memóriába egyszerre betöltött nagy adathalmazokat.
- Használj hatékony ciklusokat, és kerüld a felesleges számításokat a ciklusokon belül.
- Rendszeresen tisztítsa meg az erőforrásokat, például a munkafüzet-objektumokat, a memóriavesztés megelőzése érdekében.

## Következtetés
Megtanultad, hogyan készíthetsz kördiagramokat vezető vonalakkal az Aspose.Cells for .NET segítségével. Ez a funkció javítja az adatvizualizációk áttekinthetőségét, így azok könnyebben hozzáférhetők és hatásosabbak. 

**Következő lépések:**
Fedezze fel a diagramok megjelenésének további testreszabási lehetőségeit, vagy kísérletezzen az Aspose.Cells-ben elérhető más diagramtípusokkal.

## GYIK szekció
1. **Mi a vezető vonal a kördiagramban?**
   vezetővonalak az adatfeliratokat a megfelelő szegmensekhez kötik, javítva az olvashatóságot.

2. **Ingyenesen használhatom az Aspose.Cells-t?**
   Igen, ingyenes próbaverzióval is elkezdheted, de a teljes funkciók használatához licenc szükséges.

3. **Lehetséges diagramokat képként exportálni?**
   Feltétlenül! Használd `ImageOrPrintOptions` a diagram PNG vagy JPEG formátumban történő mentéséhez.

4. **Hogyan tudom manuálisan beállítani az adatcímkék pozícióját?**
   Módosítsa az adatcímkék X és Y koordinátáit a sorozatpont-hurkon belül.

5. **Integrálható-e az Aspose.Cells más rendszerekkel?**
   Igen, adatbázisokkal, webszolgáltatásokkal és egyebekkel együtt használható automatizált jelentéskészítési megoldásokhoz.

## Erőforrás
- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/)
- [Aspose.Cells letöltése](https://releases.aspose.com/cells/net/)
- [Licenc vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próbaverzió](https://releases.aspose.com/cells/net/)
- [Ideiglenes engedély](https://purchase.aspose.com/temporary-license/)
- [Támogatási fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}