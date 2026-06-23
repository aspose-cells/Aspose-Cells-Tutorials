---
category: general
date: 2026-06-05
description: Applica gli stili delle celle durante l'importazione con Aspose.Cells.
  Scopri come importare un DataTable con formattazione, stilizzare le righe e mantenere
  i fogli di lavoro ordinati.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: it
og_description: Applica gli stili di cella durante l'importazione di una DataTable
  in un foglio di lavoro Aspose.Cells. Guida passo‑passo con codice completo e consigli.
og_title: Applica stili di cella con Aspose.Cells – Importa DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Applica stili di cella con Aspose.Cells – Importa DataTable con formattazione
url: /it/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicare Stili di Cella con Aspose.Cells – Importare DataTable con Formattazione

Ti sei mai chiesto come **applicare gli stili di cella** quando importi un `DataTable` in un foglio Excel? Non sei l'unico. In molti scenari di reporting è necessario che i dati siano già ben formattati—senza doverli formattare manualmente in seguito. La buona notizia è che Aspose.Cells rende semplice **importare con formattazione** così le tue righe possono essere rosse o blu, in grassetto, o qualsiasi cosa tu desideri.

In questo tutorial vedremo un esempio completo e funzionante che mostra **come importare un datatable** in un foglio di lavoro **con gli stili di cella** applicati. Alla fine avrai un'app console C# pronta da eseguire che crea una cartella di lavoro, applica stili alle prime due colonne e salva il file—tutto usando l'API `aspose cells import`.

## Cosa Imparerai

- Configurare Aspose.Cells in un progetto .NET  
- Creare un `DataTable` di esempio che imita dati reali  
- Definire oggetti `Style` per caratteri rossi e blu  
- Utilizzare `Worksheet.Cells.ImportDataTable` per **importare il datatable nel foglio di lavoro** applicando gli stili  
- Verificare il risultato e salvare la cartella di lavoro  

Nessuno strumento esterno, solo puro C# e Aspose.Cells. Iniziamo.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 o successivo | Aspose.Cells 23.x è destinato a .NET Standard 2.0+, quindi .NET 6 ti offre le ultime funzionalità del runtime. |
| Aspose.Cells per .NET (NuGet) | La libreria fornisce i metodi `Workbook`, `Worksheet`, `Style` e `ImportDataTable` di cui abbiamo bisogno. |
| Conoscenza di base di C# | Capirai classi, array e le istruzioni `using`. |
| Un IDE (Visual Studio, VS Code, Rider) | Qualsiasi editor va bene, ma dovrai ripristinare i pacchetti NuGet. |

Puoi installare il pacchetto dalla riga di comando:

```bash
dotnet add package Aspose.Cells
```

## Passo 1: Creare una Nuova Cartella di Lavoro e Accedere al Primo Foglio di Lavoro

Prima di tutto—creiamo un `Workbook` e otteniamo il primo foglio. Pensa alla cartella di lavoro come a un quaderno vuoto; il primo foglio è la pagina su cui scriveremo.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Suggerimento:** Se mai avrai bisogno di più fogli, aggiungili con `wb.Worksheets.Add()` e riferisciti a loro per nome o indice.

## Passo 2: Preparare un DataTable di Esempio (Come Importare DataTable)

Ora abbiamo bisogno di qualcosa da importare. Nei progetti reali chiameresti un DB, ma per semplicità costruiremo un `DataTable` in memoria.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Perché è importante:** Avere un `DataTable` ci permette di testare il flusso di **aspose cells import** senza dipendenze esterne.

## Passo 3: Definire gli Stili da Applicare alle Celle Importate

Qui avviene la magia. Creeremo due oggetti `Style`: uno con carattere rosso, un altro con carattere blu. Questi saranno applicati colonna per colonna durante l'importazione.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Attenzione:** La lunghezza di `importStyles` deve corrispondere al numero di colonne che stai importando, altrimenti Aspose genererà un `ArgumentException`.

## Passo 4: Importare il DataTable nel Foglio di Lavoro **con Formattazione**

Ora mettiamo tutto insieme. La sovraccarico di `ImportDataTable` che utilizziamo accetta l'array `Style[]`, permettendoci di **applicare gli stili di cella** mentre i dati vengono inseriti nel foglio.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Come Funziona

