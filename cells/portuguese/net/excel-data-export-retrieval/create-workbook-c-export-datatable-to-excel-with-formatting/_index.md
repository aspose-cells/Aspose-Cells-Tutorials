---
category: general
date: 2026-02-15
description: Crie uma planilha em C# e exporte um DataTable para o Excel com formatação
  de linhas, defina o fundo da linha e automatize tarefas do Excel em minutos.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: pt
og_description: Crie uma planilha C# rapidamente, aplique estilos de linha e automatize
  a exportação para Excel com exemplos de código completos e dicas de boas práticas.
og_title: Criar Workbook C# – Exportar DataTable para Excel com Formatação
tags:
- C#
- Excel
- DataExport
title: Criar Workbook C# – Exportar DataTable para Excel com Formatação
url: /pt/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Workbook C# – Exportar DataTable para Excel com Formatação

Já precisou **criar workbook C#** e despejar um `DataTable` no Excel com estilo personalizado? Você não está sozinho. Em muitas aplicações de linha de negócio, a exigência é gerar uma planilha bem formatada que um usuário não‑técnico possa abrir e entender instantaneamente.  

Neste guia vamos percorrer uma solução completa, pronta‑para‑executar, que mostra **como criar workbook C#**, aplicar **excel export formatting**, definir um **row background**, e aproveitar **excel automation c#** para produzir um arquivo refinado. Sem atalhos vagos “consulte a documentação” — apenas o código completo, explicações sobre por que cada linha importa e dicas que você realmente usará amanhã.

---

## Pré‑requisitos

- .NET 6 (ou .NET Framework 4.6+).  
- Visual Studio 2022 ou qualquer IDE compatível com C#.  
- O pacote NuGet **Aspose.Cells for .NET** (ou qualquer biblioteca que exponha `Workbook`, `Worksheet`, `Style`).  
- Familiaridade básica com `DataTable`.  

Se ainda não tem o Aspose.Cells, execute:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** O trial gratuito funciona na maioria dos cenários de desenvolvimento; apenas lembre‑se de substituir a chave de licença antes de publicar.

---

![Exemplo de criação de workbook C# mostrando linhas estilizadas no Excel]( "Exemplo de criação de workbook C# com cores de fundo nas linhas")

---

## Etapa 1: Inicializar o Workbook e a Worksheet (Create Workbook C#)

A primeira coisa que você deve fazer é instanciar um `Workbook`. Pense nele como abrir um arquivo Excel novinho em folha na memória.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Por que?**  
`Workbook` contém todo o documento Excel, enquanto `Worksheet` representa uma única aba. Começar com um workbook limpo garante que você controla cada aspecto da saída — sem estilos padrão ocultos surgindo inesperadamente.

---

## Etapa 2: Preparar um DataTable de Exemplo (Export DataTable Excel)

Em um projeto real você buscaria os dados em um banco, mas para ilustração vamos criar um pequeno `DataTable` na hora.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Por que isso importa:**  
Exportar um `DataTable` é a forma mais comum de mover dados tabulares de uma aplicação para o Excel. O método acima é totalmente autônomo, então você pode copiar‑colar em qualquer projeto e ele funcionará.

---

## Etapa 3: Criar um Estilo por Linha (Excel Export Formatting)

Para dar a cada linha sua própria cor de fundo, geramos um objeto `Style` para cada linha do `DataTable`. É aqui que **excel export formatting** brilha.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Por que estilizar linha a linha?**  
Se precisar destacar registros específicos (por exemplo, faturas vencidas) você pode substituir o ciclo simples de cores por lógica condicional — basta definir `style.ForegroundColor` com base nos dados da linha.

---

## Etapa 4: Importar o DataTable com Estilos de Linha (Set Row Background)

Agora juntamos tudo: os dados, o workbook e os estilos.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**O que você verá:**  
Abrir `EmployeesReport.xlsx` mostra uma linha de cabeçalho com formatação padrão, seguida por quatro linhas de dados cada uma pintada com uma cor de fundo clara. O resultado parece um relatório artesanal, não um despejo sem graça.

---

## Etapa 5: Dicas Avançadas de Excel Automation C# (Excel Automation C#)

Abaixo estão alguns truques rápidos que você pode aplicar ao exemplo básico:

| Dica | Trecho de Código | Quando Usar |
|-----|------------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Após importar os dados para evitar texto truncado. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Quando a tabela pode rolar além da tela. |
| **Conditional Formatting** | <details><summary>Mostrar</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Destacar salários acima de um limite. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Quando precisar de relatórios somente leitura. |

Esses trechos demonstram a amplitude de **excel automation c#** — você pode continuar estendendo o workbook sem reescrever a lógica central de importação.

---

## Perguntas Frequentes & Casos de Borda

**E se o DataTable tiver milhares de linhas?**  
Aspose.Cells transmite dados de forma eficiente, mas você pode querer desativar a criação de estilo para cada linha a fim de economizar memória. Em vez disso, aplique um único estilo a um intervalo:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Posso exportar para .csv em vez de .xlsx?**  
Claro — basta mudar o formato de salvamento:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

A formatação será perdida (CSV não possui estilos), mas a exportação de dados permanece a mesma.

**Isso funciona no .NET Core?**  
Sim. Aspose.Cells suporta .NET Standard 2.0 e posteriores, então o mesmo código roda no .NET 6, .NET 7 ou .NET Framework.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}