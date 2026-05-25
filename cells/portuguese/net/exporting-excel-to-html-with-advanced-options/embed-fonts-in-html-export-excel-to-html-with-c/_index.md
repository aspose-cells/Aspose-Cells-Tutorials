---
category: general
date: 2026-05-23
description: Incorpore fontes em HTML ao exportar Excel para HTML usando Aspose.Cells.
  Guia passo a passo para converter planilha em HTML com fontes incorporadas.
draft: false
keywords:
- embed fonts in html
- export excel to html
- convert spreadsheet to html
- save workbook as html
- how to embed fonts html
language: pt
og_description: Incorpore fontes em HTML ao exportar o Excel para HTML. Aprenda como
  converter planilhas para HTML com fontes incorporadas em alguns passos simples.
og_title: Incorporar fontes em HTML – Exportar Excel para HTML com C#
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  headline: Embed fonts in HTML – Export Excel to HTML with C#
  type: TechArticle
- description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  name: Embed fonts in HTML – Export Excel to HTML with C#
  steps:
  - name: 1️⃣ **What if my workbook uses a custom font that isn’t installed on the
      server?**
    text: Aspose.Cells can only embed fonts that are available to the runtime. Install
      the `.ttf` or `.otf` file on the machine running the conversion, or copy it
      into the project directory and register it via `System.Drawing.Text.PrivateFontCollection`
      before invoking the save operation.
  - name: 2️⃣ **Will embedding increase the file size dramatically?**
    text: Yes, each embedded font is Base64‑encoded, which adds roughly 33 % overhead.
      If the workbook uses many large fonts, consider enabling `EmbedOnlyUsedFonts
      = true` to limit the payload to fonts actually referenced in the sheet.
  - name: 3️⃣ **Can I still export images separately?**
    text: Setting `ExportImagesAsBase64 = true` (as shown above) inlines images, making
      the HTML truly self‑contained. If you prefer external image files, set this
      property to `false` and specify `ExportImagesFolder` to control the output folder.
  - name: 4️⃣ **Is this approach compatible with older browsers?**
    text: Most modern browsers (Chrome, Edge, Firefox, Safari) support Base64‑encoded
      `@font-face`. Internet Explorer 11 also works, but you might need to ensure
      the MIME type is correct. For legacy support, consider providing a fallback
      font stack in your CSS.
  - name: 5️⃣ **How does this differ from a simple “export excel to html” without
      embedding?**
    text: A plain export writes the text using generic web fonts (`Arial`, `Helvetica`,
      etc.). The visual layout may shift, especially for corporate reports that rely
      on a brand‑specific typeface. Embedding removes that uncertainty.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Incorporar fontes em HTML – Exportar Excel para HTML com C#
url: /pt/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar fontes em HTML – Exportar Excel para HTML com C#

Já se perguntou como **incorporar fontes em HTML** ao exportar uma pasta de trabalho do Excel? Você não está sozinho. Quando você compartilha uma planilha como página da web, fontes ausentes podem transformar um relatório bem elaborado em uma bagunça – especialmente se o visualizador não tiver a tipografia original instalada.  

Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que mostra exatamente **como incorporar fontes em HTML** usando Aspose.Cells para .NET. Ao final, você será capaz de **exportar Excel para HTML**, **converter planilha para HTML** e **salvar a pasta de trabalho como HTML** com as fontes incorporadas diretamente no arquivo.

---

## O que você aprenderá

- Por que fontes incorporadas são importantes para exportações de Excel baseadas na web.  
- Como configurar `HtmlSaveOptions` para ativar a opção `EmbedFonts`.  
- Um programa C# completo que carrega uma pasta de trabalho, aplica as configurações e grava um arquivo HTML.  
- Dicas para lidar com fontes personalizadas, compatibilidade de versões e solução de problemas comuns.  

