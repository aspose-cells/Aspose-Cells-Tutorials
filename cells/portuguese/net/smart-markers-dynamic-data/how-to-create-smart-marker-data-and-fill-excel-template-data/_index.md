---
category: general
date: 2026-10-10
description: Crie dados de marcadores inteligentes e preencha o modelo Excel usando
  marcadores inteligentes do Aspose.Cells. Siga este guia passo a passo para automatizar
  relatórios Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create smart marker data
- fill excel template data
- use aspose.cells smart markers
language: pt
lastmod: 2026-10-10
og_description: Crie dados de marcadores inteligentes com os marcadores inteligentes
  do Aspose.Cells e preencha os dados do modelo Excel em minutos. Este guia orienta
  você através de um exemplo completo e executável.
og_image_alt: Screenshot showing the process of creating smart marker data in an Excel
  worksheet
og_title: Criar dados de marcador inteligente e preencher dados do modelo do Excel
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  headline: How to create smart marker data and fill Excel template data
  type: TechArticle
- description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  name: How to create smart marker data and fill Excel template data
  steps:
  - name: '**Loading the workbook** gives the processor a concrete file to work on.'
    text: '**Loading the workbook** gives the processor a concrete file to work on.'
  - name: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
    text: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
  - name: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
    text: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
  - name: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
    text: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
  - name: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
    text: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
  - name: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
    text: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
  - name: Open a new Excel workbook.
    text: Open a new Excel workbook.
  - name: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
    text: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
  - name: Save the file as `Template.xlsx`.
    text: Save the file as `Template.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar dados de marcador inteligente e preencher dados do modelo do Excel
url: /pt/net/smart-markers-dynamic-data/how-to-create-smart-marker-data-and-fill-excel-template-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar dados de marcador inteligente e preencher dados de modelo Excel

Se você precisar **criar dados de marcador inteligente** para uma pasta de trabalho Excel, os marcadores inteligentes do Aspose.Cells tornam isso fácil. Este tutorial mostra como **preencher dados de modelo Excel** usando marcadores inteligentes em algumas linhas de código C#.

Você aprenderá como incorporar tags Smart Marker em um modelo, fornecer uma fonte de dados, executar o processador e salvar o arquivo preenchido. Nenhuma ferramenta externa é necessária — apenas Aspose.Cells para .NET e um projeto C# básico.

## O que você precisará

- .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+)
- Aspose.Cells for .NET (pacote NuGet `Aspose.Cells`)
- Uma pasta de trabalho Excel que contém tags Smart Marker como `${Comment:fieldName}`
- Um IDE C# (Visual Studio, Rider ou VS Code)

> **Dica profissional:** Mantenha a pasta de trabalho na mesma pasta do projeto ou use um caminho absoluto para evitar erros de arquivo não encontrado.

## Como criar dados de marcador inteligente com Aspose.Cells

O núcleo da solução é o `SmartMarkerProcessor`. Ele varre uma planilha em busca de tags, obtém os valores correspondentes de uma fonte de dados e grava os resultados de volta na planilha.

```csharp
using Aspose.Cells;
using System;

// 1️⃣ Load the workbook that contains Smart Marker tags.
Workbook workbook = new Workbook("Template.xlsx");

// 2️⃣ Get the worksheet where the tags reside.
Worksheet ws = workbook.Worksheets[0];

// 3️⃣ Prepare the data source that supplies values for the markers.
var dataSource = new[]
{
    new { fieldName = "Sample comment text generated by C#." }
};

// 4️⃣ Create a SmartMarkerProcessor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();

// 5️⃣ Process the worksheet, replacing Smart Marker tags with data from the source.
processor.Process(ws, dataSource);

// 6️⃣ Save the populated workbook.
workbook.Save("Result.xlsx");
```

### Por que cada linha importa

1. **Carregando a pasta de trabalho** fornece ao processador um arquivo concreto para trabalhar.  
2. **Selecionando a planilha** garante que o processador varra a folha correta; você pode direcionar qualquer folha por índice ou nome.  
3. **A fonte de dados** é um array de objetos anônimos. Cada nome de propriedade (`fieldName`) deve corresponder ao nome do marcador dentro de `${Comment:fieldName}`.  
4. **`SmartMarkerProcessor`** é o mecanismo que analisa as tags e realiza a substituição.  
5. **`Process`** realiza o trabalho pesado: ele lê cada tag `${...}`, procura a propriedade correspondente na fonte de dados e grava o valor na célula.  
6. **Salvando a pasta de trabalho** grava o arquivo atualizado no disco, pronto para consumo posterior.

## Preparando o modelo Excel para **preencher dados de modelo Excel**

1. Abra uma nova pasta de trabalho Excel.  
2. Em qualquer célula onde você desejar conteúdo dinâmico, digite uma tag Smart Marker, por exemplo:  

   ```
   ${Comment:fieldName}
   ```

3. Salve o arquivo como `Template.xlsx`.  

A sintaxe da tag segue o padrão `${<CollectionName>:<PropertyName>}`. Neste exemplo simples, omitimos o nome da coleção e usamos a coleção padrão, que é a fonte de dados passada para `Process`.

> **Caso extremo:** Se a tag referenciar uma propriedade que não exista na fonte de dados, o Aspose.Cells deixa a célula inalterada. Sempre verifique se os nomes das propriedades correspondem exatamente, incluindo diferenciação de maiúsculas e minúsculas.

## Construindo a fonte de dados para **usar marcadores inteligentes Aspose.Cells**

Você pode fornecer qualquer coleção enumerável — arrays, `List<T>`, `DataTable` ou até objetos personalizados. O processador itera sobre a coleção e repete linhas para cada item quando um marcador no estilo de tabela é usado.

```csharp
// Example with a List<T>
var comments = new List<Comment>
{
    new Comment { fieldName = "First comment." },
    new Comment { fieldName = "Second comment." }
};

processor.Process(ws, comments);
```

```csharp
public class Comment
{
    public string fieldName { get; set; }
}
```

Quando você fornece várias linhas, o Aspose.Cells expande automaticamente a região do modelo para acomodar todos os itens, o que é útil para gerar relatórios, faturas ou tabelas baseadas em dados.

## Processando a planilha usando **marcadores inteligentes Aspose.Cells**

O método `Process` pode aceitar configurações opcionais, como:

- `SmartMarkerOptions` para controlar como células vazias são tratadas.
- `DataSourceOptions` para especificar um nome de coleção diferente.

```csharp
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Preserve empty cells as blanks instead of removing them.
    PreserveEmptyCells = true
};

processor.Process(ws, dataSource, options);
```

Essas opções dão a você controle granular sobre a operação de **preencher dados de modelo Excel**, garantindo que a saída corresponda aos seus requisitos de formatação.

## Salvando o resultado e verificando a saída

Após o processamento, você pode salvar a pasta de trabalho em qualquer formato suportado pelo Aspose.Cells, como XLSX, CSV ou PDF.

```csharp
workbook.Save("Result.pdf", SaveFormat.Pdf);
```

Abra `Result.xlsx` (ou `Result.pdf`) para verificar se o placeholder `${Comment:fieldName}` foi substituído por **Sample comment text generated by C#**. Se a célula ainda mostrar a tag original, verifique novamente o nome da propriedade na fonte de dados.

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Solução |
|----------|-------|--------|
| Tag não substituída | Incompatibilidade no nome da propriedade (ex.: `fieldname` vs `fieldName`) | Garantir correspondência exata sensível a maiúsculas/minúsculas |
| Linhas não duplicadas | Fonte de dados contém apenas um objeto enquanto o modelo espera uma tabela | Fornecer uma coleção com múltiplos itens |
| Pasta de trabalho falha ao salvar | Uso de uma versão desatualizada do Aspose.Cells | Atualizar para o pacote NuGet mais recente |
| Formatação perdida | O processador sobrescreve o estilo da célula | Preservar o estilo com `SmartMarkerOptions.PreserveCellFormatting = true` |

## Exemplo completo em funcionamento

Abaixo está um programa autocontido que você pode copiar, colar e executar.

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Load the template that contains the Smart Marker tag ${Comment:fieldName}
            Workbook workbook = new Workbook("Template.xlsx");
            Worksheet ws = workbook.Worksheets[0];

            // Create a list of data objects – each object maps to the marker property.
            var data = new List<Comment>
            {
                new Comment { fieldName = "First generated comment." },
                new Comment { fieldName = "Second generated comment." },
                new Comment { fieldName = "Third generated comment." }
            };

            // Initialise the processor and run it.
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.Process(ws, data);

            // Save the populated workbook.
            workbook.Save("Result.xlsx");
            Console.WriteLine("Smart marker processing complete. Check Result.xlsx.");
        }
    }

    public class Comment
    {
        public string fieldName { get; set; }
    }
}
```

**Resultado esperado:** Em `Result.xlsx`, a célula que originalmente continha `${Comment:fieldName}` se expande em três linhas, cada uma preenchida com o texto de comentário correspondente da lista `data`.

## Conclusão

Agora você sabe como **criar dados de marcador inteligente**, **preencher dados de modelo Excel** e **usar marcadores inteligentes Aspose.Cells** para automatizar a geração de relatórios Excel. O processo se resume a três ações: incorporar tags Smart Marker, fornecer uma fonte de dados correspondente e invocar `SmartMarkerProcessor.Process`. A partir daqui, você pode explorar cenários mais avançados, como coleções aninhadas, formatação condicional ou exportação para PDF.

### Próximos passos

- Experimente **marcadores inteligentes no estilo de tabela** para gerar tabelas com várias linhas automaticamente.  
- Combine marcadores inteligentes com **formatação condicional** para destacar linhas que atendam a determinados critérios.  
- Revise a documentação do Aspose.Cells sobre **opções de Smart Marker** para otimização de desempenho.

Feliz codificação, e aproveite o tempo economizado ao automatizar seus fluxos de trabalho Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automatizar pastas de trabalho Excel com Aspose.Cells .NET: Utilizar Smart Markers para Processamento Eficiente de Dados](/cells/english/net/automation-batch-processing/automate-excel-aspose-cells-workbook-smart-markers/)
- [Dominar Smart Markers e Integração DataTable do Aspose.Cells .NET para Gerenciamento Eficiente de Dados no Excel](/cells/english/net/import-export/aspose-cells-net-smart-markers-data-table-integration/)
- [Mesclagem de dados Excel em C# – Guia Completo de Smart Marker](/cells/english/net/smart-markers-dynamic-data/excel-data-merging-in-c-complete-smart-marker-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}