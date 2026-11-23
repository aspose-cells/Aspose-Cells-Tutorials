---
category: general
date: 2026-11-22
description: Aprenda a criar planilhas Excel a partir de dados JSON em C# usando Aspose.Cells
  Smart Marker. Guia passo a passo cobre o design do modelo, o tratamento de JSON
  e a exportação de arquivos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: pt
lastmod: 2026-11-22
og_description: Crie um Excel a partir de dados JSON usando o Aspose.Cells Smart Marker.
  Siga este tutorial conciso para gerar uma pasta de trabalho totalmente formatada
  a partir de um array JSON.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Criar Excel a partir de dados JSON em C# – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar Excel a partir de dados JSON com Aspose.Cells e Smart Marker
url: /pt/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar Excel a partir de dados JSON com Aspose.Cells e Smart Marker

Se você precisa **criar Excel a partir de dados JSON** em uma aplicação .NET, este tutorial mostra uma solução completa, pronta para produção. Você verá como incorporar um array JSON em uma única célula, usar o recurso **Smart Marker** do **Aspose.Cells**, e gerar uma planilha final sem codificação manual célula por célula.

A abordagem funciona para qualquer payload JSON — seja exportando resultados de API, serializando objetos ou criando relatórios. Ao final do guia você terá um projeto C# pronto‑para‑executar que lê uma string JSON, aplica-a a um **modelo Excel**, e salva o resultado como um novo arquivo.

## Pré-requisitos

- .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.6+)
- Visual Studio 2022 (ou qualquer IDE que suporte C#)
- Pacote NuGet **Aspose.Cells for .NET** (versão 23.10 ou mais recente)
- Um arquivo de modelo Excel simples que contém a tag Smart Marker `<%=Fruits:ArrayAsSingle%>` na célula de destino

> **Dica profissional:** Mantenha o modelo em uma pasta que sua aplicação possa acessar em tempo de execução (por exemplo, `Resources` ou um caminho configurável).  

## Etapa 1: Preparar o payload JSON

Primeiro, defina o array JSON que você deseja inserir na planilha. Neste exemplo usamos uma lista de nomes de frutas.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

A string JSON pode ser gerada dinamicamente (por exemplo, `JsonSerializer.Serialize(myList)`) ou lida de uma fonte externa como uma API REST. O ponto chave é que a string deve ser um array JSON válido porque **Smart Marker** espera uma representação JSON ao usar a opção `ArrayAsSingle`.

## Etapa 2: Construir a fonte de dados Smart Marker

O mecanismo Smart Marker do Aspose.Cells funciona com qualquer objeto .NET. Criamos um objeto anônimo que contém a string JSON em uma propriedade chamada `Fruits`. O nome da propriedade deve corresponder ao nome do marcador usado no modelo.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Por que um objeto anônimo?** Ele permite passar um contêiner de dados leve sem definir uma classe dedicada, o que acelera a prototipagem. Para projetos maiores você pode substituí‑lo por um DTO fortemente tipado.

## Etapa 3: Projetar o modelo Excel com um placeholder Smart Marker

Crie um arquivo Excel (`SmartMarkerTemplate.xlsx`) que contenha o placeholder onde o JSON aparecerá. Coloque o marcador a seguir na célula desejada (por exemplo, **A1**):

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – corresponde ao nome da propriedade na fonte de dados.
- `ArrayAsSingle` – indica ao Smart Marker que escreva todo o array JSON como uma única string, preservando colchetes e aspas.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Modelo Excel contendo <%=Fruits:ArrayAsSingle%> para criar Excel a partir de dados JSON"}

## Etapa 4: Carregar a workbook e inicializar o processador Smart Marker

Agora carregue o arquivo de modelo em uma instância `Aspose.Cells.Workbook` e crie um `SmartMarkerProcessor` que cuidará da substituição.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Carregar a workbook uma única vez e reutilizar a mesma instância `SmartMarkerProcessor` é mais eficiente do que criar um novo processador para cada célula.

## Etapa 5: Aplicar a fonte de dados para substituir o marcador

O método `ApplyTemplate` varre a workbook em busca de todos os marcadores e os substitui pelos valores do objeto fornecido.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Como usamos `ArrayAsSingle`, a célula agora contém a string JSON bruta:

```
["Apple","Banana","Cherry"]
```

Se precisar de um formato diferente (por exemplo, uma lista separada por vírgulas), você pode usar `ArrayAsCommaSeparated` em vez de `ArrayAsSingle`.

## Etapa 6: Salvar a workbook processada

Finalmente, escreva a workbook modificada em um novo arquivo. Você pode escolher qualquer formato suportado (`.xlsx`, `.xls`, `.csv`, etc.).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

O arquivo resultante `JsonExported.xlsx` pode ser aberto no Excel, Google Sheets ou qualquer visualizador compatível, e exibirá o array JSON exatamente como inserido.

## Exemplo completo em funcionamento

Juntando todas as peças, você obtém um programa de console autônomo:

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Saída esperada

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

O JSON aparece exatamente como uma string na célula **A1** do `JsonExported.xlsx`.

## Lidando com variações comuns e casos de borda

| Situação                                 | Ajuste recomendado |
|-------------------------------------------|--------------------|
| **Large JSON objects** (nested dictionaries) | Use `ArrayAsJson` para incorporar toda a hierarquia de objetos, ou mapeie o JSON para um modelo fortemente tipado e use marcadores aninhados (`<%=Parent.Child%>`). |
| **Multiple JSON arrays** in different cells | Adicione propriedades adicionais ao objeto anônimo (por exemplo, `Vegetables = vegJson`) e marcadores correspondentes (`<%=Vegetables:ArrayAsSingle%>`). |
| **Need to split the array into rows** | Substitua `ArrayAsSingle` por `Array` – o Smart Marker criará uma nova linha para cada elemento. |
| **Template stored as an embedded resource** | Carregue a workbook a partir de um stream: `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Running in ASP.NET Core** | Use `IWebHostEnvironment.ContentRootPath` para construir o caminho completo até o modelo e os arquivos de saída. |

## Considerações de desempenho

- **Reutilize o objeto `Workbook`** ao processar muitos registros em lote; crie o processador uma vez por workbook.
- **Desative o cálculo** (`workbook.CalculateFormula = false`) se o modelo contiver fórmulas pesadas que não são necessárias na etapa de inserção do JSON.
- **Salvamento em stream** (`workbook.Save(stream, SaveFormat.Xlsx)`) reduz a sobrecarga de I/O ao enviar o arquivo diretamente na resposta ao cliente.

## Conclusão

Agora você sabe como **criar Excel a partir de dados JSON** em C# usando **Aspose.Cells** e o recurso **Smart Marker**. O tutorial abordou a preparação do JSON, criação da fonte de dados, design do modelo, processamento do marcador e salvamento do arquivo — tudo dentro de um único programa executável.

Daqui você pode:

- Estender o modelo com tags **Smart Marker** adicionais para relatórios mais ricos.
- Trocar para `Array` ou `ArrayAsJson` para gerar JSON como linhas ou estruturas aninhadas.
- Combinar esta técnica com bibliotecas de geração de Excel em **C#** como EPPlus ou ClosedXML se precisar de uma alternativa gratuita.

Boa codificação, e aproveite transformar JSON em planilhas Excel bem elaboradas!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Importar Dados JSON para Excel usando Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Tutorial Aspose Cells GridJs – Exportar dados Excel para JSON com carregamento preguiçoso](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Criar Excel a partir de JSON com Smart Marker do Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}