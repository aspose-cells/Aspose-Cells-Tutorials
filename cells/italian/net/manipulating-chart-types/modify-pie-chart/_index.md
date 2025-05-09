---
"description": "Sfrutta la potenza di Aspose.Cells per .NET per modificare i tuoi grafici a torta di Excel senza sforzo. Segui questo tutorial per una guida passo passo."
"linktitle": "Modifica grafico a torta"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Modifica grafico a torta"
"url": "/it/net/manipulating-chart-types/modify-pie-chart/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifica grafico a torta

## Introduzione

Ti sei mai chiesto come abbellire i grafici a torta nei tuoi fogli Excel? I grafici a torta possono essere un modo fantastico per visualizzare i dati, mantenendo il pubblico coinvolto e informato. Tuttavia, a volte questi grafici non raccontano la storia che vorresti che raccontassero fin da subito. È qui che entra in gioco Aspose.Cells per .NET. Questa potente libreria ti permette di manipolare i file Excel a livello di codice, fornendoti gli strumenti necessari per personalizzare i tuoi grafici a torta fin nei minimi dettagli. In questo tutorial, approfondiremo la modifica di un grafico a torta utilizzando Aspose.Cells, che si tratti di cambiare le etichette dei dati o di modificare l'estetica del grafico.

## Prerequisiti

Prima di addentrarci nei dettagli della modifica dei grafici a torta, ecco alcuni prerequisiti che dovresti avere:

- Conoscenza di base di C#: una conoscenza fondamentale della programmazione C# ti aiuterà a seguire facilmente il corso.
- Aspose.Cells per .NET: è necessario avere installata la libreria Aspose.Cells. Che tu decida di utilizzare la versione completa o di optare per una prova gratuita, assicurati che sia pronta all'uso.
- Visual Studio o qualsiasi IDE C#: avrai bisogno di un ambiente in cui scrivere ed eseguire il codice C#.
- File di esempio Excel: per questo tutorial, un file di esempio Excel denominato `sampleModifyPieChart.xlsx` verrà utilizzato.

