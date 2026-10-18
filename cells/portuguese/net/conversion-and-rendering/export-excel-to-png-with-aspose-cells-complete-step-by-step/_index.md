---
category: general
date: 2026-06-17
description: Exporte Excel para PNG rapidamente usando Aspose.Cells. Aprenda como
  salvar Excel como PNG, converter Excel para PNG e exportar uma planilha como imagem
  em C#.
draft: false
keywords:
- export excel to png
- save excel as png
- convert excel to png
- convert excel sheet image
- save worksheet as image
language: pt
og_description: Exportar Excel para PNG em C#. Este guia mostra como salvar o Excel
  como PNG, converter Excel para PNG e exportar uma planilha como imagem com Aspose.Cells.
og_title: Exportar Excel para PNG com Aspose.Cells – Tutorial Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Export Excel to PNG quickly using Aspose.Cells. Learn how to save Excel
    as PNG, convert Excel to PNG, and export a worksheet as an image in C#.
  headline: Export Excel to PNG with Aspose.Cells – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to PNG quickly using Aspose.Cells. Learn how to save Excel
    as PNG, convert Excel to PNG, and export a worksheet as an image in C#.
  name: Export Excel to PNG with Aspose.Cells – Complete Step‑by‑Step Guide
  steps:
  - name: Rendering All Pages (Optional)
    text: 'If your sheet prints on more than one page, you can loop through them:'
  - name: Can I **save Excel as PNG** without installing Aspose?
    text: Yes, you could automate Excel via COM interop, but that requires Excel to
      be installed on the server—a big maintenance headache. Aspose.Cells runs entirely
      in managed code, making it safe for web apps, services, or CI pipelines.
  - name: What about **convert excel sheet image** for a hidden sheet?
    text: '`SheetRender` works on hidden sheets too; just make sure the worksheet’s
      `IsVisible` property is set to `true` before rendering, or temporarily set it:'
  - name: How do I **save worksheet as image** with a transparent background?
    text: 'Set the `Transparent` flag in `ImageOrPrintOptions`:'
  - name: I need a **convert excel to png** for a range only, not the whole sheet—possible?
    text: 'Absolutely. Use `RenderRange` instead of `SheetRender`:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Exportar Excel para PNG com Aspose.Cells – Guia Completo Passo a Passo
url: /pt/net/conversion-and-rendering/export-excel-to-png-with-aspose-cells-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel to PNG – Guia Completo Passo a Passo

Já precisou **exportar Excel para PNG** mas não sabia qual biblioteca permitiria fazer isso sem uma interface pesada? Você não está sozinho. Em muitos cenários de relatório você quer uma imagem estática de uma planilha — talvez para uma miniatura de e‑mail ou uma pré‑visualização rápida — então aprender a **salvar Excel como PNG** é um truque útil para qualquer desenvolvedor .NET.

Neste tutorial vamos percorrer todo o processo usando Aspose.Cells, uma biblioteca poderosa, sem licença (para avaliação) que permite **converter Excel para PNG** em apenas algumas linhas de código. Vamos cobrir tudo, desde a configuração do projeto até o tratamento de múltiplas planilhas, e ainda incluiremos algumas dicas práticas que você não encontrará na documentação oficial. Ao final, você será capaz de **converter imagem da planilha Excel** com confiança, e também verá como **salvar planilha como imagem** para qualquer aba que escolher.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

- .NET 6.0 SDK ou superior (o código também funciona com .NET Framework 4.7+).
- Visual Studio 2022 (ou qualquer IDE de sua preferência).
- O pacote NuGet **Aspose.Cells for .NET** (`Aspose.Cells`).
- Uma pasta de trabalho Excel de exemplo (`sample.xlsx`) que contenha uma planilha chamada **Pivot** (o nome é arbitrário; você pode escolher qualquer aba).

Se algum desses itens lhe for desconhecido, não se preocupe — instalar o pacote NuGet é tão simples quanto clicar com o botão direito no seu projeto → **Manage NuGet Packages** → pesquisar por *Aspose.Cells* e clicar em **Install**.

## Etapa 1: Carregar a Pasta de Trabalho e Selecionar a Planilha

