---
category: general
date: 2026-10-04
description: Aprenda como copiar uma tabela dinâmica de uma pasta de trabalho para
  outra usando C#. Este guia também aborda como copiar linhas, duplicar a tabela dinâmica
  e copiar intervalos do Excel de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: pt
lastmod: 2026-10-04
og_description: Copie tabela dinâmica no Excel usando C#. Siga este tutorial completo
  para duplicar tabelas dinâmicas, copiar linhas e copiar intervalo do Excel com Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Copiar tabela dinâmica no Excel com C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como copiar tabela dinâmica no Excel com C# e Aspose.Cells
url: /pt/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabela dinâmica no Excel com C# e Aspose.Cells

Se você precisar **copy pivot table** de uma pasta de trabalho para outra, este tutorial mostra uma solução completa e executável. Você verá exatamente como carregar um arquivo de origem, definir o intervalo que contém a tabela dinâmica, copiar as linhas (incluindo a definição da tabela dinâmica) e salvar o resultado. Seja automatizando um pipeline de relatórios ou construindo uma ferramenta de migração, os passos abaixo permitem duplicar uma tabela dinâmica com apenas algumas linhas de C#.

Copiar uma tabela dinâmica é mais do que copiar valores de células; o cache subjacente e as configurações de campo devem ser transferidos juntos. O exemplo usa a biblioteca **Aspose.Cells** porque ela lida com metadados da tabela dinâmica automaticamente, de modo que você não precise reconstruir o cache manualmente. Ao final deste guia, você será capaz de **how to copy pivot**, **copy excel range**, e **how to copy rows** com segurança.

## Pré-requisitos

- .NET 6.0 ou posterior instalado (o código também funciona com .NET Framework 4.7+).
- Uma licença válida do Aspose.Cells for .NET ou uma licença de avaliação temporária.
- Dois arquivos Excel: `Source.xlsx` contendo a tabela dinâmica que você deseja duplicar, e uma pasta vazia onde `CopyWithPivot.xlsx` será gravado.
- Visual Studio 2022 (ou qualquer IDE que suporte C#).

## Etapa 1: Configurar o projeto e adicionar Aspose.Cells

Crie um novo projeto de console e adicione o pacote NuGet Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

O pacote fornece as classes `Workbook`, `Worksheet` e `CellArea` usadas no código abaixo.

## Etapa 2: Carregar a pasta de trabalho de origem que contém a tabela dinâmica

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Por que isso importa:** Carregar a pasta de trabalho cria uma representação em memória de todas as planilhas, incluindo quaisquer caches de tabela dinâmica ocultos. Sem carregar o arquivo, você não pode referenciar o intervalo da tabela dinâmica.

## Etapa 3: Definir a área de células que cobre a tabela dinâmica

Você deve informar ao Aspose.Cells quais linhas e colunas pertencem à tabela dinâmica. A estrutura `CellArea` permite especificar um bloco retangular.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Dica:** Se você não tem certeza do tamanho exato, abra o arquivo de origem no Excel, selecione a tabela dinâmica e observe o intervalo exibido na Caixa de Nome (por exemplo, `A1:K31`). Converta as coordenadas do Excel para índices baseados em zero para o código.

## Etapa 4: Criar uma nova pasta de trabalho de destino e obter sua primeira planilha

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Por que esta etapa é necessária:** A pasta de trabalho de destino deve existir antes que você possa copiar linhas. O Aspose.Cells cria automaticamente uma planilha padrão, que usaremos como destino.

## Etapa 5: Copiar as linhas (incluindo a tabela dinâmica) da origem para o destino

O método `CopyRows` copia tanto os valores das células quanto o cache subjacente da tabela dinâmica.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Como isso funciona:**  
> - `CopyRows` recebe a planilha de origem, a linha inicial e a quantidade de linhas a copiar.  
> - Também recebe a planilha de destino e a linha onde a cópia deve começar.  
> - Como o intervalo de origem inclui a tabela dinâmica, o método transfere o cache da tabela dinâmica, a lista de campos e o layout intactos. Este é o núcleo de **how to copy pivot** sem perder funcionalidade.

### Caso de borda: copiando uma tabela dinâmica que abrange várias planilhas

Se os dados de origem da tabela dinâmica estiverem em uma planilha diferente da própria tabela dinâmica, o cache ainda acompanha a cópia porque o Aspose.Cells armazena o cache na pasta de trabalho, não na planilha. No entanto, você deve garantir que a pasta de trabalho de destino contenha o mesmo intervalo de dados de origem; caso contrário, a tabela dinâmica exibirá erros `#REF!`. Nesses casos, copie primeiro o intervalo de dados de origem e depois as linhas da tabela dinâmica.

## Etapa 6: Salvar a pasta de trabalho que agora contém a tabela dinâmica copiada

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Executar o programa gera `CopyWithPivot.xlsx` com uma réplica exata da tabela dinâmica original, incluindo todos os slicers, filtros e campos calculados.

### Saída esperada

Quando você abrir `CopyWithPivot.xlsx`:

- A tabela dinâmica aparece na mesma posição (por exemplo, A1:K31) que em `Source.xlsx`.
- Todos os rótulos de linhas e colunas, totais e formatação são preservados.
- Atualizar a tabela dinâmica mostra os mesmos dados da origem, confirmando que o cache foi copiado corretamente.

## Como copiar linhas sem uma tabela dinâmica (copy excel range)

Se você precisar apenas **copy excel range** sem nenhum dado de tabela dinâmica, pode usar o mesmo método `CopyRows` mas apontar para um intervalo que não contenha uma tabela dinâmica. Por exemplo:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Isso demonstra **how to copy rows** para dados genéricos, reforçando a versatilidade da mesma API.

## Duplicar tabela dinâmica na mesma pasta de trabalho (abordagem alternativa)

Às vezes você deseja **duplicate pivot table** dentro da mesma pasta de trabalho ao invés de criar um novo arquivo. Você pode conseguir isso copiando linhas para um local diferente:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Após salvar, a pasta de trabalho conterá duas tabelas dinâmicas idênticas — útil para comparação lado a lado ou criação de cópias de backup.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Solução |
|-----------|------------------|---------|
| Tabela dinâmica mostra `#REF!` após cópia | Intervalo de dados de origem não presente na pasta de trabalho de destino | Copie primeiro o intervalo de dados de origem, ou use `CopyRows` na planilha de dados de origem antes de copiar a tabela dinâmica |
| Formatação perdida | Apenas valores foram copiados (por exemplo, usando `Copy` ao invés de `CopyRows`) | Sempre use `CopyRows`, que preserva estilo, formatação e metadados da tabela dinâmica |
| Deslocamento de linha inesperado | A linha inicial de destino não corresponde à linha inicial da origem | Verifique se a linha inicial de `destWorksheet.Cells` corresponde ao local desejado |
| Pastas de trabalho grandes causam pressão de memória | `CopyRows` carrega planilhas inteiras na memória | Processar a cópia em blocos ou usar APIs de streaming se trabalhar com mais de 100.000 linhas |

## Exemplo completo e executável

Abaixo está o programa completo que você pode colar em `Program.cs` e executar imediatamente (substitua `YOUR_DIRECTORY` por um caminho real em sua máquina).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Execute o programa com `dotnet run`. Após a execução, abra `CopyWithPivot.xlsx` para verificar se a tabela dinâmica aparece exatamente como no arquivo de origem.

## Conclusão

Agora você sabe como **copy pivot table** de uma pasta de trabalho Excel para outra usando C# e Aspose.Cells. O guia cobriu o fluxo de trabalho completo — desde o carregamento do arquivo de origem, definição da área de células da tabela dinâmica, cópia de linhas e salvamento da pasta de trabalho de destino. Você também aprendeu **how to copy rows**, **copy excel range**, e **duplicate pivot table** dentro do mesmo arquivo, além de armadilhas comuns e dicas de boas práticas.

Pronto para o próximo passo? Tente adicionar código para atualizar programaticamente a tabela dinâmica copiada, ou explore exportar a tabela dinâmica para PDF com Aspose.Cells. Experimente diferentes intervalos de origem, e você dominará rapidamente a automação do Excel em .NET.

---

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Copiar Tabela Dinâmica em C# – Guia Completo Passo a Passo](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Criar Nova Pasta de Trabalho Excel – Copiar & Duplicar Tabela Dinâmica](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copiar linhas excel – Preservar Tabela Dinâmica ao Duplicar Linhas](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}