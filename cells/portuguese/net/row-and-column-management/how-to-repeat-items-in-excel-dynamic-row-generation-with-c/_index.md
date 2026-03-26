---
category: general
date: 2026-03-25
description: Aprenda a repetir itens no Excel usando C#. Este guia mostra como gerar
  linhas do Excel dinamicamente e preencher um modelo de Excel em C# para qualquer
  coleção.
draft: false
keywords:
- how to repeat items in excel
- generate excel rows dynamically
- populate excel template c#
language: pt
og_description: Como repetir itens no Excel com C#? Siga este tutorial completo para
  gerar linhas do Excel dinamicamente e preencher um modelo de Excel em C# sem esforço.
og_title: Como Repetir Itens no Excel – Guia C# Passo a Passo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Como Repetir Itens no Excel – Geração Dinâmica de Linhas com C#
url: /pt/net/row-and-column-management/how-to-repeat-items-in-excel-dynamic-row-generation-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Repetir Itens no Excel – Geração Dinâmica de Linhas com C#

Já se perguntou **como repetir itens no Excel** sem copiar linhas manualmente? Talvez você tenha uma lista de pedidos, cada um com vários itens, e precise de uma planilha organizada que se expanda automaticamente. Neste tutorial você verá exatamente isso: vamos gerar linhas do Excel dinamicamente e **preencher um modelo Excel C#** usando o poderoso recurso Smart Marker do Aspose.Cells.

Percorreremos um cenário do mundo real, construiremos um pequeno modelo de dados e veremos a biblioteca transformar nosso modelo em uma planilha totalmente preenchida. Ao final, você será capaz de repetir itens no Excel para qualquer coleção, seja um único pedido ou um catálogo enorme. Sem enrolação — apenas uma solução funcional que você pode copiar e colar no seu projeto.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+)
- Visual Studio 2022 (ou qualquer IDE de sua preferência)
- **Aspose.Cells for .NET** pacote NuGet (`Install-Package Aspose.Cells`)
- Um entendimento básico de tipos anônimos em C#

Se estiver faltando algum desses itens, basta adicionar o pacote NuGet e você está pronto para começar. A biblioteca é totalmente gerenciada, portanto não há necessidade de interop COM ou instalação do Office.

---

## Etapa 1: Definir um Modelo Smart Marker – o Núcleo de “repetir itens no Excel”

A primeira coisa que precisamos é de uma célula modelo que indique ao Aspose.Cells como iterar sobre nossa coleção. Smart Markers usam uma sintaxe de placeholder simples que vive diretamente dentro da planilha.

```csharp
// Put the template into cell A1
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +          // Start repeating the Orders collection
    "   ${Item:Repeat}\n" +        // For each Order, repeat the Item collection
    "      ${Item.Name}\n" +       // Insert the Name of each Item
    "   ${/Item}\n" +              // End Item repeat block
    "${/Orders}");                 // End Orders repeat block
```

**Por que isso importa:** O marcador `${Orders:Repeat}` indica ao processador para percorrer o array `Orders`. Dentro desse loop iniciamos outro bloco de repetição para `Item`. Cada vez que o loop interno executa, `${Item.Name}` é substituído pelo nome real, como “Apple” ou “Banana”. Quando o processador termina, o modelo se expande em tantas linhas quantas forem necessárias — exatamente o que você precisa para **gerar linhas do Excel dinamicamente**.

> **Dica profissional:** Mantenha a identação dentro da string; ela se traduz em alinhamento correto das linhas na planilha final.

## Etapa 2: Construir um Modelo de Dados Correspondente – “populate excel template c#” Simplificado

Nosso modelo espera um objeto com a propriedade `Orders`, cada pedido contendo um array `Item`. Criaremos um objeto anônimo que reflita essa estrutura:

```csharp
// Create a simple data model that matches the template
var dataModel = new
{
    Orders = new[]
    {
        new
        {
            Item = new[]
            {
                new { Name = "Apple" },
                new { Name = "Banana" }
            }
        },
        // You can add more orders here – the template will repeat automatically
        new
        {
            Item = new[]
            {
                new { Name = "Orange" },
                new { Name = "Grape" },
                new { Name = "Mango" }
            }
        }
    }
};
```

**Por que isso importa:** A estrutura do objeto anônimo deve coincidir exatamente com os marcadores. Se você esquecer uma propriedade ou nomeá‑la de forma diferente, o motor Smart Marker a ignorará silenciosamente, deixando linhas vazias. Essa é uma armadilha comum ao tentar **populate excel template c#** pela primeira vez.

## Etapa 3: Executar o Processador Smart Marker – O Motor que Repete Itens

Agora que temos um modelo e um modelo de dados, entregamos ambos ao Aspose.Cells. O processador percorre a planilha, expande os blocos de repetição e grava os valores.

