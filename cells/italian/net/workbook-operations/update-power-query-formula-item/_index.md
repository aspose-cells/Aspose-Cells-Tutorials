---
"description": "Scopri come aggiornare le formule di Power Query in Excel con Aspose.Cells per .NET in questa guida completa passo dopo passo."
"linktitle": "Aggiorna l'elemento della formula di Power Query nella cartella di lavoro"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiorna l'elemento della formula di Power Query nella cartella di lavoro"
"url": "/it/net/workbook-operations/update-power-query-formula-item/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiorna l'elemento della formula di Power Query nella cartella di lavoro

## Introduzione
Capire come gestire i dati in modo efficiente utilizzando Power Query in Excel è fondamentale per qualsiasi analista di dati o appassionato di Excel. Se hai mai avuto bisogno di aggiornare gli elementi delle formule nella tua cartella di lavoro di Power Query, sei nel posto giusto. Questa guida è pensata per aiutarti a imparare a utilizzare Aspose.Cells per .NET per aggiornare senza problemi le formule di Power Query in una cartella di lavoro di Excel. Con pochi semplici passaggi, sarai in grado di manipolare e ottimizzare i tuoi dati, garantendo che le tue cartelle di lavoro rimangano dinamiche e centralizzate.
## Prerequisiti
Prima di iniziare a leggere il codice di esempio e i passaggi da seguire, vediamo cosa ti servirà:
1. Nozioni di base di C# e .NET: la familiarità con i concetti di programmazione in C# sarà utile perché scriveremo del codice.
2. Installa Aspose.Cells per .NET: devi avere la libreria Aspose.Cells integrata nel tuo progetto .NET. Puoi scaricarla. [Qui](https://releases.aspose.com/cells/net/).
3. Un file Excel pronto per la modifica: assicurati di avere un file Excel contenente una Power Query che desideri aggiornare. Devi avere una cartella di lavoro di esempio come `SamplePowerQueryFormula.xlsx` a vostra disposizione.
## Importa pacchetti
Per iniziare, assicurati di includere i seguenti namespace nel tuo file C#:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Ciò consentirà di accedere alle funzionalità fornite dalla libreria Aspose.Cells, in particolare per lavorare con cartelle di lavoro e dati Power Query.
## Passaggio 1: imposta le directory di lavoro
Per prima cosa, devi definire dove si trovano i file di origine e di output. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
In questo passaggio, si specificano i percorsi delle directory. Sostituisci `"Your Document Directory"` Con il percorso effettivo in cui sono salvati i file Excel. Questo indica al programma dove cercare il file sorgente e dove salvare quello aggiornato.
## Passaggio 2: caricare la cartella di lavoro
Ora che hai impostato le directory di lavoro, il passo successivo è caricare il file Excel nel programma.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Qui crei un `Workbook` oggetto che carica il file Excel specificato. L' `Workbook` La classe fa parte della libreria Aspose.Cells ed è essenziale per tutte le operazioni che eseguirai su quel file Excel.
## Passaggio 3: accedere ai dati di Power Query
Una volta caricata la cartella di lavoro, è il momento di accedere alle formule di Power Query in essa memorizzate.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
In questa linea, il `DataMashup` La proprietà consente di accedere alle strutture dati di Power Query all'interno della cartella di lavoro. Questa proprietà offre la possibilità di interagire con vari aspetti dei dati di Power Query contenuti nel file Excel.
## Passaggio 4: scorrere le formule di Power Query
Una volta accessibili i dati di Power Query, il passaggio successivo consiste nell'eseguire l'iterazione di ciascuna delle formule presenti.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
È qui che avviene la magia. Facciamo un giro attraverso ogni `PowerQueryFormula` e poi attraverso ciascuno `PowerQueryFormulaItem`. IL `if` L'istruzione cerca l'elemento della formula denominato "Origine" e ne aggiorna il valore in modo che corrisponda al percorso del file di origine a cui si desidera che Power Query faccia riferimento. Ciò consente di modificare dinamicamente il file da cui Power Query estrae i dati.
## Passaggio 5: salvare la cartella di lavoro aggiornata
Dopo aver aggiornato gli elementi necessari della formula, il passaggio finale consiste nel salvare la cartella di lavoro.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Questa riga salva la cartella di lavoro modificata in un nuovo file, preservando così l'originale ma consentendo di lavorare con la versione aggiornata.
## Passaggio 6: messaggio di conferma
Infine, è buona norma verificare se il codice è stato eseguito correttamente.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Questo semplice messaggio ti confermerà sulla console che l'operazione è andata a buon fine, concludendo in modo rassicurante il processo.
## Conclusione
Ed ecco fatto! Aggiornare gli elementi della formula di Power Query in Excel utilizzando Aspose.Cells per .NET può essere eseguito in pochi semplici passaggi. Seguendo questa guida, puoi gestire in modo efficiente le connessioni dati di Excel e garantire il corretto funzionamento delle tue cartelle di lavoro. Che tu sia un professionista esperto o un principiante nella manipolazione dei dati, Aspose.Cells offre un potente strumento per automatizzare e migliorare i flussi di lavoro di Excel. 
## Domande frequenti
### Posso usare Aspose.Cells con qualsiasi versione di .NET?
Aspose.Cells è compatibile con più versioni di .NET, tra cui .NET Framework e .NET Core.
### Aspose.Cells è gratuito?
Aspose.Cells offre una prova gratuita, ma per un utilizzo continuativo è necessaria una licenza. È possibile ottenere una licenza temporanea. [Qui](https://purchase.aspose.com/temporary-license/).
### Cosa succede se il mio file Excel esistente non ha Power Query?
Il processo descritto si concentra sull'aggiornamento degli elementi di Power Query, quindi se nel file ne mancano, è necessario prima integrare Power Query.
### Dove posso trovare maggiori informazioni su Aspose.Cells?
Consulta la documentazione per una guida completa ed esempi. Visita il sito [documentazione](https://reference.aspose.com/cells/net/).
### Come posso segnalare bug o problemi con Aspose.Cells?
Puoi contattare il loro forum di supporto per ricevere assistenza in merito a qualsiasi problema tu riscontri.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}