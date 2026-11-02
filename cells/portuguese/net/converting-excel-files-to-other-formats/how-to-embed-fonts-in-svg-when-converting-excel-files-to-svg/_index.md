---
category: general
date: 2026-09-15
description: Aprenda como incorporar fontes em SVG e exportar gráficos do Excel para
  PowerPoint, abordando a conversão de XLSX para SVG e a conversão de XLSX para PPTX
  com exemplos de código completos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: pt
lastmod: 2026-09-15
og_description: Incorpore fontes em SVG e exporte gráficos do Excel para PowerPoint
  com código C# passo a passo. Converta XLSX para SVG e XLSX para PPTX de forma rápida
  e confiável.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Incorpore fontes em SVG e exporte gráficos do Excel para PowerPoint – guia
  completo
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como incorporar fontes em SVG ao converter arquivos Excel para SVG e PowerPoint
url: /pt/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como incorporar fontes em SVG ao converter arquivos Excel para SVG e PowerPoint  

Se você precisa **incorporar fontes em SVG** ao converter uma pasta de trabalho Excel, este guia mostra exatamente como fazer isso. Você também aprenderá como **exportar gráfico do Excel para PowerPoint** e como **converter XLSX para SVG** e **converter XLSX para PPTX** com gráficos editáveis.  

Trabalhar com dados do Excel programaticamente costuma significar mover o mesmo conteúdo visual entre diferentes formatos de arquivo. Recriar manualmente um gráfico no PowerPoint ou reaplicar fontes em um SVG é propenso a erros e consome tempo. Ao final deste tutorial você terá um trecho de código C# único e reutilizável que:

* Salva uma pasta de trabalho como arquivo SVG com fontes incorporadas e seletores de variação de fonte.  
* Exporta a mesma pasta de trabalho para um arquivo PPTX onde o gráfico permanece editável.  

O único pré‑requisito é uma versão recente do **Aspose.Cells for .NET** (2024‑x ou posterior) e um ambiente de desenvolvimento .NET como o Visual Studio 2022.

---

## O que você precisará  

* .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.8).  
* Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Um arquivo Excel (`input.xlsx`) que contenha ao menos um gráfico.  
* Permissão de gravação no diretório de saída.  

---

## Incorporar fontes em SVG ao converter XLSX para SVG  

Incorporar fontes garante que o SVG seja renderizado corretamente em qualquer dispositivo, mesmo que o sistema de destino não possua as tipografias originais. A classe `SvgSaveOptions` fornece duas flags que tornam isso possível: `EmbedFonts` e `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Por que isso funciona:**  
* `EmbedFonts = true` copia os arquivos de fonte para a seção `<defs>` do SVG, eliminando dependências externas.  
* `FontVariationSelectors = true` adiciona os seletores necessários para fontes que suportam recursos OpenType, preservando variações de glifos como ligaduras.  

**Resultado esperado:** Abra `WithFonts.svg` em qualquer navegador moderno; o texto dentro do gráfico ou das células aparecerá com a tipografia exata usada no Excel, mesmo em máquinas que não tenham essa fonte instalada.

---

## Exportar gráfico do Excel para PowerPoint com gráficos editáveis  

Quando você precisa incorporar um gráfico em um slide do PowerPoint, mas ainda permitir que o destinatário edite os dados do gráfico, o `PptxSaveOptions` do Aspose.Cells oferece a flag `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Por que isso importa:**  
Definir `ExportEditableChart` como `true` armazena o gráfico como um objeto de gráfico Office Open XML em vez de uma imagem estática. Ao abrir `EditableChart.pptx` no PowerPoint, você pode clicar com o botão direito no gráfico → **Edit Data** e modificar as séries como em um gráfico nativo do PowerPoint.

**Etapas de verificação:**  

1. Abra `EditableChart.pptx` no PowerPoint.  
2. Localize o slide que contém o gráfico.  
3. Escolha **Chart Tools → Design → Edit Data**.  
4. Confirme que a grade de dados no estilo Excel aparece e que você pode alterar os valores.

---

## Converter XLSX para SVG – resumo do fluxo completo  

Abaixo está uma versão compacta que combina carregamento, manipulação opcional de dados e salvamento como SVG. Use-a quando precisar apenas da saída SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Chame o método assim:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Dica para casos extremos:** Se sua pasta de trabalho contém fontes personalizadas que não estão instaladas no servidor, incorpore‑as manualmente antes de chamar `Save`. Use `FontInfoCollection` para adicionar os arquivos de fonte ao `SvgSaveOptions` via propriedade `CustomFonts` (disponível nas versões mais recentes do Aspose.Cells).

---

## Converter XLSX para PPTX – preservando a editabilidade do gráfico  

O método auxiliar a seguir demonstra o caminho **convert XLSX to PPTX** garantindo que o gráfico permaneça editável.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Uso:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Pergunta comum:** *E se minha pasta de trabalho tiver várias planilhas com gráficos?*  
**Resposta:** O Aspose.Cells exporta a primeira planilha por padrão. Para incluir planilhas adicionais, itere sobre `workbook.Worksheets`, copie cada gráfico para um novo slide e salve cada slide individualmente usando objetos `Presentation` do Aspose.Slides. Esse cenário avançado vai além do fluxo básico “salvar pasta de trabalho como SVG” e “exportar gráfico do Excel para PowerPoint”, mas as flags principais permanecem as mesmas.

---

## Dicas práticas e armadilhas  

* **Desempenho:** Incorporar fontes aumenta o tamanho do arquivo SVG. Se o tamanho for uma preocupação, defina `EmbedFonts = false` e confie em fontes web‑seguras.  
* **Licenciamento de fontes:** Certifique‑se de que você tem o direito de incorporar as fontes que usa; algumas fontes comerciais restringem a incorporação.  
* **Compatibilidade de gráficos:** Gráficos editáveis são salvos como partes `chart.xml` dentro do PPTX. Gráficos muito complexos (por exemplo, 3‑D ou combinados) podem perder parte da formatação ao serem editados no PowerPoint. Teste os tipos de gráfico mais comuns que você precisa.  
* **Descompasso de versões:** A flag `ExportEditableChart` requer Aspose.Cells 20.10 ou posterior. Usar uma versão mais antiga reverterá silenciosamente para uma imagem rasterizada.  
* **Segurança de threads:** Objetos `Workbook` não são thread‑safe. Crie uma nova instância de `Workbook` por requisição em cenários de serviço web.  

---

## Exemplo completo de ponta a ponta  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Executar este programa gera dois arquivos:

* **WithFonts.svg** – um SVG que renderiza exatamente como a visualização do Excel, com fontes incluídas.  
* **EditableChart.pptx** – uma apresentação PowerPoint onde o gráfico pode ser editado diretamente.

---

## Conclusão  

Agora você sabe como **incorporar fontes em SVG** ao **converter XLSX para SVG**, e como **exportar gráfico do Excel para PowerPoint** mantendo o gráfico editável. O mesmo código também demonstra uma forma limpa de **salvar pasta de trabalho como SVG** e **converter XLSX para PPTX** com esforço mínimo.  

A partir daqui, você pode explorar tópicos adicionais como:

* Adicionar fontes personalizadas programaticamente (`svgOptions.CustomFonts`).  
* Processamento em lote de várias pastas de trabalho em um serviço em segundo plano.  
* Usar Aspose.Slides para criar arquivos PPTX multi‑slide que combinam vários gráficos do Excel.  

Experimente as opções, adapte os trechos ao seu projeto e aproveite conversões confiáveis de Excel‑para‑SVG/PPTX sem pós‑processamento manual. Feliz codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}