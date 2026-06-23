---
category: general
date: 2026-05-30
description: Aprenda a adicionar cores alternadas nas linhas de planilhas C#, definir
  o fundo das células com um padrão de preenchimento sólido e personalizar o estilo
  das células da planilha sem esforço.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: pt
og_description: Cores alternadas nas linhas de planilhas C# facilitadas. Aprenda a
  definir o fundo da célula, usar um padrão de preenchimento sólido e dominar o estilo
  de célula da planilha.
og_title: Cores Alternadas nas Linhas de Planilhas C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Cores Alternadas nas Linhas de Planilhas C# – Guia Completo
url: /pt/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cores Alternadas nas Linhas de Planilhas C# – Guia Completo

Já se perguntou como deixar a exportação do Excel mais elegante usando **cores alternadas nas linhas**? Você não está sozinho — desenvolvedores perguntam constantemente como *adicionar cor de fundo* às linhas sem escrever milhares de linhas de código.  

Neste tutorial vamos percorrer uma maneira simples de **definir o fundo da célula** em cada linha, aplicar um **padrão de preenchimento sólido** e controlar o **estilo da célula da planilha** para que o resultado seja legível e visualmente atraente.

## O que Você Vai Aprender

- Recuperar dados em um `DataTable` (ou qualquer fonte tabular).  
- Construir um array de objetos `Style` que alternam entre duas cores.  
- Importar o `DataTable` para uma planilha aplicando esses estilos.  
- Verificar o resultado e ajustar as cores ou padrões se necessário.  

Nenhuma ferramenta externa além de um ambiente .NET e uma biblioteca de planilhas (usaremos **Aspose.Cells** nos exemplos) é necessária. Ao final, você terá um método reutilizável que pode ser inserido em qualquer pipeline de relatórios.

---

## Passo 1: Recuperar os Dados de Origem como um `DataTable`

Primeiro de tudo — sem dados não há o que estilizar. Abaixo está um pequeno helper que cria um `DataTable` com linhas de exemplo. Em um projeto real você substituiria isso por uma chamada ao banco de dados ou um parser de CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Por que isso importa:** Ter os dados em um `DataTable` permite que o mecanismo da planilha *importe* tudo em uma única chamada, preservando nomes de colunas e tipos de dados automaticamente.

## Passo 2: Criar Estilos de **Cores Alternadas nas Linhas**

Agora vamos gerar um array de objetos `Style` — um por linha — de modo que linhas pares recebam um tom amarelo claro enquanto linhas ímpares recebem um suave ciano. Esta é a essência da técnica de **cores alternadas nas linhas**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Por que Usar um **Padrão de Preenchimento Sólido**?

A propriedade `Pattern` indica ao motor como renderizar a cor. Um preenchimento `Solid` garante que todo o fundo da célula seja pintado, eliminando linhas de grade fracas que poderiam aparecer. Esta é a forma mais comum de **definir o fundo da célula** quando se deseja um visual limpo.

## Passo 3: Importar o `DataTable` com os Estilos Preparados

Com o array de estilos pronto, a chamada de importação torna‑se uma linha única. Aspose.Cells aplicará o estilo correspondente a cada linha automaticamente.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **O que acontece nos bastidores?**  
> A biblioteca itera sobre cada linha, copia os valores para as células e, em seguida, aplica o `Style` correspondente de `rowStyles`. Como já definimos um **padrão de preenchimento sólido**, cada célula de uma linha herda a mesma cor de fundo, proporcionando **cores alternadas nas linhas** perfeitas.

## Passo 4: Salvar a Pasta de Trabalho e Verificar o Resultado

Um rápido salvamento permite abrir o arquivo no Excel (ou em qualquer visualizador compatível) e observar o efeito.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Ao abrir o arquivo, as linhas 1, 3, 5… aparecerão em amarelo claro, enquanto as linhas 2, 4, 6… ficarão em ciano claro. Os cabeçalhos das colunas permanecem brancos, destacando os dados.

![Planilha mostrando cores alternadas nas linhas](/images/alternating-row-colors.png "Captura de tela da planilha com cores alternadas nas linhas")

*Texto alternativo da imagem:* **cores alternadas nas linhas** captura de tela de uma planilha onde o fundo de cada linha alterna entre amarelo claro e ciano claro.

## Passo 5: Personalizando Ainda Mais (Opcional)

### Alterar as Cores

Se a sua marca usa tonalidades diferentes, basta substituir `Color.LightYellow` e `Color.LightCyan` por qualquer `System.Drawing.Color` que preferir. Por exemplo:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Usar um **Tipo de Fundo** Diferente

Embora `BackgroundType.Solid` seja o mais comum, você pode experimentar `BackgroundType.Gray125`, `BackgroundType.Horizontal` ou qualquer padrão suportado pela biblioteca. Isso altera a textura visual enquanto ainda **adiciona cor de fundo**.

### Aplicar um **Estilo de Célula de Planilha** a Colunas Específicas

Às vezes você quer o efeito alternado apenas nas colunas de dados, deixando a primeira coluna (por exemplo, IDs) sem alteração. Crie um estilo separado para essa coluna e atribua‑o após a importação:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusão

Agora você tem uma solução completa e reutilizável para **cores alternadas nas linhas** em planilhas C#. Ao construir um array de objetos `Style`, **definir o fundo da célula** com um **padrão de preenchimento sólido** e importar um `DataTable` em uma única chamada, você pode gerar relatórios com aparência profissional usando pouquíssimo código.  

A partir daqui, você pode:

- **Adicionar cor de fundo** às linhas de cabeçalho para maior ênfase.  
- Combinar a técnica com formatação condicional para indicadores visuais dinâmicos.  
- Explorar outras propriedades de **estilo de célula da planilha** como fontes, bordas ou formatos numéricos.

Experimente na sua próxima rotina de exportação — seus usuários agradecerão por planilhas mais limpas e legíveis. Feliz codificação!

## O que Você Deve Aprender a Seguir?

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}