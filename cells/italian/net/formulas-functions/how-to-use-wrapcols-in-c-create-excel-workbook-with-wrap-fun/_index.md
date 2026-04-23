---
category: general
date: 2026-03-30
description: Impara come usare WRAPCOLS in C# per creare una cartella di lavoro Excel,
  aggiungere dati in Excel e forzare il calcolo delle formule, utilizzando anche WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: it
og_description: Scopri come utilizzare WRAPCOLS in C# per creare una cartella di lavoro
  Excel, aggiungere dati, forzare il calcolo delle formule e sfruttare WRAPROWS per
  le formule array.
og_title: Come usare WRAPCOLS in C# – Guida completa
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Come usare WRAPCOLS in C# – Creare una cartella di lavoro Excel con le funzioni
  di avvolgimento
url: /it/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS in C# – Creare una cartella di lavoro Excel con le funzioni Wrap

Ti sei mai chiesto **how to use WRAPCOLS** quando automatizzi Excel con C#? Non sei solo—molti sviluppatori si trovano in difficoltà quando devono trasformare un intervallo orizzontale in un array verticale senza scrivere una montagna di codice. La buona notizia è che Aspose.Cells lo rende un gioco da ragazzi.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra **how to use WRAPCOLS**, come **create Excel workbook C#**‑style, come **add data to Excel**, e persino come **force formula calculation** affinché i risultati appaiano immediatamente. Inseriremo anche **how to use WRAPROWS** per la trasformazione opposta. Alla fine avrai un programma pronto da eseguire e una chiara comprensione del motivo per cui ogni passaggio è importante.

---

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## Cosa copre questa guida

* Impostare una nuova cartella di lavoro con Aspose.Cells.
* Popolare le celle programmaticamente (**add data to Excel**).
* Applicare la funzione `WRAPCOLS` per trasformare una riga in una colonna.
* Usare `WRAPROWS` per trasformare una colonna in una riga (**how to use wraprows**).
* Forzare il motore a valutare le formule immediatamente (**force formula calculation**).
* Salvare il file e verificare l'output.

Non è necessaria alcuna documentazione esterna—tutto ciò di cui hai bisogno è qui.

---

## Come usare WRAPCOLS in C# – Implementazione passo‑passo

Di seguito trovi il file sorgente completo. Sentiti libero di copiarlo‑incollarlo in un nuovo progetto console, aggiungere il pacchetto NuGet Aspose.Cells e premere **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Perché ogni riga è importante

