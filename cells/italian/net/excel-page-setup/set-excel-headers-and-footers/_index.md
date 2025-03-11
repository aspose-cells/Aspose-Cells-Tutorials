---
title: Imposta intestazioni e piè di pagina di Excel
linktitle: Imposta intestazioni e piè di pagina di Excel
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come impostare facilmente intestazioni e piè di pagina di Excel usando Aspose.Cells per .NET con la nostra guida passo-passo. Perfetto per documenti professionali.
weight: 100
url: /it/net/excel-page-setup/set-excel-headers-and-footers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta intestazioni e piè di pagina di Excel

## Introduzione

Quando si tratta di gestire documenti di fogli di calcolo, intestazioni e piè di pagina svolgono un ruolo cruciale nel fornire contesto. Immagina di aprire un file Excel e, proprio in alto, vedi il nome del foglio di lavoro, la data e forse anche il nome del file. Ciò conferisce al tuo documento un tocco professionale e aiuta a comunicare dettagli importanti a colpo d'occhio. Se stai cercando di migliorare la professionalità dei tuoi fogli Excel utilizzando Aspose.Cells per .NET, sei arrivato nel posto giusto! In questa guida, ti guideremo attraverso i passaggi per impostare intestazioni e piè di pagina nei tuoi fogli di calcolo Excel senza sforzo. 

## Prerequisiti

Prima di addentrarci nei dettagli, assicuriamoci che tu abbia tutto ciò che ti serve per iniziare. Per prima cosa, ti serviranno:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. È qui che scriverai ed eseguirai il tuo codice C#.
2.  Aspose.Cells per la libreria .NET: devi avere la libreria Aspose.Cells. Se non l'hai ancora fatto, puoi scaricarla da[Qui](https://releases.aspose.com/cells/net/).
3. Conoscenza di base del linguaggio C#: la familiarità con la programmazione in C# è fondamentale, poiché tutti gli esempi di codice saranno in questo linguaggio.
4. Impostazione del progetto: crea un nuovo progetto C# in Visual Studio in cui implementeremo la logica di intestazione/piè di pagina di Excel.

Una volta confermati i prerequisiti di cui sopra, è il momento di sporcarsi le mani!

## Importa pacchetti

Per iniziare a lavorare con Aspose.Cells, è necessario importare gli spazi dei nomi appropriati nel codice C#.

### Apri il tuo progetto C#

Apri il tuo progetto in Visual Studio dove desideri implementare le impostazioni di intestazione e piè di pagina. Assicurati di avere una struttura chiara che possa ospitare il tuo codice.

### Aggiungi riferimento a Aspose.Cells

Dopo aver creato o aperto il tuo progetto, devi aggiungere un riferimento alla libreria Aspose.Cells. Fai clic con il pulsante destro del mouse sul tuo progetto in Solution Explorer, seleziona "Manage NuGet Packages" e cerca 'Aspose.Cells'. Installalo nel tuo progetto.

### Importa lo spazio dei nomi

Nella parte superiore del file C#, aggiungi la seguente riga per importare lo spazio dei nomi Aspose.Cells:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importando questo namespace è possibile utilizzare le funzionalità fornite dalla libreria Aspose.Cells senza alcuna limitazione.

Ottimo! Ora che il tuo ambiente è impostato e i tuoi pacchetti sono importati, analizziamo passo dopo passo il processo di impostazione di intestazioni e piè di pagina in Excel.

## Passaggio 1: inizializzare la cartella di lavoro

Per prima cosa, dobbiamo creare un'istanza di un oggetto Workbook, che rappresenta il nostro file Excel in memoria.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

 Spiegazione: qui, sostituisci`YOUR DOCUMENT DIRECTORY` con il percorso effettivo in cui desideri salvare il file Excel. Il`Workbook` L'oggetto è il punto di accesso principale per la creazione e la manipolazione dei file Excel.

## Passaggio 2: ottenere il riferimento di PageSetup

 Successivamente, dobbiamo accedere al`PageSetup` proprietà del foglio di lavoro in cui vogliamo impostare intestazioni e piè di pagina.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Spiegazione: Stiamo accedendo al primo foglio di lavoro (indice`0` ) del nostro quaderno di lavoro. Il`PageSetup` La classe fornisce proprietà e metodi per personalizzare l'aspetto della pagina una volta stampata, comprese intestazioni e piè di pagina.

