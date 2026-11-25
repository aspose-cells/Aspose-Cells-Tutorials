---
category: general
date: 2026-11-25
description: Aprenda a criar várias planilhas em um arquivo Excel usando C#. Este
  guia aborda como salvar a pasta de trabalho como XLSX e lidar com nomes de planilhas
  duplicados.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: pt
lastmod: 2026-11-25
og_description: Crie várias planilhas em um arquivo Excel usando C#. Siga este tutorial
  completo para salvar a pasta de trabalho como XLSX e gerenciar nomes de planilhas
  duplicados.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Crie várias planilhas em um arquivo Excel com C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Como criar várias planilhas em um arquivo Excel usando C#
url: /pt/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar várias planilhas em um arquivo Excel usando C#

Se você precisa **criar várias planilhas** em uma pasta de trabalho Excel a partir de C#, este tutorial oferece uma solução pronta‑para‑executar. Ao final do guia você terá um programa que gera uma planilha mestre, cria planilhas de detalhe via smart markers e salva o resultado como um arquivo **XLSX** — enquanto lida com segurança com **nomes de planilhas duplicados**.

Você também verá como **create excel file c#** projetos com a biblioteca Aspose.Cells, uma escolha popular para automação de planilhas no lado do servidor.

## Pré-requisitos

* .NET 6.0 SDK ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE que suporte .NET)  
* O pacote NuGet **Aspose.Cells for .NET** (`Aspose.Cells`) – ele fornece as classes `Workbook`, `Worksheet` e `SmartMarkersFactory` usadas no código.  

Você pode adicionar o pacote com o seguinte comando CLI:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Use um feed NuGet privado ou a edição comunitária gratuita se você precisar apenas de recursos básicos.

## Visão geral da solução

A abordagem consiste em quatro etapas lógicas:

1. **Create a new workbook** e nomeie a primeira planilha como *Master*.  
2. **Insert a smart marker** que informa ao Aspose.Cells como nomear as planilhas de detalhe.  
3. **Process the smart marker** com uma fonte de dados que pode conter nomes duplicados.  
4. **Save the workbook** como um arquivo XLSX.  

Cada etapa é explicada em detalhe abaixo, e o arquivo de código completo é fornecido ao final do artigo.

## Etapa 1: Crie uma nova pasta de trabalho e adicione uma planilha mestre

A classe `Workbook` representa um arquivo Excel completo. Quando você a instancia sem parâmetros, o Aspose.Cells cria uma pasta de trabalho padrão que já contém uma única planilha. Renomear essa planilha para *Master* deixa o propósito da planilha claro.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Por que isso importa:**  
Começar com uma pasta de trabalho limpa evita formatação residual ou planilhas ocultas de execuções anteriores. Nomear a planilha *Master* ajuda a localizar o smart marker posteriormente e mantém o arquivo legível para usuários não técnicos.

## Etapa 2: Insira um smart marker que define os nomes das planilhas de detalhe

Smart markers são marcadores de posição que o Aspose.Cells substitui por dados em tempo de execução. A sintaxe `&=DetailSheetNewName=Detail` indica ao mecanismo que crie uma nova planilha para cada linha na fonte de dados, usando o valor da coluna `Detail` como nome da planilha.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Por que isso importa:**  
O smart marker elimina a necessidade de escrever um loop que adiciona planilhas manualmente. Ele também copia automaticamente o layout da planilha mestre para cada planilha recém‑gerada, garantindo consistência de estilo.

## Etapa 3: Processar o smart marker com uma fonte de dados que pode conter duplicatas

A seguir construímos um `DataTable` que simula uma fonte de dados. Observe que a coluna *Detail* contém valores duplicados (`"Report"` aparece duas vezes). O método `SmartMarkersFactory.Process` respeita a configuração `AllowDuplicateSheetNames`, que está **true** por padrão neste exemplo.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Importante:** Se você precisar garantir nomes de planilhas únicos, defina `workbook.Settings.CheckDuplicateSheetNames = true;` antes de processar. O comportamento padrão cria planilhas com o mesmo nome, o que o Excel permite, mas pode ser confuso ao navegar no arquivo.

