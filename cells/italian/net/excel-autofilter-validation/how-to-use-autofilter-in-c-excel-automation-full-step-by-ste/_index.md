---
category: general
date: 2026-05-30
description: Come utilizzare AutoFilter nell'automazione di Excel con C#. Scopri come
  creare una cartella di lavoro Excel, filtrare le righe per valore e ottimizzare
  le tue attività sui fogli di calcolo.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: it
og_description: Come utilizzare AutoFilter nell'automazione Excel con C#. Impara a
  creare cartelle di lavoro Excel, filtrare le righe per valore e automatizzare i
  fogli di calcolo con facilità.
og_title: Come utilizzare AutoFilter in C# per l'automazione di Excel – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Come utilizzare AutoFilter in C# per l'automazione di Excel – Guida completa
  passo passo
url: /it/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare AutoFilter in C# per l'automazione di Excel – Guida completa

Ti sei mai chiesto **come usare AutoFilter** quando generi file Excel dal codice C#? Non sei l'unico: molti sviluppatori incontrano questo ostacolo quando devono nascondere le righe che non corrispondono a un certo criterio.  

In questo tutorial percorreremo un esempio concreto e eseguibile che **crea una cartella di lavoro Excel**, aggiunge una tabella e poi **filtra le righe per valore** nella colonna B. Alla fine avrai uno snippet pulito e riutilizzabile da inserire in qualsiasi progetto C# che richieda l'automazione di Excel.

## Cosa imparerai

- Configurare un progetto C# con la libreria Aspose.Cells (o Microsoft.Office.Interop).  
- **Creare programmaticamente una cartella di lavoro Excel** e aggiungere una tabella con stile.  
- Applicare **AutoFilter** per mostrare solo le righe dove **la colonna B** è uguale a una stringa specifica.  
- Rimuovere completamente il filtro, ripristinando l'intero set di dati.  
- Suggerimenti per gestire casi particolari come colonne mancanti o più criteri di filtro.

Non è necessaria alcuna esperienza pregressa con Excel‑VBA; basta una conoscenza di base di C# e dei pacchetti NuGet.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 o successivo (o .NET Framework 4.7+) | I runtime moderni offrono migliori prestazioni e una gestione più semplice dei pacchetti. |
| Aspose.Cells per .NET (o Microsoft.Office.Interop.Excel) installato via NuGet | Questa libreria fornisce gli oggetti `Workbook`, `Worksheet` e `Table` usati nel codice. |
| Un editor di codice (Visual Studio, VS Code, Rider, ecc.) | Avrai bisogno di compilare ed eseguire l'esempio. |
| Conoscenze di base di C# | Il tutorial spiega *perché* ogni riga esiste, non solo *cosa* fa. |

Puoi installare Aspose.Cells con:

```bash
dotnet add package Aspose.Cells
```

---

## Come usare AutoFilter con Aspose.Cells in C#

Di seguito trovi il programma completo e autonomo. Salvalo come `Program.cs` in un progetto console ed eseguilo – otterrai `FilteredWorkbook.xlsx` nella cartella di output.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Come funziona il codice

