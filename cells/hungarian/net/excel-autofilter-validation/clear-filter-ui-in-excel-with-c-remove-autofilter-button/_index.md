---
category: general
date: 2026-02-09
description: Törölje a szűrő felületet Excelben C#-val az AutoFilter gomb eltávolításával.
  Tanulja meg, hogyan rejtheti el a szűrő gombot, jelenítheti meg a fejlécsort, és
  tarthatja rendezettnek a munkalapjait.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: hu
og_description: Tiszta szűrő felület Excelben C#-val. Ez az útmutató megmutatja, hogyan
  rejtsd el a szűrő gombot, jelenítsd meg a fejlécsort, és tartsd tisztán a munkalapokat.
og_title: Szűrő felület törlése Excelben C#‑al – AutoFilter gomb eltávolítása
tags:
- excel
- csharp
- epplus
- automation
title: Szűrő felület törlése Excelben C#-val – AutoFilter gomb eltávolítása
url: /hu/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szűrő felület törlése Excelben C#‑vel – AutoFilter gomb eltávolítása

Volt már szükséged arra, hogy **clear filter UI**‑t törölj egy Excel munkalapon, de nem tudtad, melyik kódsor rejti el azt a kis legördülő nyilat? Nem vagy egyedül. A szűrő gomb szemcsípő lehet, amikor egy jelentést küldesz a végfelhasználóknak, akiknek soha nem kell módosítaniuk a nézetet.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **remove the AutoFilter button**‑t távolítjuk el egy táblázatból, hogyan biztosítjuk, hogy a fejléc sor látható maradjon, és még arra is kitérünk, hogyan *hide filter button* véglegesen. A végére pontosan tudni fogod, **how to remove AutoFilter** C#‑ben, és miért fontos minden egyes lépés.

## Amire szükséged lesz

- .NET 6+ (vagy .NET Framework 4.7.2+) – bármely friss futtatókörnyezet működik.
- A **EPPlus** NuGet csomag (6.x vagy újabb verzió) – biztosítja a `ExcelWorksheet`, `ExcelTable`, stb. osztályokat.
- Egy egyszerű Excel fájl **SalesTable** nevű táblával (nyugodtan létrehozhatsz egyet néhány kattintással).

Ennyi. Nincs COM interop, nincs extra DLL, csak néhány `using` utasítás és néhány kódsor.

## Szűrő felület törlése: az AutoFilter gomb eltávolítása

A megoldás lényege három apró utasításban rejlik. bontsuk le őket, hogy megértsd, *miért* szükségesek, ne csak *mit* csinálnak.

### 1. lépés – Hivatkozás lekérése a táblára

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Miért fontos: Az EPPlus **tables** (`ExcelTable`)‑kel dolgozik, nem nyers tartományokkal. A táblázat objektum lekérésével hozzáférünk az `AutoFilter` tulajdonsághoz, amely a munkalapon látható UI elemet vezérli. Ha közvetlenül a munkalapot próbálod módosítani, csak az értékeket érinted, nem a szűrő gombot.

### 2. lépés – Az AutoFilter gomb sor eltávolítása

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Az `AutoFilter` null‑ra állítása azt mondja az EPPlus‑nak, hogy törölje a háttérben lévő szűrő sort. Ez a *clear filter UI* művelet, amelyet a legtöbb fejlesztő keres, amikor azt kérdezi: “**how to remove autofilter**”. Egy tiszta, egy soros megoldás, amely bármely, az EPPlus‑ által támogatott Excel verzión működik.

### 3. lépés – A fejléc sor látható maradjon

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Amikor eltávolítod a szűrő UI‑t, az Excel néha elrejtheti a fejléc sort, ha a tábla `ShowHeader` jelzője hamis. Az explicit `true` beállítással garantáljuk, hogy az oszlopcímek a képernyőn maradjanak – egy finom, de fontos részlet egy kifinomult végjelentéshez.

### Teljes, futtatható példa

Az alábbi egy minimális konzolalkalmazás, amely megnyit egy meglévő munkafüzetet, végrehajtja a három lépést, és elmenti az eredményt. Másold be, nyomd meg a **F5**‑öt, és figyeld, ahogy a szűrő gomb eltűnik.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Várt eredmény:** Nyisd meg a *SalesReport_NoFilter.xlsx* fájlt – a szűrő nyilak eltűntek, de az oszlopfejlécek megmaradnak. Nincs több “kattints‑a‑szűréshez” UI‑zavar.

