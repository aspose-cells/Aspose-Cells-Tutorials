---
category: general
date: 2026-06-05
description: Como exportar gráficos do PowerPoint usando C#. Inclui exportação de
  objetos OLE e torna os gráficos editáveis no PPTX resultante – passo a passo.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: pt
og_description: Como exportar gráficos do PowerPoint usando C#. Aprenda a exportar
  objetos OLE e tornar os gráficos editáveis no PPTX salvo – passo a passo.
og_title: Como Exportar Gráficos – Guia Completo de PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Como Exportar Gráficos – Guia Completo de PowerPoint em C#
url: /pt/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Gráficos – Guia Completo de PowerPoint C#

Já se perguntou **como exportar gráficos** de um deck PowerPoint sem perder a capacidade de editá‑los posteriormente? Você não está sozinho. Em muitos pipelines de relatórios os dados dos gráficos vivem dentro do PPTX, e depois de entregar o arquivo, o destinatário costuma precisar ajustar um valor ou mudar um rótulo. A boa notícia é que, com algumas linhas de C#, você pode preservar a editabilidade e ainda exportar objetos OLE incorporados ao mesmo tempo.

Neste tutorial, percorreremos um exemplo prático e pronto‑para‑executar que mostra **como exportar gráficos**, como **exportar objetos OLE** e como **tornar os gráficos editáveis** no arquivo de saída. Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto .NET que use a biblioteca Aspose.Slides.

> **Dica profissional:** Se você é novo no Aspose.Slides, certifique‑se de que adicionou o pacote NuGet `Aspose.Slides.NET` ao seu projeto — caso contrário o código não compilará.

## O que Você Precisa

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Runtimes modernos oferecem melhor desempenho e gerenciamento de pacotes mais fácil. |
| Aspose.Slides for .NET (latest version) | Esta biblioteca fornece as classes `Presentation` e `PptxSaveOptions` que usaremos. |
| A sample PowerPoint file with at least one chart | A demonstração funciona em qualquer `.pptx` que contenha um gráfico; você verá a editabilidade após a exportação. |
| An IDE (Visual Studio, Rider, or VS Code) | Útil para depuração rápida e visualização do arquivo gerado. |

Nenhuma ferramenta de terceiros adicional é necessária — tudo é tratado pela API Aspose.

## Etapa 1 – Carregar a Apresentação de Origem

Primeiro, precisamos trazer o PPTX original para a memória. Pense nisso como abrir um documento no Word antes de começar a editar.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Por que isso importa:** O objeto `Presentation` é o ponto de entrada para todas as operações subsequentes. Ele analisa o arquivo, constrói um modelo de objeto de slides, formas, gráficos e objetos OLE, e mantém tudo em um estado mutável.

## Etapa 2 – Criar Opções de Salvamento e Habilitar Gráficos Editáveis

Por padrão, ao chamar `Save` a biblioteca achata os gráficos em imagens estáticas. Para mantê‑los editáveis, você deve alternar o sinalizador `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Como funciona:** Quando `ExportEditableCharts` está `true`, a biblioteca grava a definição XML do gráfico (`chart.xml`) no PPTX em vez de rasterizá‑lo. O PowerPoint então lê esse XML e permite que o usuário abra o editor de gráficos.

## Etapa 3 – Ativar a Exportação de Objetos OLE Incorporados

Muitas apresentações incorporam planilhas do Excel, diagramas do Visio ou até arquivos PDF como objetos OLE. Se você quiser que eles sobrevivam ao ciclo completo, habilite `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **O que realmente significa “exportar objetos OLE”:** O pacote OLE é armazenado como um blob binário dentro do PPTX. Definir esse sinalizador preserva o binário original, permitindo que o destinatário dê um duplo‑clique no objeto e o abra em sua aplicação nativa (por exemplo, Excel). Sem isso, o objeto OLE seria removido, quebrando links e perdendo dados.

## Etapa 4 – Salvar a Apresentação com as Opções Configuradas

Agora que preparamos as opções, basta dizer ao Aspose para gravar o arquivo.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Resultado:** `editable.pptx` contém os mesmos slides que `input.pptx`, mas qualquer gráfico pode ser editado diretamente no PowerPoint, e quaisquer objetos OLE incorporados permanecem intactos.

