---
category: general
date: 2026-03-01
description: Impara come incorporare i font in HTML e altri formati. Tutorial passo‑passo
  che copre l’incorporazione dei font in HTML, la conversione di Excel in HTML, come
  esportare OLE e la conversione di Excel in XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: it
og_description: Come incorporare i font in esportazioni HTML, XPS e OLE. Impara l’intero
  flusso di lavoro, visualizza il codice Java eseguibile e padroneggia l’incorporamento
  dei font in HTML per le conversioni Excel.
og_title: Come incorporare i font – Tutorial Java completo
tags:
- Aspose.Cells
- Java
- Document Export
title: Come incorporare i font – Guida completa per l'esportazione HTML, XPS e OLE
url: /it/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font – Guida completa per HTML, XPS e esportazione OLE

Ti sei mai chiesto **come incorporare i font** quando trasformi una cartella di lavoro Excel in una pagina web o in un documento stampabile? Non sei l'unico. Molti sviluppatori si trovano di fronte a un ostacolo quando l'output sembra corretto sulla loro macchina ma si rompe su un'altra perché i font richiesti sono mancanti.  

In questo tutorial percorreremo uno scenario reale usando Aspose.Cells per Java: incorporeremo i font in HTML, conserveremo i selettori di variazione emoji durante la conversione in XPS e manterremo persino un oggetto OLE modificabile durante l'esportazione in PPTX. Alla fine avrai una soluzione solida, pronta da copiare e incollare, che risponde a “come incorporare i font” e tocca anche **embed fonts in html**, **convert excel to html**, **how to export ole** e **convert excel to xps**.

## Prerequisiti

- Java 17 (or any recent JDK)  
- Aspose.Cells for Java 25.x o successivo  
- Un IDE di sviluppo (IntelliJ IDEA, Eclipse o VS Code)  
- Familiarità di base con le strutture dati di Excel  

Non sono richiesti servizi esterni—tutto viene eseguito localmente.

## Panoramica della soluzione

1. **Create a workbook** e utilizza la funzione `WRAPCOLS` per trasformare un intervallo verticale in un layout a tre colonne.  
2. **Save the workbook as XPS** attivando i selettori di variazione dei font in modo che le emoji rimangano intatte.  
3. **Export to HTML** con font incorporati, garantendo che la pagina abbia lo stesso aspetto ovunque.  
4. **Export a workbook containing an OLE object to PPTX**, preservando la modificabilità.  
5. **Apply a Smart Marker template** che dimostra il binding dei dati master‑detail.  

Ogni passaggio è isolato nella propria sezione H2, rendendo la guida facile da scorrere sia per i motori di ricerca sia per gli assistenti AI.

![Come incorporare i font illustrazione](image.png "come incorporare i font")

*Testo alternativo dell'immagine: diagramma su come incorporare i font che mostra il flusso di lavoro da Excel a HTML, XPS e PPTX.*

---

## Passo 1 – Crea una cartella di lavoro e usa WRAPCOLS (Why This Matters for embed fonts in html)

Prima di poter parlare di incorporare i font, abbiamo bisogno di una cartella di lavoro che contenga effettivamente dei dati. La funzione `WRAPCOLS` è un modo pratico per dividere una singola colonna in più colonne, il che spesso rende l'HTML finale più leggibile.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Perché questo passaggio?**  
La chiamata `WRAPCOLS` genera un intervallo multicolonna che in seguito appare in HTML come una tabella. Quando più tardi **embed fonts in html**, lo stile della tabella dipenderà dai font che incorporiamo, garantendo un rendering coerente su tutti i browser.

---

## Passo 2 – Salva la cartella di lavoro come XPS preservando le Emoji (convert excel to xps)

