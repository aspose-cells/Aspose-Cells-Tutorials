---
category: general
date: 2026-11-22
description: Scopri come impostare la locale in un workbook Java, cambiare la lingua
  del workbook e impostare il calendario in giapponese con chiari esempi di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: it
lastmod: 2026-11-22
og_description: Come impostare rapidamente la locale in un workbook Java. Segui questo
  tutorial per cambiare la lingua del workbook, impostare la locale su giapponese
  e configurare il calendario giapponese.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Come impostare il locale in un workbook Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Come impostare la locale in una cartella di lavoro Java usando Aspose.Cells
url: /it/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare la locale in una cartella di lavoro Java con Aspose.Cells

Impostare la locale in una cartella di lavoro Java è una necessità comune quando è necessario adattare il foglio di calcolo a diverse regioni. In questa guida imparerai a impostare la locale, cambiare la lingua della cartella di lavoro e impostare il calendario giapponese utilizzando l'API Aspose.Cells.

Internazionalizzare una cartella di lavoro va oltre la traduzione del testo; influisce anche sui formati numerici, sull'analisi delle date e sul sistema di calendario predefinito. Alla fine di questo tutorial sarai in grado di:

* Configurare la locale della cartella di lavoro su Giapponese (Giappone) – **set locale to japanese**.  
* Cambiare la lingua della cartella di lavoro affinché formule e stringhe UI rispettino la cultura di destinazione – **change workbook language**.  
* Passare al calendario imperiale giapponese – **how to set calendar**.  

I passaggi funzionano con qualsiasi versione recente di Aspose.Cells per Java (v23.9 o successive) e richiedono solo un ambiente di sviluppo Java standard.

## Prerequisiti

| Requisito | Motivo |
|-----------|--------|
| Java 8 o superiore | La libreria è destinata a Java 8+. |
| Aspose.Cells per Java (v23.9+) | Fornisce `Workbook`, `WorkbookSettings` e le utility per la locale. |
| IDE (IntelliJ IDEA, Eclipse o VS Code) | Per compilare ed eseguire il campione. |
| Conoscenza di base di Java | Necessaria per comprendere gli snippet di codice. |

Aggiungi la dipendenza Maven di Aspose.Cells al tuo `pom.xml` (o scarica il JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Come impostare la locale e il calendario in una cartella di lavoro

Il primo passo è creare un'istanza di cartella di lavoro e ottenere il suo oggetto impostazioni. L'oggetto impostazioni espone le API per locale e calendario.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Perché ogni riga è importante

* **`new Workbook()`** – Istanzia una cartella di lavoro vuota che puoi manipolare prima di salvarla.  
* **`getSettings()`** – Restituisce un oggetto `WorkbookSettings`; tutte le opzioni regionali vivono qui.  
* **`setCalendar(...)`** – Sostituisce il calendario gregoriano predefinito con il calendario imperiale giapponese, influenzando il modo in cui le date vengono visualizzate e analizzate.  
* **`setLocale(new Locale("ja","JP"))`** – Cambia la lingua e le convenzioni regionali (ad es., mesi, separatori decimali). Questo è il fulcro di **how to set locale** per la cartella di lavoro.  

Eseguendo il programma viene creato `LocaleDemo.xlsx`. Aprilo in Excel o LibreOffice e vedrai i nomi dei mesi in giapponese, i simboli di valuta Yen giapponese e le date formattate secondo il calendario giapponese.

## Cambiare la lingua della cartella di lavoro (impostare la locale su Giapponese)

Se il tuo obiettivo principale è **change workbook language**, puoi concentrarti solo sulla chiamata `setLocale`. Il frammento seguente isola quel passaggio:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Cosa cambia?**  
* Le stringhe di formattazione delle celle passano al giapponese (ad es., `#,##0.00` diventa `#,##0.00` con il simbolo yen).  
* I nomi delle funzioni integrate (come `SUM`) rimangono in inglese perché la locale delle funzioni di Excel è indipendente, ma le stringhe di data e i messaggi di errore seguono le convenzioni giapponesi.  

**Quando usarlo?**  
* Quando ti serve un foglio di calcolo che visualizzi numeri e date per un pubblico giapponese ma il calendario sottostante può rimanere gregoriano.  
* Per report esportati in PDF o stampati, garantendo che la lingua visiva corrisponda al mercato di destinazione.

## Come impostare il calendario giapponese

A volte il requisito **how to set calendar** è separato dalla locale. Per i sistemi legacy che memorizzano le date nell'era imperiale giapponese, devi impostare esplicitamente il calendario mantenendo, se lo desideri, la locale predefinita.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Punti chiave:**

* `Calendar.getInstance(Locale.JAPAN)` restituisce un `java.util.Calendar` configurato per l'era giapponese.  
* La cartella di lavoro ora renderizzerà le date usando i simboli dell'era (R per Reiwa, H per Heisei, ecc.).  
* Questa impostazione **non** influisce sulla formattazione numerica o sulla lingua UI; combinala con `setLocale` se ti servono entrambe.

## Esempio completo end‑to‑end

Di seguito trovi un programma completo e eseguibile che dimostra **how to set locale**, **change workbook language** e **set the calendar** in un unico flusso coerente. Aggiunge inoltre una cella di esempio per illustrare l'effetto.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Output previsto:**  
Aprendo `FullJapaneseLocale.xlsx` la prima cella mostra una data come `R3/04/01` (Reiwa 3) e la seconda cella è formattata come `¥1,234,567.89`. Questo conferma che **how to set locale**, **change workbook language** e **how to set calendar** funzionano tutti insieme.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| Usare `Locale.CHINA` invece di `new Locale("ja","JP")` | `Locale.CHINA` imposta la lingua cinese, non giapponese. | Instanziare sempre `Locale` con `"ja", "JP"` per il giapponese. |
| Dimenticare di chiamare `settings.setCalendar(...)` dopo `setLocale` | Il calendario resta gregoriano, quindi le date appaiono nell'era sbagliata. | Chiamare `setCalendar` **dopo** aver impostato la locale, o impostare entrambi insieme come mostrato. |
| Salvare la cartella di lavoro prima di applicare le impostazioni | Le impostazioni vengono applicate all'oggetto in memoria; salvare troppo presto scrive la locale predefinita. | Applicare tutte le modifiche di locale/calendario **prima** di chiamare `workbook.save()`. |
| Usare una versione obsoleta di Aspose.Cells | Le versioni più vecchie non hanno le overload di `setCalendar`. | Aggiornare alla v23.9+ o controllare le note di rilascio per il supporto della locale. |

## Testare la configurazione

1. Esegui la classe **FullLocaleExample**.  
2. Apri il file generato `FullJapaneseLocale.xlsx` in Excel.  
3. Verifica che:  
   * La colonna delle date mostri i simboli dell'era giapponese (`R`, `H`, ecc.).  
   * La colonna dei numeri utilizzi il simbolo Yen e i separatori di migliaia.  
   * Eventuali messaggi di errore integrati (ad es., `#DIV/0!`) compaiano in giapponese se la cartella di lavoro contiene errori.  

Se uno di questi controlli fallisce, ricontrolla che l'oggetto `WorkbookSettings` modificato sia la stessa istanza usata al momento del salvataggio.

## Prossimi passi

* **Localizzare le formule** – Sebbene la locale controlli la formattazione, puoi anche tradurre i nomi delle funzioni personalizzate usando `FormulaParser`.  
* **Applicare la locale a cartelle di lavoro esistenti** – Carica una cartella di lavoro con `new Workbook`  

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}