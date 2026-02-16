---
category: general
date: 2026-02-15
description: Vytvořte nový sešit Excel a naučte se používat funkci EXPAND, rozšířit
  posloupnost a vypočítat kotangens. Také se podívejte, jak uložit sešit do souboru.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: cs
og_description: Vytvořte nový sešit Excelu pomocí C#. Naučte se používat funkci EXPAND,
  rozšířit sekvenci, vypočítat kotangens a uložit sešit do souboru.
og_title: Vytvořte nový sešit Excel v C# – kompletní programovací průvodce
tags:
- C#
- Aspose.Cells
- Excel automation
title: Vytvoření nového sešitu Excel v C# – krok za krokem
url: /cs/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

keep all shortcodes unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu Excel v C# – Kompletní programovací průvodce

Už jste někdy potřebovali **create new Excel workbook** z kódu a nebyli jste si jisti, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tuto překážku při automatizaci reportů nebo tvorbě datových pipeline. V tomto tutoriálu vám přesně ukážeme, jak vytvořit nový sešit Excel, napsat několik užitečných vzorců a poté **save workbook to file** pro pozdější kontrolu.  

Také se ponoříme do detailů funkce `EXPAND`, ukážeme **how to use expand**, jak proměnit malou sekvenci na velký blok, vysvětlíme **how to expand sequence** v praxi a nakonec odhalíme **how to calculate cotangent** přímo v Excelu. Na konci budete mít spustitelný C# program, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- **Aspose.Cells for .NET** (free trial nebo licencovaná verze) – knihovna, která nám umožňuje manipulovat s Excelem bez nainstalovaného Office.  
- **.NET 6+** (nebo .NET Framework 4.6+).  
- Skromné IDE jako Visual Studio 2022, VS Code nebo Rider.  

Žádné další NuGet balíčky nejsou potřeba kromě `Aspose.Cells`. Pokud jej ještě nemáte, spusťte:

```bash
dotnet add package Aspose.Cells
```

To je vše—nic dalšího k nastavení.

## Krok 1: Vytvoření nového sešitu Excel

Prvním krokem je vytvořit instanci objektu `Workbook`. Představte si ho jako prázdné plátno, kde budou existovat všechny listy, buňky a vzorce.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Proč je to důležité:** Vytvoření sešitu v paměti znamená, že se na disk nedotýkáme, dokud výslovně nerozhodnete **save workbook to file**. To udržuje operaci rychlou a umožňuje řetězit další úpravy bez I/O zátěže.

## Krok 2: Jak použít EXPAND k rozšíření sekvence

`EXPAND` je novější funkce Excelu, která vezme menší pole a roztáhne jej na definovanou velikost. V našem příkladu začínáme třířádkovou vertikální sekvencí a proměníme ji na blok 5 × 5.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Vysvětlení:** `SEQUENCE(3)` vytváří `{1;2;3}` (vertikální pole). `EXPAND(...,5,5)` říká Excelu, aby opakoval toto pole, dokud nevyplní obdélník 5 řádků a 5 sloupců, počínaje buňkou A1. Výsledkem je matice, kde každá sloupec opakuje původní tři čísla, a poslední dva řádky jsou prázdné, protože zdroj má jen tři řádky.

### Očekávaný výstup

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Uvidíte stejný vzor rozprostřený po rozsahu, jakmile otevřete sešit v Excelu.

## Krok 3: Jak vypočítat kotangens v Excelu

Většina lidí zná `SIN`, `COS` a `TAN`, ale `COT` je praktická zkratka pro reciprokou hodnotu tangentu. Zde je návod, jak získat kotangens 45° (což je 1) pomocí radiánů.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Proč použít COT?** Přímé volání `COT` eliminuje nutnost dalšího dělení, které byste potřebovali u `1/TAN(...)`, což činí vzorec přehlednějším a mírně rychlejším pro velké listy.

## Krok 4: Vyhodnocení všech vzorců

Aspose.Cells automaticky nevyhodnocuje vzorce, pokud mu to neřeknete. Metoda `CalculateFormula` vynutí úplné vyhodnocení, takže výsledné hodnoty jsou uloženy v buňkách.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Tip:** Pokud máte mnoho náročných vzorců, můžete předat objekt `CalculationOptions` pro jemné ladění výkonu (např. povolit vícevláknové zpracování).

