---
category: general
date: 2026-07-13
description: Como usar WRAPCOLS em C# para converter array em colunas, aplicar fórmula
  de matriz no Excel e criar uma pasta de trabalho do Excel programaticamente — tudo
  com passos claros.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: pt
lastmod: 2026-07-13
og_description: Como usar WRAPCOLS em C# permite converter rapidamente um array em
  colunas, aplicar uma fórmula de matriz ao estilo do Excel e avaliar o resultado
  programaticamente.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Como usar WRAPCOLS em C# – Criação rápida de pastas de trabalho Excel
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Como usar WRAPCOLS – Guia completo para automação Excel em C#
url: /pt/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS – Guia Completo para Automação Excel em C#

Já se perguntou **como usar WRAPCOLS** quando precisa transformar uma lista plana em uma tabela organizada dentro de um arquivo Excel gerado a partir de C#? Você não está sozinho. Seja construindo um motor de relatórios, exportando resultados de pesquisas ou apenas brincando com dados, a função WRAPCOLS pode remodelar instantaneamente um array no número de colunas que você especificar.  

Neste tutorial vamos percorrer todo o processo: desde **criar uma pasta de trabalho Excel programaticamente** até **aplicar uma fórmula de matriz no estilo Excel**, e finalmente **avaliar a fórmula com C#**. Ao final você será capaz de **converter array em colunas** em uma única linha de código, sem precisar de manipulação manual célula‑por‑célula.

> **O que você receberá:** um exemplo de código executável, explicação de cada passo, dicas para armadilhas comuns e sugestões para expandir a solução.

---

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0+ (ou qualquer runtime .NET recente)
- Uma IDE C# (Visual Studio, Rider ou VS Code)
- A biblioteca **Aspose.Cells for .NET** (a versão de teste gratuita funciona bem) – é a maneira mais fácil de manipular arquivos Excel sem precisar do Excel instalado.
- Familiaridade básica com a sintaxe C# e fórmulas Excel.

Se preferir outra biblioteca (por exemplo, EPPlus ou ClosedXML), as ideias principais permanecem as mesmas — basta trocar as chamadas de API.

---

## Etapa 1: Configure seu Projeto e Adicione a Biblioteca Excel

Primeiro de tudo, crie um novo aplicativo console e importe o Aspose.Cells via NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Dica profissional:** Use a flag `--version` para travar em uma versão estável conhecida, por exemplo, `Aspose.Cells 24.9`.

Agora abra `Program.cs`. Vamos começar adicionando os namespaces necessários:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Ter a biblioteca referenciada garante que possamos **criar uma pasta de trabalho Excel programaticamente** e trabalhar com fórmulas.

---

## Etapa 2: Crie uma Nova Pasta de Trabalho e a Célula Alvo

Em seguida, instancie uma nova pasta de trabalho e escolha a célula onde a fórmula WRAPCOLS viverá. Em termos do Excel, a célula **A1** corresponde à linha 0, coluna 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Por que fazemos isso? O objeto `Workbook` é o contêiner de todas as planilhas, estilos e cálculos. Ao referenciar explicitamente a célula, mantemos o código claro e evitamos “números mágicos” mais adiante.

---

## Etapa 3: Insira a Fórmula de Matriz WRAPCOLS

Agora vem o coração do tutorial — **como usar WRAPCOLS**. A função recebe um array e a quantidade de colunas, então devolve um intervalo bidimensional. Na sintaxe do Excel fica assim:

```
=WRAPCOLS({1,2,3,4}, 2)
```

Isso instrui o Excel a organizar os números 1‑4 em **2 colunas**, resultando em:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Para inserir essa fórmula a partir do C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Observe que estamos usando uma **string** que espelha o que você digitária na barra de fórmulas do Excel. Este é o passo de **apply array formula excel**, e o Aspose.Cells trata automaticamente como uma fórmula de matriz porque WRAPCOLS devolve um intervalo.

---

## Etapa 4: Forçar o Cálculo para que a Fórmula Seja Avaliada

O Excel normalmente recalcula de forma preguiçosa — apenas quando você abre o arquivo. Como queremos ler o resultado imediatamente, precisamos disparar um cálculo:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Chamar `Calculate()` é a ação de **evaluate excel formula c#** que força o motor a computar todas as fórmulas, incluindo nossa matriz WRAPCOLS. Sem essa chamada, `targetCell.Value` ainda seria `null`.

---

## Etapa 5: Recuperar e Verificar o Resultado

Agora que a pasta de trabalho foi calculada, podemos obter o(s) valor(es) das células ocupadas pela matriz. A célula superior‑esquerda (A1) contém o primeiro elemento, enquanto as células adjacentes contêm o restante. Vamos ler todo o bloco 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Ao executar o programa, o console deverá exibir:

```
1   3
2   4
```

Essa saída confirma que conseguimos **converter array em colunas** usando WRAPCOLS.

---

## Etapa 6: Salvar a Pasta de Trabalho (Opcional, mas Útil)

Se quiser abrir o arquivo no Excel e ver a fórmula ao vivo, basta salvá‑lo:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Abrir o arquivo mostrará a fórmula WRAPCOLS em A1 e o intervalo de 2 colunas preenchido abaixo. Essa etapa é útil para depuração ou para entregar o arquivo aos usuários finais.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar de mais de duas colunas?

Basta mudar o segundo argumento do WRAPCOLS. Por exemplo, `=WRAPCOLS({1,2,3,4,5,6},3)` produziria três colunas:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Atualize a linha C# consequentemente:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Posso alimentar um intervalo dinâmico em vez de um array codificado?

Com certeza. Você pode montar a string do array programaticamente:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

Dessa forma você **apply array formula excel** sobre a marcha, perfeito para relatórios com tamanhos de dados variáveis.

### E quanto ao tratamento de erros?

Se a fórmula estiver malformada, `Calculate()` lançará uma `CellsException`. Envolva o cálculo em um bloco try/catch e registre o erro:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Isso funciona em versões mais antigas do Excel?

WRAPCOLS foi introduzido no Excel 365/2021. Quando você salva o arquivo em um formato `.xls` mais antigo, a fórmula pode ser perdida. Use `.xlsx` se precisar que a função sobreviva fora do motor C#.

---

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está o programa completo, pronto para copiar e colar:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Execute `dotnet run` e você deverá ver a matriz impressa, seguida de uma confirmação de que o arquivo `.xlsx` existe.

---

## Recapitulação & Próximos Passos

Cobremos **como usar WRAPCOLS** para **converter array em colunas**, demonstramos a técnica de **apply array formula excel** a partir do C#, forçamos um cálculo para **evaluate excel formula c#**, e salvamos o resultado para consumo posterior.  

Se quiser ir mais longe:

- **Contagens de colunas dinâmicas:** deixe o número de colunas ser uma variável fornecida pelo usuário.
- **Estilizar a saída:** aplique fontes, bordas ou formatação condicional via Aspose.Cells após o cálculo.
- **Combinar com outras funções:** aninhe WRAPCOLS dentro de `LET` ou `FILTER`.

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Aspose.Cells .NET: Como Criar e Estilizar Pastas de Trabalho Excel Programaticamente](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [Como Criar e Salvar uma Pasta de Trabalho Excel como ODS Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Como Criar Intervalos Nomeados com Escopo de Pasta de Trabalho no Excel Usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}