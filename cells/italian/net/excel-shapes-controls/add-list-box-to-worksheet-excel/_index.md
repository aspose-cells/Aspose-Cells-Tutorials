---
title: Aggiungi casella di riepilogo al foglio di lavoro in Excel
linktitle: Aggiungi casella di riepilogo al foglio di lavoro in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come aggiungere una casella di riepilogo a un foglio di lavoro Excel usando Aspose.Cells per .NET. Segui la nostra semplice guida passo dopo passo e rendi interattivi i tuoi fogli Excel.
weight: 20
url: /it/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi casella di riepilogo al foglio di lavoro in Excel

## Introduzione
Aggiungere elementi interattivi ai tuoi fogli di lavoro Excel, come una casella di riepilogo, può migliorare notevolmente la gestione e la presentazione dei dati. Che tu stia creando un modulo interattivo o uno strumento di immissione dati personalizzato, la possibilità di controllare l'input dell'utente con una casella di riepilogo è inestimabile. Aspose.Cells per .NET fornisce un modo efficiente per aggiungere e gestire questi controlli nei tuoi file Excel. In questa guida, ti guideremo attraverso il processo di aggiunta di una casella di riepilogo a un foglio di lavoro utilizzando Aspose.Cells per .NET.
## Prerequisiti
Prima di immergerti nella codifica, assicurati di disporre dei seguenti strumenti e risorse:
-  Aspose.Cells per la libreria .NET: puoi scaricarla da[Pagina di download di Aspose.Cells per .NET](https://releases.aspose.com/cells/net/).
- Ambiente di sviluppo: qualsiasi IDE che supporti lo sviluppo .NET, come Visual Studio.
- .NET Framework: assicurati che il tuo progetto sia destinato a una versione supportata di .NET Framework.
 Inoltre, considera di procurarti un[licenza temporanea](https://purchase.aspose.com/temporary-license/) se vuoi esplorare tutte le funzionalità senza limitazioni.
## Importa pacchetti
Prima di iniziare, assicurati di aver importato i namespace Aspose.Cells necessari. Ecco come fare:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
In questo tutorial, suddivideremo il processo di aggiunta di una casella di riepilogo in più semplici passaggi. Segui attentamente ogni passaggio per assicurarti che tutto funzioni come previsto.
## Passaggio 1: impostazione della directory dei documenti
Prima di creare un file Excel, hai bisogno di una posizione in cui salvarlo. Ecco come impostare la directory:
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non esiste già.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In questo passaggio, stai definendo dove verrà archiviato il tuo file. Il codice controlla se la directory esiste e, in caso contrario, ne crea una per te. Questo assicura che non incontrerai errori "file not found" in seguito.
## Passaggio 2: creare una nuova cartella di lavoro e accedere al primo foglio di lavoro
Successivamente, creeremo una nuova cartella di lavoro e accederemo al primo foglio di lavoro in cui aggiungeremo la nostra casella di elenco.
```csharp
// Crea una nuova cartella di lavoro.
Workbook workbook = new Workbook();
// Ottieni il primo foglio di lavoro.
Worksheet sheet = workbook.Worksheets[0];
```
Una cartella di lavoro è essenzialmente il tuo file Excel. Qui, stiamo creando una nuova cartella di lavoro e accedendo al primo foglio di lavoro, che è dove posizioneremo la nostra casella di riepilogo. Pensa a questo come alla creazione di una tela bianca su cui dipingerai i controlli.
## Passaggio 3: immettere i dati per la casella di riepilogo
Prima di aggiungere la casella di riepilogo, dobbiamo inserire alcuni dati a cui la casella di riepilogo farà riferimento.
```csharp
// Ottieni la raccolta di celle del foglio di lavoro.
Cells cells = sheet.Cells;
// Immettere un valore per l'etichetta.
cells["B3"].PutValue("Choose Dept:");
// Imposta l'etichetta in grassetto.
cells["B3"].GetStyle().Font.IsBold = true;
// Valori di input per la casella di riepilogo.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Qui, stiamo aggiungendo del testo nel foglio di lavoro. L'etichetta "Scegli reparto:" è posizionata nella cella B3 e il suo carattere è impostato su grassetto. Nella colonna A, stiamo inserendo valori che fungeranno da intervallo di input per la nostra casella di riepilogo, che rappresentano diversi reparti. Questo intervallo di input è ciò che gli utenti sceglieranno quando interagiranno con la casella di riepilogo.
## Passaggio 4: aggiungere la casella di riepilogo al foglio di lavoro
Ora che abbiamo impostato i dati, aggiungiamo il controllo casella di riepilogo.
```csharp
// Aggiungi una nuova casella di riepilogo.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Questo codice aggiunge la casella di riepilogo al foglio di lavoro. I parametri definiscono la posizione e la dimensione della casella di riepilogo. La casella di riepilogo è posizionata nella riga 2, colonna 0 con una larghezza di 122 e un'altezza di 100. Queste sono le coordinate e la dimensione che determinano dove apparirà la casella di riepilogo nel foglio di lavoro.
## Passaggio 5: impostare le proprietà della casella di riepilogo
Ora imposteremo varie proprietà della casella di riepilogo per renderla pienamente funzionale.
```csharp
// Imposta il tipo di posizionamento.
listBox.Placement = PlacementType.FreeFloating;
// Imposta la cella collegata.
listBox.LinkedCell = "A1";
// Imposta l'intervallo di input.
listBox.InputRange = "A2:A7";
// Imposta il tipo di selezione.
listBox.SelectionType = SelectionType.Single;
// Imposta la casella di riepilogo con ombreggiatura 3D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: questa proprietà garantisce che la casella di riepilogo rimanga nella sua posizione indipendentemente dalle modifiche apportate al foglio di lavoro.
- LinkedCell: imposta una cella (in questo caso, A1) in cui verrà visualizzato il valore selezionato dalla casella di riepilogo.
- InputRange: indica alla casella di riepilogo dove cercare il suo elenco di opzioni (da A2 ad A7, che abbiamo impostato in precedenza).
- SelectionType.Single: limita l'utente alla selezione di un solo elemento dalla casella di riepilogo.
- Ombra: l'effetto ombra conferisce alla casella di riepilogo un aspetto più tridimensionale, rendendola visivamente accattivante.
## Passaggio 6: salvare il file Excel
Infine, salviamo la nostra cartella di lavoro con la casella di riepilogo inclusa.
```csharp
// Salvare la cartella di lavoro.
workbook.Save(dataDir + "book1.out.xls");
```
Questa riga di codice salva la cartella di lavoro nella directory che abbiamo impostato in precedenza. Il file si chiama "book1.out.xls", ma puoi scegliere qualsiasi nome che si adatti al tuo progetto.
## Conclusione
Ed ecco fatto! Hai aggiunto con successo una casella di riepilogo a un foglio di lavoro Excel usando Aspose.Cells per .NET. Con solo poche righe di codice, abbiamo creato una casella di riepilogo completamente funzionale, rendendo il foglio di lavoro più interattivo e dinamico. Questo tutorial dovrebbe darti una solida base per esplorare altri controlli e funzionalità in Aspose.Cells per .NET. Continua a sperimentare e presto padroneggerai la vasta funzionalità della libreria!
## Domande frequenti
### Posso consentire selezioni multiple nella casella di riepilogo?  
 Sì, puoi cambiare il`SelectionType` A`SelectionType.Multi` per consentire selezioni multiple.
### Posso modificare l'aspetto della casella di riepilogo?  
Assolutamente! Aspose.Cells consente di personalizzare l'aspetto della casella di riepilogo, incluse le dimensioni, il carattere e persino il colore.
### Cosa succede se in seguito ho bisogno di rimuovere la casella di riepilogo?  
 È possibile accedere e rimuovere la casella di elenco da`Shapes` raccolta utilizzando`sheet.Shapes.RemoveAt(index)`.
### Posso collegare la casella di riepilogo a una cella diversa?  
 Sì, cambia semplicemente il`LinkedCell` proprietà a qualsiasi altra cella in cui si desidera visualizzare il valore selezionato.
### Come posso aggiungere altri elementi alla casella di riepilogo?  
Basta aggiornare l'intervallo di input inserendo più valori nelle celle specificate e la casella di riepilogo verrà aggiornata automaticamente.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
