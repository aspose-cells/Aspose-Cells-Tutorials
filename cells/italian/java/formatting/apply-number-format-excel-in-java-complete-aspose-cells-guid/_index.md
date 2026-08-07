---
category: general
date: 2026-07-20
description: Applica il formato numerico di Excel usando Java e Aspose.Cells. Scopri
  come applicare lo stile valuta in Excel, creare una cartella di lavoro Excel in
  Java e importare una DataTable in Excel in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: it
lastmod: 2026-07-20
og_description: Applica il formato numerico in Excel con Java. Questa guida ti mostra
  come applicare lo stile valuta in Excel, creare una cartella di lavoro Excel con
  Java e importare una datatable in Excel passo‑passo.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Applicare il formato numerico di Excel in Java – Tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Applicare il formato numerico di Excel in Java – Guida completa ad Aspose.Cells
url: /it/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicare il formato numerico di Excel in Java – Guida completa ad Aspose.Cells

Ti sei mai chiesto come **apply number format excel** direttamente dal codice Java? Forse stai generando report finanziari o hai bisogno di un modo rapido per formattare una colonna di importi senza aprire Excel manualmente. La buona notizia? Con Aspose.Cells puoi farlo in poche righe, e imparerai anche a **apply currency style excel**, **create excel workbook java**, e **import datatable to excel** tutto in una routine compatta.

In questo tutorial percorreremo un esempio reale: un elenco di importi memorizzato in una `List<Map<String,Object>>` Java viene importato in una nuova cartella di lavoro, la prima colonna riceve un formato valuta predefinito, e il file viene salvato pronto per la distribuzione. Pronto a vedere quanto è semplice? Immergiamoci.

