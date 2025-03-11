---
title: Aggiungere la firma digitale a un file Excel già firmato
linktitle: Aggiungere la firma digitale a un file Excel già firmato
second_title: Riferimento API Aspose.Cells per .NET
description: Scopri come aggiungere una firma digitale a un file Excel già firmato utilizzando Aspose.Cells per .NET con questa guida dettagliata passo dopo passo.
weight: 30
url: /it/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere la firma digitale a un file Excel già firmato

## Introduzione

Nel mondo digitale odierno, proteggere i documenti è più importante che mai. Le firme digitali forniscono un modo per garantire l'autenticità e l'integrità dei tuoi file, specialmente quando si tratta di informazioni sensibili. Se stai lavorando con file Excel e vuoi aggiungere una nuova firma digitale a una cartella di lavoro che è già stata firmata, sei nel posto giusto! In questa guida, ti guideremo attraverso il processo di aggiunta di una firma digitale a un file Excel già firmato utilizzando Aspose.Cells per .NET. Quindi, tuffiamoci dentro!

## Prerequisiti

Prima di addentrarci nei dettagli della codifica, ecco alcune cose che devi sapere:

1.  Aspose.Cells per .NET: assicurati di avere la libreria Aspose.Cells installata nel tuo progetto .NET. Puoi scaricarla da[sito](https://releases.aspose.com/cells/net/).
2.  File del certificato: avrai bisogno di un file del certificato valido (solitamente un`.pfx`file) che contiene il tuo certificato digitale. Assicurati di conoscere la password per questo file.
3. Ambiente di sviluppo: configura il tuo ambiente di sviluppo con Visual Studio o qualsiasi altro IDE che supporti .NET.
4. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a seguire il corso senza problemi.
5. File di esempio: avere un file Excel di esempio che è già firmato digitalmente. Questo sarà il file a cui aggiungerai una nuova firma.

Ora che abbiamo tutto a posto, iniziamo a programmare!

## Importa pacchetti

Per iniziare, dovrai importare i pacchetti necessari nel tuo file C#. Ecco come fare:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Questi namespace ti consentiranno di lavorare con i file Excel e di gestire le firme digitali senza problemi.

## Passaggio 1: imposta le directory di origine e di output

Prima di poter manipolare i file Excel, devi definire dove si trovano i file sorgente e dove vuoi salvare il file di output. Ecco come fare:

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
// Directory di uscita
string outputDir = "Your Document Directory";
```

In questo passaggio, stiamo usando un metodo per ottenere i percorsi per le directory di origine e di output. Assicurati che queste directory esistano e contengano i file richiesti.

## Passaggio 2: caricare la cartella di lavoro già firmata

 Successivamente, dovrai caricare la cartella di lavoro di Excel che vuoi modificare. Questo viene fatto creando un'istanza di`Workbook` classe e passando il percorso del file firmato.

```csharp
// Caricare la cartella di lavoro già firmata digitalmente
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Qui stiamo caricando la cartella di lavoro denominata`sampleDigitallySignedByCells.xlsx`Assicurati che questo file sia già firmato.

## Passaggio 3: creare una raccolta di firme digitali

Ora, creiamo una raccolta di firme digitali. Questa raccolta conterrà tutte le firme digitali che vuoi aggiungere alla cartella di lavoro.

```csharp
// Creare la raccolta di firme digitali
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Questo passaggio è fondamentale perché consente di gestire più firme se necessario.

## Passaggio 4: creare un nuovo certificato

 Devi caricare il tuo file di certificato per creare una nuova firma digitale. Qui è dove specifichi il percorso al tuo`.pfx` file e la sua password.

```csharp
// File del certificato e relativa password
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Crea nuovo certificato
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Assicurati di sostituire`AsposeDemo.pfx` la password con il nome effettivo del file del certificato e la password.

## Passaggio 5: creare la firma digitale

Con il certificato in mano, ora puoi creare una firma digitale. Dovrai anche fornire un motivo per la firma e la data e l'ora correnti.

```csharp
// Crea una nuova firma digitale e aggiungila alla raccolta di firme digitali
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Questo passaggio aggiunge la nuova firma alla raccolta, che in seguito verrà applicata alla cartella di lavoro.

## Passaggio 6: aggiungere la raccolta di firme digitali alla cartella di lavoro

Ora è il momento di aggiungere la raccolta di firme digitali alla cartella di lavoro. È qui che avviene la magia!

```csharp
// Aggiungere la raccolta di firme digitali all'interno della cartella di lavoro
workbook.AddDigitalSignature(dsCollection);
```

Eseguendo questa riga, di fatto si allega la nuova firma digitale alla cartella di lavoro già firmata.

## Passaggio 7: salvare ed eliminare la cartella di lavoro

Infine, dovrai salvare la cartella di lavoro modificata nella directory di output e rilasciare tutte le risorse utilizzate.

```csharp
//Salvare la cartella di lavoro ed eliminarla.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Questo passaggio garantisce che le modifiche vengano salvate e che la cartella di lavoro venga eliminata correttamente per liberare risorse.

## Passaggio 8: conferma dell'esecuzione

Per concludere, è una buona idea confermare che il tuo codice è stato eseguito correttamente. Puoi farlo con un semplice messaggio della console.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Ciò fornisce un feedback che l'operazione è andata a buon fine, il che è sempre bello da vedere!

## Conclusione

Ed ecco fatto! Hai aggiunto con successo una nuova firma digitale a un file Excel già firmato utilizzando Aspose.Cells per .NET. Le firme digitali sono un modo potente per garantire l'autenticità dei tuoi documenti e ora sai come gestirle a livello di programmazione. Che tu stia lavorando su documenti finanziari, contratti o qualsiasi informazione sensibile, l'implementazione di firme digitali può migliorare la sicurezza e l'affidabilità.

## Domande frequenti

### Cos'è una firma digitale?
La firma digitale è un metodo crittografico utilizzato per convalidare l'autenticità e l'integrità di un messaggio o di un documento.

### Posso aggiungere più firme digitali allo stesso file Excel?
Sì, puoi creare una raccolta di firme digitali e aggiungere più firme alla stessa cartella di lavoro.

### Quali formati supporta Aspose.Cells per le firme digitali?
 Aspose.Cells supporta vari formati, tra cui`.pfx` per i certificati.

### Ho bisogno di una versione specifica di .NET per utilizzare Aspose.Cells?
 Controllare il[Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) per la compatibilità con la tua versione .NET.

### Come posso ottenere una licenza temporanea per Aspose.Cells?
 Puoi richiedere una licenza temporanea da[Pagina di acquisto di Aspose](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
