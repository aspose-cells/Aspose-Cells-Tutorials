---
category: general
date: 2026-10-01
description: Cores alternadas de colunas no Excel usando C# – aprenda a criar um arquivo
  Excel a partir de um DataTable, definir a cor de fundo das células em C# e importar
  um DataTable para o Excel com colunas estilizadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: pt
lastmod: 2026-10-01
og_description: Cores alternadas de colunas no Excel facilitadas. Siga este guia para
  criar um arquivo Excel a partir de um DataTable, definir a cor de fundo das células
  em C# e importar o DataTable para o Excel com colunas estilizadas.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Adicionar cores alternadas nas colunas do Excel com C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Como adicionar cores alternadas nas colunas do Excel usando C#
url: /pt/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar cores alternadas nas colunas no Excel usando C#

Se você precisa de **alternating column colors excel** em um relatório gerado a partir da sua aplicação, este guia mostra uma solução completa. Você verá como criar um arquivo Excel a partir de um `DataTable`, definir a cor de fundo da célula C# style e importar datatable to excel aplicando um estilo distinto a cada coluna.

O tutorial cobre tudo o que você precisa: pacotes NuGet necessários, um exemplo de código completo e executável, e explicações sobre por que cada passo é importante. Ao final, você terá uma pasta de trabalho estilizada que pode ser aberta diretamente no Microsoft Excel.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 (ou posterior) SDK instalado  
* Visual Studio 2022 (ou qualquer IDE compatível com C#)  
* A biblioteca **Aspose.Cells for .NET** – instale‑a com  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells fornece as classes `Workbook`, `Worksheet`, `Style` e `BackgroundType` usadas no exemplo.

## Etapa 1: Recuperar os dados de origem como um `DataTable`

A primeira tarefa é obter os dados que você deseja exportar. Em projetos reais você pode preencher o `DataTable` a partir de uma consulta ao banco de dados, uma chamada de API ou qualquer coleção em memória.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Por que isso importa:**  
Um `DataTable` é um contêiner universal que mapeia perfeitamente para uma planilha Excel. Usar um `DataTable` permite **create excel file from datatable c#** sem escrever loops personalizados para cada coluna.

## Etapa 2: Criar uma nova pasta de trabalho e obter sua primeira planilha

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Explicação:**  
`Workbook` é o objeto raiz; `Worksheets[0]` fornece a planilha padrão onde os dados serão inseridos.

## Etapa 3: Preparar um estilo distinto para cada coluna (cores de fundo alternadas)

Para alcançar **alternating column colors excel**, geramos um `Style` para cada coluna e atribuímos uma cor de fundo clara que alterna entre duas tonalidades.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Por que usamos um loop:**  
O loop garante que **set cell background color c#** seja aplicado de forma consistente, mesmo que o número de colunas mude em tempo de execução. Isso torna a solução robusta para relatórios dinâmicos.

## Etapa 4: Importar o `DataTable` para a planilha, aplicando os estilos de coluna

Aspose.Cells pode importar um `DataTable` diretamente, e podemos passar o array de estilos para colorir cada coluna.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**O que acontece nos bastidores:**  
`ImportDataTable` grava a linha de cabeçalho e, em seguida, cada linha de dados. Como fornecemos `columnStyles`, cada célula em uma coluna recebe o estilo correspondente, proporcionando as cores alternadas desejadas.

## Etapa 5: Salvar a pasta de trabalho estilizada em um arquivo

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Ao abrir *StyledTable.xlsx* no Excel, você verá cada coluna sombreada alternadamente, facilitando a leitura da tabela.

## Exemplo completo e executável

Juntando todas as peças, aqui está um programa autocontido que você pode copiar, colar e executar.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Saída esperada

* Um arquivo chamado **StyledTable.xlsx** localizado em `C:\Temp\`.
* A planilha mostra três colunas (`Id`, `Name`, `Score`) com cores de fundo alternadas: colunas 1 e 3 em *LightYellow*, coluna 2 em *LightCyan*.
* Todas as linhas do `DataTable` aparecem abaixo da linha de cabeçalho.

## Perguntas frequentes e casos de borda

| Pergunta | Resposta |
|----------|----------|
| *Posso usar outras cores?* | Sim. Substitua `System.Drawing.Color.LightYellow` e `LightCyan` por qualquer valor `System.Drawing.Color`. |
| *E se o DataTable tiver muitas colunas?* | O loop cria automaticamente um estilo para cada coluna, de modo que o padrão escala sem alterações no código. |
| *Preciso descartar a workbook?* | Aspose.Cells implementa `IDisposable`. Se envolver o `Workbook` em um bloco `using`, os recursos são liberados prontamente. |
| *Como aplicar as mesmas cores alternadas a linhas em vez de colunas?* | Crie um `Style[]` para linhas e chame `worksheet.Cells.ImportDataTable(..., rowStyles)` – as sobrecargas do Aspose.Cells suportam ambos. |
| *Posso gravar o arquivo diretamente em um stream (por exemplo, para uma API web)?* | Sim. Use `workbook.Save(stream, SaveFormat.Xlsx);` em vez de um caminho de arquivo. |

## Dicas do campo

* **Dica profissional:** Cache os objetos de estilo se você gerar muitas planilhas em uma única execução – criar um estilo é relativamente barato, mas reutilizá‑los reduz o consumo de memória.  
* **Cuidado:** Ao usar `System.Drawing.Color` em plataformas não Windows, adicione o pacote NuGet `System.Drawing.Common` e assegure‑se de que o runtime suporte GDI+.

## Conclusão

Agora você sabe como **alternating column colors excel** criando um arquivo Excel a partir de um `DataTable` em C#, definindo cores de fundo das células com Aspose.Cells e **import datatable to excel** usando um array de estilos por coluna. Essa abordagem é rápida, mantível e funciona com qualquer tamanho de conjunto de dados.

### Próximos passos

* Explore **set cell background color c#** para formatação condicional (por exemplo, destacar pontuações baixas).  
* Combine esta técnica com **create excel file from datatable c#** para gerar relatórios com várias planilhas.  
* Investigue a API de gráficos do Aspose.Cells para adicionar resumos visuais à mesma pasta de trabalho.

Sinta‑se à vontade para adaptar as cores, o formato do arquivo ou a fonte de dados para atender às necessidades do seu projeto. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}