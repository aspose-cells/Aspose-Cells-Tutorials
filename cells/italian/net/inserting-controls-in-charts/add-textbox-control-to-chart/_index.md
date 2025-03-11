---
title: Aggiungi controllo TextBox al grafico
linktitle: Aggiungi controllo TextBox al grafico
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come aggiungere una TextBox ai grafici in Excel usando Aspose.Cells per .NET. Migliora la visualizzazione dei tuoi dati senza sforzo.
weight: 12
url: /it/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi controllo TextBox al grafico

## Introduzione

Creare grafici dinamici e visivamente accattivanti in Excel è un modo fantastico per rappresentare i dati in modo efficace. Una funzionalità ingegnosa che puoi usare è l'aggiunta di una TextBox a un grafico. Con Aspose.Cells per .NET, questo compito diventa facile e divertente! In questa guida, ti guideremo passo dopo passo nel processo di integrazione di una TextBox nel tuo grafico. Che tu sia uno sviluppatore esperto o alle prime armi, questo tutorial ti fornirà tutti gli strumenti di cui hai bisogno per migliorare i tuoi grafici Excel. Quindi, sei pronto a tuffarti?

## Prerequisiti

Prima di iniziare a scrivere codice, ecco alcune cose che dovresti sapere:

- Nozioni di base di C#: una conoscenza di base della programmazione C# sarà utile. Non preoccuparti; non devi essere un esperto, solo avere dimestichezza con la sintassi.
-  Libreria Aspose.Cells installata: assicurati di aver installato la libreria Aspose.Cells per .NET. Puoi scaricarla da[Qui](https://releases.aspose.com/cells/net/) se non l'hai già fatto.
- Visual Studio: è essenziale avere familiarità con Visual Studio o con qualsiasi IDE che si preferisce utilizzare per il framework .NET.
- Un file Excel esistente: per questo esempio, lavoreremo con un file Excel esistente denominato "sampleAddingTextBoxControlInChart.xls". Puoi crearne uno o scaricare un campione.

Ora che abbiamo tutto a posto, passiamo alla parte di codifica!

## Importa pacchetti

Per prima cosa, dobbiamo importare i namespace Aspose.Cells necessari nel nostro progetto C#. Puoi farlo facilmente includendo le seguenti righe all'inizio del tuo file di codice:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Passaggio 1: definire le directory di origine e di output

Prima di iniziare a lavorare con il file Excel, è importante definire dove si trova il file di input e dove si desidera salvare il file di output. Questo aiuta a mantenere organizzato il progetto.

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";

// Directory di uscita
string outputDir = "Your Output Directory";
```
 Sostituire`"Your Document Directory"` E`"Your Output Directory"` con i percorsi effettivi del tuo sistema.

## Passaggio 2: aprire il file Excel esistente

Poi, dobbiamo aprire il file Excel che contiene il grafico che vogliamo modificare. Questo ci permetterà di recuperare il grafico e apportare modifiche.

```csharp
// Aprire il file esistente.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Questa riga inizializza un nuovo oggetto Workbook con il file specificato.

## Passaggio 3: accedere al grafico nel foglio di lavoro

Poiché i grafici in Excel sono archiviati in un foglio di lavoro, dobbiamo prima accedere al foglio di lavoro e poi ottenere il grafico desiderato. Per questo esempio, accederemo al primo grafico nel primo foglio di lavoro.

```csharp
// Prendi la tabella del designer nel primo foglio.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Modificando il valore dell'indice, puoi selezionare fogli di lavoro o grafici diversi se il tuo file ne contiene di più.

## Passaggio 4: aggiungere una nuova casella di testo al grafico

Ora siamo pronti ad aggiungere il nostro TextBox. Ne specificheremo la posizione e le dimensioni quando lo creeremo.

```csharp
// Aggiungere una nuova casella di testo al grafico.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
In questo comando, i parametri definiscono la posizione (x, y) e la dimensione (larghezza, altezza) del TextBox nel grafico. Adatta questi valori in base alle tue specifiche esigenze di layout.

## Passaggio 5: imposta il testo per la casella di testo

Una volta che il TextBox è al suo posto, è il momento di riempirlo di contenuto. Puoi aggiungere qualsiasi testo che ritieni necessario per il tuo grafico.

```csharp
// Riempi il testo.
textbox0.Text = "Sales By Region";
```
Sentiti libero di sostituire "Vendite per regione" con qualsiasi testo pertinente ai tuoi dati.

## Passaggio 6: regola le proprietà della casella di testo

Ora, rendiamo il nostro TextBox bello! Puoi personalizzare varie proprietà come colore del font, dimensione e stile.

```csharp
// Imposta il colore del carattere.
textbox0.Font.Color = Color.Maroon; // Cambia il colore desiderato

// Imposta il carattere in grassetto.
textbox0.Font.IsBold = true;

// Imposta la dimensione del carattere.
textbox0.Font.Size = 14;

// Imposta l'attributo del carattere su corsivo.
textbox0.Font.IsItalic = true;
```

Ognuna di queste righe modifica l'aspetto del testo all'interno della TextBox, migliorandone la visibilità e l'attrattiva.

## Passaggio 7: formattare l'aspetto della casella di testo

È anche essenziale formattare lo sfondo e il bordo del TextBox. Questo lo fa risaltare sul grafico.

```csharp
// Ottieni il formato di riempimento della casella di testo.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Ottieni il tipo di formato della riga della casella di testo.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Imposta lo spessore della linea.
lineformat.Weight = 2;

// Imposta lo stile del trattino su continuo.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Queste opzioni consentono di impostare il riempimento dello sfondo del TextBox e di personalizzarne il bordo.

## Passaggio 8: salvare il file Excel modificato

L'ultimo passaggio consiste nel salvare le modifiche apportate a un nuovo file Excel. Ciò garantirà che il file originale rimanga intatto.

```csharp
// Salvare il file Excel.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Sostituire`"outputAddingTextBoxControlInChart.xls"` con il nome file che preferisci.

## Conclusione

Congratulazioni! Hai aggiunto con successo un controllo TextBox a un grafico usando Aspose.Cells per .NET. Questa semplice ma efficace modifica può rendere i tuoi grafici più informativi e visivamente accattivanti. La rappresentazione dei dati è fondamentale per una comunicazione efficace e con strumenti come Aspose hai il potere di migliorare quella presentazione con il minimo sforzo.

## Domande frequenti

### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una potente libreria per creare, manipolare e convertire file Excel senza dover ricorrere a Microsoft Excel.

### Posso aggiungere più caselle di testo a un singolo grafico?
Sì! Puoi aggiungere tutti i TextBox di cui hai bisogno ripetendo i passaggi di creazione dei TextBox con posizioni diverse.

### Aspose.Cells è gratuito?
Aspose.Cells è una libreria a pagamento, ma puoi scaricare una versione di prova gratuita da[Qui](https://releases.aspose.com/).

### Dove posso trovare ulteriore documentazione su Aspose.Cells?
 Puoi accedere a una documentazione completa[Qui](https://reference.aspose.com/cells/net/).

### Come posso ottenere supporto se riscontro problemi?
 Puoi cercare assistenza tramite il forum di supporto di Aspose[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
