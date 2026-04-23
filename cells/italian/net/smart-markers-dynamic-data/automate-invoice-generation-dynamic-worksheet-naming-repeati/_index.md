---
category: general
date: 2026-02-14
description: 'Automatizza la generazione delle fatture con SmartMarker: impara a duplicare
  i fogli di lavoro, a nominarli dinamicamente e a padroneggiare la denominazione
  dinamica dei fogli di lavoro in pochi minuti.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: it
og_description: Automatizza la generazione delle fatture con SmartMarker. Questa guida
  mostra come ripetere i fogli di lavoro, nominarli dinamicamente e padroneggiare
  la denominazione dinamica dei fogli di lavoro.
og_title: Automatizza la generazione delle fatture – Nominazione dinamica dei fogli
  di lavoro e ripetizione
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatizza la generazione delle fatture – Nominazione dinamica dei fogli di
  lavoro e ripetizione in C#
url: /it/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

.

Be careful with markdown syntax.

Proceed.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatizzare la generazione di fatture – denominazione dinamica dei fogli di lavoro e ripetizione in C#

Ti sei mai chiesto come **automatizzare la generazione di fatture** senza copiare manualmente i fogli per ogni ordine? Non sei l’unico. Molti sviluppatori si trovano in difficoltà quando hanno bisogno di un foglio di lavoro separato per ogni fattura ma vogliono anche che il nome del foglio rifletta il numero dell’ordine. In questo tutorial risolveremo il problema usando `SmartMarkerProcessor` di SmartMarker e ti mostreremo **come denominare i fogli di lavoro** in modo dinamico, coprendo anche **come ripetere un foglio di lavoro** per ogni record. Alla fine avrai un esempio C# pronto all’uso che produce una cartella di lavoro dove ogni fattura vive nella sua scheda, con un nome appropriato.

Percorreremo ogni passaggio—dall’estrazione degli ordini da una fonte dati alla configurazione di `SmartMarkerOptions` per la denominazione dinamica dei fogli. Nessuna documentazione esterna è necessaria; tutto ciò che ti serve è qui. Basta una minima conoscenza preliminare di C# e un riferimento alla libreria Aspose.Cells (o a qualsiasi motore compatibile con SmartMarker).

---

## Cosa costruirai

- Recuperare una collezione di oggetti ordine.
- Configurare SmartMarker per **ripetere un foglio di lavoro** per ogni ordine.
- Applicare **denominazione dinamica dei fogli di lavoro** usando il segnaposto `{OrderId}`.
- Generare un file Excel dove ogni scheda è nominata `Invoice_12345`, `Invoice_67890`, ecc.
- Verificare l’output aprendo la cartella di lavoro.

---

## Prerequisiti

- .NET 6.0 o successivo (il codice compila anche con .NET 5+).
- Aspose.Cells per .NET (o qualsiasi libreria che implementi SmartMarker). Installala via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Una classe `Order` di base (puoi sostituirla con il tuo DTO).

---

## Passo 1: Configura il progetto e il modello

Per prima cosa, crea una nuova console app e definisci il modello dati che rappresenta un ordine.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Consiglio:** Mantieni il modello leggero per la demo; potrai sempre arricchirlo in seguito con righe di dettaglio, informazioni fiscali, ecc.

---

## Passo 2: Prepara il modello Excel

SmartMarker lavora su una cartella di lavoro modello. Crea un file chiamato `InvoiceTemplate.xlsx` con un unico foglio denominato `InvoiceTemplate`. Nella cella **A1** inserisci un segnaposto SmartMarker come:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Puoi formattare le celle come preferisci—intestazioni in grassetto, formattazione valuta, ecc. Salva il file nella cartella radice del progetto.

> **Perché un modello?** Separa il layout dal codice, consentendo ai designer di modificare l’aspetto senza toccare la logica.

---

## Passo 3: Configura le opzioni di SmartMarker – Ripeti e nomina i fogli

Ora diremo a SmartMarker di *ripetere* il foglio modello per ogni ordine e di assegnare a ciascuna copia un nome che includa l’ID ordine. Questo è il cuore della **denominazione dinamica dei fogli di lavoro**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Come funziona

