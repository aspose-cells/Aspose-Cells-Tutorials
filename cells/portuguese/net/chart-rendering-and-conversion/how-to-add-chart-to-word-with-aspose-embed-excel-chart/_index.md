---
category: general
date: 2026-10-01
description: Adicione gráficos ao Word com Aspose em apenas minutos. Aprenda a incorporar
  gráficos do Excel no Word, exportar gráficos do Excel para o Word, criar documentos
  Word com Aspose e salvar gráficos em documentos Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: pt
lastmod: 2026-10-01
og_description: Adicione gráfico ao Word com Aspose em minutos. Este guia mostra como
  incorporar gráfico do Excel no Word, exportar gráfico do Excel para Word, criar
  documento Word com Aspose e salvar o gráfico no documento Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Adicionar gráfico ao Word com Aspose – incorporar gráfico do Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Como adicionar gráfico ao Word com Aspose – incorporar gráfico do Excel
url: /pt/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar gráfico ao Word com Aspose – incorporar gráfico do Excel

Se você precisa **adicionar gráfico ao Word** rapidamente, este tutorial oferece uma solução completa e pronta‑para‑executar. Você verá como incorporar um gráfico do Excel em um arquivo Word, exportar o gráfico do Excel para o Word e, finalmente, **salvar documento Word com gráfico** com apenas algumas linhas de C#.

Incorporar gráficos é uma necessidade comum ao gerar relatórios, faturas ou dashboards programaticamente. Ao final deste guia você será capaz de **criar documento Word Aspose** que contém qualquer gráfico de uma pasta de trabalho do Excel, sem copiar‑colar manual.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+)
- Pacotes NuGet Aspose.Cells e Aspose.Words (instale via `dotnet add package Aspose.Cells` e `dotnet add package Aspose.Words`)
- Um arquivo Excel existente (`Chart.xlsx`) que contenha ao menos um gráfico
- Um ambiente de desenvolvimento como Visual Studio 2022 ou VS Code

## Adicionar gráfico ao Word com Aspose

Abaixo está o programa completo e autocontido. Copie‑o para um novo projeto de console, restaure os pacotes e execute. O programa carrega a pasta de trabalho Excel, cria um documento Word, insere o primeiro gráfico e salva o resultado.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Por que cada linha importa

1. **Carregando a pasta de trabalho** – `Workbook` analisa o arquivo Excel e fornece acesso programático às suas planilhas e gráficos.  
2. **Criando o documento Word** – `Document` é o ponto de entrada do Aspose.Words para qualquer tarefa de processamento de Word.  
3. **DocumentBuilder** – Esta classe auxiliar permite inserir conteúdo (texto, imagens, gráficos) na posição atual do cursor.  
4. **InsertChart** – A sobrecarga que aceita um objeto `Aspose.Cells.Chart` copia os dados, a formatação e as séries do gráfico diretamente para o arquivo Word. Nenhuma conversão intermediária de imagem é necessária, preservando a qualidade vetorial.  
5. **Save** – `Save` grava o pacote .docx no disco, concluindo a etapa de **salvar documento Word com gráfico**.

#### Saída esperada

Após executar o programa, abra `Chart.docx`. Você verá exatamente o gráfico que estava armazenado em `Chart.xlsx`, posicionado onde o builder foi colocado (no início do documento). O gráfico permanece totalmente editável dentro do Word (você pode redimensionar, mudar cores ou modificar a fonte de dados).

## Incorporar gráfico do Excel no Word

Se precisar incorporar mais de um gráfico, repita a chamada `InsertChart` para cada objeto de gráfico. Por exemplo, para incorporar todos os gráficos da primeira planilha:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Dica profissional:** Use `builder.Writeln()` para inserir uma quebra de parágrafo, garantindo que cada gráfico comece em uma nova linha.

## Exportar gráfico Excel Word – lidando com várias planilhas

Quando os gráficos estão distribuídos em várias planilhas, itere sobre a coleção `Worksheets` da pasta de trabalho:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Esta abordagem **exporta gráfico Excel Word** para qualquer layout de pasta de trabalho, tornando a solução robusta para relatórios complexos.

## Criar documento Word Aspose – personalizando a aparência

Você pode controlar o tamanho e a posição de cada gráfico inserido modificando o `Shape` retornado por `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Ajustar `WrapType` para `Inline` garante que o gráfico se comporte como um parágrafo normal, o que costuma ser desejável em geração automática de documentos.

## Salvar documento Word com gráfico – boas práticas

- **Use um nome de arquivo descritivo** (`Report_Q1_2026.docx`) para facilitar o versionamento.  
- **Libere os objetos** quando terminar, especialmente em processos em lote de grande volume:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Valide o resultado** programaticamente se você gerar muitos arquivos:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Perguntas frequentes & casos especiais

| Pergunta | Resposta |
|----------|----------|
| *Posso inserir um gráfico que não seja o primeiro na planilha?* | Sim. Acesse‑o por índice: `sheet.Charts[2]` para o terceiro gráfico. |
| *E se o gráfico do Excel usar uma fonte de dados que não está na pasta de trabalho?* | Aspose.Cells incorpora os dados diretamente no objeto do gráfico, então o gráfico permanece funcional mesmo se a faixa de origem for removida. |
| *Preciso de uma licença para Aspose?* | Uma avaliação gratuita funciona, mas a versão licenciada remove a marca d'água de avaliação e desbloqueia todos os recursos. |
| *O gráfico será editável no Word após a inserção?* | O gráfico é inserido como um gráfico nativo do Word, portanto os usuários podem editar séries, títulos e estilos usando a interface do Word. |
| *Como inserir um gráfico como imagem em vez de um gráfico nativo?* | Use `builder.InsertImage(chart.ToImage())` para incorporar uma imagem raster. Isso é útil quando você deseja preservar a renderização visual exata sem a editabilidade no nível do Word. |

## Exemplo completo (copiar‑colar)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Executar o código gera um arquivo Word (`ReportWithCharts.docx`) que contém os resultados de **adicionar gráfico ao Word** para cada gráfico na pasta de trabalho de origem.

## Conclusão

Agora você sabe como **adicionar gráfico ao Word** usando Aspose.Cells e Aspose.Words, como **incorporar gráfico do Excel no Word**, **exportar gráfico Excel Word**, **criar documento Word Aspose** e, finalmente, **salvar documento Word com gráfico**. A abordagem funciona tanto para cenários de um único gráfico quanto para pastas de trabalho complexas com muitos gráficos em várias planilhas.

Próximos passos que você pode explorar:

- Aplicar estilos personalizados aos gráficos inseridos (cores, fontes) via a API `Chart`.  
- Combinar a inserção de gráficos com geração de texto para produzir relatórios totalmente automatizados.  
- Usar Aspose.Slides se precisar  

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}