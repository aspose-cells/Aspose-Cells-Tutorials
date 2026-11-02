---
category: general
date: 2026-10-10
description: Tanulja meg, hogyan törölhet teljes sort egy Excel munkafüzetben C#-vel.
  Ez a lépésről‑lépésre útmutató azt is bemutatja, hogyan törölhet sort index alapján,
  és hogyan távolíthat el sort index szerint az Aspose.Cells használatával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: hu
lastmod: 2026-10-10
og_description: Törölje az egész sort egy Excel munkafüzetben C#-al. Kövesse ezt az
  útmutatót, hogy megtanulja, hogyan törölhet sort index alapján, hogyan távolíthat
  el sort index szerint, és hogyan mentheti biztonságosan a fájlt.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Teljes sor törlése Excelben C#-al – teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hogyan töröljünk teljes sort egy Excel-fájlban C#-val
url: /hu/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Teljes sor törlése egy Excel-fájlban C#-val

Ha **teljes sort** kell törölnie egy Excel munkafüzetben, ez az útmutató pontosan megmutatja, hogyan teheti ezt C#-ban. Akár importált adatokat tisztít, akár jelentéskészítő eszközt épít, az alábbi lépések lehetővé teszik, hogy egy sort az indexe alapján eltávolítson, és az eredményt anélkül mentse, hogy más adatokat elveszítene.

Látni fogja, hogyan válaszol ugyanaz a megközelítés a **hogyan töröljünk sort** kérdésre index alapján, hogyan **sor törlése index szerint**, és miért működik ez **excel sor törlése** forgatókönyveknél C#-ban.

## Előkövetelmények

* .NET 6.0 vagy újabb (a kód a .NET Framework 4.6+ verzióval is működik)  
* Az **Aspose.Cells for .NET** könyvtár (elérhető a NuGet-en: `Install-Package Aspose.Cells`)  
* Alapvető ismeretek a C# konzol vagy asztali projektekhez  

Nem szükséges további Excel interop vagy COM komponens, ami könnyűsúlyúvá és szerveroldali futtatásra biztonságossá teszi a megoldást.

## 1. lépés: A projekt beállítása és a névterek importálása

Hozzon létre egy új konzolos alkalmazást (vagy adja hozzá a kódot egy meglévő projekthez), és adja hozzá a szükséges `using` direktívákat:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Miért fontos*: Az `Aspose.Cells` importálása hozzáférést biztosít a `Workbook`, `Worksheet` és a `DeleteRows` metódushoz, amely a tényleges sor eltávolítását végzi.

## 2. lépés: A munkafüzet betöltése és a munkalap kiválasztása

Be kell töltenie a forrásfájlt (`input.xlsx`), és meg kell szereznie a módosítani kívánt munkalapot. Az első munkalap az `0` indexszel érhető el.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tipp**: Ha egy adott munkalappal kell dolgoznia, cserélje le az indexet a munkalap nevére: `workbook.Worksheets["Data"]`.

## 3. lépés: A teljes sor törlése a nulláralapú index alapján

Az Aspose.Cells nulláralapú indexelést használ, így az első sor `0`. Az 5‑ös sor (a hatodik látható sor) törléséhez hívja a `DeleteRows` metódust a `DeleteOptions.DeleteEntireRow` paraméterrel.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Magyarázat*:

