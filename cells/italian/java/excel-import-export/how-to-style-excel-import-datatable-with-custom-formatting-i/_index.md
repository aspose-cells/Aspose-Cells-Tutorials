---
category: general
date: 2026-07-03
description: Come formattare i file Excel usando Java. Impara a formattare la colonna
  data in Excel, applicare il formato numerico in Excel, esportare DataTable in XLSX
  e importare DataTable in Excel con Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: it
og_description: Come formattare i file Excel in Java. Questo tutorial mostra come
  formattare la data di una colonna in Excel, applicare il formato numerico in Excel,
  esportare DataTable in XLSX e importare DataTable in Excel.
og_title: Come stilizzare Excel – Guida Java per la formattazione personalizzata delle
  colonne
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Come formattare Excel – Importare DataTable con formattazione personalizzata
  in Java
url: /it/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come formattare Excel – Importare DataTable con formattazione personalizzata in Java

Ti sei mai chiesto **come formattare Excel** programmaticamente senza aprire il file manualmente? Non sei l'unico. Molti sviluppatori devono generare report in cui la prima colonna è in grassetto, la seconda mostra date e il resto segue un layout pulito. In questa guida percorreremo un esempio completo e funzionante che **importa una DataTable in Excel**, applica un'intestazione in grassetto, formatta una colonna data e infine **esporta DataTable in XLSX**.  

Useremo Aspose.Cells per Java, ma i concetti si applicano a qualsiasi libreria che consenta di lavorare con gli stili. Alla fine avrai un modello riutilizzabile per **apply number format Excel** celle, **format column date Excel**, e per distribuire un workbook rifinito ai tuoi utenti.

## Prerequisiti

