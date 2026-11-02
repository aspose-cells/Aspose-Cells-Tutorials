---
category: general
date: 2026-03-22
description: Scopri come formattare la data e ora in ISO durante l'estrazione della
  data da Excel e visualizzare la data ISO utilizzando Aspose.Cells in C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: it
og_description: Formattare data e ora in ISO è semplice. Questa guida mostra come
  estrarre la data da Excel e visualizzare la data ISO con Aspose.Cells.
og_title: Formattare datetime in ISO in C# – Tutorial passo‑passo
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formattare DateTime in ISO in C# – Guida completa
url: /it/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formattare datetime in iso in C# – Guida completa

Mai avuto bisogno di **format datetime to iso** ma la sorgente si trova all'interno di una cartella di lavoro Excel? Forse la cella contiene un'era giapponese come “令和3年5月1日” e ti stai grattando la testa chiedendoti come trasformarla in una stringa pulita `2021‑05‑01`. Non sei solo. In questo tutorial **extract date from excel**, analizzeremo l'era giapponese e poi **display iso date** sulla console—tutto con poche righe di C# e Aspose.Cells.

Ti guideremo passo passo su tutto ciò che ti serve: il pacchetto NuGet necessario, il codice esatto da copiare‑incollare, perché ogni riga è importante e una serie di consigli per i casi limite. Alla fine avrai uno snippet riutilizzabile che **formats datetime to iso** indipendentemente da quanto strano sia il valore originale in Excel.

## Cosa ti serve

- .NET 6.0 o successivo (il codice si compila anche su .NET Framework 4.6+)
- Visual Studio 2022 (o qualsiasi editor tu preferisca)
- **Aspose.Cells for .NET** pacchetto NuGet – `Install-Package Aspose.Cells`
- Un file Excel (o una cartella di lavoro nuova) che contiene una data in formato era giapponese

Questo è tutto. Nessuna libreria aggiuntiva, nessun interop COM, solo un singolo metodo ben documentato.

## Passo 1: Crea un Workbook e Scrivi una Data in Era Giapponese  

Prima di tutto, ci serve un workbook con cui lavorare. Se hai già un file Excel, puoi caricarlo con `new Workbook("path")`. Per questo esempio creiamo un nuovo workbook in memoria e inseriamo una stringa di era giapponese nella cella **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Why we do this:** Aspose.Cells tratta i valori delle celle come stringhe per impostazione predefinita. Inserendo il testo grezzo dell'era simuliamo uno scenario reale in cui un cliente giapponese ha inserito le date nel proprio calendario nativo.

## Passo 2: Abilita il Parsing dell'Era Giapponese e Estrai la Data  

Aspose.Cells può tradurre automaticamente le stringhe di era giapponese in oggetti .NET `DateTime`—a patto di dirglielo. Il flag `DateTimeParseOptions.EnableJapaneseEra` fa il lavoro pesante.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** Se dimentichi l'opzione `EnableJapaneseEra`, la libreria restituirà la stringa originale e la conversione successiva fallirà. Verifica sempre `parsed.Type` se gestisci contenuti misti.

## Passo 3: Converti il DateTime Analizzato in ISO 8601  

Ora che abbiamo un `DateTime` corretto, trasformarlo in una stringa formattata ISO è un gioco da ragazzi. Il pattern `"yyyy-MM-dd"` è conforme alla parte data di ISO 8601, che è ciò che la maggior parte delle API si aspetta.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Eseguendo il programma stampa:

```
ISO date: 2021-05-01
```

Questa è la **display iso date** che cercavi.

## Esempio Completo, Eseguibile  

Di seguito trovi il blocco di codice completo da copiare direttamente in un progetto console. Nessuna dipendenza nascosta, nessuna configurazione extra.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Expected output:** `ISO date: 2021-05-01`

## Analisi Passo‑per‑Passo (Perché Ogni Parte è Importante)

| Step | What Happens | Why It’s Important |
|------|--------------|--------------------|
| **Create workbook** | Inizializza un contenitore Excel in memoria. | Ti fornisce un sandbox per testare senza toccare il file system. |
| **PutValue** | Memorizza la stringa grezza dell'era giapponese in **A1**. | Simula l'inserimento reale dei dati; garantisce che il parser veda il testo esatto. |
| **GetValue with `EnableJapaneseEra`** | Converte la stringa dell'era in un .NET `DateTime`. | Gestisce automaticamente la conversione del calendario—nessuna tabella di ricerca manuale necessaria. |
| **`ToString("yyyy-MM-dd")`** | Format il `DateTime` in ISO 8601. | Garantisce una stringa data invariata dalla cultura, ordinabile e accettata da API REST, database, ecc. |
| **Console.WriteLine** | Mostra la data ISO finale. | Conferma che l'intera pipeline funziona end‑to‑end. |

## Gestione delle Varianti Comuni  

### 1. Posizioni di Celle Diverse  

Se la tua data si trova in **B2** o in un intervallo denominato, sostituisci semplicemente `"A1"` con l'indirizzo appropriato:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Più Date in una Colonna  

Quando devi **extract date from excel** per molte righe, itera sull'intervallo usato:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Fallback per Date Non‑Era  

Se una cella contiene già una stringa di data standard, il parser funziona comunque, ma potresti volere una rete di sicurezza:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Il flag `TryParse` previene eccezioni e restituisce il valore originale se la conversione fallisce.

### 4. Componente Tempo  

Se ti serve anche la parte temporale, usa `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Ottieni così un timestamp ISO 8601 completo (`2021-05-01T00:00:00`).

## Supporto Visivo  

![esempio di formattazione datetime in iso](image.png "Un esempio di formattazione datetime in iso in C#")

*Testo alternativo:* *esempio di formattazione datetime in iso che mostra l'output della console*

## Domande Frequenti  

- **Posso usarlo con file .xls?**  
  Sì. Aspose.Cells supporta `.xls`, `.xlsx`, `.csv` e molti altri formati out of the box.

- **Cosa succede se il workbook è protetto da password?**  
  Caricalo con `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Il formato ISO dipende dalla locale?**  
  No. Il pattern `"yyyy-MM-dd"` è invariato dalla cultura, garantendo la stessa stringa su qualsiasi macchina.

- **Funziona su .NET Core?**  
  Assolutamente—Aspose.Cells è conforme a .NET Standard 2.0.

## Conclusione  

Abbiamo visto come **format datetime to iso** **extract date from excel**, analizzando le stringhe di era giapponese e infine **display iso date** sulla console. I passaggi fondamentali—creare un workbook, scrivere o caricare il testo dell'era, abilitare il parsing dell'era giapponese e formattare con `ToString("yyyy-MM-dd")`—sono tutto ciò che ti serve nella maggior parte degli scenari.

Prossimi passi consigliati:

- Scrivi le date ISO in un'altra colonna per ulteriori elaborazioni.
- Esporta il workbook trasformato in CSV per importazioni massive.
- Combina questa logica con un'API web che accetta upload di Excel e restituisce date ISO codificate in JSON.

Sentiti libero di sperimentare con formati di data diversi, fusi orari o persino calendari personalizzati. La flessibilità di Aspose.Cells ti permette di non incontrare quasi mai ostacoli.

Buon coding, e che tutte le tue date siano perfettamente conformi a ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}