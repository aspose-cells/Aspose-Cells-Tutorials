---
category: general
date: 2026-06-21
description: Guida al formato data di Aspose Cells – scopri come impostare un formato
  data personalizzato, cambiare il locale della cartella di lavoro e applicare un
  formato data globale in Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: it
og_description: 'Tutorial sul formato data di Aspose Cells: impara come impostare
  un formato data personalizzato, cambiare la lingua della cartella di lavoro e impostare
  il formato data globale per progetti Java.'
og_title: Formato data di Aspose Cells – Imposta formato data personalizzato in Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Formato data Aspose Cells: Come impostare un formato data personalizzato in
  Java'
url: /it/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato Data Aspose Cells – Guida Completa Java

Ti sei mai chiesto come impostare un formato data personalizzato in Aspose Cells per Java? Non sei l'unico. Che tu stia generando report per un cliente giapponese o abbia semplicemente bisogno di uno stile data coerente in tutto un workbook, padroneggiare **aspose cells date format** è essenziale.

In questo tutorial ti guideremo attraverso un esempio pratico, end‑to‑end, che mostra **come impostare il formato data** a livello globale, cambiare la locale del workbook e applicare un modello personalizzato come l'anno dell'era giapponese. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto—senza congetture.

## Cosa Copre Questa Guida

- Creazione di una nuova istanza `Workbook`.
- Modifica della locale del workbook affinché i formati integrati rispettino le regole regionali.
- Definizione di un **set custom date format** usando `DateTimeFormatter`.
- Applicazione di quel formato a livello globale con `WorkbookSettings`.
- Problemi comuni (ad es. sovrascrittura dei formati a livello di cella) e come evitarli.
- Varianti rapide per altre locale o stringhe di formato.

Hai solo bisogno di un ambiente di sviluppo Java, Maven o Gradle per includere Aspose Cells e una conoscenza di base della sintassi Java. Pronto? Immergiamoci.

## Passo 1: Configura il tuo progetto e importa Aspose Cells

Prima di tutto—assicurati che Aspose Cells per Java sia nel tuo classpath. Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gli utenti Gradle possono aggiungere:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Pro tip:** Aspose offre una licenza di prova gratuita di 30 giorni. Inserisci il file `Aspose.Cells.lic` nella radice del progetto e chiama `License license = new License(); license.setLicense("Aspose.Cells.lic");` prima di creare qualsiasi workbook.

Ora importa le classi di cui avremo bisogno:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Queste importazioni ci danno accesso al contenitore del workbook, alle sue impostazioni e al formattatore sensibile alla locale.

## Passo 2: Crea un nuovo Workbook e accedi alle sue impostazioni

Un nuovo `Workbook` parte con la locale predefinita (di solito US). Per controllare la gestione delle date a livello globale, dobbiamo recuperare il suo oggetto `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

L'oggetto `settings` è un hub centrale. Qualsiasi cosa tu cambi qui—come il formato data—influisce su ogni cella che **non** ha già uno stile esplicito che lo sovrascrive.

## Passo 3: Definisci un Formato Data/Ora Personalizzato (Esempio Era Giapponese)

Supponiamo tu abbia bisogno di date nel formato dell'era giapponese, ad es. “令和04.10.01”. Il pattern `"ggyy.MM.dd"` funziona quando è associato a una cultura giapponese:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Se preferisci uno stile ISO più semplice (`"yyyy-MM-dd"`), basta sostituire la stringa del pattern—non servono altre modifiche.

## Passo 4: Applica il Formato Personalizzato come Formato Data Globale

Ora colleghiamo il formattatore alle impostazioni globali del workbook. Questo è il passo **set global date format** che garantisce che qualsiasi cella che visualizza una data utilizzi automaticamente il nostro pattern:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

A questo punto, qualsiasi data tu scriva nel foglio—sia tramite `Cell.putValue(new Date())` sia leggendo da una fonte dati—verrà visualizzata usando il pattern dell'era giapponese.

## Passo 5: Popola il Workbook con Date di Esempio (Opzionale)

Aggiungiamo qualche riga così puoi vedere il formato in azione. Questa parte non è strettamente necessaria per la logica di formattazione, ma aiuta a verificare che tutto funzioni:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Quando salvi il workbook, quelle celle mostreranno qualcosa del genere:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(L'anno esatto dell'era dipende dal calendario giapponese corrente.)

## Passo 6: Salva il Workbook e Verifica l'Uscita

Infine, scrivi il workbook su file così potrai aprirlo in Excel, LibreOffice o qualsiasi visualizzatore che rispetti il formato:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Apri `CustomDateFormatDemo.xlsx` e dovresti vedere le date renderizzate secondo il pattern impostato. Se noti una discrepanza, ricontrolla che nessuno stile a livello di cella stia sovrascrivendo l'impostazione globale (vedi la sezione “Edge Cases” qui sotto).

## Edge Cases & Variations

### 1. Sovrascrivere il Formato Globale a Livello di Cella

Se una cella ha già uno stile con un formato numerico specifico, l'impostazione globale viene ignorata per quella cella. Per forzare il formato globale, cancella lo stile della cella:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Cambiare la Locale del Workbook Senza un Pattern Personalizzato

A volte vuoi semplicemente **change workbook locale** affinché i formati data integrati (come `14‑03‑2024`) seguano le convenzioni regionali. Puoi farlo senza un `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Ora qualsiasi stile data predefinito apparirà come `21/04/2025` invece di `04/21/2025`.

### 3. Usare più Formati Personalizzati in un Singolo Workbook

Aspose Cells consente di definire diversi formati personalizzati e applicarli selettivamente:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Ripristinare il Formato Predefinito

Se devi tornare al comportamento predefinito di Aspose per le date, passa semplicemente `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Domande Frequenti

- **Questo influisce sui fogli di lavoro esistenti?**  
  Sì—qualsiasi foglio caricato nel `Workbook` dopo aver impostato il formato globale lo erediterà, a meno che una cella non abbia già uno stile esplicito.

- **Posso impostare il formato dopo aver scritto i dati?**  
  Assolutamente. Il formato globale viene applicato al momento del rendering, quindi puoi popolare le celle prima e impostare il formato in seguito.

- **E se ho bisogno di un calendario specifico per locale (ad es. Buddhista Thai)?**  
  Usa il codice `CultureInfo` appropriato (`"th-TH"`), e il formattatore rispetterà automaticamente quel calendario.

- **C'è un impatto sulle prestazioni?**  
  Trascurabile. Il formattatore è memorizzato nella cache all'interno di `WorkbookSettings`, quindi il sovraccarico si verifica solo una volta per workbook.

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione, che incorpora tutti i passaggi discussi:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Output previsto in Excel:**

| Cella | Valore Visualizzato |
|------|----------------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (time part may vary) |

Apri il file e vedrai le date formattate esattamente come definito.

## Conclusione

Hai appena imparato come **aspose cells date format** un workbook in Java, dalla modifica della locale all'applicazione di un **set custom date format** che funziona a livello globale. Sfruttando `WorkbookSettings` e `DateTimeFormatter`, ottieni un controllo preciso su come appare ogni data—senza necessità di stilizzare manualmente.

Successivamente potresti esplorare **how to set date format** per colonne specifiche, o combinare formati numerici personalizzati con formattazione condizionale per un report raffinato. Gli stessi principi valgono: definisci un formattatore, collegalo tramite stile e lascia che Aspose gestisca il resto.

Buona programmazione, e sentiti libero di sperimentare con altre locale—i tuoi utenti ti ringrazieranno per i fogli di calcolo curati e culturalmente consapevoli!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}