---
category: general
date: 2026-09-24
description: Esegui il parsing di DateTime con il regno dell'imperatore giapponese
  usando Aspose.Cells in C#. Abilita il calendario dell’era giapponese, scrivi le
  stringhe dell’era e ottieni valori DateTime precisi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: it
lastmod: 2026-09-24
og_description: Analizza DateTime con il regno dell'imperatore giapponese usando Aspose.Cells
  in C#. Questo tutorial mostra come abilitare il calendario dell'era giapponese,
  scrivere le stringhe dell'era e leggere nuovamente un DateTime corretto.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Analizza DateTime con il regno dell'imperatore giapponese usando Aspose.Cells
  – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Analizza DateTime con il regno dell'imperatore giapponese usando Aspose.Cells
url: /it/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizzare DateTime con il Regno dell'Imperatore Giapponese usando Aspose.Cells

Se hai bisogno di **analizzare DateTime con il Regno dell'Imperatore Giapponese** in un'applicazione .NET, questa guida ti mostra esattamente come farlo con Aspose.Cells. Abilitando il calendario delle ere giapponesi, scrivendo una stringa basata sull'era e leggendo il valore `DateTime` risultante, ottieni date affidabili e sensibili alla cultura senza manipolazioni manuali delle stringhe.

Lavorare con le date delle ere giapponesi è comune in finanza, governo e sistemi legacy che ancora memorizzano date come “令和3年5月10日”. Questo tutorial copre l'intero flusso di lavoro, dalla configurazione del progetto al recupero di un oggetto `DateTime` che puoi utilizzare in calcoli, registri o visualizzazioni UI.

## Cosa imparerai

- Come aggiungere il pacchetto NuGet Aspose.Cells a un progetto C#.
- Come attivare il **Japanese era calendar** tramite `Workbook.Settings`.
- Come scrivere una stringa di data dell'era giapponese in una cella e lasciare che Aspose.Cells la analizzi automaticamente.
- Come leggere il `DateTime` analizzato usando la proprietà `DateTimeValue`.

**Prerequisiti**  
- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+).  
- Familiarità di base con C# e Visual Studio (o qualsiasi IDE).  
- Accesso a Internet per scaricare il pacchetto Aspose.Cells.

---

## Passo 1: Installa Aspose.Cells

Apri la cartella del tuo progetto in un terminale o nella Console di Gestione Pacchetti NuGet ed esegui:

```bash
dotnet add package Aspose.Cells
```

O, in Visual Studio, fai clic con il tasto destro sul progetto → **Manage NuGet Packages** → cerca **Aspose.Cells** e fai clic su **Install**.  
Questo aggiunge l'assembly `Aspose.Cells`, che fornisce le funzionalità `Workbook`, `Worksheet` e di parsing di cui abbiamo bisogno.

## Passo 2: Abilita il calendario delle ere giapponesi

Aspose.Cells disabilita il parsing delle ere giapponesi per impostazione predefinita. È necessario attivarlo tramite il flag `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Impostare `UseJapaneseEraCalendar` su `true` indica alla libreria di interpretare le stringhe che contengono i nomi delle ere (`令和`, `平成`, `昭和`, ecc.) secondo le regole ufficiali del calendario giapponese.

## Passo 3: Scrivi una stringa di data dell'era giapponese in una cella

Successivamente, ottieni il primo foglio di lavoro e inserisci una stringa di data dell'era giapponese nella cella **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Perché funziona:**  
Quando `UseJapaneseEraCalendar` è attivo, `PutValue` esamina la stringa, rileva il prefisso dell'era (`令和`) e la converte internamente nell'anno gregoriano corrispondente (2021). La libreria quindi memorizza il valore come un vero oggetto `DateTime`, non solo come testo.

## Passo 4: Recupera il valore `DateTime` analizzato

Ora leggi il `DateTimeValue` della cella. Aspose.Cells restituisce automaticamente la data gregoriana.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

L'output conferma che **Parse DateTime with Japanese Emperor Reign** ha convertito correttamente “令和3年5月10日” in 10 maggio 2021.

## Passo 5: Gestire casi limite e variazioni comuni

### Formati di era multipli

Aspose.Cells riconosce diverse rappresentazioni delle ere:

| Era (giapponese) | Intervallo anni gregoriani |
|------------------|----------------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

Se i dati di origine mescolano caratteri a larghezza piena, spazi o usano i kanji “年”, “月”, “日”, il parser riesce comunque. Ad esempio, `"平成31年4月30日"` diventa `2019-04-30`.

### Stringhe non valide

Quando la stringa non può essere analizzata (ad esempio, `"令和99年13月40日"`), `DateTimeValue` restituisce `DateTime.MinValue`. Puoi verificare questa condizione:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Disabilitare la funzionalità

Se in seguito hai bisogno di memorizzare stringhe di era grezze senza conversione, imposta nuovamente il flag su `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Suggerimento sulle prestazioni

Abilitare il calendario delle ere aggiunge un piccolo overhead a ogni chiamata `PutValue` che coinvolge stringhe. Se devi analizzare solo poche celle, attiva il flag subito prima dell'operazione e disattivalo subito dopo per ridurre al minimo l'impatto.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire immediatamente.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Output previsto**

```
Parsed Gregorian date: 2021-05-10
```

Il programma dimostra il flusso end‑to‑end per **Parse DateTime with Japanese Emperor Reign** usando Aspose.Cells, dalla creazione della cartella di lavoro all'ottenimento di un oggetto `DateTime` utilizzabile.

---

## Conclusione

Ora sai come **Parse DateTime with Japanese Emperor Reign** in C# tramite:

1. Installare **Aspose.Cells**.  
2. Abilitare il **Japanese era calendar** tramite `Workbook.Settings`.  
3. Scrivere stringhe basate sull'era nelle celle.  
4. Leggere il `DateTimeValue` risultante.

Questo approccio elimina la logica di parsing manuale, rispetta i confini ufficiali delle ere e si integra perfettamente con il codice .NET esistente per la gestione delle date.

**Passi successivi**  
- Esplora altre funzionalità specifiche per cultura di Aspose.Cells, come **C# date parsing** per i calendari Hijri o Thai Buddhist.  
- Combina questa tecnica con **Workbook Settings** come `CalcEngine` per valutare formule che fanno riferimento a date di era.  
- Usa il `DateTime` analizzato nei report, nella memorizzazione su database o nei componenti UI che richiedono date gregoriane.

Sperimenta liberamente con diverse stringhe di era, gestisci input non validi e integra la soluzione in pipeline di importazione dati più ampie. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Analizza le date delle ere giapponesi in Excel – Guida completa per sviluppatori C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Come analizzare le date giapponesi in C# – Guida completa](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Come implementare la convalida delle date in .NET usando Aspose.Cells: Guida completa](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}