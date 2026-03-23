---
category: general
date: 2026-03-22
description: Como usar lambda em C# para trabalhar com fórmulas do Excel. Aprenda
  a escrever fórmula em uma célula, converter intervalo em array, exibir o array no
  console e calcular a cotangente no Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: pt
og_description: Como usar lambda em C# para manipular fórmulas do Excel, converter
  intervalo em array, escrever fórmula em célula, exibir array no console e calcular
  cotangente no Excel.
og_title: Como usar Lambda em C# com fórmulas do Excel – passo a passo
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Como usar Lambda em C# com fórmulas do Excel – Guia completo
url: /pt/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Lambda em C# com Fórmulas do Excel – Guia Completo

Já se perguntou **como usar lambda** ao automatizar o Excel a partir do C#? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam combinar o poder das novas funções de matriz dinâmica do Excel com a capacidade `LAMBDA` do C#. A boa notícia? Na verdade é bem simples quando você vê as peças se encaixarem.

Neste tutorial vamos percorrer **escrever uma fórmula em uma célula**, **converter um intervalo em uma matriz**, **exibir essa matriz no console**, e até **calcular cotangente no Excel** — tudo enquanto mostramos **como usar lambda** dentro de uma chamada `REDUCE`. Ao final, você terá um trecho de código executável que pode ser inserido em qualquer projeto .NET que referencie Aspose.Cells (ou uma biblioteca similar).

---

## O que você aprenderá

- Como **escrever fórmula em célula** usando C#.
- Como **converter intervalo em matriz** com a função `EXPAND`.
- Como **exibir matriz no console** após o cálculo.
- Como **calcular cotangente no Excel** usando `COT` e `COTH`.
- A sintaxe exata para **como usar lambda** dentro da função `REDUCE` do Excel a partir do C#.

> **Pré-requisito:** Você precisa de uma versão recente do .NET (Core 6+ ou .NET Framework 4.7+) e da biblioteca Aspose.Cells para .NET instalada via NuGet.

---

## Passo 1: Configurar a Pasta de Trabalho e Escrever a Fórmula na Célula

A primeira coisa que fazemos é criar uma nova pasta de trabalho e obter a primeira planilha. Em seguida, **escrevemos uma fórmula em uma célula** – neste caso `A1` conterá o resultado de uma chamada `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Por que isso importa:** Escrever a fórmula diretamente a partir do código permite gerar planilhas complexas dinamicamente sem nunca abrir o Excel. Também prepara o terreno para o próximo passo, onde **convertemos o intervalo em matriz**.

---

## Passo 2: Converter Intervalo em Matriz com EXPAND

`EXPAND` é a forma do Excel de transformar um pequeno intervalo em uma matriz maior. Ao colocar a fórmula em `A1`, o Excel derramará um bloco 4 × 5 começando nessa célula. A partir do C#, não precisamos copiar valores manualmente – a biblioteca fará o trabalho pesado quando chamarmos `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Como usar lambda:** Ainda não, mas aguarde. Primeiro precisamos dos dados na planilha, depois reduziremos com um lambda.

---

## Passo 3: Usar LAMBDA Dentro de REDUCE – O Núcleo de “Como Usar Lambda”

O Excel 365 introduziu `REDUCE`, que aceita um **valor inicial**, um **intervalo**, e um **LAMBDA** que indica como combinar cada elemento. Do C# simplesmente atribuímos a string da fórmula; o lambda vive dentro da fórmula do Excel, não no código C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Explicação:**  
- `0` é o acumulador inicial (`acc`).  
- `A1:D4` é o intervalo que queremos processar (as quatro primeiras colunas do derramamento).  
- `LAMBDA(acc, x, acc + x)` indica ao Excel para somar cada célula (`x`) ao acumulador.  

Essa é a essência de **como usar lambda** para agregação em um contexto de planilha.

---

## Passo 4: Calcular Cotangente no Excel – De Graus a Hiperbólica

Se precisar de resultados trigonométricos, as funções `COT` e `COTH` do Excel são muito práticas. Vamos colocá‑las em `G1` e `G2`, respectivamente.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Por que isso é útil:** Saber **calcular cotangente no Excel** pode economizar a escrita de código matemático personalizado, especialmente quando a pasta de trabalho será compartilhada com não‑desenvolvedores.

---

## Passo 5: Forçar o Cálculo e Recuperar a Matriz Expandida

Agora instruímos a pasta de trabalho a avaliar todas as fórmulas, então extraímos a matriz derramada de `A1`. É aqui que **exibimos a matriz no console**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**O que você verá:**  
- Uma matriz 4 × 5 formatada de forma agradável, impressa linha por linha.  
- A soma calculada pelo lambda `REDUCE`.  
- Os dois valores de cotangente.

Isso completa o fluxo desde **escrever fórmula em célula** até **exibir matriz no console**.

---

## Exemplo Completo (Pronto para Copiar e Colar)

Abaixo está o programa inteiro que você pode inserir em um aplicativo console. Lembre‑se de adicionar o pacote NuGet `Aspose.Cells` primeiro (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Saída esperada no console (os valores variarão com base no conteúdo padrão de B1:C2, que são 0 por padrão):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Sinta‑se à vontade para preencher `B1:C2` com seus próprios números antes de executar – a matriz refletirá esses valores.

---

## Dicas Profissionais & Armadilhas Comuns

- **Dica profissional:** Se precisar que o intervalo derramado comece em outro lugar, basta mudar a célula de destino (`A1`). A função `EXPAND` respeita o ponto de ancoragem.
- **Cuidado com:** Células vazias no intervalo de origem tornam‑se `0` na matriz derramada, o que pode afetar a soma do seu `REDUCE`.
- **Caso extremo:** Quando a pasta de trabalho contém fórmulas que dependem de funções voláteis (ex.: `NOW()`), chame `workbook.Calculate()` após definir todas as fórmulas para garantir que tudo esteja atualizado.
- **Nota de desempenho:** Para derramamentos muito grandes, considere limitar o tamanho na chamada `EXPAND`; caso contrário, você pode alocar mais memória do que o necessário.
- **Compatibilidade:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}