- **`RepeatWorksheet = true`** indica al motore di duplicare il foglio di origine per ogni elemento nella collezione `orders`. Questo soddisfa il requisito **come ripetere un foglio di lavoro**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** è una stringa modello dove `{OrderId}` è un segnaposto che SmartMarker sostituisce con l’ID dell’ordine corrente. È la risposta a **come denominare i fogli di lavoro** e alla **denominazione dinamica dei fogli di lavoro**.
- Il processore unisce i campi di ogni ordine (`{{OrderId}}`, `{{Customer}}`, ecc.) nel foglio duplicato, producendo una fattura completamente compilata.

---

## Passo 4: Esegui l’applicazione e verifica l’output

Compila ed esegui la console app:

```bash
dotnet run
```

Dovresti vedere il messaggio di successo nella console. Apri `GeneratedInvoices.xlsx` e troverai tre schede:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Ogni foglio contiene i dati dell’ordine sostituiti nei segnaposto. Il layout progettato nel modello è preservato, dimostrando che **automatizzare la generazione di fatture** funziona end‑to‑end.

### Screenshot previsto (testo alternativo per SEO)

![esempio di automazione della generazione di fatture che mostra tre fogli di lavoro denominati dinamicamente](/images/invoice-automation.png)

> *Il testo alternativo dell’immagine include la parola chiave principale per soddisfare la SEO.*

---

## Passo 5: Casi limite e variazioni comuni

### E se un OrderId contiene caratteri non consentiti?

I nomi dei fogli Excel non possono contenere `\ / ? * [ ] :`. Se i tuoi ID potrebbero includere questi caratteri, sanitizzali:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Aggiungi una proprietà calcolata a `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### È necessario mantenere il foglio modello originale?

Imposta `smartMarkerOptions.RemoveTemplate = false;` (il valore predefinito è `true`). In questo modo il foglio `InvoiceTemplate` originale rimane intatto come riferimento.

### Vuoi raggruppare le fatture per cliente?

Puoi annidare **gruppi di ripetizione**. Prima ripeti per cliente, poi per gli ordini all’interno di ogni foglio cliente. La sintassi diventa un po’ più complessa, ma il principio resta lo stesso—usa `RepeatWorksheet` e un modello di denominazione che rifletta la gerarchia.

---

## Esempio completo funzionante (tutto il codice in un unico posto)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copia‑incolla questo in `Program.cs`, posiziona `InvoiceTemplate.xlsx` accanto e sei pronto per partire.

---

## Domande frequenti

**D: Questo approccio funziona con grandi volumi di dati (migliaia di fatture)?**  
R: Sì. SmartMarker trasmette i dati in streaming in modo efficiente, ma tieni d’occhio l’utilizzo della memoria. Se raggiungi limiti, considera di elaborare in batch e scrivere ogni batch in una cartella di lavoro separata.

**D: Posso aggiungere un logo a ogni fattura automaticamente?**  
R: Assolutamente. Inserisci l’immagine del logo nel foglio modello. Poiché il foglio viene duplicato, il logo appare in ogni fattura generata senza codice aggiuntivo.

**D: E se devo proteggere i fogli di lavoro?**  
R: Dopo l’elaborazione, itera su `wb.Worksheets` e chiama `ws.Protect(Password, ProtectionType.All)`.

---

## Conclusione

Abbiamo appena **automatizzato la generazione di fatture** sfruttando la funzionalità di ripetizione dei fogli di SmartMarker e un modello di denominazione intelligente. Il tutorial ha coperto **come denominare i fogli di lavoro**, dimostrato **come ripetere un foglio di lavoro** per ogni ordine e mostrato **denominazione dinamica dei fogli di lavoro** per mantenere la cartella di lavoro ordinata e ricercabile.  

Dall’estrazione dei dati, alla configurazione del modello, alla configurazione di `SmartMarkerOptions` e alla gestione dei casi limite, ora disponi di una soluzione completa e pronta all’uso. Prossimo passo: aggiungi tabelle di dettaglio, applica formattazione condizionale o esporta gli stessi dati in PDF per una pipeline di fatturazione totalmente automatizzata.

Pronto a fare il salto di livello? Esplora argomenti correlati come “esportazione massiva di Excel con Aspose.Cells”, “conversione PDF dei fogli di lavoro” o “invio di fatture generate via email direttamente da C#”. Il cielo è il limite—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}