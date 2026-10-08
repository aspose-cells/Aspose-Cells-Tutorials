---
category: general
date: 2026-06-17
description: Como usar WRAPCOLS em C# para remodelar um array em uma matriz, escrever
  fórmula de matriz em uma célula e carregar arquivos Excel existentes com Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: pt
og_description: Como usar WRAPCOLS em C# para rapidamente remodelar um array em uma
  matriz, escrever uma fórmula de matriz em uma célula e trabalhar com arquivos Excel
  existentes.
og_title: Como usar WRAPCOLS em C# – Redimensionar um array para uma matriz
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: Como usar WRAPCOLS em C# – Redimensionar um array para uma matriz no Excel
url: /pt/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS em C# – Remodelar um Array em uma Matriz no Excel

Já se perguntou **como usar WRAPCOLS** para transformar uma lista plana de números em uma tabela organizada dentro do Excel? Você não está sozinho. Seja construindo uma ferramenta de relatórios ou apenas brincando com dados, remodelar um array em uma matriz pode economizar muito trabalho manual de copiar‑e‑colar.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **escrever uma fórmula de array em uma célula**, calcular o resultado e até **carregar um workbook do Excel** existente, se precisar. Ao final, você terá um trecho pronto para copiar‑e‑colar que funciona com a versão mais recente do Aspose.Cells para .NET.

## O que Você Vai Aprender

- O propósito da função `WRAPCOLS` e quando ela se destaca.  
- Como **remodelar um array em uma matriz** usando uma única fórmula.  
- Código passo a passo para **escrever uma fórmula em uma célula** e forçar o cálculo.  
- Técnicas opcionais para **carregar um arquivo Excel existente** antes de aplicar a fórmula.  
- Armadilhas comuns e dicas para expandir a abordagem para conjuntos de dados maiores.

Nenhuma documentação externa necessária—tudo que você precisa está aqui.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
- Aspose.Cells para .NET instalado (`dotnet add package Aspose.Cells`).  
- Noções básicas de sintaxe C#; se você está confortável criando um aplicativo console, está pronto para começar.

> **Dica de especialista:** Se estiver usando o Visual Studio, habilite *nullable reference types* (`<Nullable>enable</Nullable>`) para detectar possíveis bugs de null mais cedo.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Primeiro, crie um novo projeto console (ou adicione o código a um existente). Em seguida, adicione as diretivas `using` necessárias para que o compilador saiba onde `Workbook` e `Worksheet` estão.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Por que isso importa:** Importar `Aspose.Cells` lhe dá acesso ao motor de Excel de alto desempenho que avalia `WRAPCOLS` sem precisar do Excel instalado na máquina.

## Etapa 2: Criar ou Carregar um Workbook

Você pode começar do zero ou abrir um arquivo existente. O trecho abaixo mostra ambas as opções; basta comentar a que não for usar.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Caso de borda:** Se o arquivo que você está carregando estiver protegido por senha, passe a senha como segundo argumento: `new Workbook(path, "password")`.

## Etapa 3: Obter a Worksheet de Destino

Na maioria das vezes a primeira planilha (`Worksheets[0]`) é a que você quer, mas também pode referenciar uma planilha pelo nome.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Etapa 4: Escrever a Fórmula WRAPCOLS em uma Célula

Aqui está o coração do tutorial. `WRAPCOLS` recebe um array e a quantidade de colunas, então espalha os valores por linhas. Colocaremos a fórmula em **A1** para que a matriz comece no canto superior esquerdo.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **O que está acontecendo?**  
> - A sintaxe de chaves `{1,2,3,4,5,6}` cria uma constante de array inline.  
> - O segundo argumento (`3`) indica ao Excel que crie três colunas, envolvendo automaticamente os itens restantes em novas linhas.  
> - Como estamos usando Aspose.Cells, a fórmula é armazenada exatamente como você a digitasse no Excel, e o motor a avaliará sob demanda.

### Opcional: Escrever uma Referência a um Array Dinâmico

Se preferir referenciar um intervalo em vez de uma lista fixa, você pode usar:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

Dessa forma a matriz é atualizada automaticamente sempre que o intervalo de origem mudar.

## Etapa 5: Forçar o Cálculo e Persistir o Resultado

Aspose.Cells não calcula fórmulas até que você solicite. Chamando `Calculate()` o resultado é materializado, transformando a saída da fórmula em valores reais nas células.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

Ao abrir `output.xlsx` no Excel, você verá:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Esse é o efeito de **remodelar array em matriz** que você buscava.

## Exemplo Completo Funcionando

Juntando todas as peças, aqui está um programa pronto‑para‑executar:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Execute o programa, abra `output.xlsx` e você verá a matriz exatamente como mostrada acima.

## Perguntas Frequentes & Armadilhas

### 1. E se eu precisar de um número diferente de linhas?

`WRAPCOLS` aceita apenas a contagem de colunas; a quantidade de linhas é inferida. Para forçar um número específico de linhas, combine‑a com `WRAPROWS` ou preencha o array de origem com strings vazias.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. WRAPCOLS funciona com valores de texto?

Com certeza. Substitua os números por strings entre aspas:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Posso aplicar formatação à matriz gerada?

Após o cálculo, você pode estilizar o intervalo programaticamente:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. Como lidar com arrays muito grandes?

Aspose.Cells pode processar dezenas de milhares de elementos, mas fique atento ao consumo de memória. Se atingir limites, considere escrever os dados em blocos ou usar `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Dicas de Profissional para Código de Produção

- **Cache a referência da worksheet** se estiver escrevendo muitas fórmulas em um loop; isso reduz a sobrecarga de busca.  
- **Desative o cálculo automático** (`workbook.Settings.CalculateFormulaOnOpen = false;`) quando for escrever dezenas de fórmulas em lote, e chame `Calculate()` uma única vez ao final.  
- **Envolva I/O de arquivos em try/catch** para expor erros de permissão rapidamente:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Valide a entrada** antes de montar a string da fórmula—especialmente se concatenar valores fornecidos pelo usuário—para evitar fórmulas malformadas.

## Resumo Visual

![Como usar WRAPCOLS resultado matriz no Excel](wrapcols-output.png "Como usar WRAPCOLS em C# para remodelar um array em uma matriz")

*A captura de tela mostra a matriz 2 × 3 produzida pela fórmula WRAPCOLS.*

## Conclusão

Cobremos **como usar WRAPCOLS** em C# do início ao fim: criar ou carregar um workbook, escrever uma fórmula de array em uma célula, forçar o cálculo e salvar o resultado. Agora você sabe como **remodelar um array em uma matriz**, **escrever uma fórmula de array** e **carregar arquivos Excel existentes**—tudo com poucas linhas de código limpo e mantível.

Em seguida, você pode explorar:


## O que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Load Excel Files Efficiently Using Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}