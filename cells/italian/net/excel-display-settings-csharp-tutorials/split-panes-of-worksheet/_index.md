---
"description": "Scopri come dividere i riquadri del foglio di lavoro in Aspose.Cells per .NET con la nostra guida passo passo. Migliora la navigazione nei file Excel con questo semplice tutorial."
"linktitle": "Riquadri divisi del foglio di lavoro"
"second_title": "Riferimento API Aspose.Cells per .NET"
"title": "Riquadri divisi del foglio di lavoro"
"url": "/it/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Riquadri divisi del foglio di lavoro

## Introduzione

Siete pronti a dividere i riquadri di un foglio di lavoro Excel usando Aspose.Cells per .NET? Immaginate questo: avete un gigantesco foglio di lavoro Excel e siete stanchi di dover scorrere continuamente fino alle intestazioni solo per ricordare con quale colonna state lavorando. Ecco "Dividi riquadri". Questa pratica funzione vi permette di bloccare una porzione del foglio di lavoro, rendendolo molto più facile da navigare. Che stiate lavorando con dati finanziari, gestione dell'inventario o set di dati di grandi dimensioni, la suddivisione dei riquadri può aumentare la vostra produttività di dieci volte. 

## Prerequisiti

Prima di iniziare a dividere i riquadri come un mago dei fogli di calcolo, impostiamo correttamente la configurazione. Ecco cosa ti servirà:

- Aspose.Cells per .NET: assicurati di averlo scaricato e installato. Se non l'hai ancora fatto, scaricalo. [Qui](https://releases.aspose.com/cells/net/).
- .NET Framework: questa guida presuppone che tu stia lavorando in un ambiente .NET.
- Una cartella di lavoro di Excel: utilizzeremo un file Excel di esempio per mostrare il funzionamento di questa funzionalità.
- Licenza temporanea o completa: Aspose.Cells richiede una licenza. Se lo stai solo provando, procuratene una [licenza temporanea gratuita](https://purchase.aspose.com/temporary-license/) per evitare limitazioni di valutazione.

## Importa pacchetti

Prima di immergerci nel codice, importiamo i namespace necessari. Non è possibile fare nulla in Aspose.Cells senza includerli.

```csharp
using System.IO;
using Aspose.Cells;
```

Ora che abbiamo affrontato gli aspetti essenziali, passiamo alla parte emozionante: la divisione dei vetri!

## Passaggio 1: creare un'istanza di una cartella di lavoro

Il primo passo di questo processo è la creazione di un `Workbook` oggetto, che rappresenterà il file Excel che desideri modificare. In questo caso, caricheremo un file da una directory. Questa sarà la tua tela, il foglio Excel su cui lavorerai la tua magia.

Prima di poter dividere i riquadri, abbiamo bisogno di una cartella di lavoro con cui lavorare! Questo passaggio è essenziale quanto aprire un libro prima di iniziare a leggerlo.

```csharp
// Il percorso verso la directory dei documenti
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Crea una nuova cartella di lavoro e apri un file modello
Workbook book = new Workbook(dataDir + "Book1.xls");
```

Nel codice sopra, sostituisci `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui si trova il file Excel. Il `Workbook` la classe carica il file Excel nella memoria.

## Passaggio 2: imposta la cella attiva

Dopo aver caricato la cartella di lavoro, è il momento di impostare la cella attiva. In termini di Excel, la cella attiva è quella attualmente selezionata o in evidenza. In questo tutorial, selezioneremo la cella `A20` nel primo foglio di lavoro.

Impostare la cella attiva è fondamentale perché la suddivisione del riquadro inizia da questa cella attiva. È come scegliere dove fare il primo taglio in una pizza: scegli la tua fetta!

```csharp
// Imposta la cella attiva
book.Worksheets[0].ActiveCell = "A20";
```

Questo pezzo di codice rende `A20` la cella attiva. È importante perché la divisione avviene attorno a questo punto, proprio come la navigazione in Excel spesso si concentra su una cella specifica.

## Passaggio 3: dividere il foglio di lavoro

Ora che la cella attiva è impostata, passiamo alla parte divertente: la suddivisione del foglio di lavoro! Questo è il passaggio in cui avviene la magia. Potrai suddividere il foglio di lavoro in più riquadri per una visualizzazione e una navigazione più semplici.

Questo è il fulcro dell'intero tutorial. Dividendo il foglio di lavoro, si creano riquadri separati che consentono di scorrere le diverse sezioni del foglio Excel senza perdere di vista le intestazioni o altre aree importanti.

```csharp
// Dividi la finestra del foglio di lavoro
book.Worksheets[0].Split();
```

Con il `Split()` metodo, stai dicendo ad Aspose.Cells di dividere il foglio di lavoro nella cella attiva (`A20` in questo caso). Da questo punto, Excel crea una divisione nel foglio che separa i riquadri in modo da poterli esplorare in modo indipendente.

## Passaggio 4: salvare la cartella di lavoro

Dopo aver suddiviso i riquadri, non resta che salvare il lavoro. Questo passaggio finale garantirà che le modifiche vengano salvate nel file di output specificato.

cosa serve tutto il tuo duro lavoro se non lo conservi? Conservare i tuoi splendidi vetri tagliati assicura che rimangano intatti per un uso futuro.

```csharp
// Salvare il file Excel
book.Save(dataDir + "output.xls");
```

Qui, il `Save()` Il metodo salva la cartella di lavoro con i riquadri appena divisi in un file Excel di output. Le modifiche apportate sono ora pronte per essere utilizzate da te o da chiunque altro.

## Conclusione

Ed ecco fatto! Hai appena imparato a dividere i riquadri in un foglio di lavoro Excel usando Aspose.Cells per .NET. Niente più scorrimenti infiniti o perdita di traccia dei dati. Questo metodo rende la gestione di file Excel di grandi dimensioni molto meno impegnativa e molto più efficiente. Grazie alla possibilità di dividere i riquadri, ora puoi tenere traccia dei punti dati critici mentre lavori con fogli di calcolo complessi.

## Domande frequenti

### Posso dividere più di due vetri?  
Sì, puoi dividere il foglio di lavoro in più riquadri specificando celle attive diverse e chiamando il `Split()` metodo.

### Qual è la differenza tra vetri rotti e vetri congelati?  
La suddivisione dei riquadri consente di scorrere in modo indipendente in entrambi i riquadri. Il blocco dei riquadri blocca le intestazioni o righe/colonne specifiche in modo che rimangano visibili durante lo scorrimento.

### Posso rimuovere la spaccatura dopo averla applicata?  
Sì, puoi rimuovere la suddivisione chiudendo e riaprendo la cartella di lavoro oppure reimpostandola a livello di programmazione.

### La divisione dei riquadri funziona allo stesso modo per diversi formati di file Excel (XLS, XLSX)?  
Sì, il `Split()` Il metodo funziona sia per i formati XLS che XLSX.

### Posso usare Aspose.Cells senza licenza?  
Sì, ma ha delle limitazioni. Per un'esperienza completa, è meglio usare un [temporaneo](https://purchase.aspose.com/tempOary-license/) or [licenza a pagamento](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}