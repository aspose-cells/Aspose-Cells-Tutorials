---
date: '2026-10-28'
description: Scopri come incollare i valori utilizzando le opzioni di copia e incolla
  di Aspose.Cells in Java, con codice passo-passo, configurazione della dipendenza
  Maven e consigli sulla licenza.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Scopri come incollare i valori utilizzando le opzioni di copia e incolla
  di Aspose.Cells in Java, con codice passo-passo, configurazione della dipendenza
  Maven e consigli sulla licenza.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Come incollare i valori con le opzioni di copia e incolla di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Come incollare i valori con le opzioni di copia e incolla di Aspose.Cells
url: /it/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incollare valori con le opzioni di copia e incolla di Aspose.Cells

Automatizzare la generazione di report Excel in Java significa che puoi generare, consolidare e formattare cartelle di lavoro senza mai aprire Excel manualmente. Con **Aspose.Cells** ottieni il pieno controllo su formule, righe nascoste e valori delle celle, così i tuoi report rimangono accurati e leggeri. In questo tutorial imparerai a usare **CopyOptions.ReferToDestinationSheet** per mantenere le formule corrette e **PasteOptions** per incollare solo i valori visibili di cui hai bisogno.

## Risposte rapide
- **Cosa fa `CopyOptions.ReferToDestinationSheet`?** Riscrive le formule in modo che puntino al foglio di destinazione dopo un'operazione di copia.  
- **Come posso incollare solo le celle visibili?** Chiama `PasteOptions.setOnlyVisibleCells(true)` insieme a `PasteType.VALUES`.  
- **Quale versione della libreria è richiesta?** Aspose.Cells 25.3 o successiva.  
- **Ho bisogno di una licenza per la produzione?** Sì – una licenza permanente o temporanea rimuove i limiti di valutazione.  
- **Posso usare Maven o Gradle?** Entrambi sono supportati; vedi gli snippet di dipendenza qui sotto.

## Cos'è “automatizzare la generazione di report Excel”?
Automatizzare la generazione di report Excel significa generare e aggiornare cartelle di lavoro Excel in modo programmatico, consentendo di creare, unire e formattare report senza copia‑incolla manuale, riducendo gli errori e risparmiando ore di lavoro ripetitivo. Questo approccio è ideale per lavori batch programmati, dashboard basate sui dati e pipeline di consolidamento finanziario.

## Perché usare CopyOptions e PasteOptions per i report?
Queste due classi ti permettono di mantenere intatti i riferimenti delle formule durante la copia dei dati **e** estrarre solo le celle visibili dopo il filtraggio o la nasconditura delle righe. Usarle insieme riduce la quantità di dati trasferiti fino all'80 % negli scenari tipici di tabelle filtrate e garantisce che le formule continuino a calcolare correttamente nel foglio di destinazione.

## Prerequisiti
- Java 8 o superiore.  
- Maven o Gradle per la gestione delle dipendenze.  
- Aspose.Cells 25.3+ (licenza di prova, temporanea o permanente).  

## Configurare Aspose.Cells per Java

Aggiungi la libreria al tuo progetto con una delle seguenti opzioni:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Acquisizione della licenza
- **Free trial** – set completo di funzionalità per la valutazione.  
- **Temporary license** – rimuove i limiti della versione di prova mentre testi.  
- **Permanent license** – consigliata per carichi di lavoro di produzione.

Inizializza Aspose.Cells nel tuo codice Java:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guida passo‑passo

### 1. copyOptions con referToDestinationSheet

#### Panoramica
`CopyOptions` è l'oggetto di configurazione di Aspose.Cells che controlla come le formule e i riferimenti delle celle vengono gestiti durante un'operazione di copia. Impostare `CopyOptions.ReferToDestinationSheet` su `true` riscrive i riferimenti delle formule in modo che puntino al nuovo foglio dopo l'operazione di copia.

