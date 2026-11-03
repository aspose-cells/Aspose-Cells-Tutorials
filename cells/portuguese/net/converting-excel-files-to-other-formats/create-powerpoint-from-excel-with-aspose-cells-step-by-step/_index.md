---
category: general
date: 2026-10-01
description: Crie PowerPoint a partir do Excel usando Aspose.Cells em C#. Exporte
  Excel para PowerPoint e converta XLSX para PPTX rapidamente com um exemplo de código
  completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: pt
lastmod: 2026-10-01
og_description: Crie PowerPoint a partir do Excel usando Aspose.Cells em C#. Aprenda
  a exportar Excel para PowerPoint e converter XLSX para PPTX em poucas linhas de
  código.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Criar PowerPoint a partir do Excel com Aspose.Cells – guia rápido
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Criar PowerPoint a partir do Excel com Aspose.Cells – guia passo a passo
url: /pt/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PowerPoint a partir do Excel com Aspose.Cells – guia passo a passo

Se você precisa **criar PowerPoint a partir do Excel**, este tutorial mostra como fazer isso com Aspose.Cells para .NET. Você aprenderá a **exportar Excel para PowerPoint**, converter uma planilha XLSX em uma apresentação PPTX e personalizar os slides resultantes sem sair do seu projeto C#.

O guia cobre tudo o que você precisa para executar o código no .NET 6 ou posterior, incluindo configuração do projeto, pacotes NuGet necessários e um exemplo completo e executável. Ao final, você terá um arquivo PowerPoint que contém o gráfico original do Excel exatamente como aparece na planilha.

## O que você precisará

| Pré-requisito | Motivo |
|---|---|
| .NET 6 SDK ou mais recente | Fornece o runtime para o aplicativo console C# |
| Visual Studio 2022 (ou qualquer IDE) | Permite a criação fácil do projeto e depuração |
| Pacote NuGet Aspose.Cells para .NET | Disponibiliza a classe `Workbook` e as APIs de exportação |
| Um arquivo Excel (`.xlsx`) que contenha ao menos um gráfico | Dados de origem para o slide do PowerPoint |

> **Dica profissional:** Aspose.Cells funciona no Windows, Linux e macOS, então você pode executar o mesmo código em contêineres Docker ou pipelines de CI.

## Etapa 1: Crie um novo projeto console e adicione Aspose.Cells

Abra um terminal (ou o Console do Gerenciador de Pacotes do Visual Studio) e execute:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

O comando `dotnet add package` baixa a versão estável mais recente do **Aspose.Cells**, que inclui o método `ExportPptx` usado mais adiante.

## Etapa 2: Adicione a planilha Excel de origem

Coloque o arquivo Excel que você deseja converter na pasta do projeto. Para este tutorial usamos `ChartOle.xlsx`, que contém um único gráfico na primeira planilha.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Etapa 3: Escreva o código que **cria PowerPoint a partir do Excel**

Abra `Program.cs` e substitua seu conteúdo pelo código a seguir. O exemplo demonstra a operação de **exportação principal** e também mostra como lidar com casos comuns, como arquivos ausentes e tipos de gráfico não suportados.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Por que isso funciona

* `Workbook` lê todo o arquivo Excel, incluindo gráficos incorporados, tabelas e formatação.  
* `ExportPptx` converte a planilha ativa em um conjunto de slides PPTX. O método transforma automaticamente os gráficos do Excel em formas do PowerPoint, preservando a fidelidade visual.  
* O código envolve a operação em um bloco `try/catch` para expor erros, como falhas ao **converter XLSX para PPTX** causadas por arquivos corrompidos.

## Etapa 4: Execute o programa e verifique a saída

Execute a aplicação:

```bash
dotnet run
```

Você deverá ver a mensagem no console:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Abra `Exported.pptx` no Microsoft PowerPoint ou em qualquer visualizador compatível. O primeiro slide exibe o gráfico exatamente como aparecia em `ChartOle.xlsx`. Isso confirma que você gerou com sucesso **PowerPoint a partir do Excel**.

## Etapa 5: Avançado – exportando várias planilhas ou layouts de slide personalizados

O exemplo básico exporta apenas a primeira planilha. Em cenários reais você pode precisar:

* **Exportar várias planilhas** em slides separados.  
* **Controlar o tamanho do slide** ou adicionar um placeholder de título.  
* **Incluir planilhas ocultas** na conversão.  

Abaixo está um trecho conciso que itera sobre todas as planilhas e adiciona cada uma como um slide separado:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Observação:** O trecho avançado requer a biblioteca **Aspose.Slides for .NET**. Se você precisar apenas da conversão simples de uma planilha, a chamada `ExportPptx` anterior é suficiente.

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Correção |
|---|---|---|
| Slide em branco após a exportação | A planilha não contém objetos visíveis | Garanta que haja ao menos um gráfico, tabela ou forma antes de chamar `ExportPptx`. |
| Fontes ausentes no PowerPoint | Fonte não instalada na máquina onde o PPTX é aberto | Incorpore as fontes necessárias na planilha Excel ou instale‑as no sistema de destino. |
| Escala inesperada | Gráfico grande excede as dimensões do slide | Ajuste a propriedade `PageSetup.Zoom` da planilha antes da exportação. |
| `convert XLSX to PPTX` lança `NotSupportedException` | Tipo de gráfico não suportado pelo Aspose.Cells (ex.: mapas 3‑D) | Substitua o gráfico por um tipo suportado ou exporte a planilha como imagem primeiro. |

Tratar esses casos garante um fluxo de **exportação de Excel para PowerPoint** confiável em ambientes de produção.

## Conclusão

Agora você sabe como **criar PowerPoint a partir do Excel** usando Aspose.Cells para .NET. O tutorial abordou:

* Configuração do projeto e instalação do NuGet  
* Carregamento de uma planilha Excel e chamada ao `ExportPptx`  
* Execução do código e confirmação do PPTX gerado  
* Extensão da solução para lidar com múltiplas planilhas e layouts personalizados  
* Dicas práticas para evitar problemas comuns de conversão  

Com esse conhecimento você pode automatizar a geração de relatórios, criar pipelines de apresentação ou integrar a conversão de Excel para PowerPoint em qualquer aplicação C#. Experimente diferentes tipos de gráfico, adicione títulos aos slides ou combine a exportação com Aspose.Slides para criação completa de apresentações.

--- 

*Pronto para explorar mais? Confira tópicos relacionados como **converter Excel para PDF**, **incorporar dados do Excel no Word** ou **usar Aspose.Slides para editar arquivos PPTX programaticamente**.*

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Converter Excel para PowerPoint Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Converter Excel para PowerPoint Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Converter Excel para PowerPoint Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}