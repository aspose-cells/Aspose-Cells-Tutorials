---
"description": "Scopri come estrarre il testo da un elemento SmartArt a forma di ingranaggio in Excel utilizzando Aspose.Cells per .NET. Guida dettagliata ed esempio di codice inclusi."
"linktitle": "Estrarre il testo da SmartArt di tipo ingranaggio in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Estrarre il testo da SmartArt di tipo ingranaggio in Excel"
"url": "/it/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre il testo da SmartArt di tipo ingranaggio in Excel

## Introduzione
Lavorando con Excel, potreste imbattervi in elementi grafici SmartArt che vi aiutano a trasmettere i vostri messaggi in modo visivamente accattivante. Tra questi, gli elementi grafici SmartArt a forma di ingranaggio sono molto apprezzati per i loro flussi gerarchici e direzionali, spesso utilizzati nella gestione dei progetti o nella modellazione di sistemi. Ma cosa succede se avete bisogno di estrarre testo da queste forme a livello di codice? È qui che Aspose.Cells per .NET torna utile! In questo articolo del blog, vi guideremo passo passo su come estrarre testo da forme SmartArt a forma di ingranaggio in Excel utilizzando Aspose.Cells per .NET.
## Prerequisiti
Prima di iniziare, ci sono alcuni prerequisiti essenziali che devi avere. Non preoccuparti: è semplice e ti guiderò passo passo.
### Ambiente .NET
Assicurati di avere un ambiente di sviluppo .NET installato sul tuo computer. Potrebbe essere Visual Studio o qualsiasi IDE di tua scelta che supporti lo sviluppo .NET.
### Aspose.Cells per .NET
Successivamente, dovrai installare la libreria Aspose.Cells. Questa è la potenza che ti permetterà di manipolare i file Excel senza problemi. Puoi scaricarla da [Pagina delle versioni di Aspose](https://releases.aspose.com/cells/net/)Se vuoi esplorarlo prima, approfitta del [prova gratuita](https://releases.aspose.com/).
### Conoscenza di base di C#
Una conoscenza di base della programmazione in C# è proprio ciò di cui hai bisogno per seguire questo tutorial. Se sei alle prime armi, non preoccuparti: progetterò i passaggi in modo che siano il più possibile intuitivi per i principianti.
### Esempio di file Excel
Per questo tutorial, avrai anche bisogno di un file Excel di esempio contenente forme SmartArt a forma di ingranaggio. Puoi crearne facilmente uno o trovare un modello online. Assicurati solo che la SmartArt includa almeno una forma a forma di ingranaggio.
## Importa pacchetti
Per iniziare a programmare, dovrai importare i pacchetti necessari. Ecco come fare:
### Crea un nuovo progetto
1. Apri l'IDE .NET.
2. Crea un nuovo progetto. Ad esempio, seleziona "Applicazione console" nelle opzioni .NET.
3. Assegna un nome al tuo progetto e imposta il framework desiderato. 
### Aggiungi riferimenti
Per utilizzare Aspose.Cells, dovrai aggiungere i riferimenti alla libreria al tuo progetto:
1. Fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni.
2. Seleziona “Gestisci pacchetti NuGet”.
3. Cerca "Aspose.Cells" e installalo.
Una volta installato, sei pronto per iniziare a programmare!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ora analizziamo il codice che userai per estrarre il testo. Lo faremo passo dopo passo.
## Passaggio 1: impostare la directory di origine
Iniziamo definendo la directory in cui si trova il file Excel:
```csharp
// Directory di origine
string sourceDir = "Your Document Directory";
```
Assicurati di sostituire `"Your Document Directory"` con il percorso effettivo del file Excel.
## Passaggio 2: caricare la cartella di lavoro di Excel
Successivamente, caricheremo la cartella di lavoro di Excel. Ecco come possiamo accedervi:
```csharp
// Carica il file Excel di esempio contenente la forma artistica intelligente del tipo ingranaggio.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Questo pezzo caricherà la tua cartella di lavoro Excel di esempio.
## Passaggio 3: accedi al primo foglio di lavoro
Ora che abbiamo caricato la cartella di lavoro, accediamo al primo foglio di lavoro in cui è presente il nostro SmartArt:
```csharp
// Accedi al primo foglio di lavoro.
Worksheet ws = wb.Worksheets[0];
```
In questo modo viene recuperato il primo foglio di lavoro per ulteriori elaborazioni.
## Passaggio 4: accedi alla prima forma
Successivamente, dobbiamo accedere alla prima forma del nostro foglio di lavoro. In questo modo, possiamo navigare tra i nostri elementi grafici SmartArt:
```csharp
// Accedi prima alla forma.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Qui ci concentriamo sulla prima forma, che supponiamo sia lo SmartArt di cui abbiamo bisogno.
## Passaggio 5: Ottieni la forma del gruppo
Una volta ottenuta la forma, è il momento di ottenere il risultato della nostra rappresentazione SmartArt:
```csharp
// Ottieni il risultato della forma artistica intelligente del tipo di ingranaggio sotto forma di forma di gruppo.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
In questo modo il nostro SmartArt di tipo ingranaggio viene recuperato come forma raggruppata.
## Passaggio 6: Estrarre le singole forme
Ora estraiamo le singole forme che compongono il nostro SmartArt:
```csharp
// Ottieni l'elenco delle singole forme costituite da forme di gruppo.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Questo array conterrà tutte le singole forme che dobbiamo esplorare in loop.
## Passaggio 7: Estrarre e stampare il testo
Infine, possiamo scorrere il nostro array di forme ed estrarre il testo da qualsiasi forma di tipo ingranaggio:
```csharp
// Estrarre il testo delle forme di tipo ingranaggio e stamparlo sulla console.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
In questo ciclo controlliamo il tipo di forma e stampiamo il testo se si tratta di una forma di tipo ingranaggio.
## Fase 8: Conferma dell'esecuzione
Infine, potresti voler aggiungere un messaggio di conferma una volta completato correttamente il processo:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
A questo punto l'estrazione è completa e dovresti vedere il testo in output nella console!
## Conclusione
Congratulazioni! Hai appena imparato a estrarre testo da forme SmartArt a forma di ingranaggio in Excel utilizzando Aspose.Cells per .NET. Questa pratica tecnica apre le porte all'automazione di report o documentazione basati sulla rappresentazione visiva dei dati. Che tu sia uno sviluppatore esperto o alle prime armi, controllare ed estrarre informazioni da SmartArt può semplificare il tuo flusso di lavoro e renderti più efficiente. Non dimenticare di esplorare la guida dettagliata. [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) per ulteriori funzionalità.
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una libreria .NET che consente agli sviluppatori di creare e manipolare facilmente file Excel.
### Posso usare Aspose.Cells con altri linguaggi?
Sì! Aspose.Cells è disponibile in diversi linguaggi di programmazione, tra cui Java e Python.
### Devo acquistare Aspose.Cells per .NET?
Aspose.Cells offre una prova gratuita, ma per un utilizzo prolungato è richiesto un acquisto. Puoi trovare le opzioni di acquisto. [Qui](https://purchase.aspose.com/buy).
### È disponibile supporto per gli utenti di Aspose.Cells?
Assolutamente! Puoi trovare supporto dalla comunità su [Forum di Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Posso estrarre altri tipi di SmartArt utilizzando questo metodo?
Sì, con piccole modifiche puoi estrarre il testo da varie forme SmartArt cambiando le condizioni nel codice.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}