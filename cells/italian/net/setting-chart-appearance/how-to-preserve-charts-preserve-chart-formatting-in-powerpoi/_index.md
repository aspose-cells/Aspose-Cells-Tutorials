---
category: general
date: 2026-07-03
description: come preservare i grafici mantenendo la formattazione dei grafici usando
  Aspose.Slides in C#. Segui questa guida passo passo.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: it
og_description: come preservare i grafici e mantenere la formattazione dei grafici
  con Aspose.Slides in C#. Guida completa con codice.
og_title: come preservare i grafici – conservare la formattazione dei grafici in PowerPoint
  (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Come preservare i grafici – preservare la formattazione dei grafici in PowerPoint
  C#
url: /it/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come preservare i grafici – preservare la formattazione dei grafici in PowerPoint C#

Ti sei mai chiesto **come preservare i grafici** quando devi esportare o manipolare un file PowerPoint in modo programmatico? Forse hai provato un salvataggio rapido e il grafico è diventato un'immagine statica, rompendo la modificabilità di cui contavi.  

In questo tutorial ti mostreremo **come preservare i grafici** **e** mantenere intatta la loro **preserve chart formatting** utilizzando Aspose.Slides per .NET. Alla fine avrai uno snippet C# pronto da eseguire che produce un PPTX in cui ogni grafico rimane un oggetto OOXML modificabile—niente più immagini appiattite.

## Cosa imparerai

- I passaggi esatti per caricare una presentazione, configurare le opzioni di esportazione e salvare mantenendo **preserving chart formatting**.  
- Perché il flag `ExportEditableObjects` è importante e come impedisce la rasterizzazione dei grafici.  
- Problemi comuni (ad es., formati PPT più vecchi, font mancanti) e soluzioni rapide.  

Non è necessaria alcuna esperienza pregressa con Aspose; basta una configurazione di base C# e un file PowerPoint che desideri mantenere compatibile con i grafici.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+).  
- Pacchetto NuGet Aspose.Slides per .NET (`Install-Package Aspose.Slides.NET`).  
- Un file di esempio `input.pptx` che contiene almeno un grafico.  
- Visual Studio, Rider o qualsiasi editor tu preferisca.

---

## Passo 1: Installa Aspose.Slides e crea un nuovo progetto console

Per iniziare, crea una nuova app console e includi la libreria:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Suggerimento:** Se sei dietro un proxy aziendale, aggiungi il flag `--no-restore` e ripristina più tardi con le impostazioni del proxy.

## Passo 2: Carica la presentazione di origine – il primo punto dove applicare **how to preserve charts**

Apri il tuo file PPTX usando la classe `Presentation`. È qui che il percorso verso **how to preserve charts** inizia davvero.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Nota che non abbiamo ancora toccato alcun oggetto grafico—è intenzionale. Caricare il file così com'è garantisce di mantenere la struttura XML originale, fondamentale per **preserve chart formatting** in seguito.

## Passo 3: Configura le opzioni di esportazione – il cuore di **how to preserve charts**

Aspose.Slides offre la classe `PresentationExportOptions`. Impostare `ExportEditableObjects` su `true` indica al motore di mantenere grafici, tabelle e SmartArt come parti OOXML native invece di appiattirle.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Perché funziona? Quando `ExportEditableObjects` è `false` (impostazione predefinita), la libreria rasterizza gli oggetti complessi per compatibilità, il che distrugge **preserve chart formatting**. Attivandolo si conserva l'XML originale del grafico, consentendo agli utenti finali di aprire il PPTX e modificare ancora i dati del grafico.

## Passo 4: Salva la presentazione usando le opzioni configurate

Ora scriviamo il file di output. La stessa overload di `Save` che accetta `SaveFormat` e `exportOptions` garantisce che il grafico rimanga modificabile.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Eseguendo questo programma si genera `EditableCharts.pptx`. Aprilo in PowerPoint, fai clic destro su un grafico e vedrai l'opzione “Edit Data” usuale—la prova che abbiamo padroneggiato con successo **how to preserve charts** e **preserve chart formatting**.

## Passo 5: Verifica il risultato e risolvi i problemi comuni

### Verifica

1. Apri `EditableCharts.pptx` in PowerPoint.  
2. Fai clic su qualsiasi grafico → “Edit Data”.  
3. Dovrebbe apparire il foglio dati simile a Excel, consentendoti di modificare i valori delle serie.

Se vedi solo un'immagine statica, ricontrolla che:

- Stai usando una versione recente di Aspose.Slides (le versioni più vecchie avevano bug con `ExportEditableObjects`).  
- Il PPTX di origine contiene effettivamente oggetti grafico (non immagini di grafici).  
- Nessun tema personalizzato o sostituzione di font sta facendo renderizzare il grafico come immagine.

### Casi limite

- **File PPT (binari) più vecchi:** Convertirli prima in PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`) prima di applicare le opzioni di esportazione.  
- **Presentazioni grandi:** L'uso della memoria può aumentare; considera il pattern `Dispose` di `Presentation` o le API di streaming per file massivi.  
- **Font incorporati:** Se l'ambiente di destinazione non dispone dei font originali, PowerPoint potrebbe ricorrere a un fallback e renderizzare il grafico come immagine. Incorpora i font nel file di origine o includili con la tua applicazione.

---

## Domande frequenti (FAQ)

**Q: Funziona con i file PowerPoint 2003 (PPT)?**  
A: Direttamente no—`ExportEditableObjects` si applica solo al formato PPTX. Converti prima, poi esporta.

**Q: Posso preservare altri oggetti come SmartArt?**  
A: Assolutamente. Lo stesso flag `ExportEditableObjects` mantiene SmartArt, tabelle e diagrammi modificabili.

**Q: E se devo mantenere la dimensione originale della diapositiva?**  
A: La dimensione della diapositiva è memorizzata nei metadati della presentazione e non è influenzata da queste opzioni. Non è necessario alcun codice aggiuntivo.

## Prossimi passi – mantieni lo slancio

Ora che hai padroneggiato **how to preserve charts**, prova a esplorare:

- **preserve chart formatting** per tipi di grafico specifici (ad es., barre impilate vs. radar).  
- Utilizzare l'API `Chart` per modificare programmaticamente i dati prima del salvataggio.  
- Esportare in altri formati (PDF, HTML) mantenendo comunque i grafici modificabili nel PPTX di origine.  

Ognuno di questi si basa sullo stesso principio: mantenere intatto l'OOXML sottostante.

## Conclusione

Abbiamo illustrato **how to preserve charts** in un file PowerPoint usando Aspose.Slides per .NET, e abbiamo dimostrato i passaggi esatti di **preserve chart formatting** necessari per mantenere quei grafici completamente modificabili. Lo snippet di codice completo sopra è pronto per essere inserito in qualsiasi progetto C#, e le spiegazioni coprono il *perché* di ogni riga—così non ti limiterai a copiare‑incollare, ma comprenderai.

Provalo, modifica le opzioni di esportazione, e presto automatizzerai gli aggiornamenti delle presentazioni senza mai perdere la possibilità di perfezionare i dati dei grafici. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come esportare i grafici Excel in PDF usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Come convertire i grafici Excel in SVG usando Aspose.Cells per .NET (Guida passo‑passo)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Come creare grafici in Excel usando Aspose.Cells per .NET: Guida per sviluppatori](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}