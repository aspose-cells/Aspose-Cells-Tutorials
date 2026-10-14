---
category: general
date: 2026-02-14
description: Crie um objeto de dados mestre em C# e gere a planilha de detalhes sem
  esforço. Aprenda todo o fluxo de trabalho do SmartMarker com exemplos de código
  práticos.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: pt
og_description: Crie um objeto de dados mestre em C# e gere a planilha de detalhes
  com SmartMarker. Siga nosso tutorial detalhado para uma solução pronta‑para‑usar.
og_title: Criar Objeto de Dados Mestres – Guia Completo
tags:
- C#
- SmartMarker
- Excel Automation
title: Criar Objeto de Dados Mestre – Guia passo a passo para gerar a ficha de detalhes
url: /pt/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Objeto de Dados Mestre – Tutorial Completo

Já precisou **criar objeto de dados mestre** para uma planilha Excel, mas não sabia como vinculá‑lo a uma planilha de detalhes SmartMarker? Você não está sozinho. Em muitos cenários de relatórios o objeto mestre controla uma planilha de detalhes dinâmica, e acertar a conexão pode parecer montar um quebra‑cabeça sem a imagem.

Neste guia vamos percorrer todo o processo — construir o objeto de dados mestre, configurar as opções do SmartMarker para **gerar planilha de detalhes**, e finalmente disparar o processador. Ao final você terá um trecho de código executável que pode colar em qualquer projeto .NET que use a biblioteca GrapeCity Documents for Excel (GcExcel).

## O que você vai precisar

- .NET 6+ (ou .NET Framework 4.7.2) com referência a `GcExcel.dll`
- Familiaridade básica com C# (variáveis, tipos anônimos, inicializadores de objetos)
- Uma pasta de trabalho Excel que já contenha tags SmartMarker como `{{OrderId}}` e uma tabela para itens de linha
- Visual Studio, Rider ou qualquer editor de sua preferência

É só isso — nenhum pacote NuGet extra além da distribuição principal do GcExcel.

## Etapa 1: Criar o Objeto de Dados Mestre

A primeira coisa que você deve fazer é **criar objeto de dados mestre** que reflita a estrutura esperada pelas tags SmartMarker. Pense nele como um pequeno modelo de relatório em memória.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Por que usar um tipo anônimo aqui? Porque ele permite definir um contêiner leve sem declarar uma classe completa — perfeito para demonstrações rápidas ou quando a forma provavelmente não mudará. Se precisar de um modelo reutilizável depois, basta substituir `var` por um POCO adequado.

> **Dica profissional:** Mantenha os nomes das propriedades (`OrderId`, `Product`, `Quantity`) idênticos aos marcadores de posição na sua planilha; o SmartMarker faz a correspondência sem diferenciar maiúsculas de minúsculas.

## Etapa 2: Configurar as Opções do SmartMarker para Gerar uma Planilha de Detalhes

Agora informamos ao SmartMarker que queremos uma planilha separada para a tabela de itens de linha. É aqui que a palavra‑chave **generate detail sheet** entra em ação.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

O padrão `DetailSheetNewName` usa marcadores de posição entre chaves que são substituídos em tempo de execução. No nosso exemplo a planilha será chamada `Order_1`. Se você iterar sobre vários pedidos, cada um receberá sua própria aba — exatamente o que a maioria dos contadores espera.

## Etapa 3: Executar o Processador SmartMarker

Com os dados e as opções prontos, o passo final é invocar o processador na planilha de destino.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Nos bastidores, o SmartMarker varre a planilha em busca de tags, injeta os valores de `orderData` e, como `DetailSheet` está `true`, clona o modelo em uma nova planilha chamada `Order_1`. Todos os itens de linha aparecem na área de detalhes, preservando qualquer formatação que você tenha aplicado no modelo.

### Exemplo Completo Funcional

A seguir, um programa console autocontido que abre uma pasta de trabalho modelo (`Template.xlsx`), executa as três etapas e salva o resultado como `Result.xlsx`. Basta copiar‑colar isso em um novo projeto console e pressionar **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Saída Esperada

- **Result.xlsx** contém uma planilha chamada `Order_1`.
- A célula `A1` (ou onde você colocou `{{OrderId}}`) agora exibe `1`.
- Uma tabela iniciando no bloco SmartMarker lista duas linhas:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Se você abrir o arquivo, verá a formatação do modelo preservada — bordas, fontes, formatação condicional — tudo intacto.

## Perguntas Frequentes & Casos de Borda

### E se eu tiver vários pedidos?

Envolva o objeto mestre em uma coleção e deixe o SmartMarker iterar automaticamente:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Cada pedido gera sua própria planilha (`Order_1`, `Order_2`, …). O processador trata o array externo como a coleção mestre.

### Como controlo a posição da planilha?

Defina `smartMarkerOptions.DetailSheetInsertIndex = 2;` para colocar a nova planilha após a segunda aba, ou use `DetailSheetInsertAfter = "Summary"` para inserir depois de uma planilha nomeada.

### Posso desativar a planilha de detalhes para uma execução específica?

Basta mudar `DetailSheet = false;`. O SmartMarker então escreverá os itens de linha na mesma planilha onde as tags mestre estão.

### E quanto a conjuntos de dados grandes?

O SmartMarker transmite dados de forma eficiente, mas se você ultrapassar algumas centenas de milhares de linhas pode atingir o limite de 1.048.576 linhas do Excel. Nesse caso, divida os dados em vários registros mestres ou considere exportar para CSV.

## Visão Geral Visual

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*A ilustração mostra o fluxo do objeto mestre C# → opções SmartMarker → processamento da planilha → nova planilha de detalhes.*

## Conclusão

Agora você sabe como **criar objeto de dados mestre** em C# e configurar o SmartMarker para **gerar planilha de detalhes** automaticamente. O padrão de três etapas — dados, opções, processador — cobre a maioria dos cenários de automação Excel com GcExcel.

A partir daqui você pode explorar:

- Adicionar dados de cabeçalho/rodapé a cada planilha de detalhes
- Usar formatação condicional baseada no status do pedido
- Exportar a pasta de trabalho gerada para PDF com `workbook.SaveAsPdf(...)`

Sinta‑se à vontade para experimentar, quebrar coisas e depois juntá‑las novamente. Essa é a maneira mais rápida de dominar a automação de planilhas. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}