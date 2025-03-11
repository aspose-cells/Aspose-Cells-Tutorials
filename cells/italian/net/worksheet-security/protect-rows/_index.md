---
title: Proteggi le righe nel foglio di lavoro usando Aspose.Cells
linktitle: Proteggi le righe nel foglio di lavoro usando Aspose.Cells
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come proteggere le righe in un foglio di lavoro Excel usando Aspose.Cells per .NET. Proteggi i tuoi dati con la protezione a livello di riga e impedisci modifiche accidentali.
weight: 18
url: /it/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Proteggi le righe nel foglio di lavoro usando Aspose.Cells

## Introduzione
Lavorare con file Excel a livello di programmazione è spesso un'attività che richiede non solo la manipolazione dei dati, ma anche la protezione dei dati. Che tu abbia bisogno di proteggere dati sensibili o di impedire modifiche accidentali, proteggere le righe in un foglio di lavoro può essere un passaggio cruciale. In questo tutorial, approfondiremo come proteggere righe specifiche in un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Esamineremo tutti i passaggi necessari, dalla preparazione dell'ambiente all'implementazione delle funzionalità di protezione in modo semplice e facile da seguire.
## Prerequisiti
Prima di poter iniziare a proteggere le righe in un foglio di lavoro, ecco alcune cose che devi fare:
1.  Aspose.Cells per .NET: assicurati di avere Aspose.Cells per .NET installato sulla tua macchina di sviluppo. Se non lo hai già fatto, puoi scaricarlo facilmente da[Pagina di download di Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio o qualsiasi IDE .NET: per implementare la soluzione, è necessario avere un ambiente di sviluppo configurato. Visual Studio è un'ottima opzione, ma qualsiasi IDE compatibile con .NET funzionerà.
3. Conoscenza di base del linguaggio C#: comprendere le basi della programmazione in C# ti aiuterà a seguire il tutorial e a modificare il codice di esempio in base alle tue esigenze.
4.  Documentazione API Aspose.Cells: familiarizza con[Documentazione di Aspose.Cells per .NET](https://reference.aspose.com/cells/net/) per ottenere una panoramica della struttura della classe e dei metodi utilizzati nella libreria.
Se hai soddisfatto tutti i prerequisiti, possiamo passare direttamente all'implementazione.
## Importa pacchetti
Per iniziare, devi importare i pacchetti richiesti. Queste librerie sono essenziali per interagire con i file Excel nel tuo progetto C#.
```csharp
using System.IO;
using Aspose.Cells;
```
Dopo aver importato i pacchetti necessari, puoi iniziare a scrivere il codice. 
Ora, scomponiamo il processo in passaggi più piccoli per renderlo super facile da seguire. Ogni passaggio si concentrerà su una parte specifica dell'implementazione, assicurandoti di poterla comprendere e applicare rapidamente. 
## Passaggio 1: creare una nuova cartella di lavoro e un nuovo foglio di lavoro
Prima di poter applicare qualsiasi impostazione di protezione, devi creare una nuova cartella di lavoro e selezionare il foglio di lavoro con cui vuoi lavorare. Questo sarà il tuo documento di lavoro.
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
In questo esempio, stiamo creando una nuova cartella di lavoro con un singolo foglio di lavoro (che è l'impostazione predefinita quando si crea una nuova cartella di lavoro usando Aspose.Cells). Quindi prendiamo il primo foglio di lavoro nella cartella di lavoro, che sarà il target per la nostra protezione di riga.
## Passaggio 2: definire gli oggetti Style e StyleFlag
Il passo successivo è definire gli oggetti stile e flag stile. Questi oggetti consentono di modificare le proprietà della cella, ad esempio se è bloccata o sbloccata.
```csharp
// Definire l'oggetto stile.
Style style;
// Definire l'oggetto styleflag.
StyleFlag flag;
```
Utilizzerai questi oggetti nei passaggi successivi per personalizzare le proprietà delle celle e applicarle al tuo foglio di lavoro.
## Passaggio 3: sbloccare tutte le colonne nel foglio di lavoro
Per impostazione predefinita, tutte le celle in un foglio di lavoro Excel sono bloccate. Tuttavia, quando proteggi un foglio di lavoro, viene applicato lo stato di blocco. Per assicurarti che solo righe o celle specifiche siano protette, puoi prima sbloccare tutte le colonne. Questo passaggio è essenziale se vuoi proteggere solo determinate righe.
```csharp
// Esegui un ciclo tra tutte le colonne del foglio di lavoro e sbloccale.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 In questo codice, eseguiamo un ciclo su tutte le 256 colonne del foglio di lavoro (i fogli di lavoro Excel hanno un massimo di 256 colonne, indicizzate da 0 a 255) e impostiamo le loro`IsLocked` proprietà a`false`Questa azione garantisce che tutte le colonne siano sbloccate, ma in seguito bloccheremo comunque righe specifiche.
## Passaggio 4: bloccare la prima riga
Una volta sbloccate le colonne, il passo successivo è bloccare le righe specifiche che vuoi proteggere. In questo esempio, bloccheremo la prima riga. Questo assicura che gli utenti non possano modificarla mentre le altre righe rimangono sbloccate.
```csharp
//Ottieni lo stile della prima riga.
style = sheet.Cells.Rows[0].Style;
// Chiudilo a chiave.
style.IsLocked = true;
//Istanziare il flag.
flag = new StyleFlag();
// Imposta l'impostazione di blocco.
flag.Locked = true;
// Applica lo stile alla prima riga.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Qui accediamo allo stile della prima riga e impostiamo il suo`IsLocked` proprietà a`true` Dopo di che, utilizziamo il`ApplyRowStyle()` metodo per applicare lo stile di blocco all'intera riga. Puoi ripetere questo passaggio per bloccare qualsiasi altra riga che vuoi proteggere.
## Passaggio 5: proteggere il foglio
Ora che abbiamo sbloccato e bloccato le righe necessarie, è il momento di proteggere il foglio di lavoro. La protezione assicura che nessuno possa modificare le righe o le celle bloccate a meno che non rimuova la password di protezione (se fornita).
```csharp
// Proteggere il foglio.
sheet.Protect(ProtectionType.All);
```
 In questo passaggio applichiamo la protezione all'intero foglio utilizzando`ProtectionType.All`. Questo tipo di protezione significa che tutti gli aspetti del foglio, incluse le righe e le celle bloccate, sono protetti. Puoi anche personalizzare questa protezione specificando diversi tipi di protezione, se necessario.
## Passaggio 6: salvare la cartella di lavoro
Infine, dobbiamo salvare la cartella di lavoro dopo aver applicato gli stili e la protezione necessari. La cartella di lavoro può essere salvata in vari formati, come Excel 97-2003, Excel 2010, ecc.
```csharp
// Salvare il file Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Questa riga di codice salva la cartella di lavoro nel formato Excel 97-2003 con le modifiche applicate. Puoi cambiare il formato del file in base alle tue esigenze selezionando da una varietà di`SaveFormat` opzioni.
## Conclusione
Ed ecco fatto! Hai imparato con successo come proteggere le righe in un foglio di lavoro usando Aspose.Cells per .NET. Seguendo i passaggi sopra, puoi sbloccare o bloccare qualsiasi riga o colonna a seconda delle necessità e applicare la protezione per garantire l'integrità dei tuoi dati.
## Domande frequenti
### Come posso proteggere più righe contemporaneamente?  
 Puoi scorrere più righe e applicare lo stile di blocco a ciascuna singolarmente. Sostituisci semplicemente`0` con l'indice di riga che vuoi bloccare.
### Posso impostare una password per la protezione del foglio?  
 Sì! Puoi passare una password al`sheet.Protect()` metodo per applicare la protezione tramite password.
### Posso sbloccare celle invece di intere colonne?  
Sì! Invece di sbloccare le colonne, puoi sbloccare le singole celle modificandone le proprietà di stile.
### Cosa succede se provo a modificare una riga protetta?  
Quando una riga è protetta, Excel impedirà che vengano apportate modifiche alle celle bloccate, a meno che non si sblocchi la protezione del foglio.
### Posso proteggere intervalli specifici di seguito?  
 Sì! Puoi bloccare intervalli individuali in una riga impostando`IsLocked` proprietà per celle specifiche all'interno dell'intervallo.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
