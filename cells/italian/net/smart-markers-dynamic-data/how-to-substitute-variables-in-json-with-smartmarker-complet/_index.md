---
category: general
date: 2026-03-29
description: Come sostituire le variabili in JSON usando SmartMarker – impara a utilizzare
  l'espressione if, applicare la logica condizionale, moltiplicare i valori e generare
  JSON senza sforzo.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: it
og_description: Come sostituire le variabili in JSON usando SmartMarker. Scopri come
  utilizzare l'espressione if, applicare la logica condizionale, moltiplicare i valori
  e generare JSON in pochi minuti.
og_title: Come sostituire le variabili in JSON con SmartMarker – Passo dopo passo
tags:
- C#
- SmartMarker
- JSON templating
title: Come sostituire le variabili in JSON con SmartMarker – Guida completa
url: /it/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Sostituire le Variabili in JSON con SmartMarker – Guida Completa

Ti sei mai chiesto **come sostituire le variabili** all'interno di un payload JSON senza scrivere un parser personalizzato? Non sei solo. In molti scenari di integrazione—pensa a fatture, motori di pricing o file di configurazione dinamici—devi iniettare valori a runtime, applicare semplici condizioni e magari anche fare una rapida moltiplicazione. Questo tutorial ti mostra esattamente **come sostituire le variabili** usando la libreria SmartMarker, mantenendo il JSON pulito e leggibile.

Passeremo in rassegna un esempio reale che copre **use if expression**, **how to apply conditional**, **how to multiply values** e **how to generate json** al volo. Alla fine, avrai uno snippet C# pronto all'uso da inserire in qualsiasi progetto .NET.

## Cosa Imparerai

- Configura `SmartMarkerOptions` per memorizzare variabili riutilizzabili.  
- Scrivi un modello JSON che contenga un'espressione `if` per la logica condizionale.  
- Moltiplica un valore per una variabile all'interno del modello.  
- Processa il modello con `SmartMarkerProcessor` e ottieni la stringa JSON finale.  
- Risolvi i problemi comuni come variabili mancanti o espressioni malformate.

Nessun servizio esterno, nessuna dipendenza pesante—solo puro C# e il pacchetto NuGet SmartMarker.

---

## Come Sostituire le Variabili – Panoramica Passo‑per‑Passo

Di seguito è mostrata una panoramica ad alto livello del flusso di lavoro. Pensalo come una pipeline in cui il tuo modello JSON grezzo entra a sinistra, il motore SmartMarker fa la sua magia e il JSON completamente renderizzato esce a destra.

