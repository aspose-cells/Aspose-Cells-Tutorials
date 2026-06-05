---
category: general
date: 2026-06-05
description: Abilita l'opzione intervallo annidato in Aspose.Cells SmartMarkerProcessor
  per gestire i dati Excel gerarchici senza sforzo. Scopri i smart marker, gli intervalli
  annidati e le migliori pratiche.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: it
og_description: Abilita l'opzione di intervallo annidato in Aspose.Cells SmartMarkerProcessor
  per lavorare con dati gerarchici. Guida completa con codice, consigli e insidie.
og_title: Abilita l'opzione Intervallo Annidato in Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Abilita l'opzione Intervallo annidato in Aspose.Cells SmartMarker
url: /it/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abilitare l'opzione Nested Range in Aspose.Cells SmartMarker

Ti sei mai chiesto come **abilitare l'opzione nested range** in Aspose.Cells SmartMarkerProcessor? Attivare questa funzionalità ti consente di lavorare con dati gerarchici come ordini e righe di dettaglio senza problemi.  

In questo tutorial percorreremo uno scenario reale: alimentare un elenco di ordini con elementi annidati in un modello Excel usando i smart marker. Alla fine avrai una cartella di lavoro completamente funzionante, comprenderai **SmartMarkerProcessor** e saprai perché il flag di **nested range handling** è importante.

Tratteremo:

* Preparare un oggetto anonimo C# che simula dati master‑detail.  
* Attivare il flag **nested range** sul processore.  
* Eseguire il processore su una cartella di lavoro e verificare il risultato.  

Nessun framework sofisticato richiesto—solo .NET 6+ e la libreria Aspose.Cells per .NET. Se hai mai avuto difficoltà con righe ripetute all'interno di altre righe ripetute, questa guida è per te.

---

## Preparare dati gerarchici per gli Smart Marker di Excel

Per prima cosa, ci serve una fonte dati che rifletta una relazione padre‑figlio. L'esempio qui sotto crea un oggetto anonimo con un ordine che contiene due elementi.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**Perché questa struttura?**  
Gli smart marker leggono i nomi delle proprietà (`Orders`, `Items`) e generano automaticamente nested range quando il processore è configurato correttamente. Pensalo come un mini‑database che il modello Excel itererà.

> **Consiglio esperto:** Usa nomi di proprietà significativi che corrispondano ai marker inseriti nel modello (ad es., `&=Orders.Id&`, `&=Items.Name&`). Nomi non corrispondenti sono una causa comune di errori “no data”.

---

## Configurare SmartMarkerProcessor e abilitare Nested Range

Ora creiamo il processore e attiviamo l'interruttore **NestedRange**. Questa singola riga dice ad Aspose.Cells di trattare le collezioni figlio come tabelle interne.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**Cosa fa realmente `NestedRange = true`?**  
Quando impostato, il processore costruisce un range separato per ogni collezione figlio e lo annida all'interno del range padre. Senza di esso, verrebbe renderizzata solo la collezione di livello superiore (`Orders`), e le righe interne di `Items` verrebbero ignorate.

> **Attenzione:** Se abiliti i nested range ma dimentichi di contrassegnare il range figlio nel modello (usando `&=Items.Start&` / `&=Items.End&`), il processore lancerà una `SmartMarkerException`. Controlla sempre la sintassi dei marker.

---

## Caricare o creare il modello di cartella di lavoro

Per la dimostrazione genereremo una semplice cartella di lavoro al volo, ma in produzione di solito si parte da un file `.xlsx` esistente che contiene già gli smart marker.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Nota i marker `&=Orders.Start&` / `&=Orders.End&`—questi indicano al processore dove inizia e finisce ogni blocco ordine. Lo stesso schema si applica al range figlio `Items`.

---

## Elaborare la cartella di lavoro con gli Smart Marker

Con i dati e il processore pronti, l'ultimo passo è una singola riga che unisce tutto.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

Dopo questa chiamata, la cartella di lavoro conterrà:

| ID Ordine | Nome Articolo |
|-----------|---------------|
| 1         | A             |
| 1         | B             |

Puoi salvare il risultato su disco o trasmetterlo a un client:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Verificare l'output e gestire le difficoltà comuni

### Risultato atteso

Apri `NestedRangeResult.xlsx` e dovresti vedere due righe sotto l'intestazione dell'unico ordine, ciascuna riga che mostra il nome dell'articolo (`A` e `B`). L'ID ordine si ripete per ogni riga figlio—esattamente ciò per cui i nested range sono stati progettati.

### Problemi tipici

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| Nessuna riga figlio appare | `NestedRange` lasciato a `false` | Imposta `processor.Options.NestedRange = true`. |
| I marker compaiono come testo semplice | Errore di sintassi del marker (`&=Orders.Start&` vs `&=Orders.Start`) | Assicurati che siano presenti sia `&=` sia il `&` finale. |
| Righe duplicate per ogni ordine | Mancanza del marker `&=Orders.End&` | Aggiungi il marker di chiusura per delimitare il range padre. |

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Esegui il programma, apri il file generato e vedrai le righe annidate popolate esattamente come mostrato nella tabella sopra.

---

## Conclusione

Hai appena imparato come **abilitare l'opzione nested range** in Aspose.Cells SmartMarkerProcessor, trasformando un modello Excel piatto in un potente generatore di report master‑detail. Attivando `processor.Options.NestedRange = true`, la libreria crea automaticamente tabelle interne per le collezioni figlio, risparmiandoti i cicli manuali di inserimento righe.

Cosa fare dopo? Prova ad aggiungere un secondo livello di annidamento (ad es., ordine → articoli → sotto‑componenti), sperimenta con lo stile delle righe generate, o passa a un modello pre‑progettato che includa grafici e formule. La combinazione **Excel smart markers** e **nested range handling** è una solida base per qualsiasi soluzione di reporting automatizzato.

Hai domande o uno scenario complesso? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi di implementazione nei tuoi progetti.

- [Gestire oggetti annidati con Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Popolare Excel con dati annidati usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Popolare Excel con dati annidati Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}