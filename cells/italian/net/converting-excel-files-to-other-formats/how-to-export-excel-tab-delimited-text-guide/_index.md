---
category: general
date: 2026-02-26
description: come esportare Excel in un file txt delimitato da tabulazioni usando
  C#. Impara a esportare Excel come tab, convertire Excel in txt e esportare Excel
  con delimitatore in tre semplici passaggi.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: it
og_description: come esportare Excel in un file txt delimitato da tabulazioni usando
  C#. Questo tutorial mostra come esportare Excel come tabulazione, convertire Excel
  in txt e esportare Excel con delimitatore.
og_title: Come esportare Excel – Guida al testo delimitato da tabulazioni
tags:
- csharp
- excel
- file-conversion
title: Come esportare Excel – Guida al testo delimitato da tabulazioni
url: /it/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

to skip hidden rows?**  
  Yes. Set `exportOptions.ExportHiddenRows = false` (default is `true`). Hidden rows will be omitted from the final text file.

## Conclusion

Translate heading.

You now... etc.

Translate final paragraph.

Then image line unchanged.

Then closing shortcodes.

Let's produce translation.

Be careful to keep markdown formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come esportare excel – Tutorial completo C#

Ti sei mai chiesto **come esportare excel** in un file di testo semplice senza perdere la formattazione? Forse ti serve rapidamente un TSV (valori separati da tabulazione) per una pipeline di dati, o stai alimentando un sistema legacy che legge solo `.txt`. In ogni caso, non sei solo: gli sviluppatori si imbattono spesso in questo ostacolo quando devono estrarre dati da fogli di calcolo.

La buona notizia? In sole tre semplici mosse puoi **esportare excel come tab**‑delimitato, **convertire excel in txt**, e persino scegliere un delimitatore personalizzato se cambi idea più tardi. Di seguito troverai un esempio C# completamente eseguibile, perché ogni riga è importante, e una serie di consigli per evitare gli errori più comuni.

> **Pro tip:** Questo approccio funziona con la popolare libreria Aspose.Cells, ma i concetti si applicano a qualsiasi API Excel .NET che offra un metodo in stile `ExportTable`.

## Cosa ti servirà

- **.NET 6+** (o .NET Framework 4.6+). Il codice si compila su qualsiasi runtime recente.
- **Aspose.Cells for .NET** (versione di prova gratuita o licenza). Installa via NuGet: `dotnet add package Aspose.Cells`.
- Un workbook di input chiamato `input.xlsx` collocato in una cartella di tua scelta.
- Un pizzico di curiosità—non è necessario conoscere a fondo gli internals di Excel.

Se hai già tutto questo, passiamo subito alla soluzione.

## Step 1 – Carica il Workbook che Vuoi Esportare

Per prima cosa creiamo un oggetto `Workbook` che punta al file sorgente. Questo oggetto rappresenta l’intero file Excel, incluse tutte le schede, gli intervalli nominati e la formattazione.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Perché è importante:*  
Caricare il workbook ti dà accesso alla collezione di fogli (`workbook.Worksheets`). Senza questo oggetto non puoi indirizzare celle, intervalli o impostazioni di esportazione.  

> **Nota:** Se il tuo file si trova su una condivisione di rete, anteponi `\\` o usa un percorso UNC—Aspose.Cells lo gestisce senza problemi.

## Step 2 – Configura le Opzioni di Esportazione (Valori Stringa & Delimitatore Tab)

Ora indichiamo alla libreria come vogliamo che i dati vengano scritti. Impostando `ExportAsString = true` forziamo ogni cella a essere trattata come una semplice stringa, eliminando i formati numerici specifici della locale di Excel. La parte `Delimiter = "\t"` è il cuore di **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Perché è importante:*  
Se ometti `ExportAsString`, una cella contenente `12345` potrebbe diventare `12,345` in alcune impostazioni locali, rompendo i parser a valle. Il delimitatore può essere sostituito con virgole, pipe o qualsiasi altro carattere se in seguito decidi di **export excel with delimiter** diverso da una tabulazione.

