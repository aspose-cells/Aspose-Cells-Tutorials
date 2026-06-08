---
category: general
date: 2026-06-08
description: Crie opções de salvamento em HTML no C# para incorporar todas as fontes
  e salvar a pasta de trabalho como HTML. Aprenda como exportar uma pasta de trabalho
  do Excel para HTML com um exemplo simples e completo.
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: pt
og_description: Crie opções de salvamento em HTML no C# para incorporar todas as fontes
  e exportar a pasta de trabalho do Excel para HTML. Este guia orienta você passo
  a passo em uma solução completa, pronta para usar.
og_title: Criar Opções de Salvamento de HTML em C# – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: Criar opções de salvamento de HTML em C# – Guia completo
url: /pt/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Opções de Salvamento HTML em C# – Tutorial Completo

Já se perguntou como **criar opções de salvamento HTML** que mantenham cada fonte exatamente como aparece no Excel? Você não está sozinho. Muitos desenvolvedores se deparam com o problema de que o HTML exportado perde fontes personalizadas, deixando a página sem graça. A boa notícia? Com apenas algumas linhas de C# você pode **incorporar todas as fontes no HTML** e **salvar a pasta de trabalho como HTML** sem complicações.

Neste guia vamos percorrer todo o processo de **exportar pasta de trabalho Excel para HTML** usando Aspose.Cells. Ao final, você terá um programa autônomo e executável que não só cria as opções corretas, mas também explica *por que* cada configuração importa. Sem peças faltando, sem desvios “consulte a documentação” — apenas uma solução clara de ponta a ponta.

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

* .NET 6.0 SDK (ou qualquer versão recente do .NET) – o código funciona tanto no .NET Core quanto no .NET Framework.  
* O pacote NuGet **Aspose.Cells** – `dotnet add package Aspose.Cells`.  
* Um entendimento básico da sintaxe C# – se você consegue escrever um `Console.WriteLine`, está pronto para prosseguir.  

É só isso. Nenhuma ferramenta extra, nenhum arquivo de configuração obscuro.

## Passo 1: Configurar o Projeto e Carregar uma Pasta de Trabalho

Primeiro de tudo: precisamos de um projeto de console e de uma pasta de trabalho para trabalhar. Se você já tem um arquivo Excel, ótimo — caso contrário, o exemplo cria um na hora.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**Por que fazemos isso:** Carregar uma pasta de trabalho nos dá algo para exportar. Adicionar uma fonte personalizada (`Comic Sans MS`) torna a configuração *incorporar todas as fontes* visível no HTML gerado.

## Passo 2: **Criar Opções de Salvamento HTML** – O Núcleo da Tarefa

Agora chegamos ao coração da questão: configurar `HtmlSaveOptions`. Este objeto indica ao Aspose.Cells exatamente como o HTML deve ser escrito.

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**Por que `EmbedAllFonts = true` importa:** Quando você abre o HTML resultante em um navegador, as fontes personalizadas já estão incorporadas no arquivo. Isso significa que a página tem a mesma aparência da origem Excel, mesmo em máquinas que não têm a fonte instalada.

## Passo 3: **Salvar a Pasta de Trabalho como HTML** Usando as Opções Configuradas

Com as opções prontas, podemos finalmente **salvar a pasta de trabalho como HTML**. A assinatura do método aceita o caminho do arquivo, o formato desejado e o objeto de opções que acabamos de montar.

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**O que acontece nos bastidores?** Aspose.Cells renderiza cada célula, converte as definições de fonte para Base64 e as injeta em um bloco `<style>`. O `EmbeddedWorkbook.html` resultante é um único arquivo autônomo — sem arquivos `.css` ou fontes externos.

## Exemplo Completo Funcionando

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em `Program.cs` e executar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### Saída Esperada

Ao executar o programa, ele gera `EmbeddedWorkbook.html` na pasta de execução. Abra‑o em qualquer navegador moderno e você verá o texto **“Hello, Aspose.Cells!”** renderizado em **Comic Sans MS**, mesmo que seu sistema não tenha essa fonte instalada. Se inspecionar o código‑fonte HTML, perceberá um bloco `<style>` com uma regra `@font-face` contendo uma enorme string Base64 — essa é a fonte incorporada.

![Create HTML Save Options diagram](image.png "Diagram showing HTML export flow"){: alt="Create HTML Save Options flowchart"}

*O texto alternativo inclui a palavra‑chave principal para SEO.*

## Perguntas Frequentes & Casos Limites

### E se a pasta de trabalho contiver muitas fontes diferentes?

Incorporar *todas* as fontes pode inflar o tamanho do HTML drasticamente (cada fonte é codificada em Base64). Se o tamanho do arquivo se tornar um problema, considere definir `EmbedAllFonts = false` e incorporar manualmente apenas as fontes críticas via `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;`.

### Isso funciona com arquivos Excel mais antigos (`.xls`)?

Absolutamente. Aspose.Cells abstrai o formato de origem, então, seja um `.xlsx`, `.xls` ou até um CSV, a etapa de **exportar pasta de trabalho Excel para html** se comporta da mesma forma.

### Posso controlar a pasta de saída dinamicamente?

Claro — basta substituir o `outputPath` codificado por algo como:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

Dessa forma você pode **salvar a pasta de trabalho como HTML** onde precisar.

### E quanto a imagens ou gráficos dentro da pasta de trabalho?

`HtmlSaveOptions` também trata imagens, gráficos e até fórmulas. Por padrão, eles são renderizados como PNGs incorporados no HTML. Se preferir arquivos externos, altere `htmlOptions.ExportImagesAsBase64 = false`.

## Dicas Profissionais

* **Dica de desempenho:** Reutilize uma única instância de `HtmlSaveOptions` se estiver exportando muitas pastas de trabalho em um loop — gera menos lixo.  
* **Dica de teste:** Use um navegador headless (por exemplo, Puppeteer) para verificar automaticamente se as fontes incorporadas são renderizadas corretamente.  
* **Verificação de versão:** O sinalizador `EmbedAllFonts` foi introduzido no Aspose.Cells 20.9. Certifique‑se de que seu pacote NuGet está atualizado.

## Conclusão

Agora você sabe exatamente como **criar opções de salvamento HTML** em C# que **incorporam todas as fontes no HTML**, e viu uma maneira prática de **salvar a pasta de trabalho como HTML** para qualquer arquivo Excel. Este exemplo completo, pronto para execução, cobre o *o quê*, *por quê* e *como* da **exportar pasta de trabalho Excel para HTML**, oferecendo uma base sólida para cenários mais avançados, como processamento em lote ou estilos personalizados.

Pronto para o próximo passo? Experimente exportar uma pasta de trabalho que contenha gráficos, ou teste diferentes propriedades de `HtmlSaveOptions` como `ExportImagesAsBase64` ou `CssClassPrefix`. O mesmo padrão se aplica — crie as opções, ajuste os flags e chame `wb.Save`. Boa codificação, e que suas exportações HTML sempre pareçam exatamente como as planilhas Excel originais!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Prefixando Estilos de Elementos de Tabela com Opções de Salvamento HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [Definir Fonte Padrão na Conversão de Excel para HTML com Aspose.Cells para .NET \| Guia de Operações de Pasta de Trabalho](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Exportar Pasta de Trabalho Excel e Propriedades da Planilha para HTML Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}