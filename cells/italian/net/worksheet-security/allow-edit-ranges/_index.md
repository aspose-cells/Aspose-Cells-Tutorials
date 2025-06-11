---
"description": "Impara a creare intervalli modificabili nei fogli di lavoro di Excel utilizzando Aspose.Cells per .NET, consentendo la modifica di celle specifiche e proteggendo le altre con la protezione del foglio di lavoro."
"linktitle": "Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells"
"url": "/it/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells

## Introduzione
documenti Excel contengono spesso dati sensibili o contenuti strutturati che si desidera proteggere da modifiche indesiderate. Tuttavia, potrebbero esserci celle o intervalli specifici che si desidera rendere modificabili per determinati utenti. È qui che entra in gioco Aspose.Cells per .NET, un potente strumento che consente di proteggere un intero foglio di lavoro, pur concedendo autorizzazioni di modifica agli intervalli designati. Immagina di condividere un foglio di calcolo del budget in cui solo alcune celle sono modificabili e altre rimangono protette: Aspose.Cells rende tutto questo semplice ed efficiente.
## Prerequisiti
Prima di immergerci nella parte di codifica, assicuriamoci di avere tutto ciò di cui hai bisogno:
- Aspose.Cells per .NET: assicurati di aver installato la libreria Aspose.Cells per .NET. Puoi scaricarla. [Qui](https://releases.aspose.com/cells/net/).
- Ambiente di sviluppo: Visual Studio o qualsiasi IDE compatibile con C#.
- .NET Framework: versione 4.0 o successiva.
- Licenza: valuta la possibilità di ottenere una licenza per evitare limitazioni di prova. Puoi ottenere una [licenza temporanea qui](https://purchase.aspose.com/temporary-license/).
## Importa pacchetti
Assicurati di includere lo spazio dei nomi Aspose.Cells necessario all'inizio del codice:
```csharp
using System.IO;
using Aspose.Cells;
```
Ciò garantirà l'accesso a tutte le classi e a tutti i metodi necessari per impostare intervalli protetti nei file Excel.
Ora che le basi sono state gettate, esaminiamo il codice in dettaglio, un passo alla volta.
## Passaggio 1: impostare la directory
Prima di lavorare con i file, è necessario impostare la directory in cui salvare il file Excel. Questo garantisce che i file siano ben organizzati e archiviati in modo sicuro.
```csharp
// Definisci il percorso verso la directory dei tuoi documenti
string dataDir = "Your Document Directory";
// Controlla se la directory esiste, in caso contrario, creala
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Questa parte del codice assicura che la directory sia pronta per le operazioni sui file. Consideratela come la base per tutto ciò che segue.
## Passaggio 2: inizializzare la cartella di lavoro e il foglio di lavoro
Ora procediamo creando una nuova cartella di lavoro e accedendo al suo foglio di lavoro predefinito.
```csharp
// Inizializza una nuova cartella di lavoro
Workbook book = new Workbook();
// Accedi al primo foglio di lavoro nella cartella di lavoro
Worksheet sheet = book.Worksheets[0];
```
Qui, stiamo inizializzando una cartella di lavoro di Excel e selezionando il primo foglio di lavoro al suo interno. Questo foglio di lavoro sarà l'area di lavoro in cui applicheremo le impostazioni di protezione e definiremo gli intervalli modificabili.
## Passaggio 3: accedere alla raccolta Consenti modifica intervalli
Aspose.Cells ha una funzionalità chiamata `AllowEditRanges`, che è una raccolta di intervalli modificabili anche quando il foglio di lavoro è protetto.
```csharp
// Accedi alla raccolta Consenti modifica intervalli
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Questa riga imposta l'accesso a una raccolta speciale di intervalli modificabili. Consideratela come un'area "VIP" nel vostro foglio di lavoro, in cui solo intervalli specifici possono aggirare la protezione.
## Passaggio 4: definire e creare un intervallo protetto
Ora definiamo e creiamo un intervallo protetto nel nostro foglio di lavoro. Specifichiamo le celle iniziali e finali di questo intervallo.
```csharp
// Definisci una variabile ProtectedRange
ProtectedRange protectedRange;
// Aggiungi un nuovo intervallo alla raccolta con un nome specifico e posizioni delle celle
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
In questo blocco di codice:
- `EditableRange` è il nome assegnato all'intervallo.
- I numeri (1, 1, 3, 3) definiscono le coordinate dell'intervallo, ovvero inizia dalla cella B2 (riga 1, colonna 1) alla cella D4 (riga 3, colonna 3).
## Passaggio 5: impostare una password per l'intervallo protetto
Per maggiore sicurezza, è possibile impostare una password per l'intervallo protetto. Questo passaggio aggiunge un ulteriore livello di protezione per garantire che solo gli utenti autorizzati possano modificare l'intervallo.
```csharp
// Imposta una password per l'intervallo modificabile
protectedRange.Password = "123";
```
Qui abbiamo aggiunto una password (`"123"`) all'intervallo protetto. Questo requisito di password fornisce un ulteriore livello di controllo su chi può apportare modifiche.
## Passaggio 6: proteggere il foglio di lavoro
Una volta stabilito l'intervallo modificabile, il passo successivo è proteggere l'intero foglio di lavoro. Questa impostazione di protezione garantirà che tutte le celle al di fuori dell'intervallo definito siano bloccate e non modificabili.
```csharp
// Applica protezione al foglio di lavoro, rendendo tutte le altre celle non modificabili
sheet.Protect(ProtectionType.All);
```
IL `Protect` Il metodo blocca l'intero foglio di lavoro, ad eccezione degli intervalli che abbiamo definito come modificabili. Questo passaggio crea essenzialmente un ambiente sicuro di "sola lettura", con accesso a celle specifiche in base alle esigenze.
## Passaggio 7: salvare la cartella di lavoro
Il passaggio finale consiste nel salvare la cartella di lavoro, in modo che le impostazioni vengano applicate e memorizzate.
```csharp
// Salva il file Excel nella directory specificata
book.Save(dataDir + "protectedrange.out.xls");
```
In questo passaggio, salviamo la nostra cartella di lavoro come "protectedrange.out.xls" nella directory creata nel passaggio 1. Ora hai un file Excel completamente funzionante e sicuro, in cui sono modificabili solo intervalli specifici!
## Conclusione
Aspose.Cells per .NET offre un modo eccellente per gestire la protezione e le autorizzazioni all'interno dei file Excel. Creando intervalli modificabili, è possibile proteggere i fogli di lavoro mantenendo comunque accessibili aree specifiche. Questa funzionalità è particolarmente utile per i documenti collaborativi, in cui solo poche celle devono essere aperte per la modifica, mentre altre rimangono bloccate.
## Domande frequenti
### Posso aggiungere più intervalli modificabili a un foglio di lavoro?
Sì, puoi aggiungere più intervalli semplicemente ripetendo la `allowRanges.Add()` metodo per ogni nuovo intervallo.
### Cosa succede se in seguito volessi rimuovere un intervallo protetto?
Utilizzare il `allowRanges.RemoveAt()` metodo con l'indice dell'intervallo che si desidera rimuovere.
### Posso impostare password diverse per ogni intervallo?
Assolutamente. Ogni `ProtectedRange` può avere una password univoca, garantendoti un controllo granulare.
### Cosa succede se proteggo il foglio di lavoro senza intervalli modificabili?
Se non si definiscono intervalli modificabili, l'intero foglio di lavoro non sarà modificabile una volta protetto.
### L'intervallo protetto è visibile agli altri utenti?
No, la protezione è interna. Agli utenti verrà richiesto di inserire una password solo se tentano di modificare l'area protetta.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}