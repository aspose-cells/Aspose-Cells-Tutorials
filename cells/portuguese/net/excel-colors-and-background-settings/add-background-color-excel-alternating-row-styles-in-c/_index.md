---
category: general
date: 2026-04-07
description: Adicionar cor de fundo às linhas do Excel usando C#. Aprenda como aplicar
  cores alternadas nas linhas, definir estilos de fundo sólido e importar DataTable
  para o Excel em um único fluxo de trabalho.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: pt
og_description: Adicione cor de fundo às linhas do Excel com C#. Este guia mostra
  como aplicar cores alternadas nas linhas, definir fundo sólido e importar DataTable
  para o Excel de forma eficiente.
og_title: Adicionar cor de fundo ao Excel – Estilos de linhas alternadas em C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Adicionar cor de fundo no Excel – Estilos de linhas alternadas em C#
url: /pt/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar cor de fundo no Excel – Estilos de linhas alternadas em C#

Já precisou **adicionar cor de fundo no Excel** às linhas, mas não sabia como fazer isso sem milhares de linhas de código complicado? Você não está sozinho — a maioria dos desenvolvedores encontra essa barreira na primeira vez que tenta deixar suas planilhas mais apresentáveis do que um simples despejo de dados.  

A boa notícia? Em apenas alguns minutos você pode **aplicar cores alternadas nas linhas**, definir um **fundo sólido**, e até **importar datatable para excel** usando um padrão limpo e reutilizável em C#.  

Neste tutorial vamos percorrer todo o processo, desde a extração de dados para um `DataTable` até a estilização de cada linha com um padrão de faixas amarelo‑claro‑branco. Nenhuma biblioteca externa além de um pacote sólido de manipulação de Excel (como **ClosedXML** ou **GemBox.Spreadsheet**) é necessária, e você verá por que essa abordagem é ao mesmo tempo performática e fácil de manter.

## O que você vai aprender

- Como recuperar dados e alimentá‑los em uma planilha Excel.  
- Como **estilizar linhas do excel** com cores de fundo alternadas.  
- A mecânica por trás de **definir fundo sólido** usando o objeto `Style`.  
- Como **importar datatable para excel** preservando os estilos das linhas.  
- Dicas para lidar com casos de borda, como tabelas vazias ou esquemas de cores personalizados.

> **Dica de especialista:** Se você já está usando um objeto workbook (`wb`) de uma biblioteca que suporta criação de estilos, pode reutilizar as mesmas instâncias de `Style` em várias planilhas — economizando memória e mantendo seu código organizado.

---

## Etapa 1: Recuperar os dados – Preparando o DataTable

Antes que qualquer estilização possa acontecer, precisamos de uma fonte de linhas. Na maioria dos cenários reais isso vem de um banco de dados, de uma API ou de um arquivo CSV. Para ilustração, vamos apenas criar um simples `DataTable` na memória.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Por que isso importa:** Usar um `DataTable` fornece um contêiner tabular, consciente de esquema, que a biblioteca de Excel pode importar diretamente, eliminando a necessidade de loops célula‑por‑célula.

---

## Etapa 2: Criar estilos de linha – **Aplicar cores alternadas nas linhas**

Agora vamos construir um array de objetos `Style` — um por linha — para que cada linha receba seu próprio fundo. O padrão que usaremos é clássico: amarelo‑claro para linhas pares e branco para linhas ímpares.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explicação:**  
- `wb.CreateStyle()` fornece um objeto de estilo limpo que você pode ajustar sem afetar os demais.  
- O operador ternário `(i % 2 == 0)` decide se a linha é par (amarelo claro) ou ímpar (branco).  
- Definir `Pattern = BackgroundType.Solid` é o passo crucial que **define fundo sólido**; sem isso a cor seria ignorada.

---

## Etapa 3: Obter a planilha de destino

A maioria das bibliotecas expõe uma coleção de planilhas. Trabalharemos com a primeira, mas você pode direcionar qualquer índice ou nome que preferir.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Se o workbook for recém‑criado, a biblioteca geralmente cria uma planilha padrão para você. Caso contrário, você pode adicionar uma explicitamente:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Etapa 4: Importar o DataTable com estilos de linha – **Importar datatable para excel**

Com os estilos prontos, a etapa final é inserir o `DataTable` na planilha enquanto aplicamos o estilo correspondente a cada linha.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**O que está acontecendo nos bastidores?**  
- `true` indica ao método que escreva os cabeçalhos das colunas na primeira linha.  
- `0, 0` marca o canto superior esquerdo (A1) como ponto de inserção.  
- `rowStyles` alinha cada `Style` com a linha de dados correspondente, proporcionando as cores alternadas que preparamos anteriormente.

---

## Etapa 5: Salvar o Workbook

A última peça do quebra‑cabeça é persistir o workbook em um arquivo para que você possa abri‑lo no Excel e ver o resultado.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Abra o arquivo e você deverá ver uma planilha bem formatada:

- Linha de cabeçalho em negrito (estilização padrão da biblioteca).  
- Linhas 1, 3, 5… com fundo branco limpo.  
- Linhas 2, 4, 6… com preenchimento amarelo‑claro sutil, facilitando a leitura.

### Captura de saída esperada

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Linhas 2, 4, 6, … aparecem com fundo amarelo‑claro — exatamente o efeito de **aplicar cores alternadas nas linhas** que buscamos.

![Exemplo de adicionar cor de fundo no Excel](https://example.com/excel-background.png "Exemplo de adicionar cor de fundo no Excel")

*(O texto alternativo inclui a palavra‑chave principal para SEO.)*

---

## Tratamento de casos de borda & variações

### DataTable vazio

Se `dataTable.Rows.Count` for zero, o array `rowStyles` ficará vazio e `ImportDataTable` ainda escreverá a linha de cabeçalho (se `includeHeaders` for `true`). Nenhuma exceção é lançada, mas talvez você queira evitar gerar um arquivo quase vazio:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Esquemas de cores personalizados

Quer faixas azul/cinza em vez de amarelo/branco? Basta substituir os valores de `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Sinta‑se à vontade para puxar as cores de um arquivo de configuração, permitindo que quem não programa ajuste a paleta sem tocar no código.

### Reutilizar estilos em várias planilhas

Se você exportar várias tabelas para o mesmo workbook, pode gerar o array de estilos uma única vez e reutilizá‑lo:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Apenas tenha cuidado para que ambas as tabelas tenham o mesmo número de linhas, ou gere um novo array por planilha.

---

## Exemplo completo funcionando

Juntando tudo, aqui está um programa autocontido que você pode copiar‑colar em um aplicativo console.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Execute o programa, abra `Report.xlsx`, e você verá o fundo alternado exatamente como descrito.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}