## Krok 5: Uložení sešitu do souboru

Nyní, když je vše připraveno, konečně **save workbook to file**. Vyberte složku, do které máte právo zápisu, a dejte souboru smysluplný název.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Co se stane na disku?** Volání `Save` zapíše kompletní balíček `.xlsx`, včetně rozprostřeného pole z `EXPAND` a vypočtené hodnoty kotangensu. Otevřete soubor v Excelu a uvidíte blok 5 × 5 začínající v A1 a číslo `1` v B1.

![Výstup Excelu zobrazující rozšířenou sekvenci a hodnotu kotangensu](excel-output.png "příklad výstupu create new excel workbook")

*Text alternativy obrázku: create new excel workbook example output*

### Rychlé ověření

1. Otevřete `output.xlsx`.  
2. Zkontrolujte, že buňky **A1:E5** obsahují opakovaný vzor 1‑2‑3.  
3. Podívejte se na **B1** – měla by zobrazovat `1`.  

Pokud vše souhlasí, gratulujeme—úspěšně jste automatizovali Excel!

## Jak rozšířit sekvenci v jiných scénářích

Ačkoliv výše uvedený příklad používá statickou `SEQUENCE(3)`, můžete ji snadno nahradit dynamickým rozsahem nebo jiným vzorcem:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Kdy to použít?**  
- Generování zástupných tabulek pro šablony.  
- Rychlé replikování řádku hlavičky napříč mnoha sloupci.  
- Vytváření mřížek heat‑map bez ručního kopírování a vkládání.

## Časté úskalí a jak se jim vyhnout

| Úskalí | Proč k tomu dochází | Řešení |
|--------|----------------------|--------|
| `#VALUE!` po `EXPAND` | Zdrojové pole není správný rozsah (např. obsahuje chyby) | Vyčistěte zdrojová data nebo je obalte funkcí `IFERROR`. |
| Kotangens vrací `#DIV/0!` pro 0° | `COT(0)` je matematicky nekonečný | Ochránit pomocí `IF(PI()/4=0,0,COT(...))`. |
| Sešit není uložen | Cesta je neplatná nebo chybí oprávnění k zápisu | Použijte `Path.GetFullPath` a ověřte, že složka existuje. |
| Vzorce nejsou vypočteny | `CalculateFormula` vynecháno | Vždy jej zavolejte před `Save`. |

## Bonus: Přidání stylování (volitelné)

Pokud chcete, aby výstup vypadal lépe, můžete po výpočtech použít jednoduchý styl:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Tento úryvek je volitelný, ale ukazuje, jak můžete zkombinovat logiku **create new Excel workbook** s formátováním v jednom kroku.

## Shrnutí

Prošli jsme celý proces:

1. **Create new Excel workbook** s Aspose.Cells.  
2. Použijte **how to use expand** k proměně malé `SEQUENCE` na matici 5 × 5.  
3. Ukázat **how to calculate cotangent** přímo v buňce.  
4. Vynutit výpočet pomocí `CalculateFormula`.  
5. **Save workbook to file** a ověřte výsledek.

Vše je samostatné, běží na jakémkoli moderním .NET runtime a vyžaduje jen jeden NuGet balíček.

## Co dál?

- **Dynamic data sources:** Načíst data z databáze a předat je do `EXPAND`.  
- **Multiple worksheets:** Procházet kolekci listů a vygenerovat kompletní zprávu.  
- **Advanced formulas:** Prozkoumat `LET`, `LAMBDA` nebo pole‑založenou podmíněnou logiku pro chytřejší tabulky.  

Neváhejte experimentovat—vyměňte argument `SEQUENCE`, vyzkoušejte různé úhly pro `COT` nebo zkombinujte s generováním grafů. Možnosti jsou neomezené, když můžete **create new Excel workbook** programově.

---

*Šťastné programování! Pokud narazíte na problémy, zanechte komentář níže nebo mi napište na Twitteru @YourHandle. Rád pomohu.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}