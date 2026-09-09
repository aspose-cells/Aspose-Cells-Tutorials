---
category: general
date: 2026-02-15
description: Hogyan formázzuk gyorsan a pénznemet a „set column number format” használatával
  és egyedi numerikus formátum alkalmazásával C#-ban. Tanulja meg, hogyan lehet név
  alapján lekérni egy oszlopot és beállítani a rács oszlopának igazítását.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: hu
og_description: Hogyan formázzuk a pénznemet egy rácsoszlopban C#-ban. Ez az útmutató
  bemutatja, hogyan lehet oszlopot lekérni név alapján, beállítani az oszlop számformátumát,
  egyéni numerikus formátumot alkalmazni, és beállítani a rácsoszlop igazítását.
og_title: Hogyan formázzuk a pénznemet egy rácsoszlopban – Teljes útmutató
tags:
- C#
- GridFormatting
- UI
title: Hogyan formázzuk a pénznemet egy rács oszlopban – Lépésről lépésre útmutató
url: /hu/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan formázzuk a pénznemet egy rácsoszlopban – Teljes programozási útmutató

Valaha is elgondolkodtál **hogyan formázzuk a pénznemet** egy rácsoszlopban anélkül, hogy a hajad kihúznád? Nem vagy egyedül. Amikor egy egyszerű számot, például `1234.5` nézel, és azt szeretnéd, hogy varázslatosan megjelenjen `$1,234.50`‑ként, a válasz általában csak néhány sor konfiguráció.  

Ebben az útmutatóban **lekérjük a oszlopot név alapján**, **beállítjuk az oszlop számformátumát**, és **alkalmazunk egy egyedi numerikus formátumot**, amely a tipikus könyvelési elrendezést követi. Útközben **beállítjuk a rácsoszlop igazítását** és hozzáadunk egy finom keretet, hogy a felhasználói felület kifinomultabb legyen.

> **TL;DR** – A végére egy kész, futtatható kódrészletet kapsz, amely a nyers decimális értékeket gyönyörűen formázott pénznemértékekké alakítja bármely `GridJs`‑stílusú vezérlőben.

---

## Amire szükséged lesz

