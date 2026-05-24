---
category: general
date: 2026-05-23
description: Come analizzare la data da una cella Excel usando C#. Impara i trucchi
  dei formati numerici personalizzati di Excel, leggi la data dalla cella e applica
  un formato personalizzato per risultati accurati.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: it
og_description: Come analizzare la data da una cella Excel usando C#. Questo tutorial
  mostra come applicare un formato numerico personalizzato in Excel, leggere la data
  dalla cella e formattare correttamente la data della cella Excel.
og_title: Come analizzare le date in Excel con C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Come analizzare le date in Excel con C# – Guida completa
url: /it/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come analizzare le date in Excel con C# – Guida completa

Ti sei mai chiesto **come analizzare una data** memorizzata in un foglio Excel senza dover manipolare manualmente le conversioni di stringa? Non sei l'unico. Che tu stia estraendo date fiscali giapponesi, combinazioni mese‑giorno europee, o qualsiasi stringa specifica di locale, ottenere un `DateTime` affidabile in C# può sembrare inseguire un bersaglio in movimento.  

In questo tutorial percorreremo un esempio concreto, end‑to‑end, che **applica un formato numerico personalizzato di Excel** a una cella di testo, poi **legge la data dalla cella** come un corretto `DateTime`. Alla fine saprai esattamente come **formattare la data di una cella Excel**, **applicare un formato personalizzato**, ed evitare le insidie comuni che ostacolano la maggior parte degli sviluppatori.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona con .NET Core, .NET Framework e .NET 5+)
- Un riferimento a una libreria per fogli di calcolo che supporti la manipolazione degli stili – l'esempio utilizza **Aspose.Cells**, ma i concetti si applicano a EPPlus, ClosedXML o NPOI.
- Conoscenze di base di C# (ce la fai, vero?)

> **Consiglio professionale:** Se non hai ancora Aspose.Cells, puoi scaricare una versione di prova gratuita dal loro sito e aggiungerla tramite NuGet: `dotnet add package Aspose.Cells`.

## Panoramica della soluzione

1. **Crea una cartella di lavoro** e individua la prima cella del primo foglio di lavoro.  
2. **Inserisci una stringa di data specifica per locale** (giapponese nel nostro caso).  
3. **Applica un formato numerico personalizzato** che indica a Excel di trattare la stringa come una data.  
4. **Leggi il valore della cella** come oggetto `DateTime`.  

Questo è l'intero flusso – nessuna analisi manuale, nessuna acrobazia con `DateTime.ParseExact`. Immergiamoci.

---

## Passo 1: Configurare la cartella di lavoro e la cella target

Per prima cosa, crea una nuova cartella di lavoro e prendi la cella con cui lavoreremo. Questo rispecchia lo scenario “nuova cartella di lavoro” da cui la maggior parte dei processi batch parte.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Perché è importante:** Inizializzare la cartella di lavoro programmaticamente garantisce il controllo su ogni aspetto del file – nessuna sorpresa di formattazione nascosta. L'oggetto `Cell` è il nostro punto di ingresso sia per il contenuto che per lo stile.

---

## Passo 2: Inserire una stringa di data giapponese

Excel spesso riceve le date come testo semplice, specialmente quando i dati provengono da sistemi legacy. Qui simuliamo questo inserendo direttamente una data dell'era giapponese nella cella.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Nota caso limite:** Se la cella contiene già una vera data Excel (un numero seriale), potresti saltare il passaggio del formato personalizzato. Questa guida si concentra sul percorso di conversione *testo‑a‑data*.

---

## Passo 3: Applicare un formato numerico personalizzato che interpreta il testo come data

Ora arriva la magia: diciamo a Excel di trattare la stringa usando un modello **custom number format Excel** che rispetti il locale giapponese. La stringa di formato `[$-ja-JP]yyyy` estrae la componente dell'anno, ma puoi estenderla a mese e giorno secondo necessità.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Perché funziona un formato personalizzato

