---
category: general
date: 2026-02-28
description: Crie um relatório mestre‑detalhe em C# e aprenda a preencher um modelo
  do Excel, mesclar dados no Excel e carregar a pasta de trabalho do Excel em C# em
  apenas alguns passos.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: pt
og_description: Crie relatório mestre‑detalhe em C# usando Aspose.Cells SmartMarker.
  Aprenda a carregar uma pasta de trabalho Excel em C#, mesclar dados no Excel e preencher
  um modelo Excel.
og_title: Criar relatório mestre‑detalhe em C# – Preencher modelo do Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Criar relatório mestre‑detalhe em C# – Preencher modelo Excel com SmartMarker
url: /pt/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar relatório mestre‑detalhe em C# – Preencher modelo Excel com SmartMarker

Já precisou **criar relatório mestre‑detalhe** em C# mas não sabia como colocar os dados em um arquivo Excel? Você não está sozinho. Neste guia, percorreremos os passos exatos para **preencher modelo Excel**, **mesclar dados no Excel**, e **carregar pasta de trabalho Excel em C#**‑style para que você obtenha um relatório mestre‑detalhe polido pronto para distribuição.

Usaremos Aspose.Cells SmartMarker, um mecanismo poderoso que entende relacionamentos mestre‑detalhe pronto para uso. Ao final do tutorial, você terá um exemplo completo e executável que pode inserir em qualquer projeto .NET. Sem atalhos vagos como “ver a documentação” — apenas uma solução autônoma que você pode copiar‑colar e executar.

## O que você aprenderá

- Como **criar master detail** estruturas de dados em C# que mapeiam diretamente para um modelo Excel.
- A forma exata de **carregar pasta de trabalho Excel C#** código que abre um arquivo `.xlsx` contendo tags SmartMarker.
- O processo de **preencher modelo Excel** executando `SmartMarkerProcessor`.
- Dicas para lidar com casos extremos, como tags ausentes ou conjuntos de dados grandes.
- Como verificar o resultado e como o **relatório mestre‑detalhe** final se parece.

### Pré-requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.8).
- Aspose.Cells para .NET (você pode obter o pacote de teste gratuito via NuGet: `Install-Package Aspose.Cells`).
- Um arquivo Excel básico (`template.xlsx`) que contém tags SmartMarker (mostraremos a marcação mínima necessária).

Se você já tem tudo pronto, vamos mergulhar.

## Etapa 1 – Criar a fonte de dados mestre‑detalhe *(como criar master detail)*

A primeira coisa que você precisa é um objeto C# que representa as linhas mestre (pedidos) e suas linhas filhas (itens do pedido). SmartMarker lerá essa hierarquia automaticamente quando `MasterDetail` estiver definido como `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Por que isso importa:**  
SmartMarker procura uma propriedade chamada `Orders` (o mestre) e, para cada pedido, busca uma coleção chamada `Items`. Ao combinar esses nomes, você obtém automaticamente um **relatório mestre‑detalhe** sem precisar escrever loops.

> **Dica profissional:** Mantenha os nomes das propriedades curtos e significativos; eles se tornam os marcadores de posição no seu modelo Excel.

## Etapa 2 – Configurar opções do SmartMarker para processamento mestre‑detalhe

Informe ao mecanismo que você está lidando com um cenário mestre‑detalhe e forneça o nome da planilha de detalhe que receberá as linhas filhas.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Por que isso importa:**  
Se você omitir `MasterDetail = true`, o SmartMarker tratará os dados como uma lista plana e as linhas de detalhe nunca aparecerão. O `DetailSheetName` deve corresponder ao nome da planilha que você criou no modelo (sensível a maiúsculas/minúsculas).

## Etapa 3 – Carregar a pasta de trabalho Excel no estilo C#

Agora abrimos o modelo que contém as tags SmartMarker. Esta é a etapa de **carregar pasta de trabalho Excel C#** que muitos desenvolvedores tropeçam porque esquecem de usar o caminho de arquivo correto ou de descartar a pasta de trabalho adequadamente.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Por que isso importa:**  
Aspose.Cells lê toda a pasta de trabalho na memória, portanto o arquivo pode estar no disco, incorporado como recurso ou até mesmo transmitido de um serviço web. Apenas certifique‑se de que o caminho aponte para um arquivo `.xlsx` válido que contenha as tags que discutiremos a seguir.

## Etapa 4 – Inserir tags SmartMarker no modelo (preencher modelo Excel)

Se você abrir `template.xlsx` agora, verá duas planilhas:

- **Orders** – a planilha mestre com uma linha como `&=Orders.Id`.
- **OrderDetail** – a planilha de detalhe com linhas como `&=Items.Sku` e `&=Items.Qty`.

Aqui está uma visualização mínima da marcação:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Você não precisa escrever nenhum código para as tags — elas vivem no arquivo Excel. A etapa de **preencher modelo Excel** consiste simplesmente em chamar o processador:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Por que isso importa:**  
O processador analisa cada planilha, substitui os marcadores `&=` pelos valores reais e expande linhas para cada registro mestre e detalhe. Como `MasterDetail` está ativado, ele cria automaticamente uma nova linha para cada item sob o pedido correspondente.

## Etapa 5 – Salvar o relatório mestre‑detalhe

Finalmente, grave a pasta de trabalho preenchida no disco. Este é o momento em que você obtém um **relatório mestre‑detalhe** pronto para ser compartilhado.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Saída esperada:**  

- A planilha **Orders** mostra duas linhas: `1` e `2` (IDs dos pedidos).  
- A planilha **OrderDetail** mostra três linhas:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Esse é um **criar relatório mestre‑detalhe** totalmente funcional que você pode enviar por e‑mail, imprimir ou alimentar em outro sistema.

## Casos extremos & perguntas comuns

### E se o modelo estiver sem uma tag?

SmartMarker ignora silenciosamente tags desconhecidas, mas você acabará com células vazias. Verifique a ortografia da tag e assegure que os nomes das propriedades no seu objeto C# correspondam exatamente.

### Como ele lida com grandes conjuntos de dados?

O processador transmite linhas, então mesmo milhares de registros de detalhe não estourarão a memória. Contudo, para arquivos extremamente grandes, você pode querer aumentar o `MemorySetting` em `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Posso usar um nome de planilha diferente para o mestre?

Sim — basta renomear a planilha no modelo e ajustar o `DetailSheetName` se você tiver uma planilha de detalhe. O nome da planilha mestre é inferido a partir do marcador (`&=Orders.Id`).

### E se eu precisar adicionar uma linha de totais?

Adicione uma fórmula Excel regular no modelo (por exemplo, `=SUM(B2:B{#})`). SmartMarker preservará a fórmula após a inserção dos dados.

## Exemplo completo executável

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele inclui todas as diretivas `using`, o modelo de dados, opções e manipulação de arquivos.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Execute o programa, abra `output.xlsx` e você verá os dados mestre‑detalhe belamente preenchidos.

## Referência visual

![Captura de tela da saída do relatório mestre‑detalhe](https://example.com/images/master-detail-report.png "Exemplo de relatório mestre‑detalhe")

*A imagem mostra a planilha Orders com IDs 1 e 2, e a planilha OrderDetail com as três linhas SKU‑Qty.*

## Conclusão

Agora você sabe **como criar relatório mestre‑detalhe** em C# usando Aspose.Cells SmartMarker, desde a construção da fonte de dados até **carregar pasta de trabalho Excel C#**, **preencher modelo Excel**, e finalmente

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}