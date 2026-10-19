---
category: general
date: 2026-07-13
description: Formate a coluna de data no Excel ao exportar um DataTable do C#. Aprenda
  a exportar DataTable para Excel em C# e a importar DataTable para Excel com formatação
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: pt
lastmod: 2026-07-13
og_description: Formate a coluna de data no Excel sem esforço. Este guia mostra como
  exportar um DataTable para Excel em C# e importar um DataTable para o Excel com
  estilos personalizados.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Formatar Coluna de Data no Excel – Tutorial de Exportação C# Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Formatar Coluna de Data no Excel – Guia Completo em C# para Exportar DataTable
url: /pt/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatar Coluna de Data no Excel – Guia Completo em C# para Exportar DataTable

Já precisou de **format date column Excel** ao extrair dados de um banco de dados, mas as células continuavam exibindo timestamps brutos? Você não está sozinho. Em muitos aplicativos empresariais a exportação padrão despeja um valor `DateTime` como `2024‑03‑15 00:00:00` e ninguém quer essa bagunça.  

A boa notícia é que você pode controlar a aparência exata de cada coluna diretamente do C#. Neste tutorial, vamos percorrer uma solução de ponta a ponta que **excel export datatable c#**, aplica um estilo de data à primeira coluna, um estilo de moeda à segunda e, finalmente, **import datatable to excel** com formatação sem esforço.

Ao final, você terá um método reutilizável que pode inserir em qualquer projeto .NET, independentemente de estar usando .NET 6, .NET Framework 4.8 ou uma versão posterior.

---

## O que você precisará

- **Aspose.Cells for .NET** (ou qualquer biblioteca que ofereça `CreateStyle` e `ImportDataTable`). Os trechos de código usam Aspose porque sua API é limpa e amplamente adotada.
- Uma **DataTable** que você já preenche a partir de SQL, CSV ou qualquer outra fonte.
- Visual Studio (ou sua IDE favorita).  
- Runtime .NET 5.0+ (o exemplo tem como alvo .NET 6, mas frameworks mais antigos funcionam da mesma forma).

Se ainda não tem o Aspose.Cells, obtenha uma avaliação gratuita no site oficial — sem necessidade de cartão de crédito.

## Etapa 1: Recuperar os Dados de Origem como um DataTable

Primeiro de tudo, você precisa de um `DataTable`. Em cenários reais isso geralmente vem de `SqlDataAdapter.Fill`, mas para fins de clareza vamos simular uma tabela simples:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Dica profissional:** Quando você extrair dados diretamente de um procedimento armazenado, certifique‑se de que os tipos de coluna correspondam aos formatos de Excel desejados. Uma coluna `datetime` será mais tarde o alvo para o nosso estilo **format date column excel**.

## Etapa 2: Criar uma Pasta de Trabalho Excel e Definir Estilos de Coluna

Agora criamos uma nova pasta de trabalho. O truque para **format date column excel** está em criar um objeto `Style`, definir sua propriedade `Number` para o formato de data interno do Excel (código 14) e atribuir esse estilo ao índice de coluna apropriado.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Por que `Number = 14`? O Excel armazena datas como números seriais; o formato 14 indica ao programa renderizar esses números usando o padrão de data curta da localidade. Se precisar de um padrão personalizado (como `dd‑MMM‑yyyy`), você pode definir `columnStyles[0].Custom = "dd-MMM-yyyy"` em vez disso.

## Etapa 3: Importar o DataTable para a Planilha com Estilos

Com o array de estilos pronto, a chamada de importação é uma única linha. Este é o coração de **excel export datatable c#** e também o local onde **import datatable to excel** enquanto preservamos nossa formatação.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

A sobrecarga `ImportDataTable` que estamos usando aceita o array de estilos, aplicando cada estilo à coluna correspondente à medida que os dados são gravados. Nenhum loop de pós‑processamento é necessário — sua coluna de data já está formatada de forma agradável.

## Etapa 4: Salvar a Pasta de Trabalho (ou Transmiti‑la Diretamente ao Navegador)

Dependendo do seu cenário, você pode salvar em disco, em um memory stream ou retornar o arquivo como resposta HTTP. Aqui estão três padrões comuns:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Atenção:** Se você estiver usando `FileResult` no ASP.NET Core, certifique‑se de definir `Response.Headers["Cache-Control"] = "no-cache"` quando o arquivo for gerado dinamicamente. Isso impede que o navegador sirva uma versão desatualizada.

## Etapa 5: Verificar o Resultado – Como a Planilha Excel Aparece

Depois de executar o código, abra `ExportedReport.xlsx`. Você deverá ver:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Observe como o **format date column excel** exibe uma data curta limpa, enquanto a coluna de moeda alinha‑se automaticamente com as configurações regionais. Nenhuma formatação manual célula por célula é necessária.

![format date column excel example](/images/format-date-column-excel.png)

*Texto alternativo da imagem: format date column excel – uma captura de tela da planilha Excel com a coluna de data devidamente formatada.*

## Perguntas Frequentes & Casos Limítrofes

### E se meu DataTable tiver mais de três colunas?

Basta estender o array `columnStyles`. Para qualquer coluna que você não estilizar explicitamente, deixe a entrada `null`; o Excel aplicará o formato padrão General.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Como Aplicar um Formato de Data Personalizado (por exemplo, “dd‑MMM‑yyyy”)?

Substitua o número interno por uma string personalizada:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Posso usar esta abordagem com EPPlus ou ClosedXML?

Sim, o conceito é idêntico: crie um objeto de estilo, atribua‑o a uma coluna e, em seguida, carregue o `DataTable`. A API difere, mas o padrão **excel export datatable c#** permanece o mesmo.

### E quanto a grandes DataSets (mais de 100 mil linhas)?

`ImportDataTable` é otimizado para gravações em lote, mas você pode atingir limites de memória. Nesse caso, considere transmitir linhas com `Cells.ImportDataTable` em blocos, ou usar `Worksheet.Cells["A1"].PutValue` em um loop reutilizando os objetos de estilo.

## Exemplo Completo Funcionando (Todas as Etapas em um Único Método)

Abaixo está um método autônomo que você pode copiar e colar em qualquer aplicativo console ou controlador ASP.NET. Ele demonstra todo o fluxo — da recuperação de dados à exportação Excel com estilos.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Execute o programa, abra `StyledExport.xlsx` e você verá o **format date column excel** aplicado perfeitamente.

## Recapitulação & Próximos Passos

Acabamos de cobrir como **format date column excel** ao realizar um **excel export datatable c#**, e como **import datatable to excel** com estilização por coluna em uma única chamada. Os principais pontos:

1. Crie um `Style` por coluna que você deseja formatar.  
2. Use `Number = 14` para datas, `Number = 2` para moeda, ou qualquer formato personalizado que precisar.  
3. Passe o array de estilos para `ImportDataTable` — a biblioteca faz o trabalho pesado.

O que você poderia explorar a seguir?

- **Formatação condicional** para destacar datas vencidas.  
- **

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Importar DataTable para Excel Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Exportar Dados do Excel para DataTable Usando Aspose.Cells para .NET: Um Guia Completo](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Exportar Strings HTML do Excel para DataTable usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}