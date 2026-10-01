---
category: general
date: 2026-10-01
description: Aprenda como incorporar fontes em HTML ao converter Excel para HTML usando
  Aspose.Cells. Exporte o Excel como HTML com fontes incorporadas em poucos passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: pt
lastmod: 2026-10-01
og_description: Como incorporar fontes em HTML ao exportar arquivos do Excel. Siga
  este guia passo a passo para converter Excel em HTML com fontes incorporadas.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Como incorporar fontes em HTML a partir do Excel – Guia Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Como incorporar fontes ao converter Excel para HTML com Aspose.Cells
url: /pt/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como incorporar fontes ao converter Excel para HTML com Aspose.Cells

Como incorporar fontes em HTML ao converter uma pasta de trabalho do Excel é essencial para preservar a aparência original em diferentes navegadores. Se você precisa converter Excel para HTML mantendo as fontes personalizadas intactas, este guia mostra o processo completo. Você também verá como exportar Excel como HTML e por que incorporar fontes em HTML é importante para uma renderização consistente.

Este tutorial cobre tudo o que você precisa saber: bibliotecas necessárias, configuração do código e verificação do arquivo HTML gerado. Ao final, você será capaz de exportar Excel como HTML com fontes incorporadas em apenas algumas linhas de C#.

## O que você precisará

Antes de começar, certifique‑se de que você tem:

* **.NET 6.0 ou superior** – o código tem como alvo o .NET 6, mas qualquer versão do .NET que suporte Aspose.Cells funciona.
* **Aspose.Cells para .NET** – obtenha uma licença ou use a versão de avaliação gratuita no site da Aspose.
* Um ambiente de desenvolvimento **C#** (Visual Studio, Rider ou VS Code) – qualquer IDE que possa compilar projetos .NET.
* Uma pasta de trabalho Excel (`Styled.xlsx`) que utiliza fontes personalizadas que você deseja preservar.

## Etapa 1: Configurar Aspose.Cells no seu projeto .NET

Primeiro, adicione o pacote NuGet Aspose.Cells ao seu projeto:

```bash
dotnet add package Aspose.Cells
```

Em seguida, inclua o namespace no topo do seu arquivo C#:

```csharp
using Aspose.Cells;
```

Adicionar o pacote disponibiliza as classes `Workbook`, `HtmlSaveOptions` e outras relacionadas.

## Etapa 2: Carregar a pasta de trabalho Excel

Carregar a pasta de trabalho é o primeiro passo concreto em **como exportar dados do Excel**. O construtor `Workbook` lê o arquivo do disco:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Por que isso importa:* Aspose.Cells analisa a pasta de trabalho, incluindo estilos de célula, fórmulas e informações de fonte. Se o arquivo não for encontrado, uma exceção será lançada, portanto, verifique se o caminho está correto.

## Etapa 3: Configurar as opções de salvamento HTML para incorporar fontes

O núcleo de **incorporar fontes em html** é a classe `HtmlSaveOptions`. Defina `EmbedFonts` como `true` para que cada fonte usada na pasta de trabalho seja escrita na saída HTML como uma regra `@font-face` codificada em Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Por que isso importa:* Por padrão, Aspose.Cells referencia arquivos de fonte externos, que podem não estar disponíveis na máquina do cliente. Habilitar `EmbedFonts` garante que o HTML renderizado tenha a mesma aparência da planilha Excel original, independentemente das fontes instaladas no visualizador.

### Caso especial: fontes não suportadas

Se a pasta de trabalho usar uma fonte que não está instalada no servidor, Aspose.Cells recairá para uma fonte padrão do sistema. Para evitar isso, instale as fontes necessárias no servidor ou incorpore‑as manualmente após a exportação.

## Etapa 4: Salvar a pasta de trabalho como HTML usando as opções configuradas

Agora você pode gravar o arquivo HTML. O método `Save` recebe o caminho de saída e a instância `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Após a execução, `Styled.html` contém os dados da planilha e um bloco `<style>` com definições `@font-face` codificadas em Base64 para cada fonte personalizada.

## Etapa 5: Verificar as fontes incorporadas

Abra `Styled.html` em um navegador. Inspecione a seção `<head>`; você deverá ver algo como:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Se as fontes aparecerem corretamente na tabela renderizada, a incorporação foi bem‑sucedida. Caso note glifos ausentes, verifique novamente se os arquivos de fonte de origem estão instalados na máquina que executa a conversão.

## Variações comuns e opções adicionais

### Converter várias planilhas

Se você precisar **converter Excel para HTML** de todas as planilhas, defina `ExportActiveWorksheetOnly = false` (o padrão). Aspose.Cells criará um arquivo HTML separado para cada planilha.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Controlar a saída CSS

Você pode reduzir o tamanho do HTML desativando o CSS embutido:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Usar um stream em vez de um arquivo

Ao integrar em uma API web, grave o HTML em um `MemoryStream` e retorne‑o diretamente:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Dica profissional: licenciar o produto para remover marcas d'água de avaliação

Se você estiver usando a versão de avaliação, o HTML gerado pode conter um comentário de marca d'água. Aplique sua licença Aspose.Cells antes de carregar a pasta de trabalho para produzir uma saída limpa:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Exemplo completo funcional

Abaixo está um programa completo e executável que demonstra **como incorporar fontes**, **converter excel para html** e **exportar excel como html** de uma só vez:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Saída esperada:** Após executar o programa, `Styled.html` aparecerá em `YOUR_DIRECTORY`. Abrir o arquivo em qualquer navegador moderno mostrará a planilha com as mesmas fontes do arquivo Excel original, mesmo em máquinas que não possuam essas fontes.

## Conclusão

Agora você sabe **como incorporar fontes** ao **converter Excel para HTML** usando Aspose.Cells, e viu todo o fluxo desde o carregamento da pasta de trabalho até a verificação das fontes incorporadas. Essa abordagem garante que a fidelidade visual dos seus arquivos Excel seja mantida no HTML gerado, sendo ideal para relatórios web, newsletters por e‑mail ou qualquer cenário em que você precise **exportar Excel como HTML** com tipografia personalizada.

Em seguida, explore tópicos relacionados como **exportar Excel como PDF**, **estilizar a saída HTML com CSS personalizado** ou **processamento em lote de várias pastas de trabalho**. Cada um desses se baseia no mesmo padrão `HtmlSaveOptions`, permitindo adaptar o código com mudanças mínimas.

Happy coding!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}