---
"description": "Impara a manipolare le tabelle pivot di Excel con Aspose.Cells per .NET, inclusi aggiornamenti dei dati, impostazioni di compatibilità e formattazione delle celle."
"linktitle": "Specificare la compatibilità del file Excel a livello di programmazione in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Specificare la compatibilità del file Excel a livello di programmazione in .NET"
"url": "/it/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specificare la compatibilità del file Excel a livello di programmazione in .NET

## Introduzione

Nell'attuale mondo basato sui dati, la gestione e la manipolazione dei file Excel a livello di codice è diventata essenziale per molti sviluppatori. Se si lavora con Excel in .NET, Aspose.Cells è una potente libreria che semplifica la creazione, la lettura, la modifica e il salvataggio dei file Excel. Una funzionalità importante di questa libreria consente di specificare la compatibilità dei file Excel a livello di codice. In questo tutorial, esploreremo come manipolare i file Excel, concentrandoci in particolare sulla gestione della compatibilità utilizzando Aspose.Cells per .NET. Al termine, si comprenderà come impostare la compatibilità per i file Excel, in particolare per le tabelle pivot, durante l'aggiornamento e la gestione dei dati.

## Prerequisiti

Prima di immergerti nella fase di codifica, assicurati di avere quanto segue:

1. Conoscenza di base di C#: poiché scriveremo codice in C#, avere familiarità con il linguaggio ti aiuterà a comprendere meglio il tutorial.
2. Libreria Aspose.Cells per .NET: puoi scaricarla da [Pagina delle release di Aspose Cells](https://releases.aspose.com/cells/net/)Se non l'hai ancora fatto, ti consigliamo di richiedere una prova gratuita per esplorarne prima le funzionalità.
3. Visual Studio: un IDE in cui puoi scrivere e testare efficacemente il tuo codice C#.
4. File Excel di esempio: assicurati di avere un file Excel di esempio, preferibilmente uno che contenga una tabella pivot per la demo. Per il nostro esempio, useremo `sample-pivot-table.xlsx`.

Una volta stabiliti questi prerequisiti, possiamo iniziare il processo di codifica.

## Importa pacchetti

Prima di iniziare a scrivere la tua applicazione, devi includere nel codice i namespace necessari per utilizzare al meglio la libreria Aspose.Cells. Ecco come fare.

### Importa lo spazio dei nomi Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Questa riga di codice garantisce l'accesso a tutte le classi e a tutti i metodi all'interno della libreria Aspose.Cells.

Ora analizziamo il processo in dettaglio per assicurarci che tutto sia chiaro e comprensibile.

## Passaggio 1: imposta la tua directory

Per prima cosa, imposta la directory in cui si trovano i file Excel. È importante fornire il percorso corretto.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```

Qui, sostituisci `"Your Document Directory"` Con il percorso effettivo dei file Excel. È qui che dovrebbe risiedere il file della tabella pivot di esempio.

## Passaggio 2: caricare il file Excel di origine

Successivamente, dobbiamo caricare il file Excel che contiene la tabella pivot di esempio. 

```csharp
// Carica il file Excel di origine contenente la tabella pivot di esempio
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

In questo passaggio, creiamo un'istanza di `Workbook` classe, che carica il file Excel specificato. 

## Passaggio 3: accedi ai fogli di lavoro

Ora che la cartella di lavoro è caricata, è necessario accedere al foglio di lavoro che contiene i dati della tabella pivot.

```csharp
// Accedi al primo foglio di lavoro contenente i dati della tabella pivot
Worksheet dataSheet = wb.Worksheets[0];
```

Qui accediamo al primo foglio di lavoro in cui si trova la tabella pivot. È anche possibile scorrere o specificare altri fogli di lavoro in base alla struttura di Excel.

## Passaggio 4: manipolare i dati delle celle

Il passo successivo è modificare alcuni valori delle celle nel foglio di lavoro. 

### Passaggio 4.1: Modificare la cella A3

Iniziamo accedendo alla cella A3 e impostandone il valore.

```csharp
// Accedi alla cella A3 e imposta i suoi dati
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Questo frammento di codice aggiorna la cella A3 con il valore “FooBar”.

### Passaggio 4.2: Modificare la cella B3 con una stringa lunga

Ora impostiamo una stringa lunga nella cella B3, che supera i limiti di caratteri standard di Excel.

```csharp
// Accedi alla cella B3, imposta i suoi dati
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Questo codice è importante perché definisce le aspettative riguardo ai limiti dei dati, soprattutto quando si lavora con le impostazioni di compatibilità in Excel.

## Passaggio 5: verificare la lunghezza della cella B3

È inoltre essenziale confermare la lunghezza della stringa inserita.

```csharp
// Stampa la lunghezza della stringa della cella B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Serve solo per verificare quanti caratteri sono presenti sul tuo cellulare.

## Passaggio 6: imposta altri valori delle celle

Ora accederemo ad altre celle e imposteremo alcuni valori.

```csharp
// Accedi alla cella C3 e imposta i suoi dati
cell = cells["C3"];
cell.PutValue("closed");

// Accedi alla cella D3 e imposta i suoi dati
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Ognuno di questi frammenti aggiorna diverse celle aggiuntive all'interno del foglio di lavoro.

## Passaggio 7: accedere alla tabella pivot

Successivamente, accederai al secondo foglio di lavoro, contenente i dati della tabella pivot.

```csharp
// Accedi al secondo foglio di lavoro che contiene la tabella pivot
Worksheet pivotSheet = wb.Worksheets[1];

// Accedi alla tabella pivot
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Questo frammento consente di manipolare la tabella pivot per le impostazioni di compatibilità.

## Passaggio 8: impostare la compatibilità per Excel 2003

È fondamentale stabilire se la tabella pivot è compatibile o meno con Excel 2003. 

```csharp
// La proprietà IsExcel2003Compatible indica se la tabella pivot è compatibile con Excel2003 durante l'aggiornamento della tabella pivot
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

È qui che inizia la vera trasformazione. Impostando `IsExcel2003Compatible` A `true`puoi limitare la lunghezza dei caratteri a 255 durante l'aggiornamento.

## Passaggio 9: verificare la lunghezza dopo l'impostazione di compatibilità

Dopo aver impostato la compatibilità, vediamo come influisce sui dati.

```csharp
// Controllare il valore della cella B5 del foglio pivot.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Probabilmente vedrai un output che conferma l'effetto troncamento se i dati iniziali superano i 255 caratteri.

## Passaggio 10: modifica le impostazioni di compatibilità

Adesso modifichiamo le impostazioni di compatibilità e controlliamo di nuovo.

```csharp
// Ora imposta la proprietà IsExcel2003Compatible su false e aggiorna di nuovo
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Ciò consente ai dati di riflettere la loro lunghezza originale senza le restrizioni precedenti.

## Passaggio 11: verificare nuovamente la lunghezza 

Verifichiamo che i dati ora riflettano accuratamente la loro lunghezza reale.

```csharp
// Ora verrà stampata la lunghezza originale dei dati della cella. I dati non sono stati troncati.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Dovresti vedere che l'output conferma la rimozione del troncamento.

## Passaggio 12: formattare le celle

Per migliorare l'esperienza visiva, potresti voler formattare le celle. 

```csharp
// Imposta l'altezza della riga e la larghezza della colonna della cella B5 e anche il suo testo
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Queste righe di codice facilitano la lettura dei dati regolando le dimensioni delle celle e abilitando l'interruzione di pagina del testo.

## Passaggio 13: Salvare la cartella di lavoro

Infine, salva la cartella di lavoro con le modifiche apportate.

```csharp
// Salva la cartella di lavoro in formato xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

La scelta di un formato di file appropriato è fondamentale quando si salvano file Excel. `Xlsx` Il formato è ampiamente utilizzato e compatibile con molte versioni di Excel.

## Conclusione

Congratulazioni! Hai programmato le impostazioni di compatibilità dei file Excel utilizzando Aspose.Cells per .NET. Questo tutorial ha illustrato ogni passaggio, dalla configurazione dell'ambiente alla modifica delle impostazioni di compatibilità per le tabelle pivot. Se hai mai lavorato con dati che richiedevano limitazioni o compatibilità specifiche, questa è un'abilità che non vorrai trascurare.

## Domande frequenti

### Che cosa è Aspose.Cells?  
Aspose.Cells è una libreria .NET progettata per aiutare gli sviluppatori a creare, manipolare e convertire file Excel senza problemi.

### Perché è importante la compatibilità con Excel?  
La compatibilità con Excel è fondamentale per garantire che i file possano essere aperti e utilizzati nelle versioni previste di Excel, in particolare se contengono funzionalità o formati non supportati nelle versioni precedenti.

### Posso creare tabelle pivot a livello di programmazione con Aspose.Cells?  
Sì, è possibile creare e manipolare tabelle pivot a livello di codice utilizzando Aspose.Cells. La libreria offre diversi metodi per aggiungere origini dati, campi e funzionalità associate alle tabelle pivot.

### Come posso verificare la lunghezza di una stringa in una cella di Excel?  
Puoi usare il `StringValue` proprietà di un `Cell` oggetto per ottenere il contenuto della cella e quindi chiamare il `.Length` proprietà per scoprire la lunghezza della stringa.

### Posso personalizzare la formattazione delle celle oltre all'altezza e alla larghezza delle righe?  
Assolutamente! Aspose.Cells consente una formattazione estesa delle celle. Puoi modificare stili di carattere, colori, bordi, formati numerici e molto altro tramite `Style` classe.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}