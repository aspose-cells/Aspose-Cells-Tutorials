---
category: general
date: 2026-06-30
description: Crea un'istanza di GridJs in Python con impostazioni personalizzate del
  modal. Scopri come collegare un foglio di lavoro, configurare il modal e generare
  il JSON client.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: it
og_description: Crea un'istanza GridJs in Python con impostazioni modal personalizzate.
  Istruzioni passo‑passo per l'integrazione del foglio di lavoro e la configurazione
  del client.
og_title: Crea un'istanza GridJs – Guida completa a Python
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: Crea un'istanza GridJs – Guida completa a Python
url: /it/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un'istanza GridJs – Guida completa Python

Ti sei mai chiesto come **create gridjs instance** da Python senza impazzire? Non sei l'unico. Che tu stia costruendo una dashboard admin, un catalogo prodotti o un foglio di calcolo veloce, far funzionare GridJs è il primo ostacolo.  

In questo tutorial percorreremo un esempio reale: collegare un worksheet, attivare un modal personalizzato che appare al doppio clic e infine estrarre il JSON di configurazione client‑side così da poterlo fornire al front‑end. Alla fine avrai una configurazione GridJs funzionante da inserire in qualsiasi progetto Flask o Django.

## Prerequisiti

- Python 3.8+ installato localmente  
- Familiarità di base con OOP in Python  
- Una classe `Worksheet` minimale (ne simuliamo una per la demo)  

Non esiste un pacchetto GridJs esterno per Python, quindi simuleremo l'API che rispecchia la libreria JavaScript. I concetti si traducono direttamente all'uso reale di GridJs in JavaScript.

## Passo 1: Definisci una classe Mock GridJs (API GridJs per Python)

Prima di poter **create gridjs instance**, abbiamo bisogno di un wrapper leggero che imiti la libreria reale. Questo mantiene l'esempio eseguibile e si concentra sul flusso di configurazione.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **Consiglio:** Mantieni il wrapper Python leggero—basta così per generare il JSON che passerai al lato JavaScript. Un'eccessiva ingegnerizzazione del ponte aggiunge oneri di manutenzione.

## Passo 2: Crea un semplice oggetto Worksheet (Integrazione Worksheet GridJs)

La nostra **gridjs worksheet integration** può essere semplice come una classe con un attributo `name`. In un'app reale estrarresti i dati da un database o da un file CSV.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

Ora hai un segnaposto che puoi passare alla griglia.

## Passo 3: Assembla la griglia – La logica centrale “Create GridJs Instance”

Con le classi mock pronte, possiamo finalmente **create gridjs instance** e configurarla passo dopo passo.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### Output previsto (Configurazione client GridJs)

Eseguendo `python main.py` ottieni un blob JSON formattato correttamente:

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

Quel JSON è esattamente ciò che passeresti al costruttore GridJs del front‑end:

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## Passo 4: Collega il JSON a una pagina front‑end (Mettere tutto insieme)

La **gridjs client configuration** che hai appena stampato può essere incorporata in una route Flask:

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **Perché funziona:** Il back‑end fornisce un payload JSON che rispecchia le impostazioni definite in Python. Il front‑end legge lo stesso payload, garantendo che il **gridjs custom modal** si comporti esattamente come hai configurato.

## Problemi comuni e casi limite (GridJs Custom Modal)

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| Il modal non si apre al doppio clic | `custom_modal.enabled` lasciato su `False` | Assicurati di impostare `grid.settings.custom_modal.enabled = True` |
| Le dimensioni del modal appaiono strane su mobile | Valori in pixel fissi (`600px`) non si adattano | Usa unità CSS relative (`80%`, `vh`) o media query |
| L'URL restituisce 404 | Il percorso `/product-editor.html` non è servito | Aggiungi una route statica in Flask/Django o ospita il file su un CDN |
| Nome del Worksheet mancante nel JSON | L'oggetto `Worksheet` non ha l'attributo `name` | Fornisci un `name` significativo o estendi il mock per includere metadati |

Affrontare questi problemi in anticipo ti farà risparmiare ore di debug in seguito.

## Estendere l'esempio (Passi successivi)

- **Carica dati reali**: Sostituisci il mock `Worksheet` con un pandas DataFrame e serializza le righe in JSON.  
- **Proteggi il modal**: Aggiungi controlli di autenticazione prima di servire `/product-editor.html`.  
- **Mappatura dinamica delle colonne**: Recupera le intestazioni delle colonne dallo schema del worksheet invece di codificarle manualmente.  
- **Internazionalizzazione**: Conserva i titoli del modal in un file di lingua e iniettali tramite il payload JSON.  

Tutte queste migliorie si basano sulla stessa base **create gridjs instance** che hai appena padroneggiato.

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **create gridjs instance** in Python, dalla configurazione di un worksheet all'attivazione di un modal personalizzato e infine all'esposizione di un JSON di configurazione client‑side pulito. Il pattern è semplice, riutilizzabile e si integra perfettamente in qualsiasi framework web moderno.

Provalo, modifica le dimensioni del modal, sostituisci il worksheet con una query reale al database, e avrai un'integrazione GridJs pronta per la produzione in pochissimo tempo. Hai domande? Lascia un commento e buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare e configurare cartelle di lavoro Excel con Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Creare un PDF di grafico dimensioni personalizzate con Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [Come creare una funzione di valore statico personalizzata in Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}