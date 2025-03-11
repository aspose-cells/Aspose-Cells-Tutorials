---
title: Foglio di lavoro Excel Copia
linktitle: Foglio di lavoro Excel Copia
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come copiare un foglio di lavoro Excel usando Aspose.Cells per .NET con questa guida passo-passo facile da seguire. Ideale per gli sviluppatori .NET che desiderano automatizzare le attività di Excel.
weight: 20
url: /it/net/excel-copy-worksheet/excel-copy-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Foglio di lavoro Excel Copia

## Introduzione

Nel mondo della gestione dei dati, i fogli di calcolo sono ovunque, dalla gestione delle cifre di vendita all'organizzazione dei dati di progetto. Ma come si gestiscono questi file quando diventa necessaria l'automazione? Bene, se si lavora in .NET, Aspose.Cells è uno strumento eccellente per manipolare i file Excel a livello di programmazione. In questo articolo, vi guideremo nella copia di un foglio di lavoro all'interno di un file Excel utilizzando Aspose.Cells per .NET. Questa è un'attività comune quando si devono duplicare i dati in nuovi fogli senza partire da zero.

Quindi, allacciate le cinture! Stiamo per immergerci in questo processo, ma in un modo semplice, colloquiale e chiaro.

## Prerequisiti

Prima di iniziare a divertirci, assicuriamoci che tu abbia tutto ciò che ti serve per iniziare con questo tutorial.

### Installa Aspose.Cells per .NET
Prima di tutto, se non hai ancora installato Aspose.Cells per .NET, dovrai scaricarlo e installarlo. Puoi prendere l'ultima versione dalla loro pagina di rilascio.

- [Scarica Aspose.Cells per .NET](https://releases.aspose.com/cells/net/)

Puoi usare NuGet in Visual Studio o scaricarlo manualmente. Se preferisci la via NuGet, esegui semplicemente questo comando:

```bash
Install-Package Aspose.Cells
```

### Ottieni una licenza
Per sfruttare appieno le funzionalità di Aspose.Cells, è consigliabile procurarsi una licenza.

- [Acquista una licenza](https://purchase.aspose.com/buy) O[Richiedi una licenza temporanea](https://purchase.aspose.com/temporary-license/)

Utilizzando la libreria senza licenza verranno applicate filigrane ai file di output, quindi assicurati di avere la licenza a portata di mano!

### Imposta il tuo ambiente di sviluppo
Assicurati di aver installato quanto segue:
- Visual Studio (o qualsiasi IDE compatibile con .NET)
- .NET Framework o .NET Core

Dopo aver installato e configurato tutto, iniziamo a programmare!

## Importa pacchetti

Per lavorare con Aspose.Cells, devi prima importare i namespace richiesti nel tuo progetto. Ecco il frammento di codice per assicurarti di avere i riferimenti corretti:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ora che abbiamo fatto le cose di routine, passiamo al lavoro vero e proprio: copiare un foglio di lavoro in una cartella di lavoro di Excel.

## Passaggio 1: definire i percorsi delle directory
La prima cosa di cui hai bisogno è specificare la directory in cui si trovano i tuoi file Excel. Questo è fondamentale per caricare il file nel tuo progetto e salvare la cartella di lavoro modificata.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string InputPath = dataDir + "book1.xls";
```

-  IL`dataDir` variabile contiene il percorso della directory in cui risiedono i file Excel. Modifica`"YOUR DOCUMENT DIRECTORY"` al percorso effettivo della cartella.
- `InputPath` memorizza la posizione del file Excel su cui lavoreremo (in questo caso, "book1.xls").

È una buona idea utilizzare percorsi dinamici in modo da poter passare facilmente da un ambiente all'altro (sviluppo, staging, produzione).

## Passaggio 2: aprire la cartella di lavoro di Excel
Carichiamo ora il file Excel utilizzando la classe Workbook, che rappresenta un intero file Excel.

```csharp
Workbook wb = new Workbook(InputPath);
```

-  IL`Workbook` l'oggetto carica il file Excel che si trova in`InputPath`Aspose.Cells si occupa dell'analisi del file, così non dovrai preoccuparti della complessità del formato Excel.

## Passaggio 3: accedi alla raccolta di fogli di lavoro
Ogni cartella di lavoro ha più fogli di lavoro (pensali come schede nel tuo file Excel). Per copiare un foglio di lavoro, devi prima accedere a questi fogli.

```csharp
WorksheetCollection sheets = wb.Worksheets;
```

- `WorksheetCollection` è essenzialmente un elenco di tutti i fogli di lavoro nella cartella di lavoro. Questo è ciò con cui lavoreremo per copiare il nostro foglio.

## Passaggio 4: Copia un foglio di lavoro esistente
Ora la parte emozionante: la duplicazione del foglio di lavoro! Qui, copieremo il contenuto di "Sheet1" in un nuovo foglio.

```csharp
sheets.AddCopy("Sheet1");
```

-  IL`AddCopy` Il metodo duplica un foglio di lavoro esistente (in questo caso, "Sheet1") e aggiunge il nuovo foglio alla cartella di lavoro.
-  Puoi sostituire`"Sheet1"` con qualsiasi nome di foglio che desideri copiare.

## Passaggio 5: salvare la cartella di lavoro
Infine, dopo aver copiato il foglio di lavoro, è il momento di salvare il file Excel aggiornato. Utilizzeremo il metodo Save per salvare le modifiche in un nuovo file.

```csharp
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```

-  IL`Save` il metodo scrive la cartella di lavoro aggiornata in un nuovo file (`CopyWithinWorkbook_out.xls` ). Puoi scegliere qualsiasi nome per il file di output, ma ricorda di salvarlo nel formato appropriato (ad esempio,`.xls`, `.xlsx`).

Ecco fatto! Hai duplicato con successo un foglio di lavoro in un file Excel.

## Conclusione

Copiare un foglio di lavoro in Aspose.Cells per .NET non è solo semplice, ma anche altamente efficiente. Con solo poche righe di codice, puoi automatizzare attività Excel ripetitive, rendendoti la vita molto più semplice quando hai a che fare con grandi set di dati o report basati su modelli. Che tu stia automatizzando report finanziari, registri di inventario o qualsiasi altra cosa che richieda Excel, Aspose.Cells è la soluzione che fa per te.

## Domande frequenti

### Posso copiare più fogli di lavoro contemporaneamente utilizzando Aspose.Cells per .NET?
 No, dovrai copiarli uno per uno utilizzando il`AddCopy` metodo. Tuttavia, puoi facilmente scorrere più fogli e copiarli in sequenza.

### Aspose.Cells per .NET supporta la copia di fogli di lavoro tra cartelle di lavoro diverse?
 Sì, puoi copiare i fogli di lavoro tra diverse cartelle di lavoro aprendo entrambe le cartelle di lavoro e utilizzando`AddCopy` metodo tra di loro.

### Quali formati Excel supporta Aspose.Cells?
Aspose.Cells supporta un'ampia gamma di formati Excel, tra cui`.xls`, `.xlsx`, `.csv`, `.html`e altro ancora.

### Ho bisogno di una licenza per utilizzare Aspose.Cells per .NET?
 Sì, per evitare le filigrane e sbloccare il pieno potenziale della libreria, hai bisogno di una licenza valida. Tuttavia, puoi richiedere una[licenza temporanea gratuita](https://purchase.aspose.com/temporary-license) per provarlo prima di acquistarlo.

### Posso eseguire Aspose.Cells su .NET Core?
Sì, Aspose.Cells è completamente compatibile sia con .NET Framework che con .NET Core, il che lo rende versatile per le applicazioni multipiattaforma.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
