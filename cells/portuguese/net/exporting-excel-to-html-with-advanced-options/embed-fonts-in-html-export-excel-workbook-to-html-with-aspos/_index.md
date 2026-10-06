---
category: general
date: 2026-06-17
description: Incorpore fontes em HTML ao salvar a pasta de trabalho como HTML. Aprenda
  como converter a pasta de trabalho para HTML e exportar o HTML do Excel com fontes
  incorporadas em poucos passos.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: pt
og_description: Incorpore fontes em HTML ao salvar a pasta de trabalho como HTML.
  Siga este guia para converter a pasta de trabalho em HTML e aprenda como exportar
  HTML do Excel com suporte total a fontes.
og_title: Incorporar fontes em HTML – Exportar pasta de trabalho do Excel para HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Incorporar fontes em HTML – Exportar pasta de trabalho do Excel para HTML com
  Aspose.Cells
url: /pt/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar fontes em HTML – Exportar pasta de trabalho Excel para HTML com Aspose.Cells

Já se perguntou como **incorporar fontes em HTML** ao exportar uma planilha Excel? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando o HTML gerado mostra uma fonte genérica sem serifa em vez do estilo original do Excel. A boa notícia? Com algumas linhas de código você pode **salvar a pasta de trabalho como HTML** e manter todas as fontes intactas.

Neste tutorial, percorreremos todo o processo de **converter pasta de trabalho para HTML** usando Aspose.Cells para .NET, explicaremos por que incorporar fontes é importante e mostraremos exatamente **como exportar Excel para HTML** para que o resultado fique igual à planilha original. Sem ferramentas externas, sem pós‑processamento manual — apenas código C# limpo e executável.

## Pré-requisitos

- .NET 6.0 ou posterior (o exemplo funciona em .NET Core, .NET Framework e .NET 5+)
- Aspose.Cells for .NET pacote NuGet (`Install-Package Aspose.Cells`)
- Um entendimento básico de C# e manipulação de arquivos Excel
- Opcional: um arquivo de fonte TrueType personalizado que você deseja incorporar (por exemplo, `MyFont.ttf`)

Tem tudo isso? Ótimo — vamos mergulhar.

## Etapa 1: Configurar o Projeto e Carregar uma Pasta de Trabalho Excel

Primeiro precisamos de um objeto workbook. Você pode criar um do zero ou carregar um `.xlsx` existente. Aqui está uma configuração mínima que também adiciona uma fonte personalizada à coleção de estilos da pasta de trabalho.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*Por que esta etapa?* Ao carregar a pasta de trabalho primeiro, damos ao Aspose.Cells a chance de inspecionar todos os estilos de célula. Registrar uma fonte personalizada garante que a fonte será encontrada quando a incorporarmos ao arquivo HTML mais tarde.

## Etapa 2: Configurar as Opções de Salvamento HTML para **Incorporar Fontes em HTML**

A mágica está em `HtmlSaveOptions`. Definir `EmbedFonts = true` instrui a biblioteca a incorporar cada fonte usada como uma regra `@font-face` codificada em Base64 dentro do arquivo HTML gerado.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*Por que habilitar `EmbedFonts`?* Sem isso, o HTML de saída referencia fontes do sistema, e quem abrir o arquivo em uma máquina que não possua essas fontes verá uma fonte de fallback. Incorporar garante fidelidade visual em todos os navegadores e dispositivos.

## Etapa 3: **Salvar Pasta de Trabalho como HTML** com as Opções Configuradas

Agora finalmente gravamos o arquivo. O método `Save` recebe três argumentos: o caminho de destino, o formato (`SaveFormat.Html`) e as opções que acabamos de configurar.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Se tudo correr bem, você terá um único arquivo `with-fonts.html` que contém todo o layout da planilha *e* os dados da fonte codificados diretamente na marcação.

## Saída Esperada

Abra `with-fonts.html` em qualquer navegador moderno (Chrome, Edge, Firefox). Você deverá ver:

- Os mesmos valores de célula, cores e bordas como no arquivo Excel original.
- Texto renderizado na fonte exata que você usou no Excel, mesmo que essa fonte não esteja instalada no seu computador.
- Nenhum arquivo externo `.css` ou de imagem — tudo está dentro do arquivo HTML.

Abaixo está um pequeno trecho de como o bloco `<style>` gerado pode parecer (a string Base64 está truncada para brevidade):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Etapa 4: Armadilhas Comuns & Como Corrigi‑las

| Problema | Por que acontece | Correção |
|------|----------------|-----|
| **Fonte ausente no HTML** | O arquivo de fonte não foi registrado com `FontConfigs` antes de salvar. | Chame `FontConfigs.AddFontFile` *antes* de criar `HtmlSaveOptions`. |
| **Tamanho enorme do arquivo HTML** | Incorporar muitas fontes grandes pode inflar o arquivo. | Incorpore apenas as fontes que realmente precisa; use `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` para incorporar apenas os glifos usados (disponível em versões mais recentes do Aspose). |
| **Caracteres incorretos (ex.: glifos asiáticos)** | A fonte não contém os intervalos Unicode necessários. | Certifique‑se de que a fonte de origem suporta os caracteres, ou incorpore uma fonte de fallback adicional. |
| **Desempenho lento em pastas de trabalho grandes** | Incorporar fontes adiciona sobrecarga de processamento. | Exporte apenas a planilha ativa (`ExportActiveWorksheetOnly = true`) ou divida a pasta de trabalho em partes menores. |

## Etapa 5: Estendendo a Solução – Exportar Múltiplas Planilhas

Se você precisar **converter pasta de trabalho para HTML** para todas as planilhas, basta desativar `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Cada planilha aparecerá como um `<div>` separado no mesmo arquivo HTML, ainda com fontes incorporadas.

## Dica Pro: Combine com Personalização de CSS

Às vezes você quer um controle mais rígido sobre a marcação gerada. `HtmlSaveOptions` oferece a propriedade `CssClassPrefix` para evitar colisões de nomes de classe ao mesclar várias exportações HTML:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Agora cada classe CSS gerada começará com `myExcel_`, facilitando a aplicação da sua própria folha de estilos posteriormente.

## Recapitulação

- **Incorporar fontes em HTML** definindo `HtmlSaveOptions.EmbedFonts = true`.
- Use **salvar pasta de trabalho como HTML** (`wb.Save(..., SaveFormat.Html, ...)`) para produzir um único arquivo autônomo.
- Este método **converte pasta de trabalho para HTML** preservando todos os detalhes visuais, respondendo à clássica pergunta **como exportar Excel para HTML** com fidelidade total.
- Registre fontes personalizadas com `FontConfigs.AddFontFile` para garantir que estejam disponíveis para incorporação.
- Ajuste opções como `ExportImagesAsBase64` e `ExportActiveWorksheetOnly` para atender às necessidades do seu projeto.

## O que vem a seguir?

- Experimente exportar para **MHTML** (`SaveFormat.Mhtml`) para um pacote ainda mais portátil.
- Explore a **conversão para PDF** (`SaveFormat.Pdf`) se precisar de um formato pronto para impressão.
- Integre a exportação HTML em uma API web para que os usuários possam baixar planilhas estilizadas sob demanda.

Sinta‑se à vontade para experimentar — troque fontes, altere a seleção de planilhas ou combine múltiplos formatos de exportação. A flexibilidade do Aspose.Cells permite que você ajuste a saída para qualquer cenário, desde painéis de relatórios automatizados até trechos de HTML prontos para e‑mail.

Feliz codificação, e que seu HTML sempre se pareça exatamente com a planilha Excel original!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e exportar Excel para HTML usando Aspose.Cells Java | Guia de Operações de Pasta de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Definir fonte padrão na conversão de Excel para HTML com Aspose.Cells para .NET | Guia de Operações de Pasta de Trabalho](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Como exportar Excel para HTML com linhas de grade usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}