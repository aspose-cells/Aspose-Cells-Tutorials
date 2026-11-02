---
category: general
date: 2026-05-23
description: Como usar WRAPCOLS em C# para remodelar um array 1D em uma matriz 2D.
  Aprenda a função wrap columns, escreva a fórmula na célula e converta de 1D para
  2D facilmente.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: pt
og_description: Como usar WRAPCOLS em C# permite remodelar um array 1D em uma matriz
  2D com uma única fórmula. Siga este guia para escrever a fórmula na célula e dominar
  a função de envolver colunas.
og_title: Como usar WRAPCOLS em C# – Redimensionar arrays para matrizes
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Como usar WRAPCOLS em C# – Redimensionar arrays para matrizes
url: /pt/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS em C# – Redimensionar Arrays para Matrizes

Já se perguntou **como usar WRAPCOLS** quando precisa transformar uma lista plana de números em uma tabela organizada? Você não está sozinho — muitos desenvolvedores esbarram em um obstáculo ao tentar converter uma lista unidimensional em uma grade bidimensional sem escrever muito código de loop. A boa notícia? A função WRAPCOLS (às vezes chamada de função wrap columns) faz o trabalho pesado em uma única linha, e você pode inseri‑la diretamente em uma planilha Excel a partir do C#.

Neste tutorial vamos percorrer todo o processo: desde a criação de uma planilha, até **escrever fórmula em célula**, **redimensionar array para matriz**, e finalmente **converter 1d para 2d** usando a fórmula WRAPCOLS. Ao final, você terá um trecho reutilizável que funciona com qualquer array numérico e entenderá por que a função wrap columns costuma ser uma alternativa mais limpa ao redimensionamento manual de arrays.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

* .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)
* A biblioteca **Aspose.Cells for .NET** (versão de avaliação ou licença) — é o componente que nos fornece os objetos `Workbook`, `Worksheet` e `Cell` usados abaixo.
* Noções básicas de sintaxe C# — não é necessário conhecimento avançado de Excel.

Tem tudo isso? Ótimo — vamos colocar a mão na massa.

![Matriz 2x3 resultante após usar a função WRAPCOLS em C# – como usar WRAPCOLS](https://example.com/images/wrapcols-result.png "Como usar WRAPCOLS – matriz 2x3 resultante")

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells

### Por que isso importa

Você poderia tentar implementar sua própria lógica de matriz, mas a **função wrap columns** já trata casos de borda como divisão desigual e entradas vazias. Adicionar o pacote NuGet Aspose.Cells nos fornece uma API limpa para interagir com fórmulas do Excel diretamente do C#.

```bash
dotnet add package Aspose.Cells
```

*Dica:* Se estiver usando o Visual Studio, clique com o botão direito no projeto → **Gerenciar Pacotes NuGet** → procure por **Aspose.Cells** e instale a versão estável mais recente.

## Etapa 2: Criar uma Nova Workbook (ou Carregar uma Existente)

Agora que a biblioteca está configurada, podemos instanciar um objeto workbook. É aqui que a etapa **escrever fórmula em célula** acontecerá.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Aqui criamos um workbook novinho em folha; você também pode carregar um arquivo existente com `new Workbook("path/to/file.xlsx")` caso precise inserir a matriz em um modelo pré‑formatado.

## Etapa 3: Inserir a Fórmula WRAPCOLS em uma Célula

### O núcleo de “como usar WRAPCOLS”

A função **WRAPCOLS** recebe dois argumentos: um array (ou intervalo) e o número de colunas que você deseja por linha. No nosso caso, vamos redimensionar o array literal `{1,2,3,4,5,6}` para **2 linhas × 3 colunas**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Observe como a fórmula espelha exatamente o que você digitária no próprio Excel. Ao colocá‑la em `Cells[0,0]` (célula **A1**) estamos **escrevendo a fórmula em uma célula** sem nenhum encanamento adicional.

## Etapa 4: Forçar o Cálculo para que a Fórmula Seja Avaliada

O Aspose.Cells não avalia fórmulas automaticamente a menos que você o instrua. Esta etapa garante que o workbook realmente contenha a matriz redimensionada.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Se você pular esta linha, as células ainda exibirão o texto da fórmula em vez dos valores calculados.

## Etapa 5: Ler o Resultado de Volta (Opcional, mas Útil para Verificação)

Talvez você queira confirmar que a operação **redimensionar array para matriz** foi bem‑sucedida. Aqui está um loop rápido que imprime a grade 2‑por‑3 resultante no console.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Saída esperada

```
1   2   3
4   5   6
```

O console mostra exatamente o mesmo layout que você veria no Excel após a execução da fórmula WRAPCOLS. Essa é a transformação **converter 1d para 2d** em ação.

## Etapa 6: Tratando Casos de Borda – E se o Comprimento do Array Não for Múltiplo do Número de Colunas?

Se o array de origem tiver, por exemplo, 7 elementos e você solicitar 3 colunas, WRAPCOLS criará a última linha com o(s) elemento(s) restante(s) e deixará as células restantes vazias. Veja um ajuste rápido para demonstrar:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Resultado:

```
1   2   3
4   5   6
7       
```

A **função wrap columns** preenche elegantemente a linha final com células vazias, de modo que você não precise de código extra para lidar com tamanhos incompatíveis.

## Etapa 7: Usando WRAPCOLS com Dados Dinâmicos

Em projetos reais você raramente codificará o array manualmente. Em vez disso, você construirá uma representação em string a partir de uma coleção C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Agora você **converteu 1d para 2d** para qualquer comprimento, e ainda obtém a mesma saída de matriz limpa. A fórmula é construída em tempo de execução, mas a **função wrap columns** subjacente permanece a mesma.

## Armadilhas Comuns e Dicas Profissionais

| Armadilha | Por que acontece | Solução |
|----------|------------------|---------|
| Esquecer `workbook.CalculateFormula()` | Aspose.Cells deixa as fórmulas sem avaliação | Sempre chame o método após definir qualquer fórmula |
| Usar um literal de array não numérico | WRAPCOLS espera números ou strings que possam ser convertidas | Garanta que o literal contenha apenas números (ou strings entre aspas) |
| Sobrescrever dados existentes inadvertidamente | Colocar a fórmula em uma célula que já contém dados | Escolha uma célula livre (ex.: A1) ou limpe o intervalo primeiro |
| Não referenciar o índice correto da planilha | `Worksheets[0]` é a primeira aba, mas você pode ter adicionado outras | Verifique `worksheet = workbook.Worksheets["SheetName"];` se necessário |

## Por que WRAPCOLS Supera Loops Manuais

* **Readability** – Uma linha de fórmula substitui dezenas de loops `for`.  
* **Performance** – O motor nativo do Excel é altamente otimizado para fórmulas de array.  
* **Maintainability** – Desenvolvedores futuros podem ver a intenção instantaneamente: “envolver esses valores em colunas”.  
* **Portability** – A mesma fórmula funciona se você exportar a planilha para Google Sheets ou LibreOffice — sem lógica específica de C# necessária.

## Exemplo Completo (Pronto para Copiar‑Colar)



## Tutoriais Relacionados

- [Como usar Aspose.Cells para .NET para exibir intervalos de células como rótulos de dados em gráficos](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Como usar Aspose.Cells para .NET para agrupar linhas e colunas no Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Como usar a função IF do Excel](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}