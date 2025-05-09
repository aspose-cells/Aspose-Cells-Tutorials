---
"date": "2025-04-05"
"description": "Scopri come automatizzare l'estrazione e il salvataggio di oggetti OLE da file Excel utilizzando Aspose.Cells per .NET, migliorando il flusso di lavoro di elaborazione dati."
"title": "Automatizza l'estrazione e il salvataggio degli oggetti OLE di Excel utilizzando Aspose.Cells per .NET"
"url": "/it/net/ole-objects-embedded-content/excel-automation-extract-save-ole-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Automatizza l'estrazione e il salvataggio degli oggetti OLE di Excel con Aspose.Cells per .NET

## Introduzione

Stai cercando di semplificare il tuo flusso di lavoro automatizzando l'estrazione di oggetti incorporati nei tuoi file Excel? Che tu sia uno sviluppatore o un analista di dati, sfruttando **Aspose.Cells per .NET** può ridurre significativamente il lavoro manuale e gli errori. Questo tutorial ti guiderà nell'estrazione e nel salvataggio di oggetti OLE (Object Linking and Embedding) dalle cartelle di lavoro di Excel in base al loro formato di file.

### Cosa imparerai:
- Apertura e caricamento di una cartella di lavoro di Excel tramite Aspose.Cells.
- Accesso alla raccolta di oggetti OLE in un foglio di lavoro.
- Estrazione e salvataggio di oggetti OLE in base ai loro formati specifici.

Configuriamo il tuo ambiente e implementiamo questa efficiente funzionalità!

## Prerequisiti

Prima di iniziare, assicurati di aver soddisfatto i seguenti prerequisiti:

### Librerie richieste:
- **Aspose.Cells per .NET** - Essenziale per la gestione dei file Excel in un ambiente .NET.

### Configurazione dell'ambiente:
- Un ambiente di sviluppo come Visual Studio o qualsiasi IDE compatibile con supporto per C# e .NET.

### Prerequisiti di conoscenza:
- Conoscenza di base della programmazione C#.
- Familiarità con il framework .NET, in particolare con le operazioni di I/O sui file.

## Impostazione di Aspose.Cells per .NET

Per utilizzare Aspose.Cells per .NET, è necessario installarlo nel progetto. Ecco come fare:

### Istruzioni per l'installazione:

**Utilizzo della CLI .NET:**
```bash
dotnet add package Aspose.Cells
```

**Utilizzo del Gestore Pacchetti:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Acquisizione della licenza:
- **Prova gratuita:** Inizia con una prova gratuita di 30 giorni per esplorare tutte le funzionalità.
- **Licenza temporanea:** Richiedi una licenza temporanea per un accesso esteso.
- **Acquistare:** Se questo strumento soddisfa le tue esigenze, acquista una licenza completa.

Una volta installato, inizializza Aspose.Cells nel tuo progetto come segue:

```csharp
using Aspose.Cells;

// Inizializzare la libreria
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Path to License File");
```

## Guida all'implementazione

### Funzionalità 1: Apri e carica la cartella di lavoro

Carichiamo una cartella di lavoro di Excel da una directory specificata.

#### Implementazione passo dopo passo:

**Definisci directory di origine:**
```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
```

**Crea istanza cartella di lavoro:**
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleExtractOLEObjects.xlsx");
```
Questo passaggio carica il file Excel in un `Workbook` oggetto, consentendo di manipolarne il contenuto a livello di programmazione.

### Funzionalità 2: accedere alla raccolta OleObject nel foglio di lavoro

Ora accediamo agli oggetti OLE incorporati nel primo foglio di lavoro della cartella di lavoro.

#### Implementazione passo dopo passo:

**Foglio di lavoro Access First:**
```csharp
OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
Questo frammento recupera tutti gli oggetti OLE dal foglio di lavoro specificato per un'ulteriore elaborazione.

### Funzionalità 3: Estrarre e salvare oggetti OLE in base al formato

Successivamente, scorrere ogni oggetto OLE per estrarne i dati e salvarli in base al formato.

#### Implementazione passo dopo passo:

**Eseguire l'iterazione attraverso gli oggetti OLE:**
```csharp
using System.IO;

for (int i = 0; i < oles.Count; i++)
{
    OleObject ole = oles[i];
    byte[] oleData = ole.ObjectData;
    string fileName = outputDir + "outputExtractOLEObjects" + (i+1) + ".";

    switch (ole.FileFormatType)
    {
        case FileFormatType.Doc:
            fileName += "doc";
            break;
        case FileFormatType.Docx:
            fileName += "docx";
            break;
        case FileFormatType.Excel97To2003:
            fileName += "xls";
            break;
        case FileFormatType.Xlsx:
            // Gestione speciale per i formati XLSX
            using (MemoryStream ms = new MemoryStream())
            {
                ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
                Workbook oleBook = new Workbook(ms);
                oleBook.Settings.IsHidden = false;

                ms.SetLength(0); // Cancella il flusso
                oleBook.Save(ms, SaveFormat.Xlsx);

                ms.Position = 0;
                byte[] bts = new byte[ms.Length];
                ms.Read(bts, 0, (int)ms.Length);
                oleData = bts;
            }
            fileName += "xlsx";
            break;
        case FileFormatType.Ppt:
            fileName += "ppt";
            break;
        case FileFormatType.Pdf:
            fileName += "pdf";
            break;
        case FileFormatType.Unknown:
            Guid g = new Guid(ole.ClassIdentifier);
            if (g.ToString() == "b801ca65-a1fc-11d0-85ad-444553540000")
            {
                fileName += "pdf";
            }
            else
            {
                fileName += "jpg";
            }                      
            break;
        default:
            // Gestisci altri formati o genera un'eccezione
            break;
    }

    File.WriteAllBytes(fileName, oleData);
}
```
Questa sezione illustra come gestire dinamicamente diversi formati di file e salvarli in modo appropriato.

## Applicazioni pratiche

Ecco alcuni casi d'uso reali per l'estrazione di oggetti OLE da file Excel:
1. **Reporting automatico dei dati:** Estrarre automaticamente documenti o immagini incorporati come parte di un processo di reporting dei dati.
2. **Sistemi di archiviazione dati:** Archiviare i contenuti incorporati nei fogli di calcolo per scopi di conformità.
3. **Integrazione con i sistemi di gestione documentale:** Integrare perfettamente gli oggetti OLE estratti in altre piattaforme di gestione dei documenti.

## Considerazioni sulle prestazioni

Per garantire prestazioni ottimali quando si lavora con Aspose.Cells:
- **Ottimizza l'utilizzo della memoria:** Utilizzo `MemoryStream` gestire saggiamente ed efficacemente la memoria durante le operazioni sui file.
- **Elaborazione batch:** Se si gestiscono grandi set di dati, elaborare i file in batch per evitare un utilizzo eccessivo delle risorse.
- **Buone pratiche:** Aggiorna regolarmente le tue librerie .NET e sfrutta le ultime funzionalità di Aspose.Cells per ottenere prestazioni migliori.

## Conclusione

Seguendo questa guida, hai imparato come automatizzare l'estrazione di oggetti OLE dalle cartelle di lavoro di Excel utilizzando Aspose.Cells per .NET. Questa competenza migliora l'efficienza dell'elaborazione dei dati e riduce gli errori di gestione manuale nei flussi di lavoro.

### Prossimi passi:
- Sperimenta diversi formati di file.
- Esplora le funzionalità aggiuntive fornite da Aspose.Cells per semplificare ulteriormente le tue attività.

Pronti a provarci? Iniziate a implementare queste tecniche nei vostri progetti oggi stesso!

## Sezione FAQ

1. **Come posso gestire i formati di oggetti OLE non supportati?**
   - Per formati sconosciuti o non supportati, utilizzare `FileFormatType.Unknown` caso e implementare la logica personalizzata in base alle necessità.

2. **Aspose.Cells è in grado di gestire in modo efficiente file Excel di grandi dimensioni?**
   - Sì, è ottimizzato per le prestazioni. Considera l'elaborazione in batch per set di dati molto grandi per mantenere l'efficienza.

3. **Cosa succede se il formato del file estratto non è corretto?**
   - Ricontrolla il `FileFormatType` nell'istruzione switch e assicurarti la corretta mappatura dei formati.

4. **Aspose.Cells .NET è gratuito?**
   - Puoi iniziare con una prova gratuita di 30 giorni e acquistare licenze per un utilizzo prolungato.

5. **Come posso integrare gli oggetti OLE estratti in altri sistemi?**
   - Utilizzare operazioni I/O standard sui file o strumenti di integrazione per spostare i file sul sistema desiderato.

## Risorse
- **Documentazione:** [Documentazione di Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **Scaricamento:** [Ultime uscite](https://releases.aspose.com/cells/net/)
- **Acquista licenza:** [Acquista ora](https://purchase.aspose.com/buy)
- **Prova gratuita:** [Per iniziare](https://releases.aspose.com/cells/net/)
- **Licenza temporanea:** [Richiedi qui](https://purchase.aspose.com/temporary-license/)
- **Forum di supporto:** [Supporto Aspose](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}