- Java 17 (o qualsiasi JDK recente)  
- Aspose.Cells per Java 23.9 o successivo (la versione di prova gratuita funziona bene)  
- Una struttura simile a `DataTable` (l'esempio utilizza un semplice mock)  
- Il tuo IDE preferito (IntelliJ IDEA, Eclipse, VS Code…)

Non sono richiesti plugin Maven aggiuntivi; basta aggiungere il JAR di Aspose.Cells al classpath.

---

## Passo 1: Ottenere la DataTable di origine – Preparazione “Export DataTable to XLSX”

Prima di poter **import datatable into excel**, ci serve un oggetto `DataTable` che rappresenti i dati da esportare. Nei progetti reali potresti prelevarli da un database, un file CSV o un'API. Per questo tutorial simuliamo una piccola tabella:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Perché è importante:** Ottenere i dati corretti fin dall'inizio permette al resto della logica di formattazione di concentrarsi esclusivamente sulla presentazione, non sulla manipolazione dei dati.

---

## Passo 2: Creare un array per contenere le definizioni di stile per ogni colonna

Aspose.Cells consente di passare un array **Style[]** durante l'importazione di una `DataTable`. Ogni elemento corrisponde a una colonna e determina come quella colonna apparirà dopo l'importazione. Allochiamo l'array in base al numero di colonne:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Suggerimento:** Se hai molte colonne, considera di costruire l'array in un ciclo e riutilizzare un unico oggetto `Style` dove la formattazione è identica. Questo riduce il consumo di memoria.

---

## Passo 3: Definire gli stili – Intestazione in grassetto e formattazione data

Ora rispondiamo alla classica domanda **format column date excel** e dimostriamo anche **apply number format excel** per le altre colonne.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Cosa succede qui?**  
- `StyleNumberFormat.DATE` indica a Excel di trattare il valore della cella come una data breve (es., *31/01/2024*).  
- `StyleNumberFormat.CURRENCY_USD` aggiunge automaticamente il simbolo `$` e due decimali.  
- Impostare il font in grassetto sulla prima colonna fa risaltare l'intestazione, requisito frequente quando **how to style excel** fogli di calcolo per leggibilità.

> **Caso limite:** Se i dati di origine contengono già stringhe formattate, potresti doverle convertire in oggetti `java.util.Date` prima dell'importazione; altrimenti Excel le tratterà come testo semplice.

---

## Passo 4: Creare un nuovo Workbook e accedere al suo primo Worksheet

Un workbook nuovo ci offre una tela pulita. Preleveremo il primo worksheet, dove avverrà l'importazione.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Perché un nuovo workbook?** Partire da zero garantisce che nessuno stile residuo o righe nascoste interferiscano con l'output finale—essenziale quando **how to style excel** file in modo coerente tra più esecuzioni.

---

## Passo 5: Importare la DataTable con gli stili di colonna

Ecco il cuore dell'operazione: inserire la `DataTable` nel foglio applicando l'array di stili che abbiamo creato.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Spiegazione:**  
- `importDataTable` copia sia la riga di intestazione sia le righe di dati.  
- L'array `columnStyles` è allineato con ogni colonna, così l'intestazione della prima colonna diventa grassetto, la seconda colonna mostra le date e la terza appare come valuta.  
- Questa singola riga sostituisce decine di passaggi manuali di formattazione cella‑per‑cella, illustrando un modo pulito per **apply number format excel** programmaticamente.

---

## Passo 6: Salvare il Workbook formattato – Completa “Export DataTable to XLSX”

Infine persi stiamo il workbook su disco. Regola il percorso verso una cartella scrivibile sul tuo computer.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Apri il file in Excel e dovresti vedere:

- Intestazione colonna **ID** in grassetto.  
- Colonna **OrderDate** formattata come data (es., *27/04/2024*).  
- Colonna **Total** visualizzata con il simbolo del dollaro e due decimali.

> **Consiglio esperto:** Se devi supportare versioni più vecchie di Excel, chiama `workbook.save(outputPath, SaveFormat.XLS)` invece del default XLSX.

---

## Passo 7: Verificare il risultato e aggiustamenti opzionali

È buona pratica ricontrollare il file generato, soprattutto quando si automatizzano report per stakeholder.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Se `isBold` stampa `true`, la tua routine **how to style excel** ha funzionato correttamente. Da qui puoi:

- Aggiungere formattazione condizionale (es., evidenziare totali > $200).  
- Bloccare la riga superiore per una scorrimento più agevole.  
- Inserire un grafico che faccia riferimento ai dati importati.

Tutte queste estensioni seguono lo stesso schema: definire un `Style`, applicarlo e salvare.

---

## Domande frequenti e casi limite

| Domanda | Risposta |
|----------|--------|
| **Posso stilizzare più di una colonna allo stesso modo?** | Sì—riutilizza una singola istanza `Style` per tutte le colonne che condividono la stessa formattazione. |
| **Cosa succede se la mia DataTable ha più colonne degli stili?** | Qualsiasi colonna senza una voce corrispondente in `columnStyles` utilizzerà lo stile predefinito. |
| **Come cambio il formato data in “dd‑MMM‑yyyy”?** | Usa `columnStyles[1].setCustom("#dd-MMM-yyyy#");` al posto del valore predefinito `DATE`. |
| **C'è un modo per auto‑dimensionare le colonne dopo l'import?** | Chiama `worksheet.autoFitColumns();` dopo `importDataTable`. |
| **Funziona su Linux/macOS?** | Assolutamente—Aspose.Cells è indipendente dalla piattaforma purché tu abbia una JDK compatibile. |

---

## Conclusione

Ora disponi di un esempio completo, end‑to‑end, di **how to style Excel** workbooks tramite **importing datatable into excel**, **format column date excel**, e **apply number format excel** usando Java. Il codice mostra il flusso completo dall'**export datatable to xlsx** all'apertura del file in Excel, coprendo sia il *cosa* sia il *perché* di ogni passaggio.  

Provalo: modifica l'array di stili, aggiungi altre colonne o collega una query reale al database. Lo stesso schema ti permetterà di generare report dall'aspetto professionale con un click, senza alcuna formattazione manuale.

---

![Foglio Excel formattato generato dal codice del tutorial](https://example.com/images/styled-worksheet.png "Screenshot di un foglio Excel formattato creato con Java e Aspose.Cells")

*Testo alternativo immagine: “Foglio Excel formattato creato con Java e Aspose.Cells, con intestazione in grassetto e colonna data formattata.”*


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}