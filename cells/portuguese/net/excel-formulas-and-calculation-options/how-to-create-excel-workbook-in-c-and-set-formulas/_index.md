---
category: general
date: 2026-10-01
description: Crie uma planilha Excel em C# rapidamente, aprenda a definir uma fórmula,
  calcular a cotangente e usar a função PI no Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: pt
lastmod: 2026-10-01
og_description: Crie uma pasta de trabalho Excel em C# com Aspose.Cells. Aprenda como
  definir uma fórmula, usar a função PI e calcular a cotangente em apenas alguns passos.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Criar pasta de trabalho Excel em C# – definir fórmulas e calcular cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar uma pasta de trabalho Excel em C# e definir fórmulas
url: /pt/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel em C# e definir fórmulas

Se você precisa **criar uma pasta de trabalho Excel C#** que escreva uma fórmula em uma célula, este guia mostra exatamente como fazer. Você verá como definir uma fórmula em uma planilha, usar a função embutida PI e calcular a cotangente de um ângulo — tudo com Aspose.Cells.

O tutorial cobre tudo, desde a inicialização da pasta de trabalho até a obtenção do resultado calculado, para que você possa copiar o exemplo completo para o seu próprio projeto sem faltar nada.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado  
* Uma licença válida do Aspose.Cells (ou uma chave de avaliação temporária)  
* Visual Studio 2022 ou qualquer IDE C# de sua preferência  

Nenhum pacote NuGet adicional é necessário além do `Aspose.Cells`.

## Criar pasta de trabalho Excel em C#

O primeiro passo é instanciar um novo objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória e fornece acesso às suas planilhas.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Criar a pasta de trabalho dessa forma garante que o arquivo esteja pronto para qualquer manipulação posterior, como adicionar dados, formatar células ou escrever fórmulas.

## Definir fórmula em célula usando a função PI

Agora você vai **escrever fórmula na célula** A1. A fórmula usa a função `PI()` para fornecer a constante π e a função `COT` para calcular sua cotangente.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Por que isso importa*: `PI()` é uma função interna do Excel que devolve o valor de π. Dividindo‑a por 4 você obtém 45°, e `COT` devolve a cotangente desse ângulo. Isso demonstra **como usar a função pi** dentro de uma fórmula Excel a partir de C#.

## Como calcular cot com Aspose.Cells

Se você está se perguntando **como calcular cot** sem converter manualmente os ângulos, a função `COT` faz o trabalho pesado. Ela aceita um ângulo em radianos, então você pode combiná‑la com `PI()` para ângulos comuns.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Executar o programa exibe:

```
Cotangent of PI/4 = 1
```

Como `COT(π/4)` é igual a 1, a saída confirma que a **definição de fórmula na célula** foi feita corretamente e avaliada.

## Escrever fórmula na célula – dicas adicionais

* **Múltiplas fórmulas**: Você pode atribuir uma fórmula a qualquer célula usando a mesma propriedade `Formula`, por exemplo, `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **Configurações internacionais**: Aspose.Cells respeita o locale da pasta de trabalho, portanto os nomes das funções permanecem em inglês (`PI`, `COT`) independentemente das configurações regionais do usuário.
* **Desempenho**: Se precisar definir milhares de fórmulas, agrupe‑as e chame `workbook.Calculate()` uma única vez ao final para evitar recalculações repetidas.

## Exemplo completo executável

Abaixo está o programa completo que você pode copiar‑colar em um projeto de console. Ele inclui todas as instruções `using` necessárias e demonstra o fluxo completo, da criação da pasta de trabalho à exibição do resultado.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Saída esperada** ao executar o programa:

```
Cotangent of PI/4 = 1
```

O arquivo gerado `CotExample.xlsx` contém a fórmula na célula A1, permitindo que você o abra no Excel e veja o mesmo resultado.

## Conclusão

Agora você sabe como **criar uma pasta de trabalho Excel C#** que escreve uma fórmula, usa a função `PI` e **calcula cot** com Aspose.Cells. O exemplo cobre todo o ciclo de vida: criação da pasta de trabalho, **definir fórmula na célula**, recálculo e obtenção do resultado.

Próximos passos que você pode explorar:

* Aplicar **escrever fórmula na célula** para cálculos mais complexos, como modelos financeiros.  
* Usar **definir fórmula na célula** junto com formatação condicional para destacar resultados.  
* Combinar **como usar a função pi** com gráficos trigonométricos para relatórios científicos.

Sinta‑se à vontade para experimentar diferentes ângulos, funções e disposições de planilhas. Dominar o manuseio de fórmulas em C# abre a porta para pipelines de relatórios Excel totalmente automatizados. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais, com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}