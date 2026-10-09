---
category: general
date: 2026-03-18
description: Naučte se generovat Excel z JSON pomocí C#, povolit duplicitní názvy
  listů, vytvořit detailní list a uložit sešit v C# během několika minut.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: cs
og_description: Generovat Excel z JSON pomocí C#. Tento průvodce ukazuje, jak povolit
  duplicitní názvy listů, vytvořit detailní list a uložit sešit v C# s Aspose.Cells.
og_title: Generovat Excel z JSON v C# – kompletní tutoriál
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Generování Excelu z JSON v C# – krok za krokem průvodce
url: /cs/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generování Excelu z JSON v C# – krok za krokem průvodce

Už jste někdy potřebovali **generovat Excel z JSON**, ale nebyli jste si jisti, která knihovna to zvládne? Nejste v tom sami. V mnoha podnikových aplikacích přijímáme data jako JSON a musíme je vložit do pěkně naformátovaných tabulek – například pro prodejní reporty, výpisy zásob nebo auditní logy. Dobrá zpráva? S enginem SmartMarker od Aspose.Cells můžete převést řetězec JSON na plnohodnotný soubor Excel během několika řádků kódu.

V tomto tutoriálu projdeme celý proces: od přípravy JSON payloadu, přes konfiguraci SmartMarkeru pro **povolení duplicitních názvů listů**, vytvoření **detailního listu** a nakonec **uložení sešitu v C#** stylu. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu.

> **Rychlý přehled:**  
> • Hlavní cíl – generovat Excel z JSON.  
> • Vedlejší cíle – povolit duplicitní názvy listů, vytvořit detailní list, uložit sešit v C#.  

## Požadavky

Než začneme, ujistěte se, že máte:

- .NET 6.0 SDK (nebo jakoukoli novější verzi .NET).  
- Visual Studio 2022 nebo VS Code s rozšířením C#.  
- Aktivní licenci nebo bezplatnou zkušební verzi **Aspose.Cells for .NET** (NuGet balíček je `Aspose.Cells`).  
- Šablonu Excelu (`template.xlsx`), která již obsahuje SmartMarker tagy jako `&=Name` a placeholder pro detailní tabulku.

Pokud některý z těchto bodů není vám známý, nepanikařte – instalace NuGet balíčku je jediný příkaz a šablona může být obyčejný sešit s několika placeholder buňkami.

## Přehled řešení

Na vysoké úrovni provedeme:

1. Definování řetězce JSON, který odráží data, jež chceme v listu.  
2. Nastavení `SmartMarkerOptions`, aby byly povoleny duplicitní názvy listů a aby **detailní list** získal předvídatelný název.  
3. Načtení Excel šablony, která obsahuje SmartMarker tagy.  
4. Spuštění SmartMarker procesoru, který sloučí JSON data do sešitu.  
5. Uložení finálního souboru pomocí `workbook.Save(...)`.

Každý krok je podrobně vysvětlen níže, včetně kompletních úryvků kódu a důvodů, proč je krok důležitý.

---

## Krok 1 – Připravte JSON payload, který sloučíte

Prvním, co potřebujete, je dokument JSON, který odpovídá SmartMarker tagům ve vaší šabloně. JSON je zdroj pravdy; každý klíč se stane placeholderem v Excel souboru.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Proč je to důležité:**  
SmartMarker čte hierarchii JSON a automaticky rozšiřuje tabulky pro kolekce jako `Orders`. Pokud struktura JSON neodpovídá tagům, sloučení tiše vytvoří prázdné řádky – častá chyba.

---

## Krok 2 – Nakonfigurujte SmartMarker pro povolení duplicitních názvů listů a pojmenujte detailní list

Ve výchozím nastavení Aspose.Cells zakazuje duplicitní názvy listů, což může být překážka, když generujete detailní list pro každý hlavní záznam. Třída `SmartMarkerOptions` vám umožní tuto restrikci uvolnit a také specifikovat vzor pojmenování nově vytvořených detailních listů.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Proč je to důležité:**  
Pokud iterujete přes více zákazníků a každá iterace vytvoří nový list, engine by normálně vyhodil výjimku. Nastavením `AllowDuplicateSheetNames` na `true` říkáte Aspose.Cells, aby automaticky přidal číselný suffix, což proces zjednoduší.

---

## Krok 3 – Načtěte Excel šablonu, která obsahuje SmartMarker tagy