![Diagramma che mostra come sostituire le variabili in JSON](https://example.com/images/smartmarker-flow.png "Come sostituire le variabili in JSON")

*Testo alternativo dell'immagine: Diagramma che mostra come sostituire le variabili in JSON.*

---

## Passo 1: Installa e Importa SmartMarker

Prima di iniziare, assicurati che il pacchetto SmartMarker sia referenziato nel tuo progetto. Se usi la .NET CLI, esegui:

```bash
dotnet add package SmartMarker
```

Quindi, aggiungi le direttive `using` necessarie all'inizio del tuo file C#:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Consiglio:** L'ultima versione (a partire da marzo 2026) è 2.4.1. Supporta .NET 6 e versioni successive, ma funziona perfettamente anche con .NET Framework 4.7.

---

## Passo 2: Crea le Opzioni SmartMarker e Definisci le Variabili

Ora creeremo un'istanza di `SmartMarkerOptions` che conterrà tutte le variabili che vogliamo riutilizzare nel modello. Qui rispondiamo alla domanda **how to substitute variables**—le variabili fungono da segnaposto che SmartMarker sostituirà in seguito.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Perché memorizzare il tasso in `Variables` invece di hard‑codificarlo? Perché potresti prelevare quel numero da un database, da un file di configurazione o da un input utente. Tenerlo nelle opzioni rende il modello riutilizzabile e testabile.

---

## Passo 3: Scrivi il Modello JSON con un'Espressione `if`

Qui è dove brilla la parola chiave **use if expression**. SmartMarker ti permette di incorporare logica condizionale direttamente nella stringa JSON. La sintassi assomiglia a un nome di proprietà, ma SmartMarker la interpreta come una direttiva.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Nota la chiave `if(Amount>500)`. SmartMarker valuta l'espressione `Amount>500`; se è vera, il valore corrispondente (`${Amount * Rate}`) viene inserito nell'output. La sintassi `${...}` è il motore di *sostituzione delle variabili*—qui **how to multiply values** (`Amount * Rate`) prima di iniettare il risultato.

---

## Passo 4: Processa il Modello e Recupera il JSON Finale

Con le opzioni e il modello pronti, passiamo tutto al processore. Il metodo `ProcessJson` analizza il modello, applica la condizione, esegue la moltiplicazione e restituisce una stringa JSON pulita.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Eseguendo lo snippet stampa:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Cosa è successo?**  
- `Amount` è 1000, il che soddisfa `Amount>500`.  
- SmartMarker valuta `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- La chiave condizionale originale (`if(Amount>500)`) viene sostituita da un nome di proprietà pulito (`Result`). Per impostazione predefinita SmartMarker usa `"Result"` ma è possibile personalizzarlo (vedi più avanti).

Se cambi `Amount` a `400`, l'output diventa:

```json
{
  "Amount": 400
}
```

Il blocco condizionale scompare perché l'espressione è valutata come `false`. Questa è l'essenza della logica **how to apply conditional** in JSON.

---

## Passo 5: Personalizzare il Nome della Proprietà di Output (Opzionale)

A volte non vuoi la chiave generica `"Result"`. SmartMarker ti consente di specificare un nome personalizzato usando l'opzione `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Ora il valore condizionale è memorizzato sotto un nome di proprietà più significativo—perfetto per i servizi downstream che si aspettano un campo specifico.

---

## Problemi Comuni e Come Evitarli

| Problema | Perché Succede | Soluzione |
|----------|----------------|-----------|
| Variabile non trovata | Hai fatto riferimento a una variabile che non è presente in `smartMarkerOptions.Variables`. | Controlla l'ortografia e assicurati che la variabile sia aggiunta prima del processing. |
| Sintassi `if` non valida | Mancano parentesi o l'operatore è errato (`>`, `<`, `==`). | Segui esattamente il pattern `if(<expression>)`; SmartMarker supporta solo semplici confronti numerici. |
| JSON malformato | Hai lasciato accidentalmente una virgola finale dopo il blocco condizionale. | Lascia che SmartMarker gestisca la rimozione; mantieni il modello originale sintatticamente corretto. |
| Formato numerico inaspettato | Il risultato appare come stringa `"80"` invece di un numero. | Esegui il cast o il parsing successivamente, o usa `${(Amount * Rate):N0}` per la formattazione numerica. |

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il programma completo che puoi compilare ed eseguire. Dimostra **how to generate json** con variabili dinamiche, condizioni e operazioni aritmetiche—tutto in meno di 30 righe.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Output previsto della console**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Sentiti libero di modificare `Amount` per testare il ramo condizionale, o di regolare `Rate` per vedere diversi calcoli di sconto.

---

## Estendere il Pattern – Altri Scenari “How to”

- **How to substitute variables** da un file di configurazione: Carica un `Dictionary<string, object>` da `appsettings.json` e inseriscilo in `smartMarkerOptions.Variables`.  
- **How to use if expression** per più condizioni: concatenale così `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker supporta AND/OR logici.  
- **How to apply conditional** formatting: Usa `${Amount:0.00}` all'interno dell'espressione per controllare i decimali.  
- **How to multiply values** con matematica più complessa: `${(Amount - Discount) * TaxRate}` funziona allo stesso modo.  
- **how to generate json** per oggetti nidificati: Inserisci il blocco condizionale all'interno di un altro oggetto JSON, e SmartMarker manterrà la gerarchia.

---

## Conclusione

Abbiamo coperto **how to substitute variables** in JSON usando SmartMarker, mostrato **use if expression** per l'inclusione condizionale, spiegato **how to apply conditional** logic, mostrato **how to multiply values** all'interno di un modello, e infine illustrato **how to generate json** pronto per il consumo downstream. L'approccio è leggero, non richiede motori di templating esterni e si integra perfettamente in qualsiasi codebase C#.

Provalo—modifica le variabili, aggiungi più condizioni, o avvolgi il tutto in una classe helper per il riuso nella tua soluzione. Quando hai bisogno di generare JSON dinamico rapidamente, SmartMarker è un'opzione solida e pronta per la produzione.

**Passi successivi**

- Approfondisci le funzionalità avanzate di SmartMarker come i loop (`foreach`) e le funzioni personalizzate.  
- Combina questa tecnica con endpoint ASP.NET Core per servire API JSON dinamiche.  
- Esplora altre librerie di templating (ad esempio, Handlebars.NET) per il confronto, soprattutto se ti serve una sintassi più ricca.

Hai domande o un caso d'uso specifico su cui stai lavorando? Lascia un commento qui sotto e risolviamo insieme. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}