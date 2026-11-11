---
category: general
date: 2026-10-26
description: Scopri come impostare un formato numerico personalizzato in un file Excel
  con C# configurando le cifre significative, creando una cartella di lavoro Excel
  e salvandola come documento XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: it
lastmod: 2026-10-26
og_description: Il formato numerico personalizzato di Excel in C# ti consente di controllare
  le cifre significative, creare una cartella di lavoro Excel e salvarla come XLSX.
  Segui questo tutorial completo.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Formato numerico personalizzato in Excel con C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Come applicare un formato numerico personalizzato in Excel con C#
url: /it/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come applicare un formato numerico personalizzato in Excel con C#

Se hai bisogno di un **custom number format excel** che mostri un numero specifico di cifre significative, questa guida ti mostra esattamente come farlo in C#. Vedrai come impostare le cifre significative, creare una cartella di lavoro Excel e salvare il file come XLSX—tutto con poche righe di codice.

Lavorare con i file Excel in modo programmatico spesso richiede di controllare come appaiono i numeri. Utilizzando Aspose.Cells per .NET puoi definire un’opzione globale di formattazione numerica che costringe ogni cella numerica a rispettare un dato conteggio di cifre significative. Questo tutorial copre l’intero flusso di lavoro, dall’impostazione del progetto alla verifica del risultato in Excel.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate (il codice funziona anche con .NET Framework 4.7.2+)
* Visual Studio 2022 o qualsiasi IDE C# tu preferisca
* Il pacchetto NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`) – una libreria completamente gestita per la manipolazione di Excel
* Familiarità di base con la sintassi C#

## Passo 1: Creare una cartella di lavoro Excel in C#

La prima operazione è istanziare un nuovo oggetto `Workbook`. Questo oggetto rappresenta l’intero file Excel in memoria.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Perché è importante:** `Workbook` è il punto di ingresso per ogni operazione su Excel. Creandolo per primo, garantisci un file pulito che potrai successivamente salvare come XLSX.

## Passo 2: Configurare il formato numerico per impostare le cifre significative

Aspose.Cells fornisce un’impostazione globale chiamata `NumberFormatOptions`. Assegnando `SignificantDigits = 4`, ogni cella numerica visualizzerà fino a quattro cifre significative, a meno che un formato più specifico non la sovrascriva.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Perché è importante:** Usare `SetNumberFormatOptions` ti permette di definire un **custom number format excel** senza dover scrivere una stringa di formato per ogni cella. È l’equivalente dell’opzione “Cifre significative” che trovi nella finestra *Formato celle → Numero → Personalizzato* di Excel.

## Passo 3: Scrivere valori e verificare il formato numerico personalizzato

Ora inserisci un valore numerico in una cella. L’impostazione globale applicherà automaticamente la regola a 4 cifre.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Quando apri il file salvato, la cella **A1** mostrerà `123.5` (arrotondato a quattro cifre significative). Il valore originale rimane invariato nei dati sottostanti, cosa che puoi confermare osservando la barra della formula.

**Suggerimento per casi limite:** Se memorizzi un numero molto grande come `12345678.9`, la stessa impostazione visualizzerà `1.235E+07` (notazione scientifica) perché Excel sceglie la rappresentazione più compatta mantenendo quattro cifre significative.

## Passo 4: Salvare la cartella di lavoro come XLSX

Infine, persisti la cartella di lavoro su disco. Il metodo `Save` sceglie automaticamente il formato del file in base all’estensione.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Perché è importante:** Salvare come **XLSX** (`save workbook xlsx`) garantisce la massima compatibilità con le versioni moderne di Excel, Office 365 e altri strumenti di fogli di calcolo.

## Risultato atteso

Apri *C:\Temp\SigDigits.xlsx* in Microsoft Excel. Dovresti vedere:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Valore originale: | **123.456789**  |

*La cella A1* mostra il numero arrotondato a quattro cifre significative, mentre *C1* conserva la precisione completa per il confronto.

## Varianti comuni e come impostare il formato numerico per celle specifiche

### Utilizzare una stringa di formato personalizzata invece delle opzioni globali

Se ti serve un formato che si applichi solo a un intervallo singolo, puoi assegnare direttamente una stringa di formato:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Applicare l’impostazione a un’intera colonna

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Gestire i numeri negativi

L’opzione globale `SignificantDigits` funziona uniformemente per numeri positivi e negativi. Se desideri una visualizzazione diversa per i valori negativi, combinala con un formato personalizzato:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Consigli e insidie

* **Consiglio:** Imposta le opzioni di formattazione numerica **prima** di scrivere qualsiasi dato. Modificare l’opzione dopo aver popolato le celle non riformatta retroattivamente i valori esistenti.
* **Attenzione a:** Usare `PutValue` con una **stringa** che assomiglia a un numero (es. `"123.45"`). Excel la tratterà come testo e il formato personalizzato non verrà applicato.
* **Nota sulle prestazioni:** Le impostazioni globali sono poco costose, ma applicare uno stile a milioni di celle può aumentare l’utilizzo di memoria. Usa la formattazione a livello di colonna quando possibile.

## Prossimi passi

Ora che sai **custom number format excel** con cifre significative, potresti approfondire:

* **Come impostare il formato numerico** per date e valute usando `Style.Custom`.
* **Creare grafici** che rispettino i tuoi formati personalizzati.
* **Esportare in CSV** mantenendo la precisione numerica (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Questi argomenti si basano sugli stessi concetti di `Workbook` e `Worksheet` mostrati qui.

---

**Riepilogo**

Hai imparato a **custom number format excel** configurando `NumberFormatOptions` per **impostare le cifre significative**, creando una cartella di lavoro Excel in C#, scrivendo valori e **salvando la cartella di lavoro come file XLSX**. Il codice completo e funzionante sopra mostra ogni passaggio, spiega perché ciascuna parte è necessaria e fornisce consigli per varianti comuni. Sentiti libero di adattare gli snippet ai tuoi progetti e sperimentare con altri scenari di formattazione.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [Custom Number Format Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Create Excel Workbook C# – Limit Significant Digits Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}