> **Pro tipp:** Ha **több táblád** van, és mindegyiknél el szeretnéd rejteni a szűrő gombot, iterálj a `worksheet.Tables`-en, és alkalmazd ugyanazt a három sort a ciklusban.

## Hogy távolítsuk el az AutoFilter-t Excelben C#‑vel – mélyebb betekintés

Gondolhatod, “Mi van, ha a munkafüzet már tartalmaz szűrőt? A `AutoFilter = null` beállítás is törli a szűrt sorokat?” A válasz **igen**. Az EPPlus mind a UI‑t, mind a háttérben lévő szűrőfeltételeket törli, a adatokat az eredeti sorrendben hagyva.

Ha csak a gombot szeretnéd *elrejteni*, de a szűrőt aktívan tartani, beállíthatod az `AutoFilter` tulajdonságot egy **új üres szűrő**-re:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Ez a változat hasznos, ha *hide filter button*‑t szeretnél egy letisztult megjelenésért, de mégis engedélyezni akarod a haladó felhasználóknak a szűrők váltását VBA‑val vagy a szalagon.

### Szélsőséges eset: Táblák fejléc sor nélkül

Néhány régi jelentés egyszerű tartományokat használ táblák helyett. Ebben az esetben az EPPlus nem ad `ExcelTable` objektumot, így a fenti kód hibát dob. A megoldás, hogy először **a tartományt táblává konvertálod**:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Most már *removed autofilter excel* stílusú UI‑t is eltávolítottál egy olyan tartományról, amely eleinte formális tábla nélkül indult.

## Fejléc sor megjelenítése a szűrő gomb elrejtése után – miért fontos

Gyakori panasz, hogy a szűrő UI elrejtése után a fejléc sor néha eltűnik, különösen, ha a munkafüzet eredetileg “Hide Header” beállítással készült. Az `salesTable.ShowHeader = true;` explicit beállításával elkerüljük ezt a meglepetést.

Ha valaha **hide filter button**-t kell alkalmaznod, de a fejlécet rejtve szeretnéd tartani (például nyers adat dumpot generálsz), egyszerűen állítsd `salesTable.ShowHeader = false;`-ra a szűrő törlése után. A kód szimmetrikus, így könnyen átkapcsolható egy konfigurációs zászló alapján.

## Hide filter button – gyakorlati tippek és buktatók

- **Verzió kompatibilitás:** Az EPPlus 6+ csak `.xlsx` fájlokkal működik. Ha a régebbi `.xls` formátummal dolgozol, másik könyvtárra lesz szükséged (pl. NPOI), mivel a *clear filter UI* API nem érhető el.
- **Teljesítmény:** Egy hatalmas munkafüzet betöltése csak egy gomb elrejtéséhez lassú lehet. Fontold meg a `ExcelPackage.Load(stream, true)` használatát **read‑only** módban történő megnyitáshoz, a módosítás alkalmazásához, majd mentéshez.
- **Tesztelés:** Mindig manuálisan ellenőrizd az első alkalommal a kimeneti fájlt. Automatizált UI tesztek ellenőrizhetik, hogy a szűrő nyilak valóban eltűntek (`worksheet.Tables[0].AutoFilter == null`).
- **Licencelés:** Az EPPlus az 5‑ös verziótól kettős licencet használ. Kereskedelmi projektekhez fizetett licencre vagy alternatív könyvtárra lesz szükség.

## Teljes forrásfájl másoláshoz

Az alábbi a pontos fájl, amelyet beilleszthetsz egy új konzolprojektbe. Nincsenek rejtett függőségek, minden önálló.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Futtasd a `dotnet add package EPPlus --version 6.0.8` (vagy a legújabbat) parancsot a buildelés előtt, és egy tiszta munkalappal leszel felkészülve a terjesztésre.

## Összegzés

Most megmutattuk, hogyan **remove AutoFilter** és **clear filter UI** egy Excel munkafüzetben C#‑vel. A három soros mag (`AutoFilter = null;`, `ShowHeader = true;`) végzi a nehéz munkát, míg a környező boilerplate a megoldást

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}