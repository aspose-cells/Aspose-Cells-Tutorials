---
title: Aggiungi arco al foglio di lavoro in Excel
linktitle: Aggiungi arco al foglio di lavoro in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Impara ad aggiungere archi ai fogli di lavoro Excel usando Aspose.Cells per .NET. Segui la nostra guida passo passo per migliorare i tuoi progetti di fogli di calcolo.
weight: 16
url: /it/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi arco al foglio di lavoro in Excel

## Introduzione
Creare fogli di calcolo Excel visivamente accattivanti è fondamentale per la presentazione dei dati e la libreria Aspose.Cells fornisce agli sviluppatori strumenti robusti per svolgere questo compito. Una caratteristica interessante che potresti voler incorporare nei tuoi documenti Excel è la possibilità di aggiungere forme, come gli archi. In questo tutorial, ti guideremo passo dopo passo su come aggiungere archi a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Alla fine di questo articolo, non solo imparerai come aggiungere archi, ma acquisirai anche una visione della gestione delle forme in generale.
## Prerequisiti
Prima di immergerci nei dettagli dell'aggiunta di archi al tuo foglio di lavoro, è essenziale assicurarti di avere alcune cose a posto. Ecco i prerequisiti di cui avrai bisogno per iniziare:
1. Visual Studio: sarà necessario che Visual Studio sia installato sul computer poiché utilizzeremo C# come linguaggio di programmazione.
2. .NET Framework: assicurati di avere installato .NET Framework o .NET Core. Aspose.Cells supporta entrambi.
3. Aspose.Cells per .NET: devi avere la libreria Aspose.Cells. Puoi scaricarla da[Download di Aspose.Cells](https://releases.aspose.com/cells/net/) pagina.
4. Nozioni di base di C#: la familiarità con C# ti aiuterà a seguire i frammenti di codice senza troppa difficoltà.
## Importa pacchetti
Per iniziare a lavorare con Aspose.Cells nel tuo progetto, devi importare i pacchetti necessari. Ecco come fare:
### Crea un nuovo progetto
- Aprire Visual Studio.
- Seleziona "Crea un nuovo progetto".
- Selezionare un modello che funzioni con .NET (ad esempio Applicazione console).
  
### Aggiungi riferimenti Aspose.Cells
- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Seleziona "Gestisci pacchetti NuGet".
- Cerca “Aspose.Cells” e installalo.
Ora sei pronto per iniziare a codificare l'addizione dell'arco.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ecco una ripartizione dettagliata del codice che mostra come aggiungere archi a un foglio di lavoro in Excel.
## Passaggio 1: impostazione della directory
Il primo passo è impostare una directory in cui salvare il file Excel. Questo aiuta a gestire facilmente i file di output.
```csharp
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In questo frammento di codice, specifichiamo il percorso alla directory del documento. Controlliamo anche se la directory esiste; in caso contrario, la creiamo. Questo imposta le basi per il nostro output.
## Passaggio 2: creare un'istanza di una cartella di lavoro
Ora creiamo una nuova istanza della cartella di lavoro.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
Questa riga crea una nuova cartella di lavoro Excel. Immaginala come una tela bianca dove possiamo aggiungere forme, dati e altro.
## Passaggio 3: aggiungere la prima forma ad arco
Ora aggiungiamo la nostra prima forma ad arco al foglio di lavoro.
```csharp
// Aggiungere una forma ad arco.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Qui, stiamo aggiungendo un arco al primo foglio di lavoro. I parametri definiscono la posizione e la dimensione dell'arco:`(left, top, width, height, startAngle, endAngle)`È come tracciare un segmento di cerchio!
## Passaggio 4: personalizza il primo arco
Dopo aver aggiunto l'arco, potresti voler personalizzarne l'aspetto.
```csharp
// Imposta il colore della forma di riempimento
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Imposta la posizione dell'arco.
arc1.Placement = PlacementType.FreeFloating;           
// Imposta lo spessore della linea.
arc1.Line.Weight = 1;      
// Imposta lo stile del trattino dell'arco.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
In questa sezione, personalizziamo l'arco. Impostiamo il suo tipo di riempimento su colore pieno (blu in questo caso), definiamo come è posizionato, stabiliamo lo spessore della linea e scegliamo uno stile di tratteggio. In pratica, stiamo abbellendo il nostro arco per renderlo visivamente accattivante!
## Passaggio 5: aggiungere una seconda forma ad arco
Aggiungiamo un'altra forma ad arco per fornire più contesto.
```csharp
// Aggiungere un'altra forma ad arco.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Similmente al primo arco, stiamo aggiungendo un secondo arco sullo stesso foglio di lavoro. Le coordinate qui sono un po' spostate per posizionarlo diversamente.
## Passaggio 6: personalizza il secondo arco
Proprio come abbiamo fatto con il primo arco narrativo, personalizzeremo anche il secondo.
```csharp
// Imposta il colore della linea
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Imposta la posizione dell'arco.
arc2.Placement = PlacementType.FreeFloating;          
// Imposta lo spessore della linea.
arc2.Line.Weight = 1;           
// Imposta lo stile del trattino dell'arco.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Qui, stiamo dando al secondo arco lo stesso stile del primo. Puoi cambiare il colore o lo stile come preferisci per motivi di unicità o tematici.
## Passaggio 7: salvare la cartella di lavoro
Infine, è il momento di salvare la cartella di lavoro appena creata con gli archi.
```csharp
// Salvare il file Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Questa riga funziona come premere il pulsante salva. Stiamo salvando il nostro lavoro nella posizione specificata con un nome file designato. Assicurati di controllare la tua directory per vedere il tuo capolavoro in formato Excel!
## Conclusione
In questo tutorial, abbiamo esplorato il processo di aggiunta di forme ad arco a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Tramite una semplice guida passo-passo, hai imparato come creare una nuova cartella di lavoro, aggiungere archi, personalizzarne l'aspetto e salvare il documento. Questa capacità non solo migliora l'aspetto visivo dei tuoi fogli di calcolo, ma rende anche le tue presentazioni di dati più informative. Che tu stia creando grafici, report o semplicemente sperimentando, l'utilizzo di forme come gli archi può aggiungere un tocco creativo ai tuoi progetti.
## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire file Excel a livello di programmazione, senza dover ricorrere a Microsoft Excel.
### Devo installare Microsoft Excel per utilizzare Aspose.Cells?
No, Aspose.Cells è completamente indipendente e non richiede l'installazione di Microsoft Excel.
### Posso provare Aspose.Cells gratuitamente?
 Sì, puoi provare Aspose.Cells usando il loro[Prova gratuita](https://releases.aspose.com/).
### Quali linguaggi di programmazione supporta Aspose.Cells?
Aspose.Cells supporta diversi linguaggi, tra cui C#, VB.NET e altri.
### Dove posso ottenere supporto per Aspose.Cells?
 Puoi ottenere supporto tramite[Forum di Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
