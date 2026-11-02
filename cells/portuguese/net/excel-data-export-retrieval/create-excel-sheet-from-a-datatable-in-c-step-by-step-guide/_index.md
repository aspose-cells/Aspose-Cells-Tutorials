---
category: general
date: 2026-08-11
description: Criar planilha Excel a partir de um DataTable em C# e exportar o DataTable
  para Excel com nomeação automática da planilha. Aprenda como adicionar linhas ao
  DataTable e salvar a pasta de trabalho como xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: pt
lastmod: 2026-08-11
og_description: Criar planilha Excel a partir de um DataTable em C#. Este tutorial
  mostra como exportar um DataTable para Excel, adicionar linhas ao DataTable, gerar
  várias planilhas Excel e salvar a pasta de trabalho como xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Criar planilha Excel a partir de um DataTable em C# – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Criar planilha Excel a partir de um DataTable em C# – guia passo a passo
url: /pt/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar planilha excel a partir de um DataTable em C# – guia passo a passo

Se você precisa **criar planilha excel** a partir de um `DataTable` em C#, este guia mostra exatamente como fazer isso. Você verá como **exportar datatable para excel**, adicionar linhas, lidar com nomes de planilhas duplicados e, finalmente, **salvar a pasta de trabalho como xlsx**.

O exemplo usa Aspose.Cells, uma biblioteca .NET amplamente utilizada para automação de Excel. Os mesmos conceitos se aplicam a outras bibliotecas que suportam processamento no estilo SmartMarker, mas o código abaixo funciona pronto para uso com Aspose.Cells 22.12 ou posterior.

## Pré-requisitos

* .NET 6.0 SDK ou posterior instalado  
* Uma referência ao pacote NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Familiaridade básica com `DataTable` e aplicativos de console C#  

Esses requisitos mantêm o tutorial autocontido e evitam ferramentas externas.

## Etapa 1: Criar um DataTable que será exportado para Excel

O primeiro passo é construir um `DataTable` que reflita os dados que você deseja na planilha. Aqui criamos uma tabela chamada **Sheet1**, adicionamos uma coluna `Id` e inserimos duas linhas.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Por que isso importa:**  
`DataTable` é uma representação conveniente em memória de dados tabulares. Nomear a tabela `"Sheet1"` informa ao Aspose.Cells qual planilha deve ser alvo ao processar SmartMarkers.

## Etapa 2: Adicionar linhas ao DataTable (expansão opcional)

Se seus dados de origem são dinâmicos, você frequentemente precisará adicionar linhas em um loop. O trecho a seguir demonstra um padrão típico:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Dica:** Ao adicionar muitas linhas, considere desativar restrições (`dataTable.Constraints.Clear()`) para melhorar o desempenho.

## Etapa 3: Configurar opções SmartMarker para criar várias planilhas excel automaticamente

As opções SmartMarker permitem controlar como nomes de planilhas duplicados são tratados. Definir `DetailSheetNewName` como `"Sheet1_{0}"` instrui o Aspose.Cells a renomear planilhas subsequentes como `Sheet1_1`, `Sheet1_2` e assim por diante.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Por que isso importa:**  
Ao processar vários objetos `DataTable` que compartilham o mesmo nome, o Excel normalmente lançaria um erro porque os nomes das planilhas devem ser únicos. O padrão `DetailSheetNewName` elimina esse conflito automaticamente.

## Etapa 4: Processar os SmartMarkers e exportar datatable para excel

Agora criamos um novo `Workbook`, executamos `ProcessSmartMarkers` e deixamos o Aspose.Cells preencher a(s) planilha(s) com base no `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explicação:**  
`ProcessSmartMarkers` examina a pasta de trabalho em busca de marcadores como `&=Sheet1!A1` (não mostrados aqui) e os substitui pelos dados de `dataTable`. Como começamos com uma pasta de trabalho vazia, o Aspose.Cells cria uma nova planilha correspondendo ao nome da tabela e a preenche com as linhas que adicionamos.

## Etapa 5: Salvar a pasta de trabalho como xlsx

Finalmente, grave a pasta de trabalho no disco usando o formato OpenXML moderno (`.xlsx`). Você pode alterar o caminho para adequar ao seu ambiente.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultado:**  
Executar o programa produz um arquivo Excel que contém:

| Nome da Planilha | Linhas |
|------------------|--------|
| Sheet1           | 1, 2, 3, 4, 5 |
| Sheet1_1         | (se outro DataTable com o mesmo nome fosse processado) |

A lógica de renomeação de planilhas garante **criar múltiplas planilhas excel** sem gerenciamento manual de nomes.

## Variações comuns e casos extremos

| Situação | Como lidar |
|----------|------------|
| **Tabelas muito grandes** (≥ 100 000 linhas) | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` antes do processamento para manter o uso de memória baixo. |
| **Ordem de colunas personalizada** | Reordene os objetos `DataColumn` no `DataTable` antes de chamar `ProcessSmartMarkers`. |
| **Múltiplos DataTables com nomes diferentes** | Chame `ProcessSmartMarkers` para cada tabela; o Aspose.Cells criará uma planilha separada para cada nome automaticamente. |
| **Necessita de uma linha de cabeçalho com estilo** | Após o processamento, acesse `Worksheet.Cells["A1"]` e aplique as propriedades `Style` (fonte, plano de fundo). |
| **Salvar em um stream em vez de um arquivo** | Substitua `workbook.Save(outputPath, SaveFormat.Xlsx)` por `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Dica profissional:** Sempre envolva operações de sistema de arquivos em blocos `try…catch` para detectar problemas de permissão cedo.

## Código fonte completo (pronto para copiar)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Saída esperada

Executar o programa imprime:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Abrir `DuplicateSheets.xlsx` mostra uma planilha chamada **Sheet1** com a coluna `Id` contendo os valores `1, 2, 3, 4, 5`. Se você posteriormente processar outro `DataTable` chamado `"Sheet1"` na mesma pasta de trabalho, o Aspose.Cells criará **Sheet1_1**, **Sheet1_2**, etc., automaticamente.

## Conclusão

Agora você sabe como **criar planilha excel** a partir de um `DataTable` em C#, **exportar datatable para excel**, **adicionar linhas ao datatable**, gerar **criar múltiplas planilhas excel** com nomeação automática e **salvar a pasta de trabalho como xlsx**. O exemplo completo e executável demonstra o fluxo de trabalho de ponta a ponta e fornece dicas práticas para conjuntos de dados grandes e estilização personalizada.

### O que vem a seguir?

* Explore **formatação de células** (fontes, cores, bordas) acessando `Worksheet.Cells` após `ProcessSmartMarkers`.  
* Use **loops SmartMarker** para gerar relatórios mestre‑detalhe em uma única pasta de trabalho.  
* Mude para **exportação CSV** alterando `SaveFormat.Csv` se precisar de uma representação em texto simples.  

Sinta-se à vontade para adaptar o código às suas próprias fontes de dados — seja uma consulta de banco de dados, uma resposta de API ou uma coleção em memória. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e salvar uma pasta de trabalho Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Como criar e salvar uma pasta de trabalho Excel como SVG usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Como criar e exportar Excel para HTML usando Aspose.Cells Java | Guia de Operações de Pasta de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}