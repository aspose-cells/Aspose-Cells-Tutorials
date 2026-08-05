---
category: general
date: 2026-08-04
description: Exportar gráfico do Excel para PowerPoint usando Aspose.Cells em C#.
  Siga este guia passo a passo de conversão de Excel para PowerPoint e mantenha as
  formas editáveis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: pt
lastmod: 2026-08-04
og_description: Exportar gráfico do Excel para PowerPoint com Aspose.Cells em C#.
  Aprenda como criar um PPTX editável, preservar os dados do gráfico e automatizar
  a conversão de Excel para PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Exportar gráfico do Excel para PowerPoint com C# – tutorial completo do
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Exportar gráfico do Excel para PowerPoint com C# – guia completo do Aspose.Cells
url: /pt/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico do Excel para PowerPoint com C# – guia completo do Aspose.Cells

Se você precisa **exportar gráfico do Excel para PowerPoint**, este tutorial mostra como fazer isso com Aspose.Cells e Aspose.Slides em C#. Você obterá um PPTX totalmente editável que preserva os dados e formas do gráfico, tornando a conversão pronta para trabalhos de design adicionais.

Exportar gráficos do Excel para PowerPoint é uma necessidade comum ao criar pipelines de relatórios automatizados, apresentações de vendas ou materiais de treinamento. Neste guia você aprenderá os passos exatos para realizar uma **conversão de Excel para PowerPoint** que mantém todos os elementos do gráfico editáveis. Nenhuma cópia‑colagem manual é necessária, e o código funciona com .NET 6+ assim como com o clássico .NET Framework.

## Pré-requisitos

- Uma licença válida do Aspose.Cells (ou uma chave de avaliação gratuita)  
- Aspose.Slides for .NET adicionado ao projeto (a biblioteca trata a saída PPTX)  
- .NET 6 SDK ou posterior instalado  
- Uma pasta de trabalho Excel que contém ao menos um gráfico (para este exemplo usamos `Shapes.xlsx`)  

Você pode instalar os pacotes NuGet com os seguintes comandos:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Etapa 1: Carregar a pasta de trabalho Excel

A primeira operação é abrir a pasta de trabalho que contém o gráfico que você deseja exportar. A classe `Workbook` representa o arquivo Excel completo.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Por que isso importa:** Carregar a pasta de trabalho lhe dá acesso às suas planilhas, gráficos e formatações. Aspose.Cells lê o arquivo sem exigir que o Microsoft Office esteja instalado, o que mantém a solução leve e amigável ao servidor.

## Etapa 2: Selecionar a planilha e definir a área de impressão

Uma planilha pode conter muitos gráficos, mas normalmente você exporta uma região específica. Definir o `PrintArea` indica ao Aspose.Cells quais células (incluindo gráficos) devem ser renderizadas.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Por que isso importa:** Ao restringir a exportação a uma área de impressão definida, você evita slides em branco desnecessários e mantém o tamanho do arquivo PPTX pequeno. A área pode ser ajustada para corresponder ao intervalo exato do seu gráfico.

## Etapa 3: Configurar opções de exportação para um PPTX editável

Aspose.Cells usa a classe `ImageOrPrintOptions` para controlar o formato de saída e a editabilidade. Definir `ImageFormat` como `ImageFormat.Pptx` cria um arquivo PowerPoint, enquanto `ExportEditableShapes = true` preserva os objetos do gráfico como formas editáveis.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Por que isso importa:** O sinalizador `ExportEditableShapes` é a chave para um resultado de **formas editáveis no PowerPoint**. Sem ele, o gráfico seria rasterizado como uma imagem, perdendo a capacidade de modificar pontos de dados ou estilos posteriormente.

## Etapa 4: Salvar a planilha como uma apresentação PowerPoint

Finalmente, invoque o método `Save` no objeto `Workbook`. O enum `SaveFormat.Pptx` indica ao Aspose.Cells que deve gerar um arquivo PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Quando o código terminar, abra `ShapesExport.pptx` no PowerPoint. Você verá um slide que contém o gráfico original do Excel como um objeto de gráfico nativo do PowerPoint. Clique duas vezes no gráfico para editar os dados, mudar cores ou adicionar animações — como se você tivesse criado o gráfico diretamente no PowerPoint.

