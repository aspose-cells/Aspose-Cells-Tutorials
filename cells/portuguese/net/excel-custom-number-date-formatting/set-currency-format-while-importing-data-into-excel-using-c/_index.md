---
category: general
date: 2026-11-19
description: Defina o formato de moeda no Excel com C# – aprenda como definir o formato
  numérico e o estilo das colunas do Excel durante a importação de uma planilha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: pt
lastmod: 2026-11-19
og_description: Defina o formato de moeda no Excel com C# e descubra como definir
  o formato numérico, atribuir o formato de número e estilizar colunas do Excel durante
  a importação de uma planilha.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Defina o formato de moeda no Excel com C# – guia completo passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Definir formato de moeda ao importar dados para o Excel usando C#
url: /pt/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir formato de moeda ao importar dados para o Excel usando C#

Se você precisar **definir o formato de moeda** em uma planilha do Excel, este guia mostra como **definir o formato numérico** e estilizar as colunas ao realizar uma **importação de planilha do Excel**. Você verá um exemplo completo e executável que atribui o formato numérico correto a cada coluna de um `DataTable` e importa os dados com o estilo desejado.

Trabalhar com Excel a partir do C# costuma exigir mais do que apenas despejar valores brutos — você também deve controlar como os números são exibidos. Seja gerando faturas, relatórios financeiros ou painéis, formatar corretamente moedas, porcentagens ou datas torna a saída imediatamente legível.

## Pré-requisitos

* .NET 6.0 (ou superior) instalado.
* Uma referência ao **Aspose.Cells for .NET** (ou qualquer biblioteca que exponha uma classe `Style` com a propriedade `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Familiaridade básica com `DataTable` e coleções C#.
* Uma IDE como Visual Studio 2022 ou VS Code.

## Etapa 1: Recuperar os dados a serem escritos na planilha

Primeiro obtenha um `DataTable` que contenha os dados brutos que você deseja exportar. Em projetos reais isso pode vir de uma consulta ao banco de dados, de uma chamada de API ou de um analisador CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Por que isso importa:** Importar um `DataTable` totalmente preenchido permite manter a lógica de recuperação de dados separada da lógica de geração do Excel, o que melhora a testabilidade e a manutenção.

## Etapa 2: Criar um array de estilos – uma entrada por coluna no DataTable

O Aspose.Cells espera um `Style[]` cujo comprimento corresponda ao número de colunas que você planeja importar. Cada elemento pode conter um formato numérico específico.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Dica profissional:** Mesmo que você precise de formatação apenas para um subconjunto de colunas, ainda assim deve criar uma instância `Style` para cada coluna; caso contrário, você receberá uma `NullReferenceException` durante a importação.

## Etapa 3: Atribuir formato numérico às colunas desejadas

Os números de estilo embutidos diferem entre bibliotecas. No Aspose.Cells:

* `0` → General (inteiro)  
* `2` → Currency (ex.: `$#,##0.00`)  
* `3` → Date, etc.

Aqui nós **atribuímos o formato numérico** a duas colunas: a primeira coluna (Id) permanece como inteiro, enquanto a segunda coluna (Amount) recebe um formato de moeda.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Como definir o formato numérico:** Usar a propriedade `Number` é a maneira mais rápida de escolher um formato embutido. Para moedas específicas de localidade, considere usar uma string de formato personalizada que inclua o símbolo de moeda apropriado.

## Etapa 4: Importar o DataTable para a planilha, aplicando os estilos de coluna

Agora que o array de estilos está pronto, importe os dados. O método `ImportDataTable` respeita os estilos que você passou.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Resultado esperado

Ao abrir **FinancialReport.xlsx**, você verá:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Suprimentos de escritório |
| 2  | $98,765.43 | Honorários de consultoria |
| 3  | $0.99      | Diversos    |

*A coluna **Amount** é exibida usando o formato de moeda que você definiu, enquanto **Id** permanece um inteiro.*

## Como definir formato numérico para cenários adicionais

### Atribuir formato numérico a colunas de data

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Usar formatos numéricos personalizados para porcentagens

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Estilização além de formatos numéricos

Você também pode definir fonte, cor de fundo ou alinhamento no mesmo objeto `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Por que isso funciona:** O objeto `Style` agrega todas as propriedades visuais de uma célula. Quando você passa o array para `ImportDataTable`, cada célula herda o estilo definido automaticamente.

## Armadilhas comuns e como evitá‑las

| Armadilha | Sintoma | Correção |
|-----------|---------|----------|
| Esquecer de instanciar cada `Style` | `NullReferenceException` on import | Percorra o array e chame `CreateStyle()` antes de definir as propriedades. |
| Usar o índice numérico embutido errado | Wrong format (e.g., dates appear as integers) | Consulte a documentação da biblioteca para os constantes `Number` corretos. |
| Não salvar a pasta de trabalho | No output file or empty file | Chame `workbook.Save(...)` após a conclusão da importação. |
| Incompatibilidade de localidade para o símbolo da moeda | `$` appears even in non‑US locales | Use uma string de formato personalizada com o símbolo apropriado (e.g., `"€#,##0.00"`). |

## Exemplo completo e executável



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar arquivo Excel c# – estilizar células e definir formato de moeda](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Como formatar colunas do Excel em C# – Guia completo](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Criar Workbook Excel C# – Aplicar formato de moeda e importar DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}