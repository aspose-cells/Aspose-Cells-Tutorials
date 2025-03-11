---
title: Estrai il file Mol incorporato dalla cartella di lavoro
linktitle: Estrai il file Mol incorporato dalla cartella di lavoro
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come estrarre i file MOL incorporati dalle cartelle di lavoro di Excel utilizzando Aspose.Cells per .NET in questo tutorial dettagliato passo dopo passo.
weight: 18
url: /it/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai il file Mol incorporato dalla cartella di lavoro

## Introduzione
Quando si tratta di gestire i dati all'interno delle cartelle di lavoro di Excel, a volte si incontrano vari oggetti incorporati che non sono in un formato standard. Uno di questi formati è il MOL (Molecular Structure File), comunemente utilizzato in chimica per rappresentare informazioni molecolari. Se stai cercando di estrarre questi file MOL da una cartella di lavoro di Excel utilizzando Aspose.Cells per .NET, sei arrivato sulla guida giusta. In questo articolo, ti guideremo passo dopo passo nel processo, svelando ogni parte lungo il percorso.
## Prerequisiti
Prima di immergerti nel codice, è essenziale assicurarti di avere le competenze e gli strumenti necessari. Ecco cosa ti servirà:
1. Nozioni di base sulla programmazione .NET: è necessario avere familiarità con C# e con il framework .NET.
2.  Aspose.Cells per .NET: assicurati di avere la libreria Aspose.Cells. Puoi[scaricalo qui](https://releases.aspose.com/cells/net/).
3. Un IDE: puoi utilizzare Visual Studio o qualsiasi altro IDE compatibile con .NET.
4. Cartella di lavoro Excel con file MOL incorporati: per questo tutorial, hai bisogno di un file Excel contenente oggetti MOL. Puoi crearne uno tuo o usare qualsiasi file di esempio.
## Importa pacchetti
Per iniziare, dovrai importare i namespace necessari nel tuo progetto. Questo è fondamentale per accedere alle funzionalità di Aspose.Cells. Ecco come puoi farlo:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Questi spazi dei nomi consentiranno di manipolare cartelle di lavoro, accedere ai fogli di lavoro e lavorare con i file in generale.
Ora che abbiamo chiarito i prerequisiti, analizziamo il codice e comprendiamo ogni passaggio necessario per estrarre i file MOL incorporati da una cartella di lavoro di Excel. 
## Passaggio 1: impostazione delle directory
Il primo passo è definire dove si trova il documento sorgente e dove si desidera salvare i file MOL estratti. Impostiamo queste directory.
```csharp
string SourceDir = "Your Document Directory"; // Sostituisci con il percorso della tua directory
string outputDir = "Your Document Directory"; // Sostituisci con il tuo percorso di output
```
 Qui, sostituisci`"Your Document Directory"`con il percorso alle tue directory effettive. È importante che sia la directory di origine che quella di output siano accessibili alla tua applicazione.
## Passaggio 2: caricamento della cartella di lavoro
Una volta impostate le directory, il compito successivo è caricare la cartella di lavoro di Excel. Facciamolo ora.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Stiamo creando un'istanza di`Workbook` classe e passando il percorso al nostro file Excel denominato`EmbeddedMolSample.xlsx`Questo passaggio inizializza la cartella di lavoro, consentendo di accederne al contenuto.
## Fase 3: iterazione sui fogli di lavoro
Ora che la tua cartella di lavoro è caricata, devi scorrere ogni foglio di lavoro al suo interno. Questo ti consente di esaminare ogni foglio per gli oggetti incorporati.

```csharp
var index = 1; // Utilizzato per nominare i file MOL estratti
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Qui va la logica di estrazione ulteriore
}
```

 Qui, stai usando un`foreach` loop per navigare tra i fogli di lavoro. Per ogni foglio di lavoro, accedi al`OleObjects` raccolta, che contiene tutti gli oggetti incorporati.
## Passaggio 4: estrazione dei file MOL
Ora arriva la parte critica: estrarre i file MOL dagli oggetti OLE. Ciò richiede un altro ciclo all'interno del ciclo del foglio di lavoro.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Per ogni oggetto OLE trovato, stai creando un nuovo file nella directory di output.`ObjectData` proprietà del`OleObject` contiene i dati dell'oggetto incorporato, che scrivi in un file appena creato utilizzando un`FileStream`. Il file è denominato in sequenza (`OleObject1.mol`, `OleObject2.mol` , ecc.) in base al`index` variabile.
## Fase 5: Conferma del completamento del processo
Infine, una volta estratti tutti i file MOL, è buona norma informare l'utente che il processo è stato completato con successo.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Questa riga stampa semplicemente un messaggio sulla console per farti sapere che l'estrazione è riuscita. È un bel tocco per il feedback degli utenti.
## Conclusione
Ed ecco fatto! Hai estratto con successo file MOL incorporati da una cartella di lavoro Excel usando Aspose.Cells per .NET. Questo processo integra alcuni passaggi fondamentali, assicurando un approccio strutturato alla gestione di oggetti incorporati. Che tu sia nella ricerca scientifica, nell'analisi chimica o semplicemente nella gestione di set di dati complessi, essere in grado di estrarre e manipolare questi tipi di file può fare una differenza significativa nel modo in cui gestisci le tue informazioni. 
## Domande frequenti
### Posso estrarre altri tipi di file oltre a MOL da Excel?
Sì, è possibile estrarre vari altri tipi di file incorporati con tecniche simili.
### Aspose.Cells è gratuito?
 Aspose.Cells è una libreria commerciale, ma puoi[provalo gratuitamente per un periodo limitato](https://releases.aspose.com/).
### Questo metodo funziona con tutte le versioni di Excel?
Sì, a patto che il formato del file sia supportato da Aspose.Cells.
### Posso automatizzare questo processo di estrazione?
Assolutamente! Puoi automatizzare questo processo inserendo il codice in un'attività pianificata o in uno script.
### Dove posso trovare ulteriore documentazione su Aspose.Cells?
 Puoi controllare il[Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) per maggiori dettagli ed esempi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
