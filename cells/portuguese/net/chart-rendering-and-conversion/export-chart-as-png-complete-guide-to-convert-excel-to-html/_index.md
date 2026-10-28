---
category: general
date: 2026-06-30
description: Exporte o gráfico como PNG enquanto converte o Excel para HTML usando
  Aspose.Cells. Aprenda a incorporar imagens como Base64 e salvar a pasta de trabalho
  como HTML em minutos.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: pt
og_description: Exporte o gráfico como PNG e incorpore imagens como Base64 ao converter
  Excel para HTML. Siga este tutorial passo a passo em C# para salvar a pasta de trabalho
  como HTML sem esforço.
og_title: Exportar gráfico como PNG – Converter Excel para HTML com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Exportar Gráfico como PNG – Guia Completo para Converter Excel em HTML com
  Aspose.Cells
url: /pt/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Gráfico como PNG – Guia Completo para Converter Excel em HTML com Aspose.Cells

Já se perguntou como **exportar gráfico como PNG** diretamente de uma pasta de trabalho do Excel enquanto também transforma toda a planilha em HTML limpo e responsivo? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam de um relatório pronto para a web que exiba gráficos sem lidar com arquivos de imagem separados. A boa notícia é que o Aspose.Cells torna isso muito fácil.

Neste tutorial vamos percorrer os passos exatos para **converter Excel em HTML**, **incorporar imagens como Base64** e, finalmente, **salvar a pasta de trabalho como HTML** — tudo garantindo que cada gráfico seja salvo como uma imagem PNG. Ao final, você terá um único arquivo HTML que pode ser inserido em qualquer página web, e cada gráfico aparecerá instantaneamente, sem necessidade de ativos adicionais.

## O que você aprenderá

- Como carregar uma pasta de trabalho existente que já contém gráficos.  
- Quais sinalizadores de `HtmlSaveOptions` controlam a exportação de imagens, o formato dos gráficos e a responsividade.  
- O código exato necessário para **exportar gráfico como PNG** e incorporar esses PNGs como strings Base64.  
- Como **salvar a pasta de trabalho como HTML** com uma única chamada de método.  
- Dicas para solucionar armadilhas comuns, como imagens de gráfico ausentes ou strings Base64 excessivamente grandes.  

**Pré‑requisitos:**  
- .NET 6+ (ou .NET Framework 4.6+) instalado.  
- Uma licença válida do Aspose.Cells (ou uma chave de avaliação temporária).  
- Familiaridade básica com C# e Visual Studio (ou sua IDE favorita).  

Se algum desses itens lhe for desconhecido, faça uma pausa e configure‑os; o restante do guia assume que tudo está pronto.

---

## Etapa 1: Configurar Seu Projeto e Instalar Aspose.Cells

Antes de podermos **exportar gráfico como PNG**, precisamos de um projeto C# que faça referência à biblioteca Aspose.Cells.

1. Abra o Visual Studio e crie um novo **Console App** (`dotnet new console`).  
2. Adicione o pacote NuGet do Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (Opcional) Se você possui um arquivo de licença, coloque‑o na raiz do projeto e ative‑o em tempo de execução:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Dica profissional:** Mantenha o arquivo de licença fora do controle de versão. Use variáveis de ambiente ou armazenamentos seguros de segredos em produção.

---

## Etapa 2: Carregar a Pasta de Trabalho que Contém o Gráfico

Agora vamos carregar o arquivo Excel que já possui o gráfico que queremos **exportar gráfico como PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Por que isso importa:** Carregar a pasta de trabalho antecipadamente nos dá acesso a todas as planilhas, gráficos e objetos incorporados. Se a pasta de trabalho falhar ao carregar, a etapa subsequente de **exportar gráfico para PNG** nunca será executada.

---

## Etapa 3: Configurar as Opções de Salvamento HTML

O coração da solução está em `HtmlSaveOptions`. Ao alternar algumas propriedades podemos:

- **ExportChartImageFormat = ImageFormat.Png** → garante que cada gráfico se torne um PNG.  
- **ExportImagesAsBase64 = true** → incorpora os dados PNG diretamente no HTML, eliminando arquivos externos.  
- **IsResponsive = true** → faz com que as tabelas geradas se adaptem a telas móveis.  
- **ExportPrintingHeadersFooters = false** → remove metadados de impressão desnecessários.  

Aqui está a configuração completa:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Por que essas configurações?

- **ExportChartImageFormat = ImageFormat.Png** é a única maneira de garantir uma imagem de gráfico sem perdas e segura para a web.  
- **ExportImagesAsBase64 = true** permite **incorporar imagens como Base64**, ideal para relatórios por e‑mail ou implantações de arquivo único.  
- **IsResponsive = true** resolve uma reclamação comum: tabelas que transbordam em smartphones.  
- **ExportPrintingHeadersFooters = false** mantém o HTML leve — sem informações de impressão ocultas que nunca são usadas na web.  

---

## Etapa 4: Salvar a Pasta de Trabalho como HTML

Com as opções definidas, a linha final é uma única chamada que tanto **converte Excel em HTML** quanto **exporta gráfico como PNG** nos bastidores.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

Quando essa linha terminar, você terá um arquivo chamado `Report.html`. Abra‑o em qualquer navegador e verá:

- Todos os dados da planilha renderizados como tabelas HTML limpas.  
- Cada gráfico exibido como uma imagem PNG embutida (graças ao Base64).  
- Nenhum arquivo de imagem extra ao lado do HTML.  

### Saída Esperada

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Observe o atributo `src="data:image/png;base64,..."` — essa é a mágica de **incorporar imagens como base64** em ação. Nenhum arquivo `.png` separado é criado no disco.

---

## Etapa 5: Verificar a Exportação PNG e Ajustar se Necessário

Às vezes um gráfico pode ficar ligeiramente distorcido após a conversão, especialmente se usar fontes personalizadas ou gradientes complexos. Veja como conferir:

1. Abra o HTML gerado no Chrome. Clique com o botão direito na imagem do gráfico e selecione **Abrir imagem em nova aba**. A URL ainda começará com `data:image/png;base64,`.  
2. Se a imagem aparecer borrada, considere aumentar a resolução do gráfico antes de salvar:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Para gráficos que dependem de fontes de dados externas, certifique‑se de que a pasta de trabalho esteja totalmente atualizada antes de salvar:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Esses ajustes garantem que a etapa **exportar gráfico do Excel para PNG** produza gráficos nítidos e prontos para produção.

---

## Etapa 6: Implantar o HTML em Qualquer Lugar

Como todas as imagens estão incorporadas, você pode agora:

- Enviar o HTML como um único anexo de e‑mail.  
- Colar o HTML em um CMS que aceite código bruto.  
- Hospedar em um site estático sem se preocupar com arquivos PNG ausentes.  

Se precisar dos arquivos PNG como ativos separados (talvez para um PDF mais tarde), basta mudar `ExportImagesAsBase64` para `false` e apontar `HtmlSaveOptions` para uma pasta de saída de imagens.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Agora o HTML referenciará arquivos PNG externos, ainda garantindo **exportar gráfico como PNG**, mas fornecendo arquivos de imagem individuais para outros usos.

---

## Armadilhas Comuns & Como Evitá‑las

| Sintoma | Causa Provável | Solução |
|---------|----------------|---------|
| Gráfico ausente no HTML | `ExportChartImageFormat` deixado no padrão (`Jpeg`) e o navegador bloqueia conteúdo misto. | Defina `ExportChartImageFormat = ImageFormat.Png`. |
| Arquivo HTML muito grande (vários MB) | Gráficos grandes ou muitas imagens de alta resolução incorporadas como Base64. | Reduza `htmlOptions.ImageResolution` ou comprima o gráfico no Excel antes da conversão. |
| Tabelas transbordam em dispositivos móveis | `IsResponsive` não habilitado. | Garanta `IsResponsive = true` em `HtmlSaveOptions`. |
| Strings Base64 contêm quebras de linha | Versões antigas do .NET podem envolver strings longas. | Atualize para .NET 6+ ou defina `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bônus: Envolver Tudo em um Método Reutilizável

Se você for fazer essa conversão repetidamente, encapsule a lógica:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Agora você pode chamar `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` de qualquer lugar do seu código.

---

## Conclusão

Você acabou de dominar como **exportar gráfico como PNG** enquanto **converte Excel em HTML**, **incorpora imagens como Base64** e **salva a pasta de trabalho como HTML** usando Aspose.Cells. O ponto principal é que algumas configurações bem escolhidas de `HtmlSaveOptions` fornecem um único arquivo HTML autocontido que funciona em qualquer dispositivo — sem arquivos PNG extras, sem pastas bagunçadas.

Pronto para o próximo desafio? Experimente combinar esta abordagem com **exportar gráfico do Excel para PNG** para geração de PDF, ou teste CSS personalizado para estilizar ainda mais as tabelas. O céu é o limite quando você controla tanto os dados quanto a apresentação programaticamente.

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo, ou compartilhar como adaptou esse padrão em seus próprios projetos. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}