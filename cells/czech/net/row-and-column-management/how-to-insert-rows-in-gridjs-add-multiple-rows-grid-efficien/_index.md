---
category: general
date: 2026-03-29
description: Naučte se rychle vkládat řádky do GridJs. Tento průvodce také popisuje,
  jak přidávat řádky a přidávat více řádků do mřížky pomocí hromadné operace.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: cs
og_description: Naučte se rychle vkládat řádky v GridJs. Tento průvodce ukazuje, jak
  přidávat řádky, přidávat více řádků do gridu a zpracovávat velké dávky vkládání.
og_title: Jak vložit řádky v GridJs – Efektivně přidávejte více řádků do mřížky
tags:
- GridJs
- C#
- data‑grid
title: Jak vložit řádky v GridJs – Efektivně přidávejte více řádků do gridu
url: /cs/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit řádky v GridJs – Efektivně přidávat více řádků do mřížky

Už jste se někdy zamysleli **jak vložit řádky** do obrovské tabulky GridJs, aniž by se UI zamrzlo? Možná jste narazili na problém při **přidávání řádků** po jednom a výkon se rozpadl. Dobrou zprávou je, že GridJs nabízí batch API, které vám umožní **přidat více řádků do mřížky** v jediném volání, takže vše zůstane rychlé i při práci s miliony záznamů.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který přesně ukazuje **jak vložit řádky** pomocí `InsertRowsBatch`. Uvidíte, proč je dávkování důležité, jak ověřit výsledek a na co si dát pozor, když je cílový index obrovský. Na konci budete schopni s jistotou vložit tisíc nových záznamů do libovolné instance GridJs.

## Požadavky

- .NET 6.0 nebo novější (kód se kompiluje s jakýmkoli aktuálním SDK)
- Odkaz na NuGet balíček `GridJs` (nebo DLL, pokud používáte vlastní build)
- Základní znalost C# – nemusíte být guru, stačí vám pohodlná práce s třídami a metodami
- IDE nebo editor dle vašeho výběru (Visual Studio, Rider, VS Code… vše funguje)

> **Tip:** Pokud plánujete pracovat s opravdu obrovskými mřížkami (desítky milionů řádků), povolte `gridJs.EnableVirtualization = true;`, aby bylo vykreslování UI lehké.

## Krok 1: Vytvořte a nakonfigurujte instanci GridJs

Nejprve potřebujete živý objekt `GridJs`. Představte si ho jako plátno, na které budete malovat řádky.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Proč je tento krok důležitý:** Inicializace mřížky a volitelné naplnění dat odráží reálný scénář, kdy mřížka již obsahuje velké množství informací. Dávkové vkládání, které provedeme později, musí respektovat indexování od nuly, proto předem naplníme data, abychom ukázali přesný bod vložení.

## Krok 2: Použijte `InsertRowsBatch` k **přidání více řádků do mřížky**

Nyní jádro tutoriálu – volání, které skutečně **přidává řádky** ve velkém. Signatura metody je `InsertRowsBatch(int startIndex, int count)`. V našem příkladu začneme na indexu 2 000 000 (což odpovídá 2 000 001. řádku) a přidáme deset řádků.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Jak to funguje:** `InsertRowsBatch` interně alokuje požadovaný počet řádků a posune existující řádky dolů. Protože operace probíhá v jedné transakci, UI se obnoví jen jednou, což je důvod, proč je tato metoda doporučeným způsobem, jak **přidávat řádky** efektivně.

## Krok 3: Ověřte vložení – Dostaly se řádky na očekávané místo?

Po dávkové operaci budete chtít mít jistotu, že řádky jsou tam, kde očekáváte. Následující pomocná metoda načte první a poslední řádek nově přidaného bloku a vypíše je do konzole.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Očekávaný výstup**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Prázdné buňky naznačují, že řádky jsou jen zástupci čekající na data. Nyní je můžete individuálně naplnit nebo spustit další dávkovou aktualizaci.

> **Poznámka k okrajovým případům:** Pokud `startIndex` překročí aktuální počet řádků, GridJs automaticky přidá nové řádky na konec. Naopak záporný index vyvolá `ArgumentOutOfRangeException`, takže vždy ověřujte indexy dodané uživatelem.

## Krok 4: Naplňte nové řádky (volitelné, ale běžné)

Často nechcete jen prázdné řádky; potřebujete je naplnit smysluplnými hodnotami. Můžete projít nově vytvořený rozsah a zavolat `SetCell` nebo podobné API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Můžete zavolat `PopulateNewRows(gridJs, startIndex, rowsToAdd);` hned po dávkovém vložení, pokud potřebujete řádky okamžitě připravené k zobrazení.

## Krok 5: Tipy pro výkon u velmi velkých mřížek

Když pracujete s **přidáváním více řádků do mřížky** v milionech, mějte na paměti tyto triky:

1. **Velikost dávky má význam** – Vložení 10 000 řádků najednou může být rychlejší než deset samostatných dávek po 1 000 řádcích, protože každá dávka způsobí jedinou obnovu UI.
2. **Vypněte aktualizace UI** – Některé verze GridJs poskytují `grid.SuspendLayout()` / `grid.ResumeLayout()`. Zabalte svou dávku do těchto volání, pokud zaznamenáte zpoždění.
3. **Použijte virtualizaci** – Jak bylo ukázáno dříve, `EnableVirtualization` dramaticky snižuje spotřebu paměti a čas vykreslování.
4. **Vyhněte se hlubokým kopiím** – Předávejte do mřížky jednoduché typy hodnot nebo lehké objekty; těžké objekty nutí mřížku klonovat data, což snižuje výkon.

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Spusťte program a uvidíte výstup v konzoli, který potvrzuje, že deset řádků bylo vloženo na správné místo a následně naplněno.

## Závěr

Probrali jsme **jak vložit řádky** v GridJs pomocí batch API, ukázali **jak přidávat řádky** efektivně a prozkoumali způsoby, jak **přidat více řádků do mřížky** bez zatížení UI. Hlavní poznatky jsou:

- Použijte `InsertRowsBatch(startIndex, count)` pro jakoukoli hromadnou operaci.
- Ověřujte indexy a zvažte virtualizaci pro masivní datové sady.
- Naplněte řádky po dávce, pokud potřebujete okamžitý obsah.

Dále byste mohli chtít prozkoumat **jak mazat řádky**, implementovat **undo/redo** pro dávkové úpravy, nebo integrovat GridJs s backendovou službou, která streamuje data na požádání. Všechny tyto témata staví přímo na konceptech, které jste se právě naučili.

Neváhejte experimentovat – změňte velikost dávky, zkuste vložit na úplný začátek mřížky nebo zkombinovat více dávek v jedné transakci. Čím více si s tím pohráváte, tím jistěji se budete cítit při práci s velkými

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}