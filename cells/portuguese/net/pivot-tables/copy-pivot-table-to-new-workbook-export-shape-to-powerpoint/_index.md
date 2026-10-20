---
category: general
date: 2026-10-20
description: Copie a tabela dinâmica para uma nova pasta de trabalho usando Aspose.Cells
  e aprenda como exportar uma forma editável para o PowerPoint em um único guia.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: pt
lastmod: 2026-10-20
og_description: Copiar tabela dinâmica para uma nova pasta de trabalho usando Aspose.Cells
  e exportar uma forma editável para PowerPoint — código passo a passo que você pode
  executar hoje.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Copiar tabela dinâmica para nova pasta de trabalho, exportar forma para
  PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Copiar tabela dinâmica para nova pasta de trabalho, exportar forma para PowerPoint
url: /pt/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabela dinâmica para nova pasta de trabalho, exportar forma para PowerPoint

Se você precisar **copy pivot table to new workbook** enquanto preserva sua funcionalidade, este guia mostra exatamente como fazer isso com Aspose.Cells. Você também verá a maneira mais rápida de **export an editable shape to PowerPoint**, para que a caixa de texto permaneça editável após a conversão.

Muitos desenvolvedores assumem que copiar um intervalo que contém uma tabela dinâmica perderá a lógica da tabela dinâmica, ou que as formas se tornam imagens estáticas ao serem salvas como PPTX. Este tutorial refuta esses mitos e oferece uma solução confiável e pronta para produção.

Nas seções a seguir você irá:

* Carregar uma pasta de trabalho fonte e copiar um intervalo que inclui uma tabela dinâmica.
* Criar uma pasta de trabalho de destino que contém a mesma tabela dinâmica.
* Adicionar uma forma de caixa de texto, modificar seu texto e salvar a pasta de trabalho como uma apresentação PowerPoint onde a caixa de texto permanece editável.
* Entender por que cada chamada de API é necessária e como evitar armadilhas comuns.

**Prerequisites**

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+).
* Aspose.Cells for .NET instalado (`Install-Package Aspose.Cells`).
* Conhecimento básico de C# e Visual Studio (ou qualquer IDE de sua preferência).

---

## Copy pivot table to new workbook

Esta seção passo a passo demonstra como copiar um intervalo que contém uma tabela dinâmica e manter a definição da tabela dinâmica no novo arquivo.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` é o ponto de entrada para qualquer manipulação de Excel no Aspose.Cells. Selecionar a planilha correta garante que trabalhemos exatamente onde a tabela dinâmica está localizada.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
A tabela dinâmica vive dentro de um bloco específico de células. Ao especificar um `CellArea` que engloba totalmente a tabela dinâmica, o Aspose.Cells sabe copiar também o cache subjacente da tabela dinâmica.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
Uma pasta de trabalho nova garante que não haja intervalos nomeados conflitantes ou pivôs existentes, tornando a operação de cópia limpa.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` faz parte da **Aspose.Cells copy rows** API. Ele copia tanto os valores das células quanto o cache oculto da tabela dinâmica, de modo que a tabela dinâmica permanece funcional após a movimentação.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Abra `CopyWithPivot.xlsx` no Excel. A tabela dinâmica aparece exatamente como no arquivo fonte, e você pode atualizá‑la ou modificá‑la normalmente.

---

## Export editable shape to PowerPoint

Agora adicionaremos uma forma de caixa de texto, alteraremos seu conteúdo e salvaremos a pasta de trabalho como um arquivo PPTX. A forma permanecerá totalmente editável ao ser aberta no PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` cria uma **editable textbox in PowerPoint**‑compatible shape. As coordenadas estão em pontos; ajuste‑as para se adequar ao seu layout.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
Acessar diretamente o objeto `Shape` permite mudar propriedades como `Text`, `Font` ou `Fill`. Esta etapa demonstra como definir programaticamente o conteúdo inicial.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Abra `Presentation.pptx` no Microsoft PowerPoint. A caixa de texto aparece no primeiro slide, e você pode dar um duplo‑clique para editar o texto como qualquer forma nativa do PowerPoint.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | Uma planilha contendo a tabela dinâmica original, totalmente funcional (a atualização funciona). |
| `Presentation.pptx` | Um único slide com uma caixa de texto editável que exibe “Change me in PowerPoint”. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – Se você copiar apenas os valores das células (por exemplo, usando `CopyRows` com a flag `PasteOptions` definida para `PasteValues`), o cache da tabela dinâmica será omitido e a tabela se tornará estática. Sempre use a sobrecarga padrão de `CopyRows` como mostrado.
* **Shape positioning** – `AddTextBox` usa unidades de ponto, não índices de células do Excel. Teste as coordenadas em um arquivo de exemplo para evitar posicionamento fora do slide.
* **File format mismatch** – Salvar uma pasta de trabalho como PPTX com `SaveFormat.Pptx` converte automaticamente todas as formas suportadas. Tentar salvar como `Pdf` rasterizará a forma, tornando‑a não editável.

---

## Conclusion

Agora você sabe como **copy pivot table to new workbook** e como **export an editable shape to PowerPoint** usando Aspose.Cells para .NET. Os exemplos de código completos e executáveis cobrem todas as chamadas de API necessárias, explicam por que cada passo é importante e mostram os resultados esperados.

A seguir, você pode explorar:

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`).
* **

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}