### Exemplo Completo em Funcionamento

Abaixo está o programa completo e autocontido que você pode compilar e executar. Ele inclui instruções `using`, descarte adequado e comentários que explicam cada linha.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Saída esperada:** Após executar o programa, abra `editable.pptx` no PowerPoint. Clique com o botão direito em qualquer gráfico → *Edit Data* → o editor de gráficos abre, confirmando que **tornar os gráficos editáveis** foi bem‑sucedido. Dê um duplo‑clique em uma planilha Excel incorporada, e ela abrirá no Excel, provando que **exportar objetos OLE** funcionou.

![diagrama de como exportar gráficos](https://example.com/images/export-charts.png "como exportar gráficos – PowerPoint após exportação")

*(Texto alternativo: como exportar gráficos – captura de tela do PowerPoint com gráfico editável e objeto OLE)*

## Perguntas Frequentes & Casos Limites

### E se o arquivo de origem não tiver gráficos?

O código ainda será executado; `ExportEditableCharts` simplesmente não tem efeito porque não há nada para converter. Nenhum erro é lançado.

### Posso exportar apenas gráficos específicos?

Sim. Em vez de usar o sinalizador global `ExportEditableCharts`, você pode iterar através de `presentation.Slides` e definir `Chart.IsEditable = true` em objetos de gráfico individuais antes de salvar. Isso lhe dá controle granular.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Habilitar a exportação OLE aumenta o tamanho do arquivo?

Um pouco. Os fluxos binários OLE são armazenados literalmente, portanto o PPTX resultante pode ficar alguns kilobytes maior. Na maioria dos cenários de negócios, a troca vale a pena porque você mantém a editabilidade total.

### Quais versões do PowerPoint podem abrir o arquivo resultante?

Qualquer versão que suporte o padrão OOXML (PowerPoint 2007 e posteriores). O recurso de gráfico editável depende do editor de gráficos nativo introduzido no Office 2007, portanto binários mais antigos como `.ppt` não se beneficiarão.

## Dicas para Código Pronto para Produção

| Tip | Reason |
|-----|--------|
| Use blocos `using` (conforme mostrado) para descartar objetos `Presentation`. | Previne vazamentos de memória, especialmente ao processar muitos arquivos em lote. |
| Valide caminhos de arquivo antes de carregar. | Evita `FileNotFoundException` que faria um serviço em segundo plano travar. |
| Registre as configurações `ExportEditableCharts` e `ExportOLEObjects`. | Útil para solução de problemas quando um usuário relata gráficos não editáveis. |
| Capture `Aspose.Slides.Exception` separadamente. | Fornece mensagens de erro mais claras da biblioteca (por exemplo, tipos de gráfico não suportados). |
| Considere `PptxCompressionLevel` se o tamanho do arquivo for importante. | Você pode comprimir a saída mantendo a editabilidade. |

## Recapitulação – O que Conquistamos

Começamos com uma pergunta clara: **como exportar gráficos** de um arquivo PowerPoint mantendo‑os editáveis e preservando objetos OLE incorporados. Ao carregar a apresentação, configurar `PptxSaveOptions` (`ExportEditableCharts = true` e `ExportOLEObjects = true`) e salvar o arquivo, agora temos um PPTX que satisfaz ambos os requisitos. O mesmo padrão pode ser reutilizado para conversões em lote, pipelines de CI ou qualquer ferramenta de relatório automatizada.

## O que Explorar a Seguir?

- **Exportar gráficos como imagens** para relatórios estáticos (`saveOptions.ExportEditableCharts = false`).  
- **Converter PPTX para PDF** preservando gráficos vetoriais (`PdfSaveOptions`).  
- **Manipular dados de gráficos programaticamente** (por exemplo, atualizar valores de séries antes da exportação).  
- **Integrar com Azure Functions** para fornecer uma API de exportação de gráficos sob demanda.

Sinta‑se à vontade para experimentar e nos informe quais casos limites você encontrar. Boa codificação, e que todos os seus gráficos permaneçam editáveis!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar Gráficos do Excel para PDF Usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Como Converter Gráficos do Excel para SVG Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Como Aplicar Temas a Gráficos do Excel Usando Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}