Não é necessário ter experiência prévia com Aspose.Cells, mas você deve ter um entendimento básico de C# e desenvolvimento .NET.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| **.NET 6.0 ou superior** | Runtime moderno; frameworks mais antigos podem não suportar os recursos mais recentes do Aspose.Cells. |
| **Aspose.Cells para .NET** (pacote NuGet `Aspose.Cells`) | Fornece a classe `HtmlSaveOptions` que precisamos. |
| **Uma fonte TrueType ou OpenType** que você deseja incorporar (ex.: `Arial.ttf`) | Apenas esses formatos de fonte podem ser incorporados ao arquivo HTML. |
| **Uma IDE** (Visual Studio, Rider, VS Code) | Facilita a execução e depuração do exemplo. |

Se ainda não instalou o pacote NuGet, execute:

```bash
dotnet add package Aspose.Cells
```

---

## Etapa 1: Carregar a Pasta de Trabalho que Você Deseja Converter

Primeiro, precisamos de uma instância `Workbook`. Você pode carregar um arquivo `.xlsx` existente, criar um do zero ou até mesmo obter dados de um banco de dados. Aqui está um exemplo mínimo que abre um arquivo chamado `Sample.xlsx` na pasta do projeto:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source Excel file
        var workbook = new Workbook("Sample.xlsx");
        // Continue with HTML conversion...
```

> **Por que esta etapa?**  
> O objeto `Workbook` é o ponto de entrada para todas as operações do Aspose.Cells. Sem ele você não pode acessar as planilhas, estilos ou dados que eventualmente se tornarão HTML.

---

## Etapa 2: Configurar as Opções de Salvamento HTML para **Incorporar Fontes em HTML**

Agora vem a linha mágica que responde à pergunta “como incorporar fontes html”. Criamos uma instância de `HtmlSaveOptions` e definimos `EmbedFonts` como `true`. Isso indica à biblioteca que incorpore os dados da fonte como regras CSS `@font-face` codificadas em Base64.

```csharp
        // Step 2: Set up HTML save options with embedded fonts
        var htmlOptions = new HtmlSaveOptions
        {
            // This flag ensures fonts are written directly into the HTML file
            EmbedFonts = true,

            // Optional: you can control whether to embed only used fonts
            // EmbedOnlyUsedFonts = true,

            // Optional: control the output folder for external resources
            ExportImagesAsBase64 = true
        };
```

> **Por que habilitar `EmbedFonts`?**  
> Quando o HTML resultante é aberto em uma máquina que não possui a fonte original, o navegador recorre a uma tipografia genérica. Incorporar garante fidelidade visual em todas as plataformas.

---

## Etapa 3: Salvar a Pasta de Trabalho como HTML

Com as opções preparadas, chamamos `Workbook.Save`, passando o nome de arquivo desejado e o objeto `HtmlSaveOptions`. A biblioteca faz o trabalho pesado – converte células, fórmulas e estilos em marcação HTML, e então insere os dados da fonte nas tags `<style>`.

```csharp
        // Step 3: Export the workbook to HTML with embedded fonts
        workbook.Save("output.html", htmlOptions);

        // Inform the user
        Console.WriteLine("Workbook successfully saved as HTML with embedded fonts.");
    }
}
```

> **O que você verá:**  
> Abra `output.html` em qualquer navegador moderno e perceberá a mesma tipografia do arquivo Excel original, mesmo que o visualizador não tenha a fonte instalada localmente.

---

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em um projeto de console:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook
        var workbook = new Workbook("Sample.xlsx");

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportImagesAsBase64 = true,
            // You can also set ExportActiveWorksheetOnly = true if you only need one sheet
        };

        // 3️⃣ Save the workbook as HTML
        workbook.Save("output.html", htmlOptions);

        Console.WriteLine("✅ Workbook saved as HTML with embedded fonts.");
    }
}
```

Execute o programa (`dotnet run`) e, em seguida, abra `output.html`. Você deverá ver uma réplica fiel da planilha original, completa com as fontes exatas que utilizou.

![Exemplo de saída com fontes incorporadas em HTML](embed-fonts-html.png "Captura de tela mostrando o arquivo HTML com fontes incorporadas")

*Texto alternativo da imagem: incorporar fontes em html – captura de tela da página HTML gerada preservando as fontes da planilha original.*

---

## Perguntas Frequentes & Casos Limite

