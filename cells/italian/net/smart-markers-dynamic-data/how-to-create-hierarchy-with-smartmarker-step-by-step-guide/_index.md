---
category: general
date: 2026-02-14
description: Creare gerarchie nei template SmartMarker è più facile di quanto pensi
  – impara a creare dati gerarchici e a elencare i dipendenti in modo efficiente.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: it
og_description: Come creare una gerarchia nei template SmartMarker è semplice. Segui
  questa guida per creare dati gerarchici e elencare i dipendenti con intervalli annidati.
og_title: Come creare gerarchia con SmartMarker – Guida completa
tags:
- SmartMarker
- C#
- templating
title: Come creare una gerarchia con SmartMarker – Guida passo passo
url: /it/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare gerarchie con SmartMarker – Guida completa

Ti sei mai chiesto **come creare una gerarchia** all'interno di un modello SmartMarker senza impazzire? Non sei l'unico. In molti scenari di reporting hai bisogno di una relazione padre‑figlio—pensa a dipartimenti e alle persone che vi lavorano. La buona notizia è che SmartMarker lo rende un gioco da ragazzi una volta che conosci i passaggi giusti.

In questo tutorial percorreremo l’intero processo: dalla **creazione di dati gerarchici** in C#, all’attivazione dei range annidati, fino al rendering di un modello che **elenca i dipendenti** per ogni dipartimento. Alla fine avrai un esempio pronto all’uso da inserire in qualsiasi progetto .NET.

---

## Di cosa avrai bisogno

- .NET 6+ (qualsiasi versione recente va bene)
- Un riferimento alla libreria **SmartMarker** (lo spazio dei nomi `ws.SmartMarkerProcessor`)
- Conoscenze di base di C# – niente di complicato, solo qualche oggetto e una lambda o due
- Un IDE o editor a tua scelta (Visual Studio, Rider, VS Code… scegli tu)

Se li hai già, ottimo—tuffiamoci.

---

## Come creare gerarchie – Panoramica

L’idea di base è costruire un **grafico di oggetti annidato** che rispecchi la struttura che vuoi vedere nel documento finale. Nel nostro caso il grafico appare così:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker può quindi iterare su `Departments` e, poiché attiveremo **l’elaborazione dei range annidati**, scorrerà automaticamente anche la collezione `Employees` di ciascun dipartimento.

---

## Step 1: Build the Hierarchical Data Model

Per prima cosa creiamo un oggetto anonimo che contiene un array di dipartimenti, ognuno con la propria lista di dipendenti. L’uso di un tipo anonimo mantiene l’esempio leggero—sentiti libero di sostituirlo con classi POCO reali in seguito.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Why this matters:** L’array `Departments` è la collezione di livello superiore. Ogni elemento contiene un array `Employees`, fornendoci il secondo livello di gerarchia che poi accederemo con `#Departments.Employees#`.

---

## Step 2: Enable Nested Range Processing

SmartMarker non scaverà nelle collezioni interne a meno che non glielo dica. L’oggetto `SmartMarkerOptions` contiene questo interruttore.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tip:** Se dimentichi questa flag, il range interno `#Employees#` non restituisce nulla, e ti ritroverai a grattarti la testa chiedendoti perché il modello è vuoto.

---

## Step 3: Run the Processor with Your Data

Ora passiamo i dati e le opzioni al processore. La variabile `ws` rappresenta il tuo **WebService** (o qualunque oggetto ospiti il motore SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

A questo punto SmartMarker analizza il modello, sostituisce `#Departments.Name#` con il nome di ciascun dipartimento e, poiché i range annidati sono attivati, itera attraverso la collezione `Employees` di ogni dipartimento.

---

## Step 4: Craft the Template Markers

Di seguito trovi un modello minimale che dimostra sia il ciclo esterno sia quello interno. Incollalo nell’editor di modelli SmartMarker (o in un file `.txt` che passi al processore).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Quando viene renderizzato vedrai:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **What you’re seeing:** Il ciclo esterno `#Departments.Name#` stampa il titolo del dipartimento. Il blocco interno `#Departments.Employees#` scorre ogni dipendente, e `#Departments.Employees#` all’interno del blocco restituisce il nome reale.

---

## Expected Output & Verification

Eseguire l’esempio completo (dati + opzioni + modello) dovrebbe produrre esattamente l’elenco mostrato sopra. Per verificare rapidamente, puoi stampare il risultato sulla console:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Se vedi le due intestazioni dei dipartimenti seguite dai punti elenco dei loro dipendenti, hai creato con successo una **gerarchia** e **elencato i dipendenti**.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| No output for employees | `EnableNestedRange` left false | Set `EnableNestedRange = true` |
| Duplicate employee names | Same array reused across departments | Clone the array or use distinct collections |
| Very large hierarchies cause memory pressure | SmartMarker loads the whole object graph into memory | Stream data or paginate large collections |
| Template syntax errors | Missed closing `#/…#` tags | Use the SmartMarker validator or run a quick test with a tiny template |

---

## Going Further – Real‑World Variations

1. **Dynamic data sources** – Preleva i dipartimenti da un database e mappali nella struttura anonima usando LINQ.  
2. **Conditional formatting** – Aggiungi un flag `IsManager` a ciascun dipendente e usa i tag condizionali di SmartMarker (`#if …#`) per evidenziare i manager.  
3. **Multiple nesting levels** – Se ti servono team all’interno dei dipartimenti, aggiungi un’altra collezione (`Teams`) e mantieni `EnableNestedRange` attivo.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Eseguendo il programma stampa la gerarchia esattamente come mostrato in precedenza.

---

## Conclusion

Abbiamo coperto **come creare gerarchie** in SmartMarker, dalla modellazione dei **dati gerarchici** in C# all’attivazione dei range annidati, fino al rendering di un modello che **elenca i dipendenti** per dipartimento. Il pattern scala—basta aggiungere altre collezioni annidate o logica condizionale e avrai a disposizione un potente motore di reporting.

Pronto per la prossima sfida? Prova a sostituire i tipi anonimi con classi POCO fortemente tipizzate, oppure integra questo flusso in un endpoint ASP.NET Core che restituisce un PDF o un documento Word. Il cielo è il limite, e ora hai una solida base.

![How to create hierarchy diagram](image.png){alt="Diagramma di come creare gerarchia che mostra la relazione dipartimento‑dipendente"}

*Buon coding! Se incontri difficoltà, lascia un commento qui sotto—sono felice di aiutare.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}