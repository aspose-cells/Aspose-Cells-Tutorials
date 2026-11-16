---
category: general
date: 2026-11-16
description: Aprenda como expandir arrays no Excel usando Aspose.Cells, funções de
  arrays dinâmicos e um redutor lambda, e depois escreva o arquivo Excel a partir
  do C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: pt
lastmod: 2026-11-16
og_description: Como expandir um array no Excel usando Aspose.Cells, funções de array
  dinâmicas e um redutor lambda. Siga o exemplo completo em C# para escrever o arquivo
  Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Como expandir array no Excel com Aspose.Cells – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como expandir uma matriz no Excel com Aspose.Cells
url: /pt/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como expandir array no Excel com Aspose.Cells

Se você precisa **como expandir array** em uma planilha Excel a partir de C#, este tutorial mostra os passos exatos. Você criará um workbook Excel, usará funções de array dinâmico como `EXPAND` e `REDUCE`, aplicará um acumulador **lambda**, e finalmente **escrever arquivo Excel** para o disco. A abordagem funciona com Aspose.Cells 23.10 ou posterior e não requer instalação manual do Excel.

Ao final deste guia você terá um `ExpandReduceDemo.xlsx` totalmente funcional que demonstra o poder das fórmulas de array dinâmico em um contexto programático.

## O que você precisará

- .NET 6.0 (ou qualquer versão .NET suportada pelo Aspose.Cells)
- Pacote Aspose.Cells para .NET (`dotnet add package Aspose.Cells`)
- Um editor de código ou IDE (Visual Studio, VS Code, Rider, etc.)

Nenhum interop COM adicional ou instalação do Office é necessário porque o Aspose.Cells lida com o formato de arquivo internamente.

## Etapa 1: Criar workbook Excel

A primeira tarefa é **criar workbook Excel** na memória. O Aspose.Cells fornece a classe `Workbook`, que representa um arquivo XLSX completo.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Por que isso importa:** Instanciar um `Workbook` fornece uma tela limpa. A planilha padrão já está preparada, então você não precisa adicionar uma manualmente, a menos que queira várias planilhas.

## Etapa 2: Inserir uma constante de array vertical

O mecanismo de array dinâmico do Excel pode trabalhar com constantes de array literais. Vamos colocar o array vertical `{1;2;3;4;5}` na célula **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Dica:** O ponto e vírgula (`;`) separa linhas na constante, enquanto a vírgula (`,`) separaria colunas. Isso reflete a própria sintaxe do Excel.

## Etapa 3: Expandir o array em uma matriz

Agora respondemos à questão central – **como expandir array** – usando a função `EXPAND`. A fórmula expande o array de coluna única em uma matriz de 5 linhas × 2 colunas, começando em **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Por que EXPAND?** `EXPAND(source, rows, cols)` força o intervalo de origem a ocupar o tamanho especificado, preenchendo com vazios se necessário. É a maneira mais legível de gerar uma matriz maior a partir de um único array.

## Etapa 4: Reduzir a matriz com um acumulador lambda

A função `REDUCE` itera sobre um intervalo e agrega valores usando uma expressão **lambda**. Aqui somamos cada valor de coluna em uma única coluna, colocando o resultado em **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Como usar lambda:** O `LAMBDA(acc, val, acc+val)` recebe o acumulador atual (`acc`) e o próximo valor da célula (`val`). Ele retorna o novo acumulador, efetivamente realizando um total acumulado. Isso demonstra **como usar lambda** em fórmulas do Excel a partir do código.

## Etapa 5: Calcular fórmulas para que os resultados apareçam

O Aspose.Cells não avalia automaticamente as fórmulas quando você as define. Chamar `CalculateFormula` força o motor a calcular todas as fórmulas na pasta de trabalho.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Observação:** Se você abrir o arquivo gerado no Excel, os valores já estarão visíveis porque foram pré‑calculados.

## Etapa 6: Escrever arquivo Excel no disco

Finalmente, **escrever arquivo Excel** usando o método `Save`. Escolha uma pasta na qual você tenha permissão de escrita.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Resultado esperado

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Coluna B** e **C** contêm a matriz 5 × 2 produzida por `EXPAND`.
- **Célula D1** mostra `15`, a soma de todos os números, calculada pela fórmula `REDUCE` + **lambda**.

## Perguntas comuns e casos de borda

- **Posso expandir para mais colunas do que a origem fornece?**  
  Sim. `EXPAND` preenche colunas ausentes com células vazias. O mesmo vale para linhas.

- **E se o array de origem for horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` tratará a origem como uma única linha; ainda assim você pode especificar linhas e colunas para remodelá‑lo.

- **O `REDUCE` funciona com dados não numéricos?**  
  O lambda deve retornar um valor compatível com o tipo do acumulador. Para concatenação de texto, você poderia usar `LAMBDA(acc, val, acc & val)`.

- **Preciso chamar `CalculateFormula` a cada alteração?**  
  Apenas quando precisar dos valores calculados antes de salvar. O Excel recalculará ao abrir se você pular essa chamada.

## Dicas profissionais

- **Desempenho:** Para pastas de trabalho grandes, chame `workbook.CalculateFormula` uma única vez após todas as fórmulas serem definidas, em vez de após cada célula.
- **Segurança de versão:** `EXPAND` e `REDUCE` estão disponíveis no Excel 365 e posteriores. O Aspose.Cells os implementa independentemente da versão alvo do Excel porque o motor de cálculo é interno.
- **Depuração de fórmulas:** Use `sheet.Cells["B1"].Formula` para ler a string exata que você definiu; isso ajuda ao construir fórmulas dinamicamente.

## Conclusão

Agora você sabe **como expandir array** no Excel usando Aspose.Cells, aproveitar **funções de array dinâmico**, aplicar um **lambda** com `REDUCE` e **escrever arquivo Excel** a partir de C#. Este exemplo de ponta a ponta pode ser adaptado para transformações de dados mais complexas, como transposição de matriz, totais cumulativos ou agregações personalizadas.

---

*Próximos passos:*  
- Explore outras funções dinâmicas como `FILTER`, `SORT` e `UNIQUE`.  
- Combine múltiplas expressões `LAMBDA` para criar funções definidas pelo usuário reutilizáveis.  
- Integre a geração da pasta de trabalho em APIs ASP.NET Core para criação de relatórios sob demanda.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar workbook Excel C# com uma fórmula de array dinâmico](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Como expandir array no Excel e preencher um modelo](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Como Expandir Array em C# com Aspose.Cells – Guia passo a passo](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}