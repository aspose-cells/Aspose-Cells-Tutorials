---
category: general
date: 2026-03-18
description: Új munkafüzet létrehozása és az Excel TXT formátumba exportálása a numerikus
  pontosság megőrzése mellett. Tanulja meg, hogyan mentse a munkalapot TXT‑ként, és
  hogyan konvertálja a munkalapot hatékonyan TXT formátumba.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: hu
og_description: Új munkafüzet létrehozása és az Excel pontos TXT exportálása. Ez az
  útmutató bemutatja, hogyan lehet a munkalapot TXT formátumban menteni, és a munkalapot
  C# használatával TXT-re konvertálni.
og_title: Új munkafüzet létrehozása – Excel TXT exportálási útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Új munkafüzet létrehozása – Excel exportálása TXT-be teljes pontossággal
url: /hu/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új munkafüzet létrehozása – Excel exportálása TXT-be teljes pontossággal

Volt már szükséged **create new workbook** C#‑ban, csak hogy néhány adatot egy egyszerű szövegfájlba írj? Lehet, hogy egy régi rendszerből húzol ki egy jelentést, és a downstream eszköz csak egy `.txt` adatfolyamot fogad el. A jó hír? Nem kell feláldoznod a numerikus pontosságot, és egyáltalán nem kell kézzel összeállítanod CSV karakterláncokat.

Ebben az útmutatóban végigvezetünk a **export excel to txt** teljes folyamatán, az munkafüzet inicializálásától a záró nullák megőrzéséig, amikor **save worksheet as txt**. A végére egy azonnal futtatható kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz – extra segédprogramok nélkül.

## Amire szükséged lesz

- **ASP.NET/ .NET 6+** (a kód .NET Framework 4.6+‑on is működik)  
- **Aspose.Cells for .NET** – a könyvtár, amely a `Workbook`, `Worksheet` és `TxtSaveOptions` osztályokat biztosítja. Letöltheted a NuGet‑ből a `Install-Package Aspose.Cells` paranccsal.  
- Alapvető C# ismeretek (ha kényelmesen használod a `using` utasításokat, már készen is vagy).  

Ennyi—nincs Excel interop, nincs COM objektum, és egyáltalán nincs kézi karakterlánc-összefűzés.

## 1. lépés: Új munkafüzet inicializálása (Primary Keyword)

Az első dolog, amit meg kell tenned, **create new workbook**. Tekintsd a munkafüzetet egy üres vászonnak, ahová később számokat, szöveget vagy képleteket illeszthetsz.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Miért fontos:** A `Workbook` példányosítása fájl betöltése nélkül egy tiszta lapot ad. Ezután programozottan adhatsz hozzá adatokat, ami tökéletes a **convert worksheet to txt** esetekben, amikor nincs meglévő `.xlsx` fájl.

## 2. lépés: Cellák feltöltése – A záró nullák megtartása

Gyakori buktató a számok szövegbe írásakor a záró nullák elvesztése (`123.45000` helyett `123.45`). Ha a downstream rendszerek rögzített szélességű mezőkre támaszkodnak, ez a veszteség mindent tönkretehet.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tipp:** `PutValue` automatikusan meghatározza az adat típust. Ha olyan karakterláncot akarsz, ami számként néz ki, használd a `PutValue("123.45000")`-t.

## 3. lépés: TXT mentési beállítások konfigurálása – Numerikus pontosság megőrzése

Itt történik a varázslat. A `PreserveNumericPrecision` beállításával azt mondod az Aspose.Cells‑nek, hogy pontosan azt az értéket írja ki, amit megadtál, beleértve a jelentéktelen záró nullákat is.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Miért engedélyezd?** Amikor **save excel as txt**, az alapértelmezett viselkedés levágja a felesleges tizedesjegyeket. A `PreserveNumericPrecision = true` beállítása garantálja, hogy a kimenet tükrözi a cella megjelenített értékét, ami kritikus a pénzügyi jelentések vagy tudományos adatok esetén.

## 4. lépés: Munkalap mentése TXT‑ként – A végső export

Most már ténylegesen **save worksheet as txt**. A útvonalat bárhová beállíthatod, ahol írási jogosultságod van; a példában egy `output` nevű relatív mappát használunk.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Várható kimenet** (`num-preserve.txt`):

```
123.45000
```

Vedd észre, hogy a záró nullák megmaradtak – pontosan úgy, ahogy szeretted.

## 5. lépés: Az eredmény ellenőrzése – Gyors ellenőrzés

A program futása után nyisd meg a `num-preserve.txt` fájlt bármely szövegszerkesztőben. Egyetlen sort kell látnod: `123.45000`. Ha `123.45`-öt látsz helyette, ellenőrizd, hogy a `PreserveNumericPrecision` `true`‑ra van állítva, és hogy a legújabb Aspose.Cells verziót (v23.10+) használod.

## Gyakori változatok és szélhelyzetek

### Több cella vagy tartomány exportálása

Ha egy teljes tartományt szeretnél **export excel to txt**, egyszerűen tölts fel több cellát a mentés előtt:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Az Aspose alapértelmezés szerint minden cellát új sorba ír. A határolót (tab, vessző) a `txtSaveOptions.Separator` segítségével is módosíthatod.

### Munkalap konvertálása TXT‑be különböző kódolásokkal

Néha a downstream rendszerek UTF‑8 BOM vagy ASCII kódolást igényelnek. Ilyen módon állíthatod be a kódolást:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Nagy munkafüzetek kezelése

Amikor hatalmas munkalapokkal (több százezer sor) dolgozol, fontold meg a kimenet streamelését:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## Pro tippek és buktatók

- **Ne felejtsd el létrehozni a kimeneti könyvtárat** a `Save` hívása előtt, különben `DirectoryNotFoundException` hibát kapsz.  
- **Figyelj a helyi beállítások szerinti tizedes elválasztókra**. Ha a környezeted vesszőt használ (`1,23`), állítsd be a `txtSaveOptions.DecimalSeparator = '.'`-t a pont kényszerítéséhez.  
- **Verziókompatibilitás**: A `PreserveNumericPrecision` jelző az Aspose.Cells 20.6‑ban került bevezetésre. Ha régebbi verziót használsz, ez a jelző nem létezik, és a mentés előtt a cellát szövegként kell formázni.

![Új munkafüzet létrehozása és Excel exportálása TXT-be a numerikus pontosság megőrzésével](excel-to-txt.png "Új munkafüzet")

*Kép alternatív szöveg: "Új munkafüzet létrehozása és Excel exportálása TXT-be a numerikus pontosság megőrzésével"*

## Összefoglaló – Amit lefedtünk

- **Create new workbook** használata Aspose.Cells‑szel.  
- Egy cella feltöltése olyan számmal, amely tartalmaz záró nullákat.  
- A `TxtSaveOptions.PreserveNumericPrecision = true` beállítása a **save excel as txt** során a pontosság megőrzéséhez.  
- A fájl írása a lemezre, ellenőrizve, hogy a kimenet megegyezik az eredeti értékkel.

Ez a teljes **convert worksheet to txt** munkafolyamat kevesebb, mint 50 sor C#‑ban.

## Következő lépések és kapcsolódó témák

Most, hogy már **export excel to txt** tudsz tökéletes pontossággal, érdemes lehet a következőket felfedezni:

- **Exportálás CSV‑be** egyedi határolókkal (`TxtSaveOptions.Separator`).  
- **Mentés más egyszerű szöveges formátumokba**, például TSV‑be (`SaveFormat.TabDelimited`).  
- **Kötegelt feldolgozás** több munkafüzetre egy mappában a `Directory.GetFiles` használatával.  
- **Integráció Azure Functions‑szel** a felhőben igény szerinti konverzióhoz.

Ezek mind ugyanarra a `Workbook` → `Worksheet` → `TxtSaveOptions` mintára épülnek, így otthonosan fogod használni őket.

### Záró gondolat

Ha követted az útmutatót, most pontosan tudod, hogyan **create new workbook**, töltsd fel, és **save worksheet as txt**, miközben megőrzöd minden tizedesjegyet, ami fontos számodra. Ez egy kis kódrészlet, de megold egy meglepően gyakori fejfájást, amikor a régi csővezetékek egyszerű szöveges bemenetet igényelnek.

Próbáld ki, finomítsd a beállításokat, és engedd, hogy az adatok pontosan úgy áramoljanak, ahogy szükséged van. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}