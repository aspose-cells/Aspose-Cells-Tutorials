---
category: general
date: 2026-08-04
description: Defina a área da célula no Aspose.Cells e aprenda como copiar tabelas
  dinâmicas, copiar intervalos do Excel em C# e copiar intervalos na mesma planilha
  de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: pt
lastmod: 2026-08-04
og_description: Defina a área da célula no Aspose.Cells e copie o intervalo do Excel
  em C# preservando as tabelas dinâmicas. Siga este guia passo a passo para obter
  resultados confiáveis.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definir área da célula no Aspose.Cells – copiar intervalo do Excel em C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definir área da célula no Aspose.Cells e copiar intervalo do Excel em C#
url: /pt/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir área de célula no Aspose.Cells e copiar intervalo do Excel em C#

Se você precisar **definir área de célula** para um intervalo e, em seguida, copiar esse intervalo na mesma planilha, este guia mostra exatamente como fazer isso com Aspose.Cells para .NET. Seja movendo um relatório baseado em pivot ou duplicando um bloco de dados, você aprenderá o processo completo em apenas alguns passos.

Você também descobrirá **como copiar pivot** tables sem perder suas conexões, e verá um exemplo claro de **copy excel range c#** que funciona no cenário de **copy range same sheet**. Nenhuma ferramenta externa é necessária — apenas Aspose.Cells e algumas linhas de C#.

## O que você precisará

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+)
- Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`)
- Uma pasta de trabalho Excel (`input.xlsx`) que contém uma tabela pivot no intervalo A1:J50
- Um ambiente de desenvolvimento como o Visual Studio 2022

## Etapa 1: Definir a área de célula para o intervalo de origem

A primeira tarefa é **definir área de célula** que representa o bloco que você deseja copiar. Aspose.Cells usa a estrutura `CellArea`, que armazena índices de linha e coluna baseados em zero.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Por que isso importa:** `CellArea` informa ao Aspose.Cells exatamente quais células devem ser manipuladas. Usar índices baseados em zero evita erros de deslocamento comuns ao traduzir a notação A1 do Excel para código.

## Etapa 2: Definir a área de célula de destino na mesma planilha

Para **copy range same sheet**, você também deve especificar onde os dados devem ser colocados. O destino pode começar em qualquer linha; aqui começamos na linha 61 (índice base zero 60) para deixar um espaço em branco.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Por que isso importa:** Ao espelhar as dimensões da origem, você garante que o bloco copiado se encaixe perfeitamente sem truncamento.

## Etapa 3: Copiar o intervalo preservando tabelas pivot

Agora você pode **how to copy pivot** com segurança. A classe `CopyOptions` inclui a flag `CopyPivotTables` que mantém a definição da pivot, a fonte de dados e a formatação.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Por que isso importa:** Sem definir `CopyPivotTables = true`, a pivot se tornaria uma captura estática, perdendo a interatividade. Essa opção copia o cache subjacente e as conexões, de modo que a nova pivot se comporte exatamente como a original.

## Etapa 4: Salvar a pasta de trabalho

Por fim, grave as alterações no disco. O arquivo de saída demonstra que a tabela pivot foi duplicada na mesma planilha.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Dica profissional:** Use `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` se precisar impor um formato específico, especialmente ao trabalhar com versões mais antigas do Excel.

## Etapa 5: Verificar a tabela pivot copiada

Abra `CopyWithPivot.xlsx` no Excel e verifique o seguinte:

1. O intervalo A61:J110 contém uma cópia dos dados originais.
2. Uma nova tabela pivot aparece no topo do intervalo copiado.
3. Atualizar a pivot reflete alterações nos dados de origem, confirmando que **how to copy pivot** foi bem‑sucedido.

Se a pivot não atualizar, verifique se o intervalo de dados de origem na definição da pivot ainda aponta para a área original da pasta de trabalho. Aspose.Cells atualiza automaticamente a referência de origem quando `CopyPivotTables` está true.

## Casos limites e variações

| Situação | O que mudar |
|-----------|----------------|
| **Copiar para uma planilha diferente** | Substitua `srcWorkbook.Worksheets[0]` pelo índice ou nome da planilha de destino e ajuste `destinationRange` conforme necessário. |
| **Copiar um bloco de células mescladas** | Defina `CopyOptions.PasteType = PasteType.All` para preservar células mescladas e formatação. |
| **Copiar apenas valores, não fórmulas** | Use `CopyOptions.PasteType = PasteType.Values` para evitar transferir fórmulas que referenciam a planilha original. |
| **Intervalos grandes ( > 10.000 linhas )** | Considere usar `Workbook.Copy` para copiar planilhas inteiras e melhorar o desempenho, depois exclua as linhas indesejadas. |

Essas variações demonstram que a mesma lógica de **aspose.cells copy range** pode ser adaptada a muitos cenários reais.

## Exemplo completo em funcionamento

Abaixo está o programa completo, pronto para ser executado. Substitua `YOUR_DIRECTORY` por um caminho de pasta real na sua máquina.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Saída esperada:** Após executar o programa, `CopyWithPivot.xlsx` contém os dados originais mais um bloco idêntico começando na linha 61, completo com uma tabela pivot funcional.

## Conclusão

Agora você sabe como **definir área de célula** no Aspose.Cells, **copy excel range c#**, e **copy range same sheet** preservando toda a funcionalidade da pivot. Essa técnica elimina erros de copiar‑colar manual e escala para pastas de trabalho grandes.

Em seguida, explore tópicos relacionados como **how to copy pivot** entre várias planilhas, ou use **aspose.cells copy range** para duplicar planilhas inteiras com formatação. Experimente diferentes configurações de `CopyOptions` para adaptar o comportamento de cópia às necessidades do seu projeto.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}