---
category: general
date: 2026-02-09
description: Como criar uma pasta de trabalho em C# com fundo azul‑claro e importar
  dados com cabeçalhos. Aprenda a adicionar fundo azul‑claro, usar o estilo padrão
  do Excel e importar DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: pt
og_description: Como criar uma pasta de trabalho em C# com fundo azul claro, importar
  dados com cabeçalhos e aplicar o estilo padrão do Excel — tudo em um guia conciso.
og_title: Como criar uma pasta de trabalho – fundo azul claro, importação de dados
tags:
- C#
- Excel
- Aspose.Cells
title: Como criar pasta de trabalho – Fundo azul‑claro, importação de dados
url: /pt/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

any URLs: none.

Check for any markdown links: none.

Check for code fences: placeholders only.

Make sure to preserve headings count.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar Workbook – Fundo azul claro, importação de dados

Já se perguntou **how to create workbook** em C# que pareça um pouco mais bonito logo de cara? Talvez você tenha extraído um `DataTable` de um banco de dados e esteja cansado das células sem graça, padrão‑brancas. Neste tutorial, vamos percorrer a criação de um novo workbook, adicionar um fundo azul‑claro a uma coluna e importar dados com cabeçalhos — tudo usando o estilo padrão que o Excel fornece.

Também vamos incluir alguns cenários “what‑if”, como lidar com valores nulos ou personalizar mais de uma coluna. Ao final, você terá um arquivo Excel totalmente estilizado que pode enviar aos stakeholders sem nenhum pós‑processamento.

## Pré-requisitos

* **.NET 6+** (o código funciona também no .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – a biblioteca que fornece as chamadas `Workbook`, `Style` e `ImportDataTable`. Instale-a via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Uma fonte `DataTable` – vamos criar uma fictícia no exemplo, mas você pode substituí‑la por qualquer consulta ADO.NET.

Tem tudo isso? Ótimo, vamos começar.

## Etapa 1: Inicializar um novo Workbook (Palavra‑chave principal)

A primeira coisa que você precisa fazer é **how to create workbook** – literalmente. A classe `Workbook` representa todo o arquivo Excel, e seu construtor fornece uma tela limpa.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Por que isso importa:** Começar com um `Workbook` novo garante que você controle cada estilo desde o início. Se você abrir um arquivo existente, herdará os estilos que o autor original deixou, o que pode levar a formatação inconsistente.

## Etapa 2: Preparar o DataTable que será importado

Para fins de ilustração, vamos criar um `DataTable` simples. Em cenários reais, você provavelmente chamaria uma stored procedure ou um método de ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Dica:** Se precisar preservar a ordem das colunas exatamente como aparece no banco de dados, defina o parâmetro `importColumnNames` do `ImportDataTable` como `true`. Isso indica ao Aspose.Cells que escreva os cabeçalhos das colunas para você.

## Etapa 3: Definir estilos de coluna – Padrão + fundo azul‑claro

Agora respondemos à parte **add light blue background** do quebra‑cabeça. O Aspose.Cells permite que você passe um array de objetos `Style` que correspondem a cada coluna que você importa. A primeira entrada é o estilo para a coluna 0, a segunda para a coluna 1, e assim por diante. Se você tiver menos estilos que colunas, as colunas restantes usarão o estilo padrão.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Por que apenas dois estilos?** No nosso exemplo temos quatro colunas, mas queremos que apenas a segunda coluna (Name) se destaque. O comprimento do array não precisa corresponder ao número de colunas; quaisquer entradas ausentes herdarão automaticamente o estilo padrão do workbook.

## Etapa 4: Importar o DataTable com cabeçalhos e estilos

É aqui que juntamos **excel import datatable c#** e **import data with headers**. O método `ImportDataTable` faz o trabalho pesado: ele grava os nomes das colunas, linhas e aplica o array de estilos que acabamos de criar.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Resultado esperado

Após executar o programa, o `workbook` conterá uma única planilha que se parece com isto:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* A coluna **Name** apresenta um fundo azul‑claro, comprovando que o array de estilos funciona.
* Os cabeçalhos das colunas são gerados automaticamente porque passamos `true` para `importColumnNames`.
* Valores nulos aparecem como células vazias, que é o comportamento padrão do Aspose.Cells.

## Etapa 5: Salvar o Workbook (Opcional, mas útil)

Provavelmente você desejará gravar o arquivo no disco ou enviá‑lo como stream para um cliente web. Salvar é simples:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Dica de especialista:** Se você estiver direcionando versões mais antigas do Excel, altere `SaveFormat.Xlsx` para `SaveFormat.Xls`. A API cuida da conversão para você.

## Casos de borda & variações

### Múltiplas colunas estilizadas

Se precisar de mais de uma coluna estilizada, basta expandir o array `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Agora tanto **Name** quanto **Salary** ficarão azul‑claro.

### Formatação condicional em vez de estilos fixos

Às vezes você quer que uma coluna fique vermelha quando um valor ultrapassa um limite. É aí que **use default style excel** encontra a formatação condicional:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importando sem cabeçalhos

Se o seu sistema downstream já fornece seus próprios cabeçalhos, basta passar `false` para o argumento `importColumnNames`. Os dados começarão em `A1` e você pode escrever cabeçalhos personalizados depois.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}