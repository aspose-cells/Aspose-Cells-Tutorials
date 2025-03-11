---
title: Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells
linktitle: Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Impara a creare intervalli modificabili nei fogli di lavoro Excel utilizzando Aspose.Cells per .NET, consentendo la modifica di celle specifiche e proteggendo le altre con la protezione del foglio di lavoro.
weight: 10
url: /it/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Consenti agli utenti di modificare gli intervalli nel foglio di lavoro utilizzando Aspose.Cells

## Introduzione
I documenti Excel contengono spesso dati sensibili o contenuti strutturati che vuoi proteggere da modifiche indesiderate. Tuttavia, potrebbero esserci celle o intervalli specifici che vuoi rendere modificabili per determinati utenti. Ecco dove entra in gioco Aspose.Cells per .NET come potente strumento che ti consente di proteggere un intero foglio di lavoro pur continuando a concedere autorizzazioni di modifica agli intervalli designati. Immagina di condividere un foglio di calcolo del budget in cui solo alcune celle sono modificabili e altre rimangono protette: Aspose.Cells rende tutto questo facile ed efficiente.
## Prerequisiti
Prima di immergerci nella parte di codifica, assicuriamoci di avere tutto ciò di cui hai bisogno:
-  Aspose.Cells per .NET: assicurati di aver installato la libreria Aspose.Cells per .NET. Puoi scaricarla[Qui](https://releases.aspose.com/cells/net/).
- Ambiente di sviluppo: Visual Studio o qualsiasi IDE compatibile con C#.
- .NET Framework: versione 4.0 o successiva.
- Licenza: prendi in considerazione l'idea di ottenere una licenza per evitare limitazioni di prova. Puoi ottenere una[licenza temporanea qui](https://purchase.aspose.com/temporary-license/).
## Importa pacchetti
Assicurati di includere lo spazio dei nomi Aspose.Cells necessario all'inizio del codice:
```csharp
using System.IO;
using Aspose.Cells;
```
In questo modo sarà possibile accedere a tutte le classi e ai metodi necessari per impostare intervalli protetti nei file Excel.
Ora che le basi sono state gettate, esaminiamo il codice in dettaglio, un passo alla volta.
## Passaggio 1: impostare la directory
Prima di lavorare con i file, devi impostare la directory in cui salverai il file Excel. Questo assicura che i tuoi file siano ben organizzati e archiviati in modo sicuro.
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
Questa parte del codice assicura che la tua directory sia pronta per le operazioni sui file. Considerala come la base per tutto ciò che segue.
## Passaggio 2: inizializzare la cartella di lavoro e il foglio di lavoro
Ora procediamo creando una nuova cartella di lavoro e accedendo al suo foglio di lavoro predefinito.
```csharp
// Inizializza una nuova cartella di lavoro
Workbook book = new Workbook();
// Accedi al primo foglio di lavoro nella cartella di lavoro
Worksheet sheet = book.Worksheets[0];
```
Qui, stiamo inizializzando una cartella di lavoro Excel e selezionando il primo foglio di lavoro al suo interno. Questo foglio di lavoro sarà la tela in cui applicheremo le nostre impostazioni di protezione e definiremo intervalli modificabili.
## Passaggio 3: accedere alla raccolta Consenti intervalli di modifica
 Aspose.Cells ha una funzionalità chiamata`AllowEditRanges`, che è una raccolta di intervalli modificabili anche quando il foglio di lavoro è protetto.
```csharp
// Accedi alla raccolta Consenti intervalli di modifica
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Questa riga imposta l'accesso a una speciale raccolta di intervalli che saranno modificabili. Consideratela come un'area "VIP" nel vostro foglio di lavoro, dove solo intervalli specifici possono bypassare la protezione.
## Passaggio 4: definire e creare un intervallo protetto
Ora, definiamo e creiamo un intervallo protetto nel nostro foglio di lavoro. Specifichiamo le celle di inizio e fine per questo intervallo.
```csharp
// Definire una variabile ProtectedRange
ProtectedRange protectedRange;
// Aggiungere un nuovo intervallo alla raccolta con un nome specifico e posizioni delle celle
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
In questo blocco di codice:
- `EditableRange` è il nome assegnato all'intervallo.
- numeri (1, 1, 3, 3) definiscono le coordinate dell'intervallo, ovvero inizia dalla cella B2 (riga 1, colonna 1) alla cella D4 (riga 3, colonna 3).
## Passaggio 5: impostare una password per l'intervallo protetto
Per una maggiore sicurezza, puoi impostare una password per l'intervallo protetto. Questo passaggio aggiunge un ulteriore livello di protezione per garantire che solo gli utenti autorizzati possano modificare l'intervallo.
```csharp
// Imposta una password per l'intervallo modificabile
protectedRange.Password = "123";
```
Qui abbiamo aggiunto una password (`"123"`) all'intervallo protetto. Questo requisito di password fornisce un ulteriore livello di controllo su chi può apportare modifiche.
## Passaggio 6: proteggere il foglio di lavoro
Con il nostro intervallo modificabile stabilito, il passo successivo è proteggere l'intero foglio di lavoro. Questa impostazione di protezione assicurerà che tutte le celle al di fuori dell'intervallo definito siano bloccate e non modificabili.
```csharp
// Applica la protezione al foglio di lavoro, rendendo tutte le altre celle non modificabili
sheet.Protect(ProtectionType.All);
```
 IL`Protect`blocca l'intero foglio di lavoro, eccetto gli intervalli che abbiamo definito come modificabili. Questo passaggio crea essenzialmente un ambiente sicuro di "sola lettura", con accesso a celle specifiche in base alle necessità.
## Passaggio 7: salvare la cartella di lavoro
Il passaggio finale consiste nel salvare la cartella di lavoro, in modo che le impostazioni vengano applicate e memorizzate.
```csharp
// Salva il file Excel nella directory specificata
book.Save(dataDir + "protectedrange.out.xls");
```
In questo passaggio, salviamo la nostra cartella di lavoro come "protectedrange.out.xls" nella directory che abbiamo impostato nel passaggio 1. Ora hai un file Excel completamente funzionante e sicuro in cui solo intervalli specifici sono modificabili!
## Conclusione
Aspose.Cells per .NET fornisce un modo eccellente per gestire la protezione e le autorizzazioni nei file Excel. Creando intervalli modificabili, puoi proteggere i tuoi fogli di lavoro pur consentendo ad aree specifiche di rimanere accessibili. Questa funzionalità è particolarmente utile per i documenti collaborativi, in cui solo poche celle dovrebbero essere aperte per la modifica mentre altre rimangono bloccate.
## Domande frequenti
### Posso aggiungere più intervalli modificabili a un foglio di lavoro?
Sì, puoi aggiungere più intervalli semplicemente ripetendo la`allowRanges.Add()` metodo per ogni nuovo intervallo.
### Cosa succede se in seguito volessi rimuovere un intervallo protetto?
 Utilizzare il`allowRanges.RemoveAt()` metodo con l'indice dell'intervallo che si desidera rimuovere.
### Posso impostare password diverse per ogni intervallo?
 Assolutamente. Ciascuno`ProtectedRange` può avere una password univoca, garantendoti un controllo granulare.
### Cosa succede se proteggo il foglio di lavoro senza intervalli modificabili?
Se non si definiscono intervalli modificabili, l'intero foglio di lavoro non sarà modificabile una volta protetto.
### L'intervallo protetto è visibile agli altri utenti?
No, la protezione è interna. Agli utenti verrà chiesto di inserire una password solo se provano a modificare l'area protetta.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