Vaše šablona je plátno, na kterém SmartMarker namaluje data. Může obsahovat libovolné formátování – barvy, vzorce, grafy – takže nemusíte tuto logiku znovu programovat.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Tip:**  
Uchovávejte šablonu ve složce, která je součástí výstupu projektu (např. `Content\Templates`). Pak na ni můžete odkazovat relativní cestou a vyhnete se tvrdému kódování absolutních adresářů.

---

## Krok 4 – Spusťte SmartMarker procesor s JSON a nastavením

Nyní se děje magie. `SmartMarkerProcessor` načte JSON, respektuje nastavené možnosti a vyplní sešit podle nich.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Co se děje pod kapotou?**  
- Procesor prohledá každou buňku na značky jako `&=Name` nebo `&=Orders.Item`.  
- Nahrazuje jednoduché značky skalárními hodnotami (`Name`, `Date`).  
- Pro kolekce (`Orders`) vytvoří nový detailní list (pojmenovaný „Detail“) a naplní řádek tabulky pro každou položku.  
- Protože jsme povolili duplicitní názvy listů, pokud šablona již obsahuje list s názvem „Detail“, engine vytvoří „Detail (2)“.

---

## Krok 5 – Uložte sloučený sešit zpět na disk

Nakonec zapíšete naplněný sešit do souboru. Můžete zvolit libovolný formát podporovaný Aspose.Cells – XLSX, CSV, PDF atd. Zde zůstáváme u moderního XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Proč je to důležité:**  
Ukládání je místo, kde skutečně **uložíte sešit v C#** stylu. Pokud potřebujete streamovat soubor zpět webovému klientovi, můžete použít `workbook.Save(Stream, SaveFormat.Xlsx)`.

---

## Kompletní funkční příklad

Sestavte vše dohromady – zde je kompletní, připravený ke spuštění konzolový aplikace. Ujistěte se, že jste před kompilací nainstalovali NuGet balíček `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Očekávaný výsledek

- **Sheet 1** (hlavní list) zobrazí „John“ v buňce `Name` a „2023‑01‑01` v buňce `Date`.  
- Objeví se nový **Detail** list, který obsahuje tabulku se dvěma řádky: jeden pro objednávku Laptop a jeden pro objednávku Mouse.  
- Pokud šablona již měla list pojmenovaný „Detail“, nový list bude pojmenován „Detail (2)“, díky příznaku `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "výsledek generování excelu z jsonu")

*Image alt text:* **generování excelu z json – ukázkový sešit s hlavním a detailním listem**

---

## Časté otázky a okrajové případy

### Co když můj JSON obsahuje vnořené kolekce?

SmartMarker dokáže zpracovat vnořené pole, ale budete muset přidat další detailní listy nebo použít hierarchické značky. Například `&=Orders.SubItems.Product` automaticky vygeneruje list třetí úrovně.

### Jak mohu přizpůsobit vzor pojmenování pro duplicitní listy?

Místo statického `DetailSheetNewName` můžete přiřadit callback pomocí `smartMarkerOptions.DetailSheetNameGenerator`. To vám umožní vložit časové razítko nebo unikátní ID do názvu listu.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Můžu generovat CSV místo XLSX?

Určitě. Nahraďte poslední volání `Save` tímto:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Zbytek pipeline zůstává beze změny.

### Funguje to v ASP.NET Core?

Ano. stejný kód může běžet uvnitř akce kontroleru. Stačí streamovat sešit do odpovědi:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Profesionální tipy a úskalí

- **Pro tip:** Uchovávejte SmartMarker tagy v samostatném listu „Template“. Tak můžete list chránit před nechtěnými úpravami a zároveň umožnit procesoru jej číst.  
- **Dejte si pozor na:** JSON klíče, které obsahují mezery nebo speciální znaky. Aspose.Cells očekává platné JavaScript identifikátory; přejmenujte je nebo použijte atribut `JsonProperty`, pokud deserializujete z POCO.  
- **Tip pro výkon:** Pokud zpracováváte tisíce řádků, nastavte `smartMarkerOptions.EnableCache = true`, aby se znovu použily zkompilované značky.  
- **Kontrola verze:** Výše uvedený kód cílí na Aspose.Cells 23.9+. Starší verze nemusí podporovat `AllowDuplicateSheetNames`.

---

## Závěr

Nyní máte kompletní, end‑to‑end recept na **generování Excelu z JSON** v C#. Konfigurací `SmartMarkerOptions` jsme ukázali, jak **povolit duplicitní názvy listů**, řídit pojmenování **detailního listu** a nakonec **uložit sešit v C#** stylu. Přístup je zcela samostatný – žádné externí služby, jen jediný NuGet balíček.

Další krok? Zkuste nahradit JSON zdroj reálným API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}