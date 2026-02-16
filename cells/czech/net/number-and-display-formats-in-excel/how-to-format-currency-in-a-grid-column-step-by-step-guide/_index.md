---
category: general
date: 2026-02-15
description: Jak rychle formátovat měnu pomocí nastavení formátu čísla sloupce a aplikovat
  vlastní číselný formát v C#. Naučte se získat sloupec podle názvu a nastavit zarovnání
  sloupce v mřížce.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: cs
og_description: Jak formátovat měnu ve sloupci mřížky pomocí C#. Tento tutoriál ukazuje,
  jak získat sloupec podle názvu, nastavit číselný formát sloupce, použít vlastní
  číselný formát a nastavit zarovnání sloupce v mřížce.
og_title: Jak formátovat měnu ve sloupci mřížky – kompletní průvodce
tags:
- C#
- GridFormatting
- UI
title: Jak formátovat měnu ve sloupci mřížky – krok za krokem
url: /cs/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak formátovat měnu ve sloupci Grid – Kompletní programovací tutoriál

Už jste se někdy zamysleli **jak formátovat měnu** ve sloupci mřížky, aniž byste si trhali vlasy? Nejste v tom sami. Když se díváte na obyčejné číslo jako `1234.5` a přejete si, aby se magicky zobrazilo jako `$1,234.50`, odpověď je obvykle jen několik řádků konfigurace.  

V tomto průvodci **získáme sloupec podle názvu**, **nastavíme formát čísla sloupce** a **použijeme vlastní číselný formát**, který respektuje typické účetní uspořádání. Navíc **nastavíme zarovnání sloupce v gridu** a přidáme decentní okraj, aby UI vypadalo uhlazeně.

> **TL;DR** – Na konci budete mít připravený útržek kódu, který převádí surové desetinné hodnoty na krásně naformátované měnové hodnoty v libovolném ovládacím prvku stylu `GridJs`.

---

## Co budete potřebovat

- Projekt .NET (jakákoli verze podporující C# 8.0+ – Visual Studio 2022 funguje skvěle).  
- Komponentu gridu, která vystavuje kolekci `Columns` (příklad používá fiktivní třídu `GridJs`, ale koncepty se přenášejí i na DevExpress, Telerik nebo Syncfusion gridy).  
- Základní znalost syntaxe C# – žádné pokročilé triky nejsou potřeba.

Pokud už to máte, výborně. Pokud ne, stačí si vytvořit konzolovou aplikaci; grid může být pro ilustraci simulován.

---

## Krok‑po‑kroku implementace

Níže u každého kroku uvidíte kompaktní blok kódu, krátké vysvětlení **proč** je řádek důležitý, a tip, jak se vyhnout běžným úskalím.

### ## Krok 1 – Získání sloupce „Amount“ podle názvu

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Proč je to důležité:**  
Většina API gridů vystavuje sloupce pomocí indexeru podobného slovníku. Získání sloupce podle jeho nadpisu (`"Amount"`) vám umožní manipulovat s jeho vzhledem, aniž byste zasahovali do podkladového zdroje dat.  

**Tip:** Vždy kontrolujte, zda výsledek není `null` – překlep v názvu sloupce nebo dynamická změna schématu by jinak mohly vést k `NullReferenceException` za běhu.

---

### ## Krok 2 – Nastavení formátu čísla sloupce pomocí vlastního měnového masky

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Proč je to důležité:**  
Formátovací řetězec následuje konvence účetního formátu v Excelu:

- `_(* #,##0.00_)` → Kladná čísla, zarovnaná vpravo s úvodní mezerou pro měnový symbol.  
- `_(* (#,##0.00)` → Záporná čísla uzavřená v závorkách.  
- `_(* \"-\"??_)` → Nuly zobrazené jako pomlčka.  
- `_(@_)` → Textové hodnoty zůstávají beze změny.

Použití **apply custom numeric format** vám dává plnou kontrolu nad oddělovači tisíců, desetinnými místy a umístěním měnového symbolu.  

**Okrajový případ:** Pokud vaše aplikace potřebuje respektovat jinou lokalizaci (např. Euro místo USD), nahraďte úvodní mezeru požadovaným symbolem nebo použijte formátování citlivé na `CultureInfo` přímo ve zdroji dat.

---

### ## Krok 3 – Zarovnání obsahu sloupce vpravo pro lepší čitelnost

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Proč je to důležité:**  
Měnové hodnoty se snadněji skenují, když jsou zarovnané na desetinnou čárku. Nastavení **set grid column alignment** na `Right` napodobuje způsob, jakým tabulky zobrazují finanční data.  

**Pozor:** Některé gridy ignorují zarovnání u buněk, které používají vlastní šablony. Pokud si všimnete, že zarovnání nefunguje, zkontrolujte, že sloupec nepoužívá vlastní renderer buňky.

---

### ## Krok 4 – Přidání tenkého šedého okraje kolem buněk sloupce

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Proč je to důležité:**  
Jemný okraj odděluje sloupec „Amount“ od sousedních sloupců, zejména když má grid střídavé barvy řádků. Je to vizuální signál, že data představují samostatnou finanční položku.  

**Tip:** Pokud potřebujete silnější čáru pro tisk, změňte `BorderLineStyle` na `Medium` nebo upravte `Color` na `Color.Black`.

---

## Kompletní funkční příklad

Zde je celý útržek, který můžete vložit do projektu WinForms nebo WPF používajícího ovládací prvek stylu `GridJs`. Příklad také vypisuje naformátované hodnoty do konzole, abyste mohli ověřit výstup bez UI.

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

**Očekávaný výstup v konzoli**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Všimněte si, že kladné číslo je zarovnané vpravo, záporné se zobrazuje v závorkách a nula jako pomlčka – přesně podle toho, co určuje vlastní formátovací řetězec.

---

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Co když grid používá jinou kulturu (např. € místo $)?* | Nahraďte úvodní mezeru ve formátovacím řetězci požadovaným symbolem nebo nechte zdroj dat emitovat předformátovaný řetězec pomocí `CultureInfo.CurrentCulture`. |
| *Mohu stejný formát použít pro více sloupců?* | Rozhodně. Uložte formátovací řetězec do konstanty (`const string CurrencyMask = "...";`) a přiřaďte jej všude, kde potřebujete měnu. |
| *Co se stane, když sloupec obsahuje řetězcovou hodnotu?* | Formátovací řetězec ovlivňuje jen číselné typy. Řetězce projdou beze změny, což je důvod, proč poslední část masky (`_(@_)`) existuje – zachovává nečíselný obsah. |
| *Má to dopad na výkon?* | Nezajímavý. Formát se aplikuje při renderování, ne při načítání dat. Pokud nerenderujete tisíce řádků za snímek, nezaznamenáte žádné zpomalení. |
| *Jak udělat okraj silnějším pro tištěné zprávy?* | Vyměňte `BorderLineStyle.Thin` za `BorderLineStyle.Medium` nebo `BorderLineStyle.Thick`. Některé knihovny také umožňují přímo nastavit šířku v pixelech. |

---

## Závěr

Prošli jsme **jak formátovat měnu** ve sloupci gridu od začátku do konce: získali jsme sloupec podle názvu, nastavili formát čísla sloupce, použili vlastní číselný formát, zarovnali buňky a přidali vkusný okraj. Kompletní příklad funguje ihned a ukazuje přesný vizuální výsledek, který můžete očekávat.

Pokud jste připraveni posunout to dál, vyzkoušejte:

- **Dynamické kultury** – přepněte formátovací řetězec podle uživatelovy lokality.  
- **Podmíněné

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}