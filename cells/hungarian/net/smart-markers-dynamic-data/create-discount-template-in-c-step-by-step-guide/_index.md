---
category: general
date: 2026-02-14
description: Gyorsan hozzon létre kedvezmény sablont, és tanulja meg, hogyan alkalmazzon
  kedvezményt a táblázatban, injektálja az adatokat a sablonba, és definiáljon változó
  előtagot az okos jelölőkhöz.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: hu
og_description: Készíts kedvezmény sablont C#-ban. Tanulja meg, hogyan alkalmazzon
  kedvezményt a táblázatban, hogyan injektáljon adatot a sablonba, és hogyan definiáljon
  változó előtagot az okos jelölők számára.
og_title: Kedvezmény sablon létrehozása – Teljes C# útmutató
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Kedvezmény sablon létrehozása C#-ban – Lépésről lépésre útmutató
url: /hu/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kedvezmény Sablon Létrehozása – Teljes C# Bemutató

Valaha szükséged volt **create discount template** létrehozására egy értékesítési jelentéshez, de nem tudtad, hogyan tápláld be az adatokat automatikusan egy táblázatba? Nem vagy egyedül. Ebben az útmutatóban pontosan megmutatjuk, hogyan **create discount template**, majd hogyan **apply discount in spreadsheet** cellákban, **inject data into template**, és még **define variable prefix** a smart markerjeidhez – mindezt tiszta C# kóddal.

Először felvázoljuk a problémát, majd egy működő megoldásba ugrunk, amit egyszerűen másol‑beilleszthetsz. A végére egy újrahasználható mintát kapsz, amely működik akár számlák, árlisták vagy bármely dinamikus kedvezményeket igénylő táblázat generálásához.

---

## Mit Tanulhatsz Meg

- Hogyan tervezz egy kedvezmény‑érzékeny táblázat sablont.
- Hogyan konfigurálj egy egyedi `VariablePrefix` / `VariableSuffix`-t, hogy a marker-ek könnyen észrevehetők legyenek.
- Hogyan adj át egy névtelen objektumot (`discountData`) a `SmartMarkerProcessor`-nek.
- Hogyan számolja automatikusan a végső árat a keletkező képlet (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`).
- Tippek a szélsőséges esetek kezelésére, mint a nulla‑kedvezmény sorok vagy több kedvezmény szint.

**Prerequisites** – egy aktuális .NET futtatókörnyezet (≥ .NET 6), egy hivatkozás a `Aspose.Cells` (vagy hasonló) könyvtárra, amely biztosítja a `SmartMarkerProcessor`-t, valamint az C# szintaxis alapvető ismerete. Semmi egzotikus.

## 1. lépés: Kedvezmény Sablon Létrehozása a Táblázatban

Először nyiss meg egy új munkafüzetet (vagy használj egy meglévőt), és helyezz el egy helyőrzőt, ahol a kedvezményt alkalmazni fogod. Tekintsd a sablont egy egyszerű Excel fájlként, amely “smart marker”-eket tartalmaz, amelyeket a processzor helyettesít.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** A `#Discount#` beágyazásával a képletbe megmondjuk a processzornak, pontosan hová tartozik a kedvezmény értéke. A `SmartMarkerProcessor` a `#Discount#`-t a később megadott számmal fogja helyettesíteni, a képlet többi részét érintetlenül hagyva.

## 2. lépés: Változó Előtag Definiálása a Smart Marker-ekhez

Alapértelmezés szerint sok könyvtár a `${Variable}` vagy `{{Variable}}` szintaxist keresi. A mi esetünkben egy tiszta, emberi‑olvasásra alkalmas markert szeretnénk, ezért **define variable prefix** és suffix explicit módon.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** A `#` használata rövid és könnyen észrevehető markereket eredményez az Excel képletsorában. Ha el akarod kerülni az ütközést meglévő Excel függvényekkel, válassz másik párost (pl. `[[` és `]]`).

## 3. lépés: Adatok Befecskendezése a Sablonba a SmartMarkerProcessor-rel

Most betápláljuk a tényleges kedvezmény értékét. A processzor átvizsgálja a munkalapot, megtalálja az összes `#Discount#`-t, és a átadott névtelen objektumból származó értékkel helyettesíti.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Ez a hívás után a `B2` cellában lévő képlet a következő lesz:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Amikor a munkafüzet számol, a `B2` **90**-at mutat, vagyis a 100-as eredeti árra 10 % kedvezmény lett alkalmazva.

**Why it works:** A `StartSmartMarkerProcessing` minden cellán végigjár, keresve a `#Discount#` token-t, és helyettesíti a numerikus értékkel. Mivel a token egy `IF` utasításon belül van, a táblázat továbbra is kezeli azokat az eseteket, amikor a kedvezmény nulla lehet.

## 4. lépés: Kedvezmény Alkalmazása a Táblázatban – Az Eredmény Ellenőrzése

Indítsuk el a számítást, és írjuk ki a végső árat a konzolra. Ez a lépés bizonyítja, hogy a **apply discount in spreadsheet** munkafolyamat sikeres volt.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Várható kimenet**

```
Original: 100
Discounted (10%): 90
```

Ha a `discountData.Discount` értékét `0.25`-re változtatod, és újra futtatod a processzort, a kimenet automatikusan egy 25 % kedvezményt fog mutatni – extra kód nélkül.

## 5. lépés: Szélsőséges Esetek és Több Kedvezmény Kezelése

### Nulla‑Kedvezmény Sorok

Néha egy termék nincs akcióban. A képlet robusztusságának megőrzése érdekében a korábban elhelyezett `IF` már lefedi ezt a helyzetet: ha a `#Discount#` `0`, az eredeti ár változatlanul marad.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Több Kedvezmény Oszlop

Ha soronként külön kedvezményre van szükséged, adj minden sorhoz saját markert, pl. `#Discount1#`, `#Discount2#`, és adj át egy gyűjteményt:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

A processzor sorban egyezteti a markereket, így minden sor a megfelelő értéket kapja.

## Teljes Működő Példa

Az alábbiakban a teljes, másolásra kész program látható, amely tartalmazza a fenti lépéseket. Mentsd el `Program.cs` néven, adj hozzá hivatkozást a `Aspose.Cells`-re, és futtasd.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

A futtatás kiírja a várt számokat, és létrehoz egy `DiscountedPricing.xlsx` fájlt, amelyet megnyithatsz Excelben, hogy láthasd a már feloldott képletet.

## Következtetés

Most már tudod, hogyan **create discount template**, **apply discount in spreadsheet**, **inject data into template**, és **define variable prefix** a smart marker-ekhez – mindezt néhány tömör C# sorral. A minta skálázható – csak cseréld ki a névtelen objektumot vagy adj át egy gyűjteményt a tömeges frissítésekhez, és ugyanaz a sablon bármilyen kedvezményes helyzetet kezelni fog.

Készen állsz a következő szintre? Próbáld ki:

- Adó számítások hozzáadása a kedvezmények mellé.
- Kedvezmény százalékok adatbázisból való lekérése a hard‑kódolás helyett.
- Feltételes formázás használata a magas kedvezményű sorok kiemeléséhez.

Ezek a kiegészítések megőrzik a központi elképzelést, miközben bővítik a kedvezmény sablon hasznosságát.

Van kérdésed vagy egy klassz felhasználási eset? Hagyj egy megjegyzést alább, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}