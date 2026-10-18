---
category: general
date: 2026-07-29
description: Copie linhas de uma planilha para outra e aprenda como carregar uma pasta
  de trabalho do Excel programaticamente usando Aspose.Cells em um tutorial passo
  a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: pt
lastmod: 2026-07-29
og_description: Copie linhas de uma planilha para outra usando Aspose.Cells. Aprenda
  a carregar uma pasta de trabalho do Excel programaticamente e a preservar tabelas
  dinâmicas em apenas algumas linhas de C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Copiar linhas de uma planilha para outra – Guia de Automação Excel em C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Copiar linhas de uma planilha para outra – Guia Completo de C#
url: /pt/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar linhas de uma planilha para outra – Guia Completo em C#

Já precisou **copiar linhas de uma planilha para outra** mas não sabia como manter as fórmulas e tabelas dinâmicas intactas? Você não está sozinho. Em muitos pipelines de relatórios precisamos extrair um recorte de dados de uma planilha mestre e inseri‑lo em uma nova pasta de trabalho para processamento posterior. A boa notícia? Com Aspose.Cells você pode fazer isso programaticamente, e toda a operação leva apenas algumas linhas de código.

Neste tutorial vamos percorrer o carregamento de uma pasta de trabalho Excel programaticamente, a seleção de um intervalo e, em seguida, a cópia dessas linhas para uma pasta de trabalho novinha em folha, preservando quaisquer tabelas dinâmicas incorporadas. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto C# — sem necessidade de copiar e colar manualmente.

## O que você vai alcançar

- **Carregar a pasta de trabalho Excel programaticamente** usando a classe `Workbook` do Aspose.Cells.  
- Definir uma **área de células** que contém as linhas que você deseja mover.  
- **Copiar linhas de uma planilha para outra** com uma única chamada de método que mantém as tabelas dinâmicas ativas.  
- Salvar o resultado em um novo arquivo pronto para distribuição ou processamento adicional.

### Pré‑requisitos

- .NET 6.0 ou superior (o código funciona tanto em .NET Core quanto em .NET Framework).  
- Uma licença válida do Aspose.Cells (ou uma chave de avaliação temporária).  
- Duas pastas no disco: uma para a pasta de trabalho de origem (`Source.xlsx`) e outra para a de destino (`Destination.xlsx`).  

Se você tem tudo isso, vamos mergulhar.

## Etapa 1: Carregar a pasta de trabalho Excel programaticamente

Primeiro de tudo — antes de copiar qualquer coisa, você precisa trazer o arquivo de origem para a memória. Aspose.Cells torna isso muito fácil:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Por que isso importa:** Carregar a pasta de trabalho programaticamente lhe dá controle total sobre o conteúdo do arquivo sem nunca abrir o Excel no servidor. Também evita dores de cabeça com interop COM e funciona em ambientes sem interface gráfica, como pipelines de CI.

## Etapa 2: Definir o intervalo de origem que contém as linhas

Em seguida, identifique exatamente quais linhas você quer transferir. O objeto `CellArea` permite especificar um bloco retangular usando os endereços das células superior‑esquerda e inferior‑direita:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Dica profissional:** Se o tamanho dos seus dados mudar dinamicamente, você pode calcular `EndRow` com `sourceWorksheet.Cells.MaxDataRow` para sempre capturar a tabela completa.

## Etapa 3: Criar uma nova pasta de trabalho para o destino

Agora crie uma pasta de trabalho vazia que receberá as linhas copiadas. Essa pasta de trabalho começa com uma única planilha por padrão:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Por que uma nova pasta de trabalho?** Começar do zero garante que você não sobrescreva dados existentes por acidente e fornece um ambiente previsível para testes.

## Etapa 4: Copiar linhas de uma planilha para outra (preservando tabelas dinâmicas)

