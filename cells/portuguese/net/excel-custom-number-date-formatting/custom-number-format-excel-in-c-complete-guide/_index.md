---
category: general
date: 2026-03-22
description: Tutorial de formato de número personalizado no Excel mostrando como importar
  uma datatable para o Excel, definir a cor de fundo da coluna, formatar a coluna
  como moeda e salvar a pasta de trabalho como xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: pt
og_description: Tutorial de formato de número personalizado no Excel que orienta você
  a importar uma DataTable, definir a cor de fundo da coluna, formatar uma coluna
  como moeda e salvar a pasta de trabalho como xlsx.
og_title: Formato Personalizado de Números no Excel em C# – Guia Passo a Passo
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Formato Personalizado de Números no Excel em C# – Guia Completo
url: /pt/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato de Número Personalizado no Excel – Tutorial Full‑Stack C#

Já se perguntou como aplicar um estilo **custom number format excel** diretamente do C#? Talvez você tenha tentado despejar um DataTable em uma planilha e só viu números simples, sem cores e sem formatação de moeda. Esse é um ponto de dor comum—especialmente quando você precisa de um relatório bem apresentado para as partes interessadas.

Neste guia, resolveremos esse problema juntos: você aprenderá como **import datatable to excel**, **set column background color**, **format column as currency** e, finalmente, **save workbook as xlsx** com um formato de número personalizado que faz seus valores se destacarem. Sem referências vagas, apenas uma solução completa e executável que você pode copiar‑colar em seu projeto.

---

## O que você vai construir

Ao final deste tutorial, você terá um aplicativo console C# autônomo que:

1. Recupera um `DataTable` (você pode substituir o stub pela sua própria consulta).  
2. Cria uma nova planilha Excel usando Aspose.Cells (ou qualquer biblioteca compatível).  
3. Aplica uma fonte azul e em negrito na primeira coluna, um fundo amarelo‑claro na segunda e um formato de moeda (`$#,##0.00`) na terceira.  
4. Salva o arquivo como `DataTableWithStyleArray.xlsx` em uma pasta de sua escolha.

Você verá exatamente como cada linha contribui para o arquivo Excel final, e discutiremos por que essas escolhas são importantes para a manutenção e desempenho.

---

## Pré-requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+).  
- Aspose.Cells para .NET (versão de avaliação gratuita ou licenciada). Instale via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Familiaridade básica com `DataTable` e aplicativos console C#.

---

## Etapa 1: Recuperar os Dados de Origem como um DataTable

Primeiro, precisamos de alguns dados para exportar. Em um cenário real, você provavelmente chamaria um repositório ou executaria uma consulta SQL. Para ilustração, criaremos uma tabela simples na memória.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Por que isso importa:** Usar um `DataTable` fornece uma fonte tabular, consciente de esquema, que mapeia perfeitamente para linhas e colunas do Excel. Também permite reutilizar a mesma lógica de exportação para qualquer conjunto de dados sem reescrever código.

---

## Etapa 2: Criar uma Nova Pasta de Trabalho e Obter a Primeira Planilha

Agora criamos uma pasta de trabalho Excel. A classe `Workbook` representa o arquivo inteiro; seu `Worksheets[0]` é a planilha padrão onde inseriremos nossos dados.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Dica profissional:** Se precisar de várias planilhas, basta chamar `workbook.Worksheets.Add("SheetName")` e repetir as etapas de estilo para cada uma.

---

## Etapa 3: Definir Estilos de Coluna – Fonte, Fundo e Formato de Número

A estilização no Aspose.Cells é feita via objetos `Style`. Criaremos um array onde cada elemento corresponde a uma coluna no DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Por que um array de estilos?** Passar um array para `ImportDataTable` permite aplicar um estilo distinto a cada coluna em uma única chamada, o que é conciso e eficiente. Também garante que a formatação permaneça sincronizada com a ordem dos dados.

---

## Etapa 4: Importar o DataTable Aplicando os Estilos

