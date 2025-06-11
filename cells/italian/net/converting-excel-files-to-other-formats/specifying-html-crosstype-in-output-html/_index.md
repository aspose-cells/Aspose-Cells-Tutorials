---
"description": "Scopri come specificare HTML CrossType in Aspose.Cells per .NET. Segui il nostro tutorial passo passo per convertire i file Excel in HTML con precisione."
"linktitle": "Specificare HTML CrossType nell'output HTML a livello di programmazione in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Specificare HTML CrossType nell'output HTML a livello di programmazione in .NET"
"url": "/it/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specificare HTML CrossType nell'output HTML a livello di programmazione in .NET

## Introduzione
Quando si convertono file Excel in HTML in applicazioni .NET, potrebbe essere necessario specificare come gestire i riferimenti incrociati nell'output. La classe HtmlSaveOptions in Aspose.Cells per .NET fornisce diverse impostazioni per controllare il processo di conversione, e una di queste è HtmlCrossType. In questo tutorial, spiegheremo come specificare a livello di codice il cross-type HTML durante l'esportazione di file Excel in formato HTML. 
## Prerequisiti
Prima di immergerti nel codice, assicurati di avere quanto segue:
- Aspose.Cells per .NET: assicurati di aver installato la libreria Aspose.Cells nel tuo progetto. Puoi scaricarla da [Sito web di Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: un'installazione funzionante di Visual Studio o di qualsiasi altro ambiente di sviluppo .NET.
- Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio gli esempi.
- File Excel di esempio: tieni pronto un file Excel di esempio con cui lavorare. Per questo esempio, useremo `sampleHtmlCrossStringType.xlsx`.
## Importa pacchetti
Per iniziare, devi importare gli spazi dei nomi Aspose.Cells necessari. Ecco come fare:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Analizziamo il tutto passo dopo passo, così sarà più semplice per te seguirlo e implementare questa funzionalità nei tuoi progetti.
## Passaggio 1: definire le directory di origine e di output
Per prima cosa, devi impostare le directory per il file Excel di origine e dove desideri salvare il file HTML di output.
```csharp
// Directory di origine
string sourceDir = "Your Document Directory";
// Directory di output
string outputDir = "Your Document Directory";
```
## Passaggio 2: caricare il file Excel di esempio
Quindi, carica il tuo file Excel di esempio in un `Workbook` oggetto. È qui che inizia tutta la magia.
```csharp
// Carica il file Excel di esempio
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Qui, sostituisci `"Your Document Directory"` Con il percorso effettivo in cui si trova il file Excel. Questa riga legge il file Excel in memoria in modo da poterlo manipolare.
## Passaggio 3: specificare le opzioni di salvataggio HTML
Ora creeremo un'istanza di `HtmlSaveOptions`, che consente di configurare il modo in cui il file Excel verrà convertito in HTML.
```csharp
// Specificare il tipo incrociato HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
In questo passaggio abbiamo impostato il `HtmlCrossStringType` A `HtmlCrossType.Default`, che è una delle opzioni disponibili per gestire i riferimenti incrociati nell'HTML di output.
## Passaggio 4: modificare il tipo di croce secondo necessità
È possibile specificare diversi tipi per `HtmlCrossStringType` in base alle tue esigenze. Ecco le diverse opzioni che puoi utilizzare:
- `HtmlCrossType.Default`: Il tipo di croce predefinito.
- `HtmlCrossType.MSExport`: Esporta l'HTML con un comportamento simile a quello di MS Excel.
- `HtmlCrossType.Cross`: Crea riferimenti incrociati.
- `HtmlCrossType.FitToCell`Adatta i riferimenti incrociati alle dimensioni della cella.
Puoi modificare il `HtmlCrossStringType` in questo modo:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpOt;
// O 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Passaggio 5: salvare il file HTML di output
Una volta configurate le opzioni, è il momento di salvare il file HTML convertito. Utilizzare il `Save` metodo sul tuo `Workbook` oggetto:
```csharp
// HTML di output
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Qui, stiamo nominando il file di output in base a `HtmlCrossStringType` che abbiamo impostato. In questo modo, puoi identificare facilmente quale tipo di croce è stato utilizzato nella conversione.
## Passaggio 6: Confermare l'esecuzione corretta
Infine, è sempre buona norma confermare che l'operazione sia andata a buon fine. È possibile visualizzare un messaggio sulla console:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Questo ti farà sapere che il processo è stato completato senza errori.
## Conclusione
Ed ecco fatto! Hai specificato correttamente il cross-type HTML per l'esportazione Excel in .NET utilizzando Aspose.Cells. Questa funzionalità è particolarmente utile quando è necessario mantenere formattazioni o riferimenti specifici nell'output HTML, garantendo che i documenti convertiti soddisfino i requisiti.
## Domande frequenti
### Che cos'è HtmlCrossType in Aspose.Cells?  
HtmlCrossType definisce come gestire i riferimenti incrociati nel file Excel durante la conversione HTML. È possibile scegliere opzioni come Default, MSExport, Cross e FitToCell.
### Posso usare Aspose.Cells gratuitamente?  
Aspose.Cells offre una versione di prova gratuita. Puoi scaricarla dal loro [sito web](https://releases.aspose.com/).
### Come faccio a installare Aspose.Cells nel mio progetto .NET?  
È possibile installare Aspose.Cells tramite NuGet Package Manager in Visual Studio eseguendo il comando: `Install-Package Aspose.Cells`.
### Dove posso trovare la documentazione per Aspose.Cells?  
Puoi trovare una documentazione completa su Aspose.Cells [Qui](https://reference.aspose.com/cells/net/).
### Cosa devo fare se riscontro un errore durante il salvataggio del file HTML?  
Assicurati che i percorsi delle directory siano corretti e di disporre dei permessi di scrittura per la directory di output. Se il problema persiste, consulta il forum di supporto di Aspose per assistenza.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}