Aqui está o coração do tutorial. O método `CopyRows` copia as linhas selecionadas e, quando você passa `true` como último argumento, também copia quaisquer tabelas dinâmicas que estejam dentro do intervalo:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### O que está acontecendo nos bastidores?

- **Planilha de origem**: `sourceWorkbook.Worksheets[0]` aponta para a primeira planilha no arquivo de origem.  
- **Índices de linhas**: Aspose.Cells usa indexação baseada em zero, então `StartRow` e `EndRow` correspondem às linhas que você definiu em `sourceRange`.  
- **Linha de início no destino**: Começamos na linha 0 da nova planilha, colocando efetivamente o bloco copiado no topo.  
- **Flag `true`**: Este é o interruptor mágico que diz ao Aspose.Cells para clonar quaisquer tabelas dinâmicas encontradas dentro das linhas copiadas, preservando seu cache e conexões.

> **Aviso de caso extremo:** Se o intervalo de origem contiver células mescladas que se estendam fora da área definida, essas mesclagens serão truncadas. Para mantê‑las intactas, expanda o intervalo para cobrir totalmente a região mesclada.

## Etapa 5: Salvar a pasta de trabalho de destino

Por fim, grave o novo arquivo no disco. Você pode escolher qualquer pasta que desejar; apenas certifique‑se de que o processo tenha permissão de gravação:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Ao abrir `Destination.xlsx` você verá as linhas A1‑H20 duplicadas, completas com quaisquer tabelas dinâmicas que estavam originalmente incorporadas. O restante da pasta de trabalho permanece vazio, pronto para você adicionar mais planilhas ou dados posteriormente.

## Exemplo completo em funcionamento

Juntando tudo, aqui está o programa completo e executável:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Saída esperada** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Abra o arquivo de destino e verifique se os dados, a formatação e as tabelas dinâmicas estão exatamente como estavam na origem. Se notar algum dado faltando, verifique se o `sourceRange` engloba completamente as linhas relevantes.

## Perguntas comuns e dicas

- **Posso copiar para uma planilha específica em vez da primeira?**  
  Claro. Substitua `destinationWorkbook.Worksheets[0]` por `destinationWorkbook.Worksheets["TargetSheet"]` (crie a planilha primeiro se ela não existir).

- **E se eu precisar copiar apenas valores, não fórmulas?**  
  Use `CopyRows` com a sobrecarga que aceita um objeto `CopyRowsOptions` e defina `PasteType` para `PasteType.Values`.

- **Como lidar com arquivos grandes sem esgotar a memória?**  
  Aspose.Cells suporta **streaming** via `LoadOptions` com `MemorySetting.MemoryPreference`. Carregue a pasta de trabalho de origem com uma pegada de memória menor e a operação de cópia ainda será eficiente.

- **As tabelas dinâmicas permanecem ligadas à fonte de dados original?**  
  Quando você define a flag `true`, o cache da tabela dinâmica é duplicado, de modo que as pivôs da nova pasta de trabalho referenciam os dados copiados, não o arquivo original.

## Conclusão

Agora você sabe como **copiar linhas de uma planilha para outra** mantendo quaisquer tabelas dinâmicas intactas, e viu como **carregar uma pasta de trabalho Excel programaticamente** usando Aspose.Cells. Esse padrão é uma base sólida para construir pipelines de relatórios automatizados, scripts de migração de dados ou qualquer cenário em que seja necessário dividir dados do Excel em tempo real.

O que vem a seguir? Experimente estender o trecho para:

- Percorrer múltiplos intervalos de origem e agregá‑los em um único arquivo de destino.  
- Aplicar formatação condicional após a cópia para destacar métricas chave.  
- Exportar a pasta de trabalho final para PDF ou CSV para consumo posterior.

Sinta‑se à vontade para experimentar e, se encontrar algum obstáculo, deixe um comentário abaixo. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Copy Rows in Excel Using Aspose.Cells for .NET&#58; A C# Guide](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Copy Worksheet from One Workbook to Another using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}