### 1️⃣ **E se minha pasta de trabalho usar uma fonte personalizada que não está instalada no servidor?**  
Aspose.Cells só pode incorporar fontes que estejam disponíveis para o runtime. Instale o arquivo `.ttf` ou `.otf` na máquina que executa a conversão, ou copie‑o para o diretório do projeto e registre‑lo via `System.Drawing.Text.PrivateFontCollection` antes de chamar a operação de salvamento.

### 2️⃣ **Incorporar aumentará drasticamente o tamanho do arquivo?**  
Sim, cada fonte incorporada é codificada em Base64, o que adiciona aproximadamente 33 % de overhead. Se a pasta de trabalho usar muitas fontes grandes, considere habilitar `EmbedOnlyUsedFonts = true` para limitar o payload apenas às fontes realmente referenciadas na planilha.

### 3️⃣ **Posso ainda exportar imagens separadamente?**  
Definir `ExportImagesAsBase64 = true` (conforme mostrado acima) incorpora imagens, tornando o HTML realmente autônomo. Se preferir arquivos de imagem externos, defina essa propriedade como `false` e especifique `ExportImagesFolder` para controlar a pasta de saída.

### 4️⃣ **Esta abordagem é compatível com navegadores antigos?**  
A maioria dos navegadores modernos (Chrome, Edge, Firefox, Safari) suporta `@font-face` codificado em Base64. O Internet Explorer 11 também funciona, mas pode ser necessário garantir que o tipo MIME esteja correto. Para suporte legado, considere fornecer uma pilha de fontes de fallback no seu CSS.

### 5️⃣ **Como isso difere de um simples “exportar excel para html” sem incorporação?**  
Uma exportação simples grava o texto usando fontes web genéricas (`Arial`, `Helvetica`, etc.). O layout visual pode mudar, especialmente em relatórios corporativos que dependem de uma tipografia específica da marca. Incorporar elimina essa incerteza.

---

## Dicas Profissionais & Boas Práticas

- **Cache o HTML** se você gerar o mesmo relatório repetidamente. O processo de conversão, embora rápido, ainda consome ciclos de CPU.  
- **Valide a saída** com um validador HTML (por exemplo, o validador W3C) para detectar marcações estranhas que possam quebrar clientes de e‑mail.  
- **Combine com minificação de CSS** se for servir o HTML na web. Os dados de fonte já estão compactados, mas o CSS ao redor pode ser reduzido.  
- **Fique atento à licença**: Aspose.Cells requer uma licença válida para uso em produção; caso contrário, uma marca d’água aparecerá na saída HTML.  
- **Teste em múltiplos dispositivos** – especialmente navegadores móveis – para garantir que as fontes incorporadas sejam renderizadas corretamente em diferentes densidades de tela.

---

## Conclusão

Agora você tem uma solução completa, pronta‑para‑copiar, para **incorporar fontes em HTML** ao **exportar Excel para HTML**, **converter planilha para HTML** ou simplesmente **salvar a pasta de trabalho como HTML** com fidelidade tipográfica total. Ao ativar a flag `EmbedFonts` em `HtmlSaveOptions`, você elimina o temido problema de “fonte ausente” e entrega uma página web polida e autocontida a qualquer público.

Pronto para o próximo desafio? Experimente adicionar **gráficos interativos** à exportação HTML, ou teste a **conversão para PDF** para ver como as fontes incorporadas se comportam em outro formato. O mesmo padrão `HtmlSaveOptions` se aplica – basta trocar o tipo de saída.

Bom código, e que suas planilhas sempre apareçam exatamente como você pretende – não importa onde sejam visualizadas!

## Tutoriais Relacionados

- [Converter Excel para HTML em Java usando Aspose.Cells: Um Guia Passo a Passo](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Exportar Excel para HTML usando Aspose.Cells Java: Um Guia Passo a Passo](/cells/english/java/workbook-operations/export-excel-html-aspose-cells-java/)
- [Converter Excel para HTML com Dicas de Ferramentas usando Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/workbook-operations/excel-to-html-conversion-with-tooltips-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}