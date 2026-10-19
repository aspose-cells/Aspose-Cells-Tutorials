---
category: general
date: 2026-09-15
description: Aprenda como copiar tabela dinâmica, copiar planilha com tabela dinâmica
  e salvar a pasta de trabalho como PPTX usando Aspose.Cells em C#. Guia completo
  passo a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: pt
lastmod: 2026-09-15
og_description: Como copiar tabela dinâmica, copiar planilha com tabela dinâmica e
  salvar a pasta de trabalho como PPTX usando Aspose.Cells. Siga os exemplos completos
  e executáveis em C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Como copiar tabela dinâmica e exportar planilhas – guia completo em C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como copiar tabela dinâmica preservando as planilhas
url: /pt/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabela dinâmica preservando planilhas

Se você precisa **como copiar tabela dinâmica** de uma pasta de trabalho para outra sem perder o cache subjacente da tabela dinâmica, este guia fornece uma solução pronta‑para‑usar. Você também verá como **copiar planilha com tabela dinâmica** e como **salvar pasta de trabalho como pptx** mantendo caixas de texto editáveis intactas. Todos os exemplos usam a versão mais recente do Aspose.Cells para .NET, para que você possa inserir o código em qualquer projeto C# e ver resultados imediatos.

Trabalhar programaticamente com arquivos Excel costuma envolver mover dados entre pastas de trabalho, exportar para apresentações ou inserir Smart Markers complexos. Os três trechos de código abaixo cobrem esses cenários comuns e explicam por que cada passo é importante.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior instalado  
* Aspose.Cells para .NET (versão 25.11 ou mais recente) referenciado no seu projeto  
* Uma pasta chamada `YOUR_DIRECTORY` onde os arquivos de exemplo serão lidos e gravados  

Nenhum pacote NuGet adicional é necessário.

---

## Como copiar tabela dinâmica com Aspose.Cells

Copiar um intervalo que contém uma tabela dinâmica preservando o cache da tabela dinâmica é uma necessidade frequente. Os passos a seguir demonstram a sequência exata que você precisa.

### Etapa 1 – Carregar a pasta de trabalho de origem que contém a tabela dinâmica

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Por quê*: Aspose.Cells lê a pasta de trabalho na memória, dando acesso a planilhas, células e tabelas dinâmicas.

### Etapa 2 – Criar uma pasta de trabalho de destino vazia

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Por quê*: Começar com uma pasta de trabalho em branco garante que nenhum estilo oculto ou intervalo nomeado interfira na operação de cópia.

### Etapa 3 – Copiar as linhas que incluem a tabela dinâmica

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Por quê*: `CopyRows` copia os valores brutos das células, formatos e referências ao cache da tabela dinâmica. O intervalo deve incluir toda a área da tabela dinâmica.

### Etapa 4 – Copiar as colunas que contêm a tabela dinâmica

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Por quê*: Tabelas dinâmicas abrangem linhas e colunas; copiar colunas garante que o layout completo da tabela seja mantido.

### Etapa 5 – Transferir a planilha preparada para a pasta de trabalho de destino

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Por quê*: O método `Copy` clona a planilha, incluindo o cache da tabela dinâmica, de modo que a pasta de trabalho de destino exiba uma tabela dinâmica idêntica.

### Etapa 6 – Salvar o resultado – a tabela dinâmica permanece intacta

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Por quê*: Persistir a pasta de trabalho grava todas as estruturas internas, garantindo que a tabela dinâmica possa ser atualizada posteriormente.

**Dica profissional**: Após copiar, você pode chamar `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` para atualizar os dados se a fonte tiver mudado.

---

## Copiar planilha com tabela dinâmica – uma alternativa concisa

Se você simplesmente precisa duplicar uma planilha inteira que já contém uma tabela dinâmica, pode pular as etapas de cópia de linhas/colunas e usar diretamente o método `Copy` ao nível da planilha.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Esta abordagem é útil quando a planilha não contém dados extras fora da área da tabela dinâmica. A operação **copiar planilha com tabela dinâmica** preserva automaticamente toda a formatação, intervalos nomeados e caches de tabelas dinâmicas.

---

## Salvar pasta de trabalho como PPTX com caixas de texto editáveis

Exportar uma planilha Excel que contém uma caixa de texto editável para PowerPoint pode ser necessário para dashboards de relatórios. O código abaixo mostra **salvar pasta de trabalho como pptx** mantendo a caixa de texto editável.

### Etapa 1 – Carregar a pasta de trabalho que inclui a caixa de texto

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Etapa 2 – Configurar as opções de salvamento PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Por quê*: Definir `ExportEditableTextBox` indica ao Aspose.Cells que ele deve traduzir a caixa de texto do Excel em uma forma do PowerPoint que permanece editável após a exportação.

### Etapa 3 – Salvar a pasta de trabalho como PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Resultado esperado**: Abra `Result.pptx` no PowerPoint, selecione a caixa de texto e edite seu conteúdo como qualquer forma nativa.

**Pergunta comum**: *E se eu precisar manter a caixa de texto bloqueada?*  
Defina `pptxOptions.ExportEditableTextBox = false`; a forma será convertida em uma imagem estática.

---

## Exportar um Smart Marker que contém um array JSON como valor de célula única

Smart Markers permitem popular modelos Excel com estruturas de dados complexas. A seguir, um exemplo completo que demonstra **como copiar tabela dinâmica**‑style ao inserir um array JSON em uma única célula.

### Etapa 1 – Preparar o SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Etapa 2 – Inserir um Smart Marker na célula A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Etapa 3 – Definir a fonte de dados com um array no estilo JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Etapa 4 – Processar a pasta de trabalho

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Etapa 5 – Salvar a pasta de trabalho resultante

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Verificação do resultado**: Abra `JsonSingleCell.xlsx` e confirme que a célula A1 exibe `A,B,C`. Isso demonstra como tratar uma coleção como valor de célula única, padrão frequentemente necessário ao exportar dados para sistemas downstream.

---

## Exemplo completo em funcionamento

Abaixo está um único programa que combina os três cenários. Você pode copiar o código para um aplicativo console, ajustar os caminhos dos arquivos e executá‑lo para ver as três saídas.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Ao executar este programa são gerados:

* `CopyWithPivot.xlsx` – uma cópia perfeita da tabela dinâmica original.  
* `Result.pptx` – um slide PowerPoint com uma caixa de texto editável.  
* `JsonSingleCell.xlsx` – uma planilha onde o array JSON aparece em uma única célula.

---

## Conclusão

Agora você sabe **como copiar tabela dinâmica** com segurança, como **copiar planilha com tabela dinâmica** em uma única chamada e como **salvar pasta de trabalho como pptx** preservando caixas de texto editáveis. Esses padrões cobrem os fluxos de trabalho mais comuns de Excel‑para‑PowerPoint e Excel‑para‑JSON que você encontrará em projetos de automação corporativa.

Em seguida, considere explorar:

* Atualizar programaticamente tabelas dinâmicas copiadas (`PivotTable.Refresh()`)  
* Exportar para outros formatos como PDF ou HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Usar opções avançadas de Smart Marker como funções personalizadas ou formatação condicional  

Sinta‑se à vontade para experimentar diferentes intervalos, múltiplas planilhas ou estruturas JSON maiores. A API Aspose.Cells oferece controle granular, permitindo adaptar esses exemplos a qualquer cenário real. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}