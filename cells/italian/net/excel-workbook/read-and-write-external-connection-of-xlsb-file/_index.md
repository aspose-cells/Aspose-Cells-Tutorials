---
title: Leggere e scrivere la connessione esterna del file XLSB
linktitle: Leggere e scrivere la connessione esterna del file XLSB
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come gestire le connessioni esterne nei file XLSB utilizzando Aspose.Cells per .NET in questo tutorial completo.
weight: 130
url: /it/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leggere e scrivere la connessione esterna del file XLSB

## Introduzione

Ciao, appassionati di Excel! Siete pronti a tuffarvi nell'affascinante mondo dei file XLSB e delle connessioni esterne? Se avete mai lavorato con Excel, sapete quanto può essere potente e versatile, ma a volte presenta delle stranezze, soprattutto quando si tratta di connessioni a database esterni. Ecco dove Aspose.Cells per .NET viene in soccorso! Questa fantastica libreria vi consente di manipolare i file Excel in modo semplice. In questo articolo, vi guideremo passo dopo passo su come leggere e scrivere connessioni esterne in un file XLSB.

## Prerequisiti

Prima di iniziare, ecco alcune cose di cui avrai bisogno:

1. Conoscenza di base di C#: conoscere il linguaggio di programmazione C# ti aiuterà immensamente. Se ti senti a tuo agio a scrivere codice C#, sei a posto!
2.  Aspose.Cells per .NET: dovrai avere questa libreria installata nel tuo ambiente di sviluppo. Se non l'hai ancora fatto, puoi scaricarla facilmente[Qui](https://releases.aspose.com/cells/net/). 
3. Un IDE: avrai bisogno di un editor di codice o di un ambiente di sviluppo integrato (IDE) come Visual Studio. 
4. File XLSB di esempio: lavoreremo con un file XLSB di esempio che contiene connessioni esterne. Puoi crearne uno tuo o scaricare campioni online. 

Una volta soddisfatti tutti questi prerequisiti, siamo pronti a passare al codice!

## Importa pacchetti

Per iniziare, importiamo i pacchetti necessari nel nostro progetto. Assicurati di aver aggiunto un riferimento ad Aspose.Cells nel tuo progetto. Ecco come puoi farlo in C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Queste importazioni ti danno accesso alle funzionalità necessarie per manipolare i file Excel e le relative connessioni.

## Passaggio 1: impostare le directory

Prima di lavorare con il tuo file XLSB, devi impostare le directory di origine e di output. Questo passaggio è essenziale per mantenere i tuoi file organizzati.

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
// Directory di uscita
string outputDir = "Your Output Directory";
```

 In questo frammento di codice,`"Your Document Directory"` E`"Your Document Directory"` si presume che recuperino i rispettivi percorsi per dove risiederanno i file di input e output. Puoi sostituire questi metodi con percorsi hardcoded se preferisci.

## Passaggio 2: caricare il file XLSB

Ora è il momento di caricare il tuo file Excel in un oggetto Workbook. Questo ti dà la possibilità di manipolare i dati al suo interno.

```csharp
// Carica il file Excel Xlsb di origine
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Assicurati solo che il tuo file XLSB si trovi nella posizione specificata`sourceDir`Se il percorso è corretto, la tua cartella di lavoro sarà pronta per essere manipolata!

## Passaggio 3: accedere alle connessioni esterne

Con la cartella di lavoro caricata, puoi accedere alle sue connessioni esterne. Nel nostro caso, recupereremo la prima connessione al database.

```csharp
// Leggi la prima connessione esterna che è in realtà una connessione DB
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Qui,`DataConnections[0]` si riferisce alla prima connessione nella cartella di lavoro. La stiamo convertendo in un`DBConnection` digitare per ulteriori manipolazioni.

## Passaggio 4: estrarre le informazioni di connessione

Ora che hai accesso alla connessione al database, estraiamo e stampiamo i suoi dettagli sulla console. Questo ci aiuterà a vedere esattamente con cosa stiamo lavorando.

```csharp
// Stampa il nome, il comando e le informazioni di connessione del DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Questo passaggio ti consente di verificare lo stato attuale della tua connessione esterna. Vedrai il nome della connessione, il comando utilizzato e le informazioni sulla connessione stampate sulla console.

## Passaggio 5: modificare la connessione

A volte, un cambio di nome è tutto ciò che serve per rendere le cose più chiare o per adattarle a nuove convenzioni di denominazione. Cambiamo il nome della connessione esistente in qualcosa di più pertinente.

```csharp
// Modificare il nome della connessione
dbCon.Name = "NewCust";
```

Questa riga di codice rinomina efficacemente la tua connessione dal suo nome originale a "NewCust". È una modifica semplice ma di grande impatto!

## Passaggio 6: salva le modifiche

Dopo aver apportato le modifiche, vorrai salvare le modifiche nel file XLSB. Ecco come fare:

```csharp
// Salvare il file Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Questa riga di codice salva la cartella di lavoro aggiornata, mantenendo tutte le modifiche, incluso il nuovo nome della connessione.

## Passaggio 7: conferma dell'esecuzione

Infine, confermiamo che tutto ha funzionato senza problemi. Un semplice messaggio alla fine lo chiarirà.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Questo messaggio ti rassicurerà che il tuo codice è stato eseguito correttamente e che tutte le modifiche sono state salvate come previsto.

## Conclusione

Ed ecco fatto! Hai imparato con successo a leggere e scrivere connessioni esterne nei file XLSB usando Aspose.Cells per .NET. Seguendo questi passaggi, puoi gestire efficacemente le tue connessioni dati Excel, rendendo il tuo lavoro con Excel molto più snello e meno frustrante. Ricorda, che tu stia gestendo set di dati estesi o semplicemente organizzando le tue informazioni, Aspose.Cells ha gli strumenti di cui hai bisogno.

## Domande frequenti

### Che cos'è un file XLSB?  
Un file XLSB è un formato di file binario di Excel che memorizza i dati del foglio di calcolo in un formato binario, rendendoli più compatti e veloci da aprire.

### Come faccio a installare Aspose.Cells per .NET?  
 Puoi scaricarlo facilmente dal sito web di Aspose[Qui](https://releases.aspose.com/cells/net/).

### Posso usare Aspose.Cells gratuitamente?  
 Sì! Puoi iniziare con una prova gratuita, che è disponibile[Qui](https://releases.aspose.com/).

### Aspose.Cells supporta altri formati di file?  
Assolutamente! Aspose.Cells supporta una varietà di formati di file, tra cui XLSX, CSV e altri.

### Dove posso cercare aiuto se riscontro dei problemi?  
Puoi ottenere supporto dai forum di Aspose[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
