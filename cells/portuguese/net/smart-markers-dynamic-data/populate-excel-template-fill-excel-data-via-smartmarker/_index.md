---
category: general
date: 2026-05-30
description: Preencha rapidamente um modelo Excel e aprenda como preencher o Excel
  com dados usando o Aspose.Cells SmartMarker. Guia completo em C# com código executável.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: pt
og_description: Preencha o modelo do Excel e complete a planilha com dados usando
  Aspose.Cells SmartMarker. Siga este tutorial passo a passo em C# para obter resultados
  instantâneos.
og_title: Preencher Modelo Excel – Preencher Dados do Excel via SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Preencher Modelo Excel – Inserir Dados no Excel via SmartMarker
url: /pt/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preencher Modelo Excel – Preencher Dados do Excel via SmartMarker

Já precisou **preencher modelo Excel** mas não sabia como automatizar o processo? Neste tutorial vamos mostrar como **preencher Excel com dados** usando Aspose.Cells SmartMarker — uma ferramenta que transforma uma pasta de trabalho estática em um gerador de relatórios dinâmico.

Imagine que você tem uma planilha de fatura pré‑designada, um painel de vendas ou qualquer formulário repetível. Em vez de digitar valores manualmente, você pode fornecer um objeto C# e deixar o SmartMarker fazer o trabalho pesado. Ao final deste guia você terá um projeto totalmente executável que recebe um modelo, insere linhas, totais e até formatação condicional — tudo sem tocar na interface do usuário.

## O que você aprenderá

- Como preparar uma fonte de dados que corresponda às tags no seu modelo Excel.  
- Como instanciar **SmartMarkerProcessor** e habilitar o suporte a intervalos.  
- Como **preencher modelo Excel** com coleções aninhadas, como itens de pedido.  
- Dicas para lidar com casos de borda, como coleções vazias ou formatos numéricos personalizados.  

Nenhum serviço externo, sem macros VBA — apenas C# puro e Aspose.Cells. Tudo que você precisa é .NET 6 (ou superior) e o pacote NuGet Aspose.Cells.

## Pré-requisitos

- Visual Studio 2022 (ou qualquer IDE de sua preferência).  
- .NET 6 SDK instalado.  
- Aspose.Cells para .NET (você pode obter uma avaliação gratuita no site da Aspose).  
- Um modelo básico de Excel com tags SmartMarker (criaremos um em breve).

Se algum desses itens lhe for desconhecido, não entre em pânico; os passos abaixo orientam você em cada requisito.

## Etapa 1: Projetar o Modelo Excel com Tags SmartMarker

Primeiro, abra uma nova pasta de trabalho e disponha as partes estáticas — logotipo da empresa, cabeçalhos, etc. Em seguida, insira marcadores de posição SmartMarker onde os dados dinâmicos devem aparecer.

| Célula | Conteúdo |
|--------|----------|
| A1     | **Fatura** |
| A3     | `{{CompanyName}}` |
| A5     | **Detalhes do Pedido** |
| A7     | `{{Orders.Items.Name}}` |
| B7     | `{{Orders.Items.Qty}}` |
| C7     | `{{Orders.Items.Price}}` |
| D7     | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Por que isso importa:** O SmartMarker lê as chaves duplas e as mapeia para propriedades no objeto que você passará depois. A coleção `Orders.Items` indica ao motor que ele deve repetir a linha para cada item da lista.

> **Dica profissional:** Use a opção `RangeSmartMarker` (ativaremos mais adiante) quando precisar que o motor expanda o intervalo automaticamente — perfeito para tabelas que crescem ou diminuem.

Salve o arquivo como `InvoiceTemplate.xlsx` na pasta `Resources` do seu projeto.

## Etapa 2: Preparar a Fonte de Dados que Correspondem às Tags do Modelo

Agora criamos um objeto anônimo C# (ou uma classe fortemente tipada) cujos nomes de propriedades estejam alinhados com as tags. O segredo é espelhar a hierarquia exatamente.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Por que isso importa:** O array `Orders` contém um único pedido, e cada pedido tem um array `Items`. O SmartMarker iterará sobre `Items`, clonando a linha para cada elemento. Se mais tarde precisar de vários pedidos, basta adicionar mais objetos ao array `Orders` — sem alterações no código.

## Etapa 3: Carregar o Modelo e Criar uma Instância de SmartMarkerProcessor

Com os dados prontos, carregamos a pasta de trabalho, criamos o processador e instruímos que ele respeite as tags de intervalo.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Por que isso importa:** `SmartMarkerProcessor` é o motor que analisa as tags, expande intervalos e grava valores. Ao separar o processador da pasta de trabalho, você mantém o código limpo e reutilizável.

## Etapa 4: Processar a Planilha com RangeSmartMarker Habilitado

A mágica acontece quando chamamos `Process`. Definir `RangeSmartMarker = true` indica ao SmartMarker que trate todo o intervalo de linhas como um bloco repetível, inserindo ou excluindo linhas automaticamente conforme necessário.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

Neste ponto o motor:

1. Escaneou a planilha em busca de tags `{{...}}`.  
2. Mapeou cada tag para uma propriedade em `data`.  
3. Detectou o intervalo da tabela (A7:D7) e duplicou-o três vezes — uma vez por item.  
4. Calculou a expressão `Price * Qty` para a coluna de total.

## Etapa 5: Salvar a Pasta de Trabalho Resultante

Finalmente, grave a pasta de trabalho preenchida no disco (ou envie-a como stream para um cliente web).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Abra `InvoicePopulated.xlsx` e você verá uma tabela preenchida ordenadamente:

| Nome      | Quantidade | Preço | Total |
|-----------|------------|-------|-------|
| Pen       | 2          | 1.5   | 3.00 |
| Notebook  | 1          | 3.75  | 3.75 |
| Stapler   | 1          | 5.00  | 5.00 |

A etapa de **preencher modelo Excel** está concluída, e você preencheu **Excel com dados** com sucesso para qualquer número de linhas.

## Tratando Casos de Borda Comuns

### Coleções Vazias

Se `Items` estiver vazio, o SmartMarker deixará o cabeçalho da tabela intacto, mas não inserirá linhas. Para evitar um espaço em branco, você pode adicionar um bloco condicional:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Formatos Numéricos Personalizados

Às vezes você precisa de símbolos de moeda ou separadores de milhar. Após o processamento, você pode aplicar um estilo programaticamente:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Conjuntos de Dados Grandes

Para milhares de linhas, habilite a opção `UseFastMode` para melhorar o desempenho:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Exemplo Completo Funcionando

Abaixo está o programa completo e autocontido que você pode copiar‑colar em um aplicativo de console. Ele inclui todas as diretivas `using`, preparação de dados, processamento e salvamento.



## O que Você Deve Aprender a Seguir?

- [Preencher Excel com Dados Usando Aspose.Cells e Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Como Preencher Células do Excel com Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automatizar Exportação de Dados do Excel Usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}