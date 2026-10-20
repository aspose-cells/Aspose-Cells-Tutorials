---
category: general
date: 2026-03-30
description: Tanulja meg, hogyan formázzon számot elválasztóval az Aspose.Cells használatával
  C#-ban. Tartalmazza az egyéni számformátum beállítását, az ezres elválasztó hozzáadását,
  a tizedesjegyek formázását és a cella formázását.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: hu
og_description: Szám formázása elválasztóval C#-ban. Ez az útmutató bemutatja, hogyan
  állítható be egyéni számformátum, hogyan adható hozzá ezres elválasztó, hogyan formázhatók
  a tizedesjegyek, és hogyan formázható cella az Aspose.Cells használatával.
og_title: Szám formázása elválasztóval C#-ban – Aspose.Cells útmutató
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Szám formázása elválasztóval C#-ban – Teljes Aspose.Cells útmutató
url: /hu/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szám formázása elválasztóval C#-ban – Teljes Aspose.Cells útmutató

Valaha szükséged volt **szám formázására elválasztóval** egy táblázatban, de nem tudtad, melyik API hívást kell használni? Nem vagy egyedül – a fejlesztők folyamatosan küzdenek az ezres elválasztókkal, tizedesjegyekkel és egyedi mintákkal az adatok exportálásakor.  

Jó hír: az Aspose.Cells-szel ez gyerekjáték. Ebben az útmutatóban egy valós példán keresztül mutatjuk be, hogyan **állítható be egy egyedi számformátum**, **adható hozzá ezres elválasztó**, **formázhatók a tizedesjegyek**, és hogyan **formázható a cella** kimenete karakterláncként. A végére egy kész, futtatható kódrészletet kapsz, amelyet bármely .NET projektbe beilleszthetsz.

## Mit fed le ez az útmutató

* A szükséges NuGet csomag pontos neve és a telepítési módja.  
* Lépésről‑lépésre kód, amely létrehoz egy munkafüzetet, beír egy numerikus értéket, és alkalmaz egy egyedi formátumot.  
* Miért a `ExportTableOptions.ExportAsString` a preferált mód a formázott érték lekérésére.  
* Gyakori buktatók – például az `ExportAsString` engedélyezésének elhagyása vagy a helytelen formátummaszk használata.  
* Hogyan módosítható a formátummaszk, ha más számú tizedesjegyre vagy más elválasztó stílusra van szükség.

Hozzáférés külső dokumentációs linkekhez nem szükséges; minden, amire szükséged van, itt van. Merüljünk el.

---

## Előfeltételek

