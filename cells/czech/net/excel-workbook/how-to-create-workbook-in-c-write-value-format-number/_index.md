---
category: general
date: 2026-03-01
description: Jak rychle vytvořit sešit v C# – naučte se zapisovat hodnotu do buňky,
  nastavit formát čísla buňky a formátovat číslo buňky pomocí jednoduchých kroků.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: cs
og_description: Jak vytvořit sešit v C#? Tento průvodce vám ukáže, jak zapsat hodnotu
  do buňky, nastavit formát čísla buňky a formátovat číslo buňky pomocí jen několika
  řádků kódu.
og_title: Jak vytvořit sešit v C# – Zapsat hodnotu a formátovat číslo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak vytvořit sešit v C# – zapisovat hodnotu a formátovat číslo
url: /cs/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit sešit v C# – zápis hodnoty a formátování čísla

Vytvoření sešitu v C# je běžný úkol, když potřebujete generovat soubory Excel za běhu. V tomto průvodci vás provedeme zápisem hodnoty do buňky a formátováním čísla v buňce, aby výsledný list vypadal profesionálně.

Pokud jste někdy zírali na prázdný tabulkový list a přemýšleli, proč se čísla zobrazují s příliš mnoha desetinnými místy, nejste sami. Probereme vše od inicializace objektu sešitu po nastavení vlastního formátu čísla a přidáme několik tipů pro okrajové případy, na které můžete později narazit.

## Co se naučíte

- **Inicializovat** novou instanci `Workbook`.  
- **Zapsat hodnotu do buňky** pomocí metody `PutValue`.  
- **Nastavit formát čísla buňky** pomocí objektu `Style`, aby se zobrazovaly čisté dvě číslice.  
- Ověřit výsledek načtením buňky zpět nebo otevřením souboru v Excelu.  

Nejsou potřeba žádné externí knihovny mimo standardní Aspose.Cells (nebo jakékoli podobné API) a kód běží na .NET 6+ bez další konfigurace.

---

## Jak vytvořit sešit – inicializace objektu

Nejprve potřebujete objekt sešitu, který bude obsahovat vaše listy. `Workbook` představuje celý soubor Excel, zatímco každý `Worksheet` je jednotlivá karta.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Proč je to důležité:* Vytvoření sešitu alokuje interní struktury, které později obsahují řádky, sloupce a formátování. Bez tohoto objektu nemáte kam zapisovat hodnotu do buňky.

> **Tip:** Pokud chcete pracovat s existujícím souborem, nahraďte `new Workbook()` za `new Workbook("template.xlsx")`, abyste načetli šablonu a zachovali její styly.

## Zapsat hodnotu do buňky

Nyní, když máme sešit, vložíme číslo do buňky **A1** prvního listu.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Proč používáme `PutValue`*: Tato metoda automaticky detekuje datový typ, takže nemusíte ručně přetypovávat nebo konvertovat. Také respektuje existující styl buňky, což je užitečné, když později **nastavíte formát čísla buňky**.

### Rychlá kontrola

Pokud buňku načtete zpět, uvidíte surovou hodnotu:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

To je číslo před aplikací jakéhokoli formátování.

## Nastavit formát čísla buňky

Zobrazování surového typu double s mnoha desetinnými místy není vždy uživatelsky přívětivé. Omezme ho na dvě významné číslice.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

Vlastnost `Number` odpovídá vestavěným ID formátů v Excelu. `2` znamená „Číslo se dvěma desetinnými místy“. Pokud potřebujete jiný formát – například měnu nebo datum – použijete jiné ID nebo vlastní formátovací řetězec.

### Alternativa: Vlastní formátovací řetězec

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Proč zvolit vlastní styl?* Dává vám plnou kontrolu, zejména když vestavěná ID neodpovídají vašim regionálním nastavením.

## Ověřit výstup (volitelné, ale doporučené)

Po aplikaci stylu můžete sešit uložit a otevřít v Excelu, abyste potvrdili vzhled.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Měli byste vidět **123.46** v buňce A1 – přesně dvě desetinná místa, díky nastavenému formátu.

---

### Kompletní funkční příklad

Spojením všech částí získáte samostatný program, který můžete zkopírovat a vložit do konzolové aplikace.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Očekávaný výstup po spuštění programu:**

```
Cell A1 shows: 123.46
```

Otevřete `FormattedWorkbook.xlsx` v Excelu a uvidíte stejnou formátovanou hodnotu.

---

## Běžné varianty a okrajové případy

### 1. Různé formáty čísel

| Cíl | ID formátu | Ukázka kódu |
|------|-----------|--------------|
| Měna (dvě desetinná místa) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Procenta (žádné desetinné místo) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Vědecká notace | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Pokud žádné vestavěné ID nevyhovuje, vraťte se k vlastnímu řetězci, jak bylo ukázáno výše.

### 2. Regionální oddělovače desetinných míst

Některé lokály používají čárky jako desetinný oddělovač. Můžete vynutit formát citlivý na kulturu:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Zápis textu místo čísel

Když potřebujete **zapsat buňku** s řetězcem, stačí předat řetězec metodě `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Formát čísla není potřeba, ale stále můžete aplikovat styl písma.

### 4. Velké datové sady

Pokud naplňujete tisíce řádků, hromadné vkládání (`Cells.ImportArray`) je rychlejší než cyklické volání `PutValue`. Přístup k formátování zůstává stejný; stačí aplikovat styl na rozsah:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Často kladené otázky

**Q: Funguje to s .NET Core?**  
A: Rozhodně. Aspose.Cells podporuje .NET Standard 2.0 a novější, takže můžete cílit na .NET 5, .NET 6 nebo .NET 7 bez změn.

**Q: Co když potřebuji více než dvě desetinná místa?**  
A: Změňte vlastnost `Number` na odpovídající vestavěné ID (např. `3` pro tři desetinná místa) nebo upravte vlastní formátovací řetězec (`"#,##0.000"`).

**Q: Můžu aplikovat formát na celý sloupec najednou?**  
A: Ano. Použijte `Cells["A:A"]` pro získání celého sloupce a poté `SetStyle`.

---

## Závěr

Nyní víte, **jak vytvořit sešit** v C#, **zapsat hodnotu do buňky** a **nastavit formát čísla buňky**, aby se čísla zobrazovala přesně tak, jak chcete. Ovládnutím těchto základů budete schopni generovat profesionálně vypadající Excelové reporty, faktury nebo exporty dat s minimálním úsilím.

Dále můžete prozkoumat **formátování čísel** pro data, procenta nebo podmíněné formátování – vše staví na stejných principech, které jsme zde probírali. Prohlédněte si dokumentaci Aspose.Cells pro pokročilejší možnosti stylování nebo zkuste kombinovat více listů v jednom sešitu pro bohatší reporty.

Šťastné programování a pamatujte: dobře formátovaný tabulkový list je jen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}