Primeiro, precisamos abrir o arquivo Excel e obter a planilha que queremos exportar. O código abaixo usa a classe `Workbook` para ler o arquivo do disco, depois acessa a aba pelo nome.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook (replace the path with your actual file location)
Workbook wb = new Workbook(@"C:\Data\sample.xlsx");

// Grab the worksheet named "Pivot". Change this if your sheet has a different name.
Worksheet pivotWorksheet = wb.Worksheets["Pivot"];
```

> **Por que isso importa:** Carregar a pasta de trabalho é o primeiro passo em qualquer automação Excel. Ao referenciar a planilha pelo nome, você evita codificar índices fixos, o que torna o código mais resiliente caso você reorganize as abas depois.

## Etapa 2: Configurar Opções de Imagem para Exportação PNG

Aspose.Cells permite ajustar finamente o formato de saída via `ImageOrPrintOptions`. Aqui definimos o `ImageFormat` como PNG, que nos fornece compressão sem perdas e fundos transparentes, se necessário.

```csharp
// Set up image export options – PNG gives sharp, lossless results.
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    // Optional: adjust resolution for higher quality (default is 96 DPI)
    // HorizontalResolution = 300,
    // VerticalResolution = 300,
    // Optional: set transparent background if your sheet contains no background color
    // Transparent = true
};
```

> **Dica:** Se você pretende incorporar a imagem em uma página web, aumente o DPI para 150‑300 para obter um visual mais nítido. Apenas lembre‑se de que DPI maior gera arquivos maiores.

## Etapa 3: Criar um Objeto `SheetRender` e Renderizar a Primeira Página

Uma planilha pode abranger várias páginas imprimíveis. `SheetRender` cuida da paginação para você. O método `ToImage` recebe um índice de página baseado em zero, então `0` significa a primeira página.

```csharp
// Create a renderer that will turn the worksheet into an image.
SheetRender sheetRenderer = new SheetRender(pivotWorksheet, imageOptions);

// Export the first printable page as a PNG file.
string outputPath = @"C:\Data\Exported\pivot.png";
sheetRenderer.ToImage(0, outputPath);
```

> **O que está acontecendo?** `SheetRender` percorre o motor de layout, respeita larguras de coluna, alturas de linha e estilos aplicados, e então pinta tudo em um bitmap. A chamada `ToImage` grava esse bitmap no disco como um arquivo PNG.

### Renderizando Todas as Páginas (Opcional)

Se sua aba imprimir em mais de uma página, você pode percorrê‑las em um loop:

```csharp
int pageCount = sheetRenderer.PageCount;
for (int i = 0; i < pageCount; i++)
{
    string pagePath = $@"C:\Data\Exported\pivot_page_{i + 1}.png";
    sheetRenderer.ToImage(i, pagePath);
}
```

Agora você **converteu Excel para PNG** para cada página imprimível — um truque útil quando precisa de uma apresentação de um relatório extenso.

## Etapa 4: Verificar o Resultado

Depois que o código for executado, abra o `pivot.png` (ou os arquivos de página gerados) em qualquer visualizador de imagens. Você deverá ver uma réplica visual exata da planilha Excel, incluindo bordas de células, cores e quaisquer gráficos incorporados.

Se a imagem parecer cortada:

- Verifique a área de impressão no Excel (`Page Layout → Print Area`). Aspose respeita essa configuração.
- Ajuste propriedades de `ImageOrPrintOptions` como `OnePagePerSheet = true` para forçar tudo em uma única imagem.

## Exemplo Completo Funcional

A seguir, um aplicativo console compacto, pronto‑para‑executar, que reúne todas as peças. Copie‑e‑cole em um novo projeto console C# e pressione **F5**.

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            string excelPath = @"C:\Data\sample.xlsx";
            Workbook wb = new Workbook(excelPath);

            // 2️⃣ Choose the worksheet (replace "Pivot" if needed)
            Worksheet ws = wb.Worksheets["Pivot"];
            if (ws == null)
            {
                Console.WriteLine("Worksheet 'Pivot' not found.");
                return;
            }

            // 3️⃣ Set PNG export options
            ImageOrPrintOptions opts = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Uncomment for higher DPI:
                // HorizontalResolution = 200,
                // VerticalResolution = 200
            };

            // 4️⃣ Render to PNG
            SheetRender renderer = new SheetRender(ws, opts);
            string outDir = @"C:\Data\Exported";
            System.IO.Directory.CreateDirectory(outDir);
            string outPath = System.IO.Path.Combine(outDir, "pivot.png");
            renderer.ToImage(0, outPath);

            Console.WriteLine($"✅ Export complete: {outPath}");
        }
    }
}
```

