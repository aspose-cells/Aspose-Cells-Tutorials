---
category: general
date: 2026-02-26
description: Applica rapidamente il formato numerico in Excel e impara come formattare
  una colonna come valuta, impostare il formato numerico della colonna e impostare
  il colore del carattere della colonna in poche righe di C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: it
og_description: Applica il formato numerico di Excel in C# con passaggi semplici.
  Impara a formattare la colonna come valuta, impostare il formato numerico della
  colonna e impostare il colore del carattere della colonna per fogli di calcolo professionali.
og_title: Applica formato numerico Excel – Guida completa allo styling delle colonne
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: applicare il formato numerico in Excel – Guida passo‑passo per formattare le
  colonne
url: /it/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Come formattare le colonne di Excel in C#

Ti sei mai chiesto come **apply number format excel** mentre stai già iterando su un `DataTable`? Non sei l'unico. La maggior parte degli sviluppatori si trova in difficoltà quando ha bisogno di un'intestazione con carattere blu *e* di una colonna formattata come valuta nella stessa operazione di importazione. La buona notizia? Con poche righe di C# e gli oggetti style corretti, puoi farlo senza post‑processing del foglio.

In questo tutorial passeremo in rassegna un esempio completo e eseguibile che mostra come **format column as currency**, **set column number format** per qualsiasi altra colonna, e persino **set column font color** per le intestazioni. Alla fine avrai un modello riutilizzabile da inserire in qualsiasi progetto Aspose.Cells (o simile).

## Cosa imparerai

- Come recuperare un `DataTable` e mappare ogni colonna a uno specifico `Style`.
- I passaggi esatti per **apply number format excel** usando `Worksheet.Cells.ImportDataTable`.
- Perché creare gli stili in anticipo è più efficiente rispetto a formattare le celle una per una.
- Gestione dei casi limite quando la tabella di origine ha più colonne di quelle stilizzate.
- Un esempio di codice completo, pronto per copia‑incolla, che puoi eseguire subito.

> **Prerequisito:** Questa guida presuppone che tu abbia Aspose.Cells per .NET (o qualsiasi libreria che espone le API `Workbook`, `Worksheet`, `Style`) referenziata nel tuo progetto. Se stai usando una libreria diversa, i concetti si traducono direttamente—basta sostituire i nomi dei tipi.

---

## Passo 1: Recuperare i dati di origine come DataTable

Prima che possa avvenire qualsiasi formattazione, hai bisogno dei dati grezzi. Nella maggior parte degli scenari reali i dati risiedono in un database, CSV o un'API. Per semplicità, simuliamo un semplice `DataTable` con due colonne: *Product* (string) e *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Perché è importante:** Caricare i dati in un `DataTable` ti fornisce una rappresentazione tabellare in memoria che `ImportDataTable` può consumare direttamente, eliminando la necessità di inserimenti manuali cella per cella.

## Passo 2: Creare un array di Style – Uno per colonna

Il sovraccarico di `ImportDataTable` che utilizzeremo accetta un array di oggetti `Style`. Ogni voce corrisponde a un indice di colonna. Se lasci una voce come `null`, la colonna eredita lo stile predefinito della cartella di lavoro.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Consiglio:** Dichiarare l'array *dopo* aver ottenuto il `DataTable` garantisce che la dimensione corrisponda esattamente, evitando `IndexOutOfRangeException` in seguito.

## Passo 3: Impostare il colore del carattere della colonna (blu) per la prima colonna

Una richiesta comune è evidenziare le intestazioni o le colonne chiave con un colore di carattere distintivo. Qui impostiamo il testo della prima colonna in blu.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Perché usare un oggetto style?** Gli stili sono riutilizzabili e applicati in blocco, il che è molto più veloce rispetto all'iterazione su ogni cella dopo l'importazione. La cartella di lavoro memorizza lo stile una volta, poi lo riutilizza per ogni cella di quella colonna.

## Passo 4: Formattare la seconda colonna come valuta

