---
title: Applicazione della formattazione a una riga di Excel a livello di programmazione
linktitle: Applicazione della formattazione a una riga di Excel a livello di programmazione
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come applicare la formattazione a una riga di Excel in modo programmatico usando Aspose.Cells per .NET. Questa guida dettagliata, passo dopo passo, copre tutto, dall'allineamento ai bordi.
weight: 11
url: /it/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicazione della formattazione a una riga di Excel a livello di programmazione

## Introduzione
In questo tutorial, ti guideremo attraverso come applicare la formattazione a una riga di Excel in modo programmatico usando Aspose.Cells per .NET. Tratteremo tutto, dall'impostazione dell'ambiente all'applicazione di varie opzioni di formattazione come colore del carattere, allineamento e bordi, il tutto mantenendolo semplice e coinvolgente. Cominciamo!
## Prerequisiti
Prima di iniziare, assicuriamoci di avere tutto ciò che ti serve per seguire questo tutorial. Ecco cosa ti servirà:
1.  Aspose.Cells per la libreria .NET: puoi scaricarla da[Pagina di download di Aspose.Cells per .NET](https://releases.aspose.com/cells/net/).
2. IDE – Qualsiasi ambiente di sviluppo .NET, come Visual Studio.
3. Conoscenza di base di C#: dovresti avere familiarità con il linguaggio di programmazione C# e saper lavorare con le applicazioni .NET.
Assicuratevi di installare anche la versione più recente di Aspose.Cells scaricandola direttamente o utilizzando NuGet Package Manager in Visual Studio.
## Importa pacchetti
Per iniziare, assicurati di importare i pacchetti necessari. Ciò è essenziale per accedere alle funzionalità richieste per lavorare con file Excel e applicare stili a livello di programmazione.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Una volta completata la configurazione, siamo pronti per passare alla parte più interessante: la formattazione delle righe!
In questa sezione, analizzeremo ogni passaggio del processo. Ogni passaggio sarà accompagnato da frammenti di codice e da una spiegazione dettagliata, quindi anche se sei nuovo di Aspose.Cells, sarai in grado di seguire facilmente.
## Passaggio 1: impostare la cartella di lavoro e il foglio di lavoro
Prima di applicare qualsiasi formattazione, devi creare un'istanza della cartella di lavoro e accedere al primo foglio di lavoro. È come aprire una tela bianca prima di iniziare a dipingere.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();
// Ottenere il riferimento del primo foglio di lavoro (predefinito) passando l'indice del suo foglio
Worksheet worksheet = workbook.Worksheets[0];
```
Qui, creiamo un nuovo oggetto workbook e recuperiamo il primo foglio di lavoro. Questo è il foglio in cui applicheremo la formattazione.
## Passaggio 2: creare e personalizzare uno stile
Ora che hai il tuo foglio di lavoro pronto, il passo successivo è definire gli stili che vuoi applicare alla riga. Inizieremo creando un nuovo stile e impostando proprietà come colore del carattere, allineamento e bordi.
```csharp
// Aggiungere un nuovo stile agli stili
Style style = workbook.CreateStyle();
// Impostazione dell'allineamento verticale del testo nella cella "A1"
style.VerticalAlignment = TextAlignmentType.Center;
// Impostazione dell'allineamento orizzontale del testo nella cella "A1"
style.HorizontalAlignment = TextAlignmentType.Center;
// Impostazione del colore del carattere del testo nella cella "A1"
style.Font.Color = Color.Green;
```
In questa parte, impostiamo l'allineamento del testo nella riga (sia verticale che orizzontale) e specifichiamo il colore del carattere. È qui che inizi a definire come il contenuto apparirà visivamente nel tuo foglio Excel.
## Passaggio 3: applicare la funzione Restringi per adattare
A volte, il testo in una cella potrebbe essere troppo lungo, causandone il traboccamento. Un trucco ingegnoso è quello di ridurre il testo per adattarlo alla cella mantenendone la leggibilità.
```csharp
// Ridurre il testo per adattarlo alla cella
style.ShrinkToFit = true;
```
 Con`ShrinkToFit`, ti assicuri che il testo lungo venga ridimensionato per adattarsi ai limiti della cella, rendendo il tuo foglio Excel più organizzato.
## Passaggio 4: imposta i bordi per la riga
Per far risaltare le tue righe, applicare i bordi è un'ottima opzione. In questo esempio, personalizzeremo il bordo inferiore, impostandone il colore su rosso e lo stile su medio.
```csharp
// Impostare il colore del bordo inferiore della cella su rosso
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// Imposta il tipo di bordo inferiore della cella su medio
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
I bordi possono aiutare a separare visivamente i contenuti, rendendo i dati più facili da leggere e più gradevoli esteticamente.
## Passaggio 5: creare un oggetto StyleFlag
 IL`StyleFlag`object indica ad Aspose.Cells quali aspetti dello stile applicare. Questo ti dà un controllo preciso su cosa viene applicato e assicura che venga impostata solo la formattazione desiderata.
```csharp
// Creazione di StyleFlag
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
In questo caso, stiamo specificando che devono essere applicati l'allineamento orizzontale e verticale, il colore del carattere, la riduzione del testo e i bordi.
## Passaggio 6: accedere alla riga desiderata
Una volta creato lo stile, il passo successivo è accedere alla riga in cui vogliamo applicare la formattazione. In questo esempio, formatteremo la prima riga (indice di riga 0).
```csharp
// Accesso a una riga dalla raccolta Righe
Row row = worksheet.Cells.Rows[0];
```
Qui recuperiamo la prima riga del foglio di lavoro. Puoi modificare l'indice per formattare qualsiasi altra riga.
## Passaggio 7: applicare lo stile alla riga
 Infine, è il momento di applicare lo stile alla riga! Utilizziamo il`ApplyStyle` metodo per applicare lo stile definito alla riga selezionata.
```csharp
// Assegnazione dell'oggetto Stile alla proprietà Stile della riga
row.ApplyStyle(style, styleFlag);
```
Lo stile viene ora applicato all'intera riga, facendo sì che i tuoi dati abbiano esattamente l'aspetto che avevi immaginato.
## Passaggio 8: salvare la cartella di lavoro
Una volta terminata l'applicazione della formattazione, devi salvare la cartella di lavoro in un file Excel. È come premere "Salva" in Excel dopo aver apportato le modifiche.
```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "book1.out.xls");
```
Ora hai un foglio Excel completamente formattato salvato nella directory specificata!
## Conclusione
Ecco fatto! In pochi semplici passaggi, hai imparato come applicare la formattazione a una riga di Excel in modo programmatico utilizzando Aspose.Cells per .NET. Dall'impostazione dell'allineamento del testo alla personalizzazione dei bordi, questo tutorial ha trattato gli elementi essenziali che ti aiuteranno a creare report Excel professionali e visivamente accattivanti in modo programmatico. 
Aspose.Cells offre un'ampia gamma di capacità e i metodi mostrati qui possono essere facilmente estesi per applicare stili e formattazioni più complessi ai file Excel. Quindi perché non provarlo e far risaltare i dati?
## Domande frequenti
### Posso applicare stili diversi alle singole celle di una riga?  
Sì, puoi applicare stili diversi alle singole celle accedendovi direttamente tramite`Cells` raccolta anziché applicare lo stile all'intera riga.
### È possibile applicare la formattazione condizionale con Aspose.Cells?  
Assolutamente! Aspose.Cells supporta la formattazione condizionale, consentendo di definire regole basate sui valori delle celle.
### Come posso applicare la formattazione a più righe?  
 È possibile scorrere più righe utilizzando un`for` loop e applica lo stesso stile a ogni riga singolarmente.
### Aspose.Cells supporta l'applicazione di stili a intere colonne?  
 Sì, in modo simile alle righe, puoi accedere alle colonne utilizzando`Columns` raccolta e applicare loro degli stili.
### Posso usare Aspose.Cells con le applicazioni .NET Core?  
Sì, Aspose.Cells è completamente compatibile con .NET Core, il che consente di utilizzarlo su diverse piattaforme.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
