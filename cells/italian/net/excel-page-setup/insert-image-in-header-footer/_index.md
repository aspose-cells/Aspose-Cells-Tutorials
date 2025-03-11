---
title: Inserisci immagine nell'intestazione o nel piè di pagina
linktitle: Inserisci immagine nell'intestazione o nel piè di pagina
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come inserire immagini nelle intestazioni e nei piè di pagina utilizzando Aspose.Cells per .NET con questa guida completa passo dopo passo.
weight: 60
url: /it/net/excel-page-setup/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Inserisci immagine nell'intestazione o nel piè di pagina

## Introduzione

Quando si lavora con file Excel, intestazioni e piè di pagina svolgono un ruolo cruciale nel fornire contesto e informazioni preziose. Immagina di redigere un report per la tua attività e che il logo aziendale debba essere presente nell'intestazione per dargli un tocco professionale. In questa guida, ti mostreremo come usare Aspose.Cells per .NET per inserire un'immagine nell'intestazione o nel piè di pagina dei tuoi fogli Excel.

## Prerequisiti

Prima di immergerti nel codice vero e proprio, ci sono alcune cose che devi avere pronte:

1.  Aspose.Cells per la libreria .NET: assicurati di avere la libreria Aspose.Cells installata nel tuo ambiente .NET. Se non ce l'hai ancora, puoi[scaricalo qui](https://releases.aspose.com/cells/net/).
2. Visual Studio o qualsiasi altro IDE: avrai bisogno di un ambiente di sviluppo integrato per scrivere ed eseguire il codice C#.
3.  Un'immagine di esempio: prepara un'immagine che vuoi inserire nell'intestazione o nel piè di pagina. Per il nostro esempio, useremo un logo aziendale chiamato`aspose-logo.jpg`.
4. Conoscenza di base di C#: sebbene non sia obbligatorio, comprendere C# ti semplificherà la comprensione di questo tutorial.
5. Accesso al file system: assicurati di avere accesso al file system in cui leggerai l'immagine e salverai il file Excel.

## Importa pacchetti

Per iniziare, devi importare i namespace necessari nel tuo file C#. Ecco una rapida analisi:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Queste importazioni forniranno l'accesso a tutte le classi necessarie per manipolare i file Excel e gestire i file sul sistema.

## Passaggio 1: impostazione del percorso della directory

Per prima cosa, dovrai specificare la directory in cui si trovano i tuoi file Excel e le tue immagini. Aggiorna il percorso per adattarlo alla tua struttura locale.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Aggiornare di conseguenza
```

 Questa linea imposta il`dataDir`variabile, che è il percorso di base per individuare l'immagine che si desidera inserire nell'intestazione.

## Passaggio 2: creazione di un oggetto cartella di lavoro

Successivamente, dovrai creare una nuova cartella di lavoro in cui aggiungerai l'immagine.

```csharp
Workbook workbook = new Workbook();
```

 Questa riga di codice inizializza una nuova istanza di`Workbook` classe, che consente di manipolare fogli di calcolo Excel.

## Passaggio 3: Definizione del percorso dell'immagine

 È il momento di creare una variabile stringa per contenere il percorso all'immagine che vuoi usare. Nel nostro caso, stiamo usando`aspose-logo.jpg`.

```csharp
string logo_url = dataDir + "aspose-logo.jpg";
```

Qui concateniamo il percorso della directory con il nome del file del logo.

## Passaggio 4: lettura dell'immagine come dati binari

Per inserire l'immagine nell'intestazione, dobbiamo leggere il file immagine come dati binari.

```csharp
FileStream inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
byte[] binaryData = new byte[inFile.Length];
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```

-  IL`FileStream` viene utilizzato per aprire l'immagine in modalità lettura.
-  Quindi, dichiariamo un array di byte`binaryData` per contenere i dati dell'immagine.
-  Infine, leggiamo i dati dell'immagine dal`FileStream`.

## Passaggio 5: accesso all'oggetto Imposta pagina

 Per apportare modifiche all'intestazione, dobbiamo accedere a`PageSetup` oggetto associato al primo foglio di lavoro. 

```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```

 Qui otteniamo il`PageSetup` oggetto, che consente di manipolare le impostazioni di stampa del foglio di lavoro.

## Passaggio 6: inserimento dell'immagine nell'intestazione

Con i dati binari dell'immagine a disposizione, possiamo inserirli nell'intestazione.

```csharp
pageSetup.SetHeaderPicture(1, binaryData);
```

 Questa riga posiziona l'immagine nella sezione centrale dell'intestazione. Il parametro`1` specifica la sezione dell'intestazione.

## Passaggio 7: impostazione del contenuto dell'intestazione

Ora che abbiamo posizionato l'immagine, aggiungiamo del testo all'intestazione per migliorarne il contesto. 

```csharp
pageSetup.SetHeader(1, "&G"); // Inserisce l'immagine
pageSetup.SetHeader(2, "&A"); // Inserisce il nome del foglio
```

- La prima riga inserisce il segnaposto dell'immagine (`&G`).
- La seconda riga aggiunge il nome del foglio nella sezione destra dell'intestazione, utilizzando il segnaposto (`&A`).

## Passaggio 8: salvataggio della cartella di lavoro

Dopo aver apportato tutte le modifiche necessarie, è il momento di salvare la cartella di lavoro.

```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```

Questa riga salva la cartella di lavoro con il nome file specificato nella directory definita in precedenza.

## Passaggio 9: chiusura di FileStream

 Infine, non dimenticare di chiudere il tuo`FileStream` per liberare le risorse.

```csharp
inFile.Close();
```

In questo modo l'applicazione rimane ordinata e si evitano perdite di memoria.

## Conclusione

Congratulazioni! Hai aggiunto con successo un'immagine all'intestazione di un file Excel usando Aspose.Cells per .NET. Che si tratti di un logo aziendale o di una citazione stimolante, le intestazioni possono migliorare notevolmente la professionalità dei tuoi documenti. Ora puoi applicare questa conoscenza a vari progetti: immagina quanto saranno raffinati i tuoi report con intestazioni e piè di pagina personalizzati!

## Domande frequenti

### Quali formati di file supporta Aspose.Cells per le immagini?
Aspose.Cells supporta diversi formati, tra cui JPEG, PNG, BMP, GIF e TIFF.

### Posso inserire più immagini nell'intestazione/piè di pagina?
Sì, puoi inserire immagini separate in sezioni diverse dell'intestazione o del piè di pagina utilizzando segnaposto diversi.

### Aspose.Cells è gratuito?
 Aspose.Cells offre una prova gratuita, ma è disponibile una versione con licenza per l'accesso completo e funzionalità aggiuntive. Puoi ottenere un[licenza temporanea qui](https://purchase.aspose.com/temporary-license/).

### Come posso risolvere i problemi relativi alle immagini che non vengono visualizzate?
Assicurati che il percorso dell'immagine sia corretto e che il file esista. Controlla anche la compatibilità del formato dell'immagine.

### Dove posso trovare ulteriore documentazione per Aspose.Cells?
 Puoi trovare la documentazione dettagliata[Qui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