## Etapa 4: Salvar a pasta de trabalho como um arquivo XLSX

Finalmente, persista a pasta de trabalho gerada no disco. O método `Save` escolhe automaticamente o gravador apropriado com base na extensão do arquivo.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Resultado esperado**

Ao abrir `duplicate_detail_sheets.xlsx` você verá:

| Nome da Planilha | Conteúdo (primeira linha) |
|------------------|---------------------------|
| Master           | Marcador inteligente (sem dados) |
| Report           | Linha de dados 1 (`123.45`) |
| Summary          | Linha de dados 2 (`67.89`) |
| Report (2)       | Linha de dados 3 (`101.12`) |

A segunda planilha *Report* é renomeada automaticamente para *Report (2)* pelo Aspose.Cells para evitar um erro crítico, ainda refletindo a intenção original de duplicação.

## Código-fonte completo

Copie o arquivo a seguir para um projeto de console (`dotnet new console`) e execute-o. O programa demonstra o fluxo de trabalho completo para **create multiple sheets** e **save workbook xlsx** enquanto lida com **duplicate sheet names**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Execute `dotnet run` a partir da pasta do projeto. Após a execução, abra o arquivo gerado para verificar que três planilhas de detalhe foram criadas, duas delas compartilhando o nome base **Report**.

## Tratamento de casos extremos e boas práticas

| Situação | Abordagem recomendada |
|----------|-----------------------|
| **Conjuntos de dados muito grandes** ( > 10 000 linhas) | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` para reduzir a pressão de memória. |
| **Regras personalizadas de nomeação de planilhas** | Pré‑procese a coluna `Detail` para substituir caracteres ilegais (`/ \ ? * [ ] :`) antes de chamar `Process`. |
| **Necessidade de nomes realmente únicos** | Defina `workbook.Settings.CheckDuplicateSheetNames = true;` e forneça um esquema de nomeação alternativo (ex.: anexar um GUID). |
| **Gerar PDFs em vez de XLSX** | Após salvar, chame `workbook.Save("output.pdf", SaveFormat.Pdf);` – o Aspose.Cells pode exportar diretamente para PDF. |
| **Executar em um serviço web** | Escreva a pasta de trabalho em um `MemoryStream` e retorne-a como download de arquivo para evitar I/O de disco. |

### Dica profissional: reutilize a mesma instância `Workbook` para múltiplas exportações

Se sua aplicação cria vários relatórios por requisição, mantenha um único objeto `Workbook` na memória, limpe suas planilhas (`workbook.Worksheets.Clear();`) e repita as etapas. Isso evita a sobrecarga de carregar repetidamente o runtime do Aspose.Cells.

## Conclusão

Agora você sabe como **create multiple sheets** em uma pasta de trabalho Excel usando C#, como **create excel file c#** com Aspose.Cells, como gerenciar **duplicate sheet names**, e como **save workbook xlsx** de forma confiável. O exemplo completo demonstra um padrão limpo e sustentável que escala de scripts rápidos a serviços de nível de produção.

### O que vem a seguir?

* Explore **conditional formatting** nas planilhas geradas para destacar valores‑chave.  
* Use **Smart Markers** para preencher tabelas, gráficos ou tabelas dinâmicas automaticamente.  
* Integre o código em uma API ASP.NET Core e retorne o arquivo XLSX como um fluxo de download.

Sinta-se à vontade para experimentar diferentes fontes de dados (JSON, XML ou um banco de dados) e adaptar a sintaxe do smart marker para atender às suas necessidades de relatório. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel C# – Guia passo a passo para escrever datas e salvar como XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Criar Nova Pasta de Trabalho em C# – Adicionar Fórmula e Salvar Arquivo Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Criar pasta de trabalho excel e salvá-la em arquivo em C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}