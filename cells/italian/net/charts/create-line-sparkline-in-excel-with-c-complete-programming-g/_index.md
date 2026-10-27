---
category: general
date: 2026-06-30
description: Crea una sparkline a linee in Excel con C# rapidamente. Scopri come aggiungere
  una sparkline, creare una cartella di lavoro Excel con C# e aggiungere la sparkline
  a una cella in pochi passaggi.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: it
og_description: Crea sparkline a linee in Excel con C#. Questo tutorial mostra come
  aggiungere una sparkline, creare una cartella di lavoro Excel con C# e incorporare
  la sparkline in una cella.
og_title: Crea sparkline a linee in Excel con C# – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crea sparkline a linee in Excel con C# – Guida completa alla programmazione
url: /it/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea sparkline a linea in Excel con C# – Guida completa di programmazione

Ti sei mai chiesto come **creare sparkline a linea** in un file Excel usando C#? Non sei l’unico—gli sviluppatori chiedono continuamente, “come aggiungo una sparkline a un report senza aprire Excel manualmente?” La buona notizia è che con poche righe di codice puoi generare una elegante sparkline a linea direttamente nella cartella di lavoro, senza interfaccia utente.

In questo tutorial percorreremo tutto ciò che devi sapere: dalle basi di **create Excel workbook C#**, al popolamento dei dati, fino ai passaggi esatti per **add line sparkline** e **add sparkline to cell**. Alla fine avrai un file *.xlsx* pronto all'uso che visualizza le tendenze di vendita mensili a colpo d'occhio. Niente superfluo, solo una soluzione pratica e eseguibile.

---

## Cosa costruirai

- Un nuovo workbook Excel chiamato *KPI_Sparklines.xlsx*  
- Un foglio di lavoro chiamato **KPI** contenente numeri di vendita di esempio  
- Una **line sparkline** posizionata nella cella **D2** che fa riferimento all'intervallo di dati **B2:B13**  
- Formattazione di base (colore, spessore della linea) per far risaltare la sparkline  

Prerequisiti? Solo il .NET SDK (3.1+ o .NET 6) e la libreria gratuita Aspose.Cells per .NET (disponibile via NuGet). Se non hai mai usato Aspose.Cells, pensala come un potente motore Excel che puoi chiamare dal codice—senza interop COM, senza necessità di installare Excel.

