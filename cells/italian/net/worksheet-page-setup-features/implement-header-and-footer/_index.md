---
"description": "Scopri come impostare intestazioni e piè di pagina nei fogli di lavoro di Excel utilizzando Aspose.Cells per .NET con una guida dettagliata, esempi pratici e suggerimenti utili."
"linktitle": "Implementare intestazione e piè di pagina nel foglio di lavoro"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Implementare intestazione e piè di pagina nel foglio di lavoro"
"url": "/it/net/worksheet-page-setup-features/implement-header-and-footer/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementare intestazione e piè di pagina nel foglio di lavoro

## Introduzione

Quando si lavora con fogli di calcolo Excel, intestazioni e piè di pagina svolgono un ruolo fondamentale nel trasmettere al pubblico informazioni contestuali importanti, come nomi di file, date o numeri di pagina. Che si stia automatizzando report o generando file dinamici, Aspose.Cells per .NET semplifica la personalizzazione di intestazioni e piè di pagina nei fogli di lavoro a livello di codice. Questa guida illustra un approccio completo e passo dopo passo per aggiungere intestazioni e piè di pagina con Aspose.Cells per .NET, conferendo ai file Excel un tocco di raffinatezza e professionalità in più.

## Prerequisiti

Prima di iniziare, assicurati di avere a disposizione quanto segue:

