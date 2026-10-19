---
category: general
date: 2026-10-10
description: Aprenda a incorporar fontes ao exportar o Excel para HTML em C#. Este
  guia cobre exportar Excel para HTML, converter Excel para HTML e como salvar o Excel
  com fontes incorporadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: pt
lastmod: 2026-10-10
og_description: Como incorporar fontes ao exportar Excel para HTML em C#. Siga este
  tutorial completo para exportar Excel em HTML, converter Excel em HTML e aprender
  como salvar o Excel com fontes incorporadas.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: Como incorporar fontes ao exportar Excel para HTML – guia passo a passo
  em C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: Como incorporar fontes ao exportar Excel para HTML com C#
url: /pt/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como incorporar fontes ao exportar Excel para HTML com C#

Se você precisa **how to embed fonts** em um arquivo HTML gerado a partir de uma pasta de trabalho do Excel, este tutorial mostra os passos exatos. Exportar Excel para HTML frequentemente remove fontes personalizadas, o que compromete a fidelidade visual da planilha original. Ao configurar as opções corretas, você pode preservar cada tipo de letra diretamente na saída HTML.

Neste guia você aprenderá como **export excel html**, **convert excel html**, e **how to save Excel** com fontes incorporadas, usando a biblioteca Aspose.Cells for .NET. A solução funciona com .NET 6+ e requer apenas algumas linhas de código C#.

## O que você alcançará

- Um programa C# completo e executável que carrega um arquivo `.xlsx` existente.
- Saída HTML onde todas as fontes usadas são incorporadas como regras `@font-face` codificadas em Base64.
- Confiança de que o HTML exportado tem a mesma aparência da pasta de trabalho original em qualquer navegador.

## Pré‑requisitos

| Requisito | Motivo |
|-------------|--------|
| .NET 6 SDK ou posterior | Fornece o runtime para o projeto C#. |
| Visual Studio 2022 (ou qualquer IDE) | Facilita a criação e execução do aplicativo console. |
| Aspose.Cells for .NET (pacote NuGet `Aspose.Cells`) | Disponibiliza a classe `HtmlSaveOptions` e o recurso `EmbedFonts`. |
| Um arquivo Excel (`sample.xlsx`) que usa uma fonte personalizada (ex., *Calibri* ou uma fonte TrueType baixada) | Demonstra o efeito da incorporação de fontes. |

> **Dica profissional:** Se você trabalha atrás de um proxy corporativo, configure o NuGet para usar o proxy antes de instalar o pacote.

## Etapa 1: Instalar Aspose.Cells

Abra um terminal na pasta do projeto e execute:

```bash
dotnet add package Aspose.Cells
```

## Etapa 2: Carregar a pasta de trabalho Excel

Crie um novo aplicativo console (`dotnet new console`) e adicione o código a seguir em `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**Por que esta etapa é importante:**  
Carregar a pasta de trabalho lhe dá acesso às suas planilhas, estilos e às fontes personalizadas referenciadas dentro do arquivo. Sem uma instância `Workbook` carregada, você não pode configurar as opções de exportação.

## Etapa 3: Configurar as opções de salvamento HTML para incorporar fontes

A classe `HtmlSaveOptions` controla todos os aspectos da exportação HTML. Definir `EmbedFonts = true` indica ao Aspose.Cells que incorpore todas as fontes usadas na pasta de trabalho diretamente no arquivo HTML gerado.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**Explicação:**  
- `EmbedFonts` é a flag principal que satisfaz o requisito **how to embed fonts**.  
- `ExportImagesAsBase64` garante que quaisquer imagens também se tornem parte do único arquivo HTML, simplificando a implantação.  
- `ExportActiveWorksheetOnly` definido como `false` garante que todas as planilhas sejam incluídas, o que é útil quando a pasta de trabalho abrange várias folhas.

## Etapa 4: Salvar a pasta de trabalho como HTML com fontes incorporadas

Agora invoque o método `Save`, passando o caminho de saída desejado e as opções que você acabou de configurar:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

O arquivo `Embedded.html` resultante contém:

- Marcação HTML padrão para os dados da planilha.
- Um ou mais blocos `<style>` com regras `@font-face` que incorporam as fontes personalizadas como strings Base64.
- Todas as imagens codificadas diretamente no HTML (se houver).

## Etapa 5: Verificar se as fontes estão realmente incorporadas

Abra `Embedded.html` em um navegador (Chrome, Edge, Firefox). A página deve ser renderizada exatamente como a pasta de trabalho Excel original, mesmo que a máquina de destino não tenha as fontes personalizadas instaladas.

Para confirmar a incorporação:

1. Abra o código‑fonte da página (`Ctrl+U` na maioria dos navegadores).  
2. Procure por `@font-face`. Você verá um bloco semelhante a:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Se o atributo `src` contiver uma URL `data:`, a fonte foi incorporada com sucesso.

## Variações comuns e casos de borda

| Situação | Ajuste sugerido |
|-----------|----------------------|
| **Large workbook with many custom fonts** | Aumente o `MaxFontEmbeddingSize` (se disponível) ou divida a exportação em vários arquivos HTML para evitar atingir os limites de tamanho dos navegadores. |
| **You need only a single worksheet** | Defina `opts.ExportActiveWorksheetOnly = true` e ative a planilha desejada antes de salvar (`wb.Worksheets[0].Activate();`). |
| **Embedding fonts is not allowed by corporate policy** | Defina `opts.EmbedFonts = false` e dependa de fontes web‑seguras ou forneça os arquivos de fonte junto com o HTML. |
| **Targeting older browsers that don’t support Base64 fonts** | Use `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (se a versão da biblioteca suportar) para gerar arquivos `.ttf` separados e referenciá‑los com URLs normais. |

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar‑colar em `Program.cs`. Ele inclui todas as diretivas `using` necessárias e tratamento de erros para um script pronto para produção.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Saída esperada:**  
Ao executar o programa, ele imprime a linha de confirmação e cria `Embedded.html`. Abrir o arquivo em qualquer navegador moderno mostra a planilha com todas as fontes originais intactas, atendendo ao objetivo **how to embed fonts**.

## Conclusão

Agora você sabe **how to embed fonts** ao realizar uma operação de **export excel html**, como **convert excel html** sem perder tipos de letra, e os passos exatos para **how to save excel** como um arquivo HTML com fontes incorporadas. Ao usar `HtmlSaveOptions.EmbedFonts = true`, o HTML gerado torna‑se autocontido, portátil e visualmente idêntico à pasta de trabalho original.

### O que vem a seguir?

- Explore as propriedades de `HtmlSaveOptions` para controlar CSS, manipulação de imagens e seleção de planilhas.  
- Combine esta técnica com automação no lado do servidor para gerar relatórios HTML dinamicamente.  
- Investigue **embed fonts html** para outros formatos de documento (ex., PDF) usando APIs Aspose semelhantes.

Sinta‑se à vontade para experimentar diferentes fontes, tamanhos de pasta de trabalho e ambientes de navegador. Se encontrar algum problema, reveja a tabela de casos de borda acima ou consulte a documentação do Aspose.Cells para cenários avançados de incorporação de fontes. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar Excel para HTML – Guia de Programação Completo](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [Como Exportar Excel para HTML – Guia Passo a Passo](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Como Incorporar Fontes ao Converter Excel para PDF – Guia Completo](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}