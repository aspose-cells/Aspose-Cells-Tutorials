---
category: general
date: 2026-08-14
description: Exporte Excel para PowerPoint usando Aspose.Cells e aprenda como calcular
  fórmulas do Excel em código. Exemplo passo a passo em C# com código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: pt
lastmod: 2026-08-14
og_description: Exporte Excel para PowerPoint com Aspose.Cells e calcule fórmulas
  do Excel no código. Siga este guia completo para gerar arquivos PPTX editáveis a
  partir de pastas de trabalho.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Exportar Excel para PowerPoint com Aspose.Cells – tutorial completo em C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Exportar Excel para PowerPoint com Aspose.Cells – guia completo de programação
url: /pt/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel para PowerPoint com Aspose.Cells – guia de programação completo

Se você precisa **exportar Excel para PowerPoint** programaticamente, este guia mostra exatamente como fazer isso com Aspose.Cells para .NET. Você também aprenderá como **calcular fórmulas do Excel em código**, copiar tabelas dinâmicas sem perder definições e usar a nova função EXPAND do Office‑365 para arrays dinâmicos.

Nas seções a seguir, percorreremos um exemplo real em C#, explicaremos por que cada linha é importante e abordaremos armadilhas comuns para que você possa adaptar a solução aos seus próprios projetos.

## O que este tutorial cobre

* Carregar uma pasta de trabalho existente (`input.xlsx`)  
* Copiar um intervalo que contém uma tabela dinâmica preservando sua definição  
* Exportar a pasta de trabalho para um arquivo PowerPoint (`.pptx`) com caixas de texto e formas editáveis  
* Exportar um intervalo de células como strings usando lógica personalizada  
* Calcular fórmulas do Excel em código, incluindo a função EXPAND do Office‑365  
* Salvar a pasta de trabalho final com todas as alterações aplicadas  

**Pré‑requisitos**  
* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7.2+)  
* Aspose.Cells for .NET v25.11 ou mais recente (a opção `CopyPivotTable` foi introduzida na v25.11)  
* Conhecimento básico de C# e conceitos do Excel, como intervalos, tabelas dinâmicas e fórmulas  

> **Dica profissional:** Instale o Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) para manter seu projeto atualizado com os recursos mais recentes.

## Exportar Excel para PowerPoint com Aspose.Cells

A primeira tarefa importante é converter a pasta de trabalho em uma apresentação PowerPoint mantendo todos os elementos visuais editáveis. Isso é essencial quando você deseja gerar decks de slides a partir de relatórios financeiros ou dashboards automaticamente.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Por que isso funciona

* **`Workbook`** carrega todo o arquivo Excel na memória, proporcionando acesso total à API.  
* **`CopyRange`** com `CopyPivotTable = true` garante que a fonte de dados, o cache e o layout da tabela dinâmica sejam duplicados exatamente — algo que versões anteriores do Aspose.Cells não conseguiam fazer.  
* Adicionar uma nova planilha (`Copy`) permite manter a planilha original intacta, o que é útil para trilhas de auditoria.

## Exportar a pasta de trabalho para PowerPoint com objetos editáveis

Agora transformamos a pasta de trabalho em um arquivo PowerPoint. Ao habilitar `ExportEditableObjects`, cada gráfico, forma ou caixa de texto se torna um objeto nativo do PowerPoint que os usuários podem editar diretamente após a exportação.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Explicação

* **`WorkbookDesigner`** é um auxiliar de alto nível que prepara a pasta de trabalho para exportação, lidando com Smart Markers, intervalos nomeados e ajustes de layout.  
* Definir `ExportEditableObjects = true` indica ao Aspose.Cells que traduza os desenhos do Excel em formas do PowerPoint em vez de achatá‑los em imagens. Isso resulta em um deck de slides **totalmente editável**.

> **Caso extremo:** Se sua pasta de trabalho contém gráficos complexos criados a partir de conexões de dados externas, certifique‑se de que essas conexões estejam resolvidas antes de chamar `ExportToPptx`; caso contrário, o gráfico pode aparecer em branco.

## Exportar um intervalo como strings usando lógica personalizada

Às vezes você precisa de valores de string brutos para processamento posterior (por exemplo, alimentar um analisador CSV). A classe `ExportTableOptions` permite controlar como cada célula é convertida.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Por que você pode usar isso