| Passo | Spiegazione |
|------|-------------|
| **1️⃣ Crea una nuova cartella di lavoro** | Questa è la base. Aspose.Cells tratta un oggetto `Workbook` come l'intero file Excel, quindi stai effettivamente **creating an Excel workbook C#**‑style. |
| **2️⃣ Ottieni il primo foglio di lavoro** | Una nuova cartella di lavoro contiene sempre almeno un foglio di lavoro (`Worksheets[0]`). Accedervi subito evita sorprese di riferimento nullo. |
| **3️⃣ Aggiungi dati a Excel** | Usando `PutValue` **add data to Excel** senza preoccuparsi della formattazione delle celle. I numeri `1` e `2` sono i nostri dati di test per le funzioni wrap. |
| **4️⃣ Come usare WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` indica a Excel di prendere l'intervallo `A1:B1` e di distribuire i suoi valori verticalmente, uno per riga. Il risultato viene collocato in `C1` e si estende verso il basso (`C1`, `C2`, …). |
| **5️⃣ Come usare WRAPROWS** | `WRAPROWS(A1:B1, 2)` fa l'opposto: crea una distribuzione orizzontale, inserendo i due valori in una singola riga a partire da `C2`. |
| **6️⃣ Forza il calcolo delle formule** | Per impostazione predefinita, Aspose.Cells può posticipare il calcolo fino a quando il file non viene aperto in Excel. Chiamare `CalculateFormula()` **forces formula calculation** così puoi leggere i risultati immediatamente dopo il salvataggio. |
| **7️⃣ Salva la cartella di lavoro** | L'ultimo passaggio scrive tutto su disco. Apri il file risultante `WrapFunctions.xlsx` per vedere il risultato. |

---

## Creare una cartella di lavoro Excel C# – Configurare l'ambiente

Prima di eseguire il codice, assicurati di avere gli strumenti giusti:

1. **.NET 6.0+** – La versione LTS più recente funziona al meglio.
2. **Visual Studio 2022** (o VS Code con l'estensione C#).
3. **Aspose.Cells for .NET** – Installa tramite NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. Una cartella scrivibile per il file di output.

Questi prerequisiti sono minimi; non è necessario alcun interop COM o installazione di Office, motivo per cui Aspose.Cells è una scelta popolare per la generazione di Excel lato server.

---

## Aggiungere dati a Excel – Migliori pratiche

Quando **add data to Excel** programmaticamente, considera questi consigli:

* **Use `PutValue`** per numeri grezzi o stringhe; rileva automaticamente il tipo di dato.
* **Avoid hard‑coding cell addresses** in large projects—usa cicli o intervalli denominati per la scalabilità.
* **Set cell styles sparingly**; ogni cambiamento di stile comporta un overhead. Se hai bisogno di formattazione, crea un unico oggetto stile e applicalo a più celle.

Nel nostro piccolo esempio inseriamo solo due numeri, ma lo stesso schema scala a migliaia di righe.

---

## Come usare WRAPROWS – Esempio di array orizzontale

Se ti serve l'opposto di `WRAPCOLS`, `WRAPROWS` è la tua soluzione. La sintassi è:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – l'intervallo che vuoi trasformare.
* `rows_per_item` – opzionale; indica a Excel quante righe occupa ogni elemento. Nel nostro demo abbiamo usato `2` per forzare entrambi i valori su una singola riga.

Puoi sperimentare cambiando il secondo argomento:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Apri la cartella di lavoro e vedrai i valori distribuiti su tre colonne, ciascuna colonna contenente i numeri originali ripetuti secondo necessità.

---

## Forzare il calcolo delle formule – Quando e perché

Potresti chiederti, “Devo davvero chiamare `CalculateFormula()`?” La risposta è **sì**, se:

* Hai intenzione di leggere i valori calcolati **programmatically** dopo il salvataggio.
* Vuoi garantire che il file si apra in Excel con i risultati corretti già visualizzati.
* Stai eseguendo in un **headless environment** (ad esempio, un'API web) dove nessun utente attiverà manualmente un ricalcolo.

Saltare questo passaggio non romperà la cartella di lavoro, ma le celle mostreranno il testo della formula (`=WRAPCOLS(...)`) invece dei valori calcolati finché Excel non ricalcola.

---

## Output previsto – Cosa cercare

Dopo aver eseguito il programma e aperto `WrapFunctions.xlsx`:

| Cella | Formula | Valore visualizzato |
|------|---------|---------------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (in C1) e `2` (in C2) – un elenco verticale |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` in C2 e `2` in D2 – un elenco orizzontale |

Quindi vedrai una colonna di valori che inizia da **C1** e una riga di valori che inizia da **C2**. Questo conferma che entrambe le funzioni wrap hanno funzionato come previsto.

---

## Casi limite e variazioni

| Scenario | Cosa cambia? | Suggerimento |
|----------|---------------|--------------|
| **Large range (A1:Z1)** | Più valori da distribuire verticalmente | Aumenta il secondo argomento di `WRAPCOLS` se desideri più colonne per gruppo. |
| **Non‑numeric data** | Le stringhe sono gestite allo stesso modo | Nessuna modifica al codice; `PutValue` accetta qualsiasi oggetto. |
| **Dynamic range** | Non conosci la dimensione al momento della compilazione | Usa `sheet.Cells.MaxDataColumn` e `MaxDataRow` per costruire la stringa dell'indirizzo. |
| **Multiple worksheets** | È necessario applicare le funzioni wrap su fogli diversi | Riferisci il foglio di lavoro corretto (`workbook.Worksheets["Sheet2"]`). |

Prevedendo queste variazioni, puoi adattare il modello di base a quasi qualsiasi scenario di automazione.

---

## Consigli professionali dal campo

* **Pro tip:** Avvolgi la creazione della cartella di lavoro in un blocco `using` se stai puntando a .NET Core 3.1+ per garantire che tutte le risorse vengano rilasciate prontamente.
* **Watch out for:** Impostare la stessa formula in un ampio intervallo senza chiamare `CalculateFormula()` può causare colli di bottiglia nelle prestazioni. Elabora le formule in batch quando possibile.
* **Tip:** Se hai bisogno di leggere nuovamente i valori calcolati nel codice, chiama `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}