Se hai bisogno di un formato pronto per la stampa, XPS è una scelta solida. Tuttavia, i documenti moderni spesso contengono emoji o simboli che utilizzano selettori di variazione. Attivare `EnableFontVariationSelectors` assicura che quei caratteri sopravvivano alla conversione.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Cosa ottieni:**  
Un file XPS che visualizza qualsiasi emoji incorporata esattamente come nel workbook di origine. Questo soddisfa il requisito **convert excel to xps** e dimostra che la gestione dei font non è limitata a HTML.

---

## Passo 3 – Esporta in HTML con Font Incorporati (how to embed fonts & embed fonts in html)

Ora arriviamo al cuore del tutorial: **how to embed fonts** durante la conversione di Excel in HTML. Aspose.Cells ci permette di incorporare i font direttamente nel file HTML generato, eliminando la necessità di file di font esterni.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Come funziona:**  
`setEmbedFonts(true)` indica al renderer di leggere i file di font usati nella cartella di lavoro e di incorporarli come regole `@font-face` codificate in Base64 all'interno del tag `<style>`. L'HTML risultante è autonomo, quindi puoi caricarlo su qualsiasi server e i font verranno renderizzati correttamente—esattamente ciò che gli sviluppatori cercano quando cercano **how to embed fonts**.

**Snippet di output previsto (all'interno di `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Nota la regola `@font-face`—questa è la risposta concreta a **embed fonts in html**.

---

## Passo 4 – Esporta una cartella di lavoro contenente un oggetto OLE in PPTX (how to export ole)

Molti report aziendali incorporano documenti Word, PDF o altri fogli Excel come oggetti OLE. Quando esporti una tale cartella di lavoro in PowerPoint, spesso perdi la possibilità di modificare quell'oggetto. Aspose.Cells preserva la modificabilità fin da subito.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Perché è importante:**  
Se stai cercando **how to export ole**, questo snippet mostra la chiamata API esatta. La diapositiva PowerPoint risultante contiene l'oggetto OLE come componente live, modificabile con doppio clic—senza necessità di post‑processing aggiuntivo.

---

## Passo 5 – Applica un modello Smart Marker (master‑detail) e completa la demo

I Smart Marker ti consentono di collegare una fonte dati (Map, JSON, DataTable) direttamente a un modello Excel. Ecco un esempio minimale che stampa righe master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Ciò che vedi:**  
Una nuova cartella di lavoro (`smartMarkerResult.xlsx`) in cui i segnaposto del modello sono sostituiti con i dati. Questo passaggio non riguarda direttamente i font, ma completa il tutorial mostrando un tipico flusso di lavoro di reporting che spesso precede un'esportazione **embed fonts in html**.

---

## Problemi comuni & consigli professionali (Assicurare l'incorporamento riuscito dei font)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| I font mancano nel file HTML | La cartella di lavoro utilizza un font di sistema che non è installato sul server. | Usa `Workbook.getSettings().setDefaultFont("Arial")` prima di caricare i dati, oppure incorpora manualmente i file dei font richiesti. |
| L'HTML di output è enorme | Incorporare molti font di grandi dimensioni aumenta la dimensione del file. | Limita l'incorporamento solo ai font che utilizzi realmente: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Le emoji scompaiono dopo la conversione XPS | I selettori di variazione vengono rimossi per impostazione predefinita. | Abilita `settings.setEnableFontVariationSelectors(true)` come mostrato nel Passo 2. |
| L'oggetto OLE diventa un'immagine statica in PPTX | La cartella di lavoro di origine è stata salvata con `setSuppressOLEObjects(true)`. | Assicurati di **non** sopprimere gli oggetti OLE quando salvi in PPTX. |

---

## Verifica dei risultati

1. Apri `embeddedFonts.html` in Chrome/Firefox. La tabella dovrebbe visualizzarsi usando il font incorporato (ad es., Arial) anche se quel font non è installato sulla macchina.  
2. Apri `withVariations.xps` nel Visualizzatore XPS di Windows. Emoji come 👍 dovrebbero essere renderizzate correttamente.  
3. Apri `oleEditable.pptx` in PowerPoint. Fai doppio clic sulla forma OLE;  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}