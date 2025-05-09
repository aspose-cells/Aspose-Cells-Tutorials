---
"date": "2025-04-05"
"description": "Un tutorial sul codice per Aspose.Cells Net"
"title": "Creare un grafico a torta in .NET con Aspose.Cells&#58; una guida completa"
"url": "/it/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Come creare un grafico a torta in .NET utilizzando Aspose.Cells: una guida passo passo

## Introduzione

Creare rappresentazioni visive dei dati è un'abilità essenziale, soprattutto quando si cerca di trasmettere informazioni complesse in modo semplice ed efficace. Che si stia lavorando a un report aziendale o analizzando statistiche demografiche, i grafici a torta offrono un modo semplice per illustrare parti di un insieme. Questa guida vi guiderà attraverso il processo di creazione di un grafico a torta in .NET utilizzando Aspose.Cells, una potente libreria che semplifica l'utilizzo dei documenti Excel a livello di programmazione.

**Cosa imparerai:**
- Come inizializzare e impostare una cartella di lavoro di Excel.
- Inserimento di dati nelle celle del foglio di lavoro per la visualizzazione.
- Creazione e configurazione di un grafico a torta utilizzando Aspose.Cells per .NET.
- Personalizzazione dei colori delle sezioni nel grafico a torta per un impatto visivo migliore.
- Adattamento automatico delle colonne e salvataggio della cartella di lavoro.

Approfondiamo come sfruttare Aspose.Cells per creare grafici a torta accattivanti senza sforzo. Prima di iniziare, assicurati di soddisfare i prerequisiti per seguire il tutorial senza problemi.

## Prerequisiti

Per iniziare questo tutorial, assicurati di avere:

- **Librerie richieste:** Avrai bisogno della libreria Aspose.Cells per .NET. Assicurati che il tuo progetto sia configurato per utilizzarla.
- **Requisiti di configurazione dell'ambiente:** Un ambiente di sviluppo adatto, come Visual Studio, installato sul tuo sistema.
- **Prerequisiti di conoscenza:** Conoscenza di base della programmazione C# e familiarità con le strutture dei documenti Excel.

## Impostazione di Aspose.Cells per .NET

Prima di immergerti nel codice, devi installare la libreria Aspose.Cells nel tuo progetto. Ecco come fare:

### Installazione tramite CLI
Apri il terminale o il prompt dei comandi ed esegui:
```bash
dotnet add package Aspose.Cells
```

### Installazione tramite Gestione pacchetti
Se utilizzi Visual Studio, apri la console di NuGet Package Manager ed esegui:
```powershell
PM> Install-Package Aspose.Cells
```

#### Fasi di acquisizione della licenza
Puoi iniziare con una prova gratuita per valutare Aspose.Cells. Per un utilizzo prolungato, valuta la possibilità di ottenere una licenza temporanea o di acquistarla direttamente dal sito web.

#### Inizializzazione e configurazione di base

Per inizializzare la libreria nel tuo progetto C#:
```csharp
using Aspose.Cells;

// Crea un'istanza della classe Workbook
Workbook workbook = new Workbook();
```

Questa configurazione di base consente di iniziare a lavorare con i file Excel in modo programmatico.

## Guida all'implementazione

### Funzionalità 1: Inizializza la cartella di lavoro e il foglio di lavoro

**Panoramica:** Questa funzionalità imposta una nuova cartella di lavoro e accede al suo primo foglio di lavoro, preparando il terreno per l'inserimento dei dati e la creazione del grafico.

#### Inizializzazione passo passo
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Crea un nuovo oggetto cartella di lavoro
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro nella cartella di lavoro
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Qui, `Workbook` rappresenta un file Excel e l'accesso `Worksheets[0]` ti dà il primo foglio.

### Funzionalità 2: popolare i dati per il grafico a torta

**Panoramica:** Il popolamento dei dati è fondamentale in quanto costituisce la base del grafico. Questo passaggio consiste nell'inserire i nomi dei paesi e le relative percentuali di popolazione mondiale in celle specifiche.

#### Inserimento dati passo dopo passo
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Inserire i dati del paese nella colonna C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Inserisci i dati percentuali nella colonna D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Questo passaggio garantisce che i dati siano pronti per la visualizzazione.

### Funzionalità 3: creare e configurare un grafico a torta

**Panoramica:** Questa funzionalità prevede la creazione di un grafico a torta, l'impostazione dei dati della serie e la configurazione di varie proprietà, come la posizione del titolo e della legenda.

#### Creazione di grafici a torta passo dopo passo
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Aggiungere un grafico a torta al foglio di lavoro
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Imposta serie di dati per il grafico
        pie.NSeries.Add("D3:D8", true);

        // Definisci i dati della categoria e configura il titolo
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Questo codice crea un grafico visivamente accattivante collegato ai tuoi dati.

### Funzionalità 4: personalizza i colori delle sezioni nel grafico a torta

**Panoramica:** Personalizzare l'aspetto di ogni sezione migliora la leggibilità e l'estetica. Questo passaggio prevede l'assegnazione di colori unici alle diverse sezioni.

#### Personalizzazione del colore passo dopo passo
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Assegna colori personalizzati a ogni fetta
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Questo passaggio aggiunge un tocco vivace al tuo grafico.

### Funzionalità 5: Adatta automaticamente le colonne e salva la cartella di lavoro

**Panoramica:** Gli ultimi passaggi prevedono la regolazione della larghezza delle colonne per una migliore visibilità dei dati e il salvataggio della cartella di lavoro in formato Excel.

#### Regolazione e salvataggio delle colonne passo dopo passo
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Adatta automaticamente le colonne al contenuto
        worksheet.AutoFitColumns();

        // Salvare la cartella di lavoro come file Excel
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
In questo modo avrai la certezza che il documento finale sarà rifinito e pronto per la presentazione.

## Applicazioni pratiche

- **Rapporti aziendali:** Utilizzare grafici a torta per rappresentare la distribuzione delle vendite per regione.
- **Studi demografici:** Visualizza i dati sulla popolazione di diversi paesi o regioni.
- **Strumenti didattici:** Creare supporti visivi accattivanti per gli studenti nei corsi di statistica.
- **Analisi sanitaria:** Visualizza la distribuzione dei dati dei pazienti all'interno delle strutture sanitarie.

## Considerazioni sulle prestazioni

Per garantire prestazioni ottimali durante l'utilizzo di Aspose.Cells, tenere presente quanto segue:

- **Gestione efficiente dei dati:** Gestire grandi set di dati elaborandoli in blocchi, se necessario.
- **Gestione della memoria:** Smaltire gli oggetti in modo appropriato per liberare risorse ed evitare perdite di memoria.
- **Configurazioni dei grafici ottimizzate:** Riduci al minimo i calcoli o il rendering complessi durante la creazione del grafico per prestazioni più rapide.

## Conclusione

Ora hai imparato a creare un grafico a torta in .NET utilizzando Aspose.Cells. Questa potente libreria semplifica la manipolazione dei documenti Excel, permettendoti di concentrarti sull'analisi dei dati anziché sulle complessità della gestione dei file. Sperimenta i diversi tipi di grafico e le opzioni di personalizzazione disponibili in Aspose.Cells per migliorare ulteriormente le tue applicazioni.

**Prossimi passi:**
- Esplora altri tipi di grafici, come i grafici a barre o a linee.
- Integrare le funzionalità di Aspose.Cells in progetti .NET più ampi per la creazione di report automatizzati.

Pronti a portare le vostre competenze di visualizzazione dati a un livello superiore? Approfondite l'argomento esplorando le funzionalità di Aspose.Cells e iniziate a implementarle nei vostri progetti oggi stesso!

## Sezione FAQ

1. **A cosa serve Aspose.Cells?**
   - Si tratta di una libreria per la gestione programmatica dei file Excel, che consente di creare, modificare e analizzare fogli di calcolo.

2. **Posso usare Aspose.Cells senza licenza?**
   - Sì, ma con delle limitazioni. Una prova gratuita o una licenza temporanea consentono l'accesso completo alle funzionalità.

3. **Come posso personalizzare ulteriormente l'aspetto del mio grafico a torta?**
   - Utilizzare proprietà aggiuntive come `pie.NSeries[0].Area.Formatting` per un maggiore controllo sull'estetica.

4. **Quali sono alcuni problemi comuni durante la creazione di grafici in Aspose.Cells?**
   - Prima del rendering, assicurati che gli intervalli di dati siano specificati correttamente e che siano state configurate tutte le proprietà necessarie del grafico.

5. **Come posso integrare Aspose.Cells con altre librerie .NET?**
   - Utilizzare Aspose.Cells come parte di una soluzione .NET più ampia, sfruttandone le capacità insieme ad altre librerie per applicazioni complete.

## Risorse

- **Documentazione:** [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Scaricamento:** [Rilasci di Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Acquistare:** [Acquista Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova gratuita:** [Prova gratuita di Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Licenza temporanea:** [Ottieni una licenza temporanea](https://purchase.aspose.com/temporary-license/)
- **Supporto:** [Forum Aspose](https://forum.aspose.com/c/cells/9)

Seguendo questa guida, sarai ora in grado di creare grafici a torta visivamente accattivanti nelle applicazioni .NET utilizzando Aspose.Cells. Buon lavoro!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}