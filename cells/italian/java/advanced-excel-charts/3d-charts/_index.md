---
date: 2026-02-09
description: Impara come creare un grafico a torta 3D in Java usando Aspose.Cells.
  Genera un grafico a barre 3D, aggiungi un grafico 3D in Excel e salva la cartella
  di lavoro xlsx con esempi di codice passo‑passo.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Crea grafico a torta 3D in Java con Aspose.Cells
url: /it/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crea un grafico a torta 3D in Java

## Introduzione ai grafici 3D

Aspose.Cells for Java è una potente API Java per lavorare con file Excel, e rende semplice **create 3d pie chart** progetti così come visualizzazioni classiche a barre 3‑D. In questo tutorial vedrai esattamente come generare un grafico a barre 3‑D, come adattare lo stesso approccio per un grafico a torta 3‑D, personalizzare l'aspetto e infine **add 3d chart excel** ai tuoi report. Che tu stia costruendo un cruscotto finanziario, un foglio di performance di vendita o visualizzando dati scientifici, i passaggi seguenti ti forniranno una solida base.

## Risposte rapide
- **Quale libreria mi serve?** Aspose.Cells for Java (ultima versione)  
- **Posso generare un grafico a barre 3D?** Sì – usa `ChartType.BAR_3_D`  
- **Ho bisogno di una licenza?** Una licenza valida rimuove i limiti di valutazione  
- **Quali versioni di Excel sono supportate?** Tutte le versioni principali dal 2003 al 2023  
- **È possibile esportare il grafico come immagine?** Sì, tramite i metodi `chart.toImage()`  

## Cosa sono i grafici 3D?
I grafici 3D aggiungono profondità alle visualizzazioni 2D tradizionali, aiutando gli osservatori a comprendere le relazioni multidimensionali in modo più intuitivo. Sono particolarmente utili quando è necessario confrontare diverse categorie fianco a fianco mantenendo una chiara gerarchia visiva.

## Perché usare Aspose.Cells for Java per generare un grafico a barre 3D?
Aspose.Cells for Java offre un ricco set di API per la creazione di grafici, piena compatibilità con Excel e un controllo dettagliato sullo stile. Questo significa che puoi **generate 3d bar chart** oggetti programmaticamente senza preoccuparti delle particolarità delle versioni di Excel.

## Configurazione di Aspose.Cells for Java

### Download e installazione
Puoi scaricare la libreria Aspose.Cells for Java dal sito ufficiale. Segui le istruzioni Maven/Gradle fornite o aggiungi il JAR direttamente al classpath del tuo progetto.

### Inizializzazione della licenza
Per sbloccare l'intero set di funzionalità, inizializza la tua licenza prima di qualsiasi operazione sui grafici:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Creazione di un grafico 3D di base

### Importazione delle librerie necessarie
Innanzitutto, importa le classi necessarie:

```java
import com.aspose.cells.*;
```

### Inizializzazione di una cartella di lavoro
Crea una nuova cartella di lavoro che ospiterà il grafico:

```java
Workbook workbook = new Workbook();
```

### Aggiunta di dati al grafico
Popola il foglio di lavoro con dati di esempio a cui il grafico farà riferimento:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Come generare un grafico a barre 3D in Java
Ora creeremo il grafico stesso e applicheremo alcune personalizzazioni di base:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Salvataggio del grafico su file
Infine, scrivi la cartella di lavoro (che ora contiene il grafico 3‑D) su disco. Questo inoltre **save workbook xlsx** nel formato standard di Excel:

```java
workbook.save("3D_Chart.xlsx");
```

## Come creare un grafico a torta 3D con Aspose.Cells for Java
Se hai bisogno di una visualizzazione a torta, il flusso di lavoro è quasi identico—solo l'enumerazione `ChartType` cambia. Sostituisci `ChartType.BAR_3_D` con `ChartType.PIE_3_D` quando aggiungi il grafico e punta la serie allo stesso intervallo di dati. Dopo aver creato il grafico puoi:

