---
"description": "Consenti agli utenti di modificare intervalli specifici in un foglio di calcolo Excel utilizzando Aspose.Cells per .NET. Guida passo passo con codice sorgente in C#."
"linktitle": "Consenti all'utente di modificare gli intervalli nel foglio di lavoro Excel"
"second_title": "Riferimento API Aspose.Cells per .NET"
"title": "Consenti all'utente di modificare gli intervalli nel foglio di lavoro Excel"
"url": "/it/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Consenti all'utente di modificare gli intervalli nel foglio di lavoro Excel

## Introduzione

Quando si lavora con i fogli di lavoro Excel, la flessibilità è spesso fondamentale, soprattutto quando più utenti devono accedere per modificare aree specifiche senza compromettere l'integrità dei dati dell'intero foglio. È qui che Aspose.Cells per .NET eccelle! In questo tutorial, approfondiremo come consentire agli utenti di modificare determinati intervalli all'interno di un foglio di lavoro Excel, proteggendo al contempo il resto del documento. Alla fine di questo articolo, non solo avrai assimilato i concetti, ma avrai anche un esempio concreto su cui lavorare. 

## Prerequisiti

Prima di entrare nei dettagli, assicuriamoci di avere tutto il necessario per iniziare:

1. Ambiente di sviluppo .NET: dovresti avere un ambiente di sviluppo .NET funzionante (potrebbe essere Visual Studio o qualsiasi altro IDE di tua scelta).
2. Libreria Aspose.Cells per .NET: scarica e installa la libreria Aspose.Cells. Puoi trovarla [Qui](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a navigare facilmente tra gli esempi di codice.
4. Nozioni di base di Excel: conoscere il funzionamento di Excel fornirà le basi per le funzionalità che esamineremo.

Una volta soddisfatti questi prerequisiti, sei pronto a partire!

## Importa pacchetti

Prima di iniziare a scrivere codice, dobbiamo assicurarci che il nostro progetto riconosca lo spazio dei nomi Aspose.Cells. Ecco come importare i pacchetti necessari:

```csharp
using System.IO;
using Aspose.Cells;
```

Ora che abbiamo importato ciò che ci serve, iniziamo con il nostro tutorial passo dopo passo.

## Passaggio 1: impostare la directory dei documenti

Per qualsiasi operazione sui file, è fondamentale avere una posizione definita in cui salvare i documenti. Impostiamo la nostra directory di lavoro per archiviare i file Excel.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Per prima cosa, sostituisci `"YOUR DOCUMENT DIRECTORY"` Con il percorso in cui desideri salvare i tuoi file. Questo codice controlla se la directory esiste; in caso contrario, ne crea una.

## Passaggio 2: creare una nuova cartella di lavoro

Ora che la nostra directory di lavoro è pronta, è il momento di creare la nostra cartella di lavoro Excel. 

```csharp
// Crea una nuova cartella di lavoro
Workbook book = new Workbook();
```

Qui stiamo creando una nuova istanza di `Workbook` classe fornita da Aspose.Cells, che ci consente di manipolare il file Excel.

## Passaggio 3: accedere al foglio di lavoro predefinito

Ogni nuova cartella di lavoro contiene almeno un foglio di lavoro. Vediamo come accedervi.

```csharp
// Ottieni il primo foglio di lavoro (predefinito)
Worksheet sheet = book.Worksheets[0];
```

In questo frammento di codice accediamo al primo foglio di lavoro della nostra cartella di lavoro, che manipoleremo nei passaggi successivi.

## Passaggio 4: Ottieni gli intervalli di modifica consentiti

Per abilitare intervalli specifici del foglio di lavoro per la modifica, dobbiamo accedere a `AllowEditRanges` proprietà.

```csharp
// Ottieni gli intervalli di modifica consentiti
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Questa raccolta ci consentirà di gestire quali intervalli sono modificabili nel nostro foglio di lavoro.

## Passaggio 5: definire l'intervallo protetto

Ora definiamo quale parte del foglio di lavoro vogliamo proteggere, consentendo al contempo le modifiche entro un intervallo specificato.

```csharp
// Definisci ProtectedRange
ProtectedRange proteced_range;

// Crea l'intervallo
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Specificare la password
proteced_range.Password = "123";
```

In questa fase, aggiungeremo un nuovo intervallo modificabile denominato "r2" che consente modifiche nelle celle dalla riga 1 colonna 1 alla riga 3 colonna 3. Inoltre, imposteremo una password per proteggere questo intervallo, garantendo che solo gli utenti autorizzati possano modificarlo.

## Passaggio 6: proteggere il foglio di lavoro

Ora che abbiamo impostato l'intervallo modificabile, dobbiamo proteggere il foglio di lavoro.

```csharp
// Proteggi il foglio
sheet.Protect(ProtectionType.All);
```

Questo codice proteggerà l'intero foglio di lavoro da qualsiasi modifica indesiderata, ad eccezione dell'intervallo appena specificato.

## Passaggio 7: salvare il file Excel

Salviamo la cartella di lavoro così potremo vedere le modifiche apportate in un file Excel.

```csharp
// Salvare il file Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Assicurati di modificare il nome del file secondo necessità. Questo creerà un file Excel nella directory specificata con le impostazioni che abbiamo configurato.

## Conclusione

Ecco fatto! Hai creato con successo un foglio di lavoro Excel che limita le modifiche a un intervallo designato, proteggendo al contempo il resto del foglio. L'utilizzo di Aspose.Cells per .NET semplifica notevolmente la gestione di questo tipo di attività. Che tu stia sviluppando un'applicazione complessa o semplicemente abbia bisogno di gestire i dati in modo sicuro, queste funzionalità possono migliorare significativamente il tuo flusso di lavoro.

## Domande frequenti

### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria .NET per la gestione di file Excel, che offre funzionalità come la creazione, la modifica e la conversione di fogli di calcolo a livello di programmazione.

### Posso applicare più intervalli modificabili?
Assolutamente! Puoi chiamare il `Add` metodo sul `allowRanges` raccolta più volte per specificare più intervalli modificabili.

### Cosa succede se dimentico la password?
Purtroppo, se si dimentica la password per un intervallo modificabile, sarà necessario rimuovere la protezione o accedere al file in una modalità predefinita che potrebbe richiedere credenziali.

### Esiste una versione gratuita di Aspose.Cells?
Sì, Aspose offre una prova gratuita che puoi utilizzare per esplorare le funzionalità prima di acquistarlo.

### Dove posso trovare maggiori informazioni su Aspose.Cells?
Puoi controllare il [documentazione](https://reference.aspose.com/cells/net/) per guide e riferimenti dettagliati.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}