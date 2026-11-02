---
category: general
date: 2026-06-27
description: como usar wrapcols e wrap rows excel em C#. Aprenda a criar uma pasta
  de trabalho Excel em C# e recalcular fórmulas do Excel com um exemplo passo a passo.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: pt
og_description: Como usar wrapcols e wrap rows no Excel usando C#. Este guia mostra
  como criar uma pasta de trabalho Excel em C# e recalcular fórmulas do Excel em minutos.
og_title: Como usar wrapcols em C# – Tutorial completo de wrap no Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Como usar wrapcols em C# – Guia completo com Excel WRAPROWS e Recalcular Fórmulas
url: /pt/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como usar wrapcols em C# – Guia Completo com Excel WRAPROWS & Recalcular Fórmulas

Já se perguntou **como usar wrapcols** quando precisa transformar uma lista longa em uma grade organizada? Talvez você já tenha tentado o truque manual de copiar‑colar, mas ele é lento, propenso a erros e, francamente, um incômodo. A boa notícia? O `WRAPCOLS` do Excel (e seu irmão `WRAPROWS`) podem fazer o trabalho pesado por você — *e* você pode acioná‑los a partir de código C#.

Neste tutorial vamos percorrer a criação de uma planilha Excel em C#, aplicar `WRAPCOLS` e `WRAPROWS` e, finalmente, **recalcular fórmulas do Excel** para que os dados envoltos apareçam instantaneamente. Ao final, você terá um trecho pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

## O que Você Vai Aprender

- Como **criar excel workbook c#** usando a biblioteca Aspose.Cells (sem necessidade de COM interop).  
- A sintaxe exata da função `WRAPCOLS` e como ela difere de `WRAPROWS`.  
- Por que você deve **recalcular excel formulas** após inserir as funções, e como fazer isso de forma eficiente.  
- Um exemplo completo e executável que você pode copiar‑colar e ver o resultado em um arquivo `.xlsx`.  

**Pré‑requisitos** – Você precisa de .NET 6+ (ou .NET Framework 4.7+), Visual Studio 2022 ou qualquer IDE de sua preferência, e o pacote NuGet Aspose.Cells for .NET. Se você é novo no Aspose.Cells, não se preocupe; os passos são diretos e totalmente explicados.

---

## Etapa 1: Configurar o Projeto e Instalar Aspose.Cells

Para começar, crie um novo projeto de console:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Dica de especialista:** Se estiver usando o Visual Studio, basta clicar com o botão direito no projeto → *Manage NuGet Packages* → pesquisar por **Aspose.Cells** e instalá‑lo.

A biblioteca nos fornece as classes `Workbook`, `Worksheet` e `Cell` que usaremos ao longo do tutorial.

## Etapa 2: Criar uma Planilha Excel e Preencher Dados de Exemplo

Agora vamos criar uma workbook, obter a primeira planilha e preencher as colunas **A** e **B** com números de exemplo. Esses dados serão posteriormente envolvidos em colunas e linhas.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Por que isso importa:** Ter dados determinísticos permite que você verifique se `WRAPCOLS` e `WRAPROWS` estão fazendo exatamente o que você espera.

## Etapa 3: Aplicar a Função `WRAPCOLS` – **como usar wrapcols**

`WRAPCOLS` recebe um intervalo unidimensional e o distribui em um número especificado de colunas, adicionando novas linhas conforme necessário. Aqui está a fórmula exata que inseriremos na célula **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explicação:** O segundo argumento (`3`) indica ao Excel que crie três colunas por linha. Assim, os três primeiros valores (1, 2, 3) ficam em A1:C1, os próximos três (4, 5, 6) vão para A2:C2, e os valores restantes preenchem a linha seguinte.

## Etapa 4: Aplicar a Função `WRAPROWS` – wrap rows excel

`WRAPROWS` faz o oposto: recebe um intervalo vertical e o organiza em um número definido de linhas por coluna. Colocaremos esta fórmula em **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explicação:** Com `2` linhas por coluna, os valores “A, B” vão para B1:B2, “C, D” para C1:C2, e assim por diante. A função expande a planilha horizontalmente automaticamente.

