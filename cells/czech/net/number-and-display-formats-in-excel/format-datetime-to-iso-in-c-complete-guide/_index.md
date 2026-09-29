---
category: general
date: 2026-03-22
description: Naučte se, jak formátovat datum a čas do ISO při extrahování data z Excelu
  a zobrazit ISO datum pomocí Aspose.Cells v C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: cs
og_description: Formátování data a času na ISO je snadné. Tento průvodce ukazuje,
  jak extrahovat datum z Excelu a zobrazit ISO datum pomocí Aspose.Cells.
og_title: Formátování DateTime na ISO v C# – krok za krokem tutoriál
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formátování DateTime na ISO v C# – Kompletní průvodce
url: /cs/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formátování datetime na iso v C# – Kompletní průvodce

Už jste někdy potřebovali **formátovat datetime na iso**, ale zdroj se nachází v sešitu Excel? Možná buňka obsahuje japonskou éru jako “令和3年5月1日” a přemýšlíte, jak ji převést na čistý řetězec `2021‑05‑01`. Nejste v tom sami. V tomto tutoriálu **extrahujeme datum z excelu**, rozparsujeme japonskou éru a pak **zobrazíme iso datum** na konzoli – vše pomocí několika řádků C# a Aspose.Cells.

Projdeme si vše, co potřebujete: požadovaný NuGet balíček, přesný kód, který můžete zkopírovat‑vložit, proč je každý řádek důležitý a několik tipů pro okrajové případy. Na konci budete mít znovupoužitelný úryvek, který formátuje datetime na iso bez ohledu na to, jak podivně vypadá původní hodnota v Excelu.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód také kompiluje na .NET Framework 4.6+)
- Visual Studio 2022 (nebo jakýkoli editor, který preferujete)
- **Aspose.Cells for .NET** NuGet balíček – `Install-Package Aspose.Cells`
- Excel soubor (nebo nový sešit), který obsahuje datum ve formátu japonské éry

To je vše. Žádné další knihovny, žádné COM interop, jen jedna dobře zdokumentovaná metoda.

## Krok 1: Vytvořte sešit a zapište datum v japonské éře  

Nejprve potřebujeme sešit, se kterým budeme pracovat. Pokud už máte Excel soubor, můžete jej načíst pomocí `new Workbook("path")`. V tomto příkladu vytvoříme nový sešit v paměti a vložíme japonský řetězec éry do buňky **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Proč to děláme:** Aspose.Cells ve výchozím nastavení zachází s hodnotami buněk jako s řetězci. Vložením surového textu éry simulujeme reálný scénář, kdy japonský klient zadal data ve svém rodném kalendáři.

## Krok 2: Povolit parsování japonské éry a extrahovat datum  

Aspose.Cells dokáže automaticky převést řetězce japonské éry na .NET `DateTime` objekty – pokud mu to povolíte. Příznak `DateTimeParseOptions.EnableJapaneseEra` dělá těžkou práci.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** Pokud zapomenete volbu `EnableJapaneseEra`, knihovna vrátí původní řetězec a následná konverze selže. Vždy ověřujte `parsed.Type`, pokud pracujete s mixovaným obsahem.

## Krok 3: Převést parsovaný DateTime na ISO 8601  

Nyní, když máme správný `DateTime`, je převod na ISO‑formátovaný řetězec hračka. Vzor `"yyyy-MM-dd"` splňuje část data ISO 8601, což je to, co většina API očekává.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Spuštění programu vypíše:

```
ISO date: 2021-05-01
```

To je **zobrazené iso datum**, které jste hledali.

## Kompletní, spustitelný příklad  

Níže je celý blok kódu, který můžete zkopírovat přímo do konzolového projektu. Žádné skryté závislosti, žádná extra konfigurace.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Očekávaný výstup:** `ISO date: 2021-05-01`

## Rozpis krok za krokem (Proč je každá část důležitá)

| Krok | Co se děje | Proč je to důležité |
|------|------------|---------------------|
| **Create workbook** | Inicializuje Excel kontejner v paměti. | Poskytuje sandbox pro testování bez zásahu do souborového systému. |
| **PutValue** | Uloží surový řetězec japonské éry do **A1**. | Napodobuje reálný vstup dat; zajišťuje, že parser vidí přesný text. |
| **GetValue with `EnableJapaneseEra`** | Převádí řetězec éry na .NET `DateTime`. | Automaticky řeší konverzi kalendáře – žádné ruční lookup tabulky nejsou potřeba. |
| `ToString("yyyy-MM-dd")` | Formátuje `DateTime` na ISO 8601. | Zaručuje kulturu‑neutrální, řaditelný datumový řetězec přijatý REST API, databázemi atd. |
| **Console.WriteLine** | Zobrazí finální ISO datum. | Potvrzuje, že celý pipeline funguje end‑to‑end. |

## Řešení běžných variant  

### 1. Různé umístění buňky  

Pokud se vaše datum nachází v **B2** nebo pojmenovaném rozsahu, stačí nahradit `"A1"` odpovídající adresou:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Více dat v jednom sloupci  

Když potřebujete **extrahovat datum z excelu** pro mnoho řádků, projděte použité rozmezí ve smyčce:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Náhradní řešení pro ne‑éra data  

Pokud buňka již obsahuje standardní datumový řetězec, parser stále funguje, ale můžete chtít bezpečnostní síť:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Příznak `TryParse` zabraňuje výjimkám a vrátí původní hodnotu, pokud konverze selže.

### 4. Časová složka  

Pokud potřebujete také časovou část, použijte `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

To vrátí plný ISO 8601 timestamp (`2021-05-01T00:00:00`).

## Vizuální pomůcka  

![příklad formátování datetime na iso](image.png "Příklad formátování datetime na iso v C#")

*Alt text:* *příklad formátování datetime na iso zobrazující výstup konzole*

## Často kladené otázky  

- **Mohu to použít s .xls soubory?**  
  Ano. Aspose.Cells podporuje `.xls`, `.xlsx`, `.csv` a mnoho dalších formátů přímo.

- **Co když je sešit chráněn heslem?**  
  Načtěte jej pomocí `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Je formát ISO závislý na locale?**  
  Ne. Vzor `"yyyy-MM-dd"` je nezávislý na kultuře, což zaručuje stejný řetězec na jakémkoli počítači.

- **Funguje to na .NET Core?**  
  Ano—Aspose.Cells je kompatibilní s .NET Standard 2.0.

## Závěr  

Probrali jsme, jak **formátovat datetime na iso** pomocí **extrahování data z excelu**, parsování japonských érových řetězců a nakonec **zobrazení iso data** na konzoli. Hlavní kroky – vytvořit sešit, zapsat nebo načíst text éry, povolit parsování japonské éry a formátovat pomocí `ToString("yyyy-MM-dd")` – jsou vše, co potřebujete pro většinu scénářů.

Dále můžete:

- Zapsat ISO data zpět do dalšího sloupce pro následné zpracování.
- Exportovat upravený sešit do CSV pro hromadný import.
- Kombinovat tuto logiku s webovým API, které přijímá nahrané Excel soubory a vrací JSON‑kódované ISO datumy.

Neváhejte experimentovat s různými formáty dat, časovými zónami nebo dokonce vlastními kalendáři. Flexibilita Aspose.Cells znamená, že zřídkakdy narazíte na neřešitelný problém.

Šťastné kódování a ať jsou všechny vaše datumy perfektně ISO‑kompatibilní!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}