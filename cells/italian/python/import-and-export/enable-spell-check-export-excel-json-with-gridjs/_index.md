---
category: general
date: 2026-06-21
description: Abilita il controllo ortografico mentre esporti JSON da Excel usando
  GridJs. Impara a convertire xlsx in JSON, configurare il lazy loading e caricare
  il workbook Excel in modo efficiente.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: it
og_description: Abilita il controllo ortografico durante l'esportazione di Excel JSON
  con GridJs. Questa guida mostra come convertire xlsx in JSON, configurare il caricamento
  lazy e caricare una cartella di lavoro Excel.
og_title: Abilita il controllo ortografico e l'esportazione Excel JSON con GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Abilita il controllo ortografico e l'esportazione di Excel JSON con GridJs
url: /it/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abilita il Controllo Ortografico e Esporta Excel JSON con GridJs

Ti è mai capitato di dover **abilitare il controllo ortografico** in un'interfaccia di foglio di calcolo basata sul web e di chiederti come ottenere i dati in formato JSON allo stesso tempo? Non sei l'unico. Molti sviluppatori si trovano nella stessa situazione quando cercano di **esportare Excel JSON** da una cartella di lavoro mantenendo attive funzionalità avanzate come la convalida delle formule.

In questo tutorial percorreremo un esempio completo e funzionante che mostra come **caricare una cartella di lavoro Excel**, trasformarla in un payload JSON con GridJs, **configurare il lazy loading** e, naturalmente, **abilitare il controllo ortografico**. Alla fine sarai in grado di **convertire xlsx in JSON** in poche righe—senza misteri, senza pezzi mancanti.

> **Cosa otterrai**  
> * Uno script Python che legge un file `.xlsx`, avvia un oggetto server GridJs e scrive `grid_data.json`.  
> * Una comprensione del perché ogni opzione è importante (controllo ortografico, verifica delle formule, lazy loading).  
> * Suggerimenti per scalare la soluzione a cartelle di lavoro più grandi.

---

## Prerequisiti

Prima di immergerci, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.9+ | Necessario per il pacchetto `cells` usato di seguito. |
| Libreria `cells` (`pip install cells`) | Fornisce le classi `Workbook` e `GridJs`. |
| Un file Excel di esempio (`sample.xlsx`) | È la sorgente da cui **caricheremo la cartella di lavoro Excel**. |
| Permessi di scrittura nella cartella di output | Necessari per il passaggio `grid.save()`. |

Se qualcuno di questi ti è sconosciuto, fermati e installalo prima—altrimenti lo script genererà un errore di importazione.

---

## Passo 1: Carica la Cartella di Lavoro Excel

La prima cosa da fare quando vuoi **convertire xlsx in json** è aprire la cartella di lavoro. Pensala come sbloccare la porta prima di poter decorare la stanza.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Consiglio professionale:** Se il tuo file è molto grande, considera l'uso di `cells.Workbook(..., read_only=True)` per ridurre il consumo di memoria.

---

## Passo 2: Crea un Oggetto Server GridJs

Ora che la cartella di lavoro è in memoria, ci serve un oggetto **GridJs** che traduca i fogli in JSON consumabile dall'interfaccia client.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

La variabile `grid` è essenzialmente un involucro leggero attorno alla cartella di lavoro che sa come serializzare celle, formule e persino informazioni di stile.

---

## Passo 3: Abilita il Controllo Ortografico (e il Verificatore di Formule)

Qui entra in gioco la parola chiave principale. Attivando il flag `enableSpellCheck`, offri agli utenti finali una rete di sicurezza contro gli errori di battitura—proprio come in Excel desktop.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Perché abilitarli entrambi? Il controllo ortografico cattura errori testuali, mentre il verificatore di formule protegge da calcoli interrotti. Insieme rendono l'interfaccia web così curata quanto l'esperienza nativa di Excel.

---

## Passo 4: Configura il Lazy Loading