## Step 3 – Esporta un Intervallo Specifico in un File di Testo

Infine, scegliamo l’intervallo di nostro interesse (`A1:D10` in questo esempio) e lo scriviamo in `out.txt`. Il metodo `ExportTable` fa tutto il lavoro pesante: legge le celle, applica le opzioni e scrive il risultato su disco.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Dopo l’esecuzione troverai `out.txt` con un contenuto simile a:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Ogni colonna è separata da una **tabulazione**, pronta per `awk`, `PowerShell` o qualsiasi strumento compatibile CSV che rispetti le tabulazioni.

### Verifica Rapida

Apri il file generato con un editor di testo semplice (Notepad, VS Code) e verifica:

1. Le colonne si allineano quando attivi “Show whitespace”.
2. Non compaiono virgolette o virgole extra.
3. Tutte le celle numeriche appaiono esattamente come in Excel (grazie a `ExportAsString`).

Se qualcosa non quadra, ricontrolla che il workbook di origine non nasconda righe/colonne e assicurati di aver indicato l’indice del foglio corretto.

## Varianti Comuni & Casi Limite

### Esportare un Intero Foglio

Se vuoi **export excel range** che copra l’intero foglio, puoi usare `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Usare un Delimitatore Differente

Passare da tab a pipe (`|`) è semplice come modificare una riga:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Questo soddisfa lo scenario **export excel with delimiter** senza riscrivere altro codice.

### Gestire File di grandi dimensioni (> 100 MB)

Per workbook molto grandi, trasmetti l’esportazione in streaming per evitare di caricare tutto in memoria:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Convertire più Fogli in un Solo Passaggio

Se devi **convertire excel in txt** per diversi fogli, itera su di essi:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Ogni foglio ottiene il proprio file TSV—pratico per lavori batch.

## Esempio Completo (Pronto per Copia‑Incolla)

Di seguito trovi l’intero programma, pronto per la compilazione. Sostituisci i percorsi dei file con i tuoi.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Output previsto:** Un file chiamato `out.txt` in cui ogni colonna è separata da un carattere di tabulazione e ogni valore di cella appare esattamente come in Excel.

## Domande Frequenti

- **Funziona con file .xls?**  
  Sì. Aspose.Cells rileva automaticamente il formato, quindi puoi puntare `Workbook` a un vecchio `.xls` e il codice rimane lo stesso.

- **E se i miei dati contengono tabulazioni?**  
  Le tabulazioni all’interno di una cella vengono preservate, il che può rompere i parser TSV. In tal caso, considera di passare a un delimitatore pipe (`|`) aggiornando `exportOptions.Delimiter`.

- **Posso esportare le formule invece dei valori?**  
  Imposta `exportOptions.ExportAsString = false` e usa la sovraccarico di `ExportTableOptions` che include `ExportFormula = true`. L’output conterrà il testo grezzo della formula.

- **C’è un modo per saltare le righe nascoste?**  
  Sì. Imposta `exportOptions.ExportHiddenRows = false` (il valore predefinito è `true`). Le righe nascoste verranno omesse dal file di testo finale.

## Conclusione

Ora disponi di una ricetta solida, pronta per la produzione, per **come esportare excel** in un file di testo tab‑delimitato, per **esportare excel come tab** e per **convertire excel in txt** con pieno controllo su delimitatori e intervalli. Utilizzando il metodo `ExportTable` di Aspose.Cells eviti la costruzione manuale di CSV, mantieni l’integrità dei dati e mantieni il codice pulito.

Pronto per la prossima sfida? Prova:

- Esportare direttamente in un `MemoryStream` per API web.  
- Aggiungere dinamicamente una riga di intestazione basata sul contenuto della prima riga.  
- Integrare questa routine in una Azure Function che monitora un bucket di storage per nuovi upload Excel.

Mettilo alla prova, modifica il delimitatore e lascia che i dati fluiscano dove ti servono. Buon coding!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}