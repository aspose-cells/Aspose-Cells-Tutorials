---
category: general
date: 2026-11-16
description: Aprenda a usar WRAPCOLS em C# para dividir uma linha em colunas, automatizar
  uma pasta de trabalho do Excel, calcular fórmulas e salvar o arquivo Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: pt
lastmod: 2026-11-16
og_description: Como usar WRAPCOLS em C# para dividir uma linha em colunas, automatizar
  uma pasta de trabalho do Excel, executar o cálculo de fórmulas e salvar o arquivo
  Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Como usar WRAPCOLS em C# – dividir linhas, calcular fórmulas e salvar arquivos
  Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Como usar WRAPCOLS para dividir uma linha em colunas no C#
url: /pt/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS para dividir uma linha em colunas no C#

Se você precisa **como usar WRAPCOLS** em um projeto C#, este guia mostra uma solução completa e executável. Você verá como dividir uma linha em colunas, automatizar uma pasta de trabalho do Excel, disparar o cálculo de fórmulas do Excel e, finalmente, salvar o arquivo Excel C# style.

Trabalhar com Excel programaticamente costuma envolver grandes conjuntos de dados, e a função `WRAPCOLS` permite remodelar uma única linha em uma matriz sem loops manuais. As etapas abaixo cobrem tudo o que você precisa — da criação da pasta de trabalho até a saída final do arquivo — para que você possa integrar a técnica em qualquer aplicação .NET.

## O que este tutorial cobre

* Criação de uma nova pasta de trabalho e acesso à sua primeira planilha.  
* Preenchimento de uma linha com valores sequenciais (1‑20).  
* Aplicação da fórmula Excel `WRAPCOLS` para dividir a linha em blocos de 5 colunas.  
* Execução do **cálculo de fórmula do Excel** para que o resultado faça parte da planilha.  
* Uso do **save excel file c#** para gravar a pasta de trabalho no disco.  

Nenhuma configuração externa é necessária além da biblioteca Aspose.Cells para .NET (ou qualquer API compatível que suporte `WRAPCOLS`). Ao final do guia você terá um arquivo chamado `WrapColsDemo.xlsx` que contém quatro linhas de cinco colunas cada, derivadas dos dados originais de uma única linha.

## Pré‑requisitos

* .NET 6.0 ou superior (o código também funciona com .NET Core 3.1 e .NET Framework 4.7+).  
* Uma referência ao **Aspose.Cells** (disponível via NuGet: `Install-Package Aspose.Cells`).  
* Familiaridade básica com a sintaxe C# e fórmulas do Excel.  

> **Dica de especialista:** Se preferir uma alternativa gratuita, a biblioteca open‑source EPPlus também suporta fórmulas personalizadas, mas `WRAPCOLS` está incorporado apenas em bibliotecas que implementam o motor completo de cálculo do Excel, como o Aspose.Cells.

## Etapa 1: Criar uma nova pasta de trabalho e obter a primeira planilha

A primeira operação é instanciar um objeto `Workbook` e obter sua planilha padrão. Esse objeto representa todo o arquivo Excel na memória.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Criar a pasta de trabalho programaticamente é a base das tarefas de **automate excel workbook**. A referência `Worksheet` permite manipular células diretamente.

## Etapa 2: Preencher a primeira linha com valores 1‑20

Em seguida, preencha as células `A1` até `T1` com os números de 1 a 20. Um simples loop `for` grava cada valor na coluna correspondente.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Por que escrever os valores programaticamente? Isso garante que a demonstração funcione em qualquer máquina sem inserção manual de dados, o que é essencial quando você **automate excel workbook** em processos em lote.

## Etapa 3: Aplicar a função WRAPCOLS para dividir a linha em blocos de 5 colunas

Agora usamos a fórmula Excel `WRAPCOLS`. Ela recebe um intervalo de origem e a contagem de colunas, retornando uma matriz bidimensional que “envolve” os dados de origem nas colunas especificadas.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Colocar a fórmula na célula `A2` indica ao Excel que o resultado deve começar na segunda linha. O resultado será uma matriz 4 × 5 porque 20 itens divididos por 5 colunas geram quatro linhas.

### Como o WRAPCOLS funciona

* **Intervalo de origem** – `A1:T1` contém os 20 valores originais.  
* **Contagem de colunas** – `5` indica ao Excel que crie cinco colunas por linha.  
* **Resultado** – O Excel preenche as células `A2:E5` com os dados “enrolados” automaticamente.

Se precisar **split row into columns** com um tamanho de bloco diferente, basta alterar o segundo argumento. Por exemplo, `WRAPCOLS(A1:T1,4)` produziria cinco linhas de quatro colunas cada.

## Etapa 4: Calcular fórmulas para materializar o resultado do WRAPCOLS

Uma fórmula recém‑adicionada permanece não avaliada até que o motor de cálculo seja executado. Ao chamar `CalculateFormula()`, você garante que a etapa de **excel formula calculation** grave os valores reais na planilha.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Executar o cálculo é crucial quando você posteriormente **save excel file c#**, pois o arquivo salvo deve conter os valores computados, não apenas o texto da fórmula. Sem essa etapa, a pasta de trabalho resultante mostraria `#N/A` ou a fórmula bruta em vez dos números esperados.

## Etapa 5: Salvar a pasta de trabalho no disco

Por fim, persista a pasta de trabalho usando o método `Save`. Você pode especificar qualquer caminho de arquivo válido; o exemplo usa um diretório placeholder que deve ser substituído pelo seu próprio caminho.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

A chamada `Save` demonstra **save excel file c#** em sua forma mais simples. O Aspose.Cells escolhe automaticamente o formato XLSX com base na extensão do arquivo. Se precisar de um arquivo `.xls` mais antigo, altere a extensão adequadamente.

### Saída esperada

Abra `WrapColsDemo.xlsx` e você verá:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

A linha única original foi **split row into columns** em quatro linhas, cada uma contendo cinco colunas.

## Código-fonte completo

Juntando todas as etapas, obtém‑se um programa compacto e autocontido:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Copie o código para um novo projeto de console, restaure o pacote NuGet Aspose.Cells e execute. O programa cria o arquivo Excel na sua área de trabalho em segundos.

## Variações comuns e casos de borda

| Situação | Ajuste |
|-----------|------------|
| **Tamanho de bloco diferente** | Alterar `WRAPCOLS(A1:T1,5)` para `WRAPCOLS(A1:T1, n)`, onde `n` é a contagem de colunas desejada. |
| **Múltiplas linhas de origem** | Usar `WRAPCOLS(A1:A10,5)` para envolver um intervalo vertical em uma matriz de 5 colunas. |
| **Intervalo de origem dinâmico** | Construir a string de endereço em C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) antes de atribuir a fórmula. |
| **Planilhas grandes** | Chamar `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` para ignorar células que causem erros e melhorar o desempenho. |
| **Salvar como CSV** | Substituir `workbook.Save(outputPath)` por `workbook.Save(outputPath, SaveFormat.Csv)`. |

Essas variações mostram que o mesmo padrão **how to use wrapcols** pode ser adaptado para muitos cenários de remodelagem de dados.

## Dicas de solução de problemas

* **Fórmula não avaliada** – Certifique‑se de chamar `workbook.CalculateFormula()` *depois* de definir a fórmula. Pular essa etapa deixa a célula com o texto bruto `WRAPCOLS`.  
* **Acesso ao arquivo negado** – Verifique se o diretório de destino existe e se o processo tem permissão de gravação. Usar `Environment.SpecialFolder.Desktop` evita a maioria dos problemas de permissão.  
* **Número incorreto de linhas** – Revise o segundo argumento do `WRAPCOLS`. Ele define a contagem de colunas, não de linhas; as linhas são derivadas do total de células de origem dividido por essa contagem.

## Conclusão

Agora você sabe **como usar WRAPCOLS** em C# para **split row into columns**, criar **automate excel workbook** totalmente automatizado, executar **excel formula calculation** e **save excel file c#** com um código limpo e único. Essa técnica elimina operações manuais de copiar‑colar e escala sem esforço para pipelines de transformação de dados de grande volume.

### Próximos passos

* Explore outras funções de matriz dinâmica como `SEQUENCE`, `FILTER` e `UNIQUE` para enriquecer seu kit de ferramentas de automação Excel.  
* Combine `WRAPCOLS` com APIs de geração de gráficos para produzir relatórios prontos para publicação.  
* Integre o código em um serviço em segundo plano que processe uploads de CSV e gere arquivos Excel remodelados para análises posteriores.

Sinta‑se à vontade para experimentar diferentes intervalos de origem e contagens de colunas — ajuste a fórmula, reexecute o cálculo e veja a pasta de trabalho atualizar instantaneamente. Feliz codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [como usar wrapcols em C# – Guia completo com Excel WRAPROWS & Recalcular Fórmulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Como usar WRAPCOLS – Guia completo para automação Excel em C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [Como usar WRAPCOLS em C# – Transformar um Array em Matriz no Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}