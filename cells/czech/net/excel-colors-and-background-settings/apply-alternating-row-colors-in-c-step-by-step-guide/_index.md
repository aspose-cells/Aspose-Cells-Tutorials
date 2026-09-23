---
category: general
date: 2026-03-18
description: Naučte se, jak v listu použít střídavé barvy řádků pomocí C#. Zahrnuje
  nastavení barvy pozadí řádku, přidání světle žlutého pozadí a střídavé barvení řádků.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: cs
og_description: Použijte střídavé barvy řádků v C# pro zlepšení čitelnosti. Tento
  návod ukazuje, jak nastavit barvu pozadí řádku, přidat světle žluté pozadí a střídavě
  barvit řádky.
og_title: Použít střídavé barvy řádků v C# – kompletní tutoriál
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Použijte střídavé barvy řádků v C# – krok za krokem
url: /cs/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití střídavých barev řádků v C# – Kompletní tutoriál

Už jste někdy potřebovali **aplikovat střídavé barvy řádků** na tabulku řízenou daty, ale nebyli jste si jisti, kde začít? Nejste v tom jediní — většina vývojářů narazí na tento problém, když poprvé chtějí, aby tabulky vypadaly přátelštěji. Dobrá zpráva? Už v několika řádcích C# můžete **nastavit barvu pozadí řádku**, přidat **světle žluté pozadí** a získat vylepšenou mřížku, která okamžitě zvyšuje čitelnost.

V tomto tutoriálu projdeme celý proces, od načtení `DataTable` do paměti až po stylování každého řádku jemnou žluto‑bílou pruhovanou šablonou. Na konci budete schopni **barevně odlišovat řádky střídavě** s jistotou a uvidíte i několik užitečných variant pro různé odstíny nebo dynamické motivy.

## Co budete potřebovat

- Projekt .NET cílící na .NET 6 nebo novější (kód funguje také na .NET Framework 4.7+).  
- Knihovna pro práci s tabulkami, která podporuje objekty stylů – příklad používá obecné API `Workbook`/`Worksheet`, které odpovídá knihovnám jako **Aspose.Cells**, **GemBox.Spreadsheet** nebo **ClosedXML**.  
- Zdroj `DataTable` – může pocházet z databázového dotazu, importu CSV nebo jakékoli kolekce v paměti.  

Žádné další NuGet balíčky kromě samotné knihovny pro tabulky. Pokud používáte Aspose.Cells, jmenný prostor je `Aspose.Cells`; pro ClosedXML je to `ClosedXML.Excel`. Vyměňte volání `CreateStyle` a `ImportDataTable` podle potřeby.

## Krok 1: Načtení zdrojových dat jako DataTable