![Crea sparkline a linea in Excel usando C#](https://example.com/images/create-line-sparkline.png "Crea sparkline a linea in Excel con C#")

*Testo alternativo immagine: esempio di codice per creare sparkline a linea in Excel usando C#*

## Passo 1: **Create Excel workbook C#** – Configura il file e il foglio di lavoro

Prima di tutto. Abbiamo bisogno di un oggetto workbook e di un foglio di lavoro dove risiederanno i dati. Questa è la base per qualsiasi automazione Excel, sia che tu aggiunga successivamente **add line sparkline** o scriva formule.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Perché è importante:** La classe `Workbook` rappresenta l'intero file, mentre `Worksheet` è la tela per righe, colonne e, eventualmente, la nostra sparkline. Dare un nome al foglio fin dall'inizio mantiene il file ordinato e auto‑documentante.

## Passo 2: Popola i dati – L'intervallo di origine per la sparkline

Una sparkline ha bisogno di dati da tracciare. Simuliamo 12 mesi di fatturato. Potresti prelevarli da un database, ma per chiarezza li genereremo al volo.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Suggerimento:** `PutValue` rileva automaticamente il tipo di dato, quindi non è necessario fare cast a `double` o `int`. Se mai dovessi formattare le celle (valuta, separatori delle migliaia), puoi applicare un oggetto `Style` in seguito.

## Passo 3: **Create line sparkline** – Aggiungi la sparkline a una cella specifica

Ora arriva la star dello spettacolo: la **line sparkline**. Aspose.Cells raggruppa le sparklines, quindi creiamo prima un `SparklineGroup` di tipo `Line`, poi indichiamo dove posizionare l'elemento visivo.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Come funziona:**  
> - `firstRow/firstColumn` e `lastRow/lastColumn` definiscono la *cella di destinazione* (dove appare la sparkline).  
> - `firstDataRow/lastDataRow` indicano l'intervallo di origine.  
> Poiché stiamo usando una **line sparkline**, l'elemento visivo sarà una semplice linea sottile che segue l'andamento dei numeri.

### Opzionale: **How to add sparkline** con stile personalizzato

Se vuoi che la sparkline risalti, regola un paio di proprietà:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Perché stilizzarla?** Una linea blu scura su sfondo bianco è facile per gli occhi, mentre i marcatori forniscono un'indicazione rapida sui singoli punti dati—utile per le presentazioni.

## Passo 4: Salva il workbook – Verifica il risultato

Con la sparkline al suo posto, dobbiamo solo scrivere il file su disco. Scegli una cartella a cui hai accesso in scrittura; l'esempio usa un percorso segnaposto che dovrai sostituire.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Verifica:** Apri il file generato in Excel (o in qualsiasi visualizzatore che supporti .xlsx). Dovresti vedere una **line sparkline** nella cella **D2** che rispecchia i numeri di vendita in crescita nella colonna **B**. Passando il mouse sopra la sparkline verrà mostrato un tooltip con i valori sottostanti.

## Passo 5: Problemi comuni quando **add sparkline to cell**

Anche un esempio semplice può creare difficoltà ai principianti. Ecco alcune cose a cui fare attenzione:

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Coordinate della cella errate | L'obiettivo della sparkline usa l'indice di colonna basato su zero ma l'indice di riga basato su uno. | Ricorda `Cells[row, column]` dove `row` è basato su zero, `column` è anch'esso basato su zero. In `SparklineGroup.Add`, righe e colonne sono **basate su 1**. |
| Nessun dato visualizzato | L'intervallo di origine è vuoto o contiene valori non numerici. | Assicurati che l'intervallo (ad es., `B2:B13`) contenga numeri. Usa `PutValue` con tipi numerici. |
| La sparkline scompare dopo il salvataggio | Incompatibilità di versione della libreria o licenza mancante. | Usa l'ultima versione del pacchetto Aspose.Cells e fornisci una licenza valida se superi i limiti di valutazione. |
| Formattazione non applicata | Le modifiche di stile sono state fatte prima di aggiungere la sparkline. | Imposta lo stile **dopo** aver creato il gruppo, come mostrato sopra. |

## Codice sorgente completo – Copia‑incolla tutto in una volta

Di seguito trovi il programma completo, pronto per l'esecuzione. Incollalo in un nuovo progetto console, aggiungi il pacchetto NuGet Aspose.Cells e premi **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Output previsto:** Quando apri *KPI_Sparklines.xlsx*, la colonna **B** elenca dodici numeri (5.000 → 13.250) e la cella **D2** contiene una morbida sparkline a linea blu scura che sale costantemente. I marcatori appaiono come piccoli punti arancione‑rossi se hai abilitato `ShowMarkers`.

## Cosa segue? Estendere le tue competenze sulle Sparkline

Ora che hai padroneggiato **create line sparkline** con Aspose.Cells, considera di esplorare questi argomenti correlati:

- **Add column sparkline** – perfetta per mostrare dati impilati.  
- **Create multi‑sparkline groups** sullo stesso foglio per confronti affiancati.  
- **Export to PDF** mantenendo le sparklines (Aspose.Cells supporta la conversione in PDF).  
- **Dynamic data sources** – estrai i dati di vendita reali da un database SQL invece di valori hard‑coded.  

Ognuno di questi si basa sugli stessi concetti fondamentali: **create Excel workbook C#**, popolamento dei dati e **add sparkline to cell** nello stile desiderato.

### TL;DR

Abbiamo mostrato come **create line sparkline** in un workbook Excel usando C#. I passaggi—*create workbook, fill data, add sparkline, style it, and save*—sono tutti racchiusi in un unico programma autonomo. Sentiti libero di modificare i colori, lo spessore della linea o l'intervallo di origine per adattarli alle tue esigenze di reporting.

Hai un'idea da condividere? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Automazione Excel: Crea un Workbook e aggiungi una ListBox usando Aspose.Cells per .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automazione Excel: Crea Workbook e aggiungi Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automazione Excel: Crea Workbook e aggiungi Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}