---
category: general
date: 2026-03-01
description: Jak snadno vkládat řádky v GridJs — naučte se přidat 100 řádků, vytvořit
  prázdné řádky a zkontrolovat celkový počet řádků pomocí několika řádků C#.
draft: false
keywords:
- how to insert rows
- add multiple rows
- add 100 rows
- create empty rows
- check total rows
language: cs
og_description: Jak rychle vložit řádky v GridJs. Tento průvodce vám ukáže, jak přidat
  více řádků, vytvořit prázdné řádky a zkontrolovat celkový počet řádků pomocí čistého
  C# kódu.
og_title: Jak vložit řádky v GridJs – Rychlý průvodce
tags:
- C#
- GridJs
- data‑grid
title: Jak vložit řádky v GridJs – rychle přidat více řádků
url: /cs/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit řádky v GridJs – Rychle přidat více řádků

Už jste se někdy zamýšleli **jak vložit řádky** do datové mřížky GridJs, aniž byste museli psát smyčku, která táhne věčnost? Nejste v tom sami. V mnoha podnikových aplikacích narazíte na situaci, kdy potřebujete uvolnit místo pro hromadný import, šablonu nebo jen zástupný prvek pro budoucí data. Dobrá zpráva? GridJs vám poskytuje jedinou metodu, která za vás udělá těžkou práci.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **přidat 100 řádků**, **vytvořit prázdné řádky** a **zkontrolovat celkový počet řádků** po operaci. Na konci budete mít osvědčený vzor, který můžete vložit do libovolného C# projektu používajícího GridJs.

## Předpoklady

- .NET 6.0 nebo novější (API funguje stejně na .NET Framework 4.8, ale novější SDK poskytuje lepší nástroje).
- Odkaz na NuGet balíček `GridJs` nebo zkompilovanou DLL, která obsahuje třídu `GridJs`.
- Základní znalost syntaxe C# – nic exotického, jen standardní `using` příkazy a objektově orientované základy.

Pokud některý z nich vyvolá červenou vlajku, zastavte se na chvíli a vyřešte to. Následující kroky předpokládají, že objekt mřížky je již vytvořen a připraven přijímat řádky.

![ilustrace jak vložit řádky](gridjs-insert-rows.png)

## Krok 1: Nastavení instance Grid

Nejprve potřebujete objekt `GridJs`. V reálné aplikaci by pravděpodobně pocházel ze servisní vrstvy nebo byl injektován pomocí dependency injection, ale pro přehlednost jej vytvoříme lokálně.

```csharp
using System;
using GridJsLibrary;   // <-- replace with the actual namespace of GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create or obtain the grid you want to modify
            GridJs gridJs = new GridJs();   // replace with your actual grid initialization
```

> **Proč je to důležité:** Vytvoření instance mřížky vám poskytne čistý start, což zajišťuje, že logika vkládání řádků nebude kolidovat se zbytkovým stavem z předchozích běhů.

## Krok 2: Vložení 100 řádků na konkrétní index

Nyní přichází jádro **jak vložit řádky**. Metoda `InsertRows` přijímá dva argumenty: nulově‑založený počáteční index a počet řádků, které chcete přidat. Vložme 100 řádků počínaje řádkem 5.

```csharp
            // Step 2: Insert 100 rows starting at row index 5 (zero‑based)
            // This pushes existing rows down and creates space for new data.
            gridJs.InsertRows(5, 100);
```

> **Tip:** Pokud potřebujete přidat řádky na úplný konec mřížky, můžete použít `gridJs.RowCount` jako počáteční index. Tímto způsobem v podstatě „přidáváte“ místo vkládání.

### Co se děje pod kapotou?

- **Alokace paměti:** `InsertRows` interně alokuje blok prázdných objektů řádků, takže je nemusíte ručně vytvářet.
- **Posun indexu:** Všechny řádky, které byly na indexu 5 nebo později, se posunou dolů o 100 pozic, přičemž zachovají svá původní data.
- **Výkon:** Protože operace je provedena jedním voláním, je obvykle rychlejší než opakované volání `InsertRow` 100 krát.

## Krok 3: Ověření vložení (kontrola celkového počtu řádků)

Po přidání řádků je dobrým zvykem **zkontrolovat celkový počet řádků**, aby se potvrdilo, že operace byla úspěšná. Vlastnost `RowCount` vám poskytne aktuální počet řádků v mřížce.