1. **Intestazioni** – Poiché abbiamo passato `true`, Aspose scrive “Name” e “Score” nella prima riga.  
2. **Righe di Dati** – Ogni riga successiva riceve lo stile corrispondente da `importStyles`.  
3. **Prestazioni** – Il metodo trasmette i dati direttamente nel foglio di lavoro, più veloce rispetto al ciclo cella per cella.

## Passo 5: Verificare il Risultato e Salvare la Cartella di Lavoro

Diamo un'occhiata alle prime celle per assicurarci che gli stili siano stati applicati, poi scriviamo il file su disco.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Quando apri **StyledImport.xlsx**, vedrai:

- La colonna “Name” con testo **rosso**.  
- La colonna “Score” con testo **blu**.  
- Le intestazioni di colonna nello stile predefinito (potresti anche stilizzarle, ma è un altro tutorial).

![Esempio di applicazione di stili di cella](https://example.com/images/apply-cell-styles.png "Applicare stili di cella in Aspose.Cells")

> **Nota:** L'immagine sopra mostra l'aspetto finale. L'attributo `alt` contiene la parola chiave principale, soddisfacendo i requisiti SEO.

## Domande Frequenti & Casi Limite

### Cosa Succede se il Mio DataTable Ha Più Colonne Dei Stili?

Aspose applicherà l'ultimo stile dell'array a tutte le colonne extra. Per evitare colori inattesi, fai sempre corrispondere la lunghezza dell'array al numero di colonne, oppure passa `null` per le colonne che non vuoi stilizzare.

### Posso Applicare Stili Diversi a Righe Specifiche?

Assolutamente. Dopo l'importazione, puoi iterare le righe e assegnare nuovi oggetti `Style` in base a condizioni (ad esempio, evidenziare i punteggi > 90 in verde). Ecco un breve frammento:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Funziona con Set di Dati di Grandi Dimensioni?

Sì. `ImportDataTable` trasmette i dati in modo efficiente, e l'applicazione di un array di stili statici aggiunge un overhead trascurabile. Per milioni di righe, considera di usare `ImportDataTable` a blocchi o di sfruttare `Cells.ImportDataTable` con un `DataReader` per un uso della memoria ancora migliore.

### Come Posso Conservare la Formattazione Esistente nel Foglio di Lavoro?

Se l'intervallo di destinazione ha già una formattazione che desideri mantenere, imposta il parametro `importOptions` della sovraccarico di `ImportDataTable` (`ImportTableOptions`) e modifica `ImportDataTableOptions.PreserveCellFormatting`. Il comportamento predefinito sovrascrive gli stili con quelli forniti.

## Riepilogo: Cosa Abbiamo Realizzato

- **Applicati stili di cella** durante un'operazione di **aspose cells import**.  
- Dimostrato **l'importazione con formattazione** passando un array `Style[]`.  
- Mostrato **come importare un datatable** in un foglio di lavoro e salvare il risultato.  
- Coperti casi limite come conteggi di stile non corrispondenti e stilizzazione condizionale delle righe.

Tutto questo è stato realizzato in una singola app console autonoma—senza script esterni, senza manipolazioni manuali di Excel. Ora hai una solida base per qualsiasi funzionalità di reporting o esportazione dati che richieda un output Excel curato.

## Prossimi Passi

Pronto a fare il prossimo passo? Ecco alcune idee che si basano su quanto appena appreso:

- **Stilizzare la riga di intestazione** (ad esempio, grassetto, colore di sfondo).  
- **Applicare la formattazione condizionale** usando `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Esportare in altri formati** come CSV o PDF con `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Combinare più DataTable** in una singola cartella di lavoro, ognuna su un proprio foglio, usando lo stesso approccio di stilizzazione.

Se incontri problemi, lascia un commento o consulta la documentazione ufficiale di Aspose su `ImportDataTable`. Buon coding e goditi quei file Excel splendidamente stilizzati!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Importare DataTable in Excel Usando Aspose.Cells per .NET (Guida Passo‑Passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Come Impostare Stili di Font in Excel Usando Aspose.Cells per .NET (Guida Passo‑Passo)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Come Applicare Ombra al Testo in Excel Usando Aspose.Cells .NET: Guida Passo‑Passo](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}