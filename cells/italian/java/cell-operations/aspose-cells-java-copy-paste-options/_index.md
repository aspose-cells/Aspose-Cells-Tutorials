---
date: '2026-02-22'
description: Scopri come automatizzare la creazione di report Excel con Aspose.Cells
  in Java utilizzando CopyOptions e PasteOptions per mantenere le formule accurate
  e incollare solo i valori visibili.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatizza la generazione di report Excel – Padroneggiare CopyOptions e PasteOptions
  in Java con Aspose.Cells
url: /it/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

6-02-22  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose

Now produce final content with all translations and unchanged elements.

Check for any other text: "step‑by‑step guide" we translated.

Make sure to keep markdown formatting exactly.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizzare la generazione di report Excel con Aspose.Cells: CopyOptions & PasteOptions in Java

Stai cercando di **automatizzare la generazione di report Excel** usando Java? Con Aspose.Cells puoi copiare, incollare e regolare le formule in modo programmatico così i tuoi report rimangono accurati e vengono trasferiti solo i dati di cui hai bisogno. In questo tutorial esamineremo due funzionalità essenziali—**CopyOptions.ReferToDestinationSheet** e **PasteOptions**—che ti consentono di preservare i riferimenti delle formule e incollare i valori solo dalle celle visibili.

## Risposte rapide
- **Cosa fa `CopyOptions.ReferToDestinationSheet`?** Regola le formule per puntare al foglio di destinazione durante la copia dei dati.  
- **Come posso incollare solo le celle visibili?** Imposta `PasteOptions.setOnlyVisibleCells(true)` con `PasteType.VALUES`.  
- **Quale versione della libreria è necessaria?** Aspose.Cells 25.3 o successiva.  
- **È necessaria una licenza per la produzione?** Sì, una licenza permanente o temporanea rimuove i limiti di valutazione.  
- **Posso usare Maven o Gradle?** Entrambi sono supportati; vedi gli snippet di dipendenza qui sotto.

## Cos'è “automatizzare la generazione di report Excel”?
Automatizzare la generazione di report Excel significa creare, consolidare e formattare cartelle di lavoro Excel in modo programmatico, eliminando le operazioni manuali di copia‑incolla e riducendo gli errori. Aspose.Cells fornisce un'API ricca che consente agli sviluppatori Java di manipolare i fogli di calcolo su larga scala.

## Perché usare CopyOptions e PasteOptions per i report?
- **Mantenere l'integrità delle formule** quando si spostano dati tra fogli.  
- **Escludere righe/colonne nascoste** per mantenere i report puliti e focalizzati.  
- **Migliorare le prestazioni** copiando solo i dati necessari invece di interi intervalli.

## Prerequisiti
- Java 8 o superiore.  
- Maven o Gradle per la gestione delle dipendenze.  
- Aspose.Cells 25.3+ (licenza trial, temporanea o permanente).  

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
- **Free Trial** – Set completo di funzionalità per la valutazione.  
- **Temporary License** – Rimuove le limitazioni della versione di prova mentre testi.  
- **Permanent License** – Consigliata per carichi di lavoro in produzione.

Inizializza Aspose.Cells nel tuo codice Java:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guida passo‑passo

### 1. CopyOptions con ReferToDestinationSheet

#### Panoramica
Impostare `CopyOptions.ReferToDestinationSheet` su `true` riscrive i riferimenti delle formule in modo che puntino al nuovo foglio dopo l'operazione di copia.

#### Passo 1: Inizializzare Workbook e Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Passo 2: Configurare CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Passo 3: Eseguire l'operazione di copia
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Perché è importante*: Le formule che originariamente facevano riferimento a `Sheet1` ora faranno correttamente riferimento a `DestSheet`, mantenendo i tuoi report automatizzati affidabili.

**Suggerimento per la risoluzione dei problemi**: Se le formule fanno ancora riferimento al vecchio foglio, assicurati che `setReferToDestinationSheet(true)` sia chiamato **prima** della copia.

### 2. PasteOptions per valori‑solo dalle celle visibili

#### Panoramica
`PasteOptions` ti consente di definire cosa viene incollato. Usare `PasteType.VALUES` insieme a `onlyVisibleCells=true` copia solo i valori visualizzati, ignorando righe/colonne nascoste e formattazione.

#### Passo 1: Inizializzare Workbook e Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Passo 2: Configurare PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Passo 3: Eseguire l'operazione di incolla
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Perché è importante*: Ideale per estrarre dati filtrati o generare report puliti senza righe nascoste o rumore di formattazione.

**Suggerimento per la risoluzione dei problemi**: Verifica che righe/colonne siano effettivamente nascoste in Excel prima della copia; altrimenti verranno incluse.

## Applicazioni pratiche
1. **Consolidamento finanziario** – Unire i fogli mensili in un workbook master mantenendo tutte le formule accurate.  
2. **Esportazione dati filtrati** – Estrarre solo le righe visibili da una tabella filtrata in un foglio di riepilogo.  
3. **Generazione di report programmata** – Automatizzare la creazione notturna di report Excel con valori di cella precisi e riferimenti corretti.

## Considerazioni sulle prestazioni
- **Disporre dei Workbook** quando terminato (`wb.dispose();`) per liberare le risorse native.  
- **Operazioni batch** – Raggruppare più chiamate di copia/incolla per ridurre l'overhead.  
- **Monitorare la memoria** – Workbook di grandi dimensioni potrebbero richiedere un heap aumentato (`-Xmx2g`).

## Domande frequenti

**Q1: A cosa serve `CopyOptions.ReferToDestinationSheet`?**  
R: Riscrive i riferimenti delle formule in modo che puntino al foglio di destinazione dopo una copia, garantendo che le formule dei report rimangano corrette.

**Q2: Come incollare solo le celle visibili?**  
R: Imposta `PasteOptions.setOnlyVisibleCells(true)` e scegli `PasteType.VALUES`.

**Q3: Posso usare Aspose.Cells senza acquistare una licenza?**  
R: Sì, è disponibile una versione di prova gratuita o una licenza temporanea per la valutazione, ma è necessaria una licenza permanente per la produzione.

**Q4: Perché alcuni riferimenti sono ancora errati dopo la copia?**  
R: Verifica che `ReferToDestinationSheet` sia abilitato **prima** dell'operazione di copia e che le formule di origine non contengano collegamenti a workbook esterni.

**Q5: Quali best practice di gestione della memoria dovrei seguire?**  
R: Disporre degli oggetti `Workbook` al termine, elaborare file di grandi dimensioni a blocchi e monitorare l'uso dell'heap JVM.

**Q6: È possibile combinare CopyOptions e PasteOptions in un'unica operazione?**  
R: Sì, puoi concatenarli copiando prima con `CopyOptions` e poi applicando `PasteOptions` sull'intervallo di destinazione.

## Risorse
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free Trial**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support Forum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ultimo aggiornamento:** 2026-02-22  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose