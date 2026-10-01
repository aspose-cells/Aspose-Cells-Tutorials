---
category: general
date: 2026-02-26
description: Exportar a pasta de trabalho para PDF com fontes incorporadas e também
  exportar gráficos para PowerPoint em C#. Aprenda a copiar a planilha de tabela dinâmica
  e salvar a pasta de trabalho como PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: pt
og_description: Exportar a pasta de trabalho para PDF com fontes incorporadas e também
  exportar gráficos para PowerPoint em C#. Siga o guia passo a passo para copiar tabelas
  dinâmicas e salvar como PPTX.
og_title: Exportar Pasta de Trabalho para PDF – Guia Completo de C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Exportar Pasta de Trabalho para PDF – Guia Completo de C#
url: /pt/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Pasta de Trabalho para PDF – Guia Completo em C#

Exportar pasta de trabalho para PDF é uma necessidade comum quando você precisa compartilhar relatórios com partes interessadas que podem não ter o Excel instalado. Neste tutorial também mostraremos como **exportar gráficos para PowerPoint**, copiar uma **planilha de tabela dinâmica** e incorporar fontes para que o PDF tenha exatamente a mesma aparência do seu design na tela.  

Já se perguntou por que alguns PDFs perdem o layout original ou por que os slides do PowerPoint acabam com formas ausentes? A resposta geralmente está nas opções ausentes durante o processo de exportação. Ao final deste guia você terá um único método reutilizável em C# que resolve todos esses pontos críticos — nada de copiar‑colar manual ou mexer nas configurações de exportação.

## O que você aprenderá

- Como criar uma pasta de trabalho, adicionar expressões Smart Marker e processá‑las.  
- Como **copiar uma planilha de tabela dinâmica** sem quebrar a fonte de dados.  
- Como **exportar gráficos, formas e caixas de texto** para uma apresentação PowerPoint mantendo‑os editáveis.  
- Como **incorporar fontes padrão** durante a exportação para PDF para renderização consistente em qualquer máquina.  
- Como **salvar a pasta de trabalho como PPTX** usando a abordagem `save workbook as pptx`.  

Tudo isso funciona com as bibliotecas mais recentes Aspose.Cells e Aspose.Slides .NET (versão 23.11 no momento da escrita). Sem ferramentas externas, sem scripts de pós‑processamento — apenas C# puro.

> **Dica profissional:** Se você já usa Aspose no seu projeto, pode inserir os trechos de código exatamente como estão; caso contrário, adicione primeiro os pacotes NuGet `Aspose.Cells` e `Aspose.Slides`.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7.2).  
- Visual Studio 2022 (ou qualquer IDE de sua preferência).  
- Aspose.Cells .NET e Aspose.Slides .NET instalados via NuGet.  
- Familiaridade básica com C# e conceitos do Excel como Smart Markers e Tabelas Dinâmicas.

---

![Export workbook to PDF diagram](export-workbook-to-pdf.png "Export workbook to PDF workflow showing PDF and PPTX outputs")

## Exportar Pasta de Trabalho para PDF – Implementação Passo a Passo

A seguir está o exemplo completo, pronto para ser executado. Ele cria uma pasta de trabalho, injeta expressões Smart Marker, processa‑as, copia um intervalo de tabela dinâmica e, finalmente, salva tanto um PDF quanto um arquivo PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Por que isso funciona

1. **Processamento de Smart Marker** permite popular a pasta de trabalho a partir de qualquer fonte de dados (JSON, DataTables, etc.) sem escrever loops.  
2. **DetailSheetNewName** cria uma planilha separada para cada departamento, proporcionando uma aba limpa por departamento.  
3. **Copiando o intervalo** (`sourceRange.Copy`) duplica a tabela dinâmica *incluindo* seu cache, de modo que a planilha copiada se comporte exatamente como a original.  
4. **PresentationOptions** com `ExportCharts`, `ExportShapes` e `ExportTextBoxes` indica ao Aspose que renderize esses objetos como elementos nativos do PowerPoint, preservando a editabilidade.  
5. **PdfSaveOptions.EmbedStandardFonts** garante que o PDF tenha a mesma aparência em máquinas que não possuam as fontes originais instaladas.

O resultado são dois arquivos — `FinalReport.pdf` e `FinalPresentation.pptx` — que podem ser enviados por e‑mail, arquivados ou exibidos em qualquer visualizador sem perda de fidelidade.

## Exportar Gráficos para PowerPoint (Salvar Pasta de Trabalho como PPTX)

Se o seu relatório contém gráficos, provavelmente você desejará que eles sejam editáveis no PowerPoint. A classe `PresentationOptions` é a chave. Aqui está um trecho focado que mostra apenas a parte de exportação de gráficos:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**O que acontece nos bastidores?** Aspose converte cada gráfico do Excel em um gráfico nativo do PowerPoint, preservando séries, títulos dos eixos e formatação. Isso é muito melhor do que exportar o gráfico como uma imagem estática, pois sua audiência pode ajustar os pontos de dados posteriormente.

## Copiar Planilha de Tabela Dinâmica Sem Perder Dados

Tabelas dinâmicas costumam ser a parte mais complicada de uma exportação porque dependem de um cache oculto. O método simples `Copy` funciona porque o Aspose copia tanto o intervalo visível **quanto** o objeto de cache subjacente.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Observação:** Se você precisar da tabela dinâmica apenas em uma nova aba dentro da mesma pasta de trabalho, a abordagem anterior `sourceRange.Copy` é mais leve e evita a criação de uma nova pasta de trabalho inteira.

## Incorporar Fontes na Exportação para PDF – Por que é Importante

Ao abrir um PDF em uma máquina que não possui as fontes originais, o texto pode mudar de posição, quebras de linha podem ser alteradas ou caracteres podem desaparecer. Definir `EmbedStandardFonts = true` instrui o Aspose a incorporar as fontes mais comuns (Arial, Times New Roman, etc.) diretamente no fluxo do PDF.

Se você usar fontes personalizadas, altere para `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Aqui está um exemplo:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Agora cada destinatário vê exatamente o mesmo layout que você projetou — sem surpresas.

## Recapitulação do Exemplo Completo

Juntando tudo, o programa completo (mostrado anteriormente) realiza o seguinte:

1. **Cria** uma pasta de trabalho com marcadores Smart Marker.  
2. **Processa** os marcadores, gerando uma planilha de detalhes nomeada de acordo com o departamento.  
3. **Copia** um intervalo que contém uma tabela dinâmica para uma nova planilha, preservando sua funcionalidade.  
4. **Exporta** a pasta de trabalho para PowerPoint, mantendo gráficos, formas e caixas de texto editáveis.  
5. **Exporta** a mesma pasta de trabalho para PDF enquanto incorpora fontes padrão para renderização confiável.

Execute o programa, abra os arquivos gerados e você verá:

- **PDF**: tabelas nítidas, fontes incorporadas e o mesmo estilo visual da fonte Excel.  
- **PowerPoint**: gráficos editáveis que podem ser clicados com o botão direito → *Edit Data* no PowerPoint, e formas que permanecem totalmente manipuláveis.

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona com .NET Core?**  
Sim — Aspose.Cells e Aspose.Slides são multiplataforma. Basta direcionar .NET 6 ou superior e o mesmo código roda no Windows, Linux ou macOS.

**Q: E se eu precisar exportar apenas um subconjunto de planilhas?**  
Use `Workbook.Save` com `SaveOptions` que permitem especificar `SheetNames`. Exemplo: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Posso criptografar o PDF?**  
Com certeza. Defina `PdfSaveOptions.EncryptionDetails` com uma senha antes de chamar `Save`.

**Q: Minha tabela dinâmica usa uma fonte de dados externa — a cópia vai quebrar o vínculo?**  
A operação de cópia inclui o cache, não a conexão externa. A tabela dinâmica ainda funcionará offline, mas não será atualizada a partir da fonte original. Se precisar de atualização ao vivo, exporte os dados de origem junto com a pasta de trabalho.

## Próximos Passos & Tópicos Relacionados

- **Fontes de Dados Dinâmicas** – Aprenda a alimentar JSON ou um DataTable nos Smart Markers para relatórios em tempo real.  
- **Estilização Avançada de PDF** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}