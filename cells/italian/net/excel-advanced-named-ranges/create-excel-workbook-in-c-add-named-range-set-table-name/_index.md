---
category: general
date: 2026-07-13
description: Crea una cartella di lavoro Excel in C# e impara come aggiungere un intervallo
  denominato, assegnare un nome a una tabella e gestire i conflitti di denominazione—tutto
  in un unico esempio chiaro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: it
lastmod: 2026-07-13
og_description: Crea una cartella di lavoro Excel in C# con Aspose.Cells. Scopri come
  aggiungere un intervallo denominato, impostare il nome della tabella e risolvere
  i conflitti di denominazione in una guida concisa e operativa.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Crea cartella di lavoro Excel in C# – Aggiungi intervallo denominato e imposta
  il nome della tabella
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Crea cartella di lavoro Excel in C# – Aggiungi intervallo denominato e imposta
  il nome della tabella
url: /it/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una cartella di lavoro Excel in C# – Guida completa all’aggiunta di intervalli denominati e impostazione dei nomi delle tabelle

Ti è mai capitato di **creare una cartella di lavoro Excel** da zero e di chiederti dove inserire un intervallo denominato o come dare a una tabella il proprio identificatore? Non sei l’unico. In molti scenari di reporting o di esportazione dati, ti troverai a gestire intervalli, tabelle e occasionali conflitti di denominazione.  

In questo tutorial percorreremo un esempio completamente eseguibile che **crea una cartella di lavoro Excel**, **aggiunge un intervallo denominato**, e poi **assegna un nome a una tabella**—mostrando esattamente cosa fare quando i nomi entrano in conflitto. Alla fine conoscerai il “come” e il “perché” di ogni passaggio, oltre a qualche consiglio per mantenere il codice pulito.

> **Quick win:** Il codice utilizza la libreria **Aspose.Cells**, che funziona con .NET 6+ e non richiede l’installazione di Excel sul server.

---

## What You’ll Need

- **.NET 6 SDK** (o qualsiasi versione recente di .NET)  
- **Aspose.Cells for .NET** pacchetto NuGet  
- Un IDE decente (Visual Studio, Rider o VS Code)  
- Conoscenze di base di C#—nulla di speciale, solo le consuete istruzioni `using`

Se hai tutto questo, possiamo passare direttamente al processo di **create excel workbook**.

---

## ## Create Excel Workbook – Step‑by‑Step Overview

Di seguito trovi il programma completo, pronto per il copia‑incolla. Dimostra tutto, dalla creazione della cartella di lavoro alla gestione di un conflitto di denominazione quando provi a **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Output previsto** quando esegui il programma:

```
Naming conflict detected:
A name with the same text already exists.
```

E se apri *DemoWorkbook.xlsx* vedrai una tabella chiamata **Table1** e un intervallo denominato chiamato **MyRange**—esattamente ciò che volevamo, senza conflitti.

---

## ## Add Named Range – Why It Matters

Un **named range** è essenzialmente un alias per un blocco di celle. Invece di riferirti costantemente a `A1:B5`, puoi scrivere `MyRange` in formule, convalide dati o anche nel codice. Questo migliora la leggibilità e riduce la probabilità di bug dovuti a errori di battitura.

Nello snippet sopra chiamiamo:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Il primo argomento è il **name** che utilizzerai in seguito.  
- Il secondo argomento è l’**address** (relativo al foglio di lavoro).  

Se mai dovessi **how to add range** in modo dinamico, puoi costruire la stringa dell’indirizzo con `Cell.GetRefersTo()` o usare `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Handling Conflicts

Le tabelle (note anche come *list objects*) hanno già una proprietà nome integrata. Per impostazione predefinita Aspose.Cells le chiama `Table1`, `Table2`, ecc. Quando provi a dare a una tabella lo stesso identificatore di un intervallo denominato esistente, la libreria lancia un’eccezione—proprio come fa Excel.

Perché succede?

- L’ambito di denominazione di Excel è **workbook‑wide** sia per gli intervalli sia per le tabelle.  
- Nomi duplicati renderebbero le formule ambigue, quindi il motore li blocca.

### Pro tip

Se davvero hai bisogno che una tabella condivida un nome logico con un intervallo, considera di **prefissare** uno dei due, ad esempio:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Oppure rinomina prima l’intervallo:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Entrambi gli approcci mantengono pulito lo spazio dei nomi ed evitano errori a runtime.

---

## ## Set Table Name – Best Practices

Quando **set table name** programmaticamente, tieni presente queste linee guida:

1. **Usa un prefisso coerente** (`tbl_`, `rng_`, ecc.) – indica subito di che tipo di oggetto si tratta.  
2. **Rimani entro 255 caratteri** – limite di Excel per i nomi.  
3. **Evita spazi e caratteri speciali** – solo lettere, numeri e underscore sono sicuri.  
4. **Valida prima di assegnare** – un rapido controllo `if (!sheet.Names.Contains(name))` previene il conflitto mostrato in precedenza.

Ecco un metodo di supporto che puoi inserire in qualsiasi progetto:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Chiamare `SafeSetTableName(sheet, table, "MyRange")` trasformerà automaticamente `MyRange` in `MyRange_1` se esiste un conflitto, garantendo che l’operazione **create excel workbook** non aborta in modo inatteso.

---

## ## Full Working Example – Putting It All Together

Di seguito trovi una versione compatta che puoi copiare direttamente in un’app console. Include la routine di sicurezza e dimostra il flusso end‑to‑end.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Eseguendo questo script otterrai `FinalDemo.xlsx` dove la tabella si chiama `MyRange_1` (o un altro suffisso unico) e l’intervallo rimane `MyRange`. Nessuna eccezione, nessun mistero—solo una denominazione pulita e deterministica.

---

## ## Frequently Asked Questions (FAQ)

**Q: Posso aggiungere un intervallo denominato che si estende su più fogli di lavoro?**  
A: Sì, ma devi qualificare l’indirizzo con il nome del foglio, ad esempio `"Sheet1!A1:B5"`. Il metodo `Names.Add` accetta quel formato.

**Q: Aspose.Cells supporta intervalli denominati dinamici (come formule OFFSET)?**  
A: Assolutamente. Puoi passare una stringa di formula invece di un indirizzo statico, ad esempio `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Cosa devo fare se devo rinominare una tabella esistente?**  
A: Basta impostare `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}