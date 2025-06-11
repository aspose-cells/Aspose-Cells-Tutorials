---
"description": "Scopri come controllare le risorse esterne in Excel utilizzando Aspose.Cells per .NET con il nostro tutorial completo passo dopo passo."
"linktitle": "Controlla le risorse esterne utilizzando le impostazioni della cartella di lavoro"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Controlla le risorse esterne utilizzando le impostazioni della cartella di lavoro"
"url": "/it/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Controlla le risorse esterne utilizzando le impostazioni della cartella di lavoro

## Introduzione
Nell'ambito della manipolazione e della presentazione dei dati, gestire in modo efficiente le risorse esterne può fare la differenza. Se lavori con file Excel e desideri gestire le risorse esterne in modo fluido utilizzando Aspose.Cells per .NET, sei nel posto giusto! In questo articolo, approfondiremo il controllo delle risorse esterne quando si lavora con le cartelle di lavoro di Excel. Al termine di questa guida, sarai in grado di implementare una soluzione personalizzata per caricare immagini e dati da fonti esterne senza problemi.
## Prerequisiti
Prima di addentrarci nel vivo della programmazione, ecco alcuni prerequisiti che è necessario soddisfare. Assicurati di:
1. Visual Studio: avrai bisogno di un IDE per scrivere e testare le tue applicazioni .NET. Visual Studio è l'opzione più consigliata per il suo ampio supporto e la sua facilità d'uso.
2. Scarica Aspose.Cells per .NET: se non l'hai già fatto, scarica la libreria Aspose.Cells da [collegamento per il download](https://releases.aspose.com/cells/net/). 
3. Conoscenza di base di C#: la familiarità con i concetti di C# e del framework .NET renderà il processo più semplice.
4. Configura l'ambiente: assicurati che il progetto faccia riferimento alla libreria Aspose.Cells. Puoi farlo tramite NuGet Package Manager in Visual Studio.
5. File di esempio: tieni a portata di mano un file Excel di esempio che includa una risorsa esterna, ad esempio un'immagine collegata. Questo file ti aiuterà a illustrare le funzionalità che discuteremo.
Una volta impostati questi elementi, sei pronto per passare al controllo delle risorse esterne con Aspose.Cells.
## Importa pacchetti
Per iniziare a programmare, dovrai importare i pacchetti necessari nel tuo file C#. Ecco cosa ti serve:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Questi namespace forniscono l'accesso alle funzionalità richieste per manipolare i file Excel e gestire le immagini.
Analizziamolo in passaggi gestibili per aiutarti a controllare le risorse esterne utilizzando `Workbook Settings`Ti guideremo nella creazione di un provider di streaming personalizzato, nel caricamento di un file Excel e nel rendering di un foglio di lavoro come immagine. Sentiti libero di seguirci!
## Passaggio 1: definire le directory di origine e di output
Per iniziare, dobbiamo specificare le directory da cui leggeremo i file e dove salveremo l'output. È fondamentale impostare i percorsi corretti per evitare errori di file non trovato.
```csharp
// Directory di origine
static string sourceDir = "Your Document Directory";
// Directory di output
static string outputDir = "Your Document Directory";
```
Sostituire `"Your Document Directory"` con il percorso effettivo in cui si trovano i tuoi file.
## Passaggio 2: implementare l'interfaccia IStreamProvider
Successivamente, creeremo una classe personalizzata che implementa il `IStreamProvider` interfaccia. Questa classe gestirà le modalità di accesso alle risorse esterne (come le immagini).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Se necessario, ripulisci tutte le risorse
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Aprire il flusso di file della risorsa esterna
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
Nel `InitStream` metodo, apriamo il file che funge da risorsa esterna e lo assegniamo al `Stream` proprietà. Ciò consente alla cartella di lavoro di accedere alla risorsa durante il rendering.
## Passaggio 3: caricare il file Excel
Ora che il nostro provider di streaming è pronto, carichiamo la cartella di lavoro di Excel che contiene la risorsa esterna.
```csharp
public static void Run()
{
    // Carica il file Excel di esempio
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Fornisci la tua implementazione di IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
In questo frammento, carichiamo il nostro file Excel e assegniamo il nostro personalizzato `StreamProvider` implementazione per gestire le risorse esterne.
## Passaggio 4: accedi al foglio di lavoro
Dopo aver caricato la cartella di lavoro, possiamo accedere facilmente al foglio di lavoro desiderato. Prendiamo il primo.
```csharp
    // Accedi al primo foglio di lavoro
    Worksheet ws = wb.Worksheets[0];
```
Semplice, vero? Puoi accedere a qualsiasi foglio di lavoro specificandone l'indice.
## Passaggio 5: configurare le opzioni di immagine o stampa
Ora definiremo l'aspetto dell'immagine di output. Configureremo opzioni come garantire che ci sia una pagina per ogni foglio e specificare il tipo di immagine di output.
```csharp
    // Specificare le opzioni di immagine o stampa
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Scegliendo PNG come formato di output avrai la certezza che la qualità rimarrà nitida e chiara!
## Passaggio 6: Trasforma il foglio di lavoro in un'immagine
Una volta impostato tutto, trasformiamo il foglio di lavoro scelto in un file immagine! Questa è la parte più emozionante: vedrai il tuo foglio Excel trasformato in una splendida immagine.
```csharp
    // Crea un rendering del foglio passando i parametri richiesti
    SheetRender sr = new SheetRender(ws, opts);
    // Converti l'intero foglio di lavoro in un'immagine png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
IL `ToImage` La funzione fa tutto il lavoro pesante, convertendo il foglio in un'immagine. Una volta completato questo passaggio, troverai l'immagine salvata nella directory di output.
## Conclusione
Ed ecco fatto! Ora possiedi le competenze necessarie per controllare le risorse esterne quando lavori con file Excel utilizzando Aspose.Cells in .NET. Questo non solo migliora le capacità della tua applicazione, ma semplifica anche la gestione di set di dati e presentazioni. Seguendo i passaggi indicati, puoi replicare e adattare facilmente questa funzionalità alle esigenze specifiche del tuo progetto.
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria progettata per consentire agli sviluppatori C# e .NET di creare, manipolare e gestire file Excel senza dover installare Microsoft Excel.
### Come posso scaricare Aspose.Cells per .NET?
Puoi scaricarlo da [Sito web di Aspose](https://releases.aspose.com/cells/net/).
### È disponibile una prova gratuita?
Sì! Puoi accedere a una prova gratuita di Aspose.Cells dal loro [pagina di rilascio](https://releases.aspose.com/).
### Quali tipi di file supporta Aspose.Cells?
Aspose.Cells supporta vari formati Excel, tra cui XLS, XLSX, CSV e altri.
### Dove posso trovare supporto per Aspose.Cells?
Puoi visitare il forum di supporto di Aspose all'indirizzo [Forum Aspose](https://forum.aspose.com/c/cells/9) per assistenza.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}