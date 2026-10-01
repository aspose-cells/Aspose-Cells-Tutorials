---
category: general
date: 2026-10-01
description: Copiar tabela dinâmica em C# usando Aspose.Cells. Aprenda como carregar
  a pasta de trabalho do Excel, definir intervalos e copiar o intervalo para a planilha,
  preservando a tabela dinâmica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- load excel workbook c#
- copy range to worksheet
language: pt
lastmod: 2026-10-01
og_description: Copiar tabela dinâmica em C# com Aspose.Cells. Este tutorial mostra
  como carregar uma pasta de trabalho do Excel, copiar um intervalo para a planilha
  e manter a tabela dinâmica.
og_image_alt: Screenshot of C# code copying a pivot table between worksheets
og_title: Copiar tabela dinâmica em C# – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Copy pivot table in C# using Aspose.Cells. Learn how to load Excel
    workbook, define ranges, and copy range to worksheet while preserving the pivot.
  headline: Copy pivot table between worksheets in C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copiar tabela dinâmica entre planilhas em C# – guia passo a passo
url: /pt/net/pivot-tables/copy-pivot-table-between-worksheets-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabela dinâmica entre planilhas em C# – guia passo a passo

Se você precisa **copiar tabela dinâmica** de uma planilha para outra em um arquivo .xlsx, este guia mostra exatamente como fazer isso com C#. Você aprenderá como **carregar pasta de trabalho Excel C#**, definir intervalos correspondentes e **copiar intervalo para planilha** mantendo a tabela dinâmica intacta. A solução funciona com Aspose.Cells .NET, uma biblioteca que preserva as definições da tabela dinâmica durante operações de cópia.

## Carregar pasta de trabalho Excel em C#

Antes de manipular quaisquer dados, você deve carregar a pasta de trabalho de origem na memória. Aspose.Cells fornece a classe `Workbook`, que lê o arquivo e constrói um modelo de objeto que representa planilhas, células e tabelas dinâmicas.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Path to the source workbook that contains the original pivot table
        const string sourcePath = @"YOUR_DIRECTORY\Input.xlsx";

        // Load the workbook – this is the step that answers “load excel workbook c#”
        Workbook workbook = new Workbook(sourcePath);
        // The workbook now holds all worksheets, including any pivot tables.
```

**Por que isso importa:** Carregar a pasta de trabalho uma única vez fornece uma única fonte de verdade. Todas as operações subsequentes trabalham nessa representação em memória, o que é mais rápido do que abrir o arquivo repetidamente.

## Definir intervalos de origem e destino

Uma tabela dinâmica vive dentro de um bloco retangular de células. Para copiá‑la, você cria um objeto `Range` que engloba todo o bloco. As mesmas dimensões devem existir na planilha de destino; caso contrário, a cópia truncará os dados.

```csharp
        // Step 2: Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.Worksheets[0];

        // Step 3: Define the exact range that includes the pivot table.
        // Adjust "A1:G20" to match the actual size of your pivot.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

> **Dica:** Se você não tem certeza sobre o intervalo, use `sourceSheet.PivotTables[0].DataRange.FirstCell.Name` e `LastCell.Name` para construir o endereço programaticamente.

## Adicionar uma nova planilha e preparar o intervalo de destino

Agora crie uma planilha nova que hospedará a tabela dinâmica copiada. O intervalo de destino deve ter o mesmo endereço que o intervalo de origem.

```csharp
        // Step 4: Add a new worksheet for the copy
        Worksheet destinationSheet = workbook.Worksheets.Add();

        // Create a matching range on the new sheet
        Range destinationRange = destinationSheet.Cells.CreateRange("A1:G20");
```

**Por que esta etapa é necessária:** Tabelas dinâmicas estão vinculadas ao contexto de uma planilha. Copiar o intervalo sem uma planilha de destino lançaria uma exceção porque as células alvo não existem.

## Copiar intervalo para a planilha preservando a tabela dinâmica

O método `Range.Copy` do Aspose.Cells copia não apenas valores brutos, mas também objetos subjacentes como tabelas dinâmicas, gráficos e intervalos nomeados. Este é o núcleo de **como copiar tabela dinâmica** sem perder sua definição.

