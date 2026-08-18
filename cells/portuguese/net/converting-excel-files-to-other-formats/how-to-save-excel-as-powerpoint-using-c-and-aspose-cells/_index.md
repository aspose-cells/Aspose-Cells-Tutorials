---
category: general
date: 2026-08-17
description: Salvar Excel como PowerPoint com C# – guia passo a passo para converter
  arquivos XLSX, tornar caixas de texto editáveis e gerar saída PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: pt
lastmod: 2026-08-17
og_description: Salve Excel como PowerPoint em C# com um exemplo completo de código.
  Aprenda como converter XLSX, tornar caixas de texto editáveis e exportar para PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Salvar Excel como PowerPoint em C# – guia completo de conversão
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Como salvar Excel como PowerPoint usando C# e Aspose.Cells
url: /pt/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar Excel como PowerPoint usando C# e Aspose.Cells

Se você precisa **salvar Excel como PowerPoint** em um projeto .NET, este guia mostra uma solução completa, pronta‑para‑executar. Você verá como carregar uma pasta de trabalho XLSX, tornar cada caixa de texto na planilha editável e exportar o resultado para um arquivo PPTX — tudo com apenas algumas linhas de C#.

Converter Excel para PowerPoint é uma necessidade comum para dashboards de relatórios, decks de slides ou geração automatizada de apresentações. Este tutorial também aborda **como editar caixas de texto** programaticamente, para que você possa personalizar o conteúdo do slide antes de salvar.

## Pré-requisitos

* SDK .NET 6.0 (ou posterior) instalado  
* Um ambiente de desenvolvimento como Visual Studio 2022 ou VS Code  
* Uma licença Aspose.Cells for .NET (ou uma chave de avaliação gratuita) – faça o download no [site da Aspose](https://products.aspose.com/cells/net/)  
* O arquivo `input.xlsx` que você deseja converter  

> **Dica profissional:** Se você usar a versão de avaliação gratuita, o PPTX de saída conterá uma marca d'água. Uma versão licenciada a remove.

## Etapa 1: Instalar o pacote NuGet Aspose.Cells

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Cells
```

Isso adiciona o assembly `Aspose.Cells`, que fornece as classes `Workbook`, `Worksheet` e `Shape` necessárias para a conversão.

## Etapa 2: Criar a estrutura de um aplicativo console

Crie um novo projeto console (se ainda não tiver um):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Substitua o `Program.cs` gerado pelo código mostrado nas próximas etapas.

## Etapa 3: Carregar a pasta de trabalho e selecionar a primeira planilha

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Por que isso importa:**  
`Workbook` lê o arquivo Excel na memória, enquanto `Worksheet` dá acesso às células, gráficos e formas da planilha. A primeira planilha costuma ser o relatório padrão que você deseja apresentar.

## Etapa 4: Tornar cada caixa de texto na planilha editável

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Por que você precisa disso:**  
Por padrão, as caixas de texto importadas do Excel são somente‑leitura quando renderizadas no PowerPoint. Definir `IsEditable = true` permite que você (ou usuários posteriores do PowerPoint) modifique o texto diretamente no slide.

## Etapa 5: Salvar a pasta de trabalho como uma apresentação PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**O que acontece nos bastidores:**  
`Workbook.Save` detecta o valor enum `SaveFormat.Pptx` e traduz o layout da planilha Excel — incluindo linhas, colunas, gráficos e as caixas de texto agora editáveis — em objetos de slide do PowerPoint.

## Código-fonte completo (executável)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Saída esperada

Ao executar o programa (`dotnet run`), você deverá ver:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Abrir `output.pptx` no Microsoft PowerPoint exibirá um slide que espelha a planilha Excel original. Todas as caixas de texto podem ser editadas diretamente ao dar um duplo‑clique nelas.

## Perguntas comuns e casos extremos

| Pergunta | Resposta |
|----------|----------|
| **Posso converter uma planilha específica em vez da primeira?** | Sim. Substitua `workbook.Worksheets[0]` por `workbook.Worksheets["SheetName"]` ou qualquer índice que precisar. |
| **E se a pasta de trabalho contiver várias planilhas?** | Chame `workbook.Save` uma vez por planilha, fornecendo um nome de arquivo PPTX distinto para cada, ou combine-as em uma única apresentação usando objetos `Presentation` do Aspose.Slides. |
| **Os gráficos serão preservados?** | Aspose.Cells converte os gráficos do Excel em objetos de gráfico do PowerPoint automaticamente. Nenhum código extra é necessário. |
| **Como alterar o tamanho do slide?** | Após `workbook.Save`, você pode carregar o PPTX gerado com Aspose.Slides e ajustar `Presentation.SlideSize`. |
| **E se eu precisar editar o texto da caixa de texto antes de salvar?** | Acesse `shapeItem.TextBox.Text` dentro do loop, modifique-o, então defina `IsEditable = true`. Exemplo: `shapeItem.TextBox.Text = "New title";` |

## Dicas de solução de problemas

* **“ShapeType.TextBox” não encontrado** – Certifique‑se de que está usando a versão 25.11 ou mais recente do Aspose.Cells; versões anteriores não possuem a propriedade `IsEditable`.  
* **Erros de arquivo não encontrado** – Verifique se `YOUR_DIRECTORY` é um caminho absoluto ou se o caminho relativo aponta para a localização correta.  
* **Licença não aplicada** – Chame `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` antes de carregar a pasta de trabalho para remover as marcas d'água de avaliação.

## Conclusão

Agora você sabe como **salvar Excel como PowerPoint** com C# carregando uma pasta de trabalho XLSX, tornando cada caixa de texto editável e exportando para PPTX. Este método lida com gráficos, imagens e formatação de células automaticamente, fornecendo um deck de slides pronto‑para‑apresentar.

Em seguida, explore tópicos relacionados como **converter Excel para PowerPoint com Aspose.Slides**, **como editar caixas de texto programaticamente após a conversão**, ou **processar em lote múltiplas pastas de trabalho**. Cada um desses se baseia nas etapas principais abordadas aqui e pode automatizar ainda mais seu fluxo de trabalho de relatórios.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como converter Excel para PowerPoint usando Aspose.Cells para .NET: um guia completo](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Como copiar Tabela Dinâmica em C# – Converter Excel para PPTX, copiar intervalo e tornar caixa de texto editável](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Como salvar arquivos Excel em múltiplos formatos usando Aspose.Cells .NET (guia 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}