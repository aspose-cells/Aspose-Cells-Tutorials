---
category: general
date: 2026-06-30
description: Crea formattazione condizionale in una cartella di lavoro Excel usando
  Aspose.Cells. Scopri come impostare lo sfondo delle celle, classificare le celle
  e generare il file programmaticamente.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: it
og_description: Crea formattazione condizionale in una cartella di lavoro Excel utilizzando
  Aspose.Cells. Segui questo tutorial completo per impostare lo sfondo delle celle,
  classificare le celle e automatizzare Excel.
og_title: Crea formattazione condizionale in Excel con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crea formattazione condizionale in Excel con Aspose.Cells – Guida passo passo
url: /it/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Formattazione Condizionale in Excel con Aspose.Cells – Guida Passo‑Passo

Ti sei mai chiesto come **creare formattazione condizionale** in un file Excel senza aprire l'interfaccia? Non sei solo. Molti sviluppatori hanno bisogno di **creare excel workbook** al volo, e farlo programmaticamente fa risparmiare ore di lavoro manuale. In questo tutorial ti mostreremo esattamente come **creare formattazione condizionale**, formattare le celle e persino classificare i valori più alti—tutto con la potente libreria Aspose.Cells per .NET.

Passeremo in rassegna un esempio reale: generare una tabella dei punteggi, evidenziare i punteggi alti in verde chiaro e applicare uno sfondo dorato ai primi 3 partecipanti. Alla fine saprai **come impostare lo sfondo delle celle**, **come classificare le celle** e **come usare Aspose** per un'automazione Excel sofisticata. Niente superfluo, solo una soluzione completa e eseguibile che puoi inserire in qualsiasi progetto C#.

## Cosa Imparerai

- Come **creare excel workbook** usando Aspose.Cells  
- Come riempire un intervallo con dati casuali (punteggi)  
- Come **impostare lo sfondo delle celle** con colori solidi  
- Come applicare una regola basata su formula per **classificare le celle** e evidenziare le prime tre  
- Come salvare il risultato come file .xlsx  

