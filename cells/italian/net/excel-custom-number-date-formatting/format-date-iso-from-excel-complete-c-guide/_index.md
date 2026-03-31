---
category: general
date: 2026-03-30
description: Impara come formattare la data ISO mentre leggi i valori datetime di
  Excel ed estrai i dati datetime di Excel usando Aspose.Cells in C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: it
og_description: formattare la data ISO dai dati di Excel usando Aspose.Cells. Questa
  guida mostra come leggere le date e gli orari di Excel, estrarre i valori datetime
  di Excel e generare date ISO.
og_title: Formattare la data ISO da Excel – Tutorial C# passo passo
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Formattare data ISO da Excel – Guida completa C#
url: /it/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formattare data iso da Excel – Guida completa C#

Ti è mai capitato di **format date iso** quando estrai date da un foglio Excel? Forse stai gestendo date dell'era giapponese, o vuoi semplicemente una stringa `yyyy‑MM‑dd` pulita per un payload API. In questo tutorial vedrai esattamente come **read Excel datetime** celle, **extract datetime Excel** valori, e trasformarli in formato ISO‑8601—senza indovinare.

Passeremo in rassegna un esempio reale che utilizza Aspose.Cells, spiega perché ogni riga è importante e ti mostra l'output finale che puoi copiare‑incollare nel tuo progetto. Alla fine, sarai in grado di gestire stringhe d'era particolari come “令和3年5月1日” e produrre una data ISO standard, pronta per database, JSON o qualsiasi altro contesto.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework)
- Aspose.Cells per .NET (versione di prova gratuita o con licenza)
- Familiarità di base con C# e i concetti di Excel
- Visual Studio o qualsiasi editor C# a tua scelta

Non sono necessari pacchetti NuGet aggiuntivi oltre a Aspose.Cells, quindi la configurazione è abbastanza semplice.

---

## Passo 1: Creare un Workbook e puntare al primo Worksheet

La prima cosa da fare è creare un nuovo oggetto `Workbook`. Questo ti fornisce una rappresentazione in memoria di un file Excel, che puoi poi manipolare o leggere da.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Perché è importante:*  
Creare il workbook programmaticamente ti consente di evitare di gestire file fisici durante i test. Inoltre garantisce che il riferimento al worksheet sia sempre valido—nessuna sorpresa di null‑reference più tardi quando provi a **read Excel datetime** valori.

---

## Passo 2: Scrivere una stringa di data dell'era giapponese in una cella

Il nostro obiettivo è dimostrare il parsing di una data non gregoriana. Inseriremo la stringa dell'era direttamente nella cella **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Consiglio professionale:* Se stai estraendo dati da un workbook esistente, salteresti la chiamata `PutValue` e semplicemente faresti riferimento alla cella che contiene già la data. L'importante è che la cella contenga una **string** che rappresenta una data nel calendario lunisolare giapponese.

---

## Passo 3: Configurare una Culture che comprende il calendario lunisolare giapponese

La classe `CultureInfo` di .NET ti consente di specificare come le date devono essere interpretate. Sostituendo il calendario gregoriano predefinito con `JapaneseLunisolarCalendar`, fornisci al parser il contesto necessario.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Perché lo facciamo:*  
Se provi a fare il parsing di “令和3年5月1日” con la culture predefinita, .NET genererebbe una `FormatException`. Sostituendo con il calendario lunisolare, il runtime sa esattamente come mappare “令和3年” (il 3° anno dell'era Reiwa) all'anno gregoriano 2021.

---

## Passo 4: Analizzare il valore della cella come `DateTime` usando la Culture configurata

Ora arriva il cuore dell'operazione—convertire quella stringa dell'era in un oggetto `DateTime` corretto. Aspose.Cells fornisce un overload conveniente di `GetDateTime` che accetta un `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Cosa succede dietro le quinte:*  
`GetDateTime` legge la stringa grezza, applica le regole del calendario della culture fornita, e restituisce un `DateTime` che rappresenta lo stesso momento nel calendario gregoriano. Questo è il momento in cui **extract datetime Excel** dati in una forma con cui puoi lavorare in .NET.

---

## Passo 5: Restituire la data analizzata in formato ISO 8601

Infine, formattiamo il `DateTime` come stringa ISO—`yyyy‑MM‑dd`—che è universalmente accettata da API, database e framework front‑end.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Perché ISO?*  
ISO 8601 elimina l'ambiguità. “05/01/2021” potrebbe essere il 1 maggio o il 5 gennaio a seconda della locale. `2021-05-01` è cristallino, ed è per questo che **format date iso** in quasi tutti gli scenari di integrazione.

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione. Copialo in un progetto console app, aggiungi il riferimento Aspose.Cells, e premi **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Output previsto**

```
2021-05-01
```

Eseguilo una volta, e vedrai la data formattata in ISO stampata sulla console. Questo è l'intero flusso da **read Excel datetime** a **format date iso**.

---

## Gestione dei casi limite comuni

### 1. Celle contenenti numeri di data reali di Excel

A volte Excel memorizza le date come numeri seriali (ad esempio `44204`). In tal caso, non è necessaria una culture; basta chiamare `GetDateTime()` senza parametri:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Celle vuote o non valide

Se una cella è vuota o contiene una stringa non analizzabile, `GetDateTime` genererà un'eccezione. Avvolgi la chiamata in un `try/catch` o verifica prima `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Formati di era diversi

Altre ere giapponesi (Heisei, Showa) seguono lo stesso schema. Lo stesso `JapaneseLunisolarCalendar` le gestirà automaticamente, quindi non serve logica aggiuntiva—basta fornire la stringa.

---

## Consigli professionali & Avvertenze

- **Performance:** Quando elabori fogli di calcolo di grandi dimensioni, riutilizza una singola istanza di `CultureInfo` invece di crearne una nuova all'interno di un ciclo.
- **Sicurezza dei thread:** Gli oggetti `CultureInfo` sono di sola lettura dopo aver impostato il calendario, quindi sono sicuri da condividere tra thread.
- **Licenza Aspose.Cells:** Se stai usando la versione di prova gratuita, ricorda che alcune funzionalità potrebbero essere limitate dopo la scadenza del periodo di prova. Il parsing delle date mostrato qui funziona bene sia in modalità trial che con licenza.
- **Fusi orari:** Il `DateTime` ottenuto è **unspecified** (senza fuso orario). Se ti serve UTC, chiama `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` o converti usando `TimeZoneInfo`.

---

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **format date iso** da un workbook Excel usando C#. Partendo da una stringa grezza dell'era giapponese, abbiamo **read Excel datetime**, configurato la culture corretta, **extract datetime excel** dati, e infine prodotto una stringa ISO‑8601 pulita. L'approccio funziona per qualsiasi rappresentazione di data che Excel possa fornire, sia che si tratti di un numero seriale, di una stringa specifica per locale o di un formato di era tradizionale.

Passi successivi? Prova a iterare su un'intera colonna di date, scrivi i risultati ISO in un nuovo foglio, o inviali direttamente in un payload JSON per un servizio web. Se sei curioso di altri sistemi di calendario (ebreo, islamico), Aspose.Cells e il `CultureInfo` di .NET rendono quegli esperimenti altrettanto semplici.

Hai domande o un formato di data difficile da decifrare? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}