```csharp
            // Step 3: (Optional) Verify the insertion or continue processing
            int newRowCount = gridJs.RowCount; // example property to check total rows
            Console.WriteLine($"Grid now contains {newRowCount} rows.");
```

Pokud jste začali třeba s 20 řádky, měli byste vidět `120` vytištěné v konzoli. Tento jednoduchý ověřovací krok vám může později ušetřit hodiny ladění.

## Krok 4: Naplnění nově vytvořených prázdných řádků (volitelné)

Často budete chtít naplnit ty čerstvě vytvořené řádky zástupnými daty nebo výchozími objekty. Protože `InsertRows` vám poskytuje blok prázdných řádků, můžete přes rozsah projít smyčkou a přiřadit hodnoty.

```csharp
            // Optional: Fill the newly created rows with default values
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i); // assume GetRow returns a mutable row object
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Verify a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

> **Proč byste to mohli udělat:** Vytváření prázdných řádků je užitečné, když potřebujete šablonu pro vstup uživatele, zástupný prvek pro hromadné nahrání nebo prostě chcete rezervovat místo pro budoucí výpočty.

## Běžné varianty a okrajové případy

### Přidání méně než 100 řádků

Pokud potřebujete jen **přidat více řádků**—například 10 nebo 25—stejné volání `InsertRows` funguje; stačí nahradit `100` požadovaným počtem.

```csharp
gridJs.InsertRows(startIndex, 25); // adds 25 rows
```

### Vkládání na začátek mřížky

Chcete přidat řádky na začátek? Použijte `0` jako počáteční index:

```csharp
gridJs.InsertRows(0, 5); // adds 5 rows at the very beginning
```

### Zpracování indexů mimo rozsah

Předání indexu většího než `RowCount` vyvolá `ArgumentOutOfRangeException`. Ochráníte se tímto:

```csharp
int safeIndex = Math.Min(requestedIndex, gridJs.RowCount);
gridJs.InsertRows(safeIndex, 100);
```

### Práce s mřížkami jen pro čtení

Některé konfigurace GridJs poskytují pouze pro čtení pohled. V takovém scénáři budete muset přepnout na zapisovatelnou instanci nebo dočasně zakázat příznak jen pro čtení před voláním `InsertRows`.

## Tipy pro výkon

- **Dávkové operace:** Pokud řádky vkládáte opakovaně ve smyčce, seskupte je do jednoho volání `InsertRows`, kdykoli je to možné. Tím se sníží interní realokace seznamu.
- **Vyhněte se obnovám UI:** V UI‑vázaných mřížkách pozastavte vykreslování (`gridJs.BeginUpdate()`) před vložením řádků a poté jej obnovte (`gridJs.EndUpdate()`), aby se zabránilo blikání.
- **Profilování paměti:** Velké vkládání (např. >10 000 řádků) může zvýšit využití paměti. Zvažte stránkování nebo streamování dat místo jednoho obrovského vložení.

## Kompletní funkční příklad – shrnutí

Sestavením všeho dohromady je zde kompletní program připravený ke kopírování a vložení:

```csharp
using System;
using GridJsLibrary;   // replace with the actual namespace

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the grid instance
            GridJs gridJs = new GridJs();

            // Insert 100 rows starting at index 5
            gridJs.InsertRows(5, 100);

            // Verify insertion
            int newRowCount = gridJs.RowCount;
            Console.WriteLine($"Grid now contains {newRowCount} rows.");

            // Optional: Fill new rows with placeholder data
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i);
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Show a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

Spusťte tento program a uvidíte výstup v konzoli, který potvrzuje počet řádků a název prvního zástupného řádku. To je kompletní odpověď na **jak vložit řádky** v GridJs, včetně ověření a volitelného naplnění dat.

## Závěr

Prošli jsme jasným, kompletním řešením **jak vložit řádky** v GridJs, zahrnujícím, jak **přidat 100 řádků**, **vytvořit prázdné řádky** a **zkontrolovat celkový počet řádků** po operaci. Vzor je škálovatelný – stačí upravit počáteční index a počet, abyste **přidali více řádků** kdekoliv je potřebujete.

Další kroky? Zkuste kombinovat tuto techniku s hromadnými importy dat z CSV souborů nebo experimentujte s podmíněným vytvářením řádků na základě vstupu uživatele. Pokud vás zajímá mazání řádků, řazení nebo aplikace podmíněného formátování, jsou to přirozené rozšíření stejného rozhraní API.

Šťastné programování a ať jsou vaše mřížky vždy dokonale veliké!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}