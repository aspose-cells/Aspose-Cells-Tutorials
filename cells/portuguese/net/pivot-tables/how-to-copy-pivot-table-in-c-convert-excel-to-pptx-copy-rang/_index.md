---
category: general
date: 2026-01-14
description: Como copiar tabela dinâmica usando Aspose.Cells e também aprender a converter
  Excel para PPTX, copiar intervalo para outra pasta de trabalho e tornar a caixa
  de texto editável em PPTX em um único tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: pt
og_description: Como copiar tabela dinâmica e, em seguida, converter Excel para PPTX,
  copiar intervalo para outra pasta de trabalho e tornar a caixa de texto editável
  no PPTX — tudo com Aspose.Cells.
og_title: Como Copiar Tabela Dinâmica em C# – Guia Completo de Excel para PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Como copiar tabela dinâmica em C# – Converter Excel para PPTX, copiar intervalo
  e tornar caixa de texto editável
url: /pt/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Copiar Tabela Dinâmica em C# – Guia Completo de Excel para PPTX

Como copiar uma tabela dinâmica de uma pasta de trabalho para outra é uma pergunta frequente quando você está automatizando relatórios baseados em Excel. Neste tutorial vamos percorrer três cenários reais usando **Aspose.Cells for .NET**: copiar um intervalo de tabela dinâmica, exportar uma planilha para um arquivo PPTX com uma caixa de texto editável e preencher uma única célula com um array JSON via Smart Markers.  

Você também verá como **converter Excel para PPTX**, **copiar intervalo para outra pasta de trabalho** e **tornar a caixa de texto editável no PPTX** sem quebrar a formatação. Ao final, você terá uma base de código pronta‑para‑executar que pode ser inserida em qualquer projeto .NET.

> **Dica profissional:** Todos os exemplos têm como alvo o Aspose.Cells 23.12, mas os mesmos conceitos se aplicam a versões anteriores com pequenas alterações na API.

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## O Que Você Precisa

- Visual Studio 2022 (ou qualquer IDE C#)
- Runtime .NET 6.0 ou superior
- Pacote NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Dois arquivos Excel de exemplo (`source.xlsx`, `chartWithTextbox.xlsx`) colocados em uma pasta que você controla (substitua `YOUR_DIRECTORY` pelo caminho real).

Nenhuma biblioteca adicional é necessária; o mesmo assembly `Aspose.Cells` lida com Excel, PPTX e Smart Markers.

---

## Como Copiar Tabela Dinâmica e Preservar Seus Dados

Quando você copia um intervalo que contém uma tabela dinâmica, o comportamento padrão é colar apenas os **valores**. Para manter a definição da tabela dinâmica intacta, você deve habilitar a flag `CopyPivotTable`.

### Passo a Passo

1. **Carregue a pasta de trabalho de origem** que contém a tabela dinâmica.  
2. **Crie uma pasta de trabalho de destino vazia** – ela receberá o intervalo copiado.  
3. **Use `CopyRange` com `CopyPivotTable = true`** para que a definição da tabela dinâmica viaje junto com os dados.  
4. **Salve o arquivo de destino** onde precisar.

#### Exemplo de Código Completo

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Por que isso funciona:**  
`CopyOptions.CopyPivotTable` indica ao Aspose.Cells que clone o objeto subjacente `PivotTable` em vez de apenas seus valores renderizados. A pasta de trabalho de destino agora contém uma tabela dinâmica totalmente funcional que você pode atualizar ou modificar programaticamente.

**Caso especial:** Se a pasta de trabalho de origem usa fontes de dados externas, pode ser necessário incorporar os dados ou ajustar as strings de conexão após a cópia; caso contrário, a tabela dinâmica exibirá “#REF!”.

---

## Converter Excel para PPTX e Tornar a Caixa de Texto Editável

Exportar uma planilha para PowerPoint é útil para criar apresentações diretamente a partir dos dados. Por padrão, a caixa de texto exportada torna‑se uma forma estática, mas definir `IsTextBoxEditable` inverte esse comportamento.

### Passo a Passo

1. **Abra a pasta de trabalho** que contém o gráfico e a caixa de texto que você deseja exportar.  
2. **Configure `ImageOrPrintOptions`** com `SaveFormat = SaveFormat.Pptx`.  
3. **Defina uma área de impressão** que inclua a caixa de texto.  
4. **Habilite `IsTextBoxEditable`** para que o texto possa ser editado após a abertura do PPTX.  
5. **Salve o arquivo PPTX**.

#### Exemplo de Código Completo

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Resultado:** Abra `result.pptx` no PowerPoint – a caixa de texto que você inseriu no Excel agora será uma caixa de texto regular que pode ser editada. Não há necessidade de recriá‑la manualmente.

**Erro comum:** Se a planilha contém células mescladas que intersectam a área de impressão, o slide resultante pode ficar deslocado. Ajuste a área de impressão ou desfaça a mesclagem antes da exportação.

---

## Copiar Intervalo para Outra Pasta de Trabalho com Smart Markers (JSON → Célula Única)

Às vezes você precisa inserir um array JSON em uma única célula Excel, por exemplo ao enviar dados para sistemas downstream que esperam uma string JSON. Os Smart Markers do Aspose.Cells podem serializar um array como uma única célula quando você define `ArrayAsSingle = true`.

### Passo a Passo

1. **Carregue uma pasta de trabalho modelo** que contém um placeholder Smart Marker (ex.: `&=Items.Name`).  
2. **Prepare o objeto de dados** – um tipo anônimo com um array `Items`.  
3. **Crie um `SmartMarkerProcessor`** e aplique os dados com `ArrayAsSingle`.  
4. **Salve a pasta de trabalho preenchida**.

#### Exemplo de Código Completo

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Explicação:**  
Quando `ArrayAsSingle` é true, o Aspose.Cells concatena cada elemento de `Items.Name` em uma string no estilo JSON (`["A","B"]`) e a grava na célula que continha o smart marker. Isso evita a criação de linhas separadas para cada elemento do array.

**Quando usar:** Ideal para exportar tabelas de configuração, payloads de API ou qualquer cenário em que o consumidor espera uma string JSON compacta em vez de um layout tabular.

---

## Dicas Adicionais & Tratamento de Casos de Borda

| Cenário | O Que Observar | Correção Sugerida |
|----------|-------------------|---------------|
| **Tabelas Dinâmicas Grandes** | Picos de uso de memória ao copiar caches de pivô enormes. | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` antes de carregar. |
| **Exportação para PPTX com Imagens** | Imagens podem ser rasterizadas com DPI baixo. | Defina `pptxOptions.ImageResolution = 300` para slides mais nítidos. |
| **Formatação JSON em Smart Marker** | Caracteres especiais (`"` , `\`) quebram o JSON. | Escape-os manualmente ou use `JsonSerializer` para pré‑serializar antes de alimentar os Smart Markers. |
| **Copiar Intervalo entre Versões Diferentes do Excel** | Arquivos `.xls` antigos podem perder formatação. | Salve o destino como `.xlsx` para preservar recursos modernos. |

---

## Recapitulando – Como Copiar Tabela Dinâmica e Muito Mais

Começamos respondendo **como copiar tabela dinâmica** preservando sua funcionalidade, depois mostramos como **converter Excel para PPTX**, **tornar a caixa de texto editável no PPTX**, e finalmente como **copiar intervalo para outra pasta de trabalho** usando Smart Markers para inserir um array JSON em uma única célula.  

Os três trechos de código são autônomos; você pode colá‑los em um novo aplicativo console, ajustar os caminhos dos arquivos e executá‑los hoje.

---

## O Que Vem a Seguir?

- **Explore outros formatos de exportação** – o Aspose.Cells também suporta PDF, XPS e HTML.  
- **Atualize tabelas dinâmicas programaticamente** usando `PivotTable.RefreshData()` após a cópia.  
- **Combine Smart Markers com gráficos** para gerar dashboards dinâmicos que se atualizam automaticamente.  

Se você tem interesse em **salvar a pasta de trabalho como PPTX** com layouts de slide personalizados, confira a documentação do Aspose.Cells sobre `SlideOptions`.  

Sinta‑se à vontade para experimentar — troque a área de impressão, teste diferentes `CopyOptions` ou alimente um payload JSON mais complexo. A API é flexível o suficiente para a maioria dos pipelines de relatório.

---

### Perguntas Frequentes

**P: O `CopyPivotTable` também copia slicers?**  
R: Não diretamente. Slicers são objetos separados; após a cópia você precisará recriá‑los ou copiá‑los via a coleção `Worksheet.Shapes`.

**P: Posso exportar várias planilhas em um único deck PPTX?**  
R: Sim. Percorra cada planilha, chame `Save` com o mesmo `ImageOrPrintOptions` e defina `pptxOptions.StartSlideNumber` para continuar a numeração.

**P: E se meu array JSON contiver objetos aninhados?**  
R: Defina `ArrayAsSingle = false` e use um template customizado que itere sobre os objetos internos.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}