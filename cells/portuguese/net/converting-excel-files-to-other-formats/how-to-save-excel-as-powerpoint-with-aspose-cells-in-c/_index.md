---
category: general
date: 2026-11-16
description: Aprenda como salvar o Excel como PowerPoint e converter o Excel para
  PowerPoint programaticamente. Este guia passo a passo também aborda a exportação
  do Excel para PPTX e a gravação de uma pasta de trabalho como PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: pt
lastmod: 2026-11-16
og_description: Salve o Excel como PowerPoint usando Aspose.Cells. Siga este guia
  para converter Excel em PowerPoint, exportar Excel para PPTX e salvar a pasta de
  trabalho como PPTX em minutos.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Salvar Excel como PowerPoint – Guia completo de C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Como salvar Excel como PowerPoint com Aspose.Cells em C#
url: /pt/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar Excel como PowerPoint com Aspose.Cells em C#

Se você precisa **salvar Excel como PowerPoint** programaticamente, este tutorial oferece uma solução completa e pronta‑para‑executar. Seja construindo um mecanismo de relatórios ou um gerador automático de slides, as etapas abaixo permitem converter uma planilha do Excel em um slide PPTX editável em apenas algumas linhas de código.

Você aprenderá como **converter Excel para PowerPoint**, exportar a planilha para um arquivo PPTX e manter caixas de texto e formas editáveis – tudo sem sair do ambiente .NET.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7.2+)
* Uma licença válida do Aspose.Cells (a avaliação gratuita funciona para testes)
* Visual Studio 2022 (ou qualquer IDE C#)
* Uma pasta de trabalho Excel que contenha os dados e as formas que você deseja exportar

## Etapa 1: Instalar Aspose.Cells

Adicione o pacote NuGet Aspose.Cells ao seu projeto:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Use a flag `-v` para direcionar uma versão específica, por exemplo, `Aspose.Cells.24.5`.

## Etapa 2: Carregar a pasta de trabalho que você deseja exportar

A primeira operação no fluxo de **salvar Excel como PowerPoint** é carregar a pasta de trabalho fonte.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Por que isso importa:* Carregar a pasta de trabalho lhe dá acesso às suas planilhas, configuração de página e objetos de desenho que se tornarão formas editáveis do PowerPoint.

## Etapa 3: Configurar opções de exportação para um slide PPTX editável

Para **converter Excel para PowerPoint** preservando a editabilidade, você deve definir algumas propriedades em `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Explicação:*  
* `SaveFormat = SaveFormat.Pptx` indica ao Aspose.Cells que deve gerar um arquivo PowerPoint.  
* `ExportEditableText` e `ExportEditableShapes` garantem que o slide resultante se comporte como um slide nativo do PowerPoint – você pode clicar em uma caixa de texto ou forma e editá‑la diretamente no PowerPoint.

## Etapa 4: Definir a área de exportação e ajustá‑la a um único slide

Ao **exportar Excel para PPTX**, geralmente você deseja que um intervalo específico apareça no slide. Definir a área de impressão e as opções de ajuste garante uma saída limpa de um único slide.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Por que isso importa:* O `PrintArea` limita a exportação às células A1 até G30, enquanto `FitToPagesTall` e `FitToPagesWide` comprimem tudo em um slide, evitando páginas extras indesejadas.

## Etapa 5: Salvar a planilha como um arquivo PPTX editável

Agora você pode finalmente **salvar a pasta de trabalho como PPTX** e concluir o processo de **salvar Excel como PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Depois de executar o programa, abra `EditableShapes.pptx` no Microsoft PowerPoint. Você verá um slide que espelha o intervalo Excel selecionado, e todas as caixas de texto e formas estão totalmente editáveis.

### Saída esperada

* Um arquivo chamado `EditableShapes.pptx` localizado em `C:\Output\`.
* Um slide PowerPoint contendo o intervalo A1:G30.
* Caixas de texto, gráficos e formas que você pode clicar duas vezes e editar diretamente no PowerPoint.

## Código‑fonte completo (pronto para copiar)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Perguntas frequentes e tratamento de casos‑limite

| Pergunta | Resposta |
|----------|----------|
| **E se eu tiver várias planilhas?** | Percorra `workbook.Worksheets` e repita as etapas 3‑5 para cada planilha, alterando o nome do arquivo de saída (por exemplo, `Sheet1.pptx`, `Sheet2.pptx`). |
| **Posso exportar toda a pasta de trabalho para um único deck PowerPoint?** | Sim. Defina `ExportAllSheets = true` em `ImageOrPrintOptions`. Cada planilha se torna um slide separado. |
| **Minhas formas aparecem como imagens, não como objetos editáveis.** | Certifique‑se de que `ExportEditableShapes = true` e de que está usando Aspose.Cells 24.5+ (versões anteriores não possuem esse recurso). |
| **O PPTX gerado está muito grande.** | Reduza a área de impressão ou diminua a resolução da imagem via `exportOptions.ImageResolution`. |
| **Preciso de licença para uso em produção?** | Uma licença paga remove a marca d'água de avaliação e desbloqueia desempenho total. A avaliação gratuita funciona para testes. |

## Dicas para código de produção robusto

* **Valide caminhos de arquivo** antes de chamar `Workbook` ou `Save` para evitar `FileNotFoundException`.  
* **Envolva a exportação em um bloco try/catch** para tratar erros de licença (`Aspose.Cells.LicenseException`).  
* **Libere a pasta de trabalho** (`workbook.Dispose()`) ao terminar para liberar recursos não gerenciados.  
* **Use I/O assíncrono** (`FileStream` com `await`) se estiver exportando muitas planilhas grandes em um serviço web.

## Próximos passos

Agora que você sabe como **salvar Excel como PowerPoint**, pode explorar tópicos relacionados:

* **Exportar Excel para PPTX com layouts de slide personalizados** – ajuste `SlideSize` e adicione um slide mestre.  
* **Converter slide Excel para PDF** – use `SaveFormat.Pdf` para uma versão imprimível.  
* **Conversão em lote de uma pasta de workbooks** – combine o loop mostrado acima com `Directory.GetFiles`.  

Experimente diferentes áreas de impressão, opções de escala e temas do PowerPoint para adaptar a saída à identidade visual da sua organização.

---

*Feliz codificação! Se este guia ajudou você a **converter Excel para PowerPoint**, sinta‑se à vontade para compartilhá‑lo com colegas ou abrir uma issue no repositório Aspose.Cells no GitHub para mais assistência.*

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to save Excel as PowerPoint using C# and Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [How to Save PPTX from Excel – Complete Guide to Export Excel Sheet PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Convert Excel to PowerPoint – Full Step‑by‑Step Guide](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}