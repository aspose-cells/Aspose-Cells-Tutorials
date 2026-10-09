---
category: general
date: 2026-06-27
description: Copie a tabela dinâmica para outra planilha em C# usando Aspose.Cells.
  Aprenda passo a passo como preservar os dados e a formatação da tabela dinâmica.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: pt
og_description: Copie a tabela dinâmica para outra planilha em C# com Aspose.Cells.
  Este tutorial mostra exatamente como duplicar uma tabela dinâmica mantendo sua formatação
  intacta.
og_title: Copiar Tabela Dinâmica para Outra Planilha – Guia Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copiar Tabela Dinâmica para Outra Planilha – Guia Completo de C#
url: /pt/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Tabela Dinâmica para Outra Planilha – Guia Completo em C#

Já precisou **copiar uma tabela dinâmica para outra planilha** mas temia perder os slicers, campos calculados ou a formatação? Você não está sozinho. Muitos desenvolvedores encontram esse obstáculo ao automatizar relatórios Excel, e a frustração é real. Neste guia vamos percorrer uma solução limpa, de ponta a ponta, que **preserva a tabela dinâmica** exatamente como aparece.

Usaremos **Aspose.Cells for .NET**, uma biblioteca poderosa que permite manipular arquivos Excel sem abrir o próprio Excel. Ao final deste tutorial você terá um trecho de código C# pronto‑para‑executar que copia uma tabela dinâmica de uma planilha para outra, mantendo todas as conexões de dados subjacentes intactas.

## O Que Este Tutorial Cobre

- Configurar um projeto .NET e adicionar o pacote NuGet Aspose.Cells.  
- Carregar uma pasta de trabalho existente que já contém uma tabela dinâmica.  
- Definir tanto o intervalo de origem (a tabela dinâmica original) quanto o intervalo de destino em outra planilha.  
- Usar `CopyOptions` para **preservar a tabela dinâmica** durante a cópia.  
- Salvar o resultado e verificar que a tabela dinâmica funciona em sua nova localização.  

Sem ferramentas externas, sem copiar‑colar manual, e sem mágica oculta — apenas código direto que você pode inserir em qualquer aplicativo console ou serviço C#.

> **Por que isso importa:** Automatizar a duplicação de tabelas dinâmicas economiza horas de trabalho manual, especialmente em pipelines de relatórios noturnos onde dezenas de pastas de trabalho precisam de estruturas de tabela dinâmica idênticas em várias planilhas.

---

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells

Primeiro de tudo. Se ainda não o fez, crie um novo projeto console .NET:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Agora adicione o pacote Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Dica de especialista:** Use a versão estável mais recente (a partir de junho 2026 v23.12). Ela inclui correções de bugs para o tratamento de `CopyPivotTable`.

## Etapa 2: Carregar a Pasta de Trabalho e Acessar as Planilhas

Abra a pasta de trabalho que contém a tabela dinâmica de origem. Na maioria dos cenários reais o arquivo está em uma unidade compartilhada, mas para esta demonstração vamos supor que ele está em uma pasta local chamada `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Aqui criamos uma nova planilha chamada **CopyDestination** onde a tabela dinâmica será inserida. Se você já tem uma planilha de destino, basta obtê‑la por índice ou nome.

## Etapa 3: Definir Intervalos de Origem e Destino

Uma tabela dinâmica vive dentro de um bloco retangular de células. Você precisa informar ao Aspose.Cells qual bloco copiar. Neste exemplo a tabela dinâmica ocupa as linhas 0‑20 e colunas 0‑10 (indexação baseada em zero).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Observe como calculamos dinamicamente a linha e a coluna final. Dessa forma, mesmo que você altere o tamanho do intervalo de origem mais tarde, o destino será ajustado automaticamente.

## Etapa 4: Executar a Cópia Preservando a Tabela Dinâmica

Agora a mágica acontece. Ao passar um objeto `CopyOptions` com `CopyPivotTable = true`, o Aspose.Cells sabe que deve manter a definição da tabela dinâmica intacta.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Nos bastidores, o Aspose.Cells recria o cache da tabela dinâmica, atualiza a referência da fonte de dados e reaplica qualquer formatação. Esta é a **duplicação de tabela dinâmica no Excel** que você estava procurando.

## Etapa 5: Salvar e Verificar o Resultado

Por fim, grave a pasta de trabalho de volta ao disco. Você pode manter o arquivo original intacto salvando com um novo nome.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Abra o `copy-pivot.xlsx` resultante e você verá a tabela dinâmica perfeitamente replicada na planilha **CopyDestination**, completa com slicers, campos calculados e formatação. A fonte de dados subjacente ainda aponta para a tabela original, de modo que a atualização funciona exatamente como antes.

> **E se a tabela dinâmica de origem abranger um intervalo dinâmico?**  
> Use `Worksheet.PivotTables[0].CacheDefinition.SourceData` para obter os limites reais, então construa `sourceRange` a partir dessas informações. Isso trata casos em que linhas ou colunas podem se expandir ao longo do tempo.

## Bônus: Preservar a Formatação da Tabela Dinâmica nas Cópias

Às vezes a cópia padrão perde formatação condicional ou formatos numéricos personalizados. Para evitar isso, amplie o `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Habilitar `CopyFormatting` garante que o requisito de **preservar a formatação da tabela dinâmica** seja atendido, proporcionando uma duplicata pixel‑perfeita.

## Saída Esperada

Ao executar o programa, o console encerrará silenciosamente (a menos que você adicione logs). Abrindo `copy-pivot.xlsx` você deverá ver:

- Planilha 1: Dados originais e tabela dinâmica inalterados.  
- **CopyDestination**: Uma réplica exata da tabela dinâmica, posicionada a partir da linha 31 (já que as linhas são baseadas em 1 na interface do Excel).  
- Todos os slicers e filtros funcionais; ao clicar em “Atualizar” ambos os pivôs são atualizados simultaneamente.

---

## Conclusão

Acabamos de demonstrar como **copiar uma tabela dinâmica para outra planilha** usando Aspose.Cells em C#. As etapas — configurar o projeto, carregar a pasta de trabalho, definir intervalos, copiar com `CopyPivotTable = true` e salvar — formam um padrão confiável que você pode reutilizar em qualquer pipeline de automação.

Se quiser ir além, considere:

- **Duplicação de tabelas dinâmicas** em múltiplas pastas de trabalho (percorrer arquivos).  
- Usar a opção **Aspose.Cells copy range with pivot** para mover pivôs entre diferentes pastas de trabalho.  
- Automatizar atualizações com `PivotTable.RefreshData()` após a cópia.

Sinta‑se à vontade para experimentar diferentes intervalos de origem ou combinar esta técnica com geração de gráficos para dashboards de relatório totalmente automatizados. Tem dúvidas? Deixe um comentário, e feliz codificação!

---

![Captura de tela mostrando a tabela dinâmica copiada em nova planilha](copy-pivot-screenshot.png "exemplo de copiar tabela dinâmica para outra planilha")


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui código completo e funcional com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como Alterar a Fonte de Dados da Tabela Dinâmica Usando Aspose.Cells for .NET | Guia de Análise de Dados](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Domine a Formatação de Tabelas Dinâmicas em .NET Usando Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Acesse Fontes de Dados Externas de Tabelas Dinâmicas em .NET usando Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}