---
category: general
date: 2026-09-18
description: Crie PowerPoint a partir do Excel com Aspose.Cells – copie tabelas dinâmicas,
  exporte intervalos e salve como PPTX em poucas linhas de código C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: pt
lastmod: 2026-09-18
og_description: Crie PowerPoint a partir do Excel rapidamente. Aprenda como copiar
  tabelas dinâmicas, exportar intervalos e salvar uma pasta de trabalho como PPTX
  usando o Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Crie PowerPoint a partir do Excel com Aspose.Cells – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Como criar PowerPoint a partir do Excel usando Aspose.Cells
url: /pt/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar PowerPoint a partir do Excel usando Aspose.Cells

Se você precisa criar PowerPoint a partir do Excel, este guia mostra uma solução concisa e completa. Você verá como copiar uma tabela dinâmica, exportar um intervalo selecionado e salvar o resultado como um arquivo PPTX com apenas algumas linhas de C#.

Gerar um conjunto de slides diretamente a partir dos dados da planilha elimina a etapa manual de copiar‑colar que desacelera os fluxos de trabalho de relatórios. O tutorial cobre tudo o que você precisa, desde a configuração do projeto até o arquivo PPTX final, e funciona com a versão mais recente do Aspose.Cells para .NET.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* **Aspose.Cells for .NET** (versão 23.12 ou mais recente). Instale via NuGet: `Install-Package Aspose.Cells`.
* Um ambiente de desenvolvimento **.NET 6+** (Visual Studio 2022 ou VS Code funciona).
* Uma pasta de trabalho Excel (`Source.xlsx`) que contém os dados e a tabela dinâmica que você deseja reutilizar.
* Permissão de gravação na pasta de saída.

Nenhuma biblioteca de terceiros adicional é necessária.

## Criar PowerPoint a partir do Excel – passo a passo

O processo consiste em quatro etapas lógicas que correspondem diretamente ao exemplo de código que você verá a seguir.

### Etapa 1: Carregar a pasta de trabalho de origem e definir o intervalo

Você deve carregar a pasta de trabalho que contém os dados de origem e a tabela dinâmica. Selecionar um intervalo preciso garante que apenas as células necessárias sejam transferidas, mantendo o slide resultante leve.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Por que isso importa:**  
`CreateRange` cria um objeto `Range` que pode ser copiado como um todo. Ao limitar o intervalo a `A1:G20`, você evita trazer células não relacionadas, o que poderia inflar o arquivo PowerPoint.

### Etapa 2: Preparar a pasta de trabalho de destino

Aspose.Cells trata um slide do PowerPoint como uma pasta de trabalho quando você o salva no formato PPTX. Criar uma nova pasta de trabalho fornece uma tela limpa para o intervalo copiado.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Dica:** Se precisar de vários slides, você pode adicionar planilhas adicionais e salvar cada uma como um arquivo PPTX separado.

### Etapa 3: Copiar o intervalo preservando a tabela dinâmica

O método `CopyRange` aceita um objeto `PasteOptions`. Definir `CopyPivotTables = true` indica ao Aspose.Cells que mantenha a estrutura da tabela dinâmica intacta, não apenas os valores renderizados.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Como funciona:**  
Quando `CopyPivotTables` está true, a planilha de destino recebe tanto os dados de origem quanto o cache da tabela dinâmica. Isso significa que a tabela dinâmica permanece totalmente funcional e pode ser atualizada posteriormente se os dados de origem mudarem.

### Etapa 4: Salvar a pasta de trabalho como arquivo PowerPoint

Por fim, exporte a pasta de trabalho para o formato PPTX. O sinalizador `SaveFormat.Pptx` indica ao Aspose.Cells que escreva a planilha como um slide do PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Resultado:**  
`CopyWithPivot.pptx` abre no Microsoft PowerPoint (ou em qualquer visualizador compatível) com um único slide que exibe o intervalo copiado, incluindo uma tabela dinâmica ativa que pode ser manipulada no PowerPoint.

## Exemplo completo executável

Abaixo está o programa completo que você pode colar em um novo projeto de console e executar imediatamente.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Saída esperada:**  
Ao executar o programa, ele imprime “PowerPoint file created successfully.” e produz um arquivo chamado `CopyWithPivot.pptx`. Abrir o arquivo no PowerPoint mostra um único slide onde o intervalo Excel copiado aparece exatamente como na planilha de origem, com uma tabela dinâmica ativa que pode ser atualizada a partir do PowerPoint.

## Variações comuns e casos de borda

| Situação | O que mudar |
|-----------|----------------|
| **Múltiplas tabelas dinâmicas** | Defina objetos `Range` separados para cada tabela e chame `CopyRange` para cada um, ou copie a planilha inteira se elas compartilharem a mesma fonte de dados. |
| **Conjuntos de dados grandes** | Aumente o intervalo (por exemplo, `"A1:Z5000"`). Considere habilitar `PasteOptions.CompressData = true` para reduzir o tamanho do PPTX. |
| **Layouts de slide diferentes** | Após salvar como PPTX, abra o arquivo no PowerPoint e aplique um layout ou tema personalizado; os dados permanecem editáveis. |
| **Salvar em um stream** | Use `destinationWorkbook.Save(stream, SaveFormat.Pptx)` quando precisar retornar o PPTX via uma API web. |
| **Preservar formatação de células** | Defina `PasteOptions.PasteType = PasteType.All` para manter fontes, cores e bordas. |

**Dica profissional:** Sempre verifique se a pasta de destino existe antes de chamar `Save`. Se a pasta estiver ausente, `Save` lança uma `DirectoryNotFoundException`.

## Conclusão

Agora você sabe como criar PowerPoint a partir do Excel, copiar uma tabela dinâmica e exportar o resultado como um arquivo PPTX usando Aspose.Cells. As etapas — carregar a pasta de trabalho de origem, definir um intervalo, copiar com `CopyPivotTables` e salvar como PPTX — cobrem todo o fluxo de trabalho de forma confiável e pronta para produção.

Em seguida, explore **como exportar Excel para PPTX** para várias planilhas, ou aprenda **como copiar intervalos entre pastas de trabalho** quando precisar mesclar dados de várias fontes antes de gerar o conjunto de slides. Ambos os tópicos se baseiam na mesma superfície de API e podem ser combinados para automatizar pipelines de relatórios complexos.

Bom desenvolvimento e aproveite para transformar suas planilhas em apresentações polidas!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}