Aqui está o coração da operação: enviamos o `DataTable` para a planilha, instruímos o Aspose a incluir a linha de cabeçalho e entregamos nosso array `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **O que acontece nos bastidores?** Aspose itera por cada coluna, escreve o cabeçalho e depois escreve cada valor de linha. Enquanto faz isso, aplica o `Style` correspondente do array, de modo que você termina com um cabeçalho azul para “Product”, um “Quantity” sombreado em amarelo e uma coluna “Revenue” bem formatada.

---

## Etapa 5: Salvar a Pasta de Trabalho como um Arquivo XLSX

Finalmente, persistimos a pasta de trabalho no disco. O método `Save` escolhe automaticamente o formato XLSX com base na extensão do arquivo.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Dica:** Se precisar transmitir o arquivo (por exemplo, para uma API web), use `workbook.Save(stream, SaveFormat.Xlsx)` em vez de um caminho de arquivo.

---

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode colar em um novo projeto console. Ele compila e executa como está, produzindo um arquivo Excel estilizado.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Resultado Esperado

Ao abrir `DataTableWithStyleArray.xlsx` você verá:

| **Produto** (azul, negrito) | **Quantidade** (amarelo‑claro) | **Receita** (moeda) |
|-----------------------------|--------------------------------|---------------------|
| Widget A                    | 120                            | $3,450.75           |
| Widget B                    | 85                             | $2,190.00           |
| Widget C                    | 60                             | $1,580.40           |

O **custom number format excel** que você especificou (`$#,##0.00`) garante que cada célula de receita exiba o símbolo de dólar, separador de milhar e duas casas decimais—exatamente o que as equipes financeiras esperam.

---

## Perguntas Frequentes & Casos de Borda

### Posso usar isso com uma biblioteca Excel diferente?

Absolutamente. O conceito—criar um estilo por coluna e aplicá‑lo durante a importação—é transferível para EPPlus, ClosedXML ou NPOI. As chamadas de API diferem, mas o padrão permanece o mesmo.

### E se meu DataTable tiver mais colunas do que estilos?

O Aspose aplicará o estilo padrão a qualquer coluna sem uma entrada correspondente no array `columnStyles`. Para evitar surpresas, dimensione o array para `dataTable.Columns.Count` ou gere estilos dinamicamente em um loop.

### Como definir um formato de número personalizado para datas?

Basta definir `style.Custom = "dd‑mm‑yyyy"` (ou qualquer string de formato Excel válida). A mesma abordagem baseada em array funciona para datas, porcentagens ou notação científica.

### Existe uma maneira de ajustar automaticamente a largura das colunas após a importação?

Sim—chame `worksheet.AutoFitColumns();` após a importação. Ele executa um cálculo rápido de largura com base no conteúdo das células.

### E quanto a conjuntos de dados grandes (mais de 100 mil linhas)?

`ImportDataTable` é otimizado para operações em lote, mas você pode atingir limites de memória. Nesse caso, considere transmitir linhas manualmente com `Cells[i, j].PutValue(...)` e reutilizar um único objeto `Style` para reduzir a sobrecarga.

---

## Dicas Profissionais & Armadilhas Comuns

- **Evite codificar caminhos** diretamente no código de produção; use `Environment.GetFolderPath` ou configurações de arquivo.  
- **Libere o workbook** se estiver em um serviço de longa execução—envolva‑o em um bloco `using` para liberar recursos nativos.  
- **Fique atento aos separadores específicos de cultura**. O formato personalizado `$#,##0.00` força um ponto como separador decimal independentemente da localidade do SO, o que geralmente é o desejado para relatórios financeiros.  
- **Lembre-se de referenciar System.Drawing** (ou `System.Drawing.Common` no .NET Core) para as structs de cor usadas na estilização.  
- **Teste a saída em diferentes versões do Excel**; versões mais antigas podem interpretar alguns formatos personalizados de forma ligeiramente diferente.

---

## Conclusão

Cobrimos tudo o que você precisa para **custom number format excel** arquivos a partir do C#: extrair dados de um `DataTable`, **import datatable to excel**, aplicar um **set column background color**, usar **format column as currency** e, finalmente, **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}