I formati numerici integrati di Excel sono identificati da un indice. `14` corrisponde al formato valuta predefinito (es., `$1,234.00`). Se ti serve un formato personalizzato, puoi assegnare una stringa di formato al suo posto.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Caso limite:** Se la tua cartella di lavoro utilizza una locale in cui il simbolo di valuta non è `$`, lo stesso indice si adatterà automaticamente (es., `€` per le impostazioni tedesche).

## Passo 5: Importare il DataTable con gli stili definiti

Ora uniamo tutto. Il metodo `ImportDataTable` incollerà i dati a partire dalla cella `A1` (riga 0, colonna 0) e applicherà gli stili che abbiamo preparato.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Il secondo parametro `true` indica ad Aspose.Cells di trattare la prima riga del `DataTable` come intestazioni di colonna.
- Le coordinate `0, 0` specificano l'angolo in alto a sinistra dove inizia l'importazione.
- `columnStyles` associa ogni colonna al rispettivo stile.

## Passo 6: Salvare la cartella di lavoro (Opzionale, ma utile per la verifica)

Se vuoi vedere il risultato in Excel, basta salvare la cartella di lavoro su disco. Questo passaggio non è necessario per la logica di formattazione, ma è utile per il debug.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Output previsto

| **Prodotto** (font blu) | **Prezzo** (valuta) |
|--------------------------|----------------------|
| Apple                    | $1.25                |
| Banana                   | $0.75                |
| Cherry                   | $2.10                |

- La colonna *Prodotto* appare in blu, rendendola evidente.
- La colonna *Prezzo* mostra i valori con il simbolo di valuta predefinito e due cifre decimali.

---

## Domande frequenti e variazioni

### Come impostare **set column number format** per più di due colonne?

Basta estendere l'array `columnStyles`. Ad esempio, per mostrare una percentuale nella terza colonna:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Cosa fare se ho bisogno di un formato di valuta *personalizzato*, come “USD 1,234.00”?

Sostituisci la proprietà `Number` con una stringa di formato:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Posso applicare un **set column font color** a una colonna numerica senza influire sul suo formato numerico?

Assolutamente. Gli stili sono composabili. Puoi impostare sia `Font.Color` che `Number` sulla stessa istanza di `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Cosa succede se il `DataTable` ha più colonne degli stili?

Qualsiasi colonna senza uno stile esplicito (`null` entry) erediterà lo stile predefinito della cartella di lavoro. Per evitare `null` accidentali, puoi inizializzare prima l'intero array con uno stile base:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Quindi sovrascrivi solo le colonne che ti interessano.

### Questo approccio funziona con set di dati di grandi dimensioni (10k+ righe)?

Sì. Poiché la formattazione viene applicata *una volta per colonna* prima dell'importazione, l'operazione rimane O(N) rispetto alle righe e l'uso della memoria rimane basso. Evita di iterare su ogni cella dopo l'importazione—è lì che le prestazioni peggiorano.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Esegui il programma, apri `StyledReport.xlsx` e vedrai immediatamente il risultato di **apply number format excel**.

---

## Conclusione

Abbiamo appena dimostrato un modo pulito ed efficiente per **apply number format excel** a un `DataTable` importato. Preparando in anticipo un array `Style[]`, puoi **format column as currency**, **set column number format** e **set column font color** in una singola chiamata—senza necessità di post‑processing.  

Sentiti libero di estendere il modello: aggiungere formattazione condizionale, unire celle per le intestazioni, o persino inserire formule. Gli stessi principi si applicano, mantenendo il tuo codice ordinato e i tuoi fogli di calcolo dall'aspetto professionale.

### Prossimi passi

- Esplora **conditional formatting** per evidenziare i valori che superano una soglia.
- Combina questa tecnica con **pivot table generation** per report dinamici.
- Prova **setting column number format** per date, percentuali o notazione scientifica personalizzata.

Hai provato una variante? Condividila nei commenti—continuiamo a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}