## Etapa 5: Recalcular Todas as Fórmulas – **recalculate excel formulas**

Quando você define uma fórmula programaticamente, o Excel não calcula o resultado até que a workbook seja aberta ou você indique explicitamente à biblioteca que a avalie. É aí que entra **recalculate excel formulas**:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Por que você precisa disso:** Sem chamar `CalculateFormula()`, as células mostrarão o texto bruto `=WRAPCOLS(...)` ao abrir o arquivo, o que anula o objetivo do tutorial.

## Etapa 6: Salvar a Workbook e Verificar a Saída

Por fim, grave a workbook no disco. Você pode abrir o arquivo resultante no Excel para ver o layout envolto.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Resultado Esperado

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Colunas A‑C** são preenchidas pela chamada `WRAPCOLS` (três colunas por linha).  
- **Linhas B‑I** são preenchidas pela chamada `WRAPROWS` (duas linhas por coluna).  

Abra `output.xlsx` e você verá exatamente o layout mostrado acima. Se os números não coincidirem, verifique as strings das fórmulas e assegure‑se de que `CalculateFormula()` foi chamado.

---

## Perguntas Frequentes & Casos de Borda

### E se o intervalo de origem estiver vazio?
Tanto `WRAPCOLS` quanto `WRAPROWS` simplesmente retornam um array vazio, resultando em uma célula em branco. É seguro chamar as funções mesmo quando não se tem certeza da presença de dados.

### Posso envolver mais de um intervalo ao mesmo tempo?
Sim — basta colocar fórmulas adicionais em outras células. Cada fórmula funciona de forma independente, então você poderia ter `WRAPCOLS` em D1, `WRAPROWS` em E1, etc.

### Como isso difere de um simples copiar‑colar transposto?
`WRAPCOLS`/`WRAPROWS` lidam com *paginação* automaticamente. Se você tem 20 itens e solicita 3 colunas, a função cria o número necessário de linhas (7 neste caso) sem que você precise calcular as dimensões manualmente.

### A biblioteca suporta funções de matriz dinâmica (Excel 365)?
Aspose.Cells oferece suporte total a funções de matriz dinâmica, incluindo `WRAPCOLS` e `WRAPROWS`. O motor de cálculo espalhará os resultados exatamente como o Excel nativo.

### E quanto ao desempenho em grandes volumes de dados?
Para milhões de linhas, considere processar o cálculo em lotes (`workbook.CalculateFormula(FormulaCalculationOptions)`) ou desativar o cálculo automático enquanto insere as fórmulas, reativando‑o antes de salvar.

---

## Código Fonte Completo (Pronto para Executar)

Abaixo está o programa completo — copie para `Program.cs` e pressione **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Conclusão

Agora você sabe **como usar wrapcols** (e seu contraponto `WRAPROWS`) a partir de C# para remodelar dados em uma planilha Excel, e entende por que **recalculate excel formulas** é uma etapa obrigatória. Esse padrão — *criar excel workbook c# → inserir funções WRAP → recalcular* — é uma base sólida para qualquer tarefa de relatório ou apresentação de dados que exija layouts dinâmicos de colunas ou linhas.

O que vem a seguir? Experimente:

- Diferentes contagens de colunas/linhas (`WRAPCOLS(..., 5)` ou `WRAPROWS(..., 4)`).  
- Combinar `WRAPCOLS` com outras funções de matriz dinâmica como `FILTER` ou `SORT`.  
- Exportar a workbook para PDF com `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Sinta‑se à vontade para ajustar o exemplo, adicionar estilos ou integrá‑lo a um pipeline de automação maior. Se encontrar algum obstáculo, deixe um comentário abaixo — feliz codificação!

![Diagrama mostrando como wrapcols e wraprows transformam uma única coluna em uma grade – exemplo de como usar wrapcols](wrapcols-wraprows-diagram.png "exemplo de como usar wrapcols")


## O que Você Deve Aprender a Seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Hide Rows and Columns in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}