---
"description": "Scopri come proteggere le righe in un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Proteggi i tuoi dati con la protezione a livello di riga e previeni modifiche accidentali."
"linktitle": "Proteggi le righe nel foglio di lavoro utilizzando Aspose.Cells"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Proteggi le righe nel foglio di lavoro utilizzando Aspose.Cells"
"url": "/it/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Proteggi le righe nel foglio di lavoro utilizzando Aspose.Cells

## Introduzione
Lavorare con file Excel a livello di programmazione è spesso un'attività che richiede non solo la manipolazione dei dati, ma anche la loro protezione. Che si tratti di proteggere dati sensibili o di impedirne la modifica accidentale, proteggere le righe di un foglio di lavoro può essere un passaggio cruciale. In questo tutorial, approfondiremo come proteggere righe specifiche di un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Illustreremo tutti i passaggi necessari, dalla preparazione dell'ambiente all'implementazione delle funzionalità di protezione, in modo semplice e intuitivo.
## Prerequisiti
Prima di poter iniziare a proteggere le righe in un foglio di lavoro, ecco alcune cose che devi fare:
1. Aspose.Cells per .NET: assicurati di aver installato Aspose.Cells per .NET sul tuo computer di sviluppo. Se non l'hai già fatto, puoi scaricarlo facilmente da [Pagina di download di Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio o qualsiasi IDE .NET: per implementare la soluzione, è necessario disporre di un ambiente di sviluppo configurato. Visual Studio è un'ottima opzione, ma qualsiasi IDE compatibile con .NET funzionerà.
3. Conoscenza di base di C#: comprendere le basi della programmazione C# ti aiuterà a seguire il tutorial e a modificare il codice di esempio in base alle tue esigenze.
4. Documentazione API Aspose.Cells: familiarizza con [Documentazione di Aspose.Cells per .NET](https://reference.aspose.com/cells/net/) per ottenere una panoramica della struttura della classe e dei metodi utilizzati nella libreria.
Se hai tutti i prerequisiti necessari, possiamo passare direttamente all'implementazione.
## Importa pacchetti
Per iniziare, è necessario importare i pacchetti necessari. Queste librerie sono fondamentali per interagire con i file Excel nel progetto C#.
```csharp
using System.IO;
using Aspose.Cells;
```
Dopo aver importato i pacchetti necessari, puoi iniziare a scrivere il codice. 
Ora, scomponiamo il processo in passaggi più piccoli per renderlo estremamente semplice da seguire. Ogni passaggio si concentrerà su una parte specifica dell'implementazione, assicurandoti di comprenderla e applicarla rapidamente. 
## Passaggio 1: creare una nuova cartella di lavoro e un nuovo foglio di lavoro
Prima di poter applicare qualsiasi impostazione di protezione, è necessario creare una nuova cartella di lavoro e selezionare il foglio di lavoro con cui si desidera lavorare. Questo sarà il documento di lavoro.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Crea una nuova cartella di lavoro.
Workbook wb = new Workbook();
// Crea un oggetto foglio di lavoro e ottieni il primo foglio.
Worksheet sheet = wb.Worksheets[0];
```
In questo esempio, stiamo creando una nuova cartella di lavoro con un singolo foglio di lavoro (impostazione predefinita quando si crea una nuova cartella di lavoro con Aspose.Cells). Quindi selezioniamo il primo foglio di lavoro della cartella di lavoro, che sarà la destinazione della nostra protezione di riga.
## Passaggio 2: definire gli oggetti Stile e StyleFlag
Il passo successivo è definire gli oggetti stile e flag di stile. Questi oggetti consentono di modificare le proprietà della cella, ad esempio se è bloccata o sbloccata.
```csharp
// Definire l'oggetto stile.
Style style;
// Definire l'oggetto styleflag.
StyleFlag flag;
```
Utilizzerai questi oggetti nei passaggi successivi per personalizzare le proprietà delle celle e applicarle al tuo foglio di lavoro.
## Passaggio 3: sbloccare tutte le colonne nel foglio di lavoro
Per impostazione predefinita, tutte le celle di un foglio di lavoro Excel sono bloccate. Tuttavia, quando si protegge un foglio di lavoro, lo stato di blocco viene applicato. Per garantire che solo righe o celle specifiche siano protette, è possibile sbloccare prima tutte le colonne. Questo passaggio è essenziale se si desidera proteggere solo determinate righe.
```csharp
// Esegui un ciclo su tutte le colonne del foglio di lavoro e sbloccale.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
In questo codice, eseguiamo un ciclo su tutte le 256 colonne del foglio di lavoro (i fogli di lavoro di Excel hanno un massimo di 256 colonne, indicizzate da 0 a 255) e impostiamo le loro `IsLocked` proprietà a `false`Questa azione garantisce che tutte le colonne siano sbloccate, ma in seguito bloccheremo comunque righe specifiche.
## Passaggio 4: bloccare la prima riga
Una volta sbloccate le colonne, il passaggio successivo consiste nel bloccare le righe specifiche che si desidera proteggere. In questo esempio, bloccheremo la prima riga. Questo garantisce che gli utenti non possano modificarla mentre le altre righe rimangono sbloccate.
```csharp
// Ottieni lo stile della prima riga.
style = sheet.Cells.Rows[0].Style;
// Chiudilo a chiave.
style.IsLocked = true;
// Istanziare il flag.
flag = new StyleFlag();
// Imposta l'impostazione di blocco.
flag.Locked = true;
// Applica lo stile alla prima riga.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Qui accediamo allo stile della prima riga e impostiamo il suo `IsLocked` proprietà a `true`. Dopodiché, utilizziamo il `ApplyRowStyle()` Metodo per applicare lo stile di blocco all'intera riga. È possibile ripetere questo passaggio per bloccare qualsiasi altra riga che si desidera proteggere.
## Passaggio 5: proteggere il foglio
Ora che abbiamo sbloccato e bloccato le righe necessarie, è il momento di proteggere il foglio di lavoro. La protezione garantisce che nessuno possa modificare le righe o le celle bloccate a meno che non rimuova la password di protezione (se fornita).
```csharp
// Proteggere il foglio.
sheet.Protect(ProtectionType.All);
```
In questo passaggio applichiamo la protezione all'intero foglio utilizzando `ProtectionType.All`Questo tipo di protezione significa che tutti gli aspetti del foglio, comprese righe e celle bloccate, sono protetti. È anche possibile personalizzare questa protezione specificando diversi tipi di protezione, se necessario.
## Passaggio 6: salvare la cartella di lavoro
Infine, dobbiamo salvare la cartella di lavoro dopo aver applicato gli stili e la protezione necessari. La cartella di lavoro può essere salvata in vari formati, come Excel 97-2003, Excel 2010, ecc.
```csharp
// Salvare il file Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Questa riga di codice salva la cartella di lavoro nel formato Excel 97-2003 con le modifiche applicate. È possibile modificare il formato del file in base alle proprie esigenze selezionando tra una varietà di `SaveFormat` opzioni.
## Conclusione
Ed ecco fatto! Hai imparato con successo come proteggere le righe di un foglio di lavoro utilizzando Aspose.Cells per .NET. Seguendo i passaggi precedenti, puoi sbloccare o bloccare qualsiasi riga o colonna a seconda delle tue esigenze e applicare la protezione per garantire l'integrità dei tuoi dati.
## Domande frequenti
### Come posso proteggere più righe contemporaneamente?  
È possibile scorrere più righe e applicare lo stile di blocco a ciascuna singolarmente. Basta sostituire `0` con l'indice di riga che vuoi bloccare.
### Posso impostare una password per la protezione del foglio?  
Sì! Puoi passare una password al `sheet.Protect()` metodo per applicare la protezione tramite password.
### Posso sbloccare celle invece di intere colonne?  
Sì! Invece di sbloccare le colonne, puoi sbloccare le singole celle modificandone le proprietà di stile.
### Cosa succede se provo a modificare una riga protetta?  
Quando una riga è protetta, Excel impedirà che vengano apportate modifiche alle celle bloccate, a meno che non si sblocchi la protezione del foglio.
### Posso proteggere intervalli specifici di seguito?  
Sì! Puoi bloccare intervalli individuali in una riga impostando `IsLocked` proprietà per celle specifiche all'interno dell'intervallo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}