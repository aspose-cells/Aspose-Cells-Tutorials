---
"description": "Impara a inserire righe di DataTable in Excel senza spostare la prima riga verso il basso utilizzando Aspose.Cells per .NET. Guida passo passo per un'automazione senza sforzo."
"linktitle": "Sposta la prima riga verso il basso quando inserisci righe di DataTable in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Sposta la prima riga verso il basso quando inserisci righe di DataTable in Excel"
"url": "/it/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sposta la prima riga verso il basso quando inserisci righe di DataTable in Excel

## Introduzione

Stanco di dover spostare manualmente le righe quando inserisci nuovi dati nei tuoi fogli di calcolo Excel? Beh, sei fortunato! In questo articolo, approfondiremo come automatizzare questo processo utilizzando Aspose.Cells per .NET. Al termine di questo tutorial, non solo imparerai a lavorare con le tabelle dati in Excel, ma anche a personalizzare le opzioni di importazione per adattarle al meglio alle tue esigenze. Fidati di me: questo può farti risparmiare un sacco di tempo e fatica! Quindi, prendi una tazza di caffè e iniziamo!

## Prerequisiti

Prima di passare alla codifica, assicuriamoci di aver impostato tutto:

1. Visual Studio: assicurati di aver installato Visual Studio (la versione 2017 o successiva dovrebbe funzionare correttamente).
2. Aspose.Cells per .NET: è necessaria la libreria Aspose.Cells. Se non l'avete ancora fatto, potete scaricarla. [Qui](https://releases.aspose.com/cells/net/).
3. Nozioni di base di C# ed Excel: una conoscenza di base della programmazione C# e del funzionamento di Excel ti aiuterà sicuramente a seguire il corso in modo più efficace.

Sarà inoltre opportuno avere a portata di mano un file Excel di esempio. In questa guida, ne useremo uno chiamato `sampleImportTableOptionsShiftFirstRowDown.xlsx`Puoi creare questo file o trovare un modello adatto alle tue esigenze.

## Importa pacchetti

Prima di immergerci nella codifica, dobbiamo assicurarci di importare i pacchetti necessari. Nel tuo progetto C#, includi i seguenti namespace:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Questi pacchetti sono essenziali per lavorare con la cartella di lavoro, il foglio di lavoro e le tabelle.

## Passaggio 1: imposta il tuo progetto

### Crea un nuovo progetto C#

Inizia creando una nuova applicazione console C# in Visual Studio. Assegna al progetto un nome appropriato, ad esempio "ExcelDataImport".

### Aggiungi il pacchetto NuGet Aspose.Cells

Per aggiungere il pacchetto Aspose.Cells, fai clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, seleziona Gestisci pacchetti NuGet e cerca "Aspose.Cells". Installa il pacchetto per assicurarti di poter accedere a tutte le funzionalità di cui abbiamo bisogno.

## Passaggio 2: definire la tabella dati

Successivamente, implementeremo il `ICellsDataTable` interfaccia per creare una classe che fornisce i dati da importare. Ecco come puoi strutturare l' `CellsDataTable` classe:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Implementare altri membri ...
}
```

Qui definiamo i nomi delle colonne e i dati per ciascuna colonna, il che semplificherà la struttura della nostra tabella importata.

## Passaggio 3: implementare i membri dell'interfaccia ICellsDataTable

All'interno del `CellsDataTable` classe, è necessario implementare i membri della `ICellsDataTable` interfaccia. Ecco l'implementazione richiesta:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Questa parte della classe gestisce il recupero dei dati, definendo quante righe e colonne sono presenti e gestendo lo stato corrente dell'indice.

## Passaggio 4: scrivere la funzione principale

Ora creiamo il `Run` metodo per orchestrare l'intero processo di importazione della tabella:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Passaggio 5: imposta le opzioni di importazione

Per controllare il comportamento dell'importazione, dovresti creare un'istanza di `ImportTableOptions` e impostare le proprietà di conseguenza. Nello specifico, vogliamo impostare `ShiftFirstRowDown` A `false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Non vogliamo spostare la prima riga verso il basso
```

## Passaggio 6: importare la tabella dati

Ora possiamo importare i dati dal nostro `CellsDataTable` nel foglio di lavoro.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Questo comando inserirà direttamente la tabella dati a partire dalla riga e dalla colonna specificate.

## Passaggio 7: salvare la cartella di lavoro

Infine, salveremo la cartella di lavoro modificata in un file:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Conclusione

Ed ecco fatto! Hai imparato come inserire righe di una tabella dati in un foglio Excel senza spostare la prima riga utilizzando Aspose.Cells per .NET. Questo processo non solo semplifica la manipolazione dei dati in Excel, ma migliora anche le prestazioni della tua applicazione automatizzando un'attività solitamente complessa. Con queste conoscenze a disposizione, sarai più preparato a gestire le attività di automazione di Excel, risparmiando tempo e fatica.

## Domande frequenti

### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una libreria di programmazione che consente agli sviluppatori di creare, manipolare e convertire file Excel nelle applicazioni .NET.

### Ho bisogno di una licenza per utilizzare Aspose.Cells?
Sì, è necessaria una licenza valida per usufruire di tutte le funzionalità. Tuttavia, è disponibile una prova gratuita per un test iniziale.

### Posso utilizzare Aspose.Cells nelle applicazioni web?
Assolutamente sì! Aspose.Cells è perfetto per applicazioni desktop, web e cloud sviluppate in .NET.

### Quali tipi di file Excel posso creare con Aspose.Cells?
È possibile creare diversi formati di file Excel, tra cui XLSX, XLS, CSV e altri.

### Dove posso ottenere supporto per Aspose.Cells?
Puoi fare domande o trovare aiuto nel [Forum di Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}