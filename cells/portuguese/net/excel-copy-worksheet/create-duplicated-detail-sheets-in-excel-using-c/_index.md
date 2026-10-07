---
category: general
date: 2026-10-07
description: Crie planilhas de detalhes duplicadas no Excel usando C#. Aprenda como
  gerar várias planilhas e construir um relatório a partir de tabelas em uma única
  execução.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: pt
lastmod: 2026-10-07
og_description: Crie planilhas de detalhes duplicadas no Excel com C#. Este tutorial
  mostra como gerar várias planilhas e produzir um relatório completo do Excel a partir
  de tabelas.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Crie planilhas de detalhes duplicadas no Excel – guia passo a passo em C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Criar planilhas de detalhes duplicadas no Excel usando C#
url: /pt/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar planilhas de detalhes duplicadas no Excel usando C#

Se você precisa **criar planilhas de detalhes duplicadas** em uma pasta de trabalho do Excel, este guia o conduz por todo o processo. Você verá como **gerar várias planilhas** a partir de um conjunto de dados mestre‑detalhe e produzir um relatório Excel polido diretamente das tabelas.

Gerar um relatório Excel a partir de tabelas é uma necessidade comum para sistemas de faturamento, painéis de inventário ou qualquer cenário em que um registro mestre possui várias linhas de detalhe relacionadas. Ao final deste tutorial você terá um programa C# executável que cria uma pasta de trabalho com uma planilha mestre e uma planilha com nome exclusivo para cada grupo de detalhes.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 (ou superior) instalado  
* Visual Studio 2022 ou qualquer IDE compatível com C#  
* O pacote NuGet **Aspose.Cells for .NET** (fornece `SmartMarkerProcessor`)  

Você pode adicionar o pacote com o seguinte comando:

```bash
dotnet add package Aspose.Cells
```

## Visão geral da solução

A solução segue estas cinco etapas:

1. **Obter a fonte de dados** que contém uma tabela mestre e duas tabelas de detalhe.  
2. **Configurar o processador Smart‑marker** para que cada planilha de detalhe duplicada receba um nome único.  
3. **Criar uma nova pasta de trabalho** e inserir um smart‑marker que referencia a tabela mestre.  
4. **Executar o processador** para gerar a planilha mestre e todas as planilhas de detalhe.  
5. **Salvar a pasta de trabalho** – cada planilha de detalhe agora tem um nome distinto.

Cada etapa é explicada em detalhes abaixo, com código completo e raciocínio.

## Etapa 1: Obter a fonte de dados que contém uma tabela mestre e duas tabelas de detalhe

A primeira tarefa é construir um `DataSet` que imite os dados que você normalmente recuperaria de um banco de dados. O `DataSet` deve conter uma tabela chamada **Master** e uma ou mais tabelas chamadas **Detail**. O mecanismo Smart‑marker usa esses nomes de tabela para preencher a pasta de trabalho.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Por que isso importa:**  
*Smart‑marker* trabalha com objetos `DataSet`; cada nome de tabela se torna um marcador que o mecanismo pode substituir. Ao estruturar os dados dessa forma, você permite que o processador duplique automaticamente a planilha de detalhe para cada `InvoiceId` distinto.

## Etapa 2: Configurar o processador Smart‑marker para dar a cada planilha de detalhe duplicada um nome único

Quando o processador encontra um marcador de detalhe, ele cria uma nova planilha para cada grupo de linhas. Por padrão, as novas planilhas compartilham o mesmo nome, o que gera um conflito de nomenclatura. Definir `DetailSheetNewName` indica ao mecanismo como renomear cada cópia.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Por que isso importa:**  
Sem um padrão de nomenclatura único, a pasta de trabalho lançaria uma exceção quando o processador tentar adicionar uma segunda planilha de detalhes. O placeholder `{0}` garante que cada planilha receba um nome distinto e previsível.

## Etapa 3: Criar uma nova pasta de trabalho e inserir um smart‑marker que referencia a tabela mestre

Agora você cria um `Workbook` novo, adiciona um marcador que aponta para a tabela **Master** e, opcionalmente, formata a linha de cabeçalho.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Por que isso importa:**  
O marcador `{{Master}}` instrui o processador a expandir a tabela mestre a partir de `A1`. As linhas subsequentes tornam‑se as linhas de dados para cada registro mestre. Este é o ponto de partida para **gerar relatório excel a partir de tabelas**.

## Etapa 4: Executar o processador Smart‑marker para gerar a planilha mestre e as planilhas de detalhe

Com a fonte de dados, o processador e o modelo prontos, você invoca `Process`. O mecanismo expande o marcador mestre e, em seguida, cria uma planilha de detalhe separada para cada `InvoiceId` distinto.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Por que isso importa:**  
`processor.Process` realiza o trabalho pesado: lê as linhas mestre, cria uma planilha de detalhe para cada chave única e renomeia essas planilhas de acordo com o padrão definido anteriormente. O resultado é uma pasta de trabalho que atende ao requisito **como gerar múltiplas planilhas**.

## Etapa 5: Salvar a pasta de trabalho resultante – cada planilha de detalhe agora tem um nome distinto

A chamada `Save` grava o arquivo no disco. Quando você abrir a pasta de trabalho, verá:

* **Sheet1** – a planilha mestre contendo os cabeçalhos das faturas.  
* **Detail_1**, **Detail_2**, … – cada planilha contém as linhas da tabela **Detail** que pertencem a uma fatura específica.

A seguir, uma ilustração do layout esperado da pasta de trabalho (a imagem é ilustrativa; você pode substituí‑la por uma captura de tela real, se desejar).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Saída esperada

| Nome da planilha | Descrição do conteúdo |
|------------------|-----------------------|
| **Sheet1** | Linhas mestre: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Linhas de detalhe onde `InvoiceId = 101` |
| **Detail_2** | Linhas de detalhe onde `InvoiceId = 102` |

Abrir `DuplicatedDetailSheets.xlsx` deve mostrar exatamente esta estrutura.

## Código‑fonte completo (pronto para copiar)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como nomear planilhas automaticamente – Gerar múltiplas planilhas em C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Como criar planilhas – Guia passo a passo para geração dinâmica de Excel](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Como gerar relatório Excel em C# – Guia completo usando SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}