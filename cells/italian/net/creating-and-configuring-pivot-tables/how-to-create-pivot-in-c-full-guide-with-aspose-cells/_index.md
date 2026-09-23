---
category: general
date: 2026-03-27
description: Come creare una tabella pivot in C# con Aspose.Cells – impara ad aggiungere
  dati, abilitare l'aggiornamento e salvare la cartella di lavoro come xlsx in un
  unico tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: it
og_description: Come creare una tabella pivot in C# con Aspose.Cells. Questa guida
  ti mostra come aggiungere dati, abilitare l'aggiornamento e salvare la cartella
  di lavoro come xlsx.
og_title: Come creare una tabella pivot in C# – Tutorial completo di Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come creare una tabella pivot in C# – Guida completa con Aspose.Cells
url: /it/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una tabella pivot in C# – Tutorial completo di Aspose.Cells

Ti sei mai chiesto **come creare una pivot** in C# senza combattere con l'interoperabilità COM? Non sei l'unico. In molte applicazioni basate sui dati abbiamo bisogno di un modo rapido per trasformare i dati grezzi di vendita in un riepilogo ordinato, e Aspose.Cells lo rende un gioco da ragazzi.  

In questo tutorial percorreremo ogni passaggio: aggiungere dati, costruire la tabella pivot, attivare l'aggiornamento automatico e infine **salvare la cartella di lavoro come xlsx** così i tuoi utenti potranno aprirla in Excel immediatamente. Alla fine avrai un file `PivotRefresh.xlsx` pronto all'uso e una solida comprensione del motivo per cui ogni riga è importante.

## Prerequisiti

- .NET 6+ (o .NET Framework 4.7.2 e successive) – qualsiasi runtime recente funziona.  
- Aspose.Cells per .NET – puoi scaricarlo da NuGet (`Install-Package Aspose.Cells`).  
- Una conoscenza di base della sintassi C# – non è necessario una conoscenza approfondita di Excel.  

> **Suggerimento:** Se sei su una macchina aziendale, assicurati che la licenza Aspose sia applicata; altrimenti otterrai una filigrana sul file generato.

## Passo 1 – Come aggiungere dati a una nuova cartella di lavoro

Prima che una pivot possa esistere, deve esserci una tabella di origine. Creeremo una nuova cartella di lavoro, chiameremo il primo foglio *SalesData* e inseriremo alcune righe che imitano un dump di vendite reale.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Perché è importante:**  
- Usare `PutValue` imposta automaticamente il tipo di cella, così non dovrai preoccuparti di incompatibilità tra stringhe e numeri in seguito.  
- Definire le intestazioni nella riga 1 fornisce al motore della pivot qualcosa a cui fare riferimento quando mappi i campi.

## Passo 2 – Creare un foglio di lavoro che ospiterà la tabella pivot

Una tabella pivot vive su un foglio dedicato, mantenendo i dati di origine puliti e il report ordinato.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **E se hai già un foglio?** Basta fare riferimento ad esso per indice (`workbook.Worksheets["MySheet"]`) invece di aggiungerne uno nuovo.

## Passo 3 – Definire l'intervallo di origine (Come aggiungere dati → Definire intervallo)

Aspose.Cells necessita di un `CellArea` o di una stringa di intervallo che includa sia le intestazioni che i dati. Qui assumiamo un massimo di 100 righe; regola secondo le necessità.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Caso limite:** Se il tuo set di dati è dinamico, puoi calcolare l'ultima riga utilizzata con `salesDataSheet.Cells.MaxDataRow` e costruire l'intervallo di conseguenza.

## Passo 4 – Come creare una pivot – Inserire la tabella pivot

Ora la parte divertente: diciamo ad Aspose.Cells di creare una pivot collegata all'intervallo appena impostato.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Nota il riferimento in stile formula (`=SalesData!A1:D100`). È la stessa sintassi che inseriresti in Excel, il che rende l'API intuitiva.

## Passo 5 – Configurare i campi di riga, colonna e dati (Come aggiungere dati → Campi)

Posizioneremo *Region* sulle righe, *Product* sulle colonne e sommeremo sia *Units* che *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Perché questi indici?**  
Aspose.Cells indicizza le colonne a partire da 0, quindi `0` corrisponde a *Region*. Il metodo `DataFields.Add` ti permette di rinominare il campo (ad es., “Sum of Units”) e scegliere un tipo di aggregazione – `Sum` è il più comune per i dati numerici.

## Passo 6 – Come abilitare l'aggiornamento – Far sì che la pivot si aggiorni automaticamente all'apertura

Se i dati di origine cambiano in seguito, probabilmente vuoi che la pivot rifletta automaticamente tali modifiche. È qui che `RefreshDataOnOpen` brilla.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Nota:** Questa opzione funziona solo quando la cartella di lavoro è aperta in Excel; non ricalcolerà all'interno di Aspose.Cells a meno che non chiami manualmente `pivotTable.RefreshData()`.

## Passo 7 – Salvare la cartella di lavoro come XLSX (Come salvare la cartella di lavoro come XLSX)

Infine, salviamo il file su disco. Il formato `.xlsx` è il moderno tipo di file Excel basato su zip che funziona ovunque.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Eseguendo il programma si genera un file chiamato **PivotRefresh.xlsx** nella cartella di esecuzione. Aprilo in Excel e vedrai una pivot ordinata con righe *Region*, colonne *Product* e valori sommati di *Units* e *Revenue*. Poiché abbiamo abilitato l'aggiornamento, qualsiasi modifica apportata al foglio *SalesData* aggiornerà automaticamente la pivot al successivo riapertura della cartella di lavoro.

### Output previsto

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(I numeri varieranno in base alle righe che aggiungi.)*

---

## Domande comuni e variazioni

### E se ho bisogno di più tabelle pivot?

Puoi ripetere **Passo 4** con un nome e una posizione diversi. Ogni chiamata a `PivotTables.Add` restituisce un nuovo indice che puoi usare per recuperare l'oggetto tabella.

### Come cambio l'aggregazione in *Average* invece di *Sum*?

Sostituisci `PivotTableDataAggregationType.Sum` con `PivotTableDataAggregationType.Average` nelle chiamate `DataFields.Add`.

### Posso stilizzare la pivot (font, colori)?

Sì. Dopo aver creato la pivot, puoi accedere alla sua proprietà `Style` o applicare formattazioni alle celle dell'intervallo che contiene la pivot. Per esempio:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### È possibile aggiungere più righe dopo aver salvato la cartella di lavoro?

Assolutamente. Carica il file con `new Workbook("PivotRefresh.xlsx")`, aggiungi righe al foglio *SalesData* e chiama `pivotTable.RefreshData()` prima di salvare nuovamente.

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Salva il file, eseguilo e apri il **PivotRefresh.xlsx** generato – hai appena imparato **come creare una pivot** in C#.

## Conclusioni

Abbiamo coperto **come creare tabelle pivot** programmaticamente, come **aggiungere dati**, come **abilitare l'aggiornamento**, e infine come **salvare la cartella di lavoro come xlsx** usando Aspose.Cells. Il codice

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}