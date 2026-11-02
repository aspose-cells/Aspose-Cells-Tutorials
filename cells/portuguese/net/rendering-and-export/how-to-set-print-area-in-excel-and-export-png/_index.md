---
category: general
date: 2026-09-27
description: Defina a área de impressão no Excel e aprenda como exportar imagens PNG
  das células selecionadas. Este guia também aborda como salvar um intervalo como
  imagem e adicionar uma imagem à planilha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: pt
lastmod: 2026-09-27
og_description: Defina a área de impressão no Excel e exporte PNG com Aspose.Cells.
  Siga este guia passo a passo para salvar o intervalo como imagem e inserir a imagem
  na planilha.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Definir área de impressão no Excel – exportar PNG em C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Como definir a área de impressão no Excel e exportar PNG
url: /pt/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como definir a área de impressão no Excel e exportar PNG

Se você precisar **definir a área de impressão no Excel** antes de criar uma imagem, este guia mostra exatamente como fazer isso. Você também aprenderá **como exportar png** a partir de um intervalo específico, **salvar intervalo como imagem** e **adicionar imagem à planilha** em um fluxo de trabalho único e repetível.

Trabalhar programaticamente com o Excel geralmente significa que você quer apenas um subconjunto de células — por exemplo, uma tabela dinâmica ou um gráfico — para se tornar uma imagem. Ao definir primeiro uma área de impressão, você garante que o PNG exportado contenha exatamente as células esperadas, nem mais nem menos. Este tutorial o conduz por cada passo, desde o carregamento da pasta de trabalho até a gravação do arquivo PNG final, explicando por que cada configuração é importante.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado  
* Visual Studio 2022 (ou qualquer IDE C#)  
* O pacote NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Um arquivo Excel (`input.xlsx`) localizado em um diretório conhecido  

Esses requisitos garantem que o código seja executado sem configurações adicionais.

## Etapa 1: Carregar a pasta de trabalho que você deseja usar

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

A classe `Workbook` representa o arquivo Excel completo. Carregá‑lo primeiro lhe dá acesso às planilhas, células e opções de configuração de página.

## Etapa 2: **Definir a área de impressão no Excel** para o intervalo alvo

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Definir a **área de impressão** informa ao Excel (e ao Aspose.Cells) quais células pertencem à página imprimível. Quando você exportar a planilha como imagem, apenas essa área será renderizada, o que é essencial para um **exportar imagem de células selecionadas** limpo.

## Etapa 3: Configurar as opções de exportação de imagem – **como exportar png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` controla o formato de saída. Ao escolher `ImageFormat.Png`, você garante uma imagem de alta resolução e fundo transparente, que funciona bem em contextos web e desktop.

## Etapa 4: Criar uma imagem a partir do intervalo definido e **adicionar imagem à planilha**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

O método `Pictures.Add` insere uma nova imagem na planilha. Ao passar o intervalo criado na Etapa 2, você **salva o intervalo como imagem** diretamente na planilha, o que é útil caso precise referenciar a imagem em outras partes da pasta de trabalho.

## Etapa 5: **Salvar a imagem como arquivo** – concluindo o fluxo **exportar imagem de células selecionadas**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Chamar `Save` grava a imagem no sistema de arquivos usando as opções definidas na Etapa 3. O arquivo resultante `selected_range.png` contém exatamente as células definidas pelo comando **definir a área de impressão no Excel**.

## Exemplo completo e executável

Juntando todas as partes, você obtém um programa compacto que pode ser inserido em qualquer aplicação console:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Saída esperada

Ao executar o programa, ele exibe:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

E você encontrará um arquivo `selected_range.png` que mostra apenas as células de A1 a G20 do `input.xlsx`.

## Problemas comuns e como evitá‑los

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| A imagem exportada contém a planilha inteira | Nenhuma área de impressão foi definida | Certifique‑se de **definir a área de impressão no Excel** antes de criar a imagem |
| PNG está borrado | DPI padrão é baixo | Defina `imageOptions.DpiX` e `imageOptions.DpiY` para um valor maior (ex.: 300) |
| Erro “arquivo não encontrado” | Caminho do diretório está errado | Use `Path.Combine` ou verifique se a pasta existe |
| A imagem aparece deslocada | Índices de linha/coluna incorretos | Os dois primeiros parâmetros de `Pictures.Add` são a célula superior‑esquerda onde a imagem será colocada; mantenha‑os em `0,0` para uma exportação limpa |

## Dica profissional: Exportar vários intervalos em uma única execução

Se precisar **exportar imagem de células selecionadas** para várias áreas, repita as Etapas 2‑5 dentro de um loop, alterando `printArea` a cada iteração. Lembre‑se de dar a cada imagem um nome de arquivo exclusivo, caso contrário a gravação posterior sobrescreverá o arquivo anterior.

## Conclusão

Agora você sabe como **definir a área de impressão no Excel**, configurar **como exportar png**, **salvar intervalo como imagem** e **adicionar imagem à planilha** usando Aspose.Cells. Esta solução de ponta a ponta permite transformar qualquer bloco de células em um PNG de alta qualidade com apenas algumas linhas de código C#.

A seguir, você pode explorar:

* Adicionar bordas ou marcas d'água ao PNG exportado (pesquise *add picture to worksheet* com estilização)  
* Exportar diretamente para PDF para relatórios imprimíveis (*export selected cells image* → fluxo PDF)  
* Automatizar o processo para várias pastas de trabalho em um job em lote  

Sinta‑se à vontade para experimentar diferentes intervalos, configurações de DPI ou formatos de imagem para atender às necessidades do seu projeto. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Definir Área de Impressão no Excel e Exportar para PowerPoint – Guia Passo a Passo](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Exportar Área de Impressão do Excel para HTML com Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Como Definir uma Área de Impressão no Excel Usando Aspose.Cells para .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}