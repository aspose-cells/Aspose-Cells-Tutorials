---
category: general
date: 2026-10-10
description: Converter JSON para XLSX em C# com SmartMarker – aprenda como importar
  JSON para o Excel e preencher uma planilha programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: pt
lastmod: 2026-10-10
og_description: Converta JSON para XLSX em C# com SmartMarker. Siga este guia para
  importar JSON para o Excel, criar uma pasta de trabalho Excel em C# e preencher
  o Excel a partir de JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Converter JSON para XLSX em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Converter JSON para XLSX em C# usando SmartMarker
url: /pt/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter JSON para XLSX em C# usando SmartMarker

Se você precisa **converter JSON para XLSX em C#**, este guia mostra como **importar JSON para o Excel** e **preencher o Excel a partir do JSON** com apenas algumas linhas de código. Você verá como **criar uma pasta de trabalho Excel C#**, configurar o processador SmartMarker e, finalmente, **importar JSON para as células da planilha**.

> **O que você obterá** – um exemplo totalmente executável que lê um array JSON, trata-o como um único registro e grava os dados em um arquivo `.xlsx` pronto para relatórios ou análises posteriores.

## Converter JSON para XLSX – visão geral

SmartMarker faz parte da biblioteca Aspose.Cells e permite vincular JSON, XML ou qualquer objeto .NET diretamente a um modelo Excel. Neste tutorial nós:

1. **Criamos uma pasta de trabalho Excel** na memória.  
2. **Carregamos os dados JSON** que representam uma lista simples de pessoas.  
3. **Configuramos o SmartMarker** para tratar o array JSON como um único registro (`ArrayAsSingle = true`).  
4. **Processamos a planilha**, permitindo que o SmartMarker substitua os marcadores pelos valores do JSON.  
5. **Salvamos a pasta de trabalho** como um arquivo `.xlsx`.

Todo o fluxo roda em .NET 6+ e requer apenas o pacote NuGet `Aspose.Cells`.

## Etapa 1: Criar uma pasta de trabalho Excel em C#

Primeiro, adicione o pacote Aspose.Cells ao seu projeto:

```bash
dotnet add package Aspose.Cells
```

Agora você pode instanciar um novo `Workbook`. A pasta de trabalho começa vazia, mas você pode adicionar uma planilha e colocar tags SmartMarker onde os dados JSON devem aparecer.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Por que criamos a pasta de trabalho primeiro** – SmartMarker atua sobre um objeto `Worksheet` já existente; a pasta de trabalho fornece o contêiner para todas as operações subsequentes.

## Etapa 2: Definir os dados JSON e configurar o SmartMarker

Usaremos um payload JSON pequeno que lista duas pessoas. A opção `ArrayAsSingle` indica ao SmartMarker que trate todo o array como um único registro lógico, ideal quando você deseja uma tabela simples sem loops aninhados.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Dica:** Se você omitir `ArrayAsSingle`, o SmartMarker tentará criar um registro separado para cada elemento do array, o que pode gerar linhas duplicadas ou layout inesperado.

## Etapa 3: Inserir tags SmartMarker na planilha

Tags SmartMarker são marcadores de texto simples cercados por `&`. Coloque‑as nas células onde você quer que os valores JSON apareçam. Neste exemplo escrevemos as tags diretamente via código, mas você também poderia projetar um modelo no Excel primeiro.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Explicação:** `&=Name&` indica ao SmartMarker que substitua a célula pelo campo `Name` do objeto JSON, enquanto `&=Age&` faz o mesmo para `Age`.

## Etapa 4: Processar a planilha – preencher o Excel a partir do JSON

Agora deixe o SmartMarker ler a string JSON e preencher os marcadores.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

Nos bastidores, o SmartMarker analisa `jsonData`, mapeia cada propriedade do objeto para a tag correspondente e expande as linhas automaticamente porque `ArrayAsSingle` está `true`. Após o processamento, a planilha fica assim:

| Nome | Idade |
|------|-------|
| John | 30    |
| Anna | 25    |

## Etapa 5: Salvar o arquivo XLSX

Por fim, grave a pasta de trabalho preenchida no disco.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Executar o programa cria `SmartMarkerJson.xlsx` na sua área de trabalho. Abrir o arquivo no Excel mostra uma tabela limpa com os dados JSON importados corretamente.

## Armadilhas comuns ao importar JSON para a planilha

| Problema | Por que acontece | Como evitar |
|----------|------------------|--------------|
| **Tags SmartMarker ausentes** | O SmartMarker só substitui células que contêm `&=...&`. | Verifique a ortografia exata e a capitalização das tags. |
| **Formato JSON incorreto** | Aspas simples (`'`) não são JSON válido para o analisador interno. | Use aspas duplas (`"`) ou deixe o Aspose.Cells lidar com o formato flexível conforme mostrado. |
| **Array tratado como múltiplos registros** | O padrão `ArrayAsSingle` é `false`. | Defina `processor.Options.ArrayAsSingle = true` quando quiser uma tabela plana. |
| **Salvando em uma pasta somente leitura** | `workbook.Save` lança uma exceção. | Escolha um diretório gravável (por exemplo, Desktop ou uma pasta temporária). |

## Expandindo a solução

- **Múltiplas planilhas:** Crie folhas adicionais e chame `processor.Process` em cada uma com fontes JSON diferentes.  
- **Estilização:** Após o processamento, aplique estilos de célula (fontes, bordas) como em qualquer operação regular do Aspose.Cells.  
- **Conjuntos de dados grandes:** Para milhares de linhas, considere fazer streaming da pasta de trabalho para reduzir o uso de memória (`WorkbookDesigner` ou `SaveOptions` com `EnableMemoryOptimization`).  

## Conclusão

Agora você sabe como **converter JSON para XLSX em C#** usando Aspose.Cells SmartMarker. O fluxo completo — **criar pasta de trabalho Excel C#**, adicionar tags SmartMarker, configurar o processador, **preencher o Excel a partir do JSON** e salvar o arquivo — permite **importar JSON para células da planilha** com código mínimo.  

Sinta‑se à vontade para experimentar estruturas JSON mais complexas, adicionar fórmulas ou gerar gráficos diretamente a partir dos dados preenchidos. Se você gostou deste guia, experimente o próximo tutorial sobre **como importar JSON para o Excel** para criação de gráficos ou sobre **criar pasta de trabalho Excel C#** com formatação avançada.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Convert JSON to Excel with C# – Step‑by‑Step Guide](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [How to Insert JSON into Excel Template – Step‑by‑Step](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}