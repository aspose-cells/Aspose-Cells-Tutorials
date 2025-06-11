---
"description": "Scopri come proteggere celle e intervalli in un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Segui questa guida passo passo per proteggere i tuoi fogli di calcolo."
"linktitle": "Proteggi celle e intervalli nel foglio di lavoro utilizzando Aspose.Cells"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Proteggi celle e intervalli nel foglio di lavoro utilizzando Aspose.Cells"
"url": "/it/net/worksheet-security/protect-cells-and-ranges/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Proteggi celle e intervalli nel foglio di lavoro utilizzando Aspose.Cells

## Introduzione
Lavorare con i fogli di calcolo spesso implica la protezione di alcune parti del foglio da modifiche indesiderate, soprattutto in ambienti collaborativi. In questo tutorial, esploreremo come proteggere celle e intervalli specifici in un foglio di lavoro utilizzando Aspose.Cells per .NET. Vi guideremo attraverso il processo di configurazione di un foglio protetto, specificando quali intervalli sono modificabili e salvando il file. Questa può essere una funzionalità estremamente utile quando si desidera limitare l'accesso a dati sensibili, consentendo al contempo la modifica di determinate sezioni da parte di altri.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:
1. Aspose.Cells per .NET: è necessario che la libreria Aspose.Cells sia installata nel progetto. Se non l'hai già fatto, puoi scaricarla da [Sito web di Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: questa guida presuppone che tu stia utilizzando Visual Studio o un IDE simile che supporti lo sviluppo in C#.
3. Conoscenza di base di C#: è necessario avere familiarità con le basi della programmazione C# e con le modalità di configurazione di un progetto in Visual Studio.
4. Licenza Aspose.Cells: sebbene Aspose offra una prova gratuita, una licenza valida ti consentirà di utilizzare tutte le funzionalità della libreria. Se non ne possiedi una, puoi ottenerne una [licenza temporanea qui](https://purchase.aspose.com/temporary-license/).
Una volta che avrai preparato tutto quanto sopra, potremo passare alla parte relativa alla codifica.
## Importa pacchetti
Per lavorare con Aspose.Cells, devi prima importare gli spazi dei nomi necessari nel tuo file C#. Ecco come importarli:
```csharp
using System.IO;
using Aspose.Cells;
```
IL `Aspose.Cells` namespace ti dà accesso alle funzionalità principali per la manipolazione dei file Excel e `System.IO` viene utilizzato per operazioni sui file come il salvataggio della cartella di lavoro.
Vediamo ora nel dettaglio i passaggi per proteggere celle e intervalli all'interno di un foglio di lavoro utilizzando Aspose.Cells.
## Passaggio 1: configura l'ambiente
Per prima cosa, crea una directory in cui salvare i file Excel. Se la directory non esiste già, ne creeremo una. Questo ti aiuterà a trovare un posto dove salvare il file di output.
```csharp
// Definisci il percorso verso la directory dei tuoi documenti
string dataDir = "Your Document Directory";
// Controlla se la directory esiste, in caso contrario, creala
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
Qui stiamo usando `System.IO.Directory.Exists()` per verificare se la cartella esiste e, in caso contrario, la creiamo utilizzando `Directory.CreateDirectory()`.
## Passaggio 2: creare una nuova cartella di lavoro
Ora, creiamo un nuovo oggetto Workbook. Questo servirà come file Excel in cui definiremo celle e intervalli.
```csharp
// Crea un'istanza di un nuovo oggetto Workbook
Workbook book = new Workbook();
```
IL `Workbook` La classe è il punto di ingresso per lavorare con i file Excel in Aspose.Cells. Rappresenta il documento Excel.
## Passaggio 3: accedere al foglio di lavoro predefinito
Ogni cartella di lavoro appena creata ha un foglio di lavoro predefinito. Lo recupereremo per lavorarci sopra.
```csharp
// Ottieni il primo foglio di lavoro (predefinito) nella cartella di lavoro
Worksheet sheet = book.Worksheets[0];
```
Qui, `Worksheets[0]` ci fornisce il primo foglio della cartella di lavoro (l'indicizzazione inizia da 0).
## Passaggio 4: definire intervalli modificabili
Per proteggere determinate parti del foglio di lavoro e consentire agli utenti di modificare celle specifiche, dobbiamo definire intervalli modificabili. Creeremo un intervallo modificabile e lo aggiungeremo alla raccolta AllowEditRanges del foglio di lavoro.
```csharp
// Ottieni la raccolta AllowEditRanges
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Definisci un ProtectedRange e aggiungilo alla raccolta
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
Nel codice sopra:
- `"r2"` è il nome dell'intervallo modificabile.
- I numeri `1, 1, 3, 3` rappresentano gli indici di riga e colonna iniziale e finale per l'intervallo (ad esempio, dalla cella B2 alla D4).
## Passaggio 5: impostare una password per l'intervallo protetto
Ora che abbiamo definito l'intervallo modificabile, aggiungiamo una password per proteggerlo. Ciò significa che gli utenti avranno bisogno della password per modificare questo specifico intervallo.
```csharp
// Specificare la password per l'intervallo modificabile
protectedRange.Password = "123";
```
Qui abbiamo impostato la password come `"123"`ma puoi scegliere qualsiasi password sicura. Questo passaggio è essenziale per controllare l'accesso alle aree modificabili.
## Passaggio 6: proteggere l'intero foglio
In questa fase, proteggeremo l'intero foglio di lavoro. Proteggere il foglio di lavoro garantisce che altre parti del foglio, ad eccezione degli intervalli consentiti, non siano modificabili.
```csharp
// Proteggere il foglio con il tipo di protezione specificato (Tutti)
sheet.Protect(ProtectionType.All);
```
In questo modo si garantisce che tutte le celle del foglio siano bloccate, ad eccezione di quelle negli intervalli modificabili.
## Passaggio 7: salvare la cartella di lavoro
Infine, salviamo la cartella di lavoro in un file. Il foglio protetto verrà salvato con il nome specificato.
```csharp
// Salva il file Excel nella directory specificata
book.Save(dataDir + "protectedrange.out.xls");
```
Qui, il file Excel verrà salvato come `protectedrange.out.xls` nella directory definita in precedenza. Se si desidera salvarlo con un nome o un formato diverso, è possibile modificare il nome e l'estensione del file.
## Conclusione
Seguendo questo tutorial, hai imparato a proteggere celle e intervalli in un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Questo approccio ti offre flessibilità nel controllare quali aree del tuo foglio di calcolo possono essere modificate e quali no. Ora puoi applicare queste competenze ai tuoi progetti, garantendo la sicurezza dei tuoi dati sensibili e offrendo al contempo aree modificabili per gli utenti.
Ricorda che Aspose.Cells offre un solido set di strumenti per lavorare con i file Excel e questa è solo una delle tante cose che puoi fare. 
## Domande frequenti
### Posso proteggere solo determinate celle in un foglio di lavoro?
Sì, utilizzando il `AllowEditRanges` proprietà, è possibile specificare quali celle o intervalli possono essere modificati mentre il resto del foglio di lavoro rimane protetto.
### Posso rimuovere la protezione in un secondo momento?
Sì, puoi rimuovere la protezione da un foglio di lavoro utilizzando `Unprotect()` metodo e, se è stata impostata una password, sarà necessario fornirla.
### Come posso proteggere un intero foglio con una password?
Per proteggere l'intero foglio, è sufficiente utilizzare il `Protect()` metodo con o senza password. Ad esempio, `sheet.Protect("password")`.
### Posso aggiungere più intervalli modificabili?
Assolutamente! Puoi aggiungere tutti gli intervalli modificabili di cui hai bisogno chiamando `allowRanges.Add()` più volte.
### Quali altre funzionalità di sicurezza offre Aspose.Cells?
Aspose.Cells supporta diverse funzionalità di sicurezza, come la crittografia delle cartelle di lavoro, l'impostazione di password per i file e la protezione di celle e fogli.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}