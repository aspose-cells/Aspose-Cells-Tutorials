---
category: general
date: 2026-03-27
description: Jak svázat data v C# pomocí Aspose.Cells – naučte se uložit sešit jako
  XLSX, přidat graf a exportovat Excel s grafem během několika minut.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: cs
og_description: Jak svázat data v C# s Aspose.Cells. Tento průvodce vám ukáže, jak
  uložit sešit jako XLSX, přidat graf a exportovat Excel s grafem.
og_title: Jak svázat data v C# – Vytvořit Excel sešit
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak vázat data v C# – Vytvořit Excel sešit
url: /cs/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak svázat data v C# – Vytvořit Excel sešit

Už jste se někdy zamysleli **jak svázat data** s grafem v C# bez toho, abyste si trhali vlasy? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují programově generovat Excel soubory, které skutečně *vypadají* jako ty, jež by vytvořili ručně.  

V tomto tutoriálu projdeme kompletní, připravený‑k‑spuštění příklad, který vytvoří Excel sešit, naplní jej daty, sváže tato data s Waterfall grafem a nakonec soubor uloží jako `.xlsx`. Na konci budete přesně vědět, jak **uložit sešit jako XLSX**, **přidat graf** do listu a jak **exportovat Excel s grafem** pro následné reportování.

> **Požadavky** – Potřebujete Aspose.Cells pro .NET (volná zkušební verze stačí) a vývojové prostředí .NET, například Visual Studio 2022. Žádné další NuGet balíčky nejsou vyžadovány.

---

## Co tento průvodce pokrývá

- **Create Excel workbook C#** – vytvoření nového `Workbook` a listu.  
- **How to bind data** – mapování číselných sérií a popisků kategorií na zdroj dat grafu.  
- **How to add chart** – vložení Waterfall grafu a nastavení jeho názvu.  
- **Save workbook as XLSX** – uložení souboru na disk, aby jej mohl otevřít kdokoli v Excelu.  
- **Export Excel with chart** – finální produkt je plně funkční sešit, který můžete sdílet.

Pokud ovládáte základní syntaxi C#, bude pro vás tato ukázka hračka. Pojďme na to.

---

## Krok 1: Vytvořit Excel sešit v C#  

Nejprve potřebujeme objekt sešitu, se kterým budeme pracovat. Třída `Workbook` je jako prázdný zápisník, který později naplníte listy (worksheets) a obsahem.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Tip:** Pokud potřebujete více listů, stačí zavolat `workbook.Worksheets.Add()` a uchovat si odkaz na každý nový `Worksheet`.

---

## Krok 2: Naplnit list kategoriemi a hodnotami  

Nyní vytvoříme data ve stylu **create excel workbook c#**. Příklad používá klasický Waterfall scénář: start, revenue, cost, profit a end.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Proč dáváme `0` pro „Start“ a „Profit“? Ve Waterfall grafu tyto nuly fungují jako *spojovací* body, které zajistí správný vizuální tok. Pokud je vynecháte, graf bude vypadat poškozeně.

---

## Krok 3: Jak přidat graf – Vložit Waterfall graf  

S připravenými daty je čas na **how to add chart**. Aspose.Cells to usnadňuje voláním `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Souřadnice `(7,0,25,10)` určují levý‑horní a pravý‑dolní buňku ohraničujícího rámečku grafu. Upravit je můžete podle potřeby rozvržení.

---

## Krok 4: Jak svázat data – Připojit řady a kategorie  

Zde je jádro tutoriálu: **how to bind data** k grafu. Metoda `NSeries.Add` přijímá rozsah Y‑hodnot, zatímco `CategoryData` ukazuje na popisky osy X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Všimněte si, že odkazujeme na stejné buňky, které jsme naplnili dříve (`A2:A6` pro kategorie, `B2:B6` pro částky). Pokud změníte rozložení dat, stačí aktualizovat tyto rozsahy.

---

## Krok 5: Uložit sešit jako XLSX – Persistovat soubor  

Nakonec **save workbook as XLSX**. Metoda `Save` automaticky zvolí správný formát podle přípony souboru.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Když otevřete `WaterfallChart.xlsx` v Excelu, uvidíte pěkně vykreslený Waterfall graf, který odráží zadaná data. Tím je část **export excel with chart** dokončena.

---

## Očekávaný výsledek  

- **Excel soubor:** `WaterfallChart.xlsx` umístěný ve složce, kterou jste zadali.  
- **Rozložení listu:** Sloupec A obsahuje kategorie, sloupec B částky a graf je umístěn pod tabulkou.  
- **Vzhled grafu:** Waterfall graf s názvem „Quarterly Waterfall“ a pěti sloupci představujícími Start, Revenue, Cost, Profit a End.  

![jak svázat data waterfall graf příklad](waterfall_chart.png "Waterfall graf vygenerovaný pomocí Aspose.Cells")

*Alt text obrázku obsahuje hlavní klíčové slovo, což pomáhá jak SEO, tak AI citacím.*

---

## Často kladené otázky a okrajové případy  

### Co když je můj zdroj dat dynamický?  
Nahraďte statické pole smyčkou, která čte z databáze nebo API. Dokud zapíšete hodnoty do stejného rozsahu buněk, kód pro svázání zůstane beze změny.

### Můžu změnit typ grafu?  
Samozřejmě. Vyměňte `ChartType.Waterfall` za `ChartType.Column`, `ChartType.Line` apod. Jen nezapomeňte upravit data řady, pokud nový typ grafu vyžaduje jinou strukturu.

### Jak nastavit barvy grafu?  
Použijte `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (nebo libovolnou `System.Drawing.Color`). To je užitečné, když chcete, aby sloupec „Profit“ vynikl.

### Co když potřebuji exportovat do PDF místo XLSX?  
Zavolejte `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Graf bude v PDF automaticky vykreslen.

---

## Tipy pro produkčně připravený kód  

- **Uvolňovat objekty** – Zabalte `Workbook` do `using` bloku, pokud používáte .NET Core, aby se prostředky uvolnily co nejdříve.  
- **Zpracování cest** – Použijte `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")`, abyste se vyhnuli ručnímu zadávání oddělovačů.  
- **Ošetření chyb** – Zachyťte `Exception` kolem `Save`, abyste včas odhalili problémy s oprávněním nebo nedostatkem místa na disku.  
- **Kontrola verze** – Aspose.Cells 23.10+ přinesl vylepšenou podporu Waterfall grafů; ujistěte se, že používáte aktuální verzi pro nejlepší výsledky.

---

## Závěr  

Nyní máte kompletní, end‑to‑end příklad, který demonstruje **how to bind data** v C#, **create excel workbook c#**, **how to add chart**, **save workbook as xlsx** a **export excel with chart**. Kód můžete vložit do libovolného .NET projektu a koncepty se snadno rozšíří na větší datové sady a různé typy grafů.

Jste připraveni na další krok? Zkuste přidat více sérií, experimentovat se stacked grafy nebo automatizovat generování měsíčních reportů, které se odešlou stakeholderům e‑mailem. Možnosti jsou neomezené, jakmile ovládnete základy automatizace Excelu s Aspose.Cells.

Šťastné kódování a ať se vaše tabulky vždy vykreslují perfektně!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}