Se devi gestire migliaia di righe, inviare l'intero dataset in un unico payload soffocherebbe il browser. **Configura il lazy loading** per spedire i dati a pezzetti (500 righe per richiesta nel nostro esempio).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Puoi regolare `pageSize` in base alle condizioni della tua rete. Pagine più piccole significano più round‑trip ma un'interfaccia più fluida; pagine più grandi riducono le chiamate ma possono causare rallentamenti.

---

## Passo 5: Esporta Excel JSON

Tutto il lavoro pesante è ora dietro le quinte. L'atto finale è **esportare excel json** in un file che il front‑end può richiedere.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Quando il metodo `save` termina, avrai un ordinato `grid_data.json` contenente:

* Nomi e ID dei fogli  
* Dati delle righe (valori, formule e formattazione)  
* Metadati sulle funzionalità abilitate (controllo ortografico, lazy loading, ecc.)

Puoi verificare l'output aprendo il file in un editor di testo o caricandolo nella console del browser:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Questa è una **soluzione completa e autonoma** per trasformare un file Excel in un payload JSON mantenendo attivo il controllo ortografico.

---

## Script Completo – Metti Tutto Insieme

Di seguito trovi l'intero programma che puoi copiare‑incollare, modificare i percorsi e far girare. Nessun passaggio nascosto, nessuno script esterno—solo un file.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Salva questo come `export_gridjs.py` ed esegui:

```bash
python export_gridjs.py
```

Dovresti vedere una serie di messaggi `[✓]` che confermano il successo di ogni passaggio.

---

## Domande Frequenti & Casi Limite

**E se la mia cartella di lavoro contiene più fogli?**  
GridJs itera automaticamente su tutti i fogli, quindi il JSON risultante avrà un array `sheets`. Puoi filtrare lato client se ti serve solo un sottoinsieme.

**Posso disabilitare il controllo ortografico per un foglio specifico?**  
Il dizionario `options` si applica globalmente. Per gestirlo per foglio dovresti creare oggetti `GridJs` separati o post‑processare il JSON.

**Il mio file è più grande di 10 MB—il lazy loading è ancora utile?**  
Assolutamente. Il lazy loading opera a livello di API; il server trasmette solo la pagina richiesta. Tuttavia, considera di aumentare `pageSize` a 1000 se la latenza della rete è bassa.

**Devo preoccuparmi dei caratteri Unicode?**  
`cells` gestisce UTF‑8 nativamente, quindi emoji o script non latini sopravvivono al round‑trip.

---

## Consigli Pro per la Produzione

* **Cache del JSON** – Se la cartella di lavoro cambia raramente, cache `grid_data.json` in una CDN per caricamenti fulminei.  
* **Sicurezza** – Non esporre mai il file Excel grezzo; servi solo il JSON generato.  
* **Versionamento** – Inserisci un numero di versione nel nome del file JSON (es. `grid_data_v2.json`) per evitare dati obsoleti dopo gli aggiornamenti.  
* **Testing** – Scrivi un piccolo test unitario che carica il JSON e verifica che `enableSpellCheck` sia `true`. Cattura regressioni presto.

---

## Conclusione

Ora disponi di una ricetta solida, end‑to‑end, per **abilitare il controllo ortografico** mentre **esporti Excel JSON** usando GridJs. Dal **caricamento della cartella di lavoro Excel** alla **configurazione del lazy loading** fino alla **conversione xlsx in json**, il processo è lineare e pronto per la produzione.

Prossimi passi? Prova a collegare il `grid_data.json` generato a una semplice pagina HTML che utilizza la libreria client GridJs, sperimenta con renderer di celle personalizzati o aggiungi autenticazione attorno all'endpoint JSON. Il cielo è il limite quando combini controllo ortografico, lazy loading e conversione fluida da Excel a JSON.

Hai altre domande o un workbook ostico con cui stai lottando? Lascia un commento qui sotto, e buona programmazione!  

---

![Abilita il controllo ortografico in GridJs](/images/enable-spell-check-gridjs.png "Screenshot che mostra il controllo ortografico abilitato nell'interfaccia GridJs")


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Esporta Excel in JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Importa dati JSON in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Come filtrare efficientemente i dati durante il caricamento di cartelle di lavoro Excel usando Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}