---
category: general
date: 2026-08-07
description: Remova o autofiltro do Excel em C# rapidamente. Aprenda como desativar
  o filtro do Excel, excluir o filtro da tabela do Excel e limpar o autofiltro da
  tabela do Excel com Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- how to turn off excel filter
- delete excel table filter
- clear excel table autofilter
language: pt
lastmod: 2026-08-07
og_description: Remova o autofiltro do Excel em C# e veja como desativar o filtro
  do Excel, excluir o filtro da tabela do Excel e limpar o autofiltro da tabela do
  Excel usando Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet after remove autofilter from excel
og_title: Remover autofiltro do Excel em C# – tutorial passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  headline: Remove autofilter from Excel in C# – complete guide
  type: TechArticle
- description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  name: Remove autofilter from Excel in C# – complete guide
  steps:
  - name: Expected output
    text: 'Open `output.xlsx` in Excel:'
  - name: Multiple tables in the same worksheet
    text: 'If the worksheet contains more than one table, iterate over the collection:'
  - name: Removing filter from a specific column only
    text: 'Aspose.Cells does not expose a column‑level `AutoFilter` removal, but you
      can recreate the table without the filter:'
  - name: Working with older Excel formats (*.xls)
    text: Aspose.Cells supports the legacy binary format automatically. The same code
      works; just ensure the file extension matches the input file.
  - name: Handling large workbooks
    text: For files larger than 100 MB, enable the **LoadOptions** to use the **MemoryOptimized**
      mode, which reduces memory pressure while still allowing table manipulation.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Remover autofiltro do Excel em C# – guia completo
url: /pt/net/excel-autofilter-validation/remove-autofilter-from-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Remover autofiltro do Excel – guia completo

Se você precisa **remover autofiltro do Excel** ao processar arquivos programaticamente, este guia mostra exatamente como fazer. Você aprenderá a maneira mais rápida de desativar o filtro do Excel, excluir o filtro da tabela do Excel e limpar o autofiltro da tabela do Excel usando a biblioteca Aspose.Cells.

