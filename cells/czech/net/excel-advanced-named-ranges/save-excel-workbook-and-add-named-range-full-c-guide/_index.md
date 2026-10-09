---
category: general
date: 2026-06-27
description: Uložte sešit Excel v C# a přidejte pojmenovaný rozsah. Naučte se vytvářet
  definované názvy a používat vzorce s definovanými názvy pomocí Aspose.Cells.
draft: false
keywords:
- save excel workbook
- add named range
- create defined name
- named range excel
- use defined name formulas
language: cs
og_description: Uložte Excel sešit v C# a naučte se, jak přidat pojmenovaný rozsah,
  vytvořit definovaný název a používat vzorce s definovanými názvy pomocí Aspose.Cells.
og_title: Uložení sešitu Excel a přidání pojmenovaného rozsahu – C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel Workbook in C# while adding a named range. Learn to create
    defined name and use defined name formulas with Aspose.Cells.
  headline: Save Excel Workbook and Add Named Range – Full C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Uložení sešitu Excel a přidání pojmenovaného rozsahu – kompletní průvodce C#
url: /cs/net/excel-advanced-named-ranges/save-excel-workbook-and-add-named-range-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložení Excel sešitu a přidání pojmenovaného rozsahu – Kompletní průvodce v C#

Už jste někdy potřebovali **uložit Excel sešit** po rozptýlení několika vlastních názvů po listu? Nejste v tom sami. V mnoha nástrojích pro reportování nebo aplikacích řízených daty nakonec vytvoříme pojmenovaný rozsah, odkazujeme na něj ve vzorcích a nakonec změny uložíme na disk.  

V tomto tutoriálu projdeme přesně to: načteme soubor *.xlsx*, **přidáme pojmenovaný rozsah**, **vytvoříme definovaný název**, použijeme ten název ve vzorci a nakonec **uložíme Excel sešit** s aktualizacemi. Žádné zbytečnosti — pouze kompletní, spustitelný příklad, který můžete vložit do libovolného .NET projektu.

> **Pro tip:** Aspose.Cells funguje bez nutnosti instalace Microsoft Office, což ho činí ideálním pro automatizaci na serveru.

## Co budete potřebovat

- .NET 6 (nebo jakékoli aktuální .NET runtime)  
- NuGet balíček Aspose.Cells pro .NET (`Install-Package Aspose.Cells`)  
- Ukázkový soubor `input.xlsx` (libovolný sešit stačí, ale ujistěte se, že Sheet1 má data v **A1**)  
- Váš oblíbený IDE (Visual Studio, Rider, VS Code…)

To je vše. Pokud máte tyto věci, můžeme rovnou přejít k kódu.

## Krok 1: Nastavení projektu

Vytvořte konzolovou aplikaci a přidejte Aspose.Cells:

```bash
dotnet new console -n ExcelNamedRangeDemo
cd ExcelNamedRangeDemo
dotnet add package Aspose.Cells
```

Otevřete `Program.cs`; uvidíte výchozí metodu `Main`. Nahraďte její obsah kompletním pracovním postupem v následujících krocích.

## Krok 2: Načtení sešitu

Načtení sešitu je první věc, kterou musíte udělat, než můžete **přidat pojmenovaný rozsah**. Představte si to jako otevření knihy, než začnete psát poznámky na okrajích.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");
```

> **Proč je to důležité:** Objekt `Workbook` představuje celý Excel soubor v paměti. Bez něj nemůžete manipulovat s buňkami, názvy ani vzorci.

## Krok 3: Vytvoření definovaného názvu (přidání pojmenovaného rozsahu)

Nyní skutečně **vytvoříme definovaný název**, který ukazuje na konkrétní buňku nebo oblast. V uživatelském rozhraní Excelu byste šli na *Formulas → Name Manager*; zde to uděláme programově.

```csharp
        // Step 3: Add a defined name that points to cell A1 on Sheet1
        // This name can be used in formulas throughout the workbook
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");
```

> **Vysvětlení:** `wb.Names.Add` zaregistruje *pojmenovaný rozsah* s názvem **Sales**. Řetězec `=Sheet1!$A$1` je referenční vzorec — přesně to, co byste zadali v dialogu Správce názvů.

## Krok 4: Použití definovaného názvu ve vzorci

Mít název je hezké, ale obvykle ho chcete **použít ve vzorcích** někde. Napíšeme jednoduchý vzorec, který přičte 10 k hodnotě v **Sales** a výsledek vloží do **B1**.

```csharp
        // Step 4: Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");
