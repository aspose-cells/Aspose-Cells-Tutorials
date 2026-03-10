---
category: general
date: 2026-02-14
description: Crea rapidamente un modello di sconto e impara come applicare lo sconto
  in un foglio di calcolo, inserire i dati nel modello e definire il prefisso variabile
  per i marker intelligenti.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: it
og_description: Crea un modello di sconto con C#. Impara ad applicare lo sconto in
  un foglio di calcolo, inserire i dati nel modello e definire un prefisso variabile
  per i marker intelligenti.
og_title: Crea modello di sconto – Guida completa a C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Crea modello di sconto in C# – Guida passo‑a‑passo
url: /it/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

.

Make sure we preserve markdown headings (#). Also preserve bold formatting.

Also note "For Italian, ensure proper RTL formatting if needed" - not relevant.

Now produce final output with all translated text and unchanged shortcodes/code placeholders.

Let's construct final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Modello di Sconto – Guida Completa in C#

Hai mai avuto bisogno di **create discount template** per un report di vendite ma non eri sicuro di come inserire i numeri in un foglio di calcolo automaticamente? Non sei solo. In questo tutorial ti mostreremo esattamente come **create discount template**, poi **apply discount in spreadsheet** celle, **inject data into template**, e anche **define variable prefix** per i tuoi smart markers—tutto con codice C# pulito.

Inizieremo delineando il problema, poi passeremo direttamente a una soluzione funzionante che puoi copiare‑incollare. Alla fine avrai un modello riutilizzabile che funziona sia che tu stia generando fatture, listini prezzi, o qualsiasi foglio di calcolo che richieda sconti dinamici.

---

## Cosa Imparerai

- Come progettare un modello di foglio di calcolo consapevole degli sconti.
- Come configurare un `VariablePrefix` / `VariableSuffix` personalizzato in modo che i marker siano facili da individuare.
- Come passare un oggetto anonimo (`discountData`) al `SmartMarkerProcessor`.
- Come la formula risultante (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) calcola automaticamente il prezzo finale.
- Suggerimenti per gestire casi limite come righe con sconto zero o più livelli di sconto.

**Prerequisites** – un runtime .NET recente (≥ .NET 6), un riferimento alla libreria `Aspose.Cells` (o simile) che fornisce `SmartMarkerProcessor`, e una conoscenza di base della sintassi C#. Nulla di esotico.

---

## Passo 1: Crea un Modello di Sconto nel Tuo Foglio di Calcolo

Per prima cosa, apri una nuova cartella di lavoro (o usane una esistente) e inserisci un segnaposto dove verrà applicato lo sconto. Considera il modello come un semplice file Excel con “smart markers” che il processore sostituirà.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** Inserendo `#Discount#` all'interno della formula indichiamo al processore esattamente dove deve andare il valore dello sconto. Il `SmartMarkerProcessor` sostituirà `#Discount#` con il numero fornito in seguito, lasciando intatta il resto della formula.

---

## Passo 2: Definisci il Prefisso Variabile per gli Smart Markers

Di default, molte librerie cercano `${Variable}` o `{{Variable}}`. Nel nostro caso vogliamo un marker pulito e leggibile, quindi **define variable prefix** e il suffisso esplicitamente.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Usare `#` mantiene i marker brevi e facili da individuare nella barra della formula di Excel. Se mai dovessi evitare conflitti con le funzioni Excel esistenti, scegli una coppia diversa (ad esempio `[[` e `]]`).

---

## Passo 3: Inserisci Dati nel Modello Usando SmartMarkerProcessor

Ora forniamo il valore reale dello sconto. Il processore scansionerà il foglio di lavoro, troverà ogni `#Discount#` e lo sostituirà con il valore dell'oggetto anonimo che passiamo.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

After this call, the formula in `B2` becomes:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

When the workbook calculates, `B2` shows **90**, i.e., a 10 % discount applied to the original price of 100.

**Why it works:** `StartSmartMarkerProcessing` attraversa ogni cella, cerca il token `#Discount#` e sostituisce il valore numerico. Poiché il token è all'interno di una dichiarazione `IF`, il foglio di calcolo gestisce comunque i casi in cui lo sconto potrebbe essere zero.

---

## Passo 4: Applica lo Sconto nel Foglio di Calcolo – Verifica il Risultato

Attiviamo il calcolo e stampiamo il prezzo finale sulla console. Questo passo dimostra che il flusso di lavoro **apply discount in spreadsheet** è riuscito.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

Se cambi `discountData.Discount` a `0.25` e riesegui il processore, l'output rifletterà automaticamente uno sconto del 25 %—nessun codice aggiuntivo necessario.

---

## Passo 5: Gestione dei Casi Limite e Sconti Multipli

### Righe con Sconto Zero

A volte un prodotto non è in sconto. Per mantenere la formula robusta, l'`IF` inserito in precedenza copre già questo scenario: quando `#Discount#` è `0`, il prezzo originale passa invariato.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Colonne di Sconto Multiple

Se ti servono sconti separati per riga, assegna a ogni riga il proprio marker, ad esempio `#Discount1#`, `#Discount2#`, e passa una collezione:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Il processore corrisponde ai marker in modo sequenziale, quindi ogni riga ottiene il valore corretto.

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla, che incorpora tutti i passaggi sopra. Salvalo come `Program.cs`, aggiungi un riferimento a `Aspose.Cells` e esegui.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Eseguendo questo stampa i numeri attesi e produce un file `DiscountedPricing.xlsx` che puoi aprire in Excel per vedere la formula già risolta.

---

## Conclusione

Ora sai come **create discount template**, **apply discount in spreadsheet**, **inject data into template**, e **define variable prefix** per gli smart markers—tutto con poche linee concise di C#. Il modello è scalabile—basta cambiare l'oggetto anonimo o fornire una collezione per aggiornamenti in blocco, e lo stesso modello gestirà qualsiasi scenario di sconto tu gli proponga.

Pronto per il livello successivo? Prova:

- Aggiungere calcoli delle tasse insieme agli sconti.
- Recuperare le percentuali di sconto da un database invece di codificarle staticamente.
- Usare la formattazione condizionale per evidenziare le righe con sconti elevati.

Queste estensioni mantengono intatta l'idea di base ampliando l'utilità del tuo modello di sconto.

Hai domande o un caso d'uso interessante? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}