## Prerequisiti – Cosa ti serve

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK) 8+** – il codice funziona su qualsiasi JDK recente.
- Libreria **Aspose.Cells for Java** (l'artifact Maven `com.aspose:aspose-cells`) – è il motore che ci permette di manipolare file Excel senza installare Office.
- Un **IDE preferito** (IntelliJ IDEA, Eclipse, VS Code…) – qualsiasi editor va bene, ma un IDE velocizza il debug.
- Familiarità di base con le **collezioni Java** – useremo una `List` di `Map` per simulare una DataTable.

Tutto qui. Nessun servizio esterno, nessuna installazione di Excel, solo puro Java.

## Passo 1: Creare Excel Workbook Java – Istanziare il Workbook

La prima cosa di cui abbiamo bisogno è un oggetto workbook. Pensalo come la tela vuota dove vivrà tutto.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Perché creare prima il workbook? Aspose.Cells lavora interamente in memoria, così puoi aggiungere fogli, stili e dati prima di toccare il disco. Questo approccio è veloce e mantiene il tuo codice testabile.

## Passo 2: Preparare i dati – Importare Datatable in Excel usando una Lista di Map

In molte applicazioni aziendali i dati provengono da database sotto forma di tabelle. Qui simuliamo ciò con una `List<Map<String,Object>>`. Ogni mappa rappresenta una riga, e la chiave `"Amount"` corrisponde a un valore numerico.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Ti potresti chiedere, “Perché non usare un `ResultSet` o POJO?” Il metodo `importDataTable` accetta qualsiasi collezione che si comporti come una DataTable, e una lista di mappe è il modo più semplice per dimostrare il concetto senza introdurre dipendenze aggiuntive.

## Passo 3: Definire il formato numerico – Apply Currency Style Excel

Ora arriva il cuore del tutorial: **apply number format excel**. Aspose.Cells fornisce formati numerici predefiniti; il formato valuta è l'indice 5. Preleviamo lo stile predefinito dal primo foglio, ne modifichiamo il formato numerico e lo memorizziamo per un uso successivo.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Perché usare lo stile predefinito come base? Contiene già il font predefinito della cartella di lavoro, l'allineamento e altre impostazioni, così devi cambiare solo ciò che è importante—in questo caso il formato numerico. Se ti servisse un formato personalizzato (ad es. “€#,##0.00”), potresti chiamare `currencyStyle.setCustom("#,##0.00 €")` invece.

## Passo 4: Configurare le opzioni di importazione – Collegare l'array di stili

Aspose.Cells ti permette di passare un array di oggetti `Style` che corrispondono alle colonne importate. Poiché i nostri dati hanno una sola colonna, forniamo un array a elemento unico contenente lo stile valuta.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Se mai dovessi formattare più colonne in modo diverso, basta espandere l'array: `new Style[] { styleForCol1, styleForCol2, … }`. L'ordine degli stili corrisponde all'ordine delle colonne nei dati di origine.

## Passo 5: Importare i dati – Portare la Datatable nel foglio di lavoro

Con il workbook pronto, i dati preparati e gli stili definiti, finalmente **import datatable to excel**. Iniziamo dalla cella `A1`, includiamo le intestazioni di colonna (`true`) e passiamo le `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Nota il flag `true`—Aspose.Cells genererà automaticamente una riga di intestazione basata sulle chiavi della mappa (`"Amount"`). Se lo impostassi a `false`, l'intestazione verrebbe omessa, dandoti più controllo sul layout finale.

## Passo 6: Salvare il file – Create Excel Workbook Java su disco

L'ultimo tassello del puzzle è persistere il workbook in memoria su un file fisico. Puoi scegliere qualsiasi formato supportato da Aspose (`.xlsx`, `.xls`, `.csv`, …). Qui salviamo come file XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Dopo aver eseguito il programma, apri il file generato. Vedrai la colonna `"Amount"` formattata con il simbolo del dollaro, due cifre decimali e i separatori delle migliaia—esattamente ciò che ti aspetti quando **apply number format excel** per valori di valuta.

## Risultato atteso

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

L'intestazione “Amount” appare in grassetto (stile predefinito), e ogni cella sottostante mostra il formato valuta che abbiamo impostato. Nessuna formattazione manuale in Excel necessaria.

## Suggerimenti professionali e errori comuni

- **Riutilizzare gli stili con saggezza** – Gli stili sono leggeri, ma creare un nuovo `Style` per ogni cella può penalizzare le prestazioni. Riutilizza sempre lo stesso oggetto stile quando applichi lo stesso formato a molte celle, come abbiamo fatto con `currencyStyle`.
- **Formati personalizzati** – Se la tua locale utilizza un simbolo di valuta diverso, sostituisci `currencyStyle.setNumber(5)` con `currencyStyle.setCustom("€#,##0.00")`. Verifica il formato in Excel per confermare che si comporti come previsto.
- **Dataset di grandi dimensioni** – Per migliaia di righe, considera l'uso di `importDataTable` con il flag `ImportTableOptions.setImportDataOnly(true)` per saltare la generazione dell'intestazione e velocizzare l'importazione.
- **Sicurezza nei thread** – Gli oggetti Aspose.Cells **non** sono thread‑safe. Crea un `Workbook` separato per ogni thread se generi report in parallelo.

## Domande frequenti

**D: Posso applicare il formato numerico a un workbook esistente?**  
R: Assolutamente. Apri il workbook con `new Workbook("Existing.xlsx")`, recupera il foglio di destinazione e segui i passi 3‑5 per applicare l'array di stili ai nuovi dati.

**D: E se devo formattare date invece di valute?**  
R: Usa un indice di numero predefinito diverso (`14` per data breve, `22` per data lunga) o un formato personalizzato come `yyyy‑mm‑dd`. Il flusso di lavoro rimane lo stesso.

**D: Funziona con versioni più vecchie di Excel (.xls)?**  
R: Sì. Basta cambiare l'estensione del file in `workbook.save("MyFile.xls")`. Aspose passerà automaticamente al formato binario.

## Conclusione – Cosa abbiamo realizzato

Abbiamo **applied number format excel** a una colonna di valori monetari, dimostrato come **apply currency style excel**, mostrato il modo più semplice per **create excel workbook java**, e usato Aspose.Cells per **import datatable to excel** senza toccare l'interfaccia grafica. Tutto questo è stato realizzato in un programma conciso e autonomo che puoi copiare, incollare ed eseguire.

Qual è il prossimo passo? Prova ad estendere l'esempio:

- Aggiungi altre colonne (ad es. “Date”, “Description”) e assegna stili diversi per colonna.
- Esporta gli stessi dati in CSV e confronta come i formati numerici vengano persi.
- Integra il codice in un servizio Spring Boot che restituisce il workbook come risposta HTTP scaricabile.

Sentiti libero di sperimentare, e se incontri difficoltà, lascia un commento qui sotto. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Come applicare stili alle celle di Excel usando Aspose.Cells per Java - Guida completa](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Unire celle e applicare stili in Excel usando Aspose.Cells per Java - Guida completa](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells per Java: Come creare e formattare cartelle di lavoro Excel in modo efficiente](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}