```csharp
        // Step 5: Perform the copy – the pivot table definition travels with the cells
        sourceRange.Copy(destinationRange);
```

> **Pro dica:** Após a cópia, você pode verificar que a tabela dinâmica aparece em `destinationSheet.PivotTables`. O método `Copy` mantém a fonte de dados, filtros e layout da tabela dinâmica original.

## Salvar a pasta de trabalho com a tabela dinâmica copiada

Por fim, grave a pasta de trabalho modificada em um novo arquivo. O arquivo resultante contém a planilha original mais uma planilha duplicada com uma tabela dinâmica idêntica.

```csharp
        // Step 6: Save the workbook under a new name
        const string outputPath = @"YOUR_DIRECTORY\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        // Optional: Inform the user
        System.Console.WriteLine($"Pivot table copied successfully to {outputPath}");
    }
}
```

Ao abrir `CopyWithPivot.xlsx` no Excel, você verá duas planilhas: a original e a nova, cada uma exibindo a mesma tabela dinâmica com os mesmos filtros e campos calculados.

## Armadilhas comuns e boas práticas

| Problema | Por que acontece | Como evitar |
|----------|------------------|--------------|
| **Intervalo não cobre toda a tabela dinâmica** | A fonte de dados da tabela pode se estender além das células selecionadas, causando campos ausentes. | Use a propriedade `DataRange` da tabela dinâmica para gerar o endereço automaticamente. |
| **Planilha de destino já contém uma tabela dinâmica com o mesmo nome** | Aspose.Cells lança um conflito de nomes. | Renomeie a tabela dinâmica de destino após a cópia: `destinationSheet.PivotTables[0].Name = "PivotCopy";` |
| **Pastas de trabalho grandes causam pressão de memória** | Carregar a pasta de trabalho inteira na memória pode ser pesado. | Use `LoadOptions` para carregar apenas as planilhas necessárias se você não precisar do arquivo completo. |
| **Cópia entre versões diferentes do Excel** | Algumas versões mais antigas não suportam certos recursos de tabela dinâmica. | Salve o resultado como `.xlsx` (Office Open XML) para garantir compatibilidade. |

## Expandindo a solução

Depois de ter uma rotina confiável de **cópia de tabela dinâmica**, você pode criar fluxos de trabalho mais sofisticados:

* **Cópia em lote:** Percorra todas as planilhas que contêm tabelas dinâmicas e duplique‑as em uma pasta de trabalho de resumo.
* **Detecção dinâmica de intervalo:** Substitua o valor fixo `"A1:G20"` por código que descubra automaticamente as extensões da tabela dinâmica.
* **Atualização da tabela dinâmica:** Após a cópia, chame `destinationSheet.PivotTables[0].RefreshData();` para garantir que a tabela reflita quaisquer alterações na fonte de dados subjacente.

## Saída esperada

Executar o programa com um `Input.xlsx` válido produz `CopyWithPivot.xlsx`. Ao abrir o arquivo, você verá:

```
Sheet1 (original)          Sheet2 (copy)
+----------------------+   +----------------------+
| Pivot Table: Sales   |   | Pivot Table: Sales   |
| – Region, Product    |   | – Region, Product    |
| – Sum of Amount      |   | – Sum of Amount      |
+----------------------+   +----------------------+
```

Ambas as planilhas exibem layouts de tabela dinâmica idênticos, filtros e campos calculados.

## Conclusão

Agora você sabe como **copiar tabela dinâmica** entre planilhas em C# usando Aspose.Cells. O tutorial abordou o carregamento da pasta de trabalho, a definição de intervalos correspondentes, a execução da cópia e a gravação do resultado — tudo preservando a definição completa da tabela dinâmica. Aplique o mesmo padrão para automatizar relatórios, criar planilhas modelo ou construir ferramentas de migração de dados.

**Próximos passos:**  
* Explore as variações de **como copiar tabela dinâmica** para múltiplas tabelas em uma única planilha.  
* Combine esta técnica com scripts de automação **carregar pasta de trabalho Excel C#** para processar lotes de arquivos.  
* Experimente o método **copiar intervalo para planilha** em gráficos, tabelas e formatações condicionais para uma solução completa de clonagem de pasta de trabalho.  

Feliz codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}