1. Aspose.Cells per .NET: sarà necessario installare Aspose.Cells per .NET. [Scaricalo qui](https://releases.aspose.com/cells/net/).
2. Configurazione IDE: Visual Studio (o l'IDE preferito) con .NET Framework installato.
3. Licenza: puoi iniziare con la prova gratuita, ma ottenendo una licenza completa o temporanea potrai sfruttare appieno il potenziale di Aspose.Cells. [Ottieni una licenza temporanea](https://purchase.aspose.com/temporary-license/).

La documentazione di Aspose.Cells è una risorsa utile da consultare durante questo processo. Puoi trovarla [Qui](https://reference.aspose.com/cells/net/).

## Importazione di pacchetti

Nel tuo progetto, importa gli spazi dei nomi richiesti:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importando questo pacchetto, avrai accesso alle classi e ai metodi necessari per lavorare con intestazioni, piè di pagina e altre funzionalità di Excel in Aspose.Cells.

In questa guida analizzeremo ogni passaggio in modo che tu possa seguirlo facilmente, anche se non hai familiarità con Aspose.Cells o .NET.

## Passaggio 1: imposta la cartella di lavoro e l'impostazione della pagina

Per prima cosa: crea una nuova cartella di lavoro e accedi alle impostazioni di pagina del foglio di lavoro. Questo ti fornirà gli strumenti necessari per modificare l'intestazione e il piè di pagina del foglio di lavoro.

```csharp
// Definisci il percorso in cui salvare il tuo documento
string dataDir = "Your Document Directory";

// Creare un'istanza di un oggetto Workbook
Workbook excel = new Workbook();
```

Qui abbiamo creato un `Workbook` oggetto, che rappresenta il nostro file Excel. L' `PageSetup` del foglio di lavoro è dove possiamo modificare le opzioni di intestazione e piè di pagina.


## Passaggio 2: accedere alle proprietà del foglio di lavoro e di PageSetup

In Aspose.Cells, ogni foglio di lavoro ha un `PageSetup` proprietà che controlla le funzionalità di layout, tra cui intestazioni e piè di pagina. Otteniamo il `PageSetup` oggetto per il nostro foglio di lavoro.

```csharp
// Ottenere il riferimento al PageSetup del primo foglio di lavoro
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

Con questo, `pageSetup` ora contiene tutte le impostazioni necessarie per personalizzare intestazioni e piè di pagina.


## Passaggio 3: imposta la sezione sinistra dell'intestazione

Le intestazioni in Excel sono divise in tre sezioni: sinistra, centro e destra. Iniziamo impostando la sezione sinistra in modo che visualizzi il nome del foglio di lavoro.

```csharp
// Imposta il nome del foglio di lavoro nella sezione sinistra dell'intestazione
pageSetup.SetHeader(0, "&A");
```

Utilizzo `&A` Permette di visualizzare dinamicamente il nome del foglio di lavoro. Questa funzionalità è particolarmente utile se si hanno più fogli in una cartella di lavoro e si desidera che ogni intestazione rifletta il titolo del foglio.


## Passaggio 4: aggiungere data e ora al centro dell'intestazione

Ora aggiungiamo la data e l'ora correnti nella sezione centrale dell'intestazione. Inoltre, useremo un font personalizzato per lo stile.

```csharp
// Imposta data e ora nella sezione centrale dell'intestazione con carattere in grassetto
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

In questo codice:
- `&D` inserisce la data corrente.
- `&T` inserisce l'ora corrente.
- `"Times New Roman,Bold"` applica il carattere Times New Roman in grassetto a questi elementi.


## Passaggio 5: visualizzare il nome del file nella sezione destra dell'intestazione

Per completare l'intestazione, mostriamo il nome del file sul lato destro, insieme a una regolazione del carattere.

```csharp
// Visualizza il nome del file nella sezione destra dell'intestazione con dimensione del carattere personalizzata
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` rappresenta il nome del file, rendendo chiaro a quale file appartengono le pagine stampate.
- `&12` modifica la dimensione del carattere a 12 per questa sezione.


## Passaggio 6: aggiungere testo con carattere personalizzato alla sezione del piè di pagina sinistro

Passiamo ai piè di pagina! Inizieremo impostando la sezione del piè di pagina sinistro con testo personalizzato e uno stile di carattere specifico.

```csharp
// Aggiungi testo personalizzato con stile di carattere alla sezione sinistra del piè di pagina
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

IL `&\"Courier New\"&14` l'impostazione nel codice soprastante applica il font "Courier New" con dimensione 14 al testo specificato (`123`). Il resto del testo mantiene il carattere predefinito del piè di pagina.


## Passaggio 7: inserire il numero di pagina al centro del piè di pagina

Inserire i numeri di pagina nel piè di pagina è un ottimo modo per aiutare i lettori a tenere traccia di documenti composti da più pagine.

```csharp
// Inserire il numero di pagina nella sezione centrale del piè di pagina
pageSetup.SetFooter(1, "&P");
```

Qui, `&P` Aggiunge il numero di pagina corrente alla sezione centrale del piè di pagina. È un piccolo dettaglio, ma fondamentale per documenti dall'aspetto professionale.


## Passaggio 8: mostra il conteggio totale delle pagine nella sezione del piè di pagina destro

Infine, completiamo il piè di pagina visualizzando il numero totale di pagine nella sezione giusta.

```csharp
// Visualizza il conteggio totale delle pagine nella sezione destra del piè di pagina
pageSetup.SetFooter(2, "&N");
```

- `&N` fornisce il numero totale delle pagine, consentendo ai lettori di sapere quanto è lungo il documento.


## Passaggio 9: salvare la cartella di lavoro

Dopo aver impostato intestazioni e piè di pagina, è il momento di salvare la cartella di lavoro. Questo è il passaggio finale per generare un file Excel con intestazioni e piè di pagina completamente personalizzati.

```csharp
// Salva la cartella di lavoro
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Questa riga salva il file nella directory designata con le intestazioni e i piè di pagina personalizzati.


## Conclusione

Aggiungere intestazioni e piè di pagina ai fogli di lavoro di Excel è una competenza preziosa per creare documenti organizzati e professionali. Con Aspose.Cells per .NET, hai il controllo completo su intestazioni e piè di pagina dei tuoi file Excel, dalla visualizzazione del nome del foglio di lavoro all'inserimento di testo personalizzato, data, ora e persino numeri di pagina dinamici. Ora che hai visto ogni passaggio in azione, puoi portare l'automazione di Excel a un livello superiore.

## Domande frequenti

### Posso usare font diversi per sezioni diverse di intestazioni e piè di pagina?  
Sì, Aspose.Cells per .NET consente di specificare i font per ogni sezione dell'intestazione e del piè di pagina utilizzando tag font specifici.

### Come faccio a rimuovere intestazioni e piè di pagina?  
È possibile cancellare intestazioni e piè di pagina impostando il testo dell'intestazione o del piè di pagina su una stringa vuota con `SetHeader` O `SetFooter`.

### Posso inserire immagini nelle intestazioni o nei piè di pagina con Aspose.Cells per .NET?  
Attualmente, Aspose.Cells supporta principalmente il testo in intestazioni e piè di pagina. Le immagini potrebbero richiedere una soluzione alternativa, come l'inserimento di immagini nel foglio di lavoro stesso.

### Aspose.Cells supporta dati dinamici nelle intestazioni e nei piè di pagina?  
Sì, puoi utilizzare vari codici dinamici (come `&D` per data o `&P` per il numero di pagina) per aggiungere contenuti dinamici.

### Come posso regolare l'altezza dell'intestazione o del piè di pagina?  
Aspose.Cells fornisce opzioni all'interno di `PageSetup` classe per regolare i margini dell'intestazione e del piè di pagina, dandoti il controllo sulla spaziatura.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}