Excel memorizza internamente le date come numeri seriali. Applicando un formato sensibile al locale, Excel tenta di *interpretare* il testo sottostante secondo il modello. Il prefisso `[$-ja-JP]` impone le regole del calendario giapponese, mentre il resto del modello mappa i caratteri a anno, mese e giorno.

> **Alternativa:** Se ti serve un approccio più generico, potresti usare `[$-en-US]mm/dd/yyyy` per le date in stile USA, o qualsiasi altro codice culturale supportato da Windows.

---

## Passo 4: Recuperare la data analizzata come oggetto `DateTime`

Infine, chiediamo alla cella il suo `DateTimeValue`. Aspose.Cells converte automaticamente il testo formattato in una corretta istanza `DateTime`.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Output console previsto**

```
Parsed date: 2021-05-12
```

> **Cosa succede se restituisce `DateTime.MinValue`?** Questo di solito indica che il formato non corrisponde al contenuto della cella. Ricontrolla la stringa del formato personalizzato e assicurati che il codice locale corrisponda alla lingua di origine.

---

## Bonus: Gestire altri locali e variazioni del mondo reale

### 1. Analizzare date europee (es., “12/05/2021” in francese)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Quando la cella contiene già una data seriale

Se il file Excel di origine contiene già un valore di data reale, puoi saltare completamente il formato personalizzato:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Ricorso al parsing manuale

A volte i dati sono disordinati (spazi extra, caratteri nascosti). Un ricorso sicuro è:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Ma l'approccio **apply custom format** è solitamente più veloce e meno soggetto a errori perché sfrutta il motore di parsing interno di Excel.

---

## Problemi comuni e come evitarli

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| Codice locale errato (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` rimane a `1/1/1900` | Verifica la stringa LCID esatta; usa `CultureInfo.GetCultureInfo("ja-JP").LCID` per sicurezza. |
| Mancano le virgolette intorno al testo statico | Excel tratta `"年"` come segnaposto di formato e fallisce | Racchiudi i caratteri statici tra virgolette doppie, ad esempio `\"年\"`. |
| La cella è già formattata come *Testo* | Formato personalizzato ignorato | Cancella prima il `NumberFormat` della cella: `firstCell.SetStyle(workbook.CreateStyle());` |
| Uso di una libreria che non supporta la proprietà `Custom` | Errore di compilazione | Passa a una libreria che espone formati numerici personalizzati (Aspose.Cells, EPPlus, ClosedXML). |

---

## Esempio completo (pronto per copia‑incolla)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Esegui il programma, apri `ParsedDateExample.xlsx`, e vedrai la cella **A1** visualizzare `2021年5月12日` mentre il valore sottostante è una data Excel corretta.

---

## Conclusione

Abbiamo coperto **come analizzare le stringhe di data** in Excel usando C# tramite **applying a custom number format Excel** e poi **reading date from cell** come un `DateTime` nativo. I punti chiave:

- Usa un formato personalizzato sensibile al locale (`[$-ja-JP]…`) per far fare a Excel il lavoro pesante.  
- Accedi a `Cell.DateTimeValue` per ottenere un `DateTime` pulito senza parsing manuale.  
- Adatta la stringa di formato per altre culture e verifica sempre con un rapido dump della console.  

Da qui puoi **format Excel cell date** per i report, inserire il `DateTime` nei database, o eseguire calcoli direttamente nella tua app C#. Sperimenta con diversi locali, combina più celle, o anche processa in batch interi fogli – gli stessi principi valgono.

Hai un formato di data strano che non riesci a decifrare? Lascia un commento e lo risolveremo insieme. Buon coding!

## Tutorial correlati

- [Formattazione personalizzata di numeri e date in Excel](/cells/english/net/excel-custom-number-date-formatting/)
- [Padroneggiare la presentazione dei dati in Excel: formattazione di numeri e date personalizzate con Aspose.Cells per Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Formattazione personalizzata di numeri e date in Excel](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}