Nejprve si načtěte data, která chcete zobrazit. V reálných aplikacích to obvykle znamená dotaz do databáze, ale pro přehlednost vytvoříme pomocnou metodu `GetData()`, která vrací naplněný `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Proč je to důležité:** `DataTable` definuje řádky a sloupce, které později získají střídavé stínování. Pokud je tabulka prázdná, není co stylovat, takže vždy ověřte, že `Rows.Count` > 0 před pokračováním.

### Pro tip
Pokud načítáte data z Entity Framework, můžete po provedení `SqlCommand` použít `DataTable.Load(reader)`. Tím udržíte kód přehledný a vyhnete se ruční definici sloupců.

## Krok 2: Alokace pole pro uchování stylu pro každý řádek

Dále potřebujeme kontejner, který odpovídá počtu řádků. Většina API pro tabulky umožňuje předat pole stylů metodě importu, takže vytvoříme `Style[]` přesně velikosti počtu řádků.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Vysvětlení:** Předalokováním pole se vyhneme vytváření nového objektu stylu při každé iteraci, což může být výkonnostní výhoda při práci s tisíci řádky.

## Krok 3: Aplikace střídavých barev řádků (světle žlutá / bílá)

Nyní přichází jádro úkolu: **aplikovat střídavé barvy řádků**. Projdeme každý řádek, vytvoříme čerstvou instanci stylu z workbooku a nastavíme jeho pozadí podle indexu řádku. Sudé řádky získají světle žlutou výplň, liché zůstanou bílé.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Proč to funguje
- `rowIndex % 2 == 0` kontroluje, zda je řádek sudý.  
- `Color.LightYellow` poskytuje jemný, nenápadný odstín, který je ideální pro datové tabulky.  
- `BackgroundType.Solid` zajišťuje, že výplň pokrývá celou buňku, čímž dosahuje efektu **nastavení barvy pozadí řádku**.  

Můžete nahradit `Color.LightYellow` libovolným jiným odstínem (např. `Color.LightCyan`), pokud preferujete jiný vzhled. Stejná logika vám také umožní **barevně odlišovat řádky střídavě** na základě jiných kritérií, jako jsou stavové příznaky.

## Krok 4: Import DataTable do listu s připravenými styly

Nakonec vše vložíme do listu. Většina knihoven poskytuje přetížení `ImportDataTable`, které přijímá pole stylů. Příznak `true` říká API, aby zapsalo záhlaví sloupců, a souřadnice `0, 0` začínají v levém horním rohu buňky.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Výsledek:** List nyní zobrazuje data s čistým **střídavým stínováním řádků** – světle žluté na sudých řádcích, bílé na lichých. Uživatelé mohou prohlížet mřížku, aniž by jejich oči skákaly sem a tam.

### Očekávaný výstup
Pokud otevřete výsledný sešit, uvidíte něco jako:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Řádky 1, 3, 5… mají **světle žluté pozadí**, zatímco řádky 2, 4, 6… zůstávají **bílé**. Záhlaví (řádek 0) dědí výchozí styl, pokud jej neupraveně nastavíte zvlášť.

## Volitelné varianty a okrajové případy

### 1. Použití jiné barevné palety
Pokud světle žlutá nesouhlasí s vaší značkou, jednoduše nahraďte `Color.LightYellow` jinou `System.Drawing.Color`. Pro téma modro‑šedé můžete použít:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamické stínování na základě dat
Někdy chcete zvýraznit řádky, které splňují podmínku (např. nízký stav zásob). Kombinujte kontrolu modulo s vlastním testem:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Aplikace stylů pouze na konkrétní sloupce
Pokud potřebujete **nastavení barvy pozadí řádku** jen na určitých sloupcích, vytvořte samostatný styl pro každý sloupec a přiřaďte jej po importu pomocí API pro rozsahy buněk listu.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Tip pro výkon u velkých tabulek
Při práci s > 10 000 řádky zvažte opětovné použití jediného objektu stylu pro každou barvu místo vytváření nového pro každý řádek. Pole pak obsahuje odkazy na dva sdílené styly, což dramaticky snižuje spotřebu paměti.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Kompletní funkční příklad

Níže je samostatný program, který můžete vložit do konzolové aplikace. Používá fiktivní API `Workbook`/`Worksheet`; nahraďte typy těmi z vámi zvolené knihovny.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Výstup:** Soubor pojmenovaný `AlternatingRows.xlsx`, kde každý řádek střídavě používá světle žlutou výplň a bílou, což usnadňuje čtení tabulky.

## Často kladené otázky

**Q: Funguje tento přístup s podmíněným formátováním ve stylu Excel?**  
A: Ano. Pokud vaše knihovna podporuje podmíněná pravidla, můžete stejnou logiku převést na pravidlo, které kontroluje `MOD(ROW(),2)=0`. Metoda založená na kódu, jak je zde ukázána, je přenosnější mezi knihovnami, které nemají vestavěné podmíněné formátování.

**Q: Co když potřebuji **barevně odlišovat řádky střídavě** v PDF tabulce místo Excel listu?**  
A: Většina generátorů PDF tabulek (např. iTextSharp, PdfSharp) umožňuje nastavit `BackgroundColor` pro každý řádek. Stejný výpočet modulo se použije—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}