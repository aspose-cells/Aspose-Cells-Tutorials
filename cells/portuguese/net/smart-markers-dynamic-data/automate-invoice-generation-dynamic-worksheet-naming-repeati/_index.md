---
category: general
date: 2026-02-14
description: 'Automatize a geração de faturas com o SmartMarker: aprenda a repetir
  planilhas, nomeá‑las dinamicamente e dominar a nomeação dinâmica de planilhas em
  minutos.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: pt
og_description: Automatize a geração de faturas com o SmartMarker. Este guia mostra
  como repetir planilhas, nomeá‑las dinamicamente e dominar a nomeação dinâmica de
  planilhas.
og_title: Automatize a Geração de Faturas – Nomeação Dinâmica de Planilhas e Repetição
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatizar a Geração de Faturas – Nomeação Dinâmica de Planilhas e Repetição
  em C#
url: /pt/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatizar a Geração de Faturas – Nomeação Dinâmica de Planilhas & Repetição em C#

Já se perguntou como **automatizar a geração de faturas** sem copiar planilhas manualmente para cada pedido? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam de uma planilha separada por fatura, mas também desejam que o nome da planilha reflita o número do pedido. Neste tutorial, resolveremos esse problema usando o `SmartMarkerProcessor` do SmartMarker e mostraremos **como nomear planilhas** dinamicamente, além de abordar **como repetir planilhas** para cada registro. Ao final, você terá um exemplo pronto‑para‑executar em C# que produz uma pasta de trabalho onde cada fatura está em sua própria aba, com nome adequado.

Caminharemos por cada passo—desde a extração de pedidos de uma fonte de dados até a configuração de `SmartMarkerOptions` para nomeação dinâmica de planilhas. Nenhuma documentação externa é necessária; tudo que você precisa está aqui. Um pequeno conhecimento prévio de C# e uma referência à biblioteca Aspose.Cells (ou qualquer engine compatível com SmartMarker) será suficiente.

---

## O que você vai construir

- Recuperar uma coleção de objetos de pedido.
- Configurar o SmartMarker para **repetir uma planilha** para cada pedido.
- Aplicar **nomeação dinâmica de planilhas** usando o placeholder `{OrderId}`.
- Gerar um arquivo Excel onde cada aba é nomeada `Invoice_12345`, `Invoice_67890`, etc.
- Verificar a saída abrindo a pasta de trabalho.

---

## Pré-requisitos

- .NET 6.0 ou superior (o código também compila com .NET 5+).
- Aspose.Cells para .NET (ou qualquer biblioteca que implemente SmartMarker). Instale via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Uma classe `Order` básica (você pode substituí-la pelo seu próprio DTO).

---

## Etapa 1: Configurar o Projeto e o Modelo

Primeiro, crie um novo aplicativo console e defina o modelo de dados que representa um pedido.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Dica profissional:** Mantenha o modelo leve para a demonstração; você pode sempre enriquecê-lo depois com itens de linha, detalhes de impostos, etc.

---

## Etapa 2: Preparar o Modelo Excel

O SmartMarker funciona contra uma pasta de trabalho modelo. Crie um arquivo chamado `InvoiceTemplate.xlsx` com uma única planilha chamada `InvoiceTemplate`. Na célula **A1** coloque um placeholder SmartMarker como:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Você pode formatar as células como quiser—cabeçalhos em negrito, formatação de moeda, etc. Salve o arquivo na pasta raiz do projeto.

> **Por que um modelo?** Ele separa o layout do código, permitindo que designers ajustem a aparência sem tocar na lógica.

---

## Etapa 3: Configurar as Opções do SmartMarker – Repetir & Nomear Planilhas

Agora vamos instruir o SmartMarker a *repetir* a planilha modelo para cada pedido e a dar a cada cópia um nome que inclua o ID do pedido. Este é o núcleo da **nomeação dinâmica de planilhas**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Como funciona