1. **Creazione della cartella di lavoro** – `new Workbook()` ti fornisce un file vuoto; `Worksheets[0]` prende il foglio predefinito.  
2. **Popolamento dei dati di esempio** – Scriviamo un piccolo dataset così puoi vedere il filtro in azione.  
3. **Aggiunta di una tabella** – `ListObjects.Add` converte l'intervallo in una tabella Excel, che supporta automaticamente filtraggio e formattazione.  
4. **Applicazione di AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` dice al motore: “Mostra solo le righe dove la seconda colonna (B) è uguale a *Apple*.”  
5. **Salvataggio dei file** – Vengono scritti due file: uno filtrato e uno con il filtro rimosso, dimostrando che `RemoveAutoFilter()` funziona come previsto.

> **Consiglio professionale:** Se devi filtrare per più criteri (ad es., “Apple” *o* “Banana”), usa la sovraccarico `Filter(int columnIndex, string criteria1, string criteria2)` oppure passa un array di stringhe.

---

## Filtrare le righe per valore – Varianti comuni

Mentre l'esempio sopra si concentra su **filtrare la colonna B**, potresti voler filtrare altre colonne o usare criteri numerici. Ecco una rapida cheat sheet:

| Filtro desiderato | Frammento di codice |
|----------------|--------------|
| Corrispondenza di testo nella colonna C | `table.AutoFilter.Filter(2, "Cherry");` |
| Numeri maggiori di 10 nella colonna C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Più valori nella colonna B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Caso limite:** Se l'intestazione della colonna è scritta in modo errato o l'indice della colonna è fuori intervallo, Aspose.Cells lancia un `ArgumentException`. Proteggi il tuo codice verificando `table.ListColumns.Count` prima di applicare il filtro.

---

## Rimuovere AutoFilter – Quando resettare

A volte è necessario mostrare nuovamente l'intero set di dati (ad es., dopo che l'utente ha cancellato una casella di ricerca). Chiamare `table.RemoveAutoFilter()` risolve il problema in una sola riga. Se usi Microsoft.Office.Interop, dovrai impostare `worksheet.AutoFilterMode = false;`.

---

## Riepilogo dell'esempio completo

Di seguito trovi nuovamente il *programma intero*, privo di commenti per chi preferisce una visuale concisa:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Eseguendo questo otterrai due file:

- **FilteredWorkbook.xlsx** – solo le righe con *Apple* visibili.  
- **UnfilteredWorkbook.xlsx** – i dati originali ripristinati.

---

## Domande frequenti

**D: Funziona con file .xls più vecchi?**  
R: Sì. Aspose.Cells può salvare sia in `.xlsx` che in `.xls` cambiando l'estensione del file o usando `SaveOptions`.

**D: E se devo filtrare *dopo* che la cartella di lavoro è già stata salvata?**  
R: Carica il file con `new Workbook("path.xlsx")`, applica il filtro, poi `Save` nuovamente.

**D: Posso applicare un filtro a un *range* che non è una tabella?**  
R: Assolutamente. Usa `worksheet.AutoFilter.Range = "A1:C5";` e poi `worksheet.AutoFilter.ApplyFilter();`. Tuttavia, le tabelle offrono stilizzazione integrata e un riferimento alle colonne più semplice.

---

## Immagine – Conferma visiva

![Screenshot che mostra AutoFilter applicato alla colonna B in una cartella di lavoro Excel creata con C#](/images/autofilter-column-b.png "AutoFilter sulla colonna B")

*(L'immagine illustra la visuale filtrata dove rimangono solo le righe contenenti “Apple”.)*

---

## Conclusione

Abbiamo appena coperto **come usare AutoFilter** in uno scenario di automazione Excel guidato da C#, dalla **creazione di una cartella di lavoro Excel** al **filtrare le righe per valore** nella **colonna B**, fino alla **rimozione del filtro** quando non è più necessario. I passaggi fondamentali—inizializzare, aggiungere una tabella, applicare il filtro e pulire—sono riutilizzabili in qualsiasi progetto che richieda **excel automation c#**.

Pronto per la prossima sfida? Prova:

- Aggiungere formattazione condizionale per evidenziare le righe filtrate.  
- Esportare i dati filtrati in CSV per l'elaborazione successiva.  
- Combinare più filtri (ad es., “Apple” *e* quantità > 8).

Sperimenta, rompe le cose e poi riparale—

## Cosa dovresti imparare dopo?

- [How to Implement AutoFilter in Excel using Aspose.Cells for .NET (Data Analysis Guide)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [How to Use Autofilter Not Contains in Aspose.Cells .NET for Excel Data Analysis](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [How to Implement Excel Autofilter 'EndsWith' Using Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}