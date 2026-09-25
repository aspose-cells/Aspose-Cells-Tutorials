---
category: general
date: 2026-03-25
description: Scopri come incorporare i font in HTML quando esporti Excel in HTML.
  Questo tutorial passo‑passo ti mostra come incorporare i font in HTML e salvare
  la cartella di lavoro come HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- how to export excel
- save workbook as html
language: it
og_description: Come incorporare i font in HTML durante l'esportazione di Excel? Segui
  questa guida per incorporare i font in HTML, esportare Excel in HTML e salvare la
  cartella di lavoro come HTML con Aspose.Cells.
og_title: Come incorporare i font in HTML da Excel – Guida completa
tags:
- Aspose.Cells
- C#
- HTML export
- Font embedding
title: Come incorporare i font in HTML da Excel – Guida completa
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-from-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font in HTML da Excel – Guida completa

Ti sei mai chiesto **come incorporare i font** in un file HTML generato da una cartella di lavoro Excel? Non sei l’unico. Molti sviluppatori si trovano in difficoltà quando l’HTML esportato appare corretto sulla propria macchina ma perde la tipografia originale su un altro dispositivo. La buona notizia? La soluzione è piuttosto semplice con Aspose.Cells, e puoi avere i font incorporati direttamente nell’output HTML.

In questo tutorial percorreremo passo passo le istruzioni per **incorporare i font in html**, ti mostreremo come **esportare Excel in html**, e infine dimostreremo come **salvare la cartella di lavoro come html** con tutte le impostazioni necessarie. Alla fine avrai un file HTML pronto da usare che renderizza esattamente come il tuo foglio di calcolo originale—nessun glifo mancante, nessun font di fallback.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework)
- Aspose.Cells per .NET (versione di prova gratuita o licenziata)
- Un file Excel di esempio (`sample.xlsx`) che utilizza almeno un font personalizzato
- Visual Studio 2022 o qualsiasi editor C# tu preferisca

Non sono necessari pacchetti NuGet aggiuntivi oltre a Aspose.Cells.

## Passo 1: Configurare il progetto e caricare la cartella di lavoro

Prima di tutto—crea una nuova console app e aggiungi il riferimento ad Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load an existing Excel workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // We'll configure the export options in the next step
        }
    }
}
```

**Perché è importante:** Il caricamento della cartella di lavoro è la base. Se la cartella di lavoro non viene caricata correttamente, nessuna delle impostazioni successive di incorporamento dei font avrà effetto. Inoltre, tieni presente che Aspose.Cells legge automaticamente le informazioni sui font memorizzate nel file, quindi non è necessario specificare manualmente i nomi dei font.

## Passo 2: Creare HtmlSaveOptions e abilitare l’incorporamento dei font

Ora creiamo un’istanza di `HtmlSaveOptions` e attiviamo il flag `EmbedAllFonts`. Questo indica ad Aspose.Cells di incorporare ogni font referenziato dalla cartella di lavoro direttamente nell’HTML generato.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions();

// Enable embedding of all fonts in the output HTML
htmlSaveOptions.EmbedAllFonts = true;

// Optional: Reduce the size of the generated HTML by using base64 encoding
htmlSaveOptions.ExportEmbeddedImages = true;
```

**Perché abilitiamo `EmbedAllFonts`:** Quando esporti Excel in HTML senza questo flag, l’HTML fa riferimento ai font solo per nome. Se il sistema dell’utente non ha quei font installati, il browser ricorre a una famiglia generica, rovinando il layout. L’incorporamento garantisce che i glifi esatti viaggino con il file HTML.

**Suggerimento professionale:** Se ti servono solo un sottoinsieme di font (ad esempio, sai che la cartella di lavoro usa solo *Calibri* e *Arial*), puoi impostare `htmlSaveOptions.FontsList` a una collezione personalizzata. Questo può ridurre drasticamente la dimensione finale del file.

## Passo 3: Salvare la cartella di lavoro come HTML con i font incorporati

Infine, chiama `Save` sull’oggetto `Workbook`, passando il percorso e le opzioni appena configurate.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string htmlPath = @"C:\Temp\embedded.html";
workbook.Save(htmlPath, htmlSaveOptions);

