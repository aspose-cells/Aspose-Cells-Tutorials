---
title: Personalizzazione dei formati di visualizzazione con numeri definiti dall'utente
linktitle: Personalizzazione dei formati di visualizzazione con numeri definiti dall'utente
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come personalizzare i formati di visualizzazione con Aspose.Cells per .NET. Formatta date, percentuali e valute utilizzando questa guida passo passo.
weight: 11
url: /it/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Personalizzazione dei formati di visualizzazione con numeri definiti dall'utente

## Introduzione
Lavorare con file Excel spesso richiede una formattazione personalizzata delle celle per presentare i dati in modo più significativo e intuitivo. Immagina di creare un file Excel per un report. Non vuoi solo numeri grezzi. Vuoi che date, percentuali e valute abbiano un aspetto elegante e professionale, giusto? È qui che entrano in gioco i formati di visualizzazione personalizzati. In questo tutorial, ci immergiamo in Aspose.Cells per .NET per mostrarti come personalizzare il formato di visualizzazione dei numeri utilizzando impostazioni definite dall'utente.
## Prerequisiti
Prima di iniziare, assicurati di avere tutto pronto per seguire questo tutorial. Ecco cosa ti servirà:
-  Aspose.Cells per .NET installato.[Scaricalo qui](https://releases.aspose.com/cells/net/).
- Conoscenza di base di C# e del framework .NET.
-  Una licenza valida per Aspose.Cells. Se non ne hai una, prendine una[prova gratuita](https://releases.aspose.com/) o richiedi un[licenza temporanea](https://purchase.aspose.com/temporary-license/).
- Un IDE come Visual Studio.
- .NET Framework 4.0 o versione successiva.
 Se ti manca qualcosa, non preoccuparti. Puoi sempre rivisitare questi link per scaricare i file necessari o chiedere aiuto al[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).
## Importazione degli spazi dei nomi
Prima di passare al codice, è necessario importare gli spazi dei nomi richiesti per accedere a tutte le funzionalità Aspose.Cells necessarie.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Questi due namespace saranno i tuoi strumenti principali in questo tutorial. Ora passiamo alla parte divertente:
## Passaggio 1: impostazione della directory del progetto
Per prima cosa, hai bisogno di un posto dove archiviare i tuoi file, giusto? Creiamo una directory per salvare il file Excel di output. In questo passaggio, ci assicureremo anche che la directory esista prima di salvare qualsiasi cosa.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Stiamo definendo un`dataDir` variabile per memorizzare il percorso in cui verrà salvato il file Excel di output.
-  Quindi controlliamo se la directory esiste utilizzando`System.IO.Directory.Exists()`.
-  Se la directory non esiste, verrà creata utilizzando`System.IO.Directory.CreateDirectory()`.
## Passaggio 2: creare una nuova cartella di lavoro e aggiungere un foglio di lavoro
Ora che abbiamo la nostra directory, creiamo una nuova cartella di lavoro di Excel e aggiungiamoci un foglio di lavoro.
```csharp
// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();
// Aggiungere un nuovo foglio di lavoro all'oggetto Excel
int i = workbook.Worksheets.Add();
// Ottenere il riferimento del foglio di lavoro appena aggiunto passando l'indice del suo foglio
Worksheet worksheet = workbook.Worksheets[i];
```
-  Per prima cosa creiamo un nuovo`Workbook` oggetto. Consideralo come il tuo file Excel.
-  Aggiungiamo un nuovo foglio di lavoro a questa cartella di lavoro utilizzando il`Add()`metodo e memorizza l'indice nella variabile`i`.
-  Facciamo riferimento a questo foglio di lavoro utilizzando il`workbook.Worksheets[i]`.
## Passaggio 3: aggiunta di una data a una cella e personalizzazione del suo formato
 Ora, inseriamo la data corrente in una cella e formattiamola per visualizzarla in un modo personalizzato. Invece del formato data predefinito, imposteremo un formato personalizzato come`d-mmm-yy`.
```csharp
// Aggiungere la data di sistema corrente alla cella "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Ottenere lo stile della cella A1
Style style = worksheet.Cells["A1"].GetStyle();
// Impostazione del formato di visualizzazione personalizzato per mostrare la data come "g-mmm-aa"
style.Custom = "d-mmm-yy";
// Applicazione dello stile alla cella A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Aggiungiamo la data corrente del sistema alla cella`A1` usando`PutValue(DateTime.Now)`.
-  Recuperiamo lo stile corrente della cella`A1` usando`GetStyle()`.
-  Modifichiamo lo stile della cella impostando`style.Custom = "d-mmm-yy"`, che formatta la data per mostrare il giorno, il mese abbreviato e l'anno.
-  Infine, applichiamo il nuovo stile alla cella con`SetStyle()`.
## Passaggio 4: formattazione di una cella come percentuale
 Ora lavoriamo con i numeri. Aggiungeremo un valore numerico a un'altra cella, diciamo`A2`e formattarlo come percentuale.
```csharp
//Aggiungere un valore numerico alla cella "A2"
worksheet.Cells["A2"].PutValue(20);
// Ottenere lo stile della cella A2
style = worksheet.Cells["A2"].GetStyle();
// Impostazione del formato di visualizzazione personalizzato per mostrare il valore come percentuale
style.Custom = "0.0%";
// Applicazione dello stile alla cella A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Aggiungiamo il valore`20` alla cella`A2`.
-  Recuperiamo lo stile della cella`A2` e imposta il formato personalizzato su`0.0%` per visualizzare il valore in percentuale (ad esempio, 20%).
-  Infine, applichiamo lo stile alla cella utilizzando`SetStyle()`.
## Passaggio 5: formattazione di una cella come valuta
 Aggiungiamo un altro valore, diciamo alla cella`A3`, e formattarlo per visualizzarlo come valuta. Per rendere le cose più interessanti, useremo un formato che visualizza i valori positivi come valuta in sterline e i valori negativi in dollari.
```csharp
// Aggiungere un valore numerico alla cella "A3"
worksheet.Cells["A3"].PutValue(2546);
// Ottenere lo stile della cella A3
style = worksheet.Cells["A3"].GetStyle();
// Impostazione del formato di visualizzazione personalizzato per mostrare il valore come valuta
style.Custom = "£#,##0;[Red]$-#,##0";
// Applicazione dello stile alla cella A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Aggiungiamo il valore`2546` alla cella`A3`.
-  Impostiamo un formato personalizzato`£#,##0;[Red]$-#,##0`, che visualizza i valori positivi con il simbolo della sterlina e i valori negativi in rosso con il simbolo del dollaro.
- Applichiamo lo stile alla cella usando`SetStyle()`.
## Passaggio 6: salvataggio della cartella di lavoro
Il passaggio finale è salvare la cartella di lavoro come file Excel. Per questo tutorial useremo il formato Excel 97-2003.
```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  IL`Save()` metodo salva la cartella di lavoro nella directory specificata.
-  Noi scegliamo`SaveFormat.Excel97To2003` per garantire la compatibilità con le versioni precedenti di Excel.
## Conclusione
Ecco fatto! Abbiamo appena creato un file Excel, aggiunto formati personalizzati di data, percentuale e valuta a celle specifiche utilizzando Aspose.Cells per .NET e salvato il file. La formattazione personalizzata rende i file Excel molto più leggibili e professionali. Non dimenticare di esplorare altre opzioni di formattazione in Aspose.Cells, come la formattazione condizionale, per un controllo ancora maggiore sull'aspetto dei dati.
## Domande frequenti
### Come posso applicare opzioni di formattazione più complesse in Aspose.Cells?
È possibile combinare diversi stili di formattazione, come colore del carattere, bordi e colori di sfondo, con formati numerici personalizzati.
### Posso applicare un formato numerico personalizzato a un intervallo di celle?
Sì, Aspose.Cells consente di applicare uno stile a un intervallo di celle utilizzando`Range.SetStyle()` metodo.
### In quali altri formati di file posso salvare la cartella di lavoro?
 Aspose.Cells supporta molti formati, tra cui XLSX, CSV e PDF. Basta cambiare il`SaveFormat` nel`Save()` metodo.
### Posso formattare i numeri negativi in modo diverso?
Assolutamente! Puoi usare formati numerici personalizzati per visualizzare numeri negativi con colori o simboli diversi.
### Aspose.Cells per .NET è gratuito?
 Aspose.Cells offre una prova gratuita, ma per la piena funzionalità, avrai bisogno di una licenza valida. Puoi ottenere una[licenza temporanea qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
