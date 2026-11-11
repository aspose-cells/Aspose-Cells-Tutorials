---
category: general
date: 2026-10-26
description: Scopri come copiare una tabella pivot in una nuova cartella di lavoro
  usando Java, preservando la formattazione e la definizione della pivot mentre copi
  un intervallo Excel con formattazione tramite Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: it
lastmod: 2026-10-26
og_description: Copia la tabella pivot in una nuova cartella di lavoro in Java con
  Aspose.Cells. Questa guida mostra come copiare l’intervallo Excel, preservare la
  formattazione e creare una cartella di lavoro vuota in modo efficiente.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Copia tabella pivot in una nuova cartella di lavoro in Java – guida passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come copiare una tabella pivot in una nuova cartella di lavoro in Java
url: /it/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in una nuova cartella di lavoro in Java

Se hai bisogno di **copy pivot table** da un file Excel a un altro, questa guida ti mostra una soluzione completa e eseguibile. Vedrai come preservare la definizione della pivot, mantenere tutta la formattazione e evitare le insidie più comuni quando si copia un intervallo Excel.

Copiare una tabella pivot solleva spesso domande come *come copiare una pivot* senza rompere l'origine dati o perdere gli stili. Alla fine di questo tutorial avrai un programma Java autonomo che crea una cartella di lavoro vuota, copia l’intervallo desiderato e salva il risultato con la pivot intatta.

## Cosa otterrai

* Caricare una cartella di lavoro sorgente che contiene una tabella pivot.  
* **Create empty workbook** che riceverà i dati copiati.  
* **Copy excel range** che include la pivot, usando opzioni che mantengono la pivot e la formattazione.  
* Salvare il file di destinazione e verificare che la pivot funzioni esattamente come l’originale.

### Prerequisiti

* Java 17 o successiva.  
* Aspose.Cells per Java (versione 23.10 o più recente).  
* Familiarità di base con gli IDE Java (IntelliJ IDEA, Eclipse, ecc.).  

> **Suggerimento professionale:** Usa la licenza di valutazione gratuita di Aspose.Cells per i test rapidi; sostituiscila con una licenza completa prima dell’uso in produzione.

## Copiare la tabella pivot in una nuova cartella di lavoro

Il primo passo è impostare le cartelle di lavoro sorgente e di destinazione. La destinazione inizia con una chiamata **create empty workbook**, che ti fornisce un file pulito con un unico foglio.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Perché funziona

* `new Workbook()` **creates empty workbook** con un foglio predefinito, evitando la necessità di eliminare dati esistenti.  
* `CopyOptions` indica ad Aspose.Cells di copiare i metadati della **pivot table**, non solo i valori grezzi. La modalità `PASTE_ALL` trasporta anche gli stili delle celle, i formati numerici e la formattazione condizionale—soddisfacendo il requisito di **copy range with formatting**.  
* `copyRange` esegue un’operazione di **copy excel range** che rispetta le strutture interne della sorgente, così la pivot rimane funzionale dopo la copia.

## Come copiare una pivot senza perdere la formattazione

Se utilizzi solo le `CopyOptions` predefinite, alcune informazioni di stile potrebbero essere omesse nelle versioni più vecchie di Aspose.Cells. Impostare esplicitamente il tipo di incolla garantisce che **copy range with formatting** venga rispettato.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Aggiungere `setPasteSpecialType` assicura che larghezze delle colonne, altezze delle righe e persino le regole di convalida dei dati vengano trasferite con l’intervallo. Questo è particolarmente utile quando la tabella pivot si estende su più colonne con larghezze personalizzate.

## Creare una cartella di lavoro vuota prima di copiare

A volte gli sviluppatori tentano di copiare in una cartella di lavoro esistente che contiene già dati. Questo può causare sovrapposizioni di intervalli o sovrascritture inattese. Iniziare con una chiamata **create empty workbook** isola l’operazione:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Se ti serve più di un foglio nella destinazione, puoi aggiungerli dopo la copia:

```java
destWb.getWorksheets().add("Summary");
```

## Copiare un intervallo Excel con formattazione usando CopyOptions

Oltre alle tabelle pivot, lo stesso schema funziona per qualsiasi **copy excel range** che richieda la conservazione della formattazione—grafici, tabelle o formati condizionali.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

L’istanza di `CopyOptions` rimane la stessa, così ottieni un comportamento coerente su diversi intervalli.

### Casi limite da considerare

| Situazione                              | Gestione consigliata |
|----------------------------------------|----------------------|
| La cartella di lavoro sorgente ha più pivot   | Copia separatamente l’intervallo di ciascuna pivot o copia l’intero foglio. |
| La destinazione contiene già dati      | Scegli una cella di partenza non conflittuale (es. "H1") quando chiami `copyRange`. |
| L’origine dati della pivot è esterna (es. DB) | Assicurati che la cartella di lavoro di destinazione punti alla stessa origine dati esterna, o aggiorna la pivot dopo la copia. |
| Cartella di lavoro grande ( > 10 MB )  | Aumenta la dimensione dell’heap Java (`-Xmx2g`) per evitare `OutOfMemoryError`. |

## Verificare il risultato

Dopo aver eseguito il programma, apri `destination.xlsx`. Dovresti vedere:

* Lo stesso layout della tabella pivot di `source.xlsx`.  
* Tutti i colori delle celle, i formati numerici e le larghezze delle colonne preservati.  
* L’origine dati della pivot punta ancora all’intervallo originale all’interno del nuovo file, così l’aggiornamento della pivot aggiorna correttamente i valori.

Se la pivot appare come una tabella statica, ricontrolla che `CopyOptions.setPasteType(PasteType.PASTE_ALL)` sia impostato. Senza questa opzione Aspose.Cells tratta la pivot come dati semplici.

## Conclusione

Ora sai come **copy pivot table** in una nuova cartella di lavoro in Java mantenendo formattazione, connessioni dati e layout del foglio. La soluzione completa dimostra come caricare un file sorgente, **create empty workbook**, configurare le opzioni di **copy excel range** e salvare il risultato.  

Da qui puoi approfondire argomenti correlati come **how to copy pivot** tra fogli diversi, incorporare grafici accanto alle pivot o automatizzare l’elaborazione batch di più cartelle di lavoro. Sperimenta con le impostazioni di `CopyOptions` per adattarle alle tue esigenze di automazione, e avrai a disposizione un toolkit robusto per la manipolazione di Excel.

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}