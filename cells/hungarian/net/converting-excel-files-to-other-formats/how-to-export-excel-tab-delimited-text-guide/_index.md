---
category: general
date: 2026-02-26
description: Hogyan exportáljunk Excel-t tabulátorral elválasztott txt fájlba C#-ban.
  Tanulja meg az Excel exportálását tabulátorral, az Excel txt‑be konvertálását, és
  az Excel exportálását határolóval három egyszerű lépésben.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: hu
og_description: Hogyan exportáljunk Excel-t tabulátorral elválasztott txt fájlba C#-ban.
  Ez az útmutató bemutatja az Excel tabulátorral való exportálását, az Excel txt‑be
  konvertálását és az Excel határolóval történő exportálását.
og_title: Hogyan exportáljuk az Excelt – Tabulátorral elválasztott szöveg útmutató
tags:
- csharp
- excel
- file-conversion
title: Hogyan exportáljunk Excelből – Tabulátorral elválasztott szöveg útmutató
url: /hu/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan exportáljunk excel – Teljes C# útmutató

Gondolkodtál már azon, **hogyan exportáljunk excel** adatokat egy egyszerű szövegfájlba anélkül, hogy elveszítenénk a formázást? Lehet, hogy gyors TSV‑re (tabulátorral elválasztott értékek) van szükséged egy adat‑csővezetékhez, vagy egy örökölt rendszernek adsz át, ami csak a `.txt`‑t olvassa. Akárhogy is, nem vagy egyedül – a fejlesztők gyakran ütköznek ebbe a falba, amikor adatot akarnak kivenni a táblázatokból.

A jó hír? Mindössze három egyszerű lépésben **exportálhatod az excel‑t tab**‑elválasztott szövegként, **konvertálhatod az excel‑t txt‑be**, és még egyedi elválasztót is választhatsz, ha később meggondolod magad. Az alábbiakban egy teljesen futtatható C# példát látsz, megmagyarázva minden sor jelentőségét, valamint néhány tippet a tipikus buktatók elkerüléséhez.

> **Pro tipp:** Ez a megközelítés az Aspose.Cells könyvtárral működik, de a koncepciók bármely .NET Excel API‑ra átültethetők, amely `ExportTable`‑szerű metódust kínál.

## Amire szükséged lesz

- **.NET 6+** (vagy .NET Framework 4.6+). A kód bármely friss runtime‑on lefordul.
- **Aspose.Cells for .NET** (ingyenes próba vagy licenc). Telepítsd NuGet‑en: `dotnet add package Aspose.Cells`.
- Egy `input.xlsx` nevű munkafüzet, amelyet egy általad irányított mappában helyezel el.
- Egy csipetnyi kíváncsiság – mély Excel‑ismeretekre nincs szükség.

Ha már megvannak ezek, ugorjunk egyenesen a megoldásra.

## 1. lépés – Töltsd be a kívánt munkafüzetet

Először létrehozunk egy `Workbook` objektumot, amely a forrásfájlra mutat. Ez az objektum képviseli az egész Excel‑fájlt, beleértve az összes munkalapot, névvel ellátott tartományt és a formázást.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Miért fontos:*  
A munkafüzet betöltése hozzáférést biztosít a munkalap‑gyűjteményhez (`workbook.Worksheets`). Enélkül nem tudsz cellákat, tartományokat vagy exportálási beállításokat kezelni.  

> **Megjegyzés:** Ha a fájl egy hálózati megosztáson van, előzd meg `\\`‑vel vagy használj UNC útvonalat – az Aspose.Cells gond nélkül kezeli.

## 2. lépés – Exportálási beállítások konfigurálása (String értékek & Tab elválasztó)

Most megmondjuk a könyvtárnak, hogyan szeretnénk, hogy az adat ki legyen írva. Az `ExportAsString = true` beállítással minden cellát egyszerű szövegként kezelünk, ami megszünteti az Excel lokálisspecifikus számformátumait. A `Delimiter = "\t"` rész a **exportálás excel‑ből tab**‑ként a lényeg.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Miért fontos:*  
Ha kihagyod az `ExportAsString`‑t, egy `12345` értékű cella egyes lokálokban `12,345`‑ként jelenhet meg, ami megtöri a downstream parser‑eket. Az elválasztó cserélhető vesszőre, csővezeték (`|`) karakterre vagy bármilyen más karakterre, ha később **exportálni szeretnél excel‑t másik elválasztóval**.

## 3. lépés – Egy adott tartomány exportálása szövegfájlba

Végül kiválasztjuk a számunkra fontos tartományt (`A1:D10` ebben a példában), és kiírjuk `out.txt`‑be. Az `ExportTable` metódus elvégzi a nehéz munkát: beolvassa a cellákat, alkalmazza a beállításokat, és a végeredményt lemezre írja.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

A futtatás után a `out.txt` tartalma így fog kinézni:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Minden oszlop **tab**‑bal van elválasztva, így készen áll az `awk`, `PowerShell` vagy bármely CSV‑kompatibilis eszköz számára, amely a tabulátorokat tiszteletben tartja.

### Gyors ellenőrzés

Nyisd meg a generált fájlt egy egyszerű szövegszerkesztőben (Notepad, VS Code) és ellenőrizd:

1. Az oszlopok egymás alá kerülnek, ha bekapcsolod a „Show whitespace” (whitespace megjelenítése) opciót.
2. Nincsenek extra idézőjelek vagy vesszők.
3. Minden numerikus cella pontosan úgy jelenik meg, ahogy az Excel‑ben (köszönhetően az `ExportAsString`‑nek).

Ha valami nem stimmel, ellenőrizd, hogy a forrás munkafüzet nem rejt el sorokat/oszlopokat, és győződj meg róla, hogy a helyes munkalap indexet adtad meg.

## Gyakori variációk és széljegyek

### Egy teljes munkalap exportálása

Ha **exportálni szeretnél excel tartományt**, amely az egész lapot lefedi, használhatod a `sheet.Cells.MaxDisplayRange`‑t:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Másik elválasztó használata

A tabulátorról csővezeték (`|`) karakterre váltás olyan egyszerű, mint egy sor módosítása:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Ez kielégíti a **exportálás excel‑t másik elválasztóval** szituációt anélkül, hogy más kódot át kellene írni.

### Nagy fájlok kezelése (> 100 MB)

Nagy munkafüzetek esetén streameld az exportot, hogy elkerüld a teljes memória betöltését:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Több lap konvertálása egy lépésben

Ha több lapra is **konvertálni szeretnél excel‑t txt‑be**, iterálj rajtuk:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Minden lap saját TSV fájlt kap – praktikus kötegelt feladatokhoz.

## Teljes működő példa (másolás‑beillesztés készen)

Az alábbi program a teljes kód, készen áll a fordításra. Csak cseréld le a fájlútvonalakat a sajátodra.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Várható kimenet:** Egy `out.txt` nevű fájl, ahol minden oszlop tabulátor karakterrel van elválasztva, és minden cella értéke pontosan úgy jelenik meg, ahogy az Excel‑ben.

## Gyakran ismételt kérdések

- **Működik ez .xls fájlokkal?**  
  Igen. Az Aspose.Cells automatikusan felismeri a formátumot, így egy régebbi `.xls` fájlra is rámutathatsz a `Workbook`‑bal, és ugyanaz a kód érvényes.

- **Mi van, ha az adataim tabulátorokat tartalmaznak?**  
  A cellán belüli tabulátorok megmaradnak, ami megtörheti a TSV parser‑eket. Ilyenkor érdemes csővezeték (`|`) elválasztóra váltani az `exportOptions.Delimiter` módosításával.

- **Exportálhatok képleteket értékek helyett?**  
  Állítsd be `exportOptions.ExportAsString = false`‑t, és használd az `ExportTableOptions` overload‑ot, amely tartalmazza az `ExportFormula = true` beállítást. A kimenet a nyers képlet szöveget fogja tartalmazni.

- **Létezik mód a rejtett sorok kihagyására?**  
  Igen. Állítsd be `exportOptions.ExportHiddenRows = false`‑t (alapértelmezett érték `true`). A rejtett sorok nem kerülnek bele a végső szövegfájlba.

## Összegzés

Most már van egy szilárd, termelés‑kész recepted arra, **hogyan exportáljunk excel** adatokat tabulátorral elválasztott szövegfájlba, hogyan **exportáljunk excel‑t tab**‑ként, és hogyan **konvertáljunk excel‑t txt‑be** teljes kontrollal az elválasztók és a tartomány kiválasztása felett. Az Aspose.Cells `ExportTable` metódusának kihasználásával elkerülöd a manuális CSV‑építést, megőrzöd az adatpontosságot, és tisztán tartod a kódbázist.

Készen állsz a következő kihívásra? Próbáld ki:

- Exportálás közvetlenül `MemoryStream`‑be web API‑khoz.  
- Dinamikus fejlécsor hozzáadása az első sor tartalma alapján.  
- Ennek a rutinnak az integrálása egy Azure Function‑be, amely figyeli a tároló bucket‑et új Excel feltöltésekért.

Próbáld ki, módosítsd az elválasztót, és engedd, hogy az adatok bárhová áramoljanak, ahol szükséged van rájuk. Boldog kódolást!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}