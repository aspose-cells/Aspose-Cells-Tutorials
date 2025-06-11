---
"description": "Scopri come aggiungere un controllo rettangolo a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET con una guida dettagliata e passo dopo passo."
"linktitle": "Aggiungere il controllo rettangolo al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungere il controllo rettangolo al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere il controllo rettangolo al foglio di lavoro in Excel

## Introduzione
Quando si tratta di automatizzare le attività di Excel, Aspose.Cells per .NET è uno strumento potente che può aiutarti a raggiungere una varietà di obiettivi, uno dei quali è l'aggiunta di forme come rettangoli ai tuoi fogli di lavoro. In questa guida, esploreremo come aggiungere un controllo rettangolo a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Al termine, sarai in grado di creare, personalizzare e salvare un foglio di lavoro con un controllo rettangolo incorporato.
Ma prima di iniziare, parliamo dei prerequisiti.
## Prerequisiti
Per seguire questo tutorial, assicurati di avere i seguenti prerequisiti:
1. Aspose.Cells per la libreria .NET: se non l'hai già fatto, [scarica la libreria](https://releases.aspose.com/cells/net/) oppure installarlo tramite NuGet in Visual Studio.
2. .NET Framework: è necessario che sul computer sia installato l'ambiente di sviluppo .NET.
3. Conoscenza di base di C#: sebbene ti guideremo passo dopo passo, è utile avere familiarità con C# e con la programmazione orientata agli oggetti.
4. Licenza: l'utilizzo di Aspose.Cells in modalità di valutazione funziona bene per le attività di base, ma per la piena funzionalità, si consiglia di prendere in considerazione l'ottenimento di una [licenza temporanea](https://purchase.aspose.com/temporary-license/) o acquistandone uno da [Qui](https://purchase.aspose.com/buy).
Adesso, immergiamoci nel codice!
## Importa pacchetti
Per iniziare a usare Aspose.Cells, assicurati di aver importato gli spazi dei nomi necessari nel tuo progetto. Queste importazioni consentiranno l'accesso a varie classi e metodi necessari per interagire con i file Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Queste linee assicurano che il tuo progetto possa interagire con le directory dei file (`System.IO`), cartelle di lavoro di Excel (`Aspose.Cells`) e disegno di forme (`Aspose.Cells.Drawing`).
Ora scomponiamo il processo in semplici passaggi, così potrai seguirli facilmente e replicarli nei tuoi progetti.
## Passaggio 1: impostazione del percorso della directory
La prima cosa da fare è definire la directory in cui verrà salvato il file Excel. Questo passaggio garantisce che il progetto sappia dove creare e archiviare il file di output.
### Definizione della directory dei dati
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
Qui puoi specificare il percorso della directory in cui verrà archiviato il file Excel. Puoi sostituire `"Your Document Directory"` con il percorso effettivo sul tuo computer oppure crea dinamicamente una cartella se non esiste.
### Controllo e creazione della directory
```csharp
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Questo blocco verifica se la directory esiste. In caso contrario, ne crea una. Immagina di avere il tuo schedario pronto prima di archiviare qualsiasi documento.
## Passaggio 2: creazione di una nuova cartella di lavoro
In questo passaggio, crei una nuova cartella di lavoro di Excel utilizzando `Aspose.Cells.Workbook` classe. Questo servirà da contenitore per il tuo foglio di lavoro e le tue forme.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
Chiamando il `Workbook` costruttore, ora hai una cartella di lavoro Excel vuota pronta per la personalizzazione.
## Passaggio 3: aggiunta di un controllo rettangolo
Ed è qui che avviene la magia. Aggiungerai una forma rettangolare al primo foglio di lavoro della tua cartella di lavoro.
```csharp
// Aggiungere un controllo rettangolare.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Analizziamolo nel dettaglio:
- `excelbook.Worksheets[0]`Questo consente di accedere al primo foglio di lavoro nella cartella di lavoro.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Questo aggiunge un rettangolo al foglio di lavoro. I parametri qui definiscono la posizione (riga e colonna), nonché la larghezza e l'altezza del rettangolo.
## Passaggio 4: personalizzazione del rettangolo
Aggiungere semplicemente un rettangolo non basta: è necessario personalizzarlo. In questo passaggio, imposteremo il posizionamento, lo spessore della linea e lo stile del tratteggio del rettangolo.
### Impostazione del posizionamento
```csharp
// Imposta la posizione del rettangolo.
rectangle.Placement = PlacementType.FreeFloating;
```
Ciò specifica che il rettangolo è mobile, ovvero non sarà vincolato dalle dimensioni delle celle.
### Impostazione dello spessore della linea
```csharp
// Imposta lo spessore della linea.
rectangle.Line.Weight = 4;
```
Qui impostiamo lo spessore della linea del rettangolo a 4 punti. Più alto è il numero, più spessa sarà la linea.
### Impostazione dello stile del trattino
```csharp
// Imposta lo stile del trattino del rettangolo.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Questa linea imposta lo stile del tratteggio del bordo del rettangolo su continuo. Puoi sperimentare diversi stili come `Dash` O `Dot` a seconda delle vostre esigenze.
## Passaggio 5: salvataggio della cartella di lavoro
Una volta aggiunto e personalizzato il rettangolo, il passaggio finale consiste nel salvare la cartella di lavoro nella directory specificata.
```csharp
// Salvare il file Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Questo salva la cartella di lavoro come `.xls` file nella cartella definita in precedenza. È possibile modificare il formato del file cambiando l'estensione, ad esempio `.xlsx` se preferisci il formato Excel più recente.
## Conclusione
Ed ecco fatto! Aggiungere un controllo rettangolo a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET è un processo semplice, una volta spiegato passo dopo passo. Che tu debba aggiungere forme per migliorare l'aspetto grafico, evidenziare sezioni dei dati o personalizzare i report, Aspose.Cells ti offre la flessibilità necessaria per farlo a livello di codice.
Questa guida dovrebbe avervi fornito tutte le conoscenze necessarie per iniziare ad aggiungere forme come rettangoli ai vostri fogli Excel con Aspose.Cells. Ora è il momento di sperimentare e vedere cos'altro potete ottenere con questa potente libreria!
## Domande frequenti
### Posso aggiungere altre forme come cerchi o linee utilizzando Aspose.Cells per .NET?  
Sì, Aspose.Cells consente di aggiungere diverse forme, tra cui cerchi, linee, frecce e altro ancora.
### Quali altre proprietà posso impostare per il controllo rettangolo?  
È possibile personalizzare il colore di riempimento, il colore della linea, la trasparenza e persino aggiungere testo all'interno del rettangolo.
### Aspose.Cells è compatibile con .NET Core?  
Sì, Aspose.Cells supporta .NET Core, nonché .NET Framework e altre piattaforme basate su .NET.
### Posso posizionare il rettangolo rispetto a una cella specifica?  
Sì, puoi posizionare il rettangolo all'interno di righe e colonne specifiche oppure utilizzare il `PlacementType` per controllare il modo in cui è ancorato.
### È disponibile una prova gratuita per Aspose.Cells?  
Sì, puoi ottenere un [prova gratuita](https://releases.aspose.com/) dal sito web per testare le funzionalità della libreria prima di acquistarla.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}