## Passaggio 3: imposta l'intestazione

Ora, iniziamo a impostare l'intestazione. Inizieremo con la sezione di sinistra:

```csharp
pageSetup.SetHeader(0, "&A");
```

 Spiegazione: Il`SetHeader` metodo ci consente di definire il contenuto dell'intestazione. Qui,`&A` indica il nome del foglio di lavoro, che apparirà sul lato sinistro dell'intestazione.

## Passaggio 4: personalizzare l'intestazione centrale

Successivamente personalizzeremo l'intestazione centrale per visualizzare la data e l'ora correnti in un font specifico.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

 Spiegazione: Il`&D` E`&T` i codici si sostituiranno automaticamente con la data e l'ora correnti, rispettivamente. Stiamo anche specificando che il font per questa intestazione deve essere "Times New Roman" e grassetto.

## Passaggio 5: imposta l'intestazione corretta

Impostiamo ora la sezione giusta dell'intestazione per visualizzare il nome del file.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

 Spiegazione: Qui,`&F` verrà sostituito dal nome del file. Utilizziamo lo stesso font che abbiamo usato per l'intestazione centrale per mantenere un aspetto coerente.

## Passaggio 6: Configurare il piè di pagina

Ora che le nostre intestazioni hanno un aspetto sgargiante, volgiamo la nostra attenzione ai piè di pagina. Inizieremo con il piè di pagina sinistro:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Spiegazione: Stiamo inserendo un messaggio personalizzato nel piè di pagina sinistro, "Hello World!" insieme al testo`123` in uno stile di carattere diverso: Courier New.

## Passaggio 7: Configurazione del piè di pagina centrale

Successivamente, impostiamo il piè di pagina centrale per visualizzare il numero di pagina corrente:

```csharp
pageSetup.SetFooter(1, "&P");
```

 Spiegazione: Il`&P` il codice inserisce automaticamente il numero di pagina al centro del piè di pagina: un modo pratico per tenere traccia delle pagine.

## Passaggio 8: Configurazione del piè di pagina destro

Per completare le impostazioni del piè di pagina, impostiamo il piè di pagina destro in modo che mostri il numero totale di pagine del documento.

```csharp
pageSetup.SetFooter(2, "&N");
```

 Spiegazione: Qui,`&N` verrà sostituito dal numero totale di pagine. Aggiunge un tocco professionale, soprattutto per i documenti più lunghi.

## Passaggio 9: Salvare la cartella di lavoro

Una volta impostato tutto, non ti resta che salvare la cartella di lavoro per vedere i frutti del tuo lavoro.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

 Spiegazione: Sostituisci`"SetHeadersAndFooters_out.xls"` con il nome file desiderato. Salva la tua cartella di lavoro e hai finito!

## Conclusione

Ed ecco fatto! Impostare intestazioni e piè di pagina in Excel usando Aspose.Cells per .NET è semplice se segui questi passaggi. Non solo hai migliorato l'aspetto del tuo documento, ma ne hai anche migliorato la funzionalità fornendo un contesto importante. Che tu stia preparando report, condividendo modelli o semplicemente organizzando i tuoi dati, intestazioni e piè di pagina aggiungono un tocco professionale difficile da battere. Quindi, provalo e scopri quanto è facile gestire i tuoi documenti Excel con questa potente libreria!

## Domande frequenti

### Che cos'è Aspose.Cells?
Aspose.Cells è una libreria .NET utilizzata per creare, manipolare e visualizzare file Excel a livello di programmazione.

### Posso provare Aspose.Cells gratuitamente?
 Sì! Puoi scaricare una prova gratuita da[Qui](https://releases.aspose.com/).

### Aspose.Cells è compatibile con i vecchi formati Excel?
Assolutamente! Aspose.Cells supporta sia i vecchi che i nuovi formati di file Excel.

### Dove posso trovare ulteriore documentazione?
 Puoi controllare la documentazione dettagliata su[Documentazione Aspose.Cells](https://reference.aspose.com/cells/net/).

### Come posso ottenere supporto per Aspose.Cells?
 Per supporto, visita il[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
