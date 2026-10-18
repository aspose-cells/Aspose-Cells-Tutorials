---
category: general
date: 2026-10-10
description: Crie uma pasta de trabalho do Excel em C# e use a função WRAPCOLS para
  dividir os dados de um array em colunas. Siga um guia completo passo a passo com
  código executável.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: pt
lastmod: 2026-10-10
og_description: Crie uma planilha Excel em C# e aplique a função WRAPCOLS para dividir
  dados de array em colunas. Este guia mostra o código completo e explica cada passo.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Criar pasta de trabalho Excel e dividir dados com WRAPCOLS em C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar uma pasta de trabalho do Excel e dividir dados com WRAPCOLS em C#
url: /pt/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel e dividir dados com WRAPCOLS em C#

Se você precisa **criar uma pasta de trabalho Excel** programaticamente, este guia mostra exatamente como fazer isso e como **dividir dados de array** entre colunas usando a função `WRAPCOLS`. Você obterá um exemplo completo e executável que produz um arquivo `.xlsx` com os dados distribuídos em três colunas.

O tutorial cobre tudo o que você precisa: pacotes NuGet necessários, cada linha de código, por que a fórmula `WRAPCOLS` funciona e como adaptar a solução para diferentes tamanhos de array ou contagens de colunas. Ao final, você será capaz de incorporar a técnica **usar a função wrapcols** em qualquer projeto C# que gera arquivos Excel.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior instalado  
* Uma IDE C# (Visual Studio, VS Code, Rider, etc.)  
* O pacote NuGet **Aspose.Cells for .NET** – a biblioteca que fornece a classe `Workbook` usada nos exemplos  

Você não precisa de uma instalação do Office; o Aspose.Cells grava o arquivo `.xlsx` diretamente.

## Etapa 1 – criar pasta de trabalho Excel

A primeira tarefa é instanciar um novo objeto workbook e obter uma referência para a primeira planilha. Esta etapa é a base para qualquer manipulação posterior.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` representa o arquivo inteiro, enquanto `Worksheet` representa uma única planilha. Ao criar a pasta de trabalho na memória, você evita I/O de disco até salvá‑la explicitamente.

## Etapa 2 – aplicar WRAPCOLS para dividir colunas de array

Agora você colocará uma fórmula na célula **A1** que usa `WRAPCOLS`. A função recebe dois argumentos: o array de origem e o número de colunas em que você deseja que o array seja distribuído.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Por que isso funciona:** `WRAPCOLS` pega o array plano `{1,2,3,4,5,6}` e preenche a planilha linha por linha, criando três colunas por linha. O primeiro argumento pode ser qualquer literal de array do Excel, um intervalo nomeado ou uma fórmula de array dinâmica. O segundo argumento (`3`) indica ao Excel quantas colunas gerar antes de passar para a próxima linha.

### Usando a função com diferentes tipos de dados

A função `WRAPCOLS` não se limita a números. Você pode dividir valores de texto, datas ou tipos mistos:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Quando o array de origem contém strings, o Excel trata automaticamente o resultado como células de texto. Essa flexibilidade permite que você **divida dados com fórmula Excel** para relatórios, painéis ou tarefas de migração de dados.

## Etapa 3 – calcular fórmulas para que a planilha seja preenchida

As fórmulas são armazenadas como strings até que você solicite que a pasta de trabalho as avalie. Chamar `CalculateFormula` força a avaliação e grava os resultados nas células.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Sem essa chamada, o arquivo salvo conteria apenas o texto da fórmula, não os valores calculados. O método funciona em toda a pasta de trabalho, de modo que você pode colocar fórmulas adicionais em outros locais e todas serão resolvidas com uma única chamada.

## Etapa 4 – salvar a pasta de trabalho para ver o resultado

Finalmente, grave a pasta de trabalho no disco. Escolha uma pasta para a qual você tenha permissão de gravação e dê ao arquivo um nome claro.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Ao abrir `output.xlsx` no Excel (ou em qualquer visualizador compatível), você verá:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Se você usou o exemplo de tipos mistos, as linhas 3‑4 conteriam o texto e os números correspondentes.

## Variações avançadas e tratamento de casos extremos

### Contagem de colunas variável em tempo de execução

Frequentemente, o número de colunas que você precisa depende da entrada do usuário. Você pode construir a string da fórmula dinamicamente:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Arrays grandes e desempenho

`WRAPCOLS` pode lidar com milhares de elementos, mas avaliar arrays extremamente grandes em uma única célula pode aumentar o tempo de cálculo. Se você notar lentidão:

* Divida o array de origem em blocos menores e escreva cada bloco em uma célula inicial separada.  
* Use `WorkbookSettings` para habilitar cálculo multi‑thread:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Tratamento de células vazias

Se o array de origem contém strings vazias (`""`) ou valores `NULL`, `WRAPCOLS` insere células em branco, preservando o layout das colunas. Esse comportamento é útil quando você precisa de colunas de espaço reservado para inserção de dados posterior.

### Usando intervalos nomeados em vez de literais

Para facilitar a manutenção, defina um intervalo nomeado que contenha os dados de origem e, em seguida, faça referência a ele:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Agora a fórmula lê os dados da própria planilha, permitindo **como usar wrapcols** em cenários de relatórios dinâmicos.

## Armadilhas comuns e dicas profissionais

* **Não omita o segundo argumento.** `WRAPCOLS(array)` sem a contagem de colunas retorna uma única coluna, o que anula o objetivo de dividir os dados.  
* **Evite misturar dimensões de array.** O array de origem deve ser unidimensional; fornecer um array bidimensional (por exemplo, `{ {1,2},{3,4} }`) gera um erro `#VALUE!`.  
* **Salve após o cálculo.** Se você chamar `wb.Save` antes de `CalculateFormula`, o arquivo conterá apenas o texto da fórmula.  
* **Verifique as permissões de arquivo.** Ao executar em ambientes restritos (por exemplo, ASP.NET), certifique‑se de que a identidade do processo possa gravar na pasta de destino.  

## Exemplo completo em funcionamento

Abaixo está o programa completo que você pode copiar, colar e executar. Ele inclui todas as importações, tratamento de erros e comentários.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Executar o programa produz `output.xlsx` com três regiões distintas demonstrando **divisão de dados com fórmula Excel** usando a função `WRAPCOLS`.

## Conclusão

Agora você sabe como **criar arquivos de pasta de trabalho Excel** em C# e como **usar a função wrapcols** para **dividir colunas de array** de forma eficiente. As etapas principais — instanciar `Workbook`, inserir a fórmula `WRAPCOLs`, calcular e salvar — formam um padrão reutilizável para qualquer tarefa de automação que requer distribuição de dados entre colunas.

A partir daqui, você pode:

* Combinar `WRAPCOLS` com outras funções de array dinâmico como `FILTER` ou `SORT`.  
* Exportar grandes conjuntos de dados de bancos de dados e deixar o Excel lidar com o layout automaticamente.  
* Construir relatórios dirigidos pelo usuário onde a contagem de colunas é selecionada via um controle de interface.

Experimente diferentes fontes de array, contagens de colunas e fórmulas adicionais para ampliar esta base. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar WRAPCOLS em C# – Criar pasta de trabalho Excel com funções de wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Criar pasta de trabalho Excel – Converter array em matriz com WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Criar pasta de trabalho Excel C# – Guia passo a passo](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}