| Követelmény | Indoklás |
|-------------|----------|
| .NET 6.0 vagy újabb | Az Aspose.Cells 23.10+ a .NET Standard 2.0+ célja, így a .NET 6 biztonságos és aktuális. |
| Visual Studio 2022 (vagy bármely C# IDE) | Megkönnyíti a hibakeresést és a csomagkezelést. |
| Aspose.Cells for .NET NuGet csomag | Biztosítja a `Workbook`, `Worksheet` és `ExportTableOptions` osztályokat, amelyeket használni fogunk. |

A csomagot a Package Manager Console segítségével telepítheted:

```powershell
Install-Package Aspose.Cells
```

Ennyi—nincs extra DLL, nincs COM interop, csak egyetlen NuGet hivatkozás.

## 1. lépés: Új munkafüzet inicializálása (Hogyan formázzuk a cellát)

Az első dolog, amit teszünk, egy új `Workbook` példány létrehozása. Tekintsd úgy, mint egy üres Excel fájlt, amely készen áll az adatok fogadására.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Miért fontos:** A `Workbook` az Aspose.Cells minden műveletének belépési pontja. Az első munkalap (`Worksheets[0]`) lekérésével tiszta vászonhoz jutunk anélkül, hogy nevet kellene adni a lapnak.

## 2. lépés: Numerikus érték írása a célcellába

Ezután egy nyers számot helyezünk a **A1** cellába. Az érték még nincs formázva – csak egy double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro tipp:** Használd a `PutValue`-t a `PutString` helyett, ha később numerikus formázást szeretnél alkalmazni. Ez megőrzi az alap adat típust, lehetővé téve az Excel‑kompatibilis számításokat.

## 3. lépés: Egyedi számformátum beállítása (Ezres elválasztó hozzáadása és tizedesjegyek formázása)

Most jön a tutorial szíve: egy formátummaszk definiálása, amely megmondja az Aspose.Cells-nek, hogyan jelenítse meg a számot. A `#,##0.00` maszk három dolgot csinál:

1. **`#,##0`** – ezres elválasztót ad hozzá (alapértelmezettként vessző).  
2. **`.00`** – pontosan két tizedesjegyet kényszerít.  

Ha más számú tizedesjegyre van szükséged, egyszerűen változtasd meg a `0`-k számát a tizedespont után.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Miért használjuk az `ExportAsString`-et**: Alapértelmezés szerint az `ExportString` a nyers értéket adja vissza. Az `ExportAsString = true` beállítás arra kényszeríti az API-t, hogy a `NumberFormat` maszkot alkalmazza a szöveggé konvertálás előtt. Ez elengedhetetlen, ha pontos karakterlánc ábrázolásra van szükség jelentésekhez, JSON payloadokhoz vagy UI megjelenítéshez.

## 4. lépés: Formázott szöveg exportálása (Hogyan formázzuk a cellát)

Az opciók készen állnak, ezért meghívjuk a `ExportString`-et ugyanazon a cellán. A metódus figyelembe veszi a most definiált maszkot, és egy szépen formázott karakterláncot ad vissza.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

A program futtatása **`12,345.68`** értéket ír ki a konzolra – pontosan a kért formátumban.

> **Szélsőséges eset:** Ha a forrás számnak több mint két tizedesjegye van, a maszk kerekíti. Ha a kerekítés helyett csonkolásra van szükség, a `PutValue` hívása előtt a `Math.Truncate`‑tel kell előfeldolgozni az értéket.

## 5. lépés: A formátum finomhangolása – Gyakori változatok

### 5.1 Tizedes pontosság módosítása

Három tizedesjegyre van szükséged? Csak cseréld le a maszkot:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Más ezres elválasztó használata

Néhány helyi beállítás a szóközt vagy a pontot részesíti előnyben. A karaktert közvetlenül beágyazhatod:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Vagy a munkafüzet kultúra beállításaira támaszkodhatsz:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Előtag vagy utótag (Pénznem, Százalék)

Adj hozzá dollárjelet vagy százalékjelet közvetlenül a maszkba:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Megjegyzés:** A maszk kis- és nagybetű érzékeny. A `$` és `%` literális szimbólumok; nem befolyásolják az alap numerikus értéket.

## 6. lépés: Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes program látható, amelyet beilleszthetsz egy új konzolos alkalmazásba. Tartalmazza az összes lépést, megjegyzést és a végső kimenet ellenőrzését.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Futtasd a programot (`dotnet run` a terminálból vagy nyomd meg az F5-öt a Visual Studio-ban), és láthatod, hogy a formázott szám pontosan úgy jelenik meg, ahogy látható.

## Gyakran Ismételt Kérdések (GYIK)

**K: Működik ez a régebbi Excel verziókkal?**  
V: Igen. A formátummaszk az Excel natív számformátum szintaxisát követi, így bármely verzió, amely érti a `#,##0.00`-t, ugyanazt a karakterláncot jeleníti meg.

**K: Mi a teendő, ha egy cellatartományt kell formázni?**  
V: Iterálj a kívánt tartományon, és alkalmazd ugyanazt az `ExportTableOptions`-t minden cellára, vagy állítsd be a `Style.Custom` tulajdonságot a tartományra, majd hívd meg az `ExportString`-et egyetlen cellán.

**K: Exportálhatok közvetlenül CSV-be ezekkel a formátumokkal?**  
V: Természetesen. Használd a `Workbook.Save("output.csv", SaveFormat.CSV);`-t a formátum minden cellára való beállítása után. Az Aspose.Cells figyelembe veszi a cella `Style`-ját CSV generálásakor.

## Következtetés

Most bemutattuk, hogyan **formázható szám elválasztóval** C#-ban az Aspose.Cells segítségével, lefedve mindent a **egyedi számformátum beállításától** a **ezres elválasztó hozzáadásáig**, a **tizedesjegyek formázásáig**, és az alapvető **hogyan formázzuk a cellát** karakterlánc exporthoz. A kód teljesen önálló, .NET 6+ környezetben működik, és bármely helyi beállításhoz vagy pontossági igényhez testre szabható.

Következő lépésként érdemes lehet felfedezni:

* Ugyanazon technika alkalmazása dátumokra és időkre (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Tömeges exportok automatizálása, ahol minden oszlopnak más maszkra van szüksége.  
* A formázott karakterláncok integrálása PDF jelentésekbe az Aspose.Words segítségével.

Próbáld ki őket, és hamarosan te leszel a csapatod első számú szakértője a táblázat formázásában. Boldog kódolást!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formázott szám elválasztóval megjelenítve az Aspose.Cells kimenetében"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}