---
category: general
date: 2026-10-01
description: Naučte se, jak přidat vlastní vlastnosti do sešitu Excel pomocí Aspose.Cells.
  Tento průvodce také ukazuje, jak přidat ID projektu a číst vlastní vlastnosti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: cs
lastmod: 2026-10-01
og_description: Přidejte vlastní vlastnosti do sešitu Excel pomocí Aspose.Cells. Postupujte
  podle tohoto kompletního tutoriálu, abyste přidali ID projektu, nastavili informace
  o recenzentovi a programově četli vlastní vlastnosti.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Přidejte vlastní vlastnosti do sešitu Excel – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak přidat vlastní vlastnosti do sešitu Excel
url: /cs/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat vlastní vlastnosti do sešitu Excel

Pokud potřebujete **přidat vlastní vlastnosti** do sešitu Excel, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells pro .NET. Také se naučíte, jak přidat ID projektu, nastavit jméno recenzenta a později **číst vlastní vlastnosti** ze souboru.

Práce s vlastními metadaty vám umožní vložit obchodně specifické informace přímo do tabulky, což usnadňuje sledování vlastnictví, verze nebo jakéhokoli jiného kontextu bez nutnosti udržovat samostatnou databázi. Níže uvedené kroky pokrývají kompletní end‑to‑end workflow, od vytvoření sešitu až po uložení nových vlastností.

## Požadavky

* .NET 6.0 nebo novější nainstalováno  
* Platná licence Aspose.Cells pro .NET (nebo bezplatná zkušební verze)  
* Visual Studio 2022 (nebo jakékoli C# IDE)

Kromě `Aspose.Cells` nejsou vyžadovány žádné další balíčky NuGet.

## Krok 1: Nastavení projektu a import jmenných prostorů

Vytvořte novou konzolovou aplikaci a přidejte odkaz na Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Jmenný prostor `Aspose.Cells` obsahuje třídy `Workbook`, `Worksheet` a `CustomPropertyCollection`, které budeme používat.

## Krok 2: Načtení existujícího sešitu (nebo vytvoření nového)

Můžete začít s existujícím souborem `.xlsb` nebo vygenerovat nový sešit. Níže uvedený příklad načte soubor pojmenovaný **Data.xlsb** umístěný ve složce `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Pokud soubor neexistuje, nahraďte kód `new Workbook();` pro vytvoření prázdného sešitu.

## Krok 3: Přidání vlastních vlastností do první listu

Hlavní operací je **přidat vlastní vlastnosti** do listu. Aspose.Cells ukládá vlastní vlastnosti do kolekce, která se chová jako slovník.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Důvod, proč používáme `CustomProperties.Add` místo `CustomProperties["Name"] = value`, je ten, že metoda `Add` vytvoří položku, pokud neexistuje, a zaručuje, že je uložena správná datová typ. Tento přístup zabraňuje neúmyslným nesouladům typů, které by mohly později při čtení hodnot způsobit chyby za běhu.

## Krok 4: Uložení sešitu s novými vlastnostmi

Po vložení metadat uložte změny do nového souboru, aby originál zůstal nedotčený.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

V tomto okamžiku Excel soubor obsahuje vlastní metadata, která jste definovali. Vlastnosti můžete ověřit pomocí kroků v následující sekci.

## Krok 5: Čtení vlastních vlastností ze sešitu

Čtení **excel custom properties** následuje stejný vzor kolekce. Tento úryvek ukazuje, jak získat hodnoty, které jsme právě uložili.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` indexer vrací objekt `CustomProperty`; přístup k jeho vlastnosti `Value` vám poskytne uložená data v jejich původním typu. Kontrola na `null` před přetypováním zabraňuje `NullReferenceException`, pokud vlastnost chybí.

### Očekávaný výstup v konzoli

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Časové razítko bude odrážet přesný okamžik, kdy jste v kroku 3 zavolali `Add`.

## Pro tip: Aktualizace existující vlastní vlastnosti

Pokud potřebujete později **přidat vlastní** informace (například změnit recenzenta), použijte setter `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Tento vzor zajišťuje, že vlastnost je buď aktualizována, nebo vytvořena, což je užitečné v iterativních pracovních postupech, jako je automatizovaná generace reportů.

## Krok 6: Ověření vlastností v Excelu (volitelné)

Vlastní vlastnosti můžete také zobrazit přímo v Excelu:

1. Otevřete uložený soubor `DataWithProps.xlsb` v Microsoft Excel.  
2. Přejděte na **File → Info → Properties → Advanced Properties**.  
3. Vyberte kartu **Custom**.

Uvidíte položky `ProjectId`, `Reviewer` a `CreatedOn` uvedené s jejich odpovídajícími hodnotami.

## Kompletní funkční příklad

Níže je kompletní, samostatný program, který kombinuje všechny předchozí úryvky. Zkopírujte jej do `Program.cs` a spusťte; konzole zobrazí načtené hodnoty.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Spuštěním tohoto programu získáte výstup v konzoli zobrazený dříve a vytvoří se soubor `DataWithProps.xlsb` obsahující vložená metadata.

## Časté otázky a okrajové případy

| Question | Answer |
|---|---|
| **Mohu ukládat ne‑primitivní typy?** | Aspose.Cells podporuje `string`, `int`, `double`, `DateTime` a `bool`. Pro složité objekty je nejprve serializujte do JSON nebo XML a uložte jako řetězec. |
| **Co když je sešit chráněn heslem?** | Otevřete sešit s heslem (`new Workbook(path, password)`) před přístupem k `CustomProperties`. Vlastnosti jsou i po dešifrování stále přístupné. |
| **Přežijí vlastní vlastnosti konverzi formátu?** | Při ukládání do jiného formátu (např. `.xlsx`) Aspose.Cells zachová vlastní vlastnosti, pokud cílový formát podporuje jejich ukládání. |
| **Jak smazat vlastní vlastnost?** | Použijte `worksheet.CustomProperties.Remove("PropertyName");`. Tím se položka z kolekce odstraní. |

## Další kroky

Nyní, když víte, jak **přidat vlastní vlastnosti**, můžete prozkoumat související témata, jako například:

* **excel custom properties** pro verzování dokumentů  
* **read custom properties** z více listů v jednom sešitu  
* Použití **Aspose.Cells** k vytvoření kontingenčních tabulek, které odkazují na vlastní metadata  
* Export sešitu do PDF při zachování vlastních vlastností  

Experimentujte s různými datovými typy, kombinujte vlastní vlastnosti s komentáři buněk nebo integrujte metadata do většího systému pro správu dokumentů.

**Připraveni automatizovat vaše Excel reportování?** Přidejte výše uvedený kód do svého projektu, upravte názvy vlastností tak, aby odpovídaly vašim obchodním potřebám, a budete mít sešit s vlastními popisy připravený pro následné zpracování.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit Excel sešit – Přidat vlastní vlastnosti a uložit jako XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Jak získat vlastní vlastnosti dokumentu v Excelu pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Mistrovství v Excel vlastních vlastnostech pomocí Aspose.Cells .NET pro pokročilou správu dat](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}