---
category: general
date: 2026-02-28
description: Elimina rapidamente le righe di una tabella Excel in C#. Scopri come
  aggiungere un intervallo denominato in Excel, accedere al foglio di lavoro per nome
  e evitare errori di nome duplicato.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: it
og_description: Elimina righe da una tabella Excel usando C#. Questo tutorial mostra
  anche come aggiungere un intervallo denominato in Excel e accedere al foglio di
  lavoro per nome.
og_title: Elimina righe della tabella Excel con C# – Guida completa
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Elimina righe da una tabella Excel con C# – Guida passo passo
url: /it/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Elimina righe da una tabella Excel con C# – Tutorial di programmazione completo

Ti è mai capitato di dover **delete rows excel table** da una cartella di lavoro ma non eri sicuro di quale chiamata API utilizzare? Non sei l'unico—la maggior parte degli sviluppatori si imbatte nello stesso ostacolo quando tenta per la prima volta di ridurre una tabella programmaticamente.  

In questa guida percorreremo un esempio completo e eseguibile che non solo rimuove le righe da una tabella Excel, ma mostra anche **how to add defined name** (aka *named range*), come **access worksheet by name**, e perché aggiungere un nome duplicato su un altro foglio genera un `InvalidOperationException`.  

Entro la fine dell'articolo sarai in grado di:

* Ottenere un foglio di lavoro usando il nome della sua scheda.  
* Eliminare in modo sicuro le righe di dati dalla prima tabella su quel foglio.  
* Creare un named range che punti a un indirizzo specifico.  
* Comprendere le insidie dei nomi duplicati tra i fogli.  

Nessuna documentazione esterna necessaria—tutto ciò di cui hai bisogno è qui.

---

## Cosa ti serve

* **DevExpress Spreadsheet** (o qualsiasi libreria che espone gli oggetti `Workbook`, `Worksheet`, `ListObject` e `Names`).  
* Un progetto .NET che targetizza **.NET 6** o versioni successive (il codice compila anche con .NET Framework 4.8).  
* Familiarità di base con C#—se sai scrivere un ciclo `foreach`, sei pronto.  

> **Pro tip:** Se stai usando la Community Edition gratuita di DevExpress, le API usate di seguito sono identiche a quelle della versione commerciale.

---

## Step 1 – Access Worksheet by Name

La prima cosa da fare è individuare il foglio che contiene la tabella che vuoi modificare.  
La maggior parte degli sviluppatori usa `Worksheets[0]` per abitudine, ma questo lega il tuo codice all'ordine dei fogli e si rompe non appena qualcuno rinomina una scheda.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Why this matters:* Usando il **name** del foglio invece del suo indice eviti modifiche accidentali al foglio sbagliato quando la cartella di lavoro cambia.  

Se il nome fornito non esiste, la libreria genera una `KeyNotFoundException`, che puoi catturare per mostrare un messaggio di errore amichevole.

---

## Step 2 – Delete Rows Excel Table (The Safe Way)

Ora che hai il foglio di lavoro corretto, rimuoviamo le righe di dati dalla prima tabella.  
Un errore comune è chiamare `DeleteRows(1, rowCount‑1)`. Dal **DevExpress 22.2** quell'overload è **prohibited** e genera un `InvalidOperationException`. La libreria si aspetta che tu elimini le righe **within the table’s data range**, non la riga di intestazione.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **What if the table is empty?** La guardia `if` impedisce una chiamata con `rowCount = 0`, che altrimenti solleverebbe un'eccezione.

### Visual Overview  

![esempio di eliminazione righe tabella excel](image.png "Screenshot che mostra le righe rimosse da una tabella Excel")  

*Alt text: esempio di eliminazione righe tabella excel in codice C#*

---

## Step 3 – How to Add Defined Name (Create a Named Range)

Dopo aver pulito la tabella potresti voler fare riferimento a un intervallo specifico in seguito—ad esempio per un grafico o una lista di convalida dati. È qui che entra in gioco **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Il metodo `Names.Add` accetta due parametri: l'identificatore e l'indirizzo in stile A1.  
Poiché in precedenza abbiamo usato **access worksheet by name**, la stringa dell'indirizzo può fare riferimento in modo sicuro a qualsiasi foglio senza preoccuparsi dei cambiamenti di indice.

---

## Step 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

Potresti pensare di poter riutilizzare lo stesso identificatore su un foglio diverso, così:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Sfortunatamente, l'ambito di denominazione di Excel è **workbook‑wide**, non per‑sheet. La chiamata sopra genera un `InvalidOperationException` con il messaggio *“A name with the same identifier already exists.”*  

### How to Work Around It

1. **Scegli un nome unico** (`MyTable_Sheet2`).  
2. **Elimina il nome esistente** prima di ri‑aggiungerlo (solo se vuoi davvero sostituirlo).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Esempio completo e eseguibile

Mettendo tutto insieme, ecco un'app console autonoma che puoi inserire in Visual Studio e eseguire su un file di esempio `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Risultato atteso**

* Tutte le righe di dati dalla prima tabella su **Sheet1** scompaiono, lasciando solo la riga di intestazione.  
* Il nome **MyTable** ora punta a `Sheet1!$A$1:$C$5`.  
* Un secondo nome **MyTable_Sheet2** fa riferimento in modo sicuro a un intervallo su **Sheet2** senza generare un'eccezione.

---

## Domande comuni e casi limite

| Question | Answer |
|----------|--------|
| *E se la cartella di lavoro ha più tabelle?* | Ottieni il `ListObject` corretto per indice (`worksheet.ListObjects[1]`) o per nome (`worksheet.ListObjects["MyTable"]`). |
| *Posso eliminare righe da una tabella che si estende su più fogli?* | No—le tabelle sono limitate a un singolo foglio. Devi ripetere la logica di eliminazione per ogni foglio. |
| *Esiste un modo per eliminare solo un sottoinsieme di righe?* | Sì—usa `table.DeleteRows(startRow, count)` dove `startRow` è basato su zero nell'area dati della tabella. |
| *I named range sopravvivono dopo il salvataggio?* | Assolutamente. Dopo aver chiamato `SaveDocument`, i nomi diventano parte dell'XML della cartella di lavoro. |
| *Come posso elencare tutti i nomi definiti nella cartella di lavoro?* | Itera `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusione

Abbiamo coperto **delete rows excel table** usando C#, dimostrato **add named range excel**, e mostrato il modo corretto per **access worksheet by name** evitando l'odiosa eccezione di nome duplicato.  

La soluzione completa è nel frammento di codice sopra—copia, incolla e eseguilo sui tuoi file. Da qui puoi espandere la logica per gestire più tabelle, calcoli di intervalli dinamici, o persino integrarla con un'interfaccia utente.  

**Prossimi passi** da esplorare:

* Usa **named range on another sheet** per alimentare le serie di un grafico.  
* Combina la logica di eliminazione con **ExcelDataReader** per importare dati prima di pulirli.  
* Automatizza aggiornamenti massivi su decine di cartelle di lavoro usando un semplice ciclo `foreach (var file in Directory.GetFiles(...))`.  

Hai altre domande sull'automazione di Excel in C#? Lascia un commento e continuiamo la conversazione. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}