```

Když sešit přepočítá, `B1` zobrazí to, co je v `A1`, plus deset. To demonstruje sílu *named range excel* — můžete změnit podkladovou referenci jednou a všechny vzorce se automaticky aktualizují.

## Krok 5: Uložení upraveného sešitu

Nakonec **uložíme Excel sešit** do nového souboru, aby změny přetrvaly. Můžete přepsat originál nebo zapsat na čerstvé místo; zde si ponecháme obojí.

```csharp
        // Step 5: Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

Spuštěním programu získáte výstup v konzoli podobný tomuto:

```
Workbook loaded successfully.
Defined name 'Sales' added (named range Excel).
Formula '=Sales + 10' written to B1.
Workbook saved as 'YOUR_DIRECTORY\output.xlsx'.
```

Otevřete `output.xlsx` a uvidíte, že **B1** nyní obsahuje `=Sales + 10`, zatímco **A1** zůstává beze změny. Název **Sales** se objeví pod *Formulas → Name Manager*.

## Okrajové případy a časté otázky

| Otázka | Odpověď |
|----------|--------|
| **Co když název listu obsahuje mezery?** | Obalte jej jednoduchými uvozovkami: `= 'My Sheet'!$A$1`. |
| **Mohu pojmenovat rozsah na více buněk?** | Určitě — při volání `wb.Names.Add` použijte `=Sheet1!$A$1:$A$5`. |
| **Musím přepočítávat ručně?** | Aspose.Cells přepočítává automaticky při čtení hodnoty buňky. Pokud potřebujete kompletní obnovení, zavolejte `wb.CalculateFormula()`. |
| **Co s existujícími názvy?** | `wb.Names.Add` vyvolá výjimku, pokud název již existuje. Použijte `wb.Names["Sales"]?.RefersTo = "...";` pro aktualizaci. |

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní, připravený program ke zkopírování. Nahraďte `YOUR_DIRECTORY` skutečnou složkou na vašem počítači.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");

        // Add a defined name (named range) that points to cell A1 on Sheet1
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");

        // Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");

        // Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

**Očekávaný výsledek:**  

- `output.xlsx` obsahuje nový název **Sales**, který ukazuje na `Sheet1!A1`.  
- Buňka **B1** zobrazuje hodnotu **A1** plus `10`.  
- Soubor je plně kompatibilní s Excelem, Google Sheets nebo jakoukoliv knihovnou, která rozumí pojmenovaným rozsahům.

## Závěr

Nyní víte, jak **uložit Excel sešit**, **přidat pojmenovaný rozsah**, **vytvořit definovaný název** a **použít definované názvy ve vzorcích** pomocí Aspose.Cells v C#. Kroky jsou jednoduché: načíst, pojmenovat, odkazovat a uložit.  

Odtud můžete rozšířit na:  

- Vytvořit dynamické rozsahy pomocí funkcí `OFFSET`.  
- Použít stejný název napříč více listy (`Scope = Worksheet`).  
- Generovat tisíce pojmenovaných rozsahů pro složité finanční modely.

Vyzkoušejte to, upravte referenci nebo použijte název v kontingenční tabulce — vaše možnosti automatizace jsou prakticky neomezené.

---

![Uložení Excel sešitu diagram](excel-workflow.png){: .align-center alt="Uložení Excel sešitu diagram"}

*Připravený automatizovat své Excel reporty? Zanechte komentář, podělte se o úpravy nebo forkni repozitář na GitHubu. Šťastné kódování!*

## Co byste se měli naučit dál?

- [Vytvořit a uložit Excel sešit Aspose Cells .NET](/cells/english/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Jak vytvořit a uložit Excel sešit jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Vytvořit a uložit Excel sešit PDF Aspnet Aspose Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}