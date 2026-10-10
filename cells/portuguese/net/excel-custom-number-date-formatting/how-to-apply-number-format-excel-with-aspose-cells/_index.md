---
category: general
date: 2026-10-10
description: Aplique rapidamente o formato numérico no Excel importando uma DataTable,
  definindo formatos de data e moeda e preservando a linha de cabeçalho em uma única
  etapa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: pt
lastmod: 2026-10-10
og_description: aplique formatação numérica no Excel em C# usando Aspose.Cells. Aprenda
  a definir o formato de data no Excel, o formato de moeda no Excel e a preservar
  a linha de cabeçalho no Excel ao importar um DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Aplicar formatação numérica do Excel em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Como aplicar formatação de número no Excel com Aspose.Cells
url: /pt/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como aplicar formatação numérica no Excel com Aspose.Cells

Se você precisa **aplicar formatação numérica no Excel** ao carregar dados de um `DataTable`, este guia mostra exatamente como fazer. Você também aprenderá a **definir formatação de data no Excel**, **definir formatação de moeda no Excel** e **preservar a linha de cabeçalho no Excel** durante a importação, para que a planilha resultante pareça profissional sem processamento adicional.

Cobriremos tudo, desde a instalação da biblioteca até a escrita de um trecho completo e executável. Ao final, você será capaz de importar qualquer `DataTable` para uma pasta de trabalho Excel, formatar automaticamente colunas numéricas e manter a linha de cabeçalho intacta — tudo em apenas algumas linhas de C#.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.6+)
* Visual Studio 2022 (ou qualquer IDE C# de sua preferência)
* **Aspose.Cells for .NET** – instale via NuGet:

```bash
dotnet add package Aspose.Cells
```

* Uma fonte `DataTable` – o exemplo usa um método auxiliar `GetTable()` que retorna dados de exemplo.

> **Dica profissional:** Aspose.Cells é uma biblioteca comercial, mas oferece um modo de avaliação gratuito que desativa a marca d'água por até 30 dias.

## Etapa 1: Criar uma pasta de trabalho e acessar a primeira planilha

O objeto workbook é o ponto de entrada para todas as operações do Excel. Criar uma nova pasta de trabalho fornece uma planilha padrão no índice 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Por que esta etapa?*  
`Workbook` gerencia o formato de arquivo, o motor de cálculo e o repositório de estilos. Acessar `Worksheet` cedo nos permite passar a planilha de destino para o método de importação posteriormente.

## Etapa 2: Recuperar os dados de origem como um DataTable

Em projetos reais, os dados geralmente vêm de uma consulta ao banco de dados, de um analisador CSV ou de uma resposta de API. Para ilustração, geramos um `DataTable` simples com três colunas: **Product**, **Price** e **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Por que esta etapa?*  
Um `DataTable` fornece uma representação tabular em memória que o Aspose.Cells pode importar diretamente, preservando a ordem das colunas e os tipos de dados.

## Etapa 3: Preparar um array `Style` – um estilo por coluna

Aspose.Cells permite aplicar um estilo distinto a cada coluna durante a importação passando um array de objetos `Style`. O comprimento do array deve corresponder ao número de colunas na tabela de origem.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Por que esta etapa?*  
Se você pular a criação explícita (`CreateStyle()`), a tentativa de definir `Number` lançará uma `NullReferenceException`. Inicializar cada `Style` garante que as atribuições posteriores sejam bem‑sucedidas.

## Etapa 4: Atribuir formatos numéricos – moeda e data

O Excel identifica formatos numéricos internos por ID.

* **14** – Moeda (ex., `$1,234.00`)  
* **22** – Data curta (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Observação:** Se precisar de um formato personalizado (ex., `"¥#,##0.00"`), use `Style.Custom = "¥#,##0.00"` em vez de um ID interno.

*Por que esta etapa?*  
Aplicar o **formato numérico** correto no momento da importação elimina a necessidade de uma segunda passagem que percorra as células para alterar a formatação. Também garante que o **format excel cells date** e **set currency format excel** sejam consistentes em todas as linhas.

## Etapa 5: Importar o DataTable preservando a linha de cabeçalho

O método `ImportDataTable` pode copiar os dados, manter a primeira linha como cabeçalho e aplicar os estilos de coluna que preparamos.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Saída esperada** – Abra `FormattedReport.xlsx` e você verá:

| Produto | Preço (moeda) | Data de Lançamento (data) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

A linha de cabeçalho permanece intacta, a coluna **Price** exibe o símbolo da moeda e a coluna **ReleaseDate** mostra um formato de data curta — tudo sem nenhum código de estilo adicional.

### Lidando com casos de borda comuns

| Situação                               | Solução |
|----------------------------------------|----------|
| **Mais colunas do que estilos**           | Garanta que `columnStyles.Length` seja igual a `sourceTable.Columns.Count`. Entradas ausentes usarão o estilo padrão da pasta de trabalho. |
| **Valores nulos em colunas numéricas**     | O Excel trata `null` como uma célula vazia; o formato numérico ainda se aplica quando um valor for inserido posteriormente. |
| **Moeda personalizada específica de local**    | Use `columnStyles[i].Custom = "\"€\"#,##0.00"` e defina `columnStyles[i].Number = -1` para desativar o ID interno. |
| **Tabelas grandes ( > 100 000 linhas )**    | Considere usar a sobrecarga `ImportDataTable` com `ImportTableOptions` para transmitir dados e reduzir a pressão de memória. |
| **Aplicar o mesmo estilo a várias colunas** | Reutilize a mesma instância `Style` no array (ex., `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bônus: Usando uma string de formato personalizada

Se os IDs internos não atenderem às suas necessidades, você pode definir um formato numérico personalizado:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Essa abordagem lhe dá controle total sobre **format excel cells date** e **set currency format excel** além dos IDs predefinidos.

## Conclusão

Agora você sabe como **aplicar formatação numérica no Excel** de forma eficiente ao importar um `DataTable` com Aspose.Cells. Ao criar um array `Style` por coluna, atribuir IDs numéricos internos ou personalizados e usar a sobrecarga `ImportDataTable` que **preserve header row excel**, você pode gerar planilhas prontas para publicação em uma única operação.

### O que vem a seguir?

* Explore **set date format excel** com padrões personalizados como `"dddd, mmmm dd, yyyy"`.
* Combine esta técnica com **conditional formatting** para destacar valores fora do intervalo.
* Use **format excel cells date** em tabelas dinâmicas ou gráficos para relatórios dinâmicos.

Sinta-se à vontade para experimentar diferentes IDs numéricos ou strings personalizadas para corresponder ao guia de estilo da sua organização. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [aplicar formatação numérica no Excel – Guia passo a passo para formatar colunas](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Criar Pasta de Trabalho Excel C# – Aplicar Formatação de Moeda e Importar DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Definir formatação de data no Excel com C# – Guia completo de formatação de importação](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}