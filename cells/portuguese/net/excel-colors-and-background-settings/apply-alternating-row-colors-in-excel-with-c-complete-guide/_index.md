---
category: general
date: 2026-07-03
description: Aplique cores alternadas nas linhas ao importar a datatable para o Excel
  usando C#. Aprenda como exportar uma datatable C# para o Excel, salvar a tabela
  estilizada no Excel e manter a formatação da pasta de trabalho.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: pt
og_description: Aplique cores alternadas nas linhas no Excel usando C#. Este tutorial
  mostra como importar uma DataTable para o Excel, exportar uma DataTable C# para
  o Excel e salvar a pasta de trabalho com formatação.
og_title: Aplicar cores alternadas nas linhas do Excel com C# – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Aplicar cores alternadas nas linhas do Excel com C# – Guia completo
url: /pt/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar cores de linhas alternadas no Excel com C# – Guia Completo

Já precisou **aplicar cores de linhas alternadas** ao exportar um `DataTable` C# para o Excel? Você não está sozinho—desenvolvedores perguntam constantemente como deixar essas planilhas com aparência profissional sem ter que mexer manualmente no Excel depois. A boa notícia? Você pode fazer isso programaticamente em apenas algumas linhas de código.

Neste tutorial vamos percorrer **import datatable to excel**, mostrar como **export c# datatable to excel** com uma tabela estilizada e, finalmente, **save styled table excel** preservando a formatação. Ao final, você será capaz de **save workbook with formatting** que parece pronto para uma reunião com o cliente.

## Pré‑requisitos

- .NET 6.0 ou superior (o exemplo usa .NET 6, mas qualquer versão recente funciona)
- Aspose.Cells para .NET (versão de avaliação ou licenciada) – esta biblioteca facilita a estilização
- Uma fonte `DataTable` (pode ser de um banco de dados, CSV ou coleção em memória)

> **Dica de especialista:** Se ainda não tem o Aspose.Cells, você pode obtê‑lo pelo NuGet com `dotnet add package Aspose.Cells`.

## Etapa 1: Configurar o Projeto e Carregar seus Dados

Primeiro, crie um aplicativo console (ou qualquer projeto C#) e adicione as declarações `using` necessárias. Em seguida, carregue os dados em um `DataTable`. Para fins de ilustração, vamos gerar uma tabela simples na hora.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Por que isso importa:** Ter um `DataTable` pronto significa que você pode **import datatable to excel** em uma única chamada, eliminando a necessidade de inserção manual célula por célula.

## Etapa 2: Criar uma Pasta de Trabalho e Definir os Estilos de Linhas Alternadas

Agora vamos instanciar um novo `Workbook`. O truque para **apply alternating row colors** está em `ImportTableOptions.StyleArray`. Usaremos os dois primeiros estilos embutidos (geralmente branco e cinza claro), mas você pode personalizá‑los depois.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explicação:** `ImportTableOptions` indica ao Aspose.Cells como tratar cada linha durante a importação. Ao fornecer um `StyleArray` com duas entradas, a biblioteca pinta automaticamente cada linha ímpar com o primeiro estilo e cada linha par com o segundo—exatamente o que você precisa para **apply alternating row colors**.

## Etapa 3: Inserir o DataTable na Planilha (Incluindo Cabeçalhos)

Com a pasta de trabalho e os estilos prontos, agora **import datatable to excel**. O método `ImportDataTable` faz o trabalho pesado: grava os cabeçalhos das colunas, respeita o array de estilos e posiciona os dados a partir da célula A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Por que incluímos `true` como segundo argumento:** Ele indica ao método que escreva os nomes das colunas na primeira linha, o que é essencial para um relatório com aparência profissional.

## Etapa 4: Ajustar a Tabela (Opcional, mas Útil)

Se quiser que a tabela ajuste automaticamente as colunas ou adicione uma linha de filtro, algumas linhas extras deixam tudo mais elegante.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Esses ajustes não afetam as cores alternadas, mas melhoram a experiência geral do usuário no arquivo **save styled table excel**.

## Etapa 5: Salvar a Pasta de Trabalho Mantendo Toda a Formatação

Por fim, gravamos o arquivo no disco. O método `Save` preserva cada estilo definido, garantindo que as linhas alternadas permaneçam intactas.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Ao abrir `StyledEmployees.xlsx`, você verá uma tabela limpa onde as linhas alternam entre branco e cinza claro—exatamente o recurso visual que muitos usuários dependem para melhorar a legibilidade.

### Saída Esperada

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Linha 1, 3 … → fundo branco  
- Linha 2, 4 … → fundo cinza‑claro  

Esse é todo o processo de **save workbook with formatting**.

## Perguntas Frequentes & Casos de Borda

### E se meu DataTable tiver milhares de linhas?

O método `ImportDataTable` transmite os dados de forma eficiente, mas você pode encontrar limites de memória em tabelas muito grandes. Nesses casos, considere dividir a exportação em várias planilhas ou usar a sobrecarga de `ImportDataTable` que permite especificar a linha e coluna de início.

### Posso usar cores personalizadas em vez das padrão?

Com certeza. Basta substituir as atribuições de `ForegroundColor` em `styleWhite` e `styleGray` por qualquer `System.Drawing.Color` que preferir—pense em azuis pastel ou cores da identidade visual da empresa.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Como garantir que o estilo alternado continue funcionando quando o usuário adicionar linhas depois?

Se os usuários editarem o arquivo manualmente, o array de estilos original não será estendido automaticamente. Uma solução rápida é converter o intervalo em uma Tabela do Excel (`ListObject`) após a importação; o Excel então repete o padrão para novas linhas.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Agora qualquer nova linha herda as cores alternadas.

## Exemplo Completo (Todas as Etapas em Um Só Lugar)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Execute o programa, abra o arquivo gerado e você verá imediatamente as cores alternadas aplicadas—sem necessidade de formatação manual.

## Conclusão

Acabamos de demonstrar como **apply alternating row colors** ao **import datatable to excel** usando C#. O processo cobre tudo que você precisa para **export c# datatable to excel**, **save styled table excel** e **save workbook with formatting** com aparência profissional desde o início.

Próximos passos? Experimente trocar os dois estilos por um tema personalizado, ou transforme o intervalo em uma Tabela do Excel para que os usuários possam ordenar e filtrar mantendo o padrão de cores. Você também pode explorar formatação condicional via `ConditionalFormattingCollection` para sinais visuais ainda mais dinâmicos.

Tem uma variação?

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Importar DataTable para Excel Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Aplicar Cores e Fundos no Excel usando Aspose.Cells para .NET](/cells/english/net/formatting/colors-and-background/)
- [Automatizar Cores de Tema do Excel Usando Aspose.Cells .NET para Formatação Eficiente](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}