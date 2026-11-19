---
category: general
date: 2026-11-19
description: Como exportar um gráfico do Excel como imagem PNG usando Aspose.Cells.
  Aprenda a salvar a imagem do gráfico do Excel e definir o formato da imagem como
  PNG em apenas alguns passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: pt
lastmod: 2026-11-19
og_description: Como exportar um gráfico do Excel como imagem PNG com Aspose.Cells.
  Siga este guia passo a passo para salvar a imagem do gráfico do Excel e definir
  o formato da imagem como PNG de forma eficiente.
og_image_alt: How to export Excel chart as a PNG image
og_title: Como exportar um gráfico do Excel como imagem PNG – guia rápido em C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Como exportar gráfico do Excel como imagem PNG com C#
url: /pt/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar um gráfico do Excel como imagem PNG com C#

Se você precisa **exportar um gráfico do Excel** para uma imagem portátil, este guia mostra uma solução completa, pronta‑para‑executar. Usando Aspose.Cells você pode **salvar a imagem do gráfico do Excel** em formato PNG com apenas três linhas de código, e o tutorial também explica como **definir o formato de imagem png** e **salvar o arquivo de imagem do Excel** com segurança.

Você terminará este artigo com um programa executável que carrega uma pasta de trabalho, renderiza o primeiro gráfico e grava um arquivo `pivot.png` no disco. Sem ferramentas adicionais, sem copiar‑colar manual—apenas código C# limpo que você pode inserir em qualquer projeto .NET.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.6+)
* Visual Studio 2022 ou qualquer editor C#
* Uma licença do Aspose.Cells for .NET (ou uma chave de avaliação temporária)
* Um arquivo Excel (`pivot.xlsx`) que contenha ao menos um gráfico na primeira planilha

Esses itens são as únicas dependências externas; o tutorial não requer o Office instalado na máquina.

## Etapa 1: Instalar o Aspose.Cells

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Cells
```

O pacote adiciona o namespace `Aspose.Cells`, que fornece as classes `Workbook`, `ImageOrPrintOptions` e outras necessárias para **salvar a imagem do gráfico do Excel**.

## Etapa 2: Criar um programa console mínimo

Crie um novo aplicativo console (`dotnet new console -n ExportChartDemo`) e substitua o `Program.cs` gerado automaticamente pelo código a seguir. O programa demonstra **como exportar um gráfico do Excel** e inclui comentários que explicam cada decisão.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Por que cada parte importa

* **Carregando a pasta de trabalho** – `Workbook` analisa o arquivo `.xlsx` sem precisar do Microsoft Excel instalado.
* **ImageOrPrintOptions** – Este objeto controla o formato de saída. Definir `ImageFormat = ImageFormat.Png` **define o formato de imagem png**, que é sem perdas e amplamente suportado.
* **RenderToImage** – O método `RenderToImage` converte o gráfico (um objeto `Picture`) em um arquivo de imagem. O método também lida com dimensionamento, DPI e transparência automaticamente.
* **Tratamento de erros** – A verificação `sheet.Pictures.Count == 0` impede uma exceção em tempo de execução se a planilha não possuir gráficos, um caso comum quando o usuário aponta para a planilha errada.

## Etapa 3: Executar o programa e verificar o resultado

1. Compile o projeto: `dotnet build`.
2. Execute-o: `dotnet run --project ExportChartDemo`.

Se tudo estiver configurado corretamente, você verá:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Abra `pivot.png` com qualquer visualizador de imagens. Você deverá ver a representação visual exata do gráfico do Excel, confirmando que você **salvou o arquivo de imagem do Excel** com sucesso.

### Saída esperada

Abaixo está um exemplo de como o PNG exportado pode ser (o gráfico real depende do seu arquivo de origem).

![Gráfico do Excel exportado salvo como imagem PNG](images/exported-chart.png){: .center alt="Como exportar um gráfico do Excel como imagem PNG"}

## Etapa 4: Opções avançadas – exportar vários gráficos

Se sua pasta de trabalho contiver mais de um gráfico, você pode percorrer a coleção `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Esse padrão permite **salvar a imagem do gráfico do Excel** para cada gráfico na planilha, o que é útil em pipelines de relatórios.

## Problemas comuns e como evitá‑los

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| `ArgumentOutOfRangeException` em `Pictures[0]` | A planilha não tem gráfico ou o gráfico está em outra planilha. | Verifique o índice da planilha (`Worksheets[0]`) e assegure‑se de que o gráfico exista. Use `Worksheets["SheetName"]` se necessário. |
| Imagem exportada está borrada | DPI definido muito baixo (padrão 96). | Aumente `HorizontalResolution` e `VerticalResolution` em `ImageOrPrintOptions`. |
| Arquivo PNG está vazio ou corrompido | Licença ausente causando restrições de avaliação. | Aplique uma licença válida do Aspose.Cells antes de carregar a pasta de trabalho (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Erros de caminho de arquivo (`FileNotFoundException`) | Placeholder `YOUR_DIRECTORY` incorreto. | Use caminhos absolutos ou `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Resolver esses problemas garante uma experiência tranquila ao **salvar o arquivo de imagem do Excel**.

## Dica profissional: Exportar diretamente para um fluxo de memória

Às vezes você precisa da imagem na memória (por exemplo, para enviar a uma API web) em vez de gravá‑la no disco:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

A mesma lógica de **definir o formato de imagem png** se aplica; você apenas substitui o caminho do arquivo por um stream.

## Conclusão

Agora você sabe **como exportar um gráfico do Excel** como um arquivo PNG usando Aspose.Cells para .NET. O tutorial abordou:

* Instalação da biblioteca
* Carregamento de uma pasta de trabalho
* **Definir o formato de imagem png**
* **Salvar a imagem do gráfico do Excel** no disco
* Manipulação de múltiplos gráficos e erros comuns

Com essa base, você pode integrar a exportação de gráficos em relatórios automatizados, serviços web ou utilitários de desktop. Em seguida, explore tópicos relacionados como **salvar o arquivo de imagem do Excel** como JPEG (`ImageFormat.Jpeg`) ou converter gráficos para PDF para relatórios imprimíveis.

Bom código!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}