* **Tipo de dado uniforme:** Exportar como strings evita erros de incompatibilidade de tipo quando o consumidor espera texto.  
* **Formatação personalizada:** Substitua `value.ToString()` por qualquer formatador customizado (por exemplo, `value.ToString("yyyy-MM-dd")` para datas).  

## Calcular fórmulas do Excel em código

Um requisito frequente é **calcular fórmulas do Excel em código** sem abrir o Excel. O Aspose.Cells fornece um motor de cálculo embutido que funciona offline e suporta as funções mais recentes do Office‑365, incluindo `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Como o motor de cálculo funciona

* A propriedade `Formula` armazena a expressão exatamente como você a digitária no Excel.  
* `CalculateFormula()` dispara uma recalculação completa da pasta de trabalho, respeitando as dependências entre as células.  
* A função `EXPAND` (disponível no Excel 365) devolve um intervalo de derramamento baseado na célula fonte (`B1`) e nas linhas (`5`) e colunas (`3`) especificadas.  

> **Dica:** Se precisar calcular apenas um subconjunto da pasta de trabalho, use `Worksheet.CalculateFormula()` para limitar o escopo e melhorar o desempenho.

## Salvar a pasta de trabalho com todas as alterações aplicadas

Por fim, grave a pasta de trabalho modificada de volta ao disco. Você pode salvar em qualquer um dos formatos suportados (`.xlsx`, `.xls`, `.csv`, etc.) alterando a extensão do arquivo.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### O que verificar

* Abra `result.xlsx` no Excel para confirmar a cópia da tabela dinâmica, o resultado da fórmula `EXPAND` e quaisquer strings exportadas customizadas.  
* Abra `output.pptx` no PowerPoint; você deverá ver um slide que espelha o layout do Excel, e todos os gráficos/caixas de texto deverão ser editáveis.

## Perguntas comuns e solução de problemas

| Pergunta | Resposta |
|----------|----------|
| **Preciso de uma licença para usar Aspose.Cells?** | Sim. Uma versão de avaliação funciona para testes, mas uma licença completa remove marcas d'água de avaliação e desbloqueia o recurso `CopyPivotTable`. |
| **E se o PPTX exportado mostrar formas em branco?** | Verifique se os objetos de desenho da pasta de trabalho não estão ocultos (`Visible = true`) e se quaisquer links de imagens externas estão incorporados antes da exportação. |
| **Posso exportar várias planilhas para slides PPTX separados?** | Use `WorkbookDesigner.ExportToPptx` em um loop, especificando um `ExportOptions` diferente para cada planilha, ou combine‑as em uma única apresentação adicionando slides manualmente via Aspose.Slides. |
| **`CalculateFormula` é thread‑safe?** | Não. Execute cálculos em um único thread ou clone a pasta de trabalho por thread para evitar condições de corrida. |

## Conclusão

Agora você tem uma **solução completa, de ponta a ponta, para exportar Excel para PowerPoint** usando Aspose.Cells, e entende como **calcular fórmulas do Excel em código** — incluindo a moderna função `EXPAND`. O tutorial abordou carregamento de pasta de trabalho, cópia de tabelas dinâmicas, exportação para PowerPoint editável, exportação customizada de strings, cálculo de fórmulas e salvamento final.

A partir daqui você pode:

* Expandir a exportação para incluir vários slides por planilha (palavra‑chave secundária: *calculate Excel formulas in code* pode ser reutilizada ao gerar dados de gráficos).  
* Integrar o Aspose.Slides para adicionar animações ou layouts de slide mestre.  
* Substituir o delegate simples `CustomExport` por formatação sensível à localidade para projetos internacionais.  

Sinta‑se à vontade para experimentar diferentes intervalos, explorar outras funções do Office‑365 (por exemplo, `FILTER`, `SORT`) e combinar este fluxo de trabalho com entrega automática de e‑mail para pipelines de relatórios totalmente autônomos.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Automatizar a Exportação de Dados do Excel Usando Aspose.Cells para .NET&#58; Um Guia Passo a Passo](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Como Exportar Gráficos do Excel para PDF Usando Aspose.Cells para .NET&#58; Um Guia Passo a Passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportar Células do Excel para Imagem Usando Aspose.Cells .NET&#58; Um Guia Passo a Passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}