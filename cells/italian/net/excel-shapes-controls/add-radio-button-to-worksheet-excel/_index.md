---
"description": "Scopri come aggiungere pulsanti di opzione a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET con questa semplice guida passo passo. Perfetta per creare moduli Excel interattivi."
"linktitle": "Aggiungi pulsante di scelta al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungi pulsante di scelta al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi pulsante di scelta al foglio di lavoro in Excel

## Introduzione
Ti sei mai chiesto come arricchire i tuoi fogli Excel con elementi interattivi come i pulsanti di opzione? Che tu stia creando un sondaggio, un modulo o uno strumento di analisi, l'aggiunta di pulsanti di opzione può davvero migliorare l'interazione dell'utente. In questo tutorial, ti guideremo attraverso il processo di aggiunta di pulsanti di opzione ai tuoi fogli Excel utilizzando Aspose.Cells per .NET. Suddivideremo ogni passaggio in semplici passaggi, assicurandoti che sarai un professionista entro la fine di questo articolo. Pronto a iniziare? Iniziamo!
## Prerequisiti
Prima di passare alla parte divertente dell'aggiunta dei pulsanti di scelta, assicuriamoci di aver impostato tutto per iniziare.
1. Aspose.Cells per .NET: per prima cosa, assicurati di aver scaricato e installato [Aspose.Cells per .NET](https://releases.aspose.com/cells/net/) libreria. Puoi scaricarla tramite NuGet in Visual Studio o dalla pagina di download.
2. IDE (Integrated Development Environment): per scrivere ed eseguire il codice C# avrai bisogno di un IDE come Visual Studio.
3. .NET Framework: assicurati di avere .NET Framework 4.0 o versione successiva installato sul tuo computer. Aspose.Cells lo richiede per funzionare.
4. Nozioni di base di C#: la familiarità con la sintassi di C# e la programmazione .NET renderà le cose più semplici man mano che seguirete le istruzioni.
Una volta che tutto è a posto, siamo pronti a partire!
## Importa pacchetti
Prima di scrivere codice, è fondamentale importare gli spazi dei nomi necessari per evitare errori in seguito. Aggiungi quanto segue al tuo codice:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Queste importazioni sono essenziali per accedere alle funzionalità della cartella di lavoro, aggiungere pulsanti di scelta e gestire le operazioni sui file.
## Passaggio 1: impostazione della cartella di lavoro
Per prima cosa, creiamo una nuova cartella di lavoro di Excel.
Per iniziare, dovrai creare un'istanza di un nuovo `Workbook` oggetto. Questo rappresenterà il tuo file Excel nel codice.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
In questo passaggio, creerai una cartella di lavoro vuota. Immaginala come una tela bianca su cui aggiungere i pulsanti di opzione nei passaggi successivi.
## Passaggio 2: aggiunta e formattazione di un valore di cella
Ora aggiungiamo un titolo al foglio di lavoro. Aggiungeremo del testo alla cella. `C2` e formattalo in grassetto. Questo passaggio aggiunge contesto ai pulsanti di opzione.
### Inserisci testo nella cella
```csharp
// Inserire un valore nella cella C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Rendi il testo in grassetto
```csharp
// Imposta il testo nella cella C2 in grassetto.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Qui abbiamo aggiunto un titolo semplice, "Gruppi di età", nella cella `C2`e l'ho messo in grassetto per farlo risaltare. Facile, vero?
## Passaggio 3: aggiunta del primo pulsante di scelta
Adesso arriva la parte emozionante: aggiungere il primo pulsante di scelta al foglio di lavoro!
### Aggiungi un pulsante di scelta
```csharp
// Aggiungere un pulsante di scelta al primo foglio.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Questa riga aggiunge il pulsante di opzione a una posizione specifica sul foglio di lavoro. I numeri ne rappresentano la posizione e le dimensioni. Immagina di impostare le coordinate X e Y del pulsante.
### Imposta il testo del pulsante di scelta
```csharp
// Imposta la stringa di testo.
radio1.Text = "20-29";
```
Qui abbiamo assegnato al pulsante di scelta un'etichetta, "20-29", che rappresenta una fascia d'età.
### Collega il pulsante di scelta a una cella
```csharp
// Imposta la cella A1 come cella collegata per il pulsante di scelta.
radio1.LinkedCell = "A1";
```
Questo collega il pulsante di scelta alla cella `A1`, il che significa che il risultato della selezione del pulsante verrà memorizzato in quella cella.
### Aggiungi effetto 3D
```csharp
// Rendi il pulsante di scelta 3D.
radio1.Shadow = true;
```
Poiché vogliamo che questo pulsante di scelta salti, abbiamo aggiunto un effetto 3D.
### Personalizza la riga del pulsante di scelta
```csharp
// Imposta lo spessore della linea del pulsante di scelta.
radio1.Line.Weight = 4;
// Imposta lo stile del trattino della linea del pulsante di scelta.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Queste righe di codice regolano lo spessore e lo stile del tratteggio del bordo del pulsante di scelta per renderlo più accattivante visivamente.
## Passaggio 4: aggiunta di pulsanti di scelta aggiuntivi
Aggiungiamo altri due pulsanti di scelta per le fasce d'età rimanenti: "30-39" e "40-49". La procedura è la stessa, con piccole variazioni nelle coordinate e nelle etichette.
### Aggiungi il secondo pulsante di scelta
```csharp
// Aggiungere un altro pulsante di scelta al primo foglio.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Imposta la stringa di testo.
radio2.Text = "30-39";
// Imposta la cella A1 come cella collegata per il pulsante di scelta.
radio2.LinkedCell = "A1";
// Rendi il pulsante di scelta 3D.
radio2.Shadow = true;
// Imposta il peso del pulsante di scelta.
radio2.Line.Weight = 4;
// Imposta lo stile del trattino del pulsante di scelta.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Aggiungi il terzo pulsante di scelta
```csharp
// Aggiungere un altro pulsante di scelta al primo foglio.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Imposta la stringa di testo.
radio3.Text = "40-49";
// Imposta la cella A1 come cella collegata per il pulsante di scelta.
radio3.LinkedCell = "A1";
// Rendi il pulsante di scelta 3D.
radio3.Shadow = true;
// Imposta il peso del pulsante di scelta.
radio3.Line.Weight = 4;
// Imposta lo stile del trattino del pulsante di scelta.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Passaggio 5: salvataggio del file Excel
Una volta aggiunti e formattati tutti i pulsanti di scelta, è il momento di salvare il file.
```csharp
// Salvare il file Excel.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
In questa fase, la cartella di lavoro viene salvata nella directory specificata. È semplicissimo: il tuo foglio di lavoro interattivo è pronto!
## Conclusione
Ecco fatto! Hai appena aggiunto pulsanti di opzione a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Questo tutorial ha trattato ogni aspetto, dalla configurazione della cartella di lavoro all'inserimento e alla formattazione di un valore, dall'aggiunta di più pulsanti di opzione al loro collegamento a una cella. Ora sei pronto per creare fogli Excel interattivi che non solo hanno un aspetto accattivante, ma offrono anche un'esperienza utente migliorata. Divertiti a esplorare nuove possibilità con Aspose.Cells!
## Domande frequenti
### Posso aggiungere più pulsanti di scelta a fogli diversi?  
Assolutamente! Puoi ripetere il processo su qualsiasi foglio della cartella di lavoro specificando l'indice corretto.
### Posso personalizzare ulteriormente l'aspetto dei pulsanti di scelta?  
Sì, Aspose.Cells offre diverse opzioni di personalizzazione, tra cui la modifica dei colori, delle dimensioni e di altri attributi di formattazione.
### Come posso individuare quale pulsante di scelta è selezionato?  
La cella collegata (ad esempio, A1) mostrerà l'indice del pulsante di opzione selezionato. È possibile controllare il valore della cella collegata per scoprire quale pulsante di opzione è selezionato.
### C'è un limite al numero di pulsanti di scelta che posso aggiungere?  
No, non c'è un limite massimo al numero di pulsanti di opzione che puoi aggiungere. Tuttavia, è bene mantenere l'interfaccia intuitiva.
### Posso usare Aspose.Cells con altri linguaggi di programmazione?  
Sì, Aspose.Cells supporta diversi linguaggi di programmazione, incluso Java. Ma questo tutorial si concentra specificamente su .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}