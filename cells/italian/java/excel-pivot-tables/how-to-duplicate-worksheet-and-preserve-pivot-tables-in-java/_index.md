---
category: general
date: 2026-08-17
description: Come duplicare un foglio di lavoro in Java usando Aspose.Cells, preservando
  la tabella pivot, copiando la pivot in una nuova cartella di lavoro e creando una
  cartella di lavoro da un foglio.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: it
lastmod: 2026-08-17
og_description: Come duplicare un foglio di lavoro in Java usando Aspose.Cells, preservando
  la tabella pivot, copiando la pivot in una nuova cartella di lavoro e creando una
  cartella di lavoro da un foglio—tutti i passaggi spiegati.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Come duplicare un foglio di lavoro e mantenere le tabelle pivot – Guida
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Come duplicare un foglio di lavoro e preservare le tabelle pivot in Java
url: /it/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come duplicare un foglio di lavoro e preservare le tabelle pivot in Java

Duplicare un foglio di lavoro mantenendo intatta la sua tabella pivot è una necessità frequente quando si automatizza la generazione di report Excel. Questa guida mostra come copiare una pivot in una nuova cartella di lavoro usando Aspose.Cells per Java, e copre anche come preservare la pivot quando si crea una cartella di lavoro da un foglio.

Imparerai come caricare una cartella di lavoro esistente, duplicare il foglio che contiene una tabella pivot e salvare il risultato come un nuovo file. Il tutorial presuppone che tu abbia un ambiente di sviluppo Java di base e una licenza valida di Aspose.Cells (la valutazione gratuita è sufficiente per i test). Non sono necessari strumenti esterni oltre al JAR di Aspose.Cells.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java Development Kit (JDK) 8 o versioni successive.
* Maven o Gradle per gestire la dipendenza Aspose.Cells.
* Un file Excel (`source.xlsx`) che contenga almeno una tabella pivot nel primo foglio.
* Una directory in cui poter leggere il file sorgente e scrivere la cartella di lavoro duplicata.

Aggiungi la dipendenza Aspose.Cells al tuo `pom.xml` (Maven) o `build.gradle` (Gradle). Per Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Come duplicare un foglio di lavoro con una tabella pivot

L'operazione principale è un processo in tre passaggi: caricare, copiare e salvare. Ogni passaggio è spiegato di seguito.

### Passo 1 – Caricare la cartella di lavoro che contiene la tabella pivot

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Perché questo passaggio è importante*: L'oggetto `Workbook` rappresenta l'intero file Excel. Recuperando il primo foglio (`get(0)`), individui il foglio che contiene la tabella pivot che desideri duplicare.

### Passo 2 – Creare una nuova cartella di lavoro e duplicare l'intero foglio

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` clona il foglio **inclusi** tutti gli oggetti incorporati, le formule e le cache delle pivot. Questo è il metodo consigliato per **come copiare la pivot** perché la definizione della pivot e la sua origine dati vengono trasferite insieme.

### Passo 3 – Salvare la nuova cartella di lavoro

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Dopo l'esecuzione, `copy_with_pivot.xlsx` contiene una copia esatta del foglio originale, e la tabella pivot funziona senza configurazioni aggiuntive.

**Risultato atteso**: Aprendo `copy_with_pivot.xlsx` in Excel vedrai il foglio duplicato con lo stesso layout della pivot, filtri e campi calcolati del file sorgente.

## Come copiare una pivot in un'altra cartella di lavoro

Se devi spostare una tabella pivot senza copiare l'intero foglio, puoi estrarre la cache della pivot e allegarla a un nuovo foglio. Il frammento seguente dimostra questo approccio:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Questo codice risponde a **come copiare la pivot** copiando solo l'oggetto pivot, non l'intero foglio. Il metodo `addCopy` sulla collezione `PivotTables` garantisce che la cache della pivot venga duplicata, soddisfacendo i requisiti di **come preservare la pivot**.

## Come preservare la pivot quando si crea una cartella di lavoro da un foglio

A volte si parte da un foglio che non appartiene a una cartella di lavoro (ad esempio, si genera un foglio in memoria). Per **creare una cartella di lavoro da un foglio** mantenendo la pivot, segui questi passaggi:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Aggiungendo il foglio a un nuovo `Workbook` dopo che la pivot è stata completamente definita, garantisci che **come preservare la pivot** funzioni anche quando il foglio proviene da un file esterno.

## Suggerimenti pratici e errori comuni

| Suggerimento | Perché è importante |
|-----|----------------|
| Usa `addCopy` invece di `copy` | `addCopy` clona la cache della pivot sottostante; un semplice `copy` potrebbe perdere la connessione all'origine dati. |
| Mantieni i file sorgente e destinazione sullo stesso file system | I percorsi relativi nell'origine dati della pivot vengono risolti correttamente, riducendo gli errori “source not found”. |
| Verifica la cache della pivot dopo la copia | Chiama `pivot.refresh()` se i dati sorgente sono cambiati tra l'operazione di copia e il salvataggio. |
| Rilascia le cartelle di lavoro al termine | `sourceWorkbook.dispose();` libera le risorse native, importante per file di grandi dimensioni. |

## Casi limite che potresti incontrare

* **Più fogli con pivot interdipendenti** – Copia ogni foglio singolarmente; le cache condivise vengono duplicate automaticamente, ma potresti dover riassegnare le connessioni dati esterne.
* **Tabelle pivot basate su query SQL esterne** – Assicurati che l'ambiente di destinazione possa accedere allo stesso database; altrimenti la pivot mostrerà errori “#REF!”. 
* **Cartelle di lavoro di grandi dimensioni (>100 MB)** – Usa `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` per ridurre la pressione sulla memoria durante l'operazione di copia.

## Esempio completo e eseguibile

Di seguito trovi il programma completo che incorpora tutti i passaggi discussi. Salvalo come `CopyPivotTable.java`, regola i percorsi dei file e eseguilo con il tuo IDE preferito o tramite `javac`/`java`.



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Come aggiornare l'origine della tabella pivot di Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Come implementare i filtri (Slicers) nelle tabelle pivot usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}