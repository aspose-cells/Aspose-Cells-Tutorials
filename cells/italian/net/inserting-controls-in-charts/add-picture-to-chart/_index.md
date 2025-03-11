---
title: Aggiungi immagine al grafico
linktitle: Aggiungi immagine al grafico
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come aggiungere facilmente immagini ai grafici Excel usando Aspose.Cells per .NET. Migliora i tuoi grafici e le tue presentazioni in pochi semplici passaggi.
weight: 11
url: /it/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi immagine al grafico

## Introduzione

Sei stanco di grafici noiosi che non hanno un tocco personale? Vuoi imparare a ravvivare i tuoi elementi visivi Excel aggiungendo immagini? Bene, sei fortunato! In questo tutorial, ci immergeremo nel mondo di Aspose.Cells per .NET e impareremo come aggiungere immagini ai grafici in Excel. Quindi, prendi la tua tazza di caffè preferita e iniziamo!

## Prerequisiti

Prima di addentrarci nei dettagli della codifica, ecco alcuni prerequisiti che devi soddisfare per seguire il tutorial senza problemi:

- Visual Studio: qui è dove scriverai ed eseguirai il tuo codice .NET. Assicurati di averlo installato.
-  Aspose.Cells per .NET: questa libreria ti servirà per lavorare con i file Excel. Puoi[scaricalo qui](https://releases.aspose.com/cells/net/).
- Nozioni di base di C#: anche se ti guiderò attraverso il codice, avere una conoscenza delle basi di C# renderà le cose più chiare.

### Fasi di installazione

1. Installa Aspose.Cells: puoi aggiungere Aspose.Cells al tuo progetto Visual Studio tramite NuGet Package Manager. Per farlo, vai su Strumenti > NuGet Package Manager > Gestisci pacchetti NuGet per la soluzione e cerca "Aspose.Cells". Fai clic su Installa.
2. Impostazione del progetto: crea un nuovo progetto di applicazione console C# in Visual Studio.

## Importa pacchetti

Una volta che hai impostato tutto, il passo successivo è importare i pacchetti necessari nel tuo progetto. Ecco come fare:

### Importare gli spazi dei nomi richiesti

Nella parte superiore del file di codice C#, dovrai importare i seguenti namespace:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Questo dice al tuo programma: "Ehi! Userò queste fantastiche funzionalità di Aspose.Cells".

Ora che abbiamo definito i prerequisiti, suddividiamo il processo in piccoli passaggi. 

## Passaggio 1: definisci le tue directory

Per prima cosa, dobbiamo impostare i percorsi per i nostri file di input e output. Questo passaggio è cruciale perché dobbiamo sapere dove trovare il nostro file Excel esistente e dove salvare il file modificato.

```csharp
//Elenco di origine
string sourceDir = "Your Document Directory/";

//Directory di output
string outputDir = "Your Output Directory/";
```

 Sostituire`Your Document Directory` E`Your Output Directory` con percorsi effettivi sul tuo computer. 

## Passaggio 2: caricare la cartella di lavoro esistente

Ora carichiamo il file Excel esistente in cui vogliamo aggiungere la nostra immagine al grafico.

```csharp
// Aprire il file esistente.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Questo codice apre la cartella di lavoro, rendendola pronta per la modifica.

## Passaggio 3: preparare il flusso di immagini

Prima di aggiungere l'immagine, dobbiamo leggere l'immagine che vogliamo inserire nel grafico. 

```csharp
// Ottenere un file immagine per il flusso.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Assicuratevi di aver salvato l'immagine nella directory specificata.

## Passaggio 4: mira al grafico

Ora, specifichiamo a quale grafico aggiungeremo la nostra immagine. In questo esempio, punteremo al primo grafico del primo foglio di lavoro.

```csharp
// Prendi la tabella del designer nel secondo foglio.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

È possibile accedere a qualsiasi foglio di lavoro modificando opportunamente l'indice.

## Passaggio 5: aggiungere l'immagine al grafico

Una volta selezionato il grafico, è il momento di aggiungere l'immagine! 

```csharp
// Aggiungi una nuova immagine al grafico.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Qui,`50` E`50` sono le coordinate X e Y in cui verrà posizionata l'immagine, e`200` è la larghezza e l'altezza dell'immagine.

## Passaggio 6: personalizzare il formato della linea dell'immagine

Vuoi aggiungere un tocco di stile alla tua foto? Puoi personalizzarne il bordo! Ecco come fare:

```csharp
// Ottieni il tipo di formato della linea dell'immagine.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Imposta lo stile del trattino.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Imposta lo spessore della linea.
lineformat.Weight = 4;    
```

Questo frammento ti consente di scegliere l'aspetto e lo spessore del bordo. Scegli qualsiasi stile che risuoni con la tua presentazione!

## Passaggio 7: salvare la cartella di lavoro modificata

Dopo tutto questo duro lavoro, salviamo le modifiche eseguendo la seguente riga di codice:

```csharp
// Salvare il file Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Ora la tua immagine è integrata correttamente nel grafico e il file di output è pronto per essere visualizzato!

## Passaggio 8: indicare il successo

Infine, puoi aggiungere un semplice messaggio per confermare che l'operazione è andata a buon fine:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusione

In questo tutorial, abbiamo esplorato come iniettare un po' di personalità nei tuoi grafici Excel aggiungendo immagini usando Aspose.Cells per .NET. Con pochi semplici passaggi, puoi elevare le tue presentazioni da banali a memorabili. Quindi, cosa aspetti? Provaci e fai risplendere i tuoi grafici!

## Domande frequenti

### Posso aggiungere più immagini a un singolo grafico?
 Sì! Puoi chiamare il`AddPictureInChart` metodo più volte per aggiungere tutte le immagini che desideri.

### Quali formati di immagine supporta Aspose.Cells?
Aspose.Cells supporta diversi formati di immagine, tra cui PNG, JPEG, BMP e GIF.

### Posso personalizzare la posizione dell'immagine?
 Certamente! Le coordinate X e Y nel`AddPictureInChart` metodo consente un posizionamento preciso.

### Aspose.Cells è gratuito?
Aspose.Cells offre una prova gratuita, ma per le funzionalità complete è richiesta una licenza. Puoi trovare i prezzi[Qui](https://purchase.aspose.com/buy).

### Dove posso trovare altri esempi?
 Dai un'occhiata al[Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) per esempi e funzionalità più dettagliati.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