Prerequisiti: .NET 6+ (o .NET Framework 4.6+), Visual Studio (o qualsiasi IDE C#), e un riferimento al pacchetto NuGet Aspose.Cells. Se non hai mai usato Aspose prima, non preoccuparti—copriremo **come usare Aspose** da zero.

![Esempio di formattazione condizionale](https://example.com/images/create-conditional-formatting.png "Screenshot che mostra la formattazione condizionale nel file Excel generato")

*Testo alternativo dell'immagine: esempio di formattazione condizionale in un workbook Excel generato con Aspose.Cells.*

## Come Creare un Workbook Excel con Aspose.Cells

Prima di tutto: ti serve un oggetto workbook con cui lavorare. Aspose.Cells lo rende possibile con una sola riga.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Perché rinominiamo il foglio? Un nome chiaro (come **Scores**) lo rende più facile da riferire in seguito, soprattutto quando condividi il file con utenti non tecnici.  

Ora che il workbook esiste, riempiamo la colonna A con punteggi casuali.

## Come Riempire i Dati – Creare Punteggi Casuali

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Una rapida nota: `PutValue` rileva automaticamente il tipo di dato, quindi non è necessario fare cast a `int`. Il ciclo inizia da `i = 0` ma scrive nella riga `i + 1` perché le righe di Excel partono da 1 mentre la collezione `Cells` parte da 0.

## Come Impostare lo Sfondo delle Celle per Punteggi Alti

Ora **creeremo una formattazione condizionale** che colora qualsiasi punteggio ≥ 80 con una tonalità verde chiaro.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

La proprietà `ForegroundColor` controlla il colore di riempimento, mentre `Pattern = BackgroundType.Solid` indica a Excel di usare un riempimento solido anziché un gradiente o un motivo. Questo è il fulcro di **come impostare lo sfondo delle celle** in base a una soglia numerica.

## Come Classificare le Celle e Evidenziare le Prime 3

La classificazione è un po' più complessa perché serve una formula che valuti ogni cella rispetto all'intero intervallo. Aspose.Cells ti permette di usare la stessa sintassi delle formule di Excel che inseriresti nell'interfaccia.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Perché `A2` nella formula? Aspose valuta la formula in modo relativo a ciascuna cella dell'intervallo, quindi `A2` si sposta automaticamente a `A3`, `A4`, ecc., man mano che la regola viene applicata riga per riga. La funzione `RANK` restituisce la posizione di un valore all'interno dell'intervallo specificato, e la parte `<=3` garantisce che solo i tre punteggi più alti ricevano il riempimento dorato.

## Come Salvare il Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo a cui la tua applicazione può scrivere. Dopo aver eseguito il metodo, apri il file in Excel e vedrai:

- Celle verde chiaro per qualsiasi punteggio ≥ 80  
- Celle dorate per i tre punteggi più alti, indipendentemente dal fatto che siano anche ≥ 80  

Questo è l'intero pipeline di **creazione della formattazione condizionale**.

## Esempio Completo, Eseguibile

Ecco di nuovo l'intero metodo, pronto per essere copiato‑incollato in un'app console o in qualsiasi classe C#:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Risultato Atteso

Quando apri `Scores_ConditionalFormatting.xlsx`:

- Celle con valori **80** o superiori si illuminano di verde chiaro.  
- I tre numeri più alti (anche se sono sotto 80) appaiono con uno sfondo **dorato**.  
- Tutte le altre celle mantengono lo sfondo bianco predefinito.

Questo indizio visivo indica immediatamente a un manager chi sono i migliori performer, senza alcun ordinamento manuale.

## Domande Frequenti & Casi Limite

**Cosa succede se ho bisogno di più di tre punteggi migliori?**  
Basta cambiare la parte `<=3` della formula in `<=5` (o qualsiasi numero tu desideri). La regola si adatterà automaticamente.

**Posso applicare più intervalli di formattazione?**  
Assolutamente. Chiama nuovamente `sheet.ConditionalFormattings.Add` con un intervallo diverso, poi aggiungi le condizioni a quel nuovo oggetto `ConditionalFormatting`.

**E per le versioni più vecchie di Excel?**  
Aspose.Cells salva di default nel formato moderno `.xlsx`, compatibile con Excel 2007 e successive. Se ti serve `.xls`, passa `SaveFormat.Excel97To2003` al metodo `Save`.

**C'è un impatto sulle prestazioni per fogli di grandi dimensioni?**  
La formattazione condizionale è memorizzata come metadati, quindi non influisce significativamente sulla dimensione del file. Tuttavia, generare centinaia di migliaia di righe può aumentare l'uso della memoria—considera l'elaborazione a lotti.

## Prossimi Passi

Ora che hai padroneggiato **come creare formattazione condizionale**, potresti voler esplorare:

- **Come creare grafici Excel** programmaticamente (un altro gioiello di Aspose.Cells)  
- **Come impostare lo sfondo delle celle** in base a valori di testo (es. “Pass/Fail”)  
- **Come usare Aspose.Cells per la convalida dei dati** e le liste a discesa  

Ognuno di questi argomenti si basa sugli stessi fondamenti appena appresi, così ti sentirai subito a tuo agio.

## Conclusione

Abbiamo appena attraversato un esempio completo, end‑to‑end, di come **creare formattazione condizionale** in un workbook Excel usando Aspose.Cells. Dall'inizializzazione del workbook, al riempimento dei dati, **impostare lo sfondo delle celle**, classificare i migliori performer, fino al salvataggio finale del file, ogni passaggio è stato trattato con sia **come classificare le celle** sia **come usare Aspose** in mente.  

Prova il codice, modifica le soglie e osserva quanto rapidamente puoi generare report curati per qualsiasi scenario aziendale. Hai una variante da condividere? Lascia un commento qui sotto—buon coding!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Automatizzare la Formattazione Condizionale di Excel con Aspose.Cells per Java&#58; Guida Completa](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Come Creare & Formattare Celle Excel con Aspose.Cells per Java&#58; Guida Passo‑Passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Creare un Workbook Excel usando Aspose.Cells in Java&#58; Guida Passo‑Passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}