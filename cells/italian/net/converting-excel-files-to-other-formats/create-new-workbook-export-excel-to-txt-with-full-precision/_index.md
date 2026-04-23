---
category: general
date: 2026-03-18
description: Crea un nuovo foglio di lavoro ed esporta Excel in TXT mantenendo la
  precisione numerica. Scopri come salvare il foglio di lavoro come txt e convertire
  il foglio di lavoro in txt in modo efficiente.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: it
og_description: Crea una nuova cartella di lavoro ed esporta Excel in TXT con precisione.
  Questo tutorial mostra come salvare il foglio di lavoro come TXT e convertire il
  foglio di lavoro in TXT usando C#.
og_title: Crea nuova cartella di lavoro – Guida all'esportazione di Excel in TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crea nuovo foglio di lavoro – Esporta Excel in TXT con precisione completa
url: /it/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea nuovo workbook – Esporta Excel in TXT con Precisione Completa

Ti è mai capitato di **create new workbook** in C# solo per scaricare alcuni dati in un file di testo semplice? Forse stai estraendo un report da un sistema legacy e lo strumento a valle accetta solo un feed `.txt`. La buona notizia? Non devi sacrificare la precisione numerica e non è necessario creare manualmente stringhe CSV.

In questa guida percorreremo l’intero processo di **export excel to txt**, coprendo tutto, dall’inizializzazione del workbook alla conservazione degli zeri finali quando **save worksheet as txt**. Alla fine avrai uno snippet pronto all’uso da inserire in qualsiasi progetto .NET—senza utilità aggiuntive.

## Di cosa avrai bisogno

- **ASP.NET/ .NET 6+** (il codice funziona anche su .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – la libreria che alimenta le classi `Workbook`, `Worksheet` e `TxtSaveOptions`. Puoi ottenerla da NuGet con `Install-Package Aspose.Cells`.  
- Una conoscenza di base di C# (se ti trovi a tuo agio con le istruzioni `using`, sei pronto).  

Questo è tutto—niente interop Excel, nessun oggetto COM e sicuramente nessuna concatenazione manuale di stringhe.  

---

## Passo 1: Inizializza un nuovo Workbook (Parola chiave principale)

La prima cosa da fare è **create new workbook**. Pensa al workbook come a una tela vuota dove incollerai successivamente numeri, testo o formule.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Perché è importante:** Istanziare `Workbook` senza caricare un file ti fornisce una pagina bianca. Puoi quindi aggiungere dati programmaticamente, il che è perfetto per scenari di **convert worksheet to txt** in cui non hai un `.xlsx` esistente.

---

## Passo 2: Popola le celle – Mantieni gli zeri finali

Un errore comune quando si scaricano numeri in testo è perdere gli zeri finali (`123.45000` diventa `123.45`). Se i sistemi a valle si basano su campi a larghezza fissa, questa perdita può rompere tutto.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Consiglio professionale:** `PutValue` inferisce automaticamente il tipo di dato. Se ti serve una stringa che assomigli a un numero, usa `PutValue("123.45000")` invece.

---

## Passo 3: Configura le opzioni di salvataggio TXT – Conserva la precisione numerica

Qui avviene la magia. Attivando `PreserveNumericPrecision`, istruisci Aspose.Cells a scrivere il valore esatto inserito, inclusi gli zeri finali insignificanti.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Perché abilitarla?** Quando **save excel as txt**, il comportamento predefinito elimina i decimali non necessari. Impostare `PreserveNumericPrecision = true` garantisce che l’output rispecchi il valore visualizzato nella cella, fondamentale per report finanziari o dati scientifici.

---

## Passo 4: Salva il foglio di lavoro come TXT – L'esportazione finale

Ora salviamo effettivamente **save worksheet as txt**. Puoi indicare qualsiasi percorso in cui hai permessi di scrittura; l’esempio usa una cartella relativa chiamata `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Output previsto** (`num-preserve.txt`):

```
123.45000
```

Nota che gli zeri finali sono intatti—esattamente come richiesto.

---

## Passo 5: Verifica il risultato – Controllo rapido

Dopo l’esecuzione del programma, apri `num-preserve.txt` in qualsiasi editor di testo. Dovresti vedere la singola riga `123.45000`. Se trovi `123.45`, ricontrolla che `PreserveNumericPrecision` sia impostato su `true` e che tu stia usando una versione recente di Aspose.Cells (v23.10+).

---

## Varianti comuni e casi limite

### Esportazione di più celle o intervalli

Se devi **export excel to txt** per un intervallo intero, riempi semplicemente più celle prima di salvare:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose scriverà ogni cella su una nuova riga per impostazione predefinita. Puoi anche cambiare il delimitatore (tab, virgola) tramite `txtSaveOptions.Separator`.

### Conversione del foglio di lavoro in TXT con codifiche diverse

A volte i sistemi a valle richiedono UTF‑8 BOM o ASCII. Regola la codifica così:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Gestione di workbook di grandi dimensioni

Quando lavori con fogli massicci (centinaia di migliaia di righe), considera lo streaming dell’output:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Consigli professionali e avvertenze

- **Non dimenticare di creare la directory di output** prima di chiamare `Save`, altrimenti otterrai una `DirectoryNotFoundException`.  
- **Fai attenzione ai separatori decimali specifici della locale**. Se il tuo ambiente usa le virgole (`1,23`), imposta `txtSaveOptions.DecimalSeparator = '.'` per forzare il punto.  
- **Compatibilità di versione**: il flag `PreserveNumericPrecision` è stato introdotto in Aspose.Cells 20.6. Se usi una versione più vecchia, il flag non esisterà e dovrai formattare la cella come testo prima di salvare.

---

![Create new workbook example](excel-to-txt.png "Create new workbook") *Testo alternativo: "Crea nuovo workbook ed esporta Excel in TXT con precisione numerica preservata"*

---

## Riepilogo – Cosa abbiamo coperto

- **Create new workbook** usando Aspose.Cells.  
- Popola una cella con un numero che include zeri finali.  
- Imposta `TxtSaveOptions.PreserveNumericPrecision = true` per **save excel as txt** senza perdere precisione.  
- Scrivi il file su disco, verificando che l’output corrisponda al valore originale.  

Questo è l’intero workflow di **convert worksheet to txt** in meno di 50 righe di C#.

---

## Prossimi passi e argomenti correlati

Ora che puoi **export excel to txt** con precisione perfetta, potresti voler esplorare:

- **Esportazione in CSV** con delimitatori personalizzati (`TxtSaveOptions.Separator`).  
- **Salvataggio in altri formati di testo** come TSV (`SaveFormat.TabDelimited`).  
- **Elaborazione batch** di più workbook in una cartella usando `Directory.GetFiles`.  
- **Integrazione con Azure Functions** per conversioni on‑demand nel cloud.

Ognuno di questi si basa sullo stesso pattern `Workbook` → `Worksheet` → `TxtSaveOptions`, quindi ti sentirai subito a tuo agio.

---

### Pensiero finale

Se hai seguito la guida, ora sai esattamente come **create new workbook**, popolarlo e **save worksheet as txt** mantenendo ogni cifra decimale di cui hai bisogno. È un piccolo frammento di codice, ma risolve un problema sorprendentemente comune quando le pipeline legacy richiedono input di testo semplice.

Provalo, modifica le opzioni e lascia che i dati fluiscano esattamente come desideri. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}