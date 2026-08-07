---
category: general
date: 2026-07-16
description: Imposta separatore di cella personalizzato durante l'esportazione di
  una tabella Excel in TXT usando Aspose.Cells. Scopri come esportare le formule Excel
  in testo e salvare il foglio di lavoro come file txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: it
lastmod: 2026-07-16
og_description: Impostare un separatore di celle personalizzato in Aspose.Cells consente
  di esportare una tabella Excel in TXT con formattazione esatta. Esporta le formule
  di Excel in testo e salva il foglio di lavoro come file txt facilmente.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Imposta separatore di cella personalizzato – Esporta tabella Excel in TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Imposta separatore di cella personalizzato – Esporta tabella Excel in TXT
url: /it/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta Separatore di Celle Personalizzato – Esporta Tabella Excel in TXT

Impostare un separatore di celle personalizzato è il tocco segreto di cui hai bisogno quando desideri un dump di testo ordinato da un foglio Excel. Ti sei mai chiesto come **esportare una tabella Excel in txt** senza finire con un caos di virgole e interruzioni di riga? In questo tutorial percorreremo l’intero processo usando Aspose.Cells per Java, dal caricamento di una cartella di lavoro al **salvataggio del foglio di lavoro come file txt** con un delimitatore a tua scelta.

## Cosa Imparerai

- Come **impostare un separatore di celle personalizzato** per le esportazioni di testo.
- I passaggi esatti per **esportare le formule Excel in testo** così i valori valutati viaggiano con te.
- Modi per **esportare i dati Excel come testo semplice** preservando il layout.
- Un esempio di codice completo, pronto all’uso, che puoi copiare‑incollare nel tuo progetto.

Alla fine di questa guida sarai in grado di prendere qualsiasi cartella di lavoro Excel, scegliere una barra verticale (`|`), una tabulazione (`\t`) o qualsiasi altro carattere, e produrre un file di testo delimitato pulito che i sistemi a valle adoreranno.

### Prerequisiti

- Java 8 o versione più recente installata.
- Maven (o qualsiasi strumento di build) per includere la libreria Aspose.Cells per Java.
- Una cartella di lavoro di esempio (`TableDemo.xlsx`) che contiene una tabella con formule.

Se hai tutto questo, immergiamoci—senza fronzoli, solo passaggi pratici.

## Passo 1: Aggiungi Aspose.Cells al Tuo Progetto

Prima di poter **impostare un separatore di celle personalizzato**, devi avere il JAR di Aspose.Cells nel classpath. Il modo più semplice è tramite Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Se preferisci Gradle, sostituisci l’XML con l’equivalente `implementation 'com.aspose:aspose-cells:24.10'`. Una volta risolta la dipendenza, sei pronto a scrivere codice Java che interagisce con i file Excel.

## Passo 2: Carica la Cartella di Lavoro – Preparazione all’Esportazione della Tabella Excel in TXT

La prima riga di codice reale è sempre la stessa: apri la cartella di lavoro che contiene la tabella da esportare.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Qui recuperiamo il primo foglio di lavoro (`get(0)`). Se i tuoi dati si trovano su un foglio diverso, cambia semplicemente l’indice o usa `get("SheetName")`. Questa parte è essenziale per **esportare una tabella Excel in txt** perché l’esportatore opera a livello di foglio di lavoro.

## Passo 3: Imposta Separatore di Celle Personalizzato – Il Cuore dell’Esportazione

Ora arriva la star dello spettacolo: configurare `ExportTableOptions`. Questo oggetto ti consente di decidere esattamente come appare ogni cella nel file di testo finale.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Perché **impostare un separatore di celle personalizzato**? Perché il separatore predefinito è una tabulazione, che può entrare in conflitto con dati che già contengono tabulazioni. Scegliendo una barra verticale (`|`) o un punto e virgola, garantisci che ogni colonna rimanga distinta quando un parser a valle legge il file.

### Esporta Formule Excel in Testo

La riga `setFormulaValueInCell(true)` indica ad Aspose.Cells di scrivere le **esportare le formule Excel in testo** come *risultato* della formula, non come stringa della formula stessa. Se ometti questa impostazione, una cella contenente `=SUM(A1:A5)` apparirebbe come `=SUM(A1:A5)` nel TXT, cosa raramente desiderata.

## Passo 4: Collega le Opzioni di Esportazione alle Opzioni di Salvataggio TXT

Ora colleghiamo quelle opzioni di tabella alla configurazione complessiva di esportazione TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` è l’oggetto ombrello che controlla come viene scritto l’intero foglio di lavoro. Inserendo `exportTableOptions` al suo interno, ti assicuri che ogni tabella nel foglio rispetti la regola **imposta separatore di celle personalizzato**.

## Passo 5: Salva il Foglio di Lavoro come File TXT – Concludi l’Esportazione

Infine, scriviamo il file su disco.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Eseguendo questo programma si crea `TableExported.txt`. Ogni riga della tabella Excel originale apparirà ora come una linea di valori separati da barre verticali, ad esempio:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Nota come la formula nella colonna **Total** è stata valutata prima di essere scritta—grazie a `setFormulaValueInCell(true)`. Questa è l’essenza di **esportare i dati Excel come testo semplice** preservando i risultati calcolati.

## Passo 6: Verifica l’Uscita – È Come Ti Aspetti?

Apri il `TableExported.txt` generato con qualsiasi editor di testo. Dovresti vedere:

- Una riga per ogni riga di Excel.
- Colonne separate dal carattere pipe che hai impostato con `setCellValueSeparator`.
- Nessuna virgola o tabulazione indesiderata, a meno che non fossero parte dei valori originali delle celle.
- Risultati delle formule, non le formule stesse.

Se noti caratteri inattesi, ricontrolla il separatore scelto. Alcuni caratteri (come la pipe) sono sicuri per la maggior parte dei parser in stile CSV, ma se i tuoi dati contengono già pipe, considera un delimitatore diverso come `~` o una tabulazione (`\t`).

## Suggerimenti, Casi Limite e Buone Pratiche – Esporta Dati Excel come Testo Semplice

| Situazione | Cosa Fare |
|------------|-----------|
| **I dati contengono già il separatore scelto** | Passa a un carattere meno comune (`^`, `~` o caratteri Unicode non stampabili). |
| **Hai bisogno della codifica UTF‑8** |  |

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Salva Excel come File di Testo con Separatore Personalizzato usando Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Salva Excel Testo Separatore Personalizzato Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Sauvegarder Excel Texte Séparateur Personnalisé Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}