O tutorial cobre tudo, desde a configuração do projeto até a verificação de que a pasta de trabalho de saída não exibe mais setas de filtro. Nenhum passo manual é necessário, e o código funciona com qualquer arquivo .xlsx que contenha uma tabela com um AutoFilter.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou superior instalado  
- Visual Studio 2022 (ou qualquer IDE C#)  
- Uma licença para **Aspose.Cells for .NET** (a avaliação gratuita funciona para testes)  
- Um arquivo Excel (`input.xlsx`) que contenha ao menos uma tabela com um AutoFilter aplicado  

Você também precisará adicionar o pacote NuGet Aspose.Cells ao seu projeto:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Mantenha a pasta de trabalho em um diretório que sua aplicação possa ler/gravar sem elevação para evitar `UnauthorizedAccessException`.

![remover autofiltro do excel](/assets/remove-autofilter.png "remover autofiltro do excel – planilha do Excel sem setas de filtro")

## Remover autofiltro do Excel – passo 1: carregar a pasta de trabalho

A primeira operação é abrir a pasta de trabalho de origem. Carregar o arquivo na memória lhe dá acesso total às planilhas, tabelas e suas propriedades.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook containing a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Por que isso importa:* `Workbook` é o objeto central no Aspose.Cells. Ele analisa o pacote XLSX e constrói um modelo de objetos que espelha a estrutura interna do Excel, permitindo que você manipule tabelas diretamente.

## Como desativar o filtro do Excel – passo 2: acessar a planilha de destino

Arquivos Excel podem ter várias planilhas, mas o exemplo foca na primeira. Ajuste o índice se seus dados estiverem em outra planilha.

```csharp
// Step 2: Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Por que isso importa:* Cada `Worksheet` contém sua própria coleção de tabelas. Ao recuperar a planilha correta, você garante que modificará a tabela pretendida.

## Excluir filtro da tabela Excel – passo 3: localizar a primeira tabela

As tabelas são armazenadas na coleção `Tables` de uma planilha. Você pode iterar sobre elas, mas, para simplificar, pegamos a primeira tabela.

```csharp
// Step 3: Retrieve the first table on the worksheet
Table table = worksheet.Tables[0];
```

*Por que isso importa:* O objeto `Table` possui a propriedade `AutoFilter` que controla a interface de filtro. Acessar a tabela é pré‑requisito para remover o filtro.

## Limpar autofiltro da tabela Excel – passo 4: remover o AutoFilter

Definir a propriedade `AutoFilter` como `null` remove completamente a interface de filtro. Os dados subjacentes permanecem inalterados.

```csharp
// Step 4: Remove the AutoFilter by setting it to null
table.AutoFilter = null;
```

*Por que isso importa:* Quando `AutoFilter` é `null`, o Excel não exibe mais as setas suspensas, e quaisquer critérios de filtro aplicados anteriormente são limpos. Esta é a operação central para **excluir filtro da tabela Excel**.

## Salvar a pasta de trabalho – passo 5: verificar o resultado

Por fim, grave a pasta de trabalho modificada no disco. O arquivo salvo abrirá no Excel sem setas de filtro.

```csharp
// Step 5: Save the workbook; the table is now a plain data table without filter UI
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

### Saída esperada

Abra `output.xlsx` no Excel:

- A tabela aparece como dados comuns — nenhuma seta de filtro aparece na linha de cabeçalho.  
- Todas as linhas estão visíveis, confirmando que o filtro foi removido.  

Se ainda vir setas, verifique novamente se o arquivo de origem realmente continha um AutoFilter e se você direcionou o índice da tabela correto.

## Variações comuns e casos de borda

### Múltiplas tabelas na mesma planilha

Se a planilha contiver mais de uma tabela, itere sobre a coleção:

```csharp
foreach (Table tbl in worksheet.Tables)
{
    tbl.AutoFilter = null; // clear filter for each table
}
```

### Remover filtro de uma coluna específica apenas

Aspose.Cells não expõe a remoção de `AutoFilter` a nível de coluna, mas você pode recriar a tabela sem o filtro:

```csharp
// Capture existing data range
CellArea range = table.DisplayRange;

// Remove the table (including filter)
worksheet.Tables.RemoveAt(table.Index);

// Re‑add the table without AutoFilter
Table newTable = worksheet.Tables[worksheet.Tables.Add(range.StartRow, range.StartColumn, range.EndRow, range.EndColumn, true)];
```

### Trabalhando com formatos Excel mais antigos (*.xls)

Aspose.Cells suporta automaticamente o formato binário legado. O mesmo código funciona; apenas certifique‑se de que a extensão do arquivo corresponde ao arquivo de entrada.

### Manipulando pastas de trabalho grandes

Para arquivos maiores que 100 MB, habilite as **LoadOptions** para usar o modo **MemoryOptimized**, que reduz a pressão de memória enquanto ainda permite a manipulação de tabelas.

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { MemoryOptimization = true };
Workbook largeWorkbook = new Workbook("large_input.xlsx", options);
```

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar, colar e executar como uma aplicação console.

```csharp
using System;
using Aspose.Cells;

namespace RemoveExcelAutoFilter
{
    class Program
    {
        static void Main()
        {
            // Define file paths
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";

            // Load the workbook
            Workbook workbook = new Workbook(inputPath);

            // Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Ensure the worksheet contains at least one table
            if (worksheet.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }

            // Retrieve the first table and clear its AutoFilter
            Table table = worksheet.Tables[0];
            table.AutoFilter = null;

            // Save the modified workbook
            workbook.Save(outputPath);

            Console.WriteLine($"AutoFilter removed. Saved to {outputPath}");
        }
    }
}
```

Execute o programa e, em seguida, abra `output.xlsx`. Você verá que a operação **remover autofiltro do excel** foi bem‑sucedida e a planilha mostra uma tabela de dados simples.

## Conclusão

Agora você sabe como **remover autofiltro do Excel** usando C#. Ao carregar a pasta de trabalho, acessar a tabela alvo e definir `AutoFilter` como `null`, você pode **desativar o filtro do Excel**, **excluir filtro da tabela Excel** e **limpar autofiltro da tabela Excel** em um único passo confiável.  

Em seguida, considere explorar tópicos relacionados, como **formatar tabelas Excel com Aspose.Cells**, **exportar dados filtrados para CSV** ou **aplicar formatação condicional programaticamente**. Cada um desses se baseia no mesmo modelo de objetos que você acabou de dominar.

Sinta‑se à vontade para experimentar com múltiplas tabelas, pastas de trabalho grandes ou diferentes formatos de arquivo — sua nova habilidade tornará a automação do Excel mais fluida e previsível. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Limpar interface de filtro no Excel com C# – Remover botão AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Como implementar AutoFilter no Excel usando Aspose.Cells for .NET (Guia de Análise de Dados)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Como implementar Autofilter 'EndsWith' no Excel usando Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}