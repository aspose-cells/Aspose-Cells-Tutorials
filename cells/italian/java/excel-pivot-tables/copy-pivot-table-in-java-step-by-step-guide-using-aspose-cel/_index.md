---
category: general
date: 2026-08-04
description: Copia la tabella pivot con Aspose.Cells per Java. Scopri come copiare
  un intervallo Excel, duplicare una tabella pivot e copiare un foglio di lavoro con
  la pivot in poche righe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: it
lastmod: 2026-08-04
og_description: Copia la tabella pivot usando Aspose.Cells per Java. Questo tutorial
  ti guida nella copia di un intervallo Excel, nella duplicazione di una tabella pivot
  e nella conservazione di tutti i dati in un nuovo foglio di lavoro.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Copia tabella pivot in Java – tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Copia tabella pivot in Java – guida passo‑passo con Aspose.Cells
url: /it/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiare una tabella pivot in Java – guida passo‑a‑passo con Aspose.Cells

Se hai bisogno di **copiare una tabella pivot** da un foglio di lavoro a un altro in Java, questa guida ti mostra esattamente come farlo con Aspose.Cells. Che tu stia generando report in modo programmatico o costruendo uno strumento di migrazione dati, vedrai un esempio completo e eseguibile che preserva la definizione e i dati della tabella pivot.

Copiare una tabella pivot è più che copiare un intervallo di celle; la cache sottostante e la fonte dati devono rimanere intatte. In questo tutorial copriamo anche come **copiare un intervallo Excel**, come **duplicare una tabella pivot** tra fogli di lavoro e come **copiare un foglio con pivot** usando la stessa API.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java Development Kit (JDK) 8 o più recente.
* Maven o Gradle per gestire le dipendenze.
* Aspose.Cells for Java (l'ultima versione, ad es., 23.12). Aggiungi la seguente coordinata Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Un workbook di origine (`Source.xlsx`) che contiene una tabella pivot nel primo foglio di lavoro.

## Come copiare una tabella pivot in Java con Aspose.Cells

L'idea principale è copiare il *range di origine* che racchiude la tabella pivot e poi incollarlo in un nuovo foglio di lavoro. Aspose.Cells copia automaticamente la cache pivot, così il foglio risultante contiene una **tabella pivot duplicata** pienamente funzionale.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Perché funziona

* **La copia dell'intervallo include la cache pivot** – Aspose.Cells tratta una tabella pivot come un oggetto speciale incorporato nell'intervallo di celle. Quando chiami `Range.copy`, la libreria copia sia le celle visibili sia la cache nascosta che alimenta la pivot.
* **Nessuna ricreazione manuale necessaria** – Non devi ricostruire i campi pivot o la fonte dati; il duplicato è pronto per essere aggiornato immediatamente.
* **Funziona con qualsiasi versione di Excel** – Il file generato segue lo standard Office Open XML (XLSX), quindi Excel 2007+ lo può aprire senza avvisi.

## Copiare un intervallo Excel – riutilizzare lo stesso codice per dati non‑pivot

Se ti serve solo **copiare un intervallo Excel** senza una tabella pivot, lo stesso schema vale. Basta adeguare l'indirizzo dell'intervallo alla zona che desideri duplicare.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Il metodo `copy` preserva formule, formattazione e commenti, rendendolo una soluzione universale per qualsiasi blocco di dati Excel.

## Duplicare una tabella pivot su più fogli di lavoro

A volte è necessario **duplicare una tabella pivot** più volte — ad esempio una per dipartimento. Scorri i fogli di destinazione e riutilizza la stessa chiamata `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Ogni nuovo foglio contiene una pivot indipendente che può essere aggiornata separatamente. La cache viene duplicata, quindi le modifiche in un foglio non influenzano gli altri.

## Copiare un foglio con pivot – preservare le impostazioni a livello di foglio

Se vuoi **copiare un foglio con pivot** mantenendo anche la configurazione di pagina, le larghezze delle colonne e gli intervalli denominati, usa `Worksheet.copy` invece di copiare manualmente un intervallo. Questo metodo clona l'intero foglio, inclusa la tabella pivot.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` è comodo quando il foglio contiene grafici, immagini o stili personalizzati che devono viaggiare insieme alla pivot.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Cache pivot persa dopo la copia** | Usare `Cell.copy` su singole celle (invece di un intervallo) elimina la cache nascosta. | Copiare sempre l'*intero* intervallo che racchiude la tabella pivot, come mostrato al Passo 2. |
| **Intervallo di origine troppo piccolo** | L'intervallo non include l'area dati della pivot, quindi il nuovo foglio mostra solo valori statici. | Espandere l'indirizzo (es., `A1:G20`) per coprire l'intera tabella pivot più eventuali slicer o filtri. |
| **Mancata corrispondenza della versione della cartella di lavoro di destinazione** | Salvare come XLS (legacy) rimuove le funzionalità pivot moderne. | Salvare come XLSX (predefinito) o impostare esplicitamente `SaveFormat.XLSX`. |
| **Fonte dati esterna interrotta** | La pivot punta a una fonte dati esterna al workbook; la copia non la incorpora. | Usare `PivotTable.refreshData()` dopo la copia, o incorporare i dati di origine nella stessa cartella di lavoro. |

## Output previsto

Dopo aver eseguito il programma:

1. `CopyWithPivot.xlsx` appare in `YOUR_DIRECTORY`.
2. L'apertura del file in Excel mostra un nuovo foglio chiamato **CopySheet**.
3. **CopySheet** contiene una tabella pivot pienamente funzionale, identica all'originale, pronta per l'aggiornamento.
4. Tutta la formattazione, i filtri e i campi calcolati sono preservati.

Se apri `FullCopy.xlsx`, vedrai una replica completa del foglio originale, inclusi eventuali grafici o immagini presenti nel foglio di origine.

## Riepilogo

* Hai imparato a **copiare una tabella pivot** in Java usando Aspose.Cells.
* Lo stesso approccio funziona per scenari di **copiare un intervallo Excel** o **copiare range java**.
* Per operazioni in batch, puoi **duplicare una tabella pivot** su molti fogli.
* Quando ti serve l'intero foglio, **copiare un foglio con pivot** usando `addCopy`.

## Prossimi passi

* Esplora **PivotTable.refreshData()** per aggiornare programmaticamente la cache dopo la copia.
* Combina la logica di copia con **Excel file streaming** per gestire workbook di grandi dimensioni senza caricare tutto in memoria.
* Dai un'occhiata al supporto di Aspose.Cells per **pivot slicers** se i tuoi report dipendono da filtri interattivi.

Sentiti libero di adattare il codice alla struttura del tuo progetto, sperimentare con diverse dimensioni di intervallo o integrarlo in una pipeline di elaborazione dati più ampia. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Come aggiornare la fonte di una tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipolazione di tabelle pivot Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Creare un nuovo workbook Excel – Copia & Duplica tabella pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}