**Saída esperada no console**

```
✅ Export complete: C:\Data\Exported\pivot.png
```

Abra o arquivo e você verá a captura exata da planilha **Pivot**.

## Perguntas Frequentes & Casos Especiais

### Posso **salvar Excel como PNG** sem instalar o Aspose?

Sim, você poderia automatizar o Excel via COM interop, mas isso exige que o Excel esteja instalado no servidor — um grande problema de manutenção. Aspose.Cells roda totalmente em código gerenciado, sendo seguro para aplicativos web, serviços ou pipelines de CI.

### E quanto a **converter imagem da planilha Excel** para uma aba oculta?

`SheetRender` funciona em abas ocultas também; basta garantir que a propriedade `IsVisible` da planilha esteja definida como `true` antes da renderização, ou alterá‑la temporariamente:

```csharp
ws.IsVisible = true; // temporarily show hidden sheet
```

### Como **salvar planilha como imagem** com fundo transparente?

Defina a flag `Transparent` em `ImageOrPrintOptions`:

```csharp
opts.Transparent = true;
```

O PNG resultante terá um canal alfa, perfeito para sobrepor em páginas web coloridas.

### Preciso de um **converter excel para png** apenas de um intervalo, não da planilha inteira — é possível?

Absolutamente. Use `RenderRange` em vez de `SheetRender`:

```csharp
CellArea range = ws.Cells.CreateRange("B2:D10");
ImageOrPrintOptions rangeOpts = new ImageOrPrintOptions { ImageFormat = ImageFormat.Png };
RangeRenderer rangeRenderer = new RangeRenderer(range, rangeOpts);
rangeRenderer.ToImage(0, @"C:\Data\range.png");
```

Agora você **converteu imagem da planilha Excel** apenas para as células que importam.

## Dicas Profissionais & Armadilhas

- **Uso de memória:** Renderizar planilhas muito grandes pode consumir gigabytes de RAM. Se ocorrer `OutOfMemoryException`, considere dividir a planilha em áreas imprimíveis menores ou aumentar as margens em `PageSetup` para reduzir o número de páginas.
- **Licenciamento:** A versão de avaliação adiciona uma marca d'água ao resultado. Adquira uma licença para uso em produção; a chamada de licenciamento é uma única linha: `License license = new License(); license.SetLicense("Aspose.Cells.lic");`.
- **Desempenho:** Reutilizar uma única instância de `ImageOrPrintOptions` para múltiplas renderizações economiza sobrecarga de alocação.
- **Caminhos de arquivos:** Sempre use `Path.Combine` para montar caminhos independentes do SO; barras invertidas fixas podem falhar em contêineres Linux.

## Conclusão

Acabamos de cobrir tudo o que você precisa para **exportar Excel para PNG** usando Aspose.Cells. Desde carregar a pasta de trabalho, escolher a aba correta, configurar opções PNG, até renderizar a primeira (ou todas) as páginas, o processo é direto e totalmente programável. Agora você sabe como **salvar Excel como PNG**, **converter Excel para PNG**, **converter imagem da planilha Excel** e **salvar planilha como imagem** para qualquer cenário — seja uma miniatura rápida de e‑mail ou um serviço de processamento em lote.

Qual o próximo passo? Experimente trocar `ImageFormat.Jpeg` por JPEG, teste `OnePagePerSheet = true` para compactar tudo em uma única imagem, ou combine esse código com uma API web que devolva os bytes PNG sob demanda. O céu é o limite, e você tem a base para construir.

Tem dúvidas ou um caso de uso interessante que gostaria de compartilhar? Deixe um comentário abaixo, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Export Excel To Png Aspose Cells Java](/cells/german/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}