Puoi scaricare la libreria Aspose.Cells [Qui](https://releases.aspose.com/cells/net/).

## Importa pacchetti

Il primo passo del nostro percorso è importare i pacchetti necessari nel nostro progetto C#. Ecco come fare:

## Imposta il tuo progetto

Per iniziare, apri l'IDE C# (Visual Studio è altamente consigliato) e crea un nuovo progetto:

1. Aprire Visual Studio.
2. Seleziona "Crea un nuovo progetto".
3. Scegliere un'applicazione console C#.
4. Assegna un nome al tuo progetto (ad esempio, `ModifyPieChartDemo`).
5. Fare clic su Crea.

## Installa Aspose.Cells

Una volta che il progetto è pronto, è il momento di aggiungere la libreria Aspose.Cells. Puoi installarla usando NuGet:

1. In "Esplora soluzioni" fai clic con il pulsante destro del mouse sul tuo progetto.
2. Selezionare Gestisci pacchetti NuGet.
3. Passare alla scheda Sfoglia.
4. Cerca Aspose.Cells.
5. Fare clic su Installa e accettare eventuali contratti di licenza.

Ora che hai installato la libreria, importiamo gli spazi dei nomi necessari nel tuo codice.

## Importazione di spazi dei nomi

In cima al tuo `Program.cs` file, importa i seguenti namespace:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Fatto questo, siamo pronti a passare al codice vero e proprio!

## Passaggio 1: definire le directory di input e output

Iniziamo definendo le directory per i file di input e output. Qui puoi specificare dove si trova il file Excel e dove vuoi salvare il file modificato.

Nel tuo `Main` metodo, digita il seguente codice:

```csharp
// Directory di output
string outputDir = "Your Output Directory Path";

// Directory di origine
string sourceDir = "Your Document Directory Path";
```

Assicurati di sostituire `Your Output Directory Path` E `Your Document Directory Path` con i percorsi effettivi del tuo sistema.

## Passaggio 2: aprire la cartella di lavoro esistente

Successivamente, dobbiamo aprire il file Excel contenente il grafico a torta che desideri modificare. Per farlo, utilizza il comando `Workbook` classe:

```csharp
// Aprire il file esistente.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

In questo frammento, stiamo creando un nuovo `Workbook` oggetto e caricando al suo interno il nostro file Excel.

## Passaggio 3: accedi al foglio di lavoro

Ora, analizziamo il foglio specifico che contiene il grafico a torta. Supponiamo che il grafico a torta si trovi nel secondo foglio di lavoro (indice 1):

```csharp
// Prendi la tabella del designer nel secondo foglio.
Worksheet sheet = workbook.Worksheets[1];
```

Accedendo al `Worksheets` raccolta, possiamo arrivare al foglio specifico di cui abbiamo bisogno.

## Passaggio 4: ottenere il grafico

Ora siamo pronti per accedere al grafico stesso. Supponendo che ci sia un solo grafico su quel foglio di lavoro, possiamo recuperarlo direttamente:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Qui prendiamo il primo grafico dal foglio di lavoro specificato.

## Passaggio 5: accedere alle etichette dati

Ora arriva la parte interessante: modificare le etichette dati sul grafico a torta. Accediamo alle etichette dati delle serie di dati:

```csharp
// Ottieni le etichette dei dati nella serie di dati del terzo punto dati.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Con questa linea miriamo specificatamente alle etichette dei dati per il terzo punto della nostra serie di dati. 

## Passaggio 6: modificare il testo dell'etichetta

Ora è il momento di cambiare il testo dell'etichetta. Nel nostro esempio, la aggiorneremo in "Regno Unito, 400K":

```csharp
// Cambia il testo dell'etichetta.
datalabels.Text = "United Kingdom, 400K";
```

Ecco fatto: abbiamo aggiornato l'etichetta! 

## Passaggio 7: salvare la cartella di lavoro

Ora che abbiamo apportato le modifiche, salviamo la cartella di lavoro modificata. 

```csharp
// Salvare il file Excel.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Questa riga salva la cartella di lavoro nella directory di output specificata. 

## Passaggio 8: conferma dell'esecuzione

Infine, pubblichiamo un messaggio di conferma per assicurarci che tutto sia andato liscio:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

Questo ti dà una piccola rassicurazione sul fatto che le modifiche siano state apportate come previsto.

# Conclusione

Ecco fatto! Con pochi semplici passaggi, hai modificato con successo un grafico a torta utilizzando Aspose.Cells per .NET. Questa potente libreria non solo semplifica la manipolazione di file Excel, ma ti permette anche di personalizzare le visualizzazioni dei dati per ottenere il massimo impatto. Se ti occupi di presentazioni di dati nel tuo lavoro, investire tempo nell'apprendimento dell'uso di Aspose.Cells sarà sicuramente utile. Quindi, vai avanti, sperimenta con questi grafici e scopri come puoi dare vita ai tuoi dati!

# Domande frequenti

### Che cos'è Aspose.Cells per .NET?  
Aspose.Cells per .NET è una potente libreria progettata per creare, manipolare e convertire file Excel a livello di programmazione, senza bisogno di Microsoft Excel.

### Posso modificare grafici diversi dai grafici a torta?  
Assolutamente sì! Aspose.Cells supporta vari tipi di grafici, inclusi grafici a barre, a linee e ad area, consentendo una visualizzazione flessibile dei dati.

### Esiste una versione gratuita di Aspose.Cells?  
Sì! Aspose offre una versione di prova gratuita che consente di testare la libreria prima di acquistarla.

### Dove posso trovare supporto per Aspose.Cells?  
Puoi trovare supporto nei forum di Aspose, dove i membri della community e lo staff di Aspose possono aiutarti.

### Per utilizzare Aspose.Cells è necessario avere installato Microsoft Excel?  
No, Aspose.Cells funziona indipendentemente da Microsoft Excel. Non è necessario installarlo sul sistema.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}