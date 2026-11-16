---
category: general
date: 2026-11-16
description: Crie Excel a partir de JSON usando SmartMarker. Aprenda como converter
  JSON para Excel, incorporar JSON no Excel e salvar a pasta de trabalho xlsx em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: pt
lastmod: 2026-11-16
og_description: Crie Excel a partir de JSON rapidamente. Este tutorial mostra como
  converter JSON para Excel, incorporar JSON no Excel e salvar a pasta de trabalho
  .xlsx com Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Crie Excel a partir de JSON com SmartMarker – guia passo a passo em C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Criar Excel a partir de JSON com SmartMarker em C#
url: /pt/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel a partir de JSON com SmartMarker em C#

Se você precisar **criar Excel a partir de JSON** em um projeto .NET, este guia mostra uma solução completa e executável. Usando o processador Smart Marker do Aspose.Cells, você pode **converter JSON para Excel**, inserir a string JSON diretamente em uma célula e **salvar workbook xlsx** sem escrever nenhum código de análise manual.

Você verá como registrar uma fonte de dados JSON, inserir um Smart Marker que gera todo o array como uma única string JSON, processar a planilha e, finalmente, gravar o arquivo no disco. Ao final do tutorial, você poderá gerar um arquivo Excel que contém a carga JSON original na célula A1, pronto para processamento ou relatórios posteriores.

## Pré-requisitos

- .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+)
- Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`)
- Conhecimento básico de C# e formatação JSON
- Uma IDE como Visual Studio ou VS Code

## Etapa 1: Configurar o projeto e importar namespaces

Crie uma nova aplicação console e adicione o pacote Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Em seguida, inclua os namespaces necessários no início do `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Por quê?**  
`Aspose.Cells` fornece o modelo de workbook, enquanto `Aspose.Cells.SmartMarkers` contém a classe `SmartMarkerProcessor` que interpreta os marcadores `&=` na planilha.

## Etapa 2: Definir a fonte de dados JSON

Coloque a string JSON em uma variável. Neste exemplo, temos um array de pedidos:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Por quê?**  
Smart Marker funciona com qualquer JSON bem‑formado. Manter o JSON em uma string permite registrá-lo diretamente sem precisar de um arquivo no disco.

## Etapa 3: Registrar os dados JSON com SmartMarkerProcessor

Crie uma instância de `SmartMarkerProcessor` e associe a string JSON a um nome que você referenciará posteriormente na planilha:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Por quê?**  
`RegisterJsonDataSource` analisa o JSON e disponibiliza sua hierarquia para os Smart Markers. O nome `"OrdersJson"` torna‑se o objeto raiz nas expressões dos marcadores.

## Etapa 4: Criar um workbook e inserir o Smart Marker

Instancie um novo workbook, obtenha sua primeira planilha e escreva um Smart Marker na célula A1 que gerará todo o array `Orders` como uma única string JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Por quê?**  
A expressão `OrdersJson.Orders.ArrayAsSingle` indica ao Smart Marker que pegue o array `Orders` e o serialize novamente para JSON, colocando o resultado na célula de destino. Esta é a maneira mais direta de **incorporar JSON no Excel**.

## Etapa 5: Processar a planilha

Execute o processador para que ele substitua o marcador pela string JSON real:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Por quê?**  
O processamento examina cada célula em busca de marcadores `&=`, avalia‑os em relação às fontes de dados registradas e grava o valor avaliado de volta na planilha.

## Etapa 6: Salvar o workbook como um arquivo .xlsx

Finalmente, grave o workbook no disco. Ajuste o caminho para uma pasta na qual você tenha permissão de gravação:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Por quê?**  
`SaveFormat.Xlsx` garante que o arquivo seja armazenado no formato moderno Office Open XML, atendendo ao requisito de **save workbook xlsx**.

## Código-fonte completo

Juntando todas as partes, aqui está o programa completo, pronto‑para‑executar:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Saída esperada no Excel

Abra `JsonArraySingleCell.xlsx`. A célula A1 conterá:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

A string JSON é uma representação compacta do array `Orders` original, facilitando o transporte ou consumo em fluxos de trabalho subsequentes baseados em Excel.

## Variações comuns e casos de borda

| Situação | Ajuste |
|-----------|------------|
| **Múltiplos objetos JSON** | Registre cada objeto com um nome distinto (por exemplo, `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) e faça referência a eles com marcadores separados. |
| **JSON formatado (pretty‑printed) em uma célula** | Use a opção `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Grandes cargas JSON** | Considere gravar o JSON em uma planilha oculta ou usar a conversão para `DataTable` para melhorar o desempenho. |
| **Incorporar JSON em várias células** | Coloque marcadores diferentes em outras células, por exemplo, `&=OrdersJson.Orders[0].Id` para extrair campos individuais. |

**Dica profissional:** Ao lidar com JSON muito grande, aumente o buffer de memória do workbook (`WorkbookSettings.MemorySetting`) para evitar `OutOfMemoryException`.

## Testando a solução

1. Compile e execute o aplicativo console (`dotnet run`).  
2. Verifique se o console exibe o caminho completo do arquivo gerado.  
3. Abra o arquivo no Excel ou em qualquer visualizador de planilhas.  
4. Confirme que a célula A1 contém a string do array JSON exatamente como mostrada acima.

Se a célula contiver o texto do marcador (`&=OrdersJson...`) em vez do JSON, verifique novamente se o processador foi invocado **depois** que o marcador foi inserido e se a string JSON é válida.

## Conclusão

Agora você sabe como **criar Excel a partir de JSON** usando Aspose.Cells Smart Markers, como **converter JSON para Excel**, incorporar a carga JSON diretamente em uma célula e **salvar workbook xlsx** com uma única linha de código. Essa abordagem elimina a análise manual, funciona com qualquer estrutura JSON e produz um arquivo Excel limpo e em conformidade com os padrões.

### Próximos passos

- Explore **loops de Smart Marker** (`&=OrdersJson.Orders`) para gerar uma linha para cada pedido em vez de uma única string JSON.  
- Combine esta técnica com **fórmulas do Excel** para calcular totais a partir dos dados incorporados.  
- Investigue **ler JSON de volta do Excel** usando `Workbook.Load` e `SmartMarkerProcessor` em sentido inverso.

Sinta‑se à vontade para experimentar diferentes formatos de JSON, várias planilhas ou exportar para outros formatos como CSV ou PDF. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Excel a partir de JSON com Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Criar Workbook Excel a partir de JSON – Guia Completo Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Salvar Workbook Excel a partir de JSON – Guia Completo](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}