- Egy .NET projekt (bármely verzió, amely támogatja a C# 8.0+‑t – a Visual Studio 2022 remekül működik).  
- Egy rácskomponens, amely egy `Columns` gyűjteményt biztosít (a példa egy fiktív `GridJs` osztályt használ, de a koncepciók átültethetők a DevExpress, Telerik vagy Syncfusion rácsokra).  
- Alapvető ismeretek a C# szintaxisról – nincs szükség haladó trükkökre.

Ha már megvannak ezek, nagyszerű. Ha nem, indíts egy konzolalkalmazást; a rácsot illusztrációként mockolhatod.

---

## Lépés‑ről‑lépésre megvalósítás

Az egyes lépések alatt egy kompakt kódrészletet, egy rövid magyarázatot **arról, hogy miért** fontos a sor, és egy tippet találsz a gyakori hibák elkerüléséhez.

### ## 1. lépés – A “Amount” oszlop lekérése név alapján

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Miért fontos:**  
A legtöbb rács‑API oszlopokat szótár‑szerű indexerrel tesz elérhetővé. Az oszlop lekérése a fejléc neve (`"Amount"`) alapján lehetővé teszi a megjelenés manipulálását anélkül, hogy az alatta lévő adatforrást érintenéd.  

**Pro tipp:** Mindig ellenőrizd a `null` visszatérési értéket – egy elütés a oszlop nevében vagy egy dinamikus séma változás egyébként `NullReferenceException`‑t okozhat futásidőben.

---

### ## 2. lépés – Oszlop számformátum beállítása egy egyedi pénznem‑maszkkal

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Miért fontos:**  
A formátum karakterlánc az Excel könyvelési formátum konvencióit követi:

- `_(* #,##0.00_)` → Pozitív számok, jobbra igazítva, a pénznem szimbólum előtt egy vezető szóközzel.  
- `_(* (#,##0.00)` → Negatív számok zárójelek közé téve.  
- `_(* \"-\"??_)` → Null értékek kötőjelként jelennek meg.  
- `_(@_)` → A szöveges értékek változatlanul maradnak.

Az **apply custom numeric format** használata teljes kontrollt ad a ezreselválasztók, tizedesjegyek és a pénznem jel elhelyezése felett.  

**Széljegyzet:** Ha alkalmazásodnak másik helyi beállítást kell támogatnia (pl. Euro a USD helyett), cseréld ki a vezető szóközt a megfelelő szimbólumra, vagy használd a `CultureInfo`‑tudatos formázást az adatforrásban.

---

### ## 3. lépés – Az oszlop tartalmának jobbra igazítása a jobb olvashatóságért

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Miért fontos:**  
A pénznemértékek könnyebben áttekinthetők, ha a tizedesponton igazodnak. A **set grid column alignment** `Right`‑ra állítása tükrözi a táblázatok pénzügyi adatok megjelenítését.  

**Figyelem:** Egyes rácsok figyelmen kívül hagyják az igazítást olyan cellákon, amelyek egyedi sablonokat tartalmaznak. Ha az igazítás nem lép életbe, ellenőrizd, hogy az oszlop nem egyedi cella‑renderert használ-e.

---

### ## 4. lépés – Vékony szürke keret hozzáadása az oszlopcellák köré

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Miért fontos:**  
Egy finom keret elválasztja a “Amount” oszlopot a szomszédosaktól, különösen ha a rácsnak váltakozó sor‑színei vannak. Ez egy vizuális jelzés, hogy az adat egy különálló pénzügyi értéket képvisel.  

**Tipp:** Ha nyomtatáshoz vastagabb vonalra van szükséged, állítsd a `BorderLineStyle`‑t `Medium`‑re, vagy változtasd a `Color`‑t `Color.Black`‑ra.

---

## Teljes működő példa

Az alábbi kódrészletet egyszerűen beillesztheted egy WinForms vagy WPF projektbe, amely `GridJs`‑stílusú vezérlőt használ. A példa a formázott értékeket a konzolra is kiírja, így UI nélkül is ellenőrizheted a kimenetet.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Várt konzolkimenet**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Figyeld meg, hogy a pozitív szám jobbra igazított, a negatív zárójelek közé kerül, a nulla pedig kötőjelként jelenik meg – pontosan úgy, ahogy az egyedi formátum karakterlánc előírja.

---

## Gyakran ismételt kérdések & széljegyzetek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a rács másik kultúrát használ (pl. € a $ helyett)?* | Cseréld ki a formátum karakterláncban a vezető szóközt a kívánt szimbólumra, vagy engedd, hogy az adatforrás egy előre formázott stringet adjon vissza a `CultureInfo.CurrentCulture`‑al. |
| *Újra felhasználhatom ugyanazt a formátumot több oszlophoz?* | Természetesen. Tárold a formátum karakterláncot egy konstansban (`const string CurrencyMask = "...";`) és rendeld hozzá bárhol, ahol pénznemet kell megjeleníteni. |
| *Mi történik, ha az oszlop szöveges értéket tartalmaz?* | A formátum karakterlánc csak numerikus típusokra hat. A stringek változatlanul átmennek, ezért létezik a maszk utolsó része (`_(@_)`) – megőrzi a nem numerikus tartalmat. |
| *Van teljesítménybeli hatása?* | Elhanyagolható. A formátum a rendereléskor kerül alkalmazásra, nem az adatlekérés során. Hacsak nem több ezer sort renderelsz képkockánként, nem fogsz lassulást észlelni. |
| *Hogyan tehetem vastagabbá a keretet nyomtatott jelentésekhez?* | Cseréld a `BorderLineStyle.Thin`‑t `BorderLineStyle.Medium`‑re vagy `BorderLineStyle.Thick`‑ra. Néhány könyvtár közvetlen pixel‑szélességet is enged megadni. |

---

## Összegzés

Lépésről lépésre végigmentünk **hogyan formázzuk a pénznemet** egy rácsoszlopban: oszlop lekérése név alapján, számformátum beállítása, egyedi numerikus formátum alkalmazása, cellák igazítása és egy ízléses keret hozzáadása. A teljes példa azonnal futtatható, és pontosan azt a vizuális eredményt mutatja, amit elvárhatsz.

Ha készen állsz a továbblépésre, próbáld ki:

- **Dinamikus kultúrák** – a formátum karakterlánc cseréje a felhasználó helyi beállításai alapján.  
- **Feltételes…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}