- **`RepeatWorksheet = true`** informa ao motor para duplicar a planilha de origem para cada elemento na coleção `orders`. Isso atende ao requisito de **como repetir planilha**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** é uma string de modelo onde `{OrderId}` é um placeholder que o SmartMarker substitui pelo ID do pedido atual. Essa é a resposta para **como nomear planilhas** e **nomeação dinâmica de planilhas**.
- O processador mescla os campos de cada pedido (`{{OrderId}}`, `{{Customer}}`, etc.) na planilha duplicada, produzindo uma fatura totalmente preenchida.

---

## Etapa 4: Executar a Aplicação e Verificar a Saída

Compile e execute o aplicativo console:

```bash
dotnet run
```

Você deverá ver a mensagem de sucesso no console. Abra `GeneratedInvoices.xlsx` e encontrará três abas:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Cada planilha contém os dados do pedido substituídos nos placeholders. O layout que você projetou no modelo é preservado, comprovando que **automatizar a geração de faturas** funciona de ponta a ponta.

### Captura de tela esperada (texto alternativo para SEO)

![exemplo de automação de geração de faturas mostrando três planilhas nomeadas dinamicamente](/images/invoice-automation.png)

> *O texto alternativo da imagem inclui a palavra‑chave principal para atender ao SEO.*

---

## Etapa 5: Casos de Borda & Variações Comuns

### E se um OrderId contiver caracteres ilegais?

Os nomes de planilhas do Excel não podem conter `\ / ? * [ ] :`. Se seus IDs puderem incluir esses caracteres, higienize‑os:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Adicione uma propriedade calculada à `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Precisa manter a planilha modelo original?

Defina `smartMarkerOptions.RemoveTemplate = false;` (o padrão é `true`). Isso deixa a `InvoiceTemplate` original intacta como referência.

### Quer agrupar faturas por cliente?

Você pode aninhar **grupos de repetição**. Primeiro repita por cliente, depois por pedidos dentro de cada planilha de cliente. A sintaxe fica um pouco mais complexa, mas o princípio permanece o mesmo—use `RepeatWorksheet` e um padrão de nomeação que reflita a hierarquia.

---

## Exemplo Completo Funcional (Todo o Código em Um Só Lugar)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copie‑e‑cole isso em `Program.cs`, coloque `InvoiceTemplate.xlsx` ao lado dele, e você está pronto para usar.

---

## Perguntas Frequentes

**Q: Essa abordagem funciona com grandes volumes de dados (milhares de faturas)?**  
A: Sim. O SmartMarker transmite os dados de forma eficiente, mas fique atento ao uso de memória. Se atingir limites, considere processar em lotes e gravar cada lote em uma pasta de trabalho separada.

**Q: Posso adicionar um logotipo a cada fatura automaticamente?**  
A: Absolutamente. Coloque a imagem do logotipo na planilha modelo. Como a planilha é duplicada, o logotipo aparecerá em cada fatura gerada sem código adicional.

**Q: E se eu precisar proteger as planilhas?**  
A: Após o processamento, percorra `wb.Worksheets` e chame `ws.Protect(Password, ProtectionType.All)`.

---

## Conclusão

Acabamos de **automatizar a geração de faturas** aproveitando o recurso de repetição de planilhas do SmartMarker e um padrão de nomeação inteligente. O tutorial abordou **como nomear planilhas**, demonstrou **como repetir planilhas** para cada pedido e apresentou **nomeação dinâmica de planilhas** que mantém sua pasta de trabalho organizada e pesquisável.

Desde a extração de dados, configuração de um modelo, configuração de `SmartMarkerOptions`, até o tratamento de casos de borda, agora você tem uma solução completa e executável. Em seguida, experimente adicionar tabelas de itens, aplicar formatação condicional ou exportar os mesmos dados para PDF, criando um pipeline de faturamento totalmente automatizado.

Pronto para evoluir? Explore tópicos relacionados como “exportação em massa de Excel com Aspose.Cells”, “conversão de planilhas para PDF” ou “envio de faturas geradas por e‑mail diretamente do C#”. O céu é o limite—bom código!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}