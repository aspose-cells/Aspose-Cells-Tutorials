---
"description": "Impara ad aggiungere archi ai fogli di lavoro Excel utilizzando Aspose.Cells per .NET. Segui la nostra guida passo passo per migliorare la progettazione dei tuoi fogli di calcolo."
"linktitle": "Aggiungi arco al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungi arco al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi arco al foglio di lavoro in Excel

## Introduzione
Creare fogli di calcolo Excel visivamente accattivanti è fondamentale per la presentazione dei dati e la libreria Aspose.Cells offre agli sviluppatori strumenti affidabili per raggiungere questo obiettivo. Una funzionalità interessante che potreste voler integrare nei vostri documenti Excel è la possibilità di aggiungere forme, come gli archi. In questo tutorial, vi guideremo passo dopo passo nell'aggiunta di archi a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Al termine di questo articolo, non solo imparerete ad aggiungere archi, ma acquisirete anche conoscenze generali sulla gestione delle forme.
## Prerequisiti
Prima di addentrarci nei dettagli dell'aggiunta di archi al tuo foglio di lavoro, è fondamentale assicurarsi di avere alcuni elementi a portata di mano. Ecco i prerequisiti necessari per iniziare:
1. Visual Studio: è necessario che Visual Studio sia installato sul computer poiché utilizzeremo C# come linguaggio di programmazione.
2. .NET Framework: assicurati di aver installato .NET Framework o .NET Core. Aspose.Cells supporta entrambi.
3. Aspose.Cells per .NET: è necessaria la libreria Aspose.Cells. È possibile scaricarla da [Download di Aspose.Cells](https://releases.aspose.com/cells/net/) pagina.
4. Nozioni di base di C#: avere familiarità con C# ti aiuterà a seguire i frammenti di codice senza troppa difficoltà.
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
Ecco una scomposizione passo passo del codice che mostra come aggiungere archi a un foglio di lavoro in Excel.
## Passaggio 1: impostazione della directory
Il primo passo è creare una directory in cui salvare il file Excel. Questo ti aiuterà a gestire facilmente i file di output.
```csharp
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In questo frammento di codice, specifichiamo il percorso della directory del documento. Controlliamo anche se la directory esiste; in caso contrario, la creiamo. Questo pone le basi per il nostro output.
## Passaggio 2: creare un'istanza di una cartella di lavoro
Ora creiamo una nuova istanza della cartella di lavoro.
```csharp
// Crea una nuova cartella di lavoro.
Workbook excelbook = new Workbook();
```
Questa riga crea una nuova cartella di lavoro di Excel. Consideratela come una tela bianca su cui possiamo aggiungere forme, dati e altro ancora.
## Passaggio 3: aggiungere la prima forma ad arco
Ora aggiungiamo la nostra prima forma ad arco al foglio di lavoro.
```csharp
// Aggiungere una forma ad arco.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Qui stiamo aggiungendo un arco al primo foglio di lavoro. I parametri definiscono la posizione e la dimensione dell'arco: `(left, top, width, height, startAngle, endAngle)`È come tracciare un segmento di cerchio!
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
In questa sezione, personalizziamo l'arco. Impostiamo il tipo di riempimento a tinta unita (blu in questo caso), definiamo come posizionarlo, stabiliamo lo spessore della linea e scegliamo uno stile di tratteggio. In pratica, stiamo abbellendo il nostro arco per renderlo visivamente accattivante!
## Passaggio 5: aggiungere una seconda forma ad arco
Aggiungiamo un'altra forma ad arco per fornire più contesto.
```csharp
// Aggiungere un'altra forma ad arco.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Analogamente al primo arco, ne stiamo aggiungendo un secondo sullo stesso foglio di lavoro. Le coordinate qui sono leggermente spostate per posizionarlo diversamente.
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
Qui, diamo al secondo arco narrativo lo stesso stile del primo. Puoi cambiare il colore o lo stile a tuo piacimento per renderlo unico o per motivi tematici.
## Passaggio 7: salvare la cartella di lavoro
Infine, è il momento di salvare la cartella di lavoro appena creata con gli archi.
```csharp
// Salvare il file Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Questa riga funziona come premere il pulsante "Salva". Stiamo salvando il nostro lavoro nella posizione specificata con un nome file designato. Assicurati di controllare la tua directory per vedere il tuo capolavoro in formato Excel!
## Conclusione
In questo tutorial abbiamo esplorato il processo di aggiunta di forme ad arco a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Attraverso una semplice guida passo passo, hai imparato come creare una nuova cartella di lavoro, aggiungere archi, personalizzarne l'aspetto e salvare il documento. Questa funzionalità non solo migliora l'aspetto visivo dei tuoi fogli di calcolo, ma rende anche le tue presentazioni di dati più informative. Che tu stia creando grafici, report o semplicemente sperimentando, l'utilizzo di forme come gli archi può aggiungere un tocco creativo ai tuoi progetti.
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire file Excel a livello di programmazione, senza dover ricorrere a Microsoft Excel.
### Devo installare Microsoft Excel per utilizzare Aspose.Cells?
No, Aspose.Cells è completamente indipendente e non richiede l'installazione di Microsoft Excel.
### Posso provare Aspose.Cells gratuitamente?
Sì, puoi provare Aspose.Cells usando il loro [Prova gratuita](https://releases.aspose.com/).
### Quali linguaggi di programmazione supporta Aspose.Cells?
Aspose.Cells supporta diversi linguaggi, tra cui C#, VB.NET e altri.
### Dove posso ottenere supporto per Aspose.Cells?
Puoi ottenere supporto tramite [Forum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}