#### Passo 1: inizializzare workbook e fogli di lavoro  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Passo 2: configurare copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Passo 3: eseguire l'operazione di copia  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Perché è importante*: Le formule che originariamente facevano riferimento a `Sheet1` ora faranno correttamente riferimento a `DestSheet`, mantenendo i tuoi report automatizzati affidabili.

**Consiglio di risoluzione**: Se le formule fanno ancora riferimento al vecchio foglio, assicurati che `setReferToDestinationSheet(true)` sia chiamato **prima** della copia.

### 2. pasteOptions per valori‑solo dalle celle visibili

#### Panoramica
`PasteOptions` è l'oggetto delle impostazioni di Aspose.Cells che definisce cosa viene incollato. Usare `PasteType.VALUES` insieme a `onlyVisibleCells=true` copia solo i valori visualizzati, ignorando righe/colonne nascoste e la formattazione.

#### Passo 1: inizializzare workbook e fogli di lavoro  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Passo 2: configurare pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Passo 3: eseguire l'operazione di incolla  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Perché è importante*: Ideale per estrarre dati filtrati o generare report puliti senza righe nascoste o rumore di formattazione.

**Consiglio di risoluzione**: Verifica che righe/colonne siano effettivamente nascoste in Excel prima della copia; altrimenti verranno incluse.

## Applicazioni pratiche
1. **Financial consolidation** – unire i fogli mensili in un workbook master mantenendo tutte le formule accurate.  
2. **Filtered data export** – estrarre solo le righe visibili da una tabella filtrata in un foglio di riepilogo.  
3. **Scheduled report generation** – automatizzare la creazione notturna di report Excel con valori di cella precisi e riferimenti corretti.

## Considerazioni sulle prestazioni
- Quando hai finito, **Dispose of workbooks** (`wb.dispose();`) per liberare le risorse native.  
- **Batch operations** – raggruppa più chiamate di copia/incolla per ridurre l'overhead.  
- **Monitor memory** – i workbook di grandi dimensioni possono richiedere un heap aumentato (`-Xmx2g`).  
- Aspose.Cells supporta **oltre 50 formati di input e output** e può elaborare workbook con **fino a 2 milioni di righe** senza caricare l'intero file in memoria, offrendo prestazioni ad alto rendimento per carichi di lavoro aziendali.

## Domande frequenti

**Q: A cosa serve `CopyOptions.ReferToDestinationSheet`?**  
A: Riscrive i riferimenti delle formule in modo che puntino al foglio di destinazione dopo una copia, garantendo che le formule dei report rimangano corrette.

**Q: Come incollare solo le celle visibili?**  
A: Imposta `PasteOptions.setOnlyVisibleCells(true)` e scegli `PasteType.VALUES`.

**Q: Posso usare Aspose.Cells senza acquistare una licenza?**  
A: Sì, è disponibile una versione di prova gratuita o una licenza temporanea per la valutazione, ma è necessaria una licenza permanente per la produzione.

**Q: Perché alcuni riferimenti sono ancora errati dopo la copia?**  
A: Verifica che `ReferToDestinationSheet` sia abilitato **prima** dell'operazione di copia e che le formule di origine non contengano collegamenti a workbook esterni.

**Q: Quali best practice di gestione della memoria dovrei seguire?**  
A: Disporre degli oggetti `Workbook` al termine, elaborare file di grandi dimensioni a blocchi e monitorare l'uso dell'heap JVM.

**Q: È possibile combinare CopyOptions e PasteOptions in un'unica operazione?**  
A: Sì, puoi concatenarli copiando prima con `CopyOptions` e poi applicando `PasteOptions` sull'intervallo di destinazione.

## Risorse
- **Documentazione**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Acquisto**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free trial**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Licenza temporanea**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Forum di supporto**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Ultimo aggiornamento:** 2026-10-28  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose

## Tutorial correlati

- [Leggi file Excel Java – Manipolazione avanzata delle celle del workbook con Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Aggiungi dati a una cella in Excel usando Aspose.Cells per Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Converti indici di riga e colonna delle celle Excel con Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}