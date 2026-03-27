---
category: general
date: 2026-03-27
description: Come collegare i dati in C# usando Aspose.Cells – impara a salvare la
  cartella di lavoro come XLSX, aggiungere un grafico e esportare Excel con grafico
  in pochi minuti.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: it
og_description: Come collegare i dati in C# con Aspose.Cells. Questa guida ti mostra
  come salvare la cartella di lavoro come XLSX, aggiungere un grafico e esportare
  Excel con il grafico.
og_title: Come collegare i dati in C# – Creare una cartella di lavoro Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Come associare i dati in C# – Creare una cartella di lavoro Excel
url: /it/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come collegare i dati in C# – Creare una cartella di lavoro Excel

Ti sei mai chiesto **come collegare i dati** a un grafico in C# senza impazzire? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando devono generare programmaticamente file Excel che *sembrino* quelli creati manualmente.  

In questo tutorial percorreremo un esempio completo, pronto all'uso, che crea una cartella di lavoro Excel, la popola con dati, collega quei dati a un grafico Waterfall e infine salva il file come `.xlsx`. Alla fine saprai esattamente **come salvare una cartella di lavoro come XLSX**, **come aggiungere un grafico** a un foglio di lavoro e **come esportare Excel con grafico** per reportistica downstream.

> **Prerequisiti** – Hai bisogno di Aspose.Cells per .NET (la versione di prova gratuita va benissimo) e di un ambiente di sviluppo .NET come Visual Studio 2022. Non sono necessari altri pacchetti NuGet.

---

## Cosa copre questa guida

- **Create Excel workbook C#** – crea un nuovo `Workbook` e un foglio di lavoro.  
- **How to bind data** – mappa le tue serie numeriche e le etichette di categoria alla sorgente dati del grafico.  
- **How to add chart** – inserisci un grafico Waterfall e configura il suo titolo.  
- **Save workbook as XLSX** – persisti il file su disco così che chiunque possa aprirlo in Excel.  
- **Export Excel with chart** – il prodotto finale è una cartella di lavoro pienamente funzionale che puoi condividere.

Se hai dimestichezza con la sintassi base di C#, troverai tutto molto semplice. Iniziamo.

---

## Passo 1: Creare una cartella di lavoro Excel in C#  

Prima di tutto – abbiamo bisogno di un oggetto workbook con cui lavorare. Pensa alla classe `Workbook` come a un quaderno vuoto che riempirai più tardi con pagine (worksheet) e contenuti.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Suggerimento professionale:** Se ti servono più fogli, chiama semplicemente `workbook.Worksheets.Add()` e conserva un riferimento a ciascun nuovo `Worksheet`.

---

## Passo 2: Popolare il foglio con categorie e valori  

Ora **creeremo dati in stile excel workbook c#**. L'esempio utilizza uno scenario classico di Waterfall: start, revenue, cost, profit e end.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Perché inseriamo `0` per “Start” e “Profit”? In un grafico Waterfall quegli zero fungono da *connettori* che fanno fluire correttamente la visualizzazione. Se li ometti, il grafico apparirà interrotto.

---

## Passo 3: How to Add Chart – Inserire un grafico Waterfall  

Con i dati al loro posto, è il momento di **how to add chart**. Aspose.Cells rende tutto semplice come chiamare `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Le coordinate `(7,0,25,10)` definiscono la cella in alto a sinistra e quella in basso a destra del riquadro del grafico. Modificale per adattarle al tuo layout.

---

## Passo 4: How to Bind Data – Collegare serie e categorie  

Ecco il cuore del tutorial: **how to bind data** al grafico. Il metodo `NSeries.Add` accetta l’intervallo dei valori Y, mentre `CategoryData` punta alle etichette dell’asse X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Nota che facciamo riferimento alle stesse celle riempite in precedenza (`A2:A6` per le categorie, `B2:B6` per gli importi). Se cambi la disposizione dei dati, aggiorna semplicemente questi intervalli.

---

## Passo 5: Save Workbook as XLSX – Persistire il file  

Infine, **salviamo la cartella di lavoro come XLSX**. Il metodo `Save` sceglie automaticamente il formato corretto in base all’estensione del file.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Quando apri `WaterfallChart.xlsx` in Excel vedrai un grafico Waterfall ben renderizzato che rispecchia i dati inseriti. Questa è la parte **export excel with chart** completata.

---

## Risultato atteso  

- **File Excel:** `WaterfallChart.xlsx` nella cartella che hai specificato.  
- **Disposizione del foglio:** la colonna A contiene le categorie, la colonna B gli importi, e il grafico è posizionato sotto la tabella.  
- **Aspetto del grafico:** Un grafico Waterfall intitolato “Quarterly Waterfall” con cinque colonne che rappresentano Start, Revenue, Cost, Profit e End.  

![come collegare i dati al grafico a cascata esempio](waterfall_chart.png "Grafico Waterfall generato da Aspose.Cells")

*Il testo alternativo dell’immagine include la parola chiave principale, aiutando sia la SEO sia la citazione da parte dell’AI.*

---

## Domande frequenti & casi particolari  

### E se la mia sorgente dati è dinamica?  
Sostituisci gli array statici con un ciclo che legge da un database o da un'API. Finché scrivi i valori nello stesso intervallo di celle, il codice di binding rimane invariato.

### Posso cambiare il tipo di grafico?  
Assolutamente. Sostituisci `ChartType.Waterfall` con `ChartType.Column`, `ChartType.Line`, ecc. Ricorda solo di adeguare i dati della serie se il nuovo grafico richiede una disposizione diversa.

### Come impostare i colori del grafico?  
Usa `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (o qualsiasi `System.Drawing.Color`). È utile quando vuoi far risaltare la colonna “Profit”.

### E se devo esportare in PDF invece di XLSX?  
Chiama `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Il grafico verrà renderizzato automaticamente nel PDF.

---

## Consigli per un codice pronto per la produzione  

- **Dispose degli oggetti** – Avvolgi `Workbook` in un blocco `using` se usi .NET Core per liberare le risorse tempestivamente.  
- **Gestione dei percorsi** – Usa `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` per evitare di hard‑codare i separatori.  
- **Gestione degli errori** – Cattura `Exception` attorno a `Save` per segnalare subito problemi di permessi o spazio su disco.  
- **Controllo versione** – Aspose.Cells 23.10+ ha introdotto un supporto Waterfall migliorato; assicurati di usare una versione recente per i migliori risultati.

---

## Conclusione  

Ora disponi di un esempio completo, end‑to‑end, che dimostra **how to bind data** in C#, **create excel workbook c#**, **how to add chart**, **save workbook as xlsx** e **export excel with chart**. Il codice è pronto per essere inserito in qualsiasi progetto .NET, e i concetti si scalano a set di dati più grandi e a diversi tipi di grafico.

Pronto per il passo successivo? Prova ad aggiungere più serie, sperimenta con grafici impilati o automatizza la generazione di report mensili da inviare via email ai stakeholder. Il cielo è il limite una volta che avrai padroneggiato le basi dell’automazione Excel con Aspose.Cells.

Buona programmazione, e che i tuoi fogli di calcolo vengano sempre renderizzati perfettamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}