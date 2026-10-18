---
category: general
date: 2026-03-30
description: Crea una cartella di lavoro Excel in C# con formattazione valuta. Scopri
  come importare un DataTable, aggiungere il formato numerico in Excel e applicare
  il formato valuta a una colonna in pochi minuti.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: it
og_description: Crea un workbook Excel in C# e formatta immediatamente le celle come
  valuta. Questo tutorial passo‑passo mostra come importare una DataTable in Excel
  e aggiungere il formato numerico Excel per una colonna.
og_title: Crea cartella di lavoro Excel C# – Guida alla formattazione della valuta
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crea cartella di lavoro Excel C# – Applica formato valuta e importa DataTable
url: /it/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare un Workbook Excel in C# – Applicare il Formato Valuta e Importare DataTable

Hai mai dovuto **creare un workbook Excel in C#** che abbia già l’aspetto di un report rifinito? Forse stai estraendo i dati di vendita da un database e vuoi che la colonna prezzo venga mostrata in dollari senza dover intervenire manualmente su Excel. Ti suona familiare? Non sei l’unico: la maggior parte degli sviluppatori incappa in questo ostacolo al primo tentativo di automatizzare le esportazioni Excel.

In questa guida percorreremo passo‑passo una soluzione completa, pronta all’uso, che **crea un workbook Excel in C#**, importa un `DataTable` e **formatta la colonna Price come valuta**. Alla fine avrai un file chiamato `StyledTable.xlsx` che potrai aprire e vedere numeri formattati correttamente. Nessun post‑processing aggiuntivo necessario.

> **Cosa imparerai**
> - Come configurare Aspose.Cells in un progetto .NET  
> - Come **importare datatable in excel** con un array di stili  
> - Come **aggiungere formato numero excel** per una colonna specifica  
> - Suggerimenti per gestire più colonne o impostazioni locali diverse  

> **Prerequisiti**  
> - .NET 6+ (o .NET Framework 4.6+) installato  
> - Pacchetto NuGet Aspose.Cells per .NET (`Install-Package Aspose.Cells`)  
> - Familiarità di base con C# e DataTables  

---

## Step 1: Prepare the DataTable (import datatable to excel)

Per prima cosa, servono dei dati di esempio. In un’app reale probabilmente riempirai questa tabella con una query al DB, ma un esempio hard‑coded mantiene le cose semplici.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Perché è importante*: il `DataTable` è il ponte tra i tuoi dati di business e il file Excel. Aspose.Cells può importarlo direttamente, preservando nomi delle colonne e tipi di dato.

---

## Step 2: Spin Up a New Workbook (create excel workbook c#)

Ora creiamo l’oggetto file Excel vero e proprio. Pensalo come la tela vuota su cui dipingere.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Consiglio:** Se ti servono più fogli, chiama `workbook.Worksheets.Add()` e assegna a ciascuno un nome significativo.

---

## Step 3: Define a Currency Style (format cells currency)

Aspose.Cells ti permette di creare un oggetto `Style` che descrive l’aspetto delle celle. Per la valuta usiamo l’ID formato numero integrato 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Perché non impostare direttamente la stringa di formato?* Usare l’ID integrato garantisce compatibilità tra le versioni di Excel ed evita stranezze legate alle impostazioni locali.

---

## Step 4: Build the Style Array (apply currency format column)

Quando importi un `DataTable`, puoi passare un array di oggetti `Style`—uno per colonna. `null` significa “usa lo stile predefinito”. Qui applichiamo `priceStyle` solo alla seconda colonna.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Se in seguito aggiungi altre colonne, estendi semplicemente l’array. La lunghezza di `columnStyles` deve corrispondere al numero di colonne che stai importando, altrimenti Aspose lancerà un’eccezione.

---

## Step 5: Import the DataTable with Styles (import datatable to excel)

Ora avviene la magia: il nostro `DataTable` viene inserito nel foglio di lavoro e la colonna prezzo appare subito formattata come valuta.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Cosa succede se hai più di due colonne?* Basta ampliare `columnStyles` in modo che ogni colonna ottenga lo stile appropriato (o `null` per quello predefinito). Questo è il modo più pulito per **aggiungere formato numero excel** in modo selettivo.

---

## Step 6: Save the Workbook (create excel workbook c#)

Infine, scriviamo il file su disco. Scegli qualsiasi cartella in cui hai permessi di scrittura.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Apri `StyledTable.xlsx` in Excel e dovresti vedere:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

La colonna **Price** è già formattata come valuta—nessun passaggio aggiuntivo necessario.

---

## Edge Cases & Variations

### More Columns, Different Formats

Se devi **formattare celle valuta** per più colonne (ad esempio Cost, Tax, Total), crea uno `Style` separato per ciascuna e popola `columnStyles` di conseguenza:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

Per Euro o Sterlina, usa ID integrati diversi (ad esempio 165 per `€#,##0.00`). In alternativa, imposta una stringa di formato personalizzata:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Aspose.Cells può gestire milioni di righe, ma il consumo di memoria cresce con gli oggetti stile. Riutilizza una singola istanza di `Style` per tutte le colonne valuta per mantenere basso l’ingombro.

### Missing Styles

Se `columnStyles` è più corto del numero di colonne, Aspose applicherà lo stile predefinito alle colonne rimanenti. Questo è utile quando ti interessano solo poche colonne.

---

## Full Working Example (All Steps Combined)

Di seguito trovi il programma completo da copiare‑incollare in una console app. Include tutti i pezzi discussi, più qualche commento utile.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Risultato atteso:** Aprendo `StyledTable.xlsx` vedrai la colonna `Price` con il simbolo del dollaro e due cifre decimali, esattamente come richiesto dall’istruzione **format cells currency**.

---

## Frequently Asked Questions

**D: Funziona con .NET Core?**  
R: Assolutamente. Aspose.Cells è conforme a .NET‑standard, quindi puoi puntare a .NET 5, .NET 6 o versioni successive senza modifiche.

**D: E se il mio DataTable ha 10 colonne ma voglio formattare solo la colonna 5?**  
R: Crea un `Style[]` di lunghezza 10, riempi le posizioni 0‑4 e 6‑9 con `null`, e inserisci lo stile personalizzato all’indice 4 (zero‑based). Aspose rispetterà ogni voce.

**D: Posso nascondere la riga di intestazione?**  
R: Dopo l’importazione, imposta `worksheet.Cells.Rows[0].Hidden = true;` oppure passa `false` per il parametro `includeColumnNames` in `ImportDataTable`.

---

## Conclusion

Abbiamo appena **creato un workbook Excel in C#**, importato un `DataTable` e **applicato un formato valuta a una colonna** usando Aspose.Cells. I passaggi principali—preparare i dati, definire uno stile, costruire un array di stili, importare con `ImportDataTable` e salvare—coprono il nucleo della maggior parte dei compiti di automazione Excel.

Da qui potresti esplorare:

- **aggiungere formato numero excel** per date o percentuali  
- Esportare più fogli in un unico file  
- Usare **format cells currency** con simboli specifici per locale  
- Automatizzare la creazione di grafici basati sugli stessi dati  

Provali e diventerai presto il punto di riferimento per i report Excel nel tuo team. Hai un trucco da condividere? Lascia un commento qui sotto—buona programmazione!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}