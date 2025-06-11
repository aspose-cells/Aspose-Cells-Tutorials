---
"description": "Automatizza la formattazione dei numeri in Excel utilizzando Aspose.Cells per .NET. Scopri come applicare i formati di data, percentuale e valuta a livello di codice."
"linktitle": "Utilizzo di formati numerici predefiniti in Excel a livello di programmazione"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Utilizzo di formati numerici predefiniti in Excel a livello di programmazione"
"url": "/it/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Utilizzo di formati numerici predefiniti in Excel a livello di programmazione

## Introduzione
In questo tutorial, ti guideremo nell'utilizzo dei formati numerici predefiniti in Excel tramite Aspose.Cells per .NET. Tratteremo ogni aspetto, dalla configurazione dell'ambiente all'applicazione di diversi formati come date, percentuali e valute. Che tu sia un professionista esperto o che tu stia appena muovendo i primi passi nell'ecosistema .NET, questa guida ti aiuterà a formattare le celle di Excel in modo semplice e veloce.
## Prerequisiti
Prima di immergerti, assicurati di avere quanto segue:
- Libreria Aspose.Cells per .NET installata. Puoi [scaricalo qui](https://releases.aspose.com/cells/net/).
- Conoscenza pratica del linguaggio C# e della programmazione .NET di base.
- Visual Studio o qualsiasi IDE .NET installato sul computer.
- Una licenza Aspose valida o [licenza temporanea](https://purchase.aspose.com/temporary-license/).
- Framework .NET installato (versione 4.0 o superiore).
  
Se ti manca qualcosa di quanto sopra, segui i link forniti per configurare tutto. Pronto? Passiamo alla parte divertente!
## Importa pacchetti
Prima di iniziare il tutorial, assicurati di importare gli spazi dei nomi necessari per lavorare con Aspose.Cells per .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Una volta importati, sei pronto per manipolare i file Excel a livello di codice. Ora, immergiamoci nella guida passo passo!
## Passaggio 1: crea o accedi alla tua cartella di lavoro Excel
In questo passaggio, creerai una nuova cartella di lavoro. Immagina di aprire un nuovo file Excel, solo che lo stai facendo tramite codice!
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();
```
Qui stiamo semplicemente creando un nuovo `Workbook` Oggetto. Questo funge da file Excel, pronto per la manipolazione dei dati. Puoi anche caricare un file esistente specificandone il percorso.
## Passaggio 2: accedi al foglio di lavoro
Le cartelle di lavoro di Excel possono contenere più fogli di lavoro. In questo passaggio, accederemo al primo foglio di lavoro della cartella di lavoro:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Stiamo ora accedendo al primo foglio di lavoro della cartella di lavoro. Se è necessario manipolare altri fogli, è possibile farvi riferimento utilizzando il loro indice o nome.
## Passaggio 3: aggiungere dati alle celle
Iniziamo ad aggiungere alcuni dati a celle specifiche. Per prima cosa, inseriamo la data di sistema corrente nella cella "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Questa riga inserisce la data corrente nella cella A1. Fantastico, vero? Immagina di doverlo fare manualmente per centinaia di celle: sarebbe un incubo. Ora passiamo alla formattazione!
## Passaggio 4: formattare la data nella cella "A1"
Ora, formattiamo la data in un formato più leggibile, come "15-ott-24". È qui che Aspose.Cells dà il meglio di sé:
1. Recupera lo stile della cella:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Qui, stiamo prendendo lo stile della cella A1. Consideratelo come se prendessimo lo "stile" della cella prima di apportare modifiche.
2. Imposta il formato della data:
```csharp
style.Number = 15;
```
Impostazione del `Number` La proprietà a 15 applica il formato data desiderato. Si tratta di un codice di formato numerico integrato per visualizzare le date nel formato "g-mmm-aa".
3. Applica lo stile alla cella:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Questa riga applica le modifiche di stile alla cella. Ora, invece del formato data predefinito, vedrai qualcosa di molto più intuitivo, come "15-ott-24".
## Passaggio 5: aggiungere e formattare una percentuale nella cella "A2"
Passiamo alla formattazione delle percentuali. Immagina di voler inserire un valore e visualizzarlo come percentuale. In questo passaggio, aggiungeremo un valore numerico alla cella "A2" e lo formatteremo come percentuale:
1. Inserisci valore numerico:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Questo inserisce il numero 20 nella cella A2. Potresti pensare: "È solo un numero, come faccio a trasformarlo in percentuale?". Bene, ci arriveremo.
2. Recupera lo stile e imposta il formato percentuale:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formato in percentuale
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Qui aggiungiamo 2546 alla cella A3. Poi formattiamo questo numero per visualizzarlo come valuta.
2. Recupera lo stile e imposta il formato della valuta:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formato come valuta
worksheet.Cells["A3"].SetStyle(style);
```
Impostazione del `Number` La proprietà a 6 applica il formato valuta. Ora il valore nella cella A3 verrà visualizzato come "2.546,00", completo di virgole e due cifre decimali.
## Passaggio 7: salvare il file Excel
Ora che abbiamo applicato tutta la magia della formattazione, è il momento di salvare il file:
```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Questa riga salva il file Excel nel formato Excel 97-2003. È possibile modificare il `SaveFormat` in base alle tue esigenze. E in un attimo, hai creato e formattato un file Excel in modo programmatico!
## Conclusione
Congratulazioni! Hai imparato a utilizzare Aspose.Cells per .NET per applicare formati numerici predefiniti alle celle di un file Excel. Dalle date alle percentuali e alle valute, abbiamo trattato alcune delle esigenze di formattazione più comuni per l'elaborazione dei dati in Excel. Ora, invece di formattare manualmente le celle, puoi automatizzare l'intero processo, risparmiando tempo e riducendo gli errori.
## Domande frequenti
### Posso applicare formati numerici personalizzati utilizzando Aspose.Cells per .NET?
Sì! Oltre ai formati predefiniti, Aspose.Cells supporta anche formati numerici personalizzati. È possibile creare formati altamente specifici utilizzando `Custom` proprietà nella `Style` classe.
### Come posso formattare una cella come valuta con un simbolo specifico?
Per applicare un simbolo di valuta specifico, è possibile utilizzare la formattazione personalizzata impostando `Style.Custom` proprietà.
### Posso formattare intere righe o colonne?
Assolutamente! Puoi applicare stili a intere righe o colonne utilizzando `Rows` O `Columns` collezioni in `Worksheet` oggetto.
### Come posso formattare più celle contemporaneamente?
Puoi usare il `Range` oggetto per selezionare più celle e applicare stili a tutte contemporaneamente.
### Per utilizzare Aspose.Cells è necessario avere installato Microsoft Excel?
No, Aspose.Cells funziona indipendentemente da Microsoft Excel, quindi non è necessario che Excel sia installato sul computer.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}