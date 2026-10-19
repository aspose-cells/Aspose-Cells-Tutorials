---
category: general
date: 2026-08-11
description: Importe JSON para Excel usando C# e Aspose.Cells. Carregue o JSON em
  um DataSet, processe marcadores inteligentes e salve como xlsx em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: pt
lastmod: 2026-08-11
og_description: Importe JSON para Excel usando C# e Aspose.Cells. Este guia mostra
  como carregar JSON em um DataSet, processar smart markers e salvar a pasta de trabalho
  como um arquivo xlsx, permitindo uma exportação de dados perfeita.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: Importar JSON para Excel com C# – guia completo passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: Importar JSON para Excel em C# – guia passo a passo
url: /pt/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar json para excel em C# – guia passo a passo

Se você precisa importar json para excel com C#, este tutorial o guiará por todo o processo. Você aprenderá como carregar JSON em um DataSet, aplicar um smart marker e salvar o resultado como um arquivo xlsx. A mesma abordagem também permite converter json para xlsx para pipelines de relatórios ou scripts de migração de dados.

O guia cobre cada linha de código necessária, explica por que cada etapa é importante e destaca armadilhas comuns. Ao final, você poderá exportar dados json para excel sem escrever analisadores personalizados, e entenderá como salvar a workbook c# de forma pronta para produção. Nenhuma ferramenta externa além do Aspose.Cells é necessária.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou posterior instalado  
- Visual Studio 2022 (ou qualquer IDE que suporte .NET)  
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Um arquivo de modelo Excel que contém um smart marker (por exemplo, `Template.xlsx`)  

O modelo deve ter uma única célula com o smart marker `&=Table(Data)`, onde `Data` corresponde ao nome da DataTable que você passará.

## Importar json para excel – configurar o projeto

Crie um novo aplicativo console e adicione a referência ao Aspose.Cells:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

Adicionar as diretivas `using` no topo permite que o compilador localize `DataSet`, `Workbook` e tipos relacionados. Essa base é necessária para todas as operações subsequentes.

## Converter json para xlsx – carregar JSON em um DataSet

A primeira etapa funcional é transformar a string JSON em um `DataSet`. Aspose.Cells fornece uma extensão conveniente `ReadJson` que analisa um array de objetos diretamente em uma tabela.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**Por que isso importa:**  
`ReadJson` cria automaticamente uma `DataTable` chamada `Table` (ou o nome do elemento raiz) e preenche as colunas com base nas chaves do JSON. Isso elimina loops manuais e garante que os tipos de dados sejam inferidos corretamente. Se seu JSON contiver objetos aninhados, Aspose.Cells os achata em tabelas separadas que você pode referenciar posteriormente.

**Dica:**  
Se a carga JSON for grande, considere transmiti‑la com um `StringReader` para evitar carregar a string inteira na memória.

## Exportar dados json para excel – abrir o modelo Excel com um smart marker

Em seguida, abra a workbook que contém o smart marker. O smart marker indica ao Aspose.Cells onde inserir os dados do `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**Por que isso importa:**  
O modelo isola a formatação do código. Você pode projetar a aparência final no Excel (fontes, bordas, formatação condicional) e deixar a biblioteca lidar com a inserção de dados. A sintaxe do smart marker `&=Table(Data)` instrui o motor a escrever toda a `DataTable` na célula onde o marcador está.

## Exportar dados json para excel – processar o smart marker

Agora processe o smart marker, passando a `DataTable` que foi criada a partir do JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**Por que isso importa:**  
`ProcessSmartMarkers` lê o marcador, expande a tabela verticalmente e mantém a formatação original da célula. O método também respeita larguras de coluna e aplica formatos numéricos automaticamente com base nos tipos .NET subjacentes.

**Caso extremo:**  
Se a célula de destino já contiver dados, o método sobrescreve‑os. Para preservar o conteúdo existente, coloque o marcador em uma área dedicada do modelo.

## Salvar workbook c# – gravar o arquivo final

Finalmente, salve a workbook como um arquivo `.xlsx`. Você pode escolher qualquer local onde sua aplicação tenha permissão de gravação.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**Por que isso importa:**  
Especificar `SaveFormat.Xlsx` garante que a saída esteja em conformidade com o padrão Open XML, tornando‑a legível por aplicativos de planilha modernos. Se precisar de um arquivo legado `.xls`, substitua `SaveFormat.Xlsx` por `SaveFormat.Excel97To2003`.

**Dica profissional:**  
Use `SaveOptions` para controlar o nível de compressão de arquivos grandes, por exemplo, `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## Código-fonte completo

Juntando todas as etapas resulta em um programa executável:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**Saída esperada:**  
Executar o programa cria `JsonSingleCell.xlsx`. Ao abrir o arquivo, você verá as duas linhas (`John`, `30` e `Anna`, `25`) preenchidas abaixo da célula com smart‑marker, preservando qualquer formatação de cabeçalho que você definiu em `Template.xlsx`.

![Exemplo de código de importação de json para excel](image.png "Exemplo de código de importação de json para excel")

## Perguntas comuns e como lidar com elas

- **E se o array JSON estiver vazio?**  
  `ReadJson` ainda cria uma `DataTable` vazia. O smart marker produzirá apenas a linha de cabeçalho, que costuma ser o resultado desejado para modelos de relatório.

- **Posso importar múltiplos arrays JSON em planilhas diferentes?**  
  Sim. Carregue cada array em sua própria `DataTable` dentro do mesmo `DataSet`, então chame `ProcessSmartMarkers` em cada planilha, referenciando o nome da tabela apropriado no marcador (por exemplo, `&=Table(Orders)`).

- **Como controlo a ordem das colunas?**  
  Após `ReadJson`, reordene as colunas manipulando `dataSet.Tables[0].Columns` antes de processar o smart marker.

- **É possível escrever JSON diretamente em uma única célula como string?**  
  Se precisar da string JSON bruta em uma célula, pule a etapa `DataSet` e atribua diretamente: `worksheet.Cells["A1"].PutValue(jsonData);`

## Conclusão

Agora você sabe como importar json para excel em C# usando Aspose.Cells, desde carregar JSON em um DataSet até processar um smart marker e salvar a workbook c#. Esta solução de ponta a ponta permite converter json para xlsx rapidamente, exportar dados json

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Importar JSON para Excel sem esforço usando Aspose.Cells para .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Importar Dados JSON para Excel usando Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importar JSON para Excel de forma eficiente usando Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}