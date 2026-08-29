---
category: general
date: 2026-08-20
description: Crea smart marker per fogli di lavoro in Java usando Aspose.Cells e controlla
  la denominazione dei fogli di dettaglio con SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: it
lastmod: 2026-08-20
og_description: Crea smart marker per fogli di lavoro in Java con Aspose.Cells. Scopri
  come denominare dinamicamente i fogli di dettaglio usando SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Crea marcatori intelligenti per fogli di lavoro – Guida Java con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Come creare smart marker nei fogli di lavoro con Aspose.Cells
url: /it/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare smart marker nei fogli di lavoro con Aspose.Cells

Se hai bisogno di **creare smart marker nei fogli di lavoro** in una cartella di lavoro Java, questa guida ti mostra i passaggi esatti per farlo con Aspose.Cells. Vedrai come configurare `SmartMarkerOptions` affinché ogni foglio di dettaglio riceva un nome unico e prevedibile.

Generare report Excel che espandono un modello master‑detail è una necessità comune nei sistemi finanziari, di inventario e di reporting. L'uso degli smart marker elimina la duplicazione manuale dei fogli e ti permette di concentrarti sui dati invece che sulla logica di gestione.

## Cosa imparerai

* Come caricare una cartella di lavoro master che contiene smart marker.  
* Come impostare `SmartMarkerOptions` per controllare la denominazione dei fogli di dettaglio generati.  
* Come fornire un `DataTable` con dati di esempio e applicarlo agli smart marker.  
* Come salvare il risultato in modo che ogni foglio di dettaglio abbia un nome distinto, evitando nomi di foglio duplicati.

**Prerequisiti**  
* Java 17 o successiva (il codice compila anche con JDK 8+).  
* Aspose.Cells per Java 23.9 o più recente – la libreria fornisce le classi `Workbook`, `SmartMarkerOptions` e correlate.  
* Un IDE come IntelliJ IDEA, Eclipse o VS Code.

I concetti secondari che incontrerai includono **Aspose.Cells Java**, **smart marker options** e la gestione dei **nomi di foglio duplicati** quando il modello si espande.

## Creare smart marker nei fogli di lavoro – guida passo‑passo

Le sezioni seguenti suddividono il processo in passaggi discreti e riutilizzabili. Ogni passaggio include uno snippet di codice, una spiegazione del perché è importante e consigli pratici per evitare errori comuni.

### Passo 1: Configurare il progetto Maven e aggiungere Aspose.Cells

Crea un nuovo modulo Maven (o progetto Gradle) e aggiungi la dipendenza Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Perché questo passaggio è importante** – La libreria fornisce la classe `Workbook` che legge e scrive file Excel, oltre al motore smart‑marker che espande automaticamente il tuo modello. Senza la dipendenza corretta, il compilatore non può risolvere le chiamate API usate successivamente.

> **Suggerimento:** Se lavori dietro un proxy aziendale, configura il file `settings.xml` di Maven per scaricare il repository Aspose in modo sicuro.

### Passo 2: Caricare la cartella di lavoro master che contiene smart marker

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Perché questo passaggio è importante** – La cartella di lavoro master definisce il layout, le formule e i tag segnaposto (`«SmartMarker»`) che il motore sostituirà. Caricare il file una sola volta mantiene basso l'uso della memoria e consente di riutilizzare la stessa cartella di lavoro per più set di dati.

### Passo 3: Configurare SmartMarkerOptions per nomi personalizzati dei fogli di dettaglio

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Perché questo passaggio è importante** – Per impostazione predefinita Aspose.Cells crea fogli di dettaglio con nomi generici come “DetailSheet”. Quando il modello si espande per molte righe, questi nomi entrano in conflitto, generando **nomi di foglio duplicati** e un'eccezione a runtime. Il pattern `"DetailSheet_{0}"` garantisce un nome unico per ogni riga, risolvendo il problema di duplicazione.

### Passo 4: Costruire un DataTable che corrisponda ai campi dello smart marker

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Perché questo passaggio è importante** – Il `DataTable` fornisce i valori effettivi che sostituiscono i segnaposto degli smart marker. I nomi delle colonne devono corrispondere ai nomi dei marker nel modello; altrimenti il motore ignora la sostituzione in modo silenzioso.

> **Errore comune:** Usare un nome di colonna che differisce per maiuscole/minuscole (es. “id” vs “Id”) porta a dati mancanti nei fogli generati.

### Passo 5: Applicare i dati agli smart marker con le opzioni di denominazione

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Perché questo passaggio è importante** – Il metodo `apply` attiva il motore smart‑marker. Legge ogni riga, crea un nuovo foglio di dettaglio usando il pattern di denominazione definito in `SmartMarkerOptions` e popola il foglio con i dati della riga. Questa singola chiamata sostituisce decine di righe di codice manuale per clonare fogli e riempire celle.

### Passo 6: Salvare la cartella di lavoro e verificare il risultato

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Dopo l'esecuzione, apri `MasterDetailDuplicatedNames.xlsx`. Dovresti vedere:

* Il foglio master originale invariato.  
* Due nuovi fogli di lavoro denominati `DetailSheet_1` e `DetailSheet_2`.  
* Ogni foglio di dettaglio contiene i valori corrispondenti alla riga del `DataTable`.

**Perché questo passaggio è importante** – Il salvataggio della cartella di lavoro finalizza l'espansione degli smart marker. Il file può ora essere inviato a sistemi downstream, allegato a email o aperto in Excel per ulteriori analisi.

## Gestione di casi limite e varianti

### Più fogli master

Se il tuo modello contiene più di un foglio master, itera sui smart marker di ciascun foglio:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Denominazione personalizzata oltre all'indice di riga

Puoi inserire qualsiasi colonna di dati nel nome del foglio usando segnaposto come `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Assicurati che la colonna `OrderId` esista nel `DataTable` fornito.

### Prevenire nomi di foglio troppo lunghi

Excel limita i nomi dei fogli a 31 caratteri. Se il tuo pattern rischia di superare questo limite, tronca o hash il valore:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Quindi elabora il nome generato con `StringUtils.abbreviate` prima di passarlo ad Aspose.

## Esempio completo eseguibile

Di seguito trovi il file sorgente completo che puoi copiare, modificare i percorsi dei file e eseguire direttamente:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Output previsto**

* `MasterDetailDuplicatedNames.xlsx` contiene:


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}