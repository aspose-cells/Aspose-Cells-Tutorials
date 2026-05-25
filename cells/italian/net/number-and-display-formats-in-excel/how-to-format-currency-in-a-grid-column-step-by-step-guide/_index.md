---
category: general
date: 2026-02-15
description: Come formattare rapidamente la valuta usando Set Column Number Format
  e applicare un formato numerico personalizzato in C#. Impara a recuperare la colonna
  per nome e impostare l’allineamento della colonna nella griglia.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: it
og_description: come formattare la valuta in una colonna di una griglia usando C#.
  Questo tutorial mostra come recuperare la colonna per nome, impostare il formato
  numerico della colonna, applicare un formato numerico personalizzato e impostare
  l'allineamento della colonna della griglia.
og_title: Come formattare la valuta in una colonna della griglia – Guida completa
tags:
- C#
- GridFormatting
- UI
title: Come formattare la valuta in una colonna della griglia – Guida passo‑passo
url: /it/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to format currency in a Grid Column – Complete Programming Tutorial

Ti sei mai chiesto **come formattare una valuta** in una colonna di una griglia senza impazzire? Non sei l'unico. Quando guardi un numero semplice come `1234.5` e desideri che appaia magicamente come `$1,234.50`, la risposta è solitamente solo qualche riga di configurazione.  

In questa guida **recupereremo la colonna per nome**, **imposteremo il formato numerico della colonna** e **applicheremo un formato numerico personalizzato** che rispetta il layout contabile tipico. Lungo il percorso imposteremo anche **l’allineamento della colonna della griglia** e aggiungeremo un sottile bordo affinché l’interfaccia abbia un aspetto curato.

> **TL;DR** – Alla fine avrai uno snippet pronto all’uso che trasforma i decimali grezzi in valori di valuta splendidamente formattati all’interno di qualsiasi controllo in stile `GridJs`.

---

## What You’ll Need

- Un progetto .NET (qualsiasi versione che supporti C# 8.0+ – Visual Studio 2022 funziona benissimo).  
- Un componente griglia che esponga una collezione `Columns` (l’esempio utilizza una classe fittizia `GridJs`, ma i concetti si applicano a griglie DevExpress, Telerik o Syncfusion).  
- Familiarità di base con la sintassi C# – non servono trucchi avanzati.

Se hai già tutto questo, ottimo. Altrimenti, crea una semplice applicazione console; la griglia può essere simulata a scopo illustrativo.

---

## Step‑by‑Step Implementation

Di seguito ogni passo è accompagnato da un blocco di codice compatto, una breve spiegazione del **perché** della riga e un suggerimento per evitare le insidie più comuni.

### ## Step 1 – Recupera la colonna “Amount” per nome

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Perché è importante:**  
La maggior parte delle API delle griglie espone le colonne tramite un indicizzatore simile a un dizionario. Recuperare la colonna tramite il suo nome di intestazione (`"Amount"`) ti consente di manipolarne l’aspetto senza toccare la sorgente dati sottostante.  

**Consiglio professionale:** Controlla sempre che il risultato non sia `null` – un errore di battitura nel nome della colonna o una modifica dinamica dello schema può altrimenti generare una `NullReferenceException` a runtime.

---

### ## Step 2 – Imposta il formato numerico della colonna usando una maschera di valuta personalizzata

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Perché è importante:**  
La stringa di formato segue le convenzioni di formattazione contabile di Excel:

- `_(* #,##0.00_)` → Numeri positivi, allineati a destra con uno spazio iniziale per il simbolo di valuta.  
- `_(* (#,##0.00)` → Numeri negativi racchiusi tra parentesi.  
- `_(* \"-\"??_)` → Valori zero visualizzati come trattino.  
- `_(@_)` → I valori di testo rimangono invariati.

Utilizzare **apply custom numeric format** ti dà il pieno controllo su separatori delle migliaia, decimali e posizionamento del simbolo di valuta.  

**Caso limite:** Se la tua applicazione deve rispettare una locale diversa (ad es. Euro invece di USD), sostituisci lo spazio iniziale con il simbolo appropriato o usa la formattazione basata su `CultureInfo` nella sorgente dati.

---

### ## Step 3 – Allinea il contenuto della colonna a destra per una migliore leggibilità

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Perché è importante:**  
I valori monetari sono più facili da leggere quando sono allineati sul separatore decimale. Impostare **set grid column alignment** a `Right` replica il modo in cui i fogli di calcolo mostrano i dati finanziari.  

**Attenzione:** Alcune griglie ignorano l’allineamento su celle che contengono template personalizzati. Se noti che l’allineamento non ha effetto, verifica che la colonna non stia usando un renderer di cella personalizzato.

---

### ## Step 4 – Aggiungi un sottile bordo grigio attorno alle celle della colonna

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Perché è importante:**  
Un bordo discreto separa la colonna “Amount” dalle colonne vicine, specialmente quando la griglia utilizza colori di riga alternati. È un indizio visivo che i dati rappresentano una cifra finanziaria distinta.  

**Suggerimento:** Se ti serve una linea più spessa per la stampa, aumenta `BorderLineStyle` a `Medium` o cambia `Color` in `Color.Black`.

---

## Full Working Example

Ecco lo snippet completo che puoi inserire in un progetto WinForms o WPF che utilizza un controllo in stile `GridJs`. L’esempio stampa anche i valori formattati sulla console così puoi verificare l’output senza un’interfaccia grafica.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected console output**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Nota come il numero positivo è allineato a destra, quello negativo appare tra parentesi e lo zero mostra un trattino – esattamente ciò che la stringa di formato personalizzato prevede.

---

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the grid uses a different culture (e.g., € instead of $)?* | Sostituisci lo spazio iniziale nella stringa di formato con il simbolo desiderato oppure lascia che la sorgente dati emetta una stringa pre‑formattata usando `CultureInfo.CurrentCulture`. |
| *Can I reuse the same format for multiple columns?* | Assolutamente. Memorizza la stringa di formato in una costante (`const string CurrencyMask = "...";`) e assegnala ovunque ti serva la valuta. |
| *What happens if the column contains a string value?* | La stringa di formato influisce solo sui tipi numerici. Le stringhe passano inalterate, ed è per questo che esiste l’ultima parte della maschera (`_(@_)`) – preserva i contenuti non numerici. |
| *Is there a performance impact?* | Trascurabile. Il formato viene applicato al momento del rendering, non durante il recupero dei dati. A meno che tu non stia renderizzando migliaia di righe per frame, non noterai rallentamenti. |
| *How do I make the border thicker for printed reports?* | Sostituisci `BorderLineStyle.Thin` con `BorderLineStyle.Medium` o `BorderLineStyle.Thick`. Alcune librerie consentono anche di specificare direttamente una larghezza in pixel. |

---

## Wrap‑Up

Abbiamo percorso tutti i passaggi per **formattare una valuta** in una colonna di griglia dall’inizio alla fine: recuperare la colonna per nome, impostare il formato numerico, applicare un formato numerico personalizzato, allineare le celle e aggiungere un bordo elegante. L’esempio completo funziona subito e dimostra il risultato visivo esatto che puoi aspettarti.

Se sei pronto a spingerti oltre, prova:

- **Culture dinamiche** – cambia la stringa di formato in base alla locale dell’utente.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}