* `ws.Cells[5, 0]` a törölni kívánt sor első cellájára mutat.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` azt mondja az Aspose.Cells-nek, hogy **1** sort távolítson el, és a `DeleteEntireRow` jelző biztosítja, hogy **az egész sor** eltűnjön, a sorok alatta felfelé tolódnak.

### Hogyan töröljünk sort index szerint más helyzetekben

* **Több egymást követő sor törlése** – módosítsa az első argumentumot a törölni kívánt sorok számával:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Az utolsó sor törlése** – használja a `ws.Cells.MaxDataRow`-t a legalsó kitöltött sor indexének lekéréséhez:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Ezek a kódrészletek megválaszolják a **sor törlése index szerint** követelményt, miközben a kód könnyen olvasható marad.

## 4. lépés: A munkafüzet mentése a sor eltávolítása után

A törlés után írja vissza a módosított munkafüzetet a lemezre. Felülírhatja az eredeti fájlt, vagy létrehozhat egy újat.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Ha az eredeti fájlt változatlanul szeretné hagyni, egyszerűen módosítsa a kimeneti útvonalat. A `Save` metódus számos formátumot támogat (`.xls`, `.csv`, `.pdf`, stb.) – csak változtassa meg a fájl kiterjesztését.

## Teljes működő példa

Összegezve, itt egy teljes, azonnal futtatható program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Várható kimenet**: A program futtatása után az `output.xlsx` tartalmazni fogja az összes eredeti sort, kivéve azt, amely a 6‑odik látható sorban kezdődött. Az eltávolított sor alatti összes adat automatikusan felfelé tolódik, megőrizve a képleteket és a formázást.

## Gyakori buktatók és hogyan kerülhetők el

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Index kívül esik** | Megpróbál egy olyan sorindexet törölni, amely nem létezik (pl. `ws.Cells[1000,0]` egy 200 soros lapon) | Használja a `ws.Cells.MaxDataRow`-t a legmagasabb érvényes index ellenőrzéséhez a `DeleteRows` hívása előtt. |
| **Részleges sor törlés** | `DeleteOptions.DeleteEntireRow` kihagyása csak a cellák tartalmát törli | Mindig adja át a `DeleteOptions.DeleteEntireRow`-t, ha az egész sort szeretné eltávolítani. |
| **Váratlan képletváltozások** | A képlet tartomány részeinek törlése megszakíthatja a hivatkozásokat | Értékelje újra a képleteket a törlés után (`workbook.CalculateFormula()`), ha a munkafüzet dinamikus tartományokra támaszkodik. |
| **Mentés csak olvasható helyre** | A `Save` hívás kivételt dob, ha a mappa védett | Győződjön meg arról, hogy a célkönyvtár írható, vagy futtassa a programot megfelelő jogosultságokkal. |

Ezeknek a kérdéseknek a kezelése a megoldást robusztusabbá teszi a termelésben való használatra, és kielégíti a **excel sor törlése** és **c# sor törlése** lekérdezéseket.

## Haladó: Sorok törlése feltétel alapján

Néha olyan sorokat kell eltávolítani, amelyek egy adott feltételnek megfelelnek (pl. azok a sorok, ahol az A oszlop üres). Az alábbi ciklus biztonságos módot mutat be a lentről felfelé történő beolvasásra és a megfelelő sorok törlésére:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

A felfelé történő beolvasás megakadályozza az indexeltolódási problémát, amely akkor jelentkezik, amikor a sorokat előre iterálva töröljük.

## Következtetés

Most már tudja, hogyan **töröljön teljes sort** egy Excel munkafüzetben C#-val. Az útmutató a következőket fedte le:

* Munkafüzet betöltése és munkalap kiválasztása  
* `DeleteRows` használata a `DeleteOptions.DeleteEntireRow`-rel a **hogyan töröljünk sort** index szerint  
* A módosított fájl biztonságos mentése  
* Szélső esetek kezelése, teljesítmény tippek, és egy feltételes törlési példa  

Ezzel a tudással magabiztosan megvalósíthatja a **sor törlése index szerint** funkciót, automatizálhatja az adattisztítást, és beépítheti az Excel manipulációt bármely C# alkalmazásba.  

**Következő lépések**: fedezze fel az Aspose.Cells egyéb funkcióit, mint például sorok beszúrása, tartományok másolása vagy a munkafüzet PDF‑re konvertálása – mindegyik az Ön által most elsajátított `Workbook` és `Worksheet` objektumokra épül. Boldog kódolást!

## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek az ebben az útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan töröljünk Excel sort Aspose.Cells .NET: Átfogó útmutató](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Sorok törlése – Fejléc sor védelme Excelben](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Hatékony sorkezelés Excelben Aspose.Cells for Java: Sorok beszúrása és törlése](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}