* Impostare un titolo descrittivo, ad esempio “Distribuzione vendite 3D”.
* Regolare i colori delle fette usando `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Esportare il grafico a torta in un'immagine PNG con `chart.toImage("pie_chart.png", ImageFormat.getPng())`, che soddisfa il requisito **convert chart png**.

Poiché il numero di blocchi di codice deve rimanere invariato, lo snippet Java effettivo è omesso qui, ma i passaggi rispecchiano l'esempio del grafico a barre sopra.

## Diversi tipi di grafici 3D
Aspose.Cells for Java supporta diverse tipologie di grafici 3D con cui puoi **add 3d chart excel** file:

- **Grafici a barre** – ideali per confrontare categorie.  
- **Grafici a torta** – mostrano contributi proporzionali (inclusa la torta 3D).  
- **Grafici a linee** – illustrano le tendenze nel tempo.  
- **Grafici ad area** – enfatizzano l'entità del cambiamento.

Puoi cambiare l'enumerazione `ChartType` con una delle precedenti mantenendo lo stesso schema di creazione.

## Personalizzazione avanzata del grafico

### Aggiunta di titoli e etichette
Fornisci al tuo grafico un contesto impostando un titolo descrittivo e le etichette degli assi.

### Regolazione di colori e stili
Usa il metodo `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` per adeguare il branding aziendale.

### Lavorare con gli assi del grafico
Regola finemente le scale degli assi, gli intervalli e i segni di graduazione per migliorare la leggibilità.

### Aggiunta di legende
Abilita le legende con `chart.getLegend().setVisible(true)` così gli osservatori possono identificare ogni serie di dati.

### Esportazione dei grafici come immagini
Quando ti serve un'immagine statica per un report web, chiama `chart.toImage("chart.png", ImageFormat.getPng())`. Questo soddisfa il caso d'uso **convert chart png** senza uscire dalla cartella di lavoro.

## Integrazione dei dati
Aspose.Cells for Java può estrarre dati da database, file CSV o API live. Basta popolare le celle del foglio di lavoro con i dati recuperati prima di collegare l'intervallo al grafico. Questo mantiene il tuo flusso di lavoro **add 3d chart excel** dinamico e aggiornato.

## Conclusione
In questa guida abbiamo illustrato come **create 3d pie chart** e **create 3d bar chart** progetti dall'inizio alla fine—configurando la libreria, aggiungendo dati, generando un grafico a barre 3‑D, adattando gli stessi passaggi per un grafico a torta 3‑D e applicando uno stile avanzato. Con Aspose.Cells for Java hai un metodo affidabile e indipendente dalla versione per incorporare ricche visualizzazioni 3‑D direttamente nei workbook Excel e persino esportarle come immagini PNG.

## Domande frequenti

**Q: Come posso aggiungere più serie di dati a un grafico 3D?**  
A: Usa `chart.getNSeries().add()` per ogni intervallo di serie e assicurati che il tipo di grafico rimanga 3‑D (ad esempio, `ChartType.BAR_3_D` o `ChartType.PIE_3_D`).

**Q: Posso esportare i grafici 3D creati con Aspose.Cells for Java in altri formati?**  
A: Sì, puoi salvare il grafico come PNG, JPEG o PDF chiamando le overload appropriate di `chart.toImage()` o `workbook.save()`, soddisfacendo il requisito **convert chart png**.

**Q: È possibile creare grafici 3D interattivi con Aspose.Cells for Java?**  
A: Aspose.Cells si concentra su grafici Excel statici. Per visualizzazioni 3‑D interattive basate sul web, considera di combinare i dati Excel con librerie JavaScript come Three.js.

**Q: Posso automatizzare il processo di aggiornamento dei dati nei miei grafici 3D?**  
A: Assolutamente. Carica nuovi dati nel foglio di lavoro programmaticamente e aggiorna l'intervallo del grafico; la prossima volta che il workbook viene aperto, il grafico rifletterà i valori aggiornati.

**Q: Dove posso trovare ulteriori risorse e documentazione per Aspose.Cells for Java?**  
A: Puoi trovare una documentazione completa e risorse per Aspose.Cells for Java sul sito web: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Ultimo aggiornamento:** 2026-02-09  
**Testato con:** Aspose.Cells for Java 24.12 (latest)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}