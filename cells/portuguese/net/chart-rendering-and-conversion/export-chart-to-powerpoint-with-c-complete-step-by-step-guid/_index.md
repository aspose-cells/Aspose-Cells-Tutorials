---
category: general
date: 2026-02-26
description: Exportar gráfico para PowerPoint a partir do Excel usando C#. Aprenda
  como converter Excel para PowerPoint, salvar Excel como PowerPoint e manter as formas
  editáveis.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: pt
og_description: Exportar gráfico para PowerPoint a partir do Excel usando C#. Este
  guia mostra como converter Excel para PowerPoint, salvar a pasta de trabalho como
  PPTX e manter as formas editáveis.
og_title: Exportar Gráfico para PowerPoint com C# – Tutorial Completo de Programação
tags:
- Aspose.Cells
- C#
- Office Automation
title: Exportar Gráfico para PowerPoint com C# – Guia Completo Passo a Passo
url: /pt/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Gráfico para PowerPoint – Tutorial Completo de Programação

Já se perguntou como **exportar gráfico para PowerPoint** sem perder a editabilidade? Em muitos cenários de relatórios você precisa de um gráfico ao vivo dentro de um slide, mas copiar e colar manualmente é um incômodo. A boa notícia é que você pode fazer isso programaticamente com algumas linhas de C#.

Neste guia vamos percorrer todo o processo: desde o carregamento de uma pasta de trabalho Excel que contém um gráfico com uma caixa de texto, configurando a exportação para que caixas de texto e formas permaneçam editáveis, e finalmente salvando o resultado como um arquivo **PowerPoint**. Ao final, você também saberá como **converter Excel para PowerPoint**, **salvar Excel como PowerPoint**, e ainda ajustar as opções para cenários de borda.

## O que Você Precisa

- **Aspose.Cells for .NET** (versão 23.10 ou posterior). É a biblioteca que torna a conversão simples.
- **.NET 6+** runtime – qualquer SDK recente funciona.
- Um arquivo Excel simples (`ChartWithTextbox.xlsx`) que contenha ao menos um gráfico e uma caixa de texto.
- Visual Studio ou sua IDE favorita.

Nenhum pacote NuGet adicional é necessário além do Aspose.Cells, mas ter uma compreensão básica da sintaxe C# certamente ajuda.

## Exportar Gráfico para PowerPoint – Passo a Passo

A seguir, dividimos a solução em etapas discretas e fáceis de seguir. Cada etapa inclui o código exato que você precisa, além de um pequeno parágrafo “por quê” que explica o raciocínio por trás dela.

### Etapa 1: Carregar a Pasta de Trabalho Excel que Contém o Gráfico

Primeiro precisamos trazer o arquivo de origem para a memória. Usando `Workbook` do Aspose.Cells lê toda a planilha, incluindo gráficos, imagens e objetos incorporados.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Por que isso importa:* Se a pasta de trabalho for aberta sem especificar o caminho corretamente, você receberá uma `FileNotFoundException`. A verificação rápida evita que você exporte um slide vazio mais tarde.

### Etapa 2: Preparar Opções de Apresentação para Manter Formas Editáveis

Aspose.Cells permite decidir se caixas de texto, formas e até o próprio gráfico permanecem **editáveis** após a exportação. Definir `ExportTextBoxes` e `ExportShapes` como `true` preserva esses objetos como elementos nativos do PowerPoint em vez de achatá‑los em uma imagem estática.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Por que isso importa:* Se você deixar esses flags nos valores padrão (`false`), o slide resultante conterá um bitmap do gráfico, impossibilitando editar as séries ou mudar a legenda depois. Habilitar ambas as opções fornece um verdadeiro gráfico PowerPoint que se comporta exatamente como um que você desenharia manualmente.

### Etapa 3: Converter Excel para PowerPoint e Salvar o Arquivo

Agora invocamos o método `Save`, passando o enum `SaveFormat.Pptx` e as opções que acabamos de configurar. A biblioteca cuida da tradução do objeto de gráfico do Excel para uma forma de gráfico do PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Por que isso importa:* A chamada `Save` faz todo o trabalho pesado — mapeia séries do Excel para séries do PowerPoint, preserva a formatação dos eixos e copia quaisquer caixas de texto vinculadas. Depois que esta linha for executada, você terá um arquivo `.pptx` totalmente editável pronto para ser aberto no Microsoft PowerPoint.

### Verificar o Resultado

Abra `Result.pptx` no PowerPoint. Você deverá ver um slide que contém:

- O gráfico original, ainda vinculado aos seus dados (você pode dar duplo‑clique para editar as séries).
- Qualquer caixa de texto que estava na planilha Excel, agora uma caixa de texto nativa do PowerPoint.
- O layout do slide é escolhido automaticamente (geralmente um slide em branco).

Se notar elementos ausentes, verifique se a pasta de trabalho de origem realmente continha objetos visíveis e se `ExportTextBoxes` / `ExportShapes` foram definidos como `true`.

### Converter Excel para PowerPoint: Manipulando Múltiplas Planilhas

Frequentemente uma pasta de trabalho contém mais de uma planilha, cada uma com seu próprio gráfico. Por padrão o Aspose.Cells exportará **todos** os gráficos de **todas** as planilhas em slides separados. Se você precisar apenas de um subconjunto, pode filtrá‑los antes de salvar:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Dica de especialista:* Definir `chart.IsVisible = false` é mais barato que remover o gráfico completamente, e permite alternar a inclusão sem modificar o arquivo fonte.

### Salvar Excel como PowerPoint – Personalizando o Tamanho do Slide

O PowerPoint usa, por padrão, um slide de 10 polegadas por 5,63 polegadas. Se o seu gráfico parecer apertado, você pode mudar as dimensões do slide via o objeto `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Agora o gráfico exportado terá mais espaço, e quaisquer caixas de texto manterão seu layout original.

### Como Converter Excel para PPT: Lidando com Objetos Ocultos

Linhas, colunas ou formas ocultas podem às vezes se infiltrar na exportação. Para removê‑las, execute uma limpeza rápida antes de salvar:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Esta etapa nem sempre é necessária, mas impede lacunas inesperadas no seu deck final de slides.

### Salvar Pasta de Trabalho como PPTX – Exemplo Completo Funcional

Juntando tudo, aqui está um programa de console pronto‑para‑executar que demonstra todo o fluxo:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Executar este programa criará `Result.pptx` com um gráfico e uma caixa de texto editáveis, exatamente o que você esperaria ao **salvar pasta de trabalho como pptx** manualmente.

![Exemplo de exportação de gráfico para PowerPoint](/images/export-chart-to-powerpoint.png "Exportar gráfico para PowerPoint – slide editável")

## Perguntas Frequentes & Casos de Borda

**E se o arquivo Excel contiver um gráfico com uma fonte de dados externa vinculada?**  
Aspose.Cells copia os valores *atuais* dos dados para o gráfico do PowerPoint. Ele **não** preserva o vínculo externo, porque o PowerPoint não pode referenciar uma conexão de dados do Excel da mesma forma. Se precisar de atualizações ao vivo, considere incorporar o arquivo Excel original no PPTX como um objeto OLE.

**Posso exportar um gráfico que usa um tema personalizado?**  
Sim. A biblioteca tenta mapear as cores do tema do Excel para os slots de tema do PowerPoint. Para paletas muito customizadas pode ser necessário ajustar as cores após a exportação usando a própria API do PowerPoint (por exemplo, Aspose.Slides).

**Existe um limite no número de gráficos?**  
Praticamente nenhum — o Aspose.Cells faz streaming dos dados, então mesmo uma pasta de trabalho com dezenas de gráficos será exportada, embora o tamanho do PPTX resultante cresça linearmente.

**Preciso de licença para o Aspose.Cells?**  
Uma avaliação gratuita funciona, mas adiciona uma marca d'água no primeiro slide. Para uso em produção, obtenha uma licença adequada para remover a marca d'água e desbloquear desempenho total.

## Recapitulação

Cobremos como **exportar gráfico para PowerPoint** usando C#, demonstramos o código exato para carregar uma pasta de trabalho Excel, configurar `PresentationOptions` para manter caixas de texto e formas editáveis, e finalmente salvar o resultado como um `.pptx`. Você também aprendeu como **converter Excel para PowerPoint**, **salvar Excel como PowerPoint**, e respondeu à pergunta “**como converter Excel para ppt**” com um exemplo completo e executável.

## O Que Vem a Seguir?

- **Salvar pasta de trabalho como PPTX** com múltiplos slides: iterar sobre cada planilha e chamar `Save` com `PresentationOptions` para cada uma.
- Explore **Aspose.Slides** se precisar modificar programaticamente o PPTX gerado (adicionar transições, notas do apresentador, etc.).
- Experimente exportar **gráficos dinâmicos** ou **gráficos 3‑D** — as mesmas opções se aplicam, mas pode ser necessário ajustar a formatação dos eixos depois.

Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte a documentação oficial do Aspose.Cells para as últimas mudanças de API. Boa codificação e aproveite para transformar aqueles gráficos do Excel em apresentações PowerPoint polidas com apenas algumas linhas de C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}