Console.WriteLine($"HTML file with embedded fonts saved to: {htmlPath}");
```

Fatto—il tuo `embedded.html` ora contiene blocchi `<style>` con definizioni `@font-face` e dati dei font codificati in base64. Aprilo in qualsiasi browser moderno e dovresti vedere la stessa tipografia di `sample.xlsx`.

### Risultato atteso

Quando apri `embedded.html`:

- Il font personalizzato appare esattamente come in Excel.
- Non vengono richiesti file di font esterni (controlla la scheda Network negli strumenti di sviluppo—non dovrebbe esserci alcun caricamento).
- La dimensione della pagina può essere maggiore rispetto a un’esportazione HTML semplice, ma la fedeltà visiva è perfetta.

## Esportare Excel in HTML – Esempio completo

Mettendo tutto insieme, ecco il programma completo e funzionante:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // 2️⃣ Configure HTML export options
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedAllFonts = true,          // ✅ Embed every used font
                ExportEmbeddedImages = true,   // ✅ Include images as base64
                ExportChartImageFormat = ImageFormat.Png,
                ExportImagesAsBase64 = true    // ✅ Keep everything in one file
            };
            
            // 3️⃣ Save as HTML
            string htmlPath = @"C:\Temp\embedded.html";
            workbook.Save(htmlPath, htmlOptions);
            
            Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
        }
    }
}
```

**Perché funziona:** L’oggetto `HtmlSaveOptions` è un contenitore potente. Attivando `EmbedAllFonts`, istruisci Aspose.Cells a scansionare la collezione di stili della cartella di lavoro, prelevare i file dei font dal sistema operativo e incorporarli. I flag `ExportEmbeddedImages` e `ExportImagesAsBase64` mantengono l’HTML autonomo, utile quando devi inviare il file via email o archiviarlo in un database.

## Problemi comuni nell’incorporare i font in HTML

Anche con il codice corretto, alcuni intoppi possono ostacolarti. Affrontiamoli prima che diventino un problema.

| Problema | Perché accade | Come risolverlo |
|----------|----------------|-----------------|
| **Font mancante sul server** | Il server dove gira il codice potrebbe non avere il font personalizzato installato. | Installa i font richiesti sul server o copia i file `.ttf/.otf` in una cartella nota e imposta `htmlSaveOptions.FontsLocation` su quel percorso. |
| **File HTML di grandi dimensioni** | Incorporare molti font pesanti può gonfiare l’HTML (a volte >5 MB). | Usa `htmlSaveOptions.FontsList` per incorporare solo i font necessari, oppure considera di sotto‑impostare i font con uno strumento come FontForge prima dell’incorporamento. |
| **Restrizioni di licenza** | Alcuni font commerciali vietano l’incorporamento. | Verifica la EULA del font. Se l’incorporamento è vietato, ricorri a un’alternativa web‑safe o converti il foglio in PDF. |
| **Compatibilità del browser** | Browser molto vecchi (IE 8) potrebbero ignorare `@font-face` con dati base64. | Fornisci una regola CSS di fallback o servi un file CSS separato per i browser legacy. |
| **Intervallo Unicode errato** | Il font incorporato potrebbe non contenere tutti i caratteri usati (ad esempio glifi asiatici). | Assicurati che il font di origine supporti i blocchi Unicode richiesti, oppure incorpora un font secondario che copra l’intervallo mancante. |

## Avanzato: Incorporare solo i font selezionati

Se sai che il tuo workbook usa solo *Calibri* e *Times New Roman*, puoi limitare l’incorporamento così:

```csharp
htmlSaveOptions.FontsList = new string[] { "Calibri", "Times New Roman" };
```

Questo riduce drasticamente le dimensioni dell’HTML mantenendo l’aspetto originale.

## Testare l’output

Dopo aver generato `embedded.html`, esegui questi rapidi controlli:

1. Apri il file in Chrome/Edge/Firefox.  
2. Apri Strumenti per sviluppatori → Rete → filtra per **font**. Non dovresti vedere richieste esterne.  
3. Ispeziona il blocco `<style>`; troverai regole `@font-face` con `src: url(data:font/ttf;base64,…)`.  
4. Confronta il testo renderizzato con la visualizzazione originale di Excel—un allineamento pixel‑perfect indica che hai avuto successo.

## Riepilogo

In questa guida abbiamo coperto **come incorporare i font** in HTML quando **esporti Excel in HTML** usando Aspose.Cells. Creando un’istanza di `HtmlSaveOptions`, impostando `EmbedAllFonts = true` e chiamando `Workbook.Save`, ottieni un file HTML autonomo che riproduce fedelmente la tipografia del foglio di calcolo originale. Abbiamo anche esaminato problemi comuni, trucchi di performance e un modo rapido per incorporare solo i font davvero necessari.

---

### Cosa c’è dopo?

- **Esportare Excel in PDF con font incorporati** – ideale per documenti pronti per la stampa.  
- **Convertire più fogli in un unico file HTML** – scopri `HtmlSaveOptions.OnePagePerSheet`.  
- **Generazione dinamica di HTML in ASP.NET Core** – trasmetti l’HTML direttamente al browser senza toccare il file system.

Sperimenta con le opzioni, lascia un commento se incontri difficoltà, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}