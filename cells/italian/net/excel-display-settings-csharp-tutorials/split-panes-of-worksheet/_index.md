---
title: Riquadri divisi del foglio di lavoro
linktitle: Riquadri divisi del foglio di lavoro
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come dividere i riquadri del foglio di lavoro in Aspose.Cells per .NET con la nostra guida passo-passo. Migliora la navigazione nei file Excel con questo semplice tutorial.
weight: 130
url: /it/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riquadri divisi del foglio di lavoro

## Introduzione

Siete pronti a dividere i riquadri di un foglio di lavoro Excel usando Aspose.Cells per .NET? Immaginate questo: avete un gigantesco foglio Excel e siete stanchi di scorrere costantemente indietro fino alle intestazioni solo per ricordare con quale colonna state lavorando. Entrate in "Split Panes". Questa comoda funzionalità vi consente di bloccare una parte del vostro foglio di lavoro, rendendolo molto più facile da navigare. Che stiate lavorando con dati finanziari, gestione dell'inventario o enormi set di dati, la divisione dei riquadri può aumentare la vostra produttività di dieci volte. 

## Prerequisiti

Prima di iniziare a dividere i riquadri come un mago dei fogli di calcolo, impostiamo correttamente la nostra configurazione. Ecco cosa ti servirà:

-  Aspose.Cells per .NET: assicurati di averlo scaricato e installato. Se non l'hai ancora fatto, prendilo[Qui](https://releases.aspose.com/cells/net/).
- .NET Framework: questa guida presuppone che si stia lavorando in un ambiente .NET.
- Una cartella di lavoro di Excel: utilizzeremo un file Excel di esempio per mostrare il funzionamento di questa funzionalità.
-  Una licenza temporanea o completa: Aspose.Cells richiede una licenza. Se lo stai solo provando, procurati una[licenza temporanea gratuita](https://purchase.aspose.com/temporary-license/) per evitare limitazioni di valutazione.

## Importa pacchetti

Prima di immergerci nel codice, importiamo prima i namespace necessari. Non puoi fare nulla in Aspose.Cells senza includerli.

```csharp
using System.IO;
using Aspose.Cells;
```

Ora che abbiamo affrontato le nozioni fondamentali, passiamo alla parte più interessante: la divisione dei vetri!

## Passaggio 1: creare un'istanza di una cartella di lavoro

 Il primo passo di questo processo è la creazione di un`Workbook` object, che rappresenterà il file Excel che vuoi modificare. In questo caso, caricheremo un file da una directory. Questa è la tua tela, il foglio Excel su cui lavorerai la tua magia.

Prima di poter dividere i riquadri, abbiamo bisogno di una cartella di lavoro con cui lavorare! Questo passaggio è essenziale quanto aprire un libro prima di iniziare a leggerlo.

```csharp
// Il percorso verso la directory dei documenti
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Crea una nuova cartella di lavoro e apri un file modello
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Nel codice sopra, sostituisci`"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui si trova il file Excel.`Workbook`la classe carica il file Excel nella memoria.

## Passaggio 2: imposta la cella attiva

 Dopo aver caricato la cartella di lavoro, è il momento di impostare la cella attiva. In termini Excel, la cella attiva è quella attualmente selezionata o in focus. In questo tutorial, selezioneremo la cella`A20` nel primo foglio di lavoro.

Impostare la cella attiva è fondamentale perché la suddivisione del riquadro inizia da questa cella attiva. È come scegliere dove fare il primo taglio in una pizza: scegli la tua fetta!

```csharp
// Imposta la cella attiva
book.Worksheets[0].ActiveCell = "A20";
```

 Questo pezzo di codice rende`A20` la cella attiva. È importante perché la divisione avviene attorno a questo punto, proprio come la navigazione in Excel spesso si concentra attorno a una cella specifica.

## Passaggio 3: dividere il foglio di lavoro

Ora che la cella attiva è impostata, passiamo alla parte divertente: la divisione del foglio di lavoro! Questo è il passaggio in cui avviene la magia. Sarai in grado di dividere il foglio di lavoro in più riquadri per una visualizzazione e una navigazione più semplici.

Questo è il nocciolo dell'intero tutorial. Dividendo il foglio di lavoro, crei riquadri separati che ti consentono di scorrere diverse sezioni del tuo foglio Excel senza perdere di vista le intestazioni o altre aree importanti.

```csharp
// Dividi la finestra del foglio di lavoro
book.Worksheets[0].Split();
```

 Con il`Split()` metodo, stai dicendo ad Aspose.Cells di dividere il foglio di lavoro nella cella attiva (`A20` in questo caso). Da questo punto, Excel crea una divisione nel foglio che separa i riquadri per consentirti di navigare in modo indipendente.

## Passaggio 4: salvare la cartella di lavoro

Dopo aver diviso i riquadri, non resta che salvare il tuo lavoro. Questo passaggio finale assicurerà che le tue modifiche vengano salvate nel file di output specificato.

A cosa serve tutto il tuo duro lavoro se non lo salvi? Il salvataggio assicura che i tuoi vetri splendidamente divisi rimangano intatti per un uso futuro.

```csharp
// Salvare il file Excel
book.Save(dataDir + "output.xls");
```

 Qui, il`Save()` il metodo salva la cartella di lavoro con i riquadri appena divisi in un file Excel di output. Le modifiche apportate sono ora pronte per essere utilizzate da te o da chiunque altro.

## Conclusione

Ed ecco fatto! Hai appena imparato a dividere i riquadri in un foglio di lavoro Excel usando Aspose.Cells per .NET. Niente più scorrimento infinito o perdita di traccia dei dati. Questo metodo rende la gestione di file Excel di grandi dimensioni molto meno opprimente e molto più efficiente. Con la possibilità di dividere i riquadri, ora puoi tenere traccia dei punti dati critici mentre lavori con fogli di calcolo complessi.

## Domande frequenti

### Posso dividere più di due vetri?  
 Sì, puoi dividere il foglio di lavoro in più riquadri specificando celle attive diverse e chiamando il`Split()` metodo.

### Qual è la differenza tra vetri rotti e vetri congelati?  
Dividere i riquadri consente di scorrere in entrambi i riquadri in modo indipendente. Bloccare i riquadri blocca le intestazioni o righe/colonne specifiche in modo che rimangano visibili durante lo scorrimento.

### Posso rimuovere la spaccatura dopo averla applicata?  
Sì, puoi rimuovere la suddivisione chiudendo e riaprendo la cartella di lavoro oppure reimpostandola a livello di programmazione.

### La suddivisione dei riquadri funziona allo stesso modo per diversi formati di file Excel (XLS, XLSX)?  
 Sì, il`Split()` Il metodo funziona sia per i formati XLS che XLSX.

### Posso usare Aspose.Cells senza licenza?  
 Sì, ma ha delle limitazioni. Per un'esperienza completa, è meglio usare un[temporaneo](https://purchase.aspose.com/temporary-license/) O[licenza a pagamento](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
