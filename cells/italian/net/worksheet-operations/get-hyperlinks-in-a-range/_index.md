---
title: Ottieni collegamenti ipertestuali in un intervallo in .NET
linktitle: Ottieni collegamenti ipertestuali in un intervallo in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Estrai e gestisci facilmente i collegamenti ipertestuali dai file Excel con Aspose.Cells per .NET. Guida dettagliata ed esempi di codice inclusi.
weight: 10
url: /it/net/worksheet-operations/get-hyperlinks-in-a-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni collegamenti ipertestuali in un intervallo in .NET

## Introduzione
Ti sei mai trovato immerso nei fogli di calcolo, chiedendoti come estrarre in modo efficiente gli hyperlink? Se è così, sei nel posto giusto! In questa guida, ti guideremo attraverso il processo di ottenimento di hyperlink in un intervallo specificato utilizzando Aspose.Cells per .NET. Questa potente libreria elimina il noioso compito di lavorare con i file Excel, rendendo facile per te recuperare e persino eliminare gli hyperlink. Quindi, prendi una tazza di caffè e tuffiamoci nel mondo di Aspose.Cells!
## Prerequisiti
Prima di addentrarci nel nocciolo della codifica, ci sono alcuni prerequisiti che dovrai avere. Non preoccuparti, non è una lunga lista!
### Prepara il tuo ambiente di sviluppo
1. .NET Framework: assicurati di avere un ambiente .NET compatibile impostato sulla tua macchina. Potrebbe essere .NET Core o il .NET Framework completo. Assicurati che la tua versione supporti la libreria Aspose.Cells.
2.  Libreria Aspose.Cells: avrai bisogno della libreria Aspose.Cells. Puoi scaricare l'ultima versione da[Qui](https://releases.aspose.com/cells/net/) Se stai appena iniziando, prendi in considerazione l'utilizzo di[prova gratuita](https://releases.aspose.com/) per testare il terreno.
3. IDE: un buon Integrated Development Environment (IDE) come Visual Studio ti renderà la vita più semplice. Ti consente di scrivere, eseguire il debug ed eseguire il tuo codice senza problemi.
4. Conoscenza di base di C#: avere familiarità con la programmazione in C# è utile, ma se sei disposto a imparare, sei a posto!
Con questi prerequisiti in atto, siamo pronti a partire. Passiamo ad un po' di codifica di base, importando i pacchetti necessari e suddividendo il nostro esempio passo dopo passo.
## Importa pacchetti
Uno dei primi passaggi nella codifica è l'importazione dei pacchetti necessari. Dovrai aggiungere un riferimento alla libreria Aspose.Cells nel tuo progetto. Questo può essere fatto in genere tramite NuGet Package Manager. Ecco come farlo:
1. Aprire Visual Studio.
2. Fare clic sul progetto in Esplora soluzioni.
3. Fare clic con il tasto destro del mouse e selezionare Gestisci pacchetti NuGet.
4. Cerca “Aspose.Cells” e installalo.
```csharp
using System.IO;
using System;
using Aspose.Cells;
```
Una volta installata la libreria, passiamo al codice per estrarre gli hyperlink!
## Passaggio 1: imposta i percorsi delle directory
Iniziamo definendo il percorso dei tuoi documenti. Vuoi impostare la directory di origine in cui si trova il tuo file Excel e la directory di output in cui verrà salvato il file elaborato.
```csharp
// Percorso verso la directory dei documenti.
string sourceDir = "Your Document Directory"; // Sostituiscilo con il percorso del tuo file Excel
// Directory di uscita
string outputDir = "Your Document Directory"; // Assicurati che questo metodo fornisca un percorso di output valido
```
 In questo frammento, sostituisci`"Your Document Directory"` con il percorso effettivo della tua directory contenente il file Excel. È come allestire il palco prima della tua esibizione: è fondamentale sapere dove si trovano i tuoi materiali.
## Passaggio 2: creare un'istanza dell'oggetto Workbook
 Successivamente, creeremo un`Workbook` oggetto per aprire il file Excel con cui stiamo lavorando.
```csharp
// Crea un'istanza di un oggetto Workbook
// Aprire un file Excel
Workbook workbook = new Workbook(sourceDir + "HyperlinksSample.xlsx");
```
 Qui stiamo creando un nuovo`Workbook` istanza. Il`Workbook`class è essenzialmente il tuo gateway per tutte le operazioni relative a un file Excel. Puoi pensare ad esso come all'apertura del libro che contiene tutti i tuoi contenuti.
## Passaggio 3: accedi al foglio di lavoro
Ora che abbiamo la cartella di lavoro pronta, prendiamo il primo foglio di lavoro da essa. In Excel, i fogli di lavoro sono come le pagine del tuo libro e dobbiamo specificare su quale pagina stiamo lavorando.
```csharp
// Ottieni il primo foglio di lavoro (predefinito)
Worksheet worksheet = workbook.Worksheets[0];
```
 Accedendo`Worksheets[0]`, stiamo scegliendo il primo foglio di lavoro. I fogli di lavoro sono indicizzati a partire da zero, quindi assicurati di selezionare quello giusto.
## Passaggio 4: creare un intervallo
Ora è il momento di definire un intervallo in cui vogliamo cercare gli hyperlink. Nel nostro caso, diciamo che vogliamo cercare nelle celle da A2 a B3.
```csharp
// Crea un intervallo A2:B3
Range range = worksheet.Cells.CreateRange("A2", "B3");
```
 Chiamando`CreateRange`, specifichiamo le celle di inizio e fine. È qui che avviene la magia: in seguito controlleremo gli hyperlink che si trovano in questo intervallo specificato.
## Passaggio 5: recuperare i collegamenti ipertestuali dall'intervallo
Questo è il passaggio in cui effettivamente accediamo ai collegamenti ipertestuali nell'intervallo definito.
```csharp
//Ottieni collegamenti ipertestuali nell'intervallo
Hyperlink[] hyperlinks = range.Hyperlinks;
```
 IL`Hyperlinks` proprietà di un`Range` l'oggetto restituisce un array di`Hyperlink`oggetti trovati in quell'intervallo. È come prendere tutte le note importanti dalla tua pagina in una volta sola!
## Passaggio 6: scorrere e visualizzare i collegamenti
Ora, andiamo a scorrere gli hyperlink recuperati. Per ora, ne stamperemo gli indirizzi e le aree nella console.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    Console.WriteLine(link.Area + " : " + link.Address);
}
```
Qui, eseguiamo un ciclo su ogni collegamento ipertestuale e ne visualizziamo l'area e l'indirizzo. È come leggere ad alta voce i dettagli importanti di ogni collegamento ipertestuale che hai trovato. 
## Passaggio 7: Facoltativo - Eliminazione dei collegamenti ipertestuali
Se necessario, puoi facilmente eliminare gli hyperlink dal tuo intervallo! Questo può essere molto utile se vuoi ripulire il tuo foglio di calcolo.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    // Per eliminare il collegamento, utilizzare il metodo Hyperlink.Delete().
    link.Delete();
}
```
 Utilizzando il`Delete()` metodo su ogni collegamento ipertestuale ti consente di rimuovere i collegamenti ipertestuali di cui potresti non aver più bisogno. È come cancellare uno scarabocchio che non ti serve più dalla tua pagina.
