---
category: general
date: 2026-11-19
description: Imposta il formato numerico delle celle in C# e scopri come applicare
  il formato data di Excel per le date dell’era giapponese, consentendo una conversione
  affidabile delle date Excel in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: it
lastmod: 2026-11-19
og_description: Imposta il formato numerico della cella in C# e applica il formato
  data di Excel alle date dell'era giapponese. Segui questa guida completa per una
  conversione accurata delle date di Excel in C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Imposta il formato numerico delle celle e converti le date giapponesi in
  C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Imposta il formato numerico della cella e converti le date giapponesi in C#
url: /it/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il formato numerico delle celle e converti le date giapponesi in C#

Se devi **impostare il formato numerico delle celle** in un progetto di automazione Excel con C#, questa guida ti mostra come **applicare il formato data di Excel** e eseguire la **conversione data Excel in C#** per le date dell’era giapponese. Otterrai un esempio completo e funzionante che converte una stringa dell’era Reiwa (ad es., `R3/04/01`) nella data gregoriana `2021‑04‑01`.

## Cosa imparerai

* Come creare una cartella di lavoro e accedere al suo primo foglio di lavoro.  
* Come **impostare il formato numerico delle celle** affinché Excel tratti il valore come una data.  
* Come **applicare il formato data di Excel** che riconosce le stringhe dell’era giapponese.  
* Come attivare la **conversione data Excel in C#** ricalcolando le formule.  
* Output previsto e suggerimenti per la risoluzione di problemi nei casi limite.

**Prerequisiti**

* .NET 6 o successivo (il codice funziona anche con .NET Framework 4.6+).  
* Aspose.Cells per .NET 2024 o più recente – installa via NuGet: `dotnet add package Aspose.Cells`.  
* Familiarità di base con C# e la gestione delle date in Excel.

> **Suggerimento professionale:** Aspose.Cells funziona senza che Microsoft Office sia installato, rendendolo ideale per l’automazione lato server.

## Imposta il formato numerico delle celle con Aspose.Cells in C#

Il primo passo è dire a Excel che la cella contiene una data. Excel memorizza le date come numeri seriali, quindi dobbiamo applicare un formato data predefinito (ID 14) alla cella di destinazione.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Perché funziona

* `Style.Number = 14` corrisponde al formato *Data breve* di Excel (`mm/dd/yyyy` per impostazione predefinita).  
* Quando la cella contiene una stringa dell’era giapponese come `R3/04/01`, il parser interno di Aspose.Cells riconosce l’era e la converte nel corrispondente numero seriale gregoriano durante `CalculateFormula()`.  
* Dopo il calcolo, `StringValue` restituisce la data gregoriana formattata.

## Applica il formato data di Excel per le date dell’era giapponese

Se desideri che la cella visualizzi l’era giapponese anziché la data gregoriana, puoi usare un formato numerico personalizzato che includa il codice dell’era. Questo dimostra la capacità di **applicare il formato data di Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` forza la localizzazione giapponese.  
* `ggg` rappresenta il nome dell’era (ad es., `R` per Reiwa).  
* Aggiungere caratteri letterali (`年`, `月`, `日`) crea un layout di data giapponese familiare.

### Quando utilizzare un formato personalizzato

* Report destinati a un pubblico giapponese.  
* Quando è necessario conservare l’informazione originale dell’era per documenti legali.  
* In dashboard dove vengono mostrati sia le date gregoriane sia quelle dell’era affiancate.

## Conversione data Excel in C# – gestione delle ere giapponesi

Il processo di **c# excel date conversion** può essere suddiviso in tre parti logiche:

1. **Analisi della stringa dell’era** – Aspose.Cells riconosce automaticamente `R` (Reiwa), `H` (Heisei), `S` (Showa), ecc.  
2. **Conversione in numero seriale** – Excel memorizza le date come giorni a partire dal 30‑12‑1899.  
3. **Formattazione del numero seriale** – con un formato predefinito (ID 14) o un formato giapponese personalizzato.

### Esempio completo end‑to‑end

Di seguito è riportato un programma autonomo che dimostra sia l’output gregoriano sia quello dell’era in un’unica esecuzione.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Output previsto nella console**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Casi limite e problemi comuni

| Situazione                              | Cosa controllare                                      | Correzione / Raccomandazione                              |
|----------------------------------------|-------------------------------------------------------|-----------------------------------------------------------|
| Stringa dell’era vuota o malformata   | `PutValue` memorizza il testo letterale; la conversione fallisce | Convalida l’input con un’espressione regolare prima di scriverlo nella cella. |
| Mismatch di localizzazione             | Il formato personalizzato mostra cifre occidentali anziché caratteri giapponesi | Assicurati che il formato `Custom` includa `[$-ja-JP]` o imposta `Workbook.Settings.CultureInfo` su `ja-JP`. |
| Cartella di lavoro contiene formule che fanno riferimento alla cella data | Il ricalcolo può sovrascrivere i risultati delle formule | Chiama `CalculateFormula` **dopo** tutti i passaggi di formattazione, o usa `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` se devi ignorare gli errori. |
| Uso di versioni più vecchie di Aspose.Cells | Il supporto per le ere giapponesi è stato aggiunto nel Q3 2022 | Aggiorna all’ultima versione del pacchetto NuGet. |

## Testare la soluzione

1. **Esegui il programma** da Visual Studio o con `dotnet run`.  
2. Verifica che la console stampi la data gregoriana `2021‑04‑01` e la stringa dell’era `R3年04月01日`.  
3. Apri la cartella di lavoro generata (se aggiungi `wb.Save("Demo.xlsx");`) in Microsoft Excel per vedere la stessa formattazione applicata alle celle.

### Suggerimento per l’automazione

Se devi elaborare un ampio intervallo di date dell’era (ad es., la colonna A contiene molte date giapponesi), avvolgi la logica di conversione in un ciclo:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Questo approccio mantiene l’operazione di **impostare il formato numerico delle celle** veloce ed efficiente in termini di memoria.

## Conclusione

Ora sai come **impostare il formato numerico delle celle** in C# usando Aspose.Cells, come **applicare il formato data di Excel** per le stringhe dell’era giapponese e come eseguire una **conversione data Excel in C#** affidabile dall’era al calendario gregoriano. Il codice completo e funzionante dimostra entrambi gli output e evidenzia i casi limite più comuni.  

**Passi successivi**

* Esplora altri ID di formato predefiniti


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [set excel date format in C# – Complete Step‑by‑Step Guide](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [How to apply a custom number format excel in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}