```csharp
// Process the template with the data model
worksheet.SmartMarkerProcessor.Process(dataModel);
```

Isso é literalmente todo o código que você precisa para **repetir itens no Excel**. Após a chamada terminar, a planilha conterá:

| A (gerado) |
|------------|
| Apple      |
| Banana     |
| Orange     |
| Grape      |
| Mango      |

Cada item aparece em sua própria linha, independentemente de quantos pedidos ou itens você adicionou ao modelo.

## Exemplo Completo – Do Início ao Fim

Abaixo está um aplicativo console completo, pronto‑para‑executar, que demonstra todo o fluxo. Copie para um novo projeto C#, adicione o pacote NuGet Aspose.Cells e execute. Um arquivo `Output.xlsx` aparecerá no diretório *bin*.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // 2️⃣ Define the Smart Marker template (Step 1)
            worksheet.Cells["A1"].PutValue(
                "${Orders:Repeat}\n" +
                "   ${Item:Repeat}\n" +
                "      ${Item.Name}\n" +
                "   ${/Item}\n" +
                "${/Orders}");

            // 3️⃣ Build the data model (Step 2)
            var dataModel = new
            {
                Orders = new[]
                {
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Apple" },
                            new { Name = "Banana" }
                        }
                    },
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Orange" },
                            new { Name = "Grape" },
                            new { Name = "Mango" }
                        }
                    }
                }
            };

            // 4️⃣ Process the template (Step 3)
            worksheet.SmartMarkerProcessor.Process(dataModel);

            // 5️⃣ Save the result
            workbook.Save("Output.xlsx");
            Console.WriteLine("Excel file generated! Open Output.xlsx to see the repeated items.");
        }
    }
}
```

**Saída esperada:** Abra `Output.xlsx` e você verá uma coluna com os cinco nomes de frutas, cada um ocupando sua própria linha. Nenhuma cópia manual necessária.

### E se a Minha Coleção estiver Vazia?

Se `Orders` ou qualquer array `Item` estiver vazio, o motor Smart Marker simplesmente ignora o bloco, não gerando linhas. Isso é útil quando você precisa **gerar linhas do Excel dinamicamente** com base em dados opcionais — nada extra aparecerá.

### Manipulando Conjuntos de Dados Grandes

Para milhares de linhas, o processador continua rápido porque trabalha na memória e grava diretamente no workbook. Contudo, você pode querer:

- Desativar o cálculo (`workbook.CalculateFormula = false`) antes do processamento.
- Usar `MemoryStream` se precisar devolver o arquivo via API web sem tocar no sistema de arquivos.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| Marcadores não se expandem | Nome da propriedade escrito errado ou com caixa diferente | Garanta que os nomes das propriedades do objeto anônimo correspondam exatamente aos marcadores (`Orders`, `Item`, `Name`). |
| Linhas em branco aparecem | Caracteres de nova linha extras dentro da string do modelo | Remova `\n` finais ou mantenha o modelo conciso. |
| Processador lança `NullReferenceException` | Modelo de dados contém `null` em uma coleção | Proteja contra `null` inicializando arrays vazios (`new object[0]`). |
| Arquivo de saída corrompido | Workbook não salvo corretamente (ex.: usando formato errado) | Use `workbook.Save("file.xlsx")` com a extensão `.xlsx`. |

## Estendendo o Modelo – Mais que Apenas Nomes

Smart Markers suportam qualquer propriedade, fórmulas e até blocos condicionais. Por exemplo, para adicionar uma coluna de preço:

```csharp
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +
    "   ${Item:Repeat}\n" +
    "      ${Item.Name}\t${Item.Price}\n" +
    "   ${/Item}\n" +
    "${/Orders}");
```

E atualizar o modelo de dados:

```csharp
new { Name = "Apple", Price = 0.99M },
new { Name = "Banana", Price = 0.59M }
```

O resultado será duas colunas — uma para o nome, outra para o preço — novamente geradas **dinamicamente**.

## Conclusão

Agora você tem uma solução completa e autônoma para **como repetir itens no Excel** usando C#. Ao definir um modelo Smart Marker, espelhá‑lo com um modelo de dados correspondente e invocar `SmartMarkerProcessor.Process`, você pode **gerar linhas do Excel dinamicamente** para qualquer coleção e preencher projetos **populate excel template c#** sem esforço.

Qual o próximo passo? Experimente adicionar totais, formatação condicional ou exportar os mesmos dados para CSV. O mesmo padrão funciona com coleções aninhadas, agrupamentos e até objetos personalizados — então sinta‑se à vontade para experimentar.

Se este guia foi útil, dê uma estrela no GitHub, compartilhe com a equipe ou deixe um comentário abaixo. Boa codificação e aproveite o poder da geração automática de Excel!

![Screenshot of generated Excel rows showing how to repeat items in Excel](/images/repeat-items-excel.png "how to repeat items in Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}