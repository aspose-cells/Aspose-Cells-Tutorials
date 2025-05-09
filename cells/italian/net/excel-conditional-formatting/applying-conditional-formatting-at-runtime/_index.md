---
"description": "Scopri come applicare la formattazione condizionale in fase di esecuzione in Excel con Aspose.Cells per .NET in questa guida completa e dettagliata."
"linktitle": "Applicazione della formattazione condizionale in fase di esecuzione in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Applicazione della formattazione condizionale in fase di esecuzione in Excel"
"url": "/it/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Applicazione della formattazione condizionale in fase di esecuzione in Excel

## Introduzione

Sono strumenti potenti per l'analisi e la visualizzazione dei dati. Una delle funzionalità più importanti di Excel è la formattazione condizionale, che consente agli utenti di applicare stili di formattazione specifici alle celle in base ai loro valori. Questo può semplificare l'identificazione di tendenze, evidenziare punti dati importanti o semplicemente rendere i dati più leggibili. Se stai cercando di implementare la formattazione condizionale nei tuoi file Excel a livello di codice, sei nel posto giusto! In questa guida, spiegheremo come applicare la formattazione condizionale in fase di esecuzione utilizzando Aspose.Cells per .NET.

## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di avere tutto il necessario per iniziare:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. Puoi utilizzare qualsiasi versione che supporti lo sviluppo .NET.
2. Aspose.Cells per .NET: è necessario aver installato Aspose.Cells per .NET. È possibile scaricarlo da [Sito web di Aspose](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
4. .NET Framework: assicurati che il tuo progetto sia destinato a una versione compatibile di .NET Framework.

Ora che abbiamo chiarito i prerequisiti, passiamo alla parte divertente!

## Importa pacchetti
Per iniziare a usare Aspose.Cells, devi importare gli spazi dei nomi necessari nel tuo progetto C#. Ecco come fare:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Questi spazi dei nomi ti daranno accesso alle classi e ai metodi necessari per manipolare i file Excel e applicare la formattazione condizionale.

Ora scomponiamo il processo di applicazione della formattazione condizionale in passaggi gestibili.

## Passaggio 1: imposta il tuo progetto
Per prima cosa, devi creare un nuovo progetto C# in Visual Studio. Ecco come fare:

1. Aprire Visual Studio e selezionare File > Nuovo > Progetto.
2. Seleziona App console (.NET Framework) e assegna un nome al progetto.
3. Fare clic su Crea.

## Passaggio 2: aggiungere il riferimento Aspose.Cells
Una volta impostato il progetto, è necessario aggiungere un riferimento alla libreria Aspose.Cells:

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
2. Selezionare Gestisci pacchetti NuGet.
3. Cerca Aspose.Cells e installalo.

Ciò consentirà di utilizzare tutte le funzionalità fornite dalla libreria Aspose.Cells.

## Passaggio 3: creare un oggetto cartella di lavoro
Ora creiamo una nuova cartella di lavoro e un nuovo foglio di lavoro. È qui che avviene tutta la magia:

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

In questo passaggio definiamo la directory in cui verrà salvato il nostro file Excel, creiamo una nuova cartella di lavoro e accediamo al primo foglio di lavoro.

## Passaggio 4: aggiungere la formattazione condizionale
Ora aggiungiamo un po' di formattazione condizionale. Inizieremo creando un oggetto di formattazione condizionale vuoto:

```csharp
// Aggiunge una formattazione condizionale vuota
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Qui stiamo aggiungendo una nuova raccolta di formattazione condizionale al nostro foglio di lavoro, che conterrà le nostre regole di formattazione.

## Passaggio 5: definire l'intervallo di formato
Successivamente, dobbiamo specificare l'intervallo di celle a cui verrà applicata la formattazione condizionale. Supponiamo di voler formattare la prima riga e la seconda colonna:

```csharp
// Imposta l'intervallo del formato condizionale.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

In questo codice, definiamo due aree per la formattazione condizionale. La prima area è per la cella in (0,0) e la seconda per (1,1). Sentiti libero di adattare questi intervalli in base alle tue esigenze specifiche!

## Passaggio 6: aggiungere condizioni di formattazione condizionale
Ora è il momento di definire le condizioni per la formattazione. Supponiamo di voler evidenziare le celle in base ai loro valori:

```csharp
// Aggiunge una condizione.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Aggiunge una condizione.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

In questo passaggio, aggiungiamo due condizioni: una per i valori compresi tra `A2` E `100`, e un altro per i valori compresi tra `50` E `100`Ciò consente di evidenziare dinamicamente le celle in base ai loro valori.

## Passaggio 7: imposta gli stili di formattazione
Una volta impostate le condizioni, possiamo ora impostare gli stili di formattazione. Modifichiamo il colore di sfondo per le nostre condizioni:

```csharp
// Imposta il colore di sfondo.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Qui, impostiamo il colore di sfondo della prima condizione su rosso. Puoi personalizzarlo ulteriormente cambiando il colore del carattere, i bordi e altri stili a seconda delle tue esigenze!

## Passaggio 8: salvare il file Excel
Infine, è il momento di salvare il nostro lavoro! Salveremo la cartella di lavoro nella directory specificata:

```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "output.xls");
```

Questa riga di codice salva il file Excel con la formattazione condizionale applicata. Assicurati di controllare la directory specificata per il file di output!

## Conclusione
Ed ecco fatto! Hai applicato con successo la formattazione condizionale in fase di esecuzione in Excel utilizzando Aspose.Cells per .NET. Questa potente libreria semplifica la manipolazione dei file Excel a livello di codice, consentendoti di automatizzare attività noiose e migliorare la presentazione dei dati. Che tu stia lavorando a un piccolo progetto o a un'applicazione su larga scala, Aspose.Cells può aiutarti a semplificare il flusso di lavoro e a migliorare la produttività.

## Domande frequenti

### Che cosa è Aspose.Cells?
Aspose.Cells è una libreria .NET che consente agli sviluppatori di creare, manipolare e convertire file Excel a livello di programmazione.

### Posso usare Aspose.Cells con altri linguaggi di programmazione?
Sì, Aspose.Cells è disponibile per diversi linguaggi di programmazione, tra cui Java, Python e altri.

### È disponibile una prova gratuita per Aspose.Cells?
Sì, puoi scaricare una versione di prova gratuita da [Sito web di Aspose](https://releases.aspose.com/).

### Come posso ottenere supporto per Aspose.Cells?
Puoi ottenere supporto visitando il [Forum di supporto di Aspose](https://forum.aspose.com/c/cells/9).

### Ho bisogno di una licenza per utilizzare Aspose.Cells?
Sì, è richiesta una licenza per l'uso commerciale, ma è possibile richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}