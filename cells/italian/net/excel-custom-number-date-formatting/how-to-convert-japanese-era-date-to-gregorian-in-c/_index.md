---
category: general
date: 2026-10-01
description: Converti la data dell'era giapponese in un DateTime gregoriano usando
  Aspose.Cells in C#. Scopri come convertire rapidamente il calendario giapponese.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: it
lastmod: 2026-10-01
og_description: Converti la data dell'era giapponese in un DateTime gregoriano in
  C#. Questo tutorial spiega come convertire accuratamente il calendario giapponese
  con Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Converti la data dell'era giapponese in gregoriano in C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Come convertire una data dell'era giapponese nel calendario gregoriano in C#
url: /it/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire una data dell'era giapponese in data gregoriana in C#

Se hai bisogno di **convertire date dell'era giapponese** in date gregoriane in C#, questa guida ti mostra esattamente come fare. Che tu stia elaborando dati legacy, leggendo input dell'utente o generando report, la libreria Aspose.Cells rende la conversione semplice. Inoltre, scoprirai il modo migliore per **convertire il calendario giapponese** quando lavori con i fogli di calcolo.

Il tutorial copre ogni passaggio—dalla creazione di una cartella di lavoro al recupero di un valore `DateTime`—in modo da poter copiare‑incollare un programma completo e eseguibile. Non è necessaria alcuna documentazione esterna; basta seguire il codice e le spiegazioni qui sotto.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.6+)
* Una licenza per **Aspose.Cells** (la versione di prova gratuita è valida per i test)
* Un ambiente di sviluppo come Visual Studio 2022 o VS Code
* Familiarità di base con le applicazioni console C#

## Convertire date dell'era giapponese con Aspose.Cells

Il cuore della conversione risiede in poche semplici chiamate API. Aspose.Cells interpreta automaticamente le stringhe dell'era giapponese (ad es., “Reiwa 2/04/01”) e restituisce il risultato come oggetto `DateTime` una volta che il foglio di lavoro è ricalcolato.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Perché ogni passaggio è importante

| Passo | Scopo | Come aiuta la conversione |
|------|---------|-----------------------------|
| **Crea cartella di lavoro** | Fornisce un contenitore che comprende le formule Excel e i sistemi di data. | Il motore interno delle date della libreria è attivato solo all'interno di una cartella di lavoro. |
| **Inserisci stringa dell'era** | Fornisce il testo grezzo del calendario giapponese che desideri tradurre. | Aspose.Cells riconosce i nomi delle ere come *Reiwa*, *Heisei*, *Showa*, ecc. |
| **Imposta stile** | Costringe la cella a essere trattata come una cella valore anziché come una stringa letterale. | Senza uno stile, il metodo `Calculate` potrebbe ignorare la cella, lasciando il testo invariato. |
| **Calcola** | Avvia l'analisi della stringa dell'era e la conversione al numero seriale interno della data. | La libreria converte “Reiwa 2/04/01” → numero seriale → `DateTime` gregoriano. |
| **Leggi `DateTimeValue`** | Restituisce l'oggetto .NET `DateTime` convertito. | Ora hai un `DateTime` standard che puoi utilizzare in qualsiasi API .NET. |

## Come convertire il calendario giapponese in altri scenari

Lo stesso approccio funziona per qualsiasi nome di era giapponese supportato da Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Gestione di stringhe non valide o ambigue

* **Invalid era name** – Aspose.Cells genera una `FormatException`. Avvolgi la conversione in `try/catch` per fornire un messaggio di errore amichevole.
* **Missing year/month/day** – La libreria si aspetta un modello completo “Era Anno/Mese/Giorno”. Se ricevi dati parziali, anteponi le parti mancanti o rifiuta l'input subito.
* **Different locale settings** – La conversione **non** dipende dalla cultura corrente del thread; utilizza sempre la mappa delle ere giapponesi integrata in Aspose.Cells. Questo rende il metodo sicuro per l'elaborazione lato server.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Consigli pratici e problemi comuni

* **Chiama sempre `SetStyle`** before `Calculate`. Saltare questo passaggio è una fonte frequente di bug perché la cella rimane un semplice contenitore di testo.
* **Riutilizza la stessa cartella di lavoro** se devi convertire molte date. Creare una nuova cartella di lavoro per ogni conversione aggiunge overhead non necessario.
* **Conversione batch** – Popola una colonna con stringhe dell'era, chiama `worksheet.Calculate()` una volta, poi leggi l'intera colonna di `DateTimeValue`. Questo è molto più efficiente rispetto al ricalcolo per cella.
* **Compatibilità della versione** – La logica di conversione dell'era è stata introdotta in Aspose.Cells 22.9. Assicurati di essere su quella versione o successiva; le versioni precedenti trattano la stringa come testo semplice.

## Esempio completo funzionante (app console)

Di seguito trovi un programma autonomo che puoi compilare ed eseguire immediatamente. Dimostra sia una conversione Reiwa sia una Heisei, gestendo gli errori in modo elegante.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Output console previsto**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Eseguire questo programma conferma che la libreria converte correttamente le stringhe **convertire date dell'era giapponese** e segnala elegantemente i valori non supportati.

## Conclusione

Ora sai come **convertire date dell'era giapponese** in oggetti `DateTime` gregoriani standard usando Aspose.Cells in C#. Il processo si riduce a inserire il testo dell'era, applicare uno stile, ricalcolare il foglio di lavoro e leggere `DateTimeValue`. Seguendo i passaggi sopra potrai anche rispondere alla domanda più ampia su **come convertire il calendario giapponese** in blocco, gestire gli errori e ottimizzare le prestazioni.

### Prossimi passi

* Esplora le **opzioni di formattazione** per scrivere la data gregoriana nel foglio di lavoro con un formato numerico personalizzato.
* Combina questa conversione con **pipeline di importazione dati** (ad es., lettura di file CSV che contengono date dell'era).
* Rivedi altre funzionalità di Aspose.Cells come **aritmetica delle date** e **impostazioni regionali** per scenari di calendario più complessi.

Buon coding, e sentiti libero di adattare il campione ai tuoi flussi di lavoro di elaborazione dati!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Analizza la data dell'era giapponese in C# con Aspose.Cells – Guida completa](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Abilita l'analisi dell'era giapponese in C# con Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Come creare una cartella di lavoro e convertire una stringa in data in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}