### Saída esperada

| Nome do arquivo          | Conteúdo no slide                                                                 |
|--------------------------|-----------------------------------------------------------------------------------|
| `ShapesExport.pptx`      | O gráfico de `Shapes.xlsx` renderizado como um gráfico PowerPoint editável, com rótulos de eixo, legendas e séries de dados intactas. |

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar, colar e executar. Ele inclui todas as declarações `using` necessárias, tratamento de erros e comentários.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Explicação de cada bloco**

| Bloco | Propósito |
|-------|-----------|
| `using` directives | Importa os namespaces Aspose.Cells e Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Carrega o arquivo Excel sem precisar do Office instalado. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Limita a exportação à região que contém o gráfico. |
| `ImageOrPrintOptions` | Configura a saída PPTX e habilita **exportação PPTX do Aspose.Cells** com formas editáveis. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Grava o arquivo PowerPoint no disco. |
| `try / catch` | Fornece tratamento básico de erros para arquivos ausentes ou questões de licenciamento. |

Executar este programa produz um slide PowerPoint que você pode abrir no Microsoft PowerPoint, Google Slides (após conversão) ou qualquer visualizador compatível.

## Variações comuns e casos de borda

### Exportando várias planilhas

Se você precisar de um slide para cada planilha, percorra `workbook.Worksheets` e chame `Save` com um nome de arquivo exclusivo para cada iteração.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Controlando o layout do slide

Aspose.Slides permite adicionar um layout de slide personalizado após a exportação. Crie uma nova apresentação, importe o slide gerado e então aplique um tema mestre.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Lidando com gráficos com fontes de dados externas

Se um gráfico referencia um intervalo de dados fora da área de impressão definida, amplie o `PrintArea` para incluir essas células. Caso contrário, o gráfico pode perder séries de dados durante a exportação.

### Considerações de licenciamento

As bibliotecas Aspose funcionam em modo de avaliação com marca d'água. Para remover a marca d'água, defina a licença antes de qualquer chamada de API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Faça o mesmo para Aspose.Slides se você usar seus recursos avançados.

## Dicas profissionais

- **Reuse export options:** Crie uma única instância de `ImageOrPrintOptions` e atribua-a a cada planilha para manter o código DRY.  
- **Batch processing:** Para relatórios em grande escala, combine esta lógica de exportação com um worker em segundo plano ou Azure Function para gerar arquivos PPTX sob demanda.  
- **Performance:** Se você precisar apenas da imagem do gráfico (não editável), defina `ExportEditableShapes = false`. Isso reduz o uso de memória e acelera a conversão.  
- **Testing:** Verifique o PPTX gerado em instalações do PowerPoint tanto no Windows quanto no macOS, pois algumas peculiaridades de renderização diferem entre as plataformas.

## Conclusão

Agora você tem uma solução completa, de ponta a ponta, para **exportar gráfico do Excel para PowerPoint** usando C#. O tutorial abordou o carregamento da pasta de trabalho, a seleção da área de impressão, a configuração da **exportação PPTX do Aspose.Cells** com **formas editáveis no PowerPoint**, e a gravação do resultado como um arquivo PPTX totalmente editável.

A partir daqui, você pode explorar cenários adicionais de **conversão de Excel para PowerPoint**, como exportação em lote, layouts de slide personalizados ou a integração do processo em uma API web. Experimente diferentes tipos de gráficos, adicione imagens ou combine várias planilhas em uma única apresentação para adaptar a saída às necessidades do seu negócio.

Pronto para automatizar seu fluxo de relatórios? Experimente trocar o arquivo de origem, ajustar a área de impressão e integrar o código aos seus serviços .NET existentes. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como converter Excel para PowerPoint usando Aspose.Cells para .NET: Um guia completo](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Como exportar gráficos do Excel para PDF usando Aspose.Cells para .NET: Um guia passo a passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportar células do Excel para imagem usando Aspose.Cells .NET: Um guia passo a passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}