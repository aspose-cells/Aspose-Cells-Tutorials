---
category: general
date: 2026-10-26
description: Aprenda a exportar gráficos do Excel para o PowerPoint com C#. Preserve
  a editabilidade das formas e salve como PPTX em poucas linhas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: pt
lastmod: 2026-10-26
og_description: Exporte gráficos do Excel para PowerPoint com C#. Este guia mostra
  como manter as formas editáveis e salvar como PPTX usando Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Exportar gráficos do Excel para PowerPoint com C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Como exportar gráficos do Excel para o PowerPoint usando C#
url: /pt/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar gráficos do Excel para PowerPoint usando C#

Se você precisa **exportar gráficos do Excel para PowerPoint**, este guia o conduz por uma solução completa, pronta‑para‑executar. Seja construindo um painel de relatórios ou automatizando apresentações, você verá como algumas linhas de código C# mantêm as formas dos seus gráficos totalmente editáveis após a conversão.

Neste tutorial você aprenderá a:

* Carregar uma pasta de trabalho do Excel existente que contém gráficos.  
* (Opcionalmente) ajustar as configurações da pasta de trabalho antes da conversão.  
* Salvar a pasta de trabalho como um arquivo PowerPoint preservando a editabilidade das formas.  

Tudo isso é feito com **Aspose.Cells for .NET**, uma biblioteca que lida com a conversão de Excel‑para‑PowerPoint sem exigir o Microsoft Office no servidor.

## O que você precisará

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 or later | Tempo de execução moderno com todos os recursos da linguagem |
| Visual Studio 2022 (or any IDE) | Editor e depurador convenientes |
| **Aspose.Cells for .NET** NuGet package | Fornece a classe `Workbook` e suporte a `SaveFormat.Pptx` |
| An Excel file (`ChartAndShapes.xlsx`) that contains at least one chart | Fonte dos gráficos que você deseja exportar |

> **Dica profissional:** Use a versão gratuita **Aspose.Cells Evaluation** para testar o código; uma chave de licença remove a marca d'água de avaliação.

```bash
dotnet add package Aspose.Cells
```

## Exportar gráficos do Excel para PowerPoint – fluxo completo

A seguir está o código de ponta a ponta que realiza a exportação enquanto **preserva a editabilidade das formas**. Cada etapa é explicada em detalhes.

### Etapa 1: Carregar a pasta de trabalho do Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*A classe `Workbook` representa o arquivo Excel completo. Carregar o arquivo lê todas as planilhas, gráficos e formas para a memória, o que é necessário para qualquer manipulação posterior.*

### Etapa 2: (Opcional) Ajustar as configurações da pasta de trabalho

Na maioria dos casos, as configurações padrão são suficientes para uma exportação limpa. No entanto, se precisar alterar o modo de cálculo, a configuração de página ou ocultar determinadas planilhas, você pode fazer isso aqui.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Por que isso importa:** Ajustar as configurações antes da conversão garante que os slides gerados reflitam exatamente o estado desejado, especialmente quando fórmulas ou planilhas ocultas podem afetar os dados do gráfico.

### Etapa 3: Salvar a pasta de trabalho como um arquivo PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*A constante `SaveFormat.Pptx` indica ao Aspose.Cells que deve gerar uma apresentação PowerPoint. Internamente, a biblioteca converte cada gráfico do Excel em uma forma do PowerPoint que permanece totalmente editável no Microsoft PowerPoint.*

### Etapa 4: Verificar o resultado

Abra `Shapes.pptx` no PowerPoint e:

1. Selecione um gráfico em qualquer slide.  
2. Clique com o botão direito → **Edit Data**.  
3. Confirme que a tabela de dados do gráfico aparece e que você pode modificar os valores.

Se o gráfico abrir o painel **Edit Data**, a conversão foi bem-sucedida e a **editabilidade das formas** foi preservada.

![Exemplo de exportação de gráficos do Excel para PowerPoint](export-excel-charts-to-powerpoint.png){.img-fluid alt="Exemplo de exportação de gráficos do Excel para PowerPoint"}

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Correção |
|----------|-------|----------|
| Gráficos aparecem como imagens estáticas | Uso de uma versão mais antiga do Aspose.Cells que não possui suporte à exportação PPTX | Atualize para a versão mais recente do Aspose.Cells 23.x ou posterior |
| Dados ausentes no gráfico do PowerPoint | Pasta de trabalho não calculada completamente antes da exportação | Chame `workbook.CalculateFormula()` antes de `Save` |
| Formas não são editáveis | Salvando com `SaveFormat.Xlsx` em vez de `SaveFormat.Pptx` | Certifique-se de passar `SaveFormat.Pptx` para `Workbook.Save` |
| Exceção de licença em tempo de execução | Versão de avaliação sem licença registrada | Registre sua licença com `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Caso especial: Exportar várias planilhas com gráficos separados

Se o seu arquivo Excel contém várias planilhas, cada uma com seu próprio gráfico, o Aspose.Cells cria automaticamente um slide separado para cada gráfico. Você pode controlar a ordem dos slides reorganizando as planilhas antes da operação de salvamento.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Dica de desempenho: Transmitir a saída em vez de gravar no disco

Ao gerar arquivos PowerPoint em uma API web, evite arquivos temporários gravando em um `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Exemplo completo e executável

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Saída esperada:** O console imprime a mensagem de confirmação, e `Shapes.pptx` abre no PowerPoint com cada gráfico do Excel aparecendo em seu próprio slide. Selecionar um gráfico permite editar seus dados, confirmando que a **editabilidade das formas** foi mantida.

## Recapitulação e próximos passos

Agora você sabe como **exportar gráficos do Excel para PowerPoint** com C# mantendo os gráficos totalmente editáveis. O núcleo da solução é o método `Workbook.Save` com `SaveFormat.Pptx`, um recurso da **exportação do Aspose.Cells** que abstrai o complexo tratamento do Open XML.

De aqui, você pode explorar:

* Adicionar títulos ou notas de slide personalizados usando a API **Aspose.Slides**.  
* Converter outros objetos do Excel (tabelas, imagens) juntamente com os gráficos.  
* Automatizar o processamento em lote de várias pastas de trabalho em um serviço em segundo plano.

Sinta‑se à vontade para experimentar as configurações opcionais mostradas acima e integrar este padrão em seus pipelines de relatórios para geração rápida e confiável de PowerPoint.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Exportar gráfico do Excel para PowerPoint com C# – guia completo do Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Como Exportar Excel para PowerPoint com C# – Guia Completo](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Como Exportar Formas do Excel para PowerPoint – Guia Completo](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}