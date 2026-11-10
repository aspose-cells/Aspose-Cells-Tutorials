---
category: general
date: 2026-10-26
description: Aprenda como criar uma pasta de trabalho do Excel e inserir dados no
  Excel usando marcadores inteligentes para construir um relatório dinâmico do Excel
  em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- insert data into excel
- dynamic excel report
language: pt
lastmod: 2026-10-26
og_description: Crie uma pasta de trabalho do Excel e insira dados no Excel usando
  marcadores inteligentes C#. Siga este guia para gerar um relatório dinâmico do Excel
  rapidamente.
og_image_alt: Screenshot showing a created excel workbook with populated data
og_title: Criar pasta de trabalho do Excel com marcadores inteligentes – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create excel workbook and insert data into excel using
    smart markers to build a dynamic excel report in C#.
  headline: How to create excel workbook with smart markers for a dynamic excel report
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Como criar uma pasta de trabalho Excel com marcadores inteligentes para um
  relatório Excel dinâmico
url: /pt/net/smart-markers-dynamic-data/how-to-create-excel-workbook-with-smart-markers-for-a-dynami/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel com marcadores inteligentes para um relatório Excel dinâmico

Se você precisa **criar uma pasta de trabalho Excel** programaticamente, este guia mostra exatamente como fazer. Usando marcadores inteligentes, você pode **inserir dados no Excel** sem escrever código célula por célula, o que torna a geração de um **relatório Excel dinâmico** rápida e fácil de manter.

Você percorrerá cada passo — desde a inicialização da pasta de trabalho até o processamento dos marcadores — para que possa copiar o exemplo completo e executável para o seu próprio projeto. Nenhuma documentação externa é necessária; todo o código e as explicações são fornecidos abaixo.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior (o exemplo também funciona com .NET Framework 4.7+)
* Uma referência à biblioteca **Aspose.Cells** (disponível via NuGet `Install-Package Aspose.Cells`)
* Familiaridade básica com tipos anônimos C# e LINQ
* Uma IDE como Visual Studio ou VS Code

> **Dica profissional:** Use a licença de avaliação gratuita do Aspose.Cells para testes; substitua‑a por uma licença completa antes de colocar em produção.

## Etapa 1: Criar a pasta de trabalho Excel e acessar a primeira planilha

A primeira operação é instanciar um objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória e fornece acesso direto às suas planilhas.

```csharp
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook – this is the core object for any Excel manipulation
            Workbook wb = new Workbook();

            // The workbook always contains at least one worksheet; we work with the first one
            Worksheet ws = wb.Worksheets[0];
```

Criar a pasta de trabalho é a base para qualquer **relatório Excel dinâmico**. Sem esse objeto, você não pode colocar marcadores inteligentes nem salvar o arquivo posteriormente.

## Etapa 2: Inserir tags de marcador inteligente onde os dados serão inseridos

Marcadores inteligentes são placeholders especiais que o Aspose.Cells substitui por dados em tempo de execução. Eles seguem a sintaxe `${Object.Property}` e podem representar linhas únicas, tabelas ou dados hierárquicos.

```csharp
            // Insert a smart marker for the master (header) section
            ws.Cells[0, 0].PutValue("${Orders.Master}");

            // Insert a smart marker for the detail (row) section
            ws.Cells[1, 0].PutValue("${Orders.Detail}");
```

* A célula `[0,0]` (A1) se tornará a linha de cabeçalho.
* A célula `[1,0]` (A2) será expandida em tantas linhas quantos forem os itens em `Orders.Detail`.

Inserir marcadores diretamente na planilha significa que você **insere dados no Excel** automaticamente mais tarde, eliminando loops manuais.

## Etapa 3: Preparar a fonte de dados que corresponde aos marcadores inteligentes

Marcadores inteligentes exigem uma fonte de dados cuja estrutura reflita a hierarquia dos marcadores. Aqui usamos um objeto anônimo que contém uma coleção de pedidos. Cada pedido inclui uma linha mestre e uma coleção de linhas de detalhe.

```csharp
            // Build the data that matches the markers
            var data = new
            {
                Orders = GetOrders()
            };
```

O método `GetOrders` (mostrado abaixo) retorna uma lista de objetos `OrderInfo`. Cada `OrderInfo` contém um objeto `Master` para o cabeçalho e uma lista `Detail` para as linhas.

```csharp
        // Sample data generator – replace with your real data source (e.g., database, API)
        static List<OrderInfo> GetOrders()
        {
            return new List<OrderInfo>
            {
                new OrderInfo
                {
                    Master = new { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today },
                    Detail = new[]
                    {
                        new { Product = "Widget A", Qty = 10, Price = 9.99 },
                        new { Product = "Widget B", Qty = 5,  Price = 19.99 }
                    }
                },
                new OrderInfo
                {
                    Master = new { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1) },
                    Detail = new[]
                    {
                        new { Product = "Gadget X", Qty = 2, Price = 99.99 },
                        new { Product = "Gadget Y", Qty = 1, Price = 149.99 }
                    }
                }
            };
        }

        // Helper class to keep master/detail together
        class OrderInfo
        {
            public object Master { get; set; }
            public object[] Detail { get; set; }
        }
```

Fornecer uma fonte de dados bem estruturada garante que o **relatório Excel dinâmico** seja expandido corretamente para qualquer número de pedidos.

## Etapa 4: Processar os marcadores inteligentes para preencher a planilha

Agora que a pasta de trabalho contém marcadores e a fonte de dados está pronta, chame `ProcessSmartMarkers`. O Aspose.Cells varre a planilha, substitui cada marcador pelos valores apropriados e expande automaticamente as linhas para coleções.

```csharp
            // Populate the worksheet by processing the smart markers
            wb.ProcessSmartMarkers(data);
```

Durante o processamento:

* `${Orders.Master}` torna‑se uma única linha contendo os campos mestre (`OrderId`, `Customer`, `Date`).
* `${Orders.Detail}` expande‑se em múltiplas linhas, uma por entrada de detalhe, preservando o alinhamento das colunas.

## Etapa 5: Salvar a pasta de trabalho e verificar o resultado

Por fim, grave a pasta de trabalho em um arquivo físico. Você pode abrir o resultado em qualquer programa compatível com Excel para confirmar que os dados foram inseridos corretamente.

```csharp
            // Save the populated workbook to disk
            string outputPath = "DynamicReport.xlsx";
            wb.Save(outputPath, SaveFormat.Xlsx);

            System.Console.WriteLine($"Report generated: {outputPath}");
        }
    }
}
```

**Saída esperada:** Ao abrir `DynamicReport.xlsx`, você verá uma linha de cabeçalho para cada pedido seguida por suas linhas de detalhe. O número de linhas se adapta automaticamente ao tamanho das coleções `Detail`, que é a essência de um **relatório Excel dinâmico**.

![Pasta de trabalho Excel criada com marcadores inteligentes](excel-workbook.png)

*Texto alternativo da imagem:* *criar pasta de trabalho Excel com marcadores inteligentes mostrando dados preenchidos.*

## Variações comuns e casos de borda

| Cenário | O que mudar | Por que importa |
|----------|----------------|----------------|
| **Layout de planilha diferente** | Mover os marcadores inteligentes para outra planilha (`wb.Worksheets[1]`) | Permite manter modelos separados das planilhas de dados |
| **Coleções aninhadas** | Usar `${Orders.SubOrders.Detail}` e adicionar uma propriedade `SubOrders` ao `OrderInfo` | Suporta relatórios mestre/detalhe de múltiplos níveis |
| **Conjuntos de dados grandes** | Chamar `wb.CalculateFormula()` após o processamento se houver fórmulas que dependam dos dados inseridos | Garante que os campos calculados estejam atualizados |
| **Formatação personalizada** | Aplicar objetos de estilo a `ws.Cells` antes do processamento (ex.: `Style style = wb.CreateStyle();`) | Assegura aparência consistente nas linhas geradas |
| **Ambientes com memória limitada** | Usar `WorkbookFactory.Create` com um stream e `Dispose` os objetos prontamente | Evita vazamentos de memória ao gerar muitos relatórios em um serviço |

## Melhores práticas para inserir dados no Excel com marcadores inteligentes

* **Mantenha o modelo limpo:** Coloque apenas os marcadores que você precisa; células extras podem causar posicionamento inesperado de dados.
* **Correspondência exata dos nomes de propriedades:** Marcadores inteligentes diferenciam maiúsculas de minúsculas; um erro de digitação resulta em células vazias sem erro.
* **Reutilize o mesmo objeto de dados:** Se precisar gerar várias planilhas a partir da mesma fonte, chame `ProcessSmartMarkers` repetidamente com a mesma instância `data`.
* **Valide os dados antes do processamento:** Referências nulas dentro da fonte de dados produzirão células em branco; proteja‑as com `?.` ou valores padrão.

## Conclusão

Agora você sabe como **criar uma pasta de trabalho Excel**, usar marcadores inteligentes para **inserir dados no Excel** e produzir um **relatório Excel dinâmico** que escala automaticamente com seus dados. O exemplo completo de código pode ser copiado para qualquer projeto C#, ajustado às suas próprias estruturas de dados e ampliado com formatação ou cálculos adicionais.

### Próximos passos

* Explore **inserir dados no Excel** usando fórmulas e gráficos para enriquecer seu relatório.
* Combine esta abordagem com geração de **relatório Excel dinâmico** para múltiplas planilhas (ex.: uma planilha por cliente).
* Integre a solução em uma API ASP.NET Core para entregar relatórios sob demanda.

Boa codificação e aproveite a construção de automação flexível do Excel com Aspose.Cells!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create Excel workbook programmatically using Smart Markers](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/)
- [Create Excel Workbook C# – Full Guide to Inserting Arrays into Cells](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-c-full-guide-to-inserting-arrays-into/)
- [Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-and-write-data-in-c-full-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}