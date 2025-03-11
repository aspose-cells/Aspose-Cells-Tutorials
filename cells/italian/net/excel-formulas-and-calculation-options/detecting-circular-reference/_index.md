---
title: Rilevamento del riferimento circolare in Excel tramite programmazione
linktitle: Rilevamento del riferimento circolare in Excel tramite programmazione
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Rileva facilmente riferimenti circolari in Excel usando Aspose.Cells per .NET. Segui la nostra guida passo passo per garantire calcoli accurati nei tuoi fogli di calcolo.
weight: 13
url: /it/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rilevamento del riferimento circolare in Excel tramite programmazione

## Introduzione
Quando si tratta di lavorare con file Excel, uno dei problemi più frustranti che potresti incontrare è un riferimento circolare. Ciò accade quando una formula fa riferimento alla propria cella, direttamente o indirettamente, creando un loop che può confondere il motore di calcolo di Excel. Ma non temere! Con Aspose.Cells per .NET, puoi rilevare a livello di programmazione questi fastidiosi riferimenti circolari, assicurandoti che i tuoi fogli di calcolo rimangano funzionali e precisi. In questa guida, ti guideremo passo dopo passo nel processo, rendendolo semplice come una torta.
## Prerequisiti
Prima di addentrarci nei dettagli del rilevamento dei riferimenti circolari, assicuriamoci di avere tutto il necessario per iniziare:
1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. Questo sarà il tuo ambiente di sviluppo.
2. .NET Framework: assicurati di utilizzare una versione compatibile di .NET Framework (almeno .NET Framework 4.0).
3.  Libreria Aspose.Cells: devi avere la libreria Aspose.Cells. Puoi scaricarla da[Sito web di Aspose](https://releases.aspose.com/cells/net/).
4. Conoscenza di base di C#: la familiarità con la programmazione C# sarà utile poiché scriveremo codice in questo linguaggio.
5. File Excel: Tieni pronto un file Excel che contenga riferimenti circolari per i test. Puoi crearne uno semplice o scaricare un campione.
Ora che abbiamo chiarito i prerequisiti, passiamo alla parte divertente!
## Importa pacchetti
Prima di poter iniziare a programmare, devi importare i pacchetti necessari. Ecco come fare:
### Crea un nuovo progetto
- Aprire Visual Studio e creare un nuovo progetto di applicazione console C#.
### Aggiungi riferimento Aspose.Cells
- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Seleziona "Gestisci pacchetti NuGet".
- Cerca “Aspose.Cells” e installa la versione più recente.
### Importa gli spazi dei nomi richiesti
 In cima al tuo`Program.cs` file, importa gli spazi dei nomi necessari:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ora che abbiamo impostato tutto, analizziamo il codice per rilevare i riferimenti circolari in un file Excel.
## Passaggio 1: definire la directory di input
Per prima cosa, devi specificare la directory in cui si trova il tuo file Excel. È qui che caricherai il tuo file Excel.
```csharp
// Directory di input
string sourceDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"` con il percorso effettivo del file Excel.
## Passaggio 2: caricare la cartella di lavoro con LoadOptions
Poi, caricherai la tua cartella di lavoro Excel. È qui che inizia la magia!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Qui stiamo creando una nuova istanza di`LoadOptions` e caricando la cartella di lavoro dal percorso specificato. Assicurati che il nome del file Excel corrisponda!
## Passaggio 3: abilitare le impostazioni di iterazione
Per consentire riferimenti circolari, è necessario abilitare le impostazioni di iterazione nella cartella di lavoro.
```csharp
objWB.Settings.Iteration = true;
```
Questo indica ad Aspose.Cells di consentire riferimenti circolari durante il calcolo.
## Passaggio 4: creare opzioni di calcolo e monitor circolare
Ora creiamo le opzioni di calcolo e il nostro monitor circolare personalizzato.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Qui stiamo creando un'istanza di`CalculationOptions` e un'usanza`CircularMonitor`Questo monitor aiuterà a tenere traccia di eventuali riferimenti circolari trovati durante i calcoli.
## Passaggio 5: calcolare le formule
Adesso è il momento di calcolare le formule presenti nella tua cartella di lavoro.
```csharp
objWB.CalculateFormula(copts);
```
Questa riga esegue il calcolo e controlla i riferimenti circolari.
## Passaggio 6: contare i riferimenti circolari
Dopo il calcolo, è possibile contare quanti riferimenti circolari sono stati trovati.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Verrà visualizzato il numero di riferimenti circolari rilevati nel file Excel.
## Passaggio 7: visualizzare i risultati
Infine, visualizziamo i risultati e confermiamo che il nostro metodo è stato eseguito correttamente.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Passaggio 8: implementare la classe CircularMonitor
 Per completare il processo, dovrai implementare il`CircularMonitor` classe. Questa classe erediterà da`AbstractCalculationMonitor` e gestire il rilevamento dei riferimenti circolari.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Questa classe cattura i dettagli di ogni riferimento circolare trovato, incluso il nome del foglio di lavoro e l'indice della cella.
## Conclusione
Rilevare riferimenti circolari in Excel usando Aspose.Cells per .NET è un processo semplice una volta suddiviso in passaggi gestibili. Seguendo questa guida, puoi identificare e gestire facilmente i riferimenti circolari nei tuoi fogli di calcolo, assicurandoti che i tuoi calcoli rimangano accurati e affidabili. Che tu sia uno sviluppatore esperto o alle prime armi, Aspose.Cells fornisce potenti strumenti per migliorare le tue capacità di manipolazione di Excel. 
## Domande frequenti
### Che cosa è un riferimento circolare in Excel?
Un riferimento circolare si verifica quando una formula fa riferimento alla propria cella, causando un ciclo infinito nei calcoli.
### Come posso rilevare i riferimenti circolari a livello di programmazione?
È possibile utilizzare la libreria Aspose.Cells in .NET per rilevare a livello di programmazione i riferimenti circolari implementando un monitor di calcolo personalizzato.
### Quali sono i prerequisiti per utilizzare Aspose.Cells?
È necessario che siano installati Visual Studio, .NET Framework e la libreria Aspose.Cells.
### Posso usare Aspose.Cells gratuitamente?
Sì, Aspose.Cells offre una prova gratuita che puoi utilizzare per esplorarne le funzionalità.
### Dove posso trovare maggiori informazioni su Aspose.Cells?
 Puoi visitare il[Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) per informazioni dettagliate ed esempi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
