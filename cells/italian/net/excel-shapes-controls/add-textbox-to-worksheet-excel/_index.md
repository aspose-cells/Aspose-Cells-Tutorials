---
title: Aggiungere una casella di testo al foglio di lavoro in Excel
linktitle: Aggiungere una casella di testo al foglio di lavoro in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come aggiungere caselle di testo personalizzabili a Excel utilizzando Aspose.Cells per .NET in questa esercitazione dettagliata.
weight: 14
url: /it/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere una casella di testo al foglio di lavoro in Excel

## Introduzione
Vuoi migliorare i tuoi fogli di calcolo Excel con elementi visivi unici che possano coinvolgere il tuo pubblico? Aggiungere caselle di testo è un ottimo modo per riuscirci! Con Aspose.Cells per .NET, puoi integrare facilmente le caselle di testo nei tuoi fogli di lavoro Excel, rendendo i tuoi documenti più informativi e visivamente accattivanti. Questa guida passo passo ti guiderà attraverso il semplice processo di aggiunta di caselle di testo utilizzando Aspose.Cells, mostrandoti come personalizzarle con testo, colori, collegamenti ipertestuali e altro ancora!
## Prerequisiti
Prima di immergerci nella meraviglia della codifica, ecco i prerequisiti essenziali per garantire un'esperienza di navigazione senza intoppi:
1. Ambiente di sviluppo .NET: avrai bisogno di un framework .NET funzionante insieme a un IDE come Visual Studio. Assicurati che sia aggiornato all'ultima versione!
2.  Aspose.Cells per .NET: assicurati di aver scaricato la libreria Aspose.Cells. Puoi prendere l'ultima versione da[Qui](https://releases.aspose.com/cells/net/).
3. Conoscenze di base di programmazione: la familiarità con C# e alcuni concetti generali sulla gestione dei file Excel renderanno questo tutorial più semplice!
## Importa pacchetti
Assicurati di importare i pacchetti necessari all'inizio del tuo file C#. Ecco come puoi farlo:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Installa Aspose.Cells
Se non lo hai ancora fatto, puoi aggiungere Aspose.Cells tramite NuGet Package Manager in Visual Studio:
1. Aprire Visual Studio.
2.  Vai a`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Cerca “Aspose.Cells” e installalo per il tuo progetto.
Ora che abbiamo gettato le basi, passiamo alla parte divertente!
## Passaggio 1: impostazione della directory dei documenti
Per prima cosa, impostiamo la directory in cui verranno archiviati tutti i tuoi documenti Excel. È essenziale assicurarsi che questa directory esista prima di iniziare a creare la nostra cartella di lavoro.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory"; 
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Questo frammento di codice creerà una directory denominata`Your Document Directory` (sostituiscilo con il tuo percorso effettivo) se non esiste già. Facile, vero?
## Passaggio 2: creazione di una nuova cartella di lavoro
Poi, dobbiamo creare una nuova cartella di lavoro in cui aggiungeremo le nostre caselle di testo. Questo può essere fatto facilmente con poche righe di codice:
```csharp
// Crea una nuova cartella di lavoro.
Workbook workbook = new Workbook();
```
Questa riga di codice crea una nuova cartella di lavoro Excel. Semplice e diretto!
## Fase 3: Accesso al primo foglio di lavoro
Ora che abbiamo pronto il nostro quaderno di lavoro, prendiamo il primo foglio di lavoro in cui aggiungeremo la nostra casella di testo:
```csharp
// Prendi il primo foglio di lavoro del libro.
Worksheet worksheet = workbook.Worksheets[0];
```
 Proprio così, ora hai accesso al primo foglio di lavoro denominato`worksheet`È tempo di farlo brillare!
## Passaggio 4: aggiunta di una casella di testo
Bene, è il momento di aggiungere la nostra prima casella di testo! Ecco come fare:
```csharp
// Aggiungi una nuova casella di testo alla raccolta.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
In questa riga, stiamo specificando la riga e la colonna in cui verrà posizionata la casella di testo, oltre a impostare la sua larghezza e altezza (rispettivamente 160 e 200). Sentiti libero di adattare questi numeri in base al tuo layout!
## Passaggio 5: Ottenere l'oggetto TextBox
Dopo aver aggiunto la casella di testo, dobbiamo ottenere un riferimento ad essa per poterne personalizzare il contenuto:
```csharp
// Ottieni l'oggetto casella di testo.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Ora,`textbox0` è la tua chiave d'accesso per modificare questa casella di testo!
## Passaggio 6: Riempimento della casella di testo con il contenuto
Ora inseriamo del testo per la casella di testo:
```csharp
// Riempi il testo.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Inserire del testo nella casella di testo è semplicissimo! 
## Passaggio 7: personalizzare l'aspetto della casella di testo
Che ne dici di ravvivarlo un po'? Puoi modificare i colori dei caratteri, gli stili e altro ancora!
```csharp
// Imposta il colore del carattere.
textbox0.Font.Color = Color.Blue;
// Imposta il carattere in grassetto.
textbox0.Font.IsBold = true;
// Imposta la dimensione del carattere.
textbox0.Font.Size = 14;
// Imposta l'attributo del carattere su corsivo.
textbox0.Font.IsItalic = true;
```
Sentiti libero di giocare con diversi colori e stili per vedere quale risalta di più a livello visivo!
## Passaggio 8: aggiunta di un collegamento ipertestuale
Vuoi trasformare la tua casella di testo in un link cliccabile? Facciamolo:
```csharp
// Aggiungere un collegamento ipertestuale alla casella di testo.
textbox0.AddHyperlink("http://"http://www.aspose.com/");
```
Ora chiunque clicchi sulla tua casella di testo verrà trasportato sul sito web di Aspose. È come una magia!
## Passaggio 9: impostazione del tipo di posizionamento della casella di testo
Hai diverse scelte su come vuoi che la casella di testo si comporti in relazione al tuo foglio di lavoro. Ecco un esempio di come impostarla come mobile:
```csharp
// Imposta il posizionamento.
textbox0.Placement = PlacementType.FreeFloating;
```
In alternativa, se vuoi che venga ridimensionato e spostato insieme alle celle, puoi impostarlo in questo modo:
```csharp
// Imposta il tipo di posizionamento in modo che la casella di testo si sposti e si ridimensioni insieme alle celle.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Passaggio 10: personalizzazione dei formati di linea e riempimento
Ecco come puoi modificare l'aspetto del bordo e del riempimento della casella di testo:
```csharp
// Ottieni il formato di riempimento della casella di testo.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Ottieni il tipo di formato della riga della casella di testo.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Imposta lo spessore della linea.
lineformat.Weight = 6;
// Imposta lo stile del trattino su squaredot.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Grazie a questo, puoi personalizzare ulteriormente la tua casella di testo, aggiungendo elementi visivi adatti al tuo stile.
## Passaggio 11: aggiunta di un'altra casella di testo
Nessuno ha detto che potevamo aggiungere solo una casella di testo! Mettiamone un'altra con un testo diverso:
```csharp
// Aggiungi un'altra casella di testo.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Ottieni la seconda casella di testo.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Inserisci del testo.
textbox1.Text = "This is another simple text box";
```
Ora stai davvero impreziosindo il tuo foglio Excel con più caselle di testo!
## Passaggio 12: Salvataggio della cartella di lavoro
Infine, è il momento di salvare il nostro capolavoro! Ecco l'ultima riga di codice per oggi:
```csharp
// Salvare il file Excel.
workbook.Save(dataDir + "book1.out.xls");
```
Con questa sola riga di codice hai creato e modificato un file Excel con caselle di testo personalizzabili!
## Conclusione
Congratulazioni! Hai navigato con successo nel mondo delle caselle di testo in Excel usando Aspose.Cells per .NET. Non hai solo imparato come aggiungere una casella di testo, ma anche come personalizzarla per rendere i tuoi fogli di calcolo più accattivanti. Dal cambiare colori e stili all'aggiunta di collegamenti ipertestuali, le possibilità sono praticamente infinite! 
Siete pronti a iniziare a trasformare i vostri documenti Excel? Lasciate che la vostra creatività brilli e sperimentate layout diversi!
## Domande frequenti
### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire file Excel senza sforzo.
### Posso provare Aspose.Cells prima di acquistarlo?
 Sì! Puoi scaricare e utilizzare una versione di prova gratuita[Qui](https://releases.aspose.com/).
### Dove posso trovare la documentazione per Aspose.Cells?
 Puoi accedere alla documentazione completa su[Documentazione Aspose.Cells](https://reference.aspose.com/cells/net/).
### C'è supporto disponibile se riscontro dei problemi?
 Assolutamente! Se hai bisogno di aiuto, vai su[Forum di Aspose](https://forum.aspose.com/c/cells/9) per assistenza.
### Posso usare Aspose.Cells senza licenza?
 Sebbene tu possa usare una versione di prova gratuita, per accedere alla funzionalità completa, dovrai acquistare una licenza. Dai un'occhiata ai prezzi[Qui](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
