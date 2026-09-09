---
category: general
date: 2026-03-01
description: Come creare rapidamente una cartella di lavoro in C# — impara a scrivere
  un valore in una cella, impostare il formato numerico della cella e formattare il
  numero della cella con semplici passaggi.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: it
og_description: Come creare una cartella di lavoro in C#? Questa guida ti mostra come
  scrivere un valore in una cella, impostare il formato numerico della cella e formattare
  il numero della cella in poche righe di codice.
og_title: Come creare una cartella di lavoro in C# – Scrivere valori e formattare
  i numeri
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Come creare una cartella di lavoro in C# – Scrivere valori e formattare i numeri
url: /it/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Creare un Workbook in C# – Scrivere Valori e Formattare Numeri

Creare un workbook in C# è un compito comune quando è necessario generare file Excel al volo. In questa guida ti mostreremo come scrivere un valore in una cella e formattare il numero della cella affinché il foglio finale abbia un aspetto curato.

Se ti sei mai trovato davanti a un foglio vuoto chiedendoti perché i numeri mostrano troppe cifre decimali, non sei solo. Copriremo tutto, dall'inizializzazione dell'oggetto workbook all'impostazione di un formato numerico personalizzato, e includeremo alcuni consigli per i casi limite che potresti incontrare in seguito.

## Cosa Imparerai

- **Inizializzare** una nuova istanza di `Workbook`.  
- **Scrivere valore nella cella** usando il metodo `PutValue`.  
- **Impostare il formato numerico della cella** con un oggetto `Style`, ottenendo una visualizzazione pulita a due cifre.  
- Verificare il risultato leggendo nuovamente la cella o aprendo il file in Excel.  

Non sono necessarie librerie esterne oltre a Aspose.Cells standard (o qualsiasi API simile), e il codice funziona su .NET 6+ senza configurazioni aggiuntive.

---

## Come Creare un Workbook – Inizializzare l'Oggetto

Prima di tutto: ti serve un oggetto workbook per contenere i fogli. Pensa al `Workbook` come all'intero file Excel, mentre ogni `Worksheet` è una singola scheda.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Perché è importante:* Creare il workbook alloca le strutture interne che in seguito conterranno righe, colonne e formattazione. Senza questo oggetto, non c'è dove scrivere un valore nella cella.

> **Pro tip:** Se prevedi di lavorare con un file esistente, sostituisci `new Workbook()` con `new Workbook("template.xlsx")` per caricare un modello e preservarne gli stili.

## Scrivere Valore nella Cella

Ora che abbiamo un workbook, inseriamo un numero nella cella **A1** del primo foglio di lavoro.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Perché usiamo `PutValue`*: Questo metodo rileva automaticamente il tipo di dato, così non devi fare cast o conversioni manuali. Rispetta anche lo stile esistente della cella, utile quando in seguito **imposti il formato numerico della cella**.

### Verifica Rapida

Se leggi nuovamente la cella, vedrai il valore grezzo:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Questo è il numero prima che venga applicata qualsiasi formattazione.

## Impostare il Formato Numerico della Cella

Visualizzare un double grezzo con molte decimali non è sempre user‑friendly. Limitiamolo a due cifre decimali.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

La proprietà `Number` corrisponde agli ID dei formati numerici predefiniti di Excel. `2` significa “Numero con due decimali”. Se ti serve un formato diverso — ad esempio valuta o data — useresti un altro ID o una stringa di formato personalizzata.

### Alternativa: Stringa di Formato Personalizzata

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Perché scegliere uno stile personalizzato?* Ti dà il pieno controllo, soprattutto quando gli ID predefiniti non coprono le impostazioni regionali.

## Verificare l'Uscita (Opzionale ma Consigliato)

Dopo aver applicato lo stile, puoi salvare il workbook e aprirlo in Excel per confermare l'aspetto.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Dovresti vedere **123,46** nella cella A1 — esattamente due decimali, grazie al formato impostato.

---

### Esempio Completo Funzionante

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare‑incollare in un'app console.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Output previsto quando esegui il programma:**

```
Cell A1 shows: 123.46
```

Apri `FormattedWorkbook.xlsx` in Excel e vedrai lo stesso valore formattato.

---

## Varianti Comuni & Casi Limite

### 1. Formati Numerici Differenti

| Obiettivo | ID Formato | Snippet di Codice |
|------|-----------|--------------|
| Valuta (due decimali) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Percentuale (nessun decimale) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Notazione scientifica | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Se nessuno degli ID predefiniti è adatto, ricorri a una stringa personalizzata come mostrato prima.

### 2. Separatori Decimali Specifici per Cultura

Alcune impostazioni locali usano la virgola per i decimali. Puoi forzare un formato sensibile alla cultura:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Scrivere Testo Invece di Numeri

Quando devi **scrivere una cella** con una stringa, passa semplicemente una stringa a `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Non è necessario alcun formato numerico, ma puoi comunque applicare lo stile del font.

### 4. Grandi Set di Dati

Se stai popolando migliaia di righe, l'inserimento in batch (`Cells.ImportArray`) è più veloce rispetto al ciclo `PutValue`. L'approccio di formattazione rimane lo stesso; basta applicare lo stile a un intervallo:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Domande Frequenti

**D: Questo funziona con .NET Core?**  
R: Assolutamente. Aspose.Cells supporta .NET Standard 2.0 e versioni successive, quindi puoi mirare a .NET 5, .NET 6 o .NET 7 senza modifiche.

**D: E se ho bisogno di più di due decimali?**  
R: Cambia la proprietà `Number` all'ID predefinito appropriato (ad esempio `3` per tre decimali) o modifica la stringa di formato personalizzata (`"#,##0.000"`).

**D: Posso applicare il formato a un'intera colonna in una volta?**  
R: Sì. Usa `Cells["A:A"]` per ottenere l'intera colonna e poi `SetStyle`.

---

## Conclusione

Ora sai **come creare oggetti workbook** in C#, **scrivere valori nella cella** e **impostare il formato numerico della cella** affinché i numeri appaiano esattamente come desideri. Padroneggiando queste basi sarai in grado di generare report Excel dall'aspetto professionale, fatture o esportazioni di dati con il minimo sforzo.

Successivamente, potresti esplorare **formattare il numero della cella** per date, percentuali o formattazione condizionale — ognuno si basa sugli stessi principi trattati. Approfondisci la documentazione di Aspose.Cells per opzioni di stile più avanzate, o prova a combinare più fogli in un unico workbook per report più ricchi.

Buon coding, e ricorda: un foglio di calcolo ben formattato è solo

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}