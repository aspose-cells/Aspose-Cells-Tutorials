---
category: general
date: 2026-07-14
description: Salve o Excel como HTML rapidamente e aprenda como converter Excel para
  HTML com formatação completa. Exporte o Excel com formatação usando Aspose.Cells
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: pt
lastmod: 2026-07-14
og_description: Salve o Excel como HTML instantaneamente. Este guia mostra como converter
  Excel para HTML preservando estilos e habilitando a formatação de números do Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Salvar Excel como HTML – Exportação passo a passo com formatação completa
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Salvar Excel como HTML – Guia Completo para Exportar Excel com Formatação
url: /pt/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar Excel como HTML – Guia Completo para Exportar Excel com Formatação

Já se perguntou como **salvar Excel como HTML** sem perder as cores, bordas ou formatos numéricos? Você não está sozinho. Em muitos cenários de relatório você precisa de uma visualização pronta para a web de uma pasta de trabalho, e a maneira mais rápida é exportar o arquivo diretamente para HTML.  

Neste tutorial vamos percorrer os passos exatos para **converter Excel para HTML** usando Aspose.Cells, habilitar a formatação numérica do Grid.js e garantir que a saída fique exatamente como a planilha original. Ao final, você terá um arquivo HTML pronto‑para‑usar que pode ser servido por qualquer servidor web.

## O que você aprenderá

- Pré-requisitos e instalação do pacote  
- Carregando uma pasta de trabalho existente (ou criando uma na hora)  
- Configurando `HtmlSaveOptions` para fidelidade visual perfeita  
- Habilitando `GridJsOptions.EnableNumberFormat` para manter a formatação numérica intacta  
- Salvando o arquivo e verificando o resultado  

Se você já tentou **exportar Excel com formatação** usando um dump genérico de CSV, sabe o quão frustrante pode ser quando os números se tornam texto simples. Este guia evita essa armadilha.

---

## Pré-requisitos – Configure seu Ambiente de Desenvolvimento

Antes de mergulharmos no código, certifique‑se de que você tem:

| Requisito | Por que isso importa |
|-------------|----------------|
| .NET 6.0 ou posterior (o tutorial usa .NET 6) | APIs modernas e melhor desempenho |
| Visual Studio 2022 (ou VS Code com extensão C#) | Edição e depuração confortáveis |
| Pacote NuGet Aspose.Cells para .NET | A biblioteca que alimenta `HtmlSaveOptions` e `GridJsOptions` |
| Um arquivo Excel de exemplo (`sample.xlsx`) ou uma pasta de trabalho que você gera no código | A fonte que você converterá |

Instale Aspose.Cells com o seguinte comando no Console do Gerenciador de Pacotes:

```powershell
Install-Package Aspose.Cells
```

> **Dica profissional:** Se você estiver em um pipeline de CI, adicione a mesma linha `dotnet add package` ao seu script de build para que a dependência esteja sempre presente.

---

## Etapa 1: Carregar ou Criar uma Pasta de Trabalho

Você pode carregar um arquivo existente ou criar um programaticamente. Aqui está um exemplo mínimo que cria uma pasta de trabalho com algumas células formatadas para que você possa ver a formatação sobreviver à exportação.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Por que isso importa:** Ao definir explicitamente os formatos numéricos, você verá mais tarde `GridJsOptions.EnableNumberFormat` manter esses formatos ativos na saída HTML.

---

## Etapa 2: Configurar Opções de Salvamento HTML

Agora criamos uma instância de `HtmlSaveOptions`. Este objeto informa ao Aspose.Cells exatamente como você deseja que o HTML seja renderizado.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Habilitando a Formatação Numérica do Grid.js

Se você pretende incorporar o HTML em uma página que usa **Grid.js** para tabelas interativas, desejará que os números permaneçam formatados (por exemplo, símbolos de moeda, separadores de milhar). A linha a seguir faz exatamente isso:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **O que está acontecendo nos bastidores?** `EnableNumberFormat` injeta um pequeno trecho de JavaScript que informa ao Grid.js para interpretar o atributo `data-format` da célula, preservando a formatação no estilo Excel no navegador.

---

## Etapa 3: Salvar a Pasta de Trabalho como um Arquivo HTML

Com a pasta de trabalho pronta e as opções ajustadas, a linha final grava o arquivo HTML no disco.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Executar o programa produz um arquivo `gridjs.html` que se parece com isto (visual simplificado):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Abra o arquivo em qualquer navegador e você verá uma tabela bem estilizada, completa com o fundo do cabeçalho cinza‑claro e formatação de moeda. Se você inserir a página em um site que já carrega o Grid.js, os números serão renderizados automaticamente com as vírgulas e símbolos corretos.

---

## Armadilhas Comuns ao **Converter Excel para HTML**

| Problema | Por que ocorre | Como evitar |
|----------|----------------|-------------|
| **Fórmulas perdidas** | HTML é estático; fórmulas se tornam valores simples. | Se você precisar de cálculos ao vivo, mantenha a pasta de trabalho no servidor e use bibliotecas JavaScript como SheetJS. |
| **Imagens ausentes** | Imagens são armazenadas como recursos separados. | Defina `HtmlSaveOptions.ExportImagesAsBase64 = true` para incorporá‑las diretamente. |
| **Arquivos enormes** | Pastas de trabalho grandes geram HTML + JS massivos. | Use `ExportOnlyVisibleSheets` ou divida em várias páginas via `HtmlSaveOptions.OnePagePerSheet`. |
| **Localidade numérica incorreta** | Excel armazena números em cultura invariável, navegadores podem aplicar configurações locais. | Defina explicitamente `htmlOptions.Encoding = Encoding.UTF8` e use `GridJsOptions.EnableNumberFormat`. |

---

## Avançado: Exportando Múltiplas Planilhas com Instâncias Individuais do Grid.js

Se sua pasta de trabalho contém várias planilhas e você deseja que cada uma se torne sua própria tabela Grid.js, você pode percorrer as planilhas e salvar cada uma separadamente:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Cada arquivo conterá seu próprio elemento `<table class="gridjs-table">`, pronto para manipulação independente.

---

## Verificando a Saída – Checklist Rápido

1. **Estilo intacto?** Compare as cores de fundo das células e bordas com a visualização original do Excel.  
2. **Formatos numéricos preservados?** Procure o atributo `data-format` nos elementos `<td>`.  
3. **Imagens exibidas?** Se você exportou imagens como Base64, elas devem aparecer embutidas.  
4. **Console do navegador limpo?** Sem erros de JavaScript relacionados ao Grid.js.  

Se alguma dessas verificações falhar, revise a propriedade correspondente de `HtmlSaveOptions` — a maioria dos problemas decorre de uma flag ausente.

---

## Conclusão

Agora você tem um método sólido e pronto para produção de **salvar Excel como HTML** mantendo cada estilo, borda e representação numérica intactos. Ao configurar `HtmlSaveOptions` e alternar `GridJsOptions.EnableNumberFormat`, você transformou uma planilha estática em uma tabela amigável para a web que funciona perfeitamente com o Grid.js.

Em resumo, este tutorial mostra como **converter Excel para HTML** e **exportar Excel com formatação** usando Aspose.Cells. Sinta‑se à vontade para experimentar: teste diferentes temas, incorpore gráficos ou até sirva o HTML através de um endpoint ASP.NET para conversão em tempo real.

Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação do Aspose.Cells para opções de configuração mais avançadas. Feliz codificação!

## O que vem a seguir?

- **Explore outros formatos de exportação**: PDF, PNG ou CSV via `Workbook.Save`.  
- **Integre com ASP.NET Core**: Retorne a string HTML diretamente de uma ação de controlador.  
- **Combine com SheetJS**: Carregue o HTML gerado de volta em uma pasta de trabalho JavaScript para edição no lado do cliente.  

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar Excel para HTML com Linhas de Grade Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Exportar Excel para HTML Preservando Estilos de Borda Usando Aspose.Cells para Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Converter HTML para Excel Usando Aspose.Cells .NET: Um Guia Abrangente](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}