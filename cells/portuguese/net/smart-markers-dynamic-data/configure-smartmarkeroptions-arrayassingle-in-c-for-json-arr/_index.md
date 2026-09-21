---
category: general
date: 2026-09-21
description: Configure a opção **ArrayAsSingle** do **SmartMarkerOptions** em C# para
  exportar arrays JSON como um único valor de célula em uma pasta de trabalho do Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: pt
lastmod: 2026-09-21
og_description: Configure a opção ArrayAsSingle do SmartMarkerOptions em C# para exportar
  arrays JSON como um único valor de célula. Aprenda a solução completa passo a passo.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Configure SmartMarkerOptions ArrayAsSingle em C# – guia completo
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Configurar SmartMarkerOptions ArrayAsSingle em C# para arrays JSON
url: /pt/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configurar SmartMarkerOptions ArrayAsSingle em C# para arrays JSON

Se você precisar **configurar SmartMarkerOptions ArrayAsSingle** ao gerar arquivos Excel com Aspose.Cells, este guia mostra exatamente como fazer isso. Você verá como manter um array JSON intacto em uma única célula em vez de espalhar seus elementos em várias linhas.

Trabalhar com dados JSON em planilhas geralmente significa escolher entre uma visualização achatada e uma representação compacta. Em muitos cenários de relatório—como armazenar uma lista de tags ou um conjunto de identificadores—você deseja que a string JSON inteira permaneça em uma única célula. A flag **ArrayAsSingle** em `SmartMarkerOptions` torna isso possível.

Neste tutorial você vai:

* Criar um `DataTable` que contém um array JSON em uma coluna.  
* Inserir Smart Markers em uma planilha Excel.  
* **Configurar SmartMarkerOptions ArrayAsSingle** para que o array JSON seja tratado como um valor de célula único.  
* Processar os marcadores e salvar a pasta de trabalho.  
* Verificar o resultado.

> **Pré‑requisitos** – Você precisa da biblioteca Aspose.Cells for .NET (v23.12 ou posterior) e de um ambiente de desenvolvimento .NET (Visual Studio 2022 recomendado). Conhecimento básico de C# e DataTables é presumido.

---

## Etapa 1: Preparar a fonte de dados com um array JSON

Primeiro, construa um `DataTable` que imita os dados que você receberia de um serviço ou de um banco de dados. A coluna **Names** contém uma string codificada em JSON representando um array de nomes.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Por que esta etapa?*  
Smart Markers leem dados diretamente de objetos .NET. Ao colocar o array JSON em uma coluna de string, você preserva a sintaxe JSON exata, que depois pode ser escrita em uma célula sem alterações.

---

## Etapa 2: Inserir Smart Markers em uma nova pasta de trabalho

Crie uma nova pasta de trabalho, selecione a primeira planilha e escreva Smart Markers que referenciam toda a tabela e a coluna específica **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

O marcador `&=dataTable.Names` indica ao Aspose.Cells que substitua a célula pelo valor da coluna **Names** para cada linha em `dataTable`. Como temos apenas uma linha, o marcador será processado uma única vez.

---

## Etapa 3: **Configurar SmartMarkerOptions ArrayAsSingle**

Por padrão, o Aspose.Cells expande uma string semelhante a um array em linhas separadas. Definir `ArrayAsSingle` como `true` sobrescreve esse comportamento, forçando a string JSON inteira a permanecer em uma única célula.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Por que habilitar `ArrayAsSingle`?*  
Quando `ArrayAsSingle` está `false`, o mecanismo interpreta `["Alice","Bob"]` como dois valores separados e os grava em linhas adjacentes. Definindo-o como `true` trata a string como um valor atômico, o que é essencial para preservar o formato JSON dentro do Excel.

---

## Etapa 4: Processar os Smart Markers com as opções configuradas

Agora execute o motor Smart Marker, passando o objeto de opções que você acabou de configurar.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Durante o processamento, o Aspose.Cells lê o `dataTable`, aplica os marcadores e respeita a flag `ArrayAsSingle`, deixando o array JSON intacto.

---

## Etapa 5: Salvar a pasta de trabalho e verificar o resultado

Por fim, grave a pasta de trabalho no disco. Abra o arquivo gerado no Excel ou em qualquer visualizador de planilhas para confirmar que a célula **A2** contém a string JSON exata.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Saída esperada

| A   |
|-----|
| **["Alice","Bob"]** |

A célula **A2** mostra o array JSON como um único valor de texto, exatamente como armazenado no `DataTable`. Nenhuma linha extra é criada.

---

## Variações comuns e tratamento de casos extremos

| Situação | Como adaptar |
|-----------|--------------|
| **Múltiplas linhas com arrays JSON** | A mesma configuração `ArrayAsSingle` funciona; o array JSON de cada linha permanece em sua própria célula. |
| **Estruturas JSON diferentes (objetos, arrays aninhados)** | Enquanto o JSON for uma string, `ArrayAsSingle` o manterá intacto. Para objetos complexos pode ser necessário escapar as aspas. |
| **Uso de uma fonte de dados diferente (por exemplo, List\<T\>)** | Substitua o `DataTable` por qualquer coleção enumerável; a sintaxe do marcador (`&=myList.Property`) permanece a mesma. |
| **Exportação para CSV em vez de XLSX** | `ArrayAsSingle` ainda se aplica, mas lembre‑se de que CSV não preserva formatação de célula; pode ser necessário envolver o JSON em aspas. |

**Dica profissional:** Sempre defina `ArrayAsSingle` *antes* de chamar `ProcessSmartMarkers`. Alterar a flag após o processamento não tem efeito nas células já geradas.

---

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar e colar em uma aplicação console. Ele inclui todas as diretivas `using` e comentários para clareza.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Execute o programa, abra `SmartMarkerJson.xlsx` e você verá o array JSON preservado na célula **A2**.

---

## Conclusão

Agora você sabe como **configurar SmartMarkerOptions ArrayAsSingle** em C# para manter um array JSON como um valor de célula único ao usar smart markers do Aspose.Cells. As etapas—preparar um `DataTable`, inserir marcadores, definir a flag `ArrayAsSingle`, processar e salvar—formam um padrão repetível que pode ser aplicado a qualquer cenário onde seja necessária uma representação JSON compacta dentro do Excel.

Em seguida, você pode explorar:

* **Smart markers do Aspose.Cells** para percorrer coleções.  
* Exportar **objetos JSON aninhados** personalizando a formatação de célula.  
* Combinar **formatação condicional** com smart markers para relatórios mais ricos.

Sinta‑se à vontade para experimentar diferentes estruturas de dados e compartilhar suas descobertas. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar pasta de trabalho Excel a partir de JSON – Guia completo do Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Criar e Configurar Pasta de Trabalho Excel Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Criar e Configurar Pasta de Trabalho Excel Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}