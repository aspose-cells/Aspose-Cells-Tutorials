---
title: Esportare il valore stringa HTML delle celle in DataTable in Excel
linktitle: Esportare il valore stringa HTML delle celle in DataTable in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come esportare valori stringa HTML da celle di Excel in una DataTable utilizzando Aspose.Cells per .NET in un semplice tutorial passo dopo passo.
weight: 11
url: /it/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esportare il valore stringa HTML delle celle in DataTable in Excel

## Introduzione

Quando lavori con file Excel in un ambiente .NET, potresti dover estrarre informazioni dalle celle, non solo come testo normale, ma piuttosto come stringhe HTML. Questo può essere molto utile quando hai a che fare con dati di testo avanzato o quando vuoi mantenere la formattazione. In questa guida, ti guiderò nell'esportazione del valore stringa HTML delle celle in una DataTable utilizzando Aspose.Cells per .NET. 

## Prerequisiti

Prima di immergerti nel codice, assicuriamoci di avere tutto ciò di cui hai bisogno al suo posto. Ecco una rapida checklist:

1. Conoscenza di base di C# e .NET: prima di iniziare a scrivere codice, assicurati di avere familiarità con la programmazione C# e con le basi del framework .NET.
2.  Aspose.Cells per .NET: se non lo hai già fatto, devi installare Aspose.Cells per .NET. Puoi scaricare una versione di prova gratuita da[Qui](https://releases.aspose.com/).
3. Visual Studio o IDE di tua scelta: imposta il tuo ambiente per scrivere codice C#. Visual Studio è consigliato per la sua ampia gamma di funzionalità e la facilità d'uso.
4. File Excel di esempio: avrai bisogno di un file Excel di esempio (`sampleExportTableAsHtmlString.xlsx`) con cui lavorare. Assicurati che si trovi in una directory accessibile.
5. NuGet Package Manager: assicurati di avere accesso a NuGet Package Manager nel tuo progetto per aggiungere facilmente la libreria Aspose.Cells.

Una volta soddisfatti questi prerequisiti, iniziamo a sporcarci le mani con un po' di programmazione!

## Importa pacchetti

Prima di poter iniziare a lavorare con Aspose.Cells, dobbiamo importare i pacchetti necessari. Questo di solito comporta l'aggiunta del pacchetto NuGet Aspose.Cells al tuo progetto. Ecco come fare:

### Aprire il gestore pacchetti NuGet

In Visual Studio, fai clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e seleziona Gestisci pacchetti NuGet.

### Cerca Aspose.Cells

 Nel Gestore pacchetti NuGet, digitare`Aspose.Cells` nella barra di ricerca.

### Installa il pacchetto

Una volta trovato Aspose.Cells, clicca sul pulsante Installa. Questo aggiungerà la libreria al tuo progetto e ti consentirà di importarla nel tuo codice.

### Importa lo spazio dei nomi

Aggiungi la seguente direttiva using all'inizio del tuo file di codice:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Ora che abbiamo impostato tutto, approfondiamo il processo passo dopo passo per esportare i valori stringa HTML da un file Excel a un DataTable. 

## Passaggio 1: definire la directory di origine

Inizierai definendo la directory in cui è archiviato il tuo file Excel di esempio. Questo è fondamentale perché indica alla tua applicazione dove trovare il file. Ecco il codice per farlo:

```csharp
string sourceDir = "Your Document Directory";
```

 Assicurati di sostituire`"Your Document Directory"` con il percorso effettivo del file Excel.

## Passaggio 2: caricare il file Excel di esempio

 Il passo successivo è caricare la cartella di lavoro di Excel. Utilizzerai il`Workbook` classe da Aspose.Cells per fare questo. Ecco come puoi caricare il file:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Questa semplice riga di codice inizializza la cartella di lavoro e carica il file Excel specificato.

## Passaggio 3: accedi al primo foglio di lavoro

Una volta caricata la cartella di lavoro, vorrai accedere al foglio di lavoro specifico che contiene i dati che ti interessano. In genere, inizierai con il primo foglio di lavoro:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Qui stiamo lavorando con il primo foglio di lavoro (indice 0). Assicurati che i tuoi dati siano sul foglio corretto.

## Passaggio 4: specificare le opzioni della tabella di esportazione

Per controllare come vengono esportati i dati, è necessario impostare`ExportTableOptions`In questo caso, vuoi assicurarti che i nomi delle colonne non vengano esportati e vuoi che i dati delle celle vengano esportati come stringhe HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Questa configurazione consente di mantenere la formattazione avanzata dei dati delle celle durante l'esportazione.

## Passaggio 5: esportare le celle in DataTable

 Ora arriva la parte cruciale in cui si esportano effettivamente i dati. Utilizzando il`ExportDataTable` metodo, è possibile estrarre i dati dal foglio di lavoro in un`DataTable`Ecco come fare:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Questo codice esporta un intervallo specificato di celle (dalla riga 0, colonna 0 alla riga 3, colonna 3) in un DataTable utilizzando le opzioni specificate in precedenza.

## Passaggio 6: stampare il valore della stringa HTML

Infine, stampiamo il valore della stringa HTML da una cella specifica nella DataTable per vedere cosa siamo riusciti a esportare. Ad esempio, se vuoi stampare il valore dalla terza riga e dalla seconda colonna, dovresti fare quanto segue:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Questa riga stampa la stringa HTML desiderata dalla DataTable nella console. 

## Conclusione 

Ed ecco fatto! Hai esportato con successo valori di stringa HTML da celle in un file Excel a un DataTable usando Aspose.Cells per .NET. Questa capacità non solo arricchisce le tue capacità di manipolazione dei dati, ma amplia anche le tue opzioni quando gestisci contenuti formattati direttamente da file Excel. 

## Domande frequenti

### Posso usare Aspose.Cells per altri formati di file oltre a Excel?  
Sì, Aspose.Cells è principalmente per Excel, ma Aspose offre altre librerie per formati diversi.

### Ho bisogno di una licenza per Aspose.Cells?  
 Sì, è richiesta una licenza valida per l'uso in produzione. Puoi ottenere una licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/).

### Cosa succede se il mio file Excel contiene formule? Verranno esportate correttamente?  
Sì, Aspose.Cells può gestire le formule e, durante l'esportazione, queste verranno valutate in base ai valori risultanti.

### È possibile modificare le opzioni di esportazione?  
 Assolutamente! Puoi personalizzare`ExportTableOptions` per soddisfare le tue esigenze specifiche.

### Dove posso trovare una documentazione più dettagliata per Aspose.Cells?  
 Puoi trovare una documentazione estesa[Qui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