## Passaggio 8: salva le modifiche
Infine, salviamo la cartella di lavoro con tutte le modifiche apportate.
```csharp
workbook.Save(outputDir + "HyperlinksSample_out.xlsx");
```
Questa riga di codice salverà la tua cartella di lavoro modificata nella directory di output specificata. È il tuo modo di pubblicare le modifiche apportate, come chiudere il libro dopo le modifiche finali.
## Conclusione
Ed ecco fatto: una guida completa passo dopo passo per estrarre collegamenti ipertestuali da un intervallo specificato in un foglio Excel usando Aspose.Cells per .NET! Hai imparato come impostare il tuo ambiente, scrivere il codice ed eseguire operazioni sui collegamenti ipertestuali in una cartella di lavoro di Excel. Che tu stia gestendo dati per progetti aziendali o personali, questo strumento può farti risparmiare un'enorme quantità di tempo a lungo termine.
## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una libreria .NET per manipolare file Excel senza dover installare Microsoft Excel sul computer.
### Posso usare Aspose.Cells gratuitamente?
Sì, è disponibile una prova gratuita che ti consente di esplorare le funzionalità prima di acquistarle.
### Ci sono delle limitazioni nella versione di prova?
La versione di prova potrebbe presentare alcune limitazioni di funzionalità, come ad esempio filigrane sui file salvati.
### Devo conoscere la programmazione per usare Aspose.Cells?
Per utilizzare efficacemente la libreria si consiglia una conoscenza di base della programmazione in C# o .NET.
### Come posso ottenere supporto se ho problemi con Aspose.Cells?
 Puoi accedere al forum di supporto[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
