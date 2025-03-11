---
title: Adattamento automatico di colonne e righe durante il caricamento di HTML nella cartella di lavoro
linktitle: Adattamento automatico di colonne e righe durante il caricamento di HTML nella cartella di lavoro
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come adattare automaticamente colonne e righe durante il caricamento di codice HTML in Excel utilizzando Aspose.Cells per .NET. Guida dettagliata inclusa.
weight: 10
url: /it/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adattamento automatico di colonne e righe durante il caricamento di HTML nella cartella di lavoro

## Introduzione
Ti sei mai chiesto come regolare automaticamente le dimensioni di colonne e righe durante il caricamento di contenuti HTML in una cartella di lavoro Excel utilizzando Aspose.Cells per .NET? Bene, sei nel posto giusto! In questo tutorial, approfondiremo come caricare una tabella HTML in una cartella di lavoro e garantire che colonne e righe vengano adattate automaticamente per corrispondere al contenuto. Se lavori con dati dinamici che cambiano frequentemente, questa guida sarà la tua guida di riferimento per creare fogli Excel ben formattati da HTML.
### Prerequisiti
Prima di buttarti nel codice, ci sono alcune cose che devi aver impostato sul tuo sistema. Non preoccuparti, è semplice e diretto!
1. Visual Studio installato: sarà necessario Visual Studio o qualsiasi altro ambiente di sviluppo .NET.
2.  Aspose.Cells per .NET: puoi[Scarica l'ultima versione](https://releases.aspose.com/cells/net/) oppure utilizzare il gestore pacchetti NuGet per installarlo.
3. .NET Framework: assicurati di aver installato .NET Framework 4.0 o versione successiva.
4. Nozioni di base di C#: avere una conoscenza di base di C# renderà questo tutorial più semplice.
5. Dati della tabella HTML: prepara del contenuto HTML (anche una tabella di base) che vuoi caricare in Excel.
## Importa pacchetti
Per prima cosa, importiamo i namespace necessari per iniziare. Ecco un semplice elenco di ciò che devi importare:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Questi pacchetti consentono di gestire la cartella di lavoro, manipolare i dati HTML e caricarli senza problemi in Excel.
Scomponiamo questo processo in parti gestibili in modo che tu possa seguirlo facilmente. Alla fine, avrai un esempio pratico di come adattare automaticamente colonne e righe durante il caricamento di HTML in una cartella di lavoro utilizzando Aspose.Cells per .NET.
## Passaggio 1: impostare la directory dei documenti
Per salvare e recuperare facilmente i file, specificheremo il percorso in cui saranno archiviati i tuoi documenti. Puoi sostituire il percorso della directory con la posizione della tua cartella.
```csharp
string dataDir = "Your Document Directory";
```
Questa riga imposta la directory in cui verranno salvati i file Excel. È importante organizzare correttamente i file quando si lavora su più progetti. Immagina questo come l'archivio del tuo progetto!
## Passaggio 2: creare dati HTML come stringa
Successivamente, definiremo un contenuto HTML di base. Per questo esempio, utilizzeremo una semplice tabella HTML. Puoi personalizzarla in base alle esigenze del tuo progetto.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Stiamo definendo una stringa HTML molto semplice. Contiene una tabella con un paio di righe e colonne. Puoi aggiungere più righe o colonne in base alle tue esigenze. Immagina di preparare gli ingredienti prima di cucinare un pasto!
## Passaggio 3: caricare la stringa HTML in MemoryStream
 Ora che abbiamo pronto il nostro contenuto HTML, il passo successivo è caricarlo nella memoria usando`MemoryStream`Ciò ci consente di manipolare il contenuto HTML in memoria senza prima salvarlo su disco.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 Convertendo la stringa HTML in un array di byte e inserendola in un`MemoryStream`, possiamo lavorare con i dati HTML in memoria. Immagina questo passaggio come la preparazione del piatto in una pentola prima di metterlo nel forno!
## Passaggio 4: caricare MemoryStream in una cartella di lavoro (senza adattamento automatico)
 Una volta che abbiamo il contenuto HTML in memoria, lo carichiamo in un Aspose`Workbook`A questo punto, non stiamo ancora adattando automaticamente le colonne e le righe. Questo è il nostro scenario "prima", da confrontare con la versione adattata automaticamente in seguito.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
La cartella di lavoro è caricata con il contenuto HTML, ma le colonne e le righe non sono ancora adattate automaticamente al testo. Immagina di cuocere una torta ma di dimenticare di controllare la temperatura: funziona, ma potrebbe non essere perfetta!
## Passaggio 5: specificare le opzioni di caricamento HTML con l'adattamento automatico abilitato
 Ora, ecco la magia! Creiamo un'istanza di`HtmlLoadOptions` e abilitare il`AutoFitColsAndRows` proprietà. Ciò assicura che quando il contenuto HTML viene caricato, le colonne e le righe si adattano per adattarsi al contenuto al loro interno.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Impostando questa opzione, stiamo dicendo ad Aspose.Cells di ridimensionare automaticamente le righe e le colonne. Immagina di impostare il forno alla temperatura perfetta in modo che la torta cresca al punto giusto!
## Passaggio 6: caricare l'HTML nella cartella di lavoro con l'adattamento automatico abilitato
 Ora carichiamo di nuovo il contenuto HTML, ma questa volta con l'`AutoFitColsAndRows`opzione abilitata. Questo regolerà le larghezze delle colonne e le altezze delle righe in base al contenuto al loro interno.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Questo passaggio carica il contenuto HTML in una nuova cartella di lavoro e lo salva come file Excel, ma ora le colonne e le righe vengono adattate automaticamente! Pensa a questo come a una torta cotta alla perfezione, dove tutto ha le dimensioni giuste.
## Conclusione
Seguendo questi semplici passaggi, hai imparato come caricare contenuto HTML in una cartella di lavoro usando Aspose.Cells per .NET e adattare automaticamente le colonne e le righe. Ciò garantisce che i tuoi fogli Excel siano sempre ordinati, indipendentemente da quanto sia dinamico il contenuto. È una funzionalità semplice ma potente che può farti risparmiare un sacco di tempo nella formattazione e nell'organizzazione dei tuoi dati Excel.
Ora che hai acquisito queste conoscenze, puoi sperimentare contenuti HTML più complessi, aggiungere stili e persino creare intere cartelle di lavoro Excel da pagine web!
## Domande frequenti
### Posso usare questo metodo per caricare tabelle HTML di grandi dimensioni?
Sì, Aspose.Cells gestisce in modo efficiente tabelle HTML di grandi dimensioni, ma per prestazioni ottimali è consigliabile effettuare dei test con le dimensioni dei dati.
### Posso applicare manualmente specifiche larghezze di colonna e altezze di riga dopo l'adattamento automatico?
Assolutamente! Puoi comunque personalizzare singole colonne e righe anche dopo aver utilizzato la funzione di adattamento automatico.
### Come posso formattare la tabella dopo aver caricato l'HTML?
Dopo aver caricato l'HTML, è possibile applicare stili utilizzando le ampie opzioni di stile di Aspose.Cells.
### Aspose.Cells per .NET è compatibile con le versioni precedenti di .NET Framework?
Sì, Aspose.Cells per .NET supporta .NET Framework 4.0 e versioni successive.
### Posso caricare altri tipi di contenuto oltre all'HTML in Excel utilizzando Aspose.Cells?
Sì, Aspose.Cells supporta il caricamento di vari formati come CSV, JSON e XML in Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
