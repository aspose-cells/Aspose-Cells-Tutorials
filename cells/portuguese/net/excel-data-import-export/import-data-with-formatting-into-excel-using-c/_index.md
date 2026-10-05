---
category: general
date: 2026-03-01
description: Importe dados com formatação para o Excel usando C#. Aprenda como importar
  DataTable para o Excel e adicionar cor de fundo às células em apenas alguns passos.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: pt
og_description: Importar dados com formatação para o Excel usando C#. Guia passo a
  passo que mostra como importar uma DataTable e adicionar cor de fundo às células.
og_title: Importar Dados com Formatação para o Excel – Guia C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importar Dados com Formatação para o Excel usando C#
url: /pt/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar Dados com Formatação para o Excel usando C#

Já precisou **importar dados com formatação** para uma pasta de trabalho do Excel, mas continuou recebendo uma planilha simples e sem graça? Você não está sozinho. A maioria dos desenvolvedores esbarra nessa situação quando descobrem que a importação padrão remove todas as cores e estilos que eles configuraram cuidadosamente nos dados de origem.

Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar que **importa um DataTable para o Excel** e **adiciona cor de fundo às células do Excel** ao mesmo tempo. Nenhum pós‑processamento extra necessário—sua planilha ficará exatamente como você deseja logo de cara.

## O que você aprenderá

- Como recuperar dados em um `DataTable`.
- Como definir um array de objetos `Style` que carregam cores de fundo.
- Como chamar `ImportDataTable` com esses estilos para que a importação preserve a formatação.
- Um exemplo completo, executável, que você pode inserir em um aplicativo console e ver o resultado instantaneamente.
- Dicas, armadilhas e variações para projetos do mundo real.

### Pré-requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+).
- A biblioteca **GemBox.Spreadsheet** (a versão gratuita é suficiente para a demonstração).
- Familiaridade básica com C# e conceitos de Excel.

Se você está se perguntando *por que GemBox?* porque ele oferece um método de linha única `ImportDataTable` que aceita arrays de estilos—exatamente o que precisamos para **importar dados com formatação** sem escrever um loop.

---

## Etapa 1: Configurar o Projeto e Adicionar GemBox.Spreadsheet

Para começar, crie um novo aplicativo console:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Dica de especialista:** A versão gratuita limita as planilhas a 150 k células, o que é mais que suficiente para demonstrações. Se você atingir o limite, faça upgrade ou troque para EPPlus, mas a API será um pouco diferente.

## Etapa 2: Recuperar os Dados de Origem como um `DataTable`

A primeira coisa que precisamos é um `DataTable` que imite os dados que você normalmente puxaria de um banco de dados. Aqui está um pequeno helper que cria um em memória:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Por que isso importa:** Ao separar a recuperação de dados em seu próprio método, você pode trocar a origem—SQL, CSV, serviço web—sem tocar na lógica de importação. Isso mantém o código limpo e torna o tutorial **como importar datatable para excel** reutilizável.

## Etapa 3: Definir os Estilos que Você Deseja Aplicar

Agora vem a parte divertida: vamos criar um array de objetos `Style`, cada um com um `ForegroundColor` distinto. O GemBox permite definir `BackgroundPatternColor` (preenchimento da célula) e `ForegroundColor` (cor do texto). Para esta demonstração, vamos colorir as duas primeiras colunas de forma diferente.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explicação:**  
- Objetos `Style` são contêineres leves; você não precisa criar um novo para cada célula.  
- Ao alinhar a ordem do array com a ordem das colunas, o GemBox aplica automaticamente o estilo correspondente durante a importação.  
- Essa é a chave para **importar dados com formatação**—a formatação viaja junto com os dados, não depois.

## Etapa 4: Importar o `DataTable` para a Worksheet com Estilos

Com os dados e estilos prontos, podemos agora criar uma workbook, escolher a primeira worksheet e chamar `ImportDataTable`. A assinatura do método é assim:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Veja como usamos:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**O que está acontecendo nos bastidores?**  
- `true` indica ao GemBox que escreva os nomes das colunas na primeira linha.  
- `0, 0` posiciona a importação na célula A1.  
- `importStyles` vincula cada coluna às cores que definimos anteriormente.  

Ao abrir *Report.xlsx*, você verá a coluna **ID** sombreada em azul claro, a coluna **Name** sombreada em verde claro e a coluna **Score** sem alterações. Isso é **importar dados com formatação** em uma única chamada.

## Etapa 5: Verificar o Resultado (Saída Esperada)

Abra o `Report.xlsx` gerado. Você deverá ver algo como isto:

| ID (azul claro) | Nome (verde claro) | Pontuação |
|-----------------|--------------------|-----------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- A coluna **ID** tem fundo azul‑claro.  
- A coluna **Nome** tem fundo verde‑claro.  
- A coluna **Pontuação** permanece com o fundo branco padrão.

![Planilha Excel mostrando importação de dados com formatação – coluna ID azul claro, coluna Nome verde claro](excel-screenshot.png "exemplo de importação de dados com formatação")

*O texto alternativo da imagem inclui a palavra‑chave principal para SEO.*

---

## Perguntas Frequentes e Casos Limítrofes

### Posso aplicar mais do que apenas cores de fundo?

Com certeza. `Style` permite definir fontes, bordas, formatos numéricos e até formatação condicional. Por exemplo, para deixar pontuações acima de 90 em negrito e vermelho:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### E se meu DataTable tiver mais colunas do que estilos?

O GemBox aplicará estilos apenas às colunas que possuírem uma entrada correspondente no array. Colunas extras usarão o estilo padrão—nenhum erro será lançado.

### Isso funciona com conjuntos de dados grandes?

Sim, mas fique de olho no limite de células da versão gratuita (150 k células). Para relatórios massivos, considere a licença paga ou faça o streaming dos dados linha a linha com `worksheet.Cells[row, col].Value = …`—embora você perca a conveniência do one‑liner.

### Como importo dados com formatação a partir de um modelo Excel existente?

Você pode carregar primeiro um workbook modelo:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Isso permite preservar logos de cabeçalho, rodapés e quaisquer estilos pré‑existentes enquanto ainda **importa dados com formatação** para a parte dinâmica.

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Execute o programa (`dotnet run`) e abra o *Report.xlsx* gerado para ver as cores aplicadas instantaneamente.

## Conclusão

Agora você tem uma base sólida, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}