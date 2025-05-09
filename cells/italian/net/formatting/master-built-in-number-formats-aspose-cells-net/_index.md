---
"date": "2025-04-05"
"description": "Scopri come applicare formati numerici predefiniti utilizzando Aspose.Cells per .NET. Questa guida illustra la formattazione di data, percentuale e valuta nei file Excel con C#, garantendo una presentazione precisa dei dati."
"title": "Padroneggiare i formati numerici integrati in Aspose.Cells per .NET - Una guida completa alla formattazione di Excel con C#"
"url": "/it/net/formatting/master-built-in-number-formats-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Padroneggiare i formati numerici integrati in Aspose.Cells per .NET

Nell'attuale mondo basato sui dati, creare e gestire file Excel a livello di codice è una competenza fondamentale per gli sviluppatori. Se hai il compito di formattare i numeri in un file Excel utilizzando C#, questa guida completa sull'implementazione di formati numerici predefiniti con Aspose.Cells per .NET è la soluzione perfetta. Questo tutorial ti guiderà nella configurazione e nell'utilizzo di Aspose.Cells per personalizzare la visualizzazione dei numeri, garantendo una presentazione dei dati accurata e visivamente accattivante.

## Cosa imparerai
- Come impostare Aspose.Cells in un progetto C# .NET.
- Utilizzo di formati numerici integrati per vari tipi di celle di Excel.
- Applicazione di stili personalizzati per date, percentuali e valute.
- Applicazioni pratiche di queste tecniche in scenari reali.

Prima di immergerci nell'implementazione, assicuriamoci che tutto sia pronto per procedere senza intoppi.

## Prerequisiti
Per iniziare questo tutorial, avrai bisogno di:

- **Aspose.Cells per la libreria .NET**: Assicurati di utilizzare la versione più recente. Le istruzioni di installazione sono disponibili qui sotto.
- **Ambiente di sviluppo**: Si consiglia Visual Studio 2019 o versione successiva.
- **Conoscenza di base di C#**: Familiarità con i concetti di programmazione orientata agli oggetti in C#.

## Impostazione di Aspose.Cells per .NET

### Installazione
Per includere Aspose.Cells nel tuo progetto, puoi utilizzare .NET CLI o Package Manager:

**Interfaccia a riga di comando .NET**
```bash
dotnet add package Aspose.Cells
```

**Gestore dei pacchetti**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Acquisizione della licenza
Aspose offre una prova gratuita per valutare i propri prodotti. Per un utilizzo prolungato, è possibile optare per una licenza temporanea o acquistarne una.

- **Prova gratuita**: Scarica l'ultima versione da [Download di Aspose](https://releases.aspose.com/cells/net/).
- **Licenza temporanea**: Ottenere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/) per valutare tutte le funzionalità.
- **Acquistare**: Per un utilizzo a lungo termine, acquistare una licenza su [Acquisto Aspose](https://purchase.aspose.com/buy).

### Inizializzazione di base
Ecco come puoi iniziare a utilizzare Aspose.Cells nella tua applicazione:
```csharp
using Aspose.Cells;

// Inizializza una nuova cartella di lavoro
Workbook workbook = new Workbook();
```

## Guida all'implementazione
Suddividiamo l'implementazione in parti gestibili, concentrandoci sull'applicazione dei formati numerici integrati a diversi tipi di dati.

### Impostazione della cartella di lavoro

#### Panoramica
Inizia creando un nuovo file Excel e ottenendo i riferimenti ai suoi fogli di lavoro. Questo passaggio è fondamentale per gestire efficacemente gli stili delle celle.

**Creazione di una cartella di lavoro**
```csharp
// Crea una nuova istanza della cartella di lavoro
Workbook workbook = new Workbook();

// Accedi al primo foglio di lavoro nella cartella di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```

### Formattazione delle date

#### Panoramica
Visualizzare le date in un formato intuitivo è essenziale per la chiarezza. Applichiamo il formato "g-mmm-aa" a una cella.

**Applicazione del formato data**
```csharp
// Inserisci la data corrente nella cella A1
worksheet.Cells["A1"].PutValue(DateTime.Now);

// Recupera e modifica lo stile della cella
Style style = worksheet.Cells["A1"].GetStyle();
style.Number = 15; // Formato incorporato per "g-mmm-aa"
worksheet.Cells["A1"].SetStyle(style);
```

### Percentuali di formattazione

#### Panoramica
Convertire i valori numerici in percentuali può migliorare l'interpretazione dei dati, soprattutto nei report finanziari.

**Applicazione del formato percentuale**
```csharp
// Inserire un valore numerico nella cella A2
worksheet.Cells["A2"].PutValue(20);

// Modifica lo stile per la visualizzazione della percentuale
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9; // Formato incorporato per le percentuali
worksheet.Cells["A2"].SetStyle(style);
```

### Formattazione della valuta

#### Panoramica
I dati finanziari richiedono spesso la formattazione della valuta per garantire la coerenza tra i report.

**Applicazione del formato di valuta**
```csharp
// Inserire un valore numerico nella cella A3
worksheet.Cells["A3"].PutValue(2546);

// Imposta lo stile per la visualizzazione della valuta
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6; // Formato integrato per la valuta
worksheet.Cells["A3"].SetStyle(style);
```

### Salvataggio della cartella di lavoro
Infine, salva la cartella di lavoro in un file Excel:
```csharp
// Salvare la cartella di lavoro nel formato Excel97To2003
workbook.Save("path/to/your/book1.out.xls", SaveFormat.Excel97To2003);
```

## Applicazioni pratiche
Aspose.Cells per .NET è versatile e può essere integrato in vari scenari, come:

- **Rendicontazione finanziaria**: Formattazione automatica dei dati finanziari con stili di valuta o percentuale.
- **Strumenti di analisi dei dati**: Miglioramento della leggibilità delle date nei dashboard analitici.
- **Generazione automatica di report**: Personalizzazione di report Excel per le aziende.

## Considerazioni sulle prestazioni
Quando si lavora con set di dati di grandi dimensioni, tenere presente i seguenti suggerimenti per ottimizzare le prestazioni:

- **Gestione della memoria**: Smaltire gli oggetti che non servono più utilizzando `GC.Collect()`.
- **Elaborazione batch**: applicare gli stili in batch anziché cella per cella per migliorare l'efficienza.
- **Utilizzo delle risorse**: Monitora e gestisci l'utilizzo della memoria durante la gestione di file Excel di grandi dimensioni.

## Conclusione
Ora hai acquisito le basi per applicare i formati numerici predefiniti in Aspose.Cells per .NET. Questa conoscenza può migliorare significativamente le tue capacità di manipolazione dei file Excel, garantendo una presentazione accurata e professionale dei dati. Per esplorare ulteriormente le funzionalità di Aspose.Cells, ti consigliamo di approfondire la sua completezza. [documentazione](https://reference.aspose.com/cells/net/).

## Sezione FAQ
**D: Posso formattare le celle con formati numerici personalizzati?**
A: Sì, puoi definire formati numerici personalizzati utilizzando `style.Custom` oltre ai formati integrati.

**D: Come gestisco le eccezioni durante il salvataggio dei file?**
A: Inserire il metodo save in un blocco try-catch per gestire in modo efficiente le potenziali eccezioni IO.

**D: Aspose.Cells è compatibile con tutte le versioni di Excel?**
R: Sì, supporta diversi formati di file Excel, comprese le versioni più vecchie come Excel97To2003 e quelle più recenti come XLSX.

**D: Cosa succede se ho bisogno di formattare tipi di dati complessi?**
R: Per esigenze di formattazione più avanzate, esplora stili personalizzati o integra Aspose.Cells con altre librerie .NET.

**D: Dove posso trovare supporto per problemi non trattati nella documentazione?**
A: Visita il [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9) per l'assistenza alla comunità e alle autorità.

## Risorse
- **Documentazione**: Esplora le guide dettagliate su [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/).
- **Scaricamento**: Ottieni l'ultima versione da [Download di Aspose](https://releases.aspose.com/cells/net/).
- **Acquistare**: Acquista una licenza per l'accesso ininterrotto a [Acquisto Aspose](https://purchase.aspose.com/buy).
- **Prova gratuita**: Inizia con una prova gratuita da [Download di Aspose](https://releases.aspose.com/cells/net/).
- **Licenza temporanea**: Ottieni una licenza temporanea per la valutazione completa delle funzionalità su [Licenza temporanea Aspose](https://purchase.aspose.com/temporary-license/).
- **Supporto**: Ottieni aiuto su [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}