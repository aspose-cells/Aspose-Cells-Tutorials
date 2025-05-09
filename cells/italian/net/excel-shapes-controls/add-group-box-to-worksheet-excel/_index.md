---
"description": "Scopri come aggiungere una casella di gruppo e pulsanti di opzione in Excel utilizzando Aspose.Cells per .NET. Una guida passo passo per sviluppatori di tutti i livelli."
"linktitle": "Aggiungi casella di gruppo al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungi casella di gruppo al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-group-box-to-worksheet-excel/"
"weight": 24
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi casella di gruppo al foglio di lavoro in Excel

## Introduzione
Quando si tratta di presentazione dei dati, Excel è il re. L'aggiunta di elementi interattivi come le caselle di gruppo può rendere i fogli di calcolo più coinvolgenti e intuitivi. Oggi ci immergiamo nel mondo di Aspose.Cells per .NET, una potente libreria che ti aiuta a manipolare i fogli Excel senza sforzo. Ma non preoccuparti se non sei un mago della programmazione: questa guida suddivide tutto in semplici passaggi. Sei pronto a migliorare le tue competenze in Excel? Iniziamo!
## Prerequisiti
Prima di passare al codice, ecco alcune cose di cui avrai bisogno:
1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer, perché è lì che scriverai il codice .NET.
2. Aspose.Cells per .NET: è necessario scaricare questa libreria. Puoi trovarla qui [Qui](https://releases.aspose.com/cells/net/). 
3. Conoscenza di base di C#: spiegherò tutto passo dopo passo, ma una minima conoscenza di C# ti aiuterà a seguire.
## Importa pacchetti
Per qualsiasi progetto, dovrai prima importare i pacchetti necessari. In questo caso, Aspose.Cells sarà il tuo focus principale. Ecco come fare:
## Passaggio 1: aprire il progetto in Visual Studio
Avvia Visual Studio e apri il progetto esistente oppure creane uno nuovo. 
## Passaggio 2: aggiungere un riferimento ad Aspose.Cells
- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Seleziona "Gestisci pacchetti NuGet".
- Cerca "Aspose.Cells" e installalo. Questo ti permetterà di utilizzare tutte le classi e i metodi forniti dalla libreria Aspose.Cells.
## Passaggio 3: includere la direttiva sull'utilizzo
Nella parte superiore del file C#, includi lo spazio dei nomi Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Questo ti dà accesso alle classi necessarie per lavorare con i file Excel.
Ora che abbiamo impostato tutto, entriamo nel vivo del tutorial: aggiungere una casella di gruppo con pulsanti di opzione a un foglio di lavoro Excel. Per maggiore chiarezza, suddivideremo questo processo in più passaggi.
## Passaggio 1: imposta la directory dei documenti
Prima di creare un file Excel, è necessario stabilire dove salvarlo. Creiamo una directory, se non esiste già.
```csharp
// Il percorso verso la directory dei documenti
string dataDir = "Your Document Directory"; // Specifica il percorso desiderato
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Questo codice verifica se la directory in cui verrà salvato il file Excel esiste. In caso contrario, ne crea una: è come preparare l'area di lavoro prima di iniziare il progetto!
## Passaggio 2: creare una nuova cartella di lavoro
Successivamente, dovrai creare una cartella di lavoro Excel in cui aggiungerai la casella di gruppo.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
Questa riga inizializza una nuova istanza di una cartella di lavoro. Immagina di aprire un nuovo file Excel vuoto, pronto per le modifiche.
## Passaggio 3: aggiungere una casella di gruppo
Ora aggiungiamo quella casella di gruppo. 
```csharp
// Aggiungere una casella di gruppo al primo foglio di lavoro.
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
Qui, stai aggiungendo un riquadro di gruppo alle coordinate specificate nel primo foglio di lavoro. I parametri definiscono la posizione e le dimensioni del riquadro, proprio come quando si posizionano i mobili in una stanza!
## Passaggio 4: imposta la didascalia della casella di gruppo
Adesso diamo un titolo alla tua casella di gruppo!
```csharp
// Imposta la didascalia della casella di gruppo.
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
La stringa "Gruppi di età" imposta l'etichetta che appare nella casella di gruppo. L'impostazione `Placement` COME `FreeFloating` consente alla scatola di essere mobile: la flessibilità è fondamentale!
## Passaggio 5: Rendi la casella di gruppo 2D
Anche se il 3D potrebbe sembrare una scelta fantasiosa, qui puntiamo su un look classico.
```csharp
// Rendila una scatola 2D.
box.Shadow = false;
```
Questo codice rimuove l'effetto ombra, conferendo alla casella un aspetto piatto, come un semplice foglio di carta!
## Passaggio 6: aggiungere pulsanti di scelta
Aggiungiamo un po' di pepe al tutto aggiungendo alcuni pulsanti di scelta per l'input dell'utente.
## Passaggio 6.1: aggiungere il primo pulsante di scelta
```csharp
// Aggiungere un pulsante di scelta.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
// Imposta la stringa di testo.
radio1.Text = "20-29";
// Imposta la cella A1 come cella collegata per il pulsante di scelta.
radio1.LinkedCell = "A1";
```
Si crea un pulsante di scelta per la fascia d'età 20-29, collegandolo alla cella A1 del foglio di lavoro. Ciò significa che quando si seleziona questo pulsante, la cella A1 riflette tale scelta!
## Passaggio 6.2: personalizzare il primo pulsante di scelta
Ora diamogli un po' di stile.
```csharp
// Rendi il pulsante di scelta 3D.
radio1.Shadow = true;
// Imposta il peso del pulsante di scelta.
radio1.Line.Weight = 4;
// Imposta lo stile del trattino del pulsante di scelta.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aggiungendo un'ombra e modificando lo stile della linea, miglioriamo la visibilità del pulsante. È come aggiungere decorazioni per farlo risaltare sulla pagina!
## Passaggio 6.3: ripetere per altri pulsanti di scelta
Ripetere questo processo per ulteriori gruppi di età:
```csharp
// Secondo pulsante di scelta
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
// Terzo pulsante di scelta
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ogni pulsante di scelta consente di scegliere tra diverse fasce d'età, collegate alla stessa cella A1. Questo consente un processo di selezione semplice e intuitivo.
## Passaggio 7: raggruppare le forme
Ora che tutto è a posto, riordiniamo le cose raggruppando le forme. 
```csharp
// Ottieni le forme.
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
// Raggruppa le forme.
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
Questo passaggio unisce tutto in un'unica unità coesa. È come mettere una cornice attorno alla tua collezione d'arte: le unisce splendidamente!
## Passaggio 8: salvare il file Excel
Infine, salviamo il nostro capolavoro!
```csharp
// Salvare il file Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Questa riga di codice scrive le modifiche in un nuovo file Excel denominato "book1.out.xls" nella directory specificata. Come sigillare una busta, il tuo lavoro è ora archiviato in modo sicuro!
## Conclusione
Ed ecco qui: una guida completa per aggiungere una casella di gruppo e pulsanti di opzione a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET! Con ogni passaggio, hai imparato a manipolare Excel a livello di programmazione, aprendo le porte a infinite possibilità di personalizzazione di report, visualizzazioni di dati e altro ancora. Il bello della programmazione è che puoi automatizzare le attività e creare interfacce intuitive con relativa facilità: immagina il potenziale!
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una libreria .NET per la gestione dei file Excel, che consente di eseguire attività come la lettura, la scrittura e la manipolazione di fogli di calcolo a livello di programmazione.
### È necessaria esperienza di programmazione per utilizzare Aspose.Cells?
Anche se alcune conoscenze di programmazione sono utili, questo tutorial ti guiderà attraverso le nozioni di base, rendendole accessibili anche ai principianti!
### Posso personalizzare l'aspetto delle caselle di gruppo e dei pulsanti?
Assolutamente! Aspose.Cells offre ampie opzioni per definire lo stile delle forme, inclusi colori, dimensioni ed effetti 3D.
### È disponibile una prova gratuita per Aspose.Cells?
Sì! Puoi provarlo gratuitamente visitando [Prova gratuita di Aspose](https://releases.aspose.com/).
### Dove posso trovare ulteriori risorse o supporto per Aspose.Cells?
IL [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9) è un luogo eccellente per cercare aiuto e condividere conoscenze con la comunità.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}