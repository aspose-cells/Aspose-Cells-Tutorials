---
category: general
date: 2026-10-01
description: Scopri come creare una cartella di lavoro Excel in C#, applicare un formato
  numerico personalizzato, impostare i decimali delle celle e salvare la cartella
  di lavoro come XLSX in una guida completa passo passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: it
lastmod: 2026-10-01
og_description: Crea una cartella di lavoro Excel in C# con formato numerico personalizzato,
  imposta i decimali delle celle e salva la cartella di lavoro come XLSX. Segui questa
  guida completa per un output numerico preciso.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Crea cartella di lavoro Excel C# – formato numerico personalizzato e esportazione
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Come creare una cartella di lavoro Excel in C# con formattazione numerica personalizzata
url: /it/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro Excel C# con formattazione numerica personalizzata

Se hai bisogno di **create excel workbook c#** che visualizzi i numeri esattamente come desideri, questa guida ti mostra come farlo in pochi passaggi chiari. Imparerai ad applicare un formato numerico personalizzato, impostare i decimali delle celle e infine **save workbook as xlsx** per l'uso successivo.

Lavorare con dati numerici spesso richiede un equilibrio tra precisione e leggibilità. Alla fine di questo tutorial avrai un modello riutilizzabile che limita le cifre visualizzate a un numero specifico di cifre significative, preservando il valore originale nel file. Non sono necessari script esterni—solo C# e la libreria Aspose.Cells.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 SDK o versioni successive installate  
* Visual Studio 2022 (o qualsiasi IDE C#)  
* Il pacchetto NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – questa libreria fornisce le classi `Workbook`, `Worksheet` e `ExportTableOptions` usate negli esempi.  

Questi requisiti sono minimi; lo stesso codice funziona in .NET Core, .NET Framework e anche in Azure Functions.

## Passo 1: Create Excel workbook C# – inizializzare il file

La prima operazione è istanziare un nuovo oggetto `Workbook`. Questo oggetto rappresenta l'intero file Excel in memoria e contiene automaticamente un foglio di lavoro predefinito.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Perché è importante:**  
Creare la cartella di lavoro in anticipo ti offre una tela pulita. Il foglio di lavoro predefinito (`Worksheets[0]`) è pronto per l'immissione dei dati, quindi non è necessario aggiungere un nuovo foglio a meno che lo scenario non richieda più schede.

## Passo 2: Write a numeric value to a cell

Ora inserisci un numero di esempio nella cella **A1**. Il valore che usiamo (`123.456789`) contiene più decimali di quanti ne vogliamo visualizzare alla fine, il che ci permette di dimostrare l'arrotondamento in seguito.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Suggerimento:** `PutValue` rileva automaticamente il tipo di dato, quindi non devi convertire il numero in una stringa.

## Passo 3: Apply custom number format – limit visible decimals

Per controllare come Excel mostra il numero, creiamo uno `Style` con un **custom number format**. Il modello `"0.######"` indica a Excel di visualizzare fino a sei decimali ma di omettere gli zero finali.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Come funziona:**  
La stringa di formato segue la sintassi dei formati personalizzati di Excel. `0` forza la presenza di una cifra, mentre `#` visualizza una cifra solo se è significativa. Combinandoli ottieni una visualizzazione flessibile che rispetta comunque la precisione originale.

## Passo 4: Set cell decimal places – using ExportTableOptions

Se devi **set cell decimal places** per i dati esportati (ad esempio quando converti in un DataTable), Aspose.Cells ti consente di specificare il numero di **significant digits**. Questo passaggio garantisce che il CSV o il DataTable esportato rispetti le stesse regole di arrotondamento applicate nella cartella di lavoro.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Perché usare `SignificantDigits`?**  
A differenza di un conteggio decimale fisso, le cifre significative preservano la magnitudine del numero limitando la precisione, il che è spesso ciò che gli analisti si aspettano quando riassumono i dati.

## Passo 5: Export the worksheet data and **save workbook as xlsx**

Infine, esporta i dati (se ti serve un DataTable) e salva la cartella di lavoro su disco. La chiamata `ExportDataTable` rispetta le `ExportTableOptions` configurate, e `workbook.Save` scrive un file XLSX standard.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Risultato atteso:**  
Quando apri *SigDigits.xlsx* in Excel, la cella **A1** mostra `123.5`. Il valore sottostante rimane `123.456789`, ma il numero visualizzato rispetta la regola dei 4 cifre significative. Se esporti il foglio in un DataTable, il valore nella tabella sarà anch'esso arrotondato a `123.5`.

---

## Apply custom number format to additional cells

Se devi formattare un intervallo anziché una singola cella, riutilizza l'oggetto `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Riutilizzare un oggetto stile riduce l'overhead di memoria e garantisce una formattazione coerente su tutto il foglio.

## How to format numbers Excel using C# – common variations

| Scenario | Format string | Result |
|----------|---------------|--------|
| Due decimali fissi | `"0.00"` | `123.46` |
| Valuta (USA) | `"$#,##0.00"` | `$123.46` |
| Percentuale con un decimale | `"0.0%"` | `12,346.0%` |
| Notazione scientifica | `"0.00E+00"` | `1.23E+02` |

Scegli il modello che corrisponde ai requisiti del tuo report. Tutti i modelli sono compatibili con la proprietà `Style.Custom` mostrata in precedenza.

## Set cell decimal places dynamically based on user input

A volte la precisione richiesta non è nota al momento della compilazione. Puoi costruire la stringa di formato a runtime:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Caso limite:** Se `decimals` è zero, il formato diventa `"0"` (visualizzazione intera). Convalida sempre l'input dell'utente per evitare stringhe di formato non valide.

## Save workbook as XLSX – best practices

* **Usa percorsi assoluti** quando scrivi in una directory nota (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** il `Workbook` se lo avvolgi in una dichiarazione `using` per liberare rapidamente le risorse non gestite:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Compatibilità versioni:** Aspose.Cells scrive file compatibili con Excel 2010‑2023, quindi gli utenti downstream non incontreranno problemi di formato.

---

## Full working example

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire immediatamente. Include tutte le direttive `using` necessarie, commenti e gestione degli errori.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Passaggi di verifica**

1. Esegui il programma (`dotnet run`).  
2. Apri `SigDigits.xlsx`.  
3. Conferma che **A1** legga `123.5`.  
4. Se apri l'XML del file (`.xlsx` è un archivio zip), vedrai il formato personalizzato `"0.######"` memorizzato nell'attributo `s` dell'elemento `<c>`.

---

## Conclusion

In questo tutorial hai imparato a **create excel workbook c#**, **apply custom number format**, **set cell decimal places** e **save workbook as xlsx** usando Aspose.Cells. La soluzione dimostra sia la formattazione visiva all'interno di Excel sia l'arrotondamento dei dati esportati tramite `ExportTableOptions`.  

Da qui puoi:

* Estendere l'approccio a interi intervalli o tabelle.  
* Combinare più stili (font, bordi) con `StyleFlag`.  
* Automatizzare la generazione di report iterando sulle fonti dati e applicando la stessa logica di formattazione.  

Sentiti libero di sperimentare con diverse stringhe di formato, conteggi decimali o opzioni di esportazione per adattarle alle tue esigenze di reporting specifiche. Buon coding!

## What Should You Learn Next?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}