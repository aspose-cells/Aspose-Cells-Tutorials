---
"description": "Scopri come aggiungere un ovale a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Guida passo passo con spiegazioni dettagliate del codice."
"linktitle": "Aggiungi ovale al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungi ovale al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi ovale al foglio di lavoro in Excel

## Introduzione
Creare file Excel accattivanti e interattivi può richiedere molto più che numeri e formule. Forme come gli ovali possono aggiungere un tocco di appeal visivo o fornire elementi funzionali ai fogli di lavoro. In questo tutorial, esploreremo come utilizzare Aspose.Cells per .NET per aggiungere ovali a un foglio di lavoro Excel tramite codice. Che tu voglia aggiungere un tocco di stile o funzionalità, abbiamo una guida passo passo che ti aiuterà a farlo.
## Prerequisiti
Prima di immergerti nel codice, ecco alcune cose che devi sapere:
1. Aspose.Cells per la libreria .NET: puoi scaricarla da [Qui](https://releases.aspose.com/cells/net/) oppure installarlo tramite NuGet in Visual Studio.
2. Ambiente di sviluppo: AC# IDE come Visual Studio.
3. Nozioni di base di C#: è necessario avere familiarità con i concetti di codifica di base in C#.
Ricordati inoltre di configurare il tuo progetto installando la libreria Aspose.Cells per .NET. Se non hai ancora una licenza, puoi richiederne una [licenza temporanea](https://purchase.aspose.com/temporary-license/) oppure utilizzare il [prova gratuita](https://releases.aspose.com/) versione.
## Importa pacchetti
Prima di scrivere qualsiasi codice, assicurati di aver incluso gli spazi dei nomi richiesti. Ecco un frammento di codice C# per assicurarti di utilizzare le librerie corrette:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Passaggio 1: imposta la tua directory
Il primo passo per aggiungere un ovale a un foglio Excel è specificare dove verrà salvato il file Excel. Definiamo il percorso della directory e assicuriamoci che la directory esista prima di salvare il nostro lavoro.

Creeremo un percorso di directory e verificheremo se esiste. Se la cartella non esiste, verrà creata.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Questo passaggio è fondamentale perché garantisce che il file venga salvato nella posizione corretta e che in seguito non si riscontrino problemi con il percorso del file.
## Passaggio 2: inizializzare una nuova cartella di lavoro
Successivamente, dobbiamo creare una nuova cartella di lavoro in cui aggiungeremo le nostre forme ovali. La cartella di lavoro rappresenta un file Excel e possiamo aggiungervi contenuti o forme.

In questo passaggio, creiamo un nuovo `Workbook` oggetto che fungerà da contenitore dei file Excel.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
## Passaggio 3: aggiungere la prima forma ovale
Ora arriva la parte divertente: aggiungere un ovale al foglio di lavoro. Questo ovale potrebbe rappresentare un elemento visivo come un pulsante o un'evidenziazione. Inizieremo aggiungendo il primo ovale al primo foglio di lavoro della nostra cartella di lavoro.

Qui utilizziamo il `Shapes.AddOval()` Metodo per creare un ovale sul foglio di lavoro in una riga e colonna specifiche.
```csharp
// Aggiungere una forma ovale.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
I parametri all'interno `AddOval()` sono i seguenti:
- I primi due numeri rappresentano la riga e la colonna dell'angolo in alto a sinistra dell'ovale.
- I due numeri successivi rappresentano l'altezza e la larghezza dell'ovale.
## Passaggio 4: imposta il posizionamento e lo stile dell'ovale
Una volta creato l'ovale, possiamo impostarne la posizione, lo spessore della linea e lo stile del trattino. `Placement` La proprietà determina il comportamento dell'ovale quando si ridimensionano o si spostano le celle nel foglio di lavoro.

Rendiamo l'ovale libero e ne modifichiamo l'aspetto.
```csharp
// Imposta la posizione dell'ovale.
oval1.Placement = PlacementType.FreeFloating;
// Imposta lo spessore della linea.
oval1.Line.Weight = 1;
// Imposta lo stile del trattino dell'ovale.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ciò consente all'ovale di muoversi liberamente all'interno del foglio di lavoro e lo spessore e lo stile della sua linea sono impostati per garantire coerenza visiva.
## Passaggio 5: aggiungere un'altra forma ovale (cerchio)
Perché fermarsi a uno solo? In questo passaggio, aggiungeremo un altro ovale, questa volta creando un cerchio perfetto mantenendo invariate altezza e larghezza.

Creiamo un altro ovale, lo posizioniamo in un punto diverso e assicuriamoci che abbia una forma circolare impostando altezza e larghezza uguali.
```csharp
// Aggiungere un'altra forma ovale (cerchio).
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Passaggio 6: modella il secondo ovale
Proprio come prima, regoleremo il posizionamento, il peso e lo stile del trattino di questo secondo ovale (o cerchio).

Applichiamo proprietà simili al secondo ovale per abbinarlo allo stile del primo.
```csharp
// Imposta la posizione dell'ovale.
oval2.Placement = PlacementType.FreeFloating;
// Imposta lo spessore della linea.
oval2.Line.Weight = 1;
// Imposta lo stile del trattino dell'ovale.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Passaggio 7: salvare la cartella di lavoro
Infine, dobbiamo salvare la cartella di lavoro con gli ovali appena aggiunti. Salvare il file garantisce che tutte le modifiche vengano salvate.

Salviamo la cartella di lavoro nel percorso della directory definito in precedenza.
```csharp
// Salvare il file Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Ed ecco fatto! Hai aggiunto con successo gli ovali al tuo foglio di lavoro Excel e salvato il file.
## Conclusione
Aggiungere forme come gli ovali a un foglio Excel utilizzando Aspose.Cells per .NET non è solo semplice, ma anche un modo divertente per arricchire i fogli di calcolo con elementi visivi aggiuntivi. Che si tratti di design o di aggiungere elementi cliccabili, le forme possono svolgere un ruolo significativo nell'aspetto e nel funzionamento dei file Excel. Quindi, la prossima volta che lavorerai a un progetto che richiede fogli Excel interattivi o visivamente accattivanti, saprai esattamente come aggiungere quegli ovali perfetti!
## Domande frequenti
### Posso aggiungere altre forme come rettangoli o linee utilizzando Aspose.Cells per .NET?
Sì, puoi aggiungere varie forme come rettangoli, linee e frecce utilizzando `Shapes` raccolta in Aspose.Cells.
### È possibile modificare le dimensioni degli ovali dopo averli aggiunti?
Assolutamente! Puoi modificare le proprietà di altezza e larghezza degli ovali dopo averli aggiunti.
### In quali formati di file posso salvare la cartella di lavoro oltre a XLS?
Aspose.Cells supporta numerosi formati, tra cui XLSX, CSV e PDF.
### Posso modificare il colore del contorno dell'ovale?
Sì, puoi cambiare il colore della linea dell'ovale usando `Line.Color` proprietà.
### È necessaria una licenza per Aspose.Cells?
Sebbene tu possa provare Aspose.Cells con una prova gratuita, avrai bisogno di un [licenza](https://purchase.aspose.com/buy) per un utilizzo a lungo termine o per accedere a funzionalità avanzate.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}