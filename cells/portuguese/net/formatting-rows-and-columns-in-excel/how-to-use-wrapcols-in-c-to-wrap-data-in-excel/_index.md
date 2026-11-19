---
category: general
date: 2026-11-19
description: Como usar wrapcols em C# para envolver dados no Excel e calcular fórmulas
  do Excel rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: pt
lastmod: 2026-11-19
og_description: Como usar wrapcols em C# para envolver dados no Excel. Aprenda a calcular
  fórmulas do Excel e salvar a planilha programaticamente.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Como usar wrapcols em C# – envolver dados no Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Como usar wrapcols em C# para envolver dados no Excel
url: /pt/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar wrapcols em C# para envolver dados no Excel

Se você precisa **how to use wrapcols** para reorganizar uma lista vertical em várias colunas, este guia mostra os passos exatos. Você também aprenderá como **calculate Excel formulas** para que o resultado seja armazenado no arquivo que você salvar.

Trabalhar com Excel a partir de C# geralmente começa com o carregamento de uma planilha, aplicação de fórmulas e, finalmente, a persistência das alterações. Este tutorial cobre todas essas etapas enquanto mantém o código fácil de copiar‑colar para o seu próprio projeto.

## O que você vai alcançar

Ao final deste tutorial você será capaz de:

* Carregar um arquivo `.xlsx` existente do disco (**load excel workbook c#**).
* Aplicar a função `WRAPCOLS` a um intervalo, efetivamente **wrap data in Excel**.
* Forçar o mecanismo a avaliar a fórmula (**calculate Excel formulas**).
* Salvar a planilha modificada (**save Excel file c#**).

O único pré‑requisito é uma referência ao **Aspose.Cells for .NET** (ou qualquer biblioteca que suporte a função `WRAPCOLS`). O código funciona com .NET 6+ e Visual Studio 2022, mas qualquer IDE C# servirá.

## Como usar wrapcols com Aspose.Cells

A função de planilha `WRAPCOLS` recebe um intervalo unidimensional e devolve uma matriz bidimensional que preenche o número especificado de colunas. Aspose.Cells avalia a função exatamente como o Excel faz, portanto você pode usá‑la diretamente em uma fórmula de célula.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Por que cada linha importa

* **Loading the workbook** fornece um modelo de objeto ativo que espelha o arquivo Excel no disco.  
* **Assigning the formula** a `A1` indica ao Excel (ou Aspose.Cells) que o intervalo deve ser tratado como uma matriz dinâmica.  
* **`CalculateFormula()`** dispara o motor de cálculo; sem ele a fórmula permaneceria não avaliada até que o arquivo fosse aberto no Excel.  
* **Saving** grava os valores calculados de volta em um novo arquivo, tornando os dados envoltos visíveis para quem abrir a planilha.

## Calcular fórmulas do Excel programaticamente

Chamar `Workbook.CalculateFormula()` é a forma recomendada de **calculate Excel formulas** quando você precisa dos resultados imediatamente. O método respeita todas as funções internas, funções definidas pelo usuário e quaisquer referências externas que já estejam resolvidas.

Se você tem várias planilhas que dependem umas das outras, também pode passar um objeto `CalculationOptions` para controlar limites de iteração ou habilitar cálculo multi‑thread:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Esta etapa extra é opcional para o exemplo simples de `WRAPCOLS`, mas torna‑se essencial em pastas de trabalho maiores onde o desempenho importa.

## Salvar arquivo Excel C# após envolver dados

A chamada a `Workbook.Save()` grava toda a pasta de trabalho, incluindo a matriz recém‑materializada produzida por `WRAPCOLS`. Você pode escolher qualquer um dos formatos suportados (`.xlsx`, `.xls`, `.csv`, etc.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

A etapa **save Excel file c#** garante que os dados envolvidos persistam, de modo que na próxima vez que alguém abrir o arquivo verá uma tabela estática em vez de uma fórmula.

## Carregar pasta de trabalho Excel C# e preparar a planilha

Se o seu arquivo de origem ainda não contém os dados que você deseja envolver, pode criá‑los na hora:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Este trecho demonstra **load excel workbook c#** no sentido de que você pode começar a partir de uma planilha em branco, preenchê‑la e então aplicar `WRAPCOLS`. O mesmo padrão funciona quando você precisa importar dados de um banco de dados ou de um arquivo CSV antes de envolver.

## Dica profissional: verificar o resultado sem abrir o Excel

Após salvar, você pode ler programaticamente a área envolvida para confirmar que a operação foi bem‑sucedida:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

O console deve exibir a lista original dividida em três colunas, confirmando que **wrap data in excel** funcionou como esperado.

## Perguntas frequentes e casos de borda

| Question | Answer |
|----------|--------|
| *What if the source range has more rows than `WRAPCOLS` can fill?* | A função continua a criar novas linhas conforme necessário. O número de colunas permanece fixo. |
| *Can I wrap into a different number of columns?* | Sim—altere o segundo argumento, por exemplo, `=WRAPCOLS(A2:A10,5)` para cinco colunas. |
| *Do I need to clear the formula after calculation?* | Não, se você chamar `CalculateFormula()`. A função devolve uma matriz estática, mas a fórmula permanece na célula. Se quiser apenas o valor, copie o intervalo e cole‑valores sobre ele. |
| *Will this work with older `.xls` files?* | `WRAPCOLS` é uma função de matriz dinâmica introduzida no Excel 365. Formatos de arquivo mais antigos que não suportam matrizes dinâmicas armazenarão a fórmula, mas podem não exibir o resultado envolto corretamente. Use `.xlsx` para comportamento confiável. |

## Conclusão

Agora você sabe **how to use wrapcols** em C# para **wrap data in Excel**, como **calculate Excel formulas** on the fly e como **save Excel file C#** após a transformação. O exemplo completo demonstra o carregamento de uma pasta de trabalho, a aplicação da função `WRAPCOLS`, a força do cálculo e a persistência do resultado.

### Próximos passos

* Explore outras funções de matriz dinâmica como `UNWRAPCOLS` ou `SEQUENCE`.  
* Use **Aspose.Cells** para importar dados de um banco de dados e então envolvê‑los automaticamente.  
* Combine `WRAPCOLS` com formatação condicional para destacar linhas específicas após o envolvimento.

Sinta‑se à vontade para experimentar diferentes intervalos de origem, contagens de colunas e formatos de saída. Se encontrar algum problema, revisitar a etapa **calculate Excel formulas** ou verificar as configurações de cálculo da planilha geralmente resolve a situação.

--- 

*Image: ![Screenshot of wrapped data in Excel](/images/wrapcols-example.png){.align-center alt="Captura de tela mostrando dados envolvidos em uma planilha Excel após aplicar WRAPCOLS"}*


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to use WRAPCOLS in C# for Excel arrays and workbook saving](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [How to create Excel workbook and split data with WRAPCOLS in C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}