---
category: general
date: 2026-02-15
description: Új munkafüzet létrehozása és az Excel TXT formátumba exportálása numerikus
  pontosság beállításával. Tanulja meg a jelentős számjegyek beállítását és a jelentős
  számjegyek korlátozását C#‑ban.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: hu
og_description: Új munkafüzet létrehozása és az Excel TXT-be exportálása, a numerikus
  pontosság jelentős számjegyeinek beállítása. Lépésről lépésre C# útmutató.
og_title: Új munkafüzet létrehozása – Excel exportálása TXT-be pontossággal
tags:
- C#
- Aspose.Cells
- Excel automation
title: Új munkafüzet létrehozása és Excel TXT-be exportálása pontossággal
url: /hu/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új munkafüzet létrehozása – Excel exportálása TXT-be pontos numerikus formázással

Gondolkodtál már azon, hogyan **create new workbook** objektumokat hozhatsz létre C#‑ban, és azonnal egy egyszerű szövegfájlba mentheted őket? Nem vagy egyedül. Sok adatcsővezeték‑szituációban **export Excel to TXT**‑t kell végrehajtanunk, miközben a számok olvashatóak maradnak, ami azt jelenti, hogy korlátozni kell a tizedespont után megjelenő számjegyek számát.  

Ebben az útmutatóban végigvezetünk a teljes folyamaton: egy új munkafüzet létrehozásától, a export beállításáig, hogy **sets significant digits** (azaz a jelentős számjegyek korlátozása), és végül a fájl lemezre írásáig. A végére egy azonnal futtatható kódrészletet kapsz, amely megfelel a **numeric precision** követelményeidnek – extra könyvtárak nélkül, varázslat nélkül.

> **Pro tip:** Ha már használod az Aspose.Cells‑t, az alább bemutatott osztályok ennek a könyvtárnak a részei. Ha más platformon vagy, a koncepciók továbbra is alkalmazhatók; csak cseréld ki az API hívásokat.

---

## Amire szükséged lesz

- .NET 6+ (a kód .NET Core‑on és .NET Framework‑ön egyaránt lefordítható)  
- Aspose.Cells for .NET (ingyenes próba vagy licencelt verzió) – telepítés NuGet‑en keresztül: `dotnet add package Aspose.Cells`  
- Bármelyik kedvenc IDE (Visual Studio, Rider, VS Code)  

Ennyi. Nincs extra konfigurációs fájl, nincs rejtett lépés.

---

## 1. lépés: Új munkafüzet létrehozása

Az első dolog, hogy **create new workbook**. Tekintsd a `Workbook` osztályt egy üres Excel‑fájlként, amely lapokra, cellákra és adatokra vár.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Miért fontos:** Egy tiszta munkafüzettel kezdve elkerülöd a rejtett formázásokat, amelyek később befolyásolhatják a pontossági beállításokat.

---

## 2. lépés: Szöveg mentési beállítások konfigurálása – Jelentős számjegyek beállítása

Most megmondjuk az Aspose.Cells‑nek, hogy hány **significant digits** számjegyet szeretnénk, amikor egy `.txt` fájlba írunk. A `TxtSaveOptions` osztály egy `SignificantDigits` tulajdonságot biztosít, amely pontosan ezt teszi.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Magyarázat:** `SignificantDigits = 5` azt jelenti, hogy az exportáló megtartja bármely szám legfontosabb öt számjegyét, függetlenül attól, hol van a tizedespont. Ez egy kényelmes módja a **set numeric precision** beállításának anélkül, hogy minden cellát kézzel formáznál.

---

## 3. lépés: Munkafüzet mentése egyszerű szövegfájlként

Miután a munkafüzet és a beállítások készen állnak, végül **export Excel to txt**. A `Save` metódus megkapja a fájl útvonalát és a most konfigurált opciós objektumot.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

A program futtatása egy ilyen kinézetű fájlt hoz létre:

```
12346
0.00012346
3.1416
```

Vedd észre, hogy minden szám betartja a korábban beállított **limit significant digits** szabályt.

---

## 4. lépés: Az eredmény ellenőrzése (opcionális, de ajánlott)

Könnyű megnyitni a generált `numbers.txt` fájlt bármely szerkesztőben, de érdemes lehet automatizálni az ellenőrzési lépést, különösen CI csővezetékekben.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Ha a konzol a fenti három sort jeleníti meg, sikeresen **set significant digits**‑t állítottál be, és az export a kívánt módon működik.

---

## Gyakori buktatók és hogyan kerüld el őket

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| A számok túl sok tizedesjegyet mutatnak | `SignificantDigits` alapértelmezett (0) értéken maradt | Állítsd be kifejezetten a `SignificantDigits` értékét a kívánt számra |
| Üres fájl jön létre | A munkafüzet mentés előtt nem kapott adatot | Töltsd fel a cellákat **előtt**, mielőtt meghívod a `Save`‑t |
| A fájl útvonal `UnauthorizedAccessException`‑t dob | Védett mappába próbálsz írni | Használj olyan mappát, amelyhez írási jogosultságod van (pl. `C:\Temp` vagy `%USERPROFILE%\Documents`) |
| A pontosság hibásnak tűnik nagyon kis számoknál | A jelentős számjegyek száma tartalmazza a tizedespont után álló vezető nullákat | Ne feledd, hogy a “significant” figyelmen kívül hagyja a vezető nullákat; a 0.000123456 5 számjeggyel `0.00012346` lesz |

---

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes, önálló program látható. Illeszd be egy új konzolprojektbe, és nyomd meg a **Run** gombot.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Várható konzolkimenet**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

A `numbers.txt` fájl a fenti három sort fogja tartalmazni.

---

## Következő lépések: Alapokon túl

- **Export other formats** – Az Aspose.Cells támogatja a CSV, HTML és PDF formátumokat is. Szükség szerint cseréld a `TxtSaveOptions`‑t `CsvSaveOptions`‑ra vagy `PdfSaveOptions`‑ra.  
- **Dynamic precision** – A `SignificantDigits` értékét futásidőben számíthatod ki felhasználói bemenet vagy konfigurációs fájlok alapján.  
- **Multiple worksheets** – Iterálj a `workbook.Worksheets`‑en, és exportáld mindegyiket egy saját `.txt` fájlba.  
- **Localization** – A tizedespont (`.` vs `,`) vezérlését a `CultureInfo`‑val szabályozhatod, ha a regionális beállításoknak kell megfelelnie.  

Mindezek a kiegészítések is az általunk bemutatott alapötletre épülnek: **create new workbook**, az export konfigurálása, és a **set numeric precision** a jelentési követelményekhez igazítása.

---

## Összefoglalás

Elkészítettünk egy friss **create new workbook** példányt, feltöltöttük adatokal, és bemutattuk, hogyan **export Excel to TXT**, miközben **setting significant digits**‑et használunk a kimeneti pontosság korlátozásához. A teljes példa azonnal futtatható, és a magyarázat lefedi az egyes sorok *miért* részét, hogy saját projektjeidhez is könnyen alkalmazhasd.

Nyugodtan kísérletezz—változtasd meg a `SignificantDigits` értékét, adj hozzá több lapot, vagy cseréld ki a kimeneti formátumot. Ha elakadsz, nézd meg az Aspose.Cells dokumentációt vagy hagyj megjegyzést alább. Boldog kódolást!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}