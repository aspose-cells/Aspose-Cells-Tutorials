---
category: general
date: 2026-11-19
description: Aprenda a gerar Excel a partir de um modelo em C# rapidamente. Este guia
  também mostra como gerar relatórios Excel em C# usando Smart Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: pt
lastmod: 2026-11-19
og_description: Gere Excel a partir de um modelo em C# com Aspose.Cells. Siga este
  tutorial para gerar relatório Excel em C# usando Smart Markers e dados mestre‑detalhe.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Gerar Excel a partir de modelo em C# – guia completo passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Como gerar Excel a partir de um modelo com C# e Aspose.Cells
url: /pt/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gerar Excel a partir de um modelo em C# – guia completo passo a passo

Se você precisa **gerar Excel a partir de um modelo** em um projeto .NET, este tutorial mostra uma solução pronta‑para‑executar. Usando Aspose.Cells Smart Markers você pode preencher uma pasta de trabalho pré‑projetada com dados mestre‑detalhe e produzir um relatório polido sem escrever fórmulas específicas do Excel.

Você também verá como a mesma abordagem permite **gerar relatório Excel C#** para faturas, resumos de pedidos ou qualquer conjunto de dados hierárquico. Ao final do guia você terá um método reutilizável que transforma um arquivo de modelo em uma pasta de trabalho totalmente preenchida.

## O que este tutorial cobre

* Carregar um modelo `.xlsx` existente que já contém marcadores Smart Marker.  
* Preparar um objeto mestre‑detalhe que corresponda à hierarquia do modelo.  
* Configurar o `SmartMarkerProcessor` para criar uma planilha de detalhe separada para coleções aninhadas.  
* Processar a planilha e salvar o resultado como um novo arquivo.  

Nenhum serviço externo é necessário — apenas a biblioteca Aspose.Cells para .NET (versão de avaliação ou licenciada) e um projeto .NET 6+.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| **Aspose.Cells for .NET** (pacote NuGet `Aspose.Cells`) | Fornece o `SmartMarkerProcessor` e as APIs de manipulação de Excel. |
| **.NET 6 SDK** ou posterior | Garante recursos de linguagem modernos e compatibilidade com a versão mais recente do Aspose.Cells. |
| **Uma pasta de trabalho modelo** (`template.xlsx`) com Smart Markers posicionados na primeira planilha | Os Smart Markers conduzem a vinculação de dados; o modelo define layout, estilos e conteúdo estático. |
| Conhecimento básico de coleções C# e tipos anônimos | A fonte de dados é construída como um objeto anônimo que espelha a estrutura do modelo. |

Você pode criar o modelo no Excel digitando `&=Orders.Id` para a coluna de ID do pedido e `&=Orders.Items.Name` para os itens aninhados. O prefixo `&=` indica aos Smart Markers que substituam a célula pelos dados em tempo de execução.

---

## Etapa 1: Configurar o projeto C# e adicionar Aspose.Cells

Crie um aplicativo console (ou integre a um serviço existente) e adicione o pacote NuGet:

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Dica profissional:** Use a flag `--version` para travar em uma versão estável conhecida, por exemplo, `Aspose.Cells 23.12`.

---

## Etapa 2: Definir a fonte de dados mestre‑detalhe

A fonte de dados deve refletir a hierarquia usada no modelo. Neste exemplo temos pedidos (mestre) cada um contendo uma coleção de itens (detalhe).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Por que isso funciona:**  
*O tipo anônimo* permite criar rapidamente uma representação em memória sem definir classes POCO explícitas. Cada `Order` tem um `Id` e um array `Items`, que corresponde aos marcadores `&=Orders.Id` e `&=Orders.Items.Name` no modelo.

---

## Etapa 3: Carregar o modelo Excel que contém Smart Markers

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Explicação:**  
`Workbook` lê o arquivo `.xlsx` para a memória. O modelo já deve conter a sintaxe de Smart Marker (`&=Orders.Id`, `&=Orders.Items.Name`, etc.) nos locais onde você deseja que os dados apareçam.

---

## Etapa 4: Obter a planilha onde os Smart Markers estão posicionados

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Por que a primeira planilha?**  
A maioria dos modelos mantém a tabela mestre na primeira planilha, mas você pode referenciar qualquer planilha pelo nome (`workbook.Worksheets["SheetName"]`) se o seu design for diferente.

---

## Etapa 5: Configurar o processador SmartMarker

O `SmartMarkerProcessor` cuida da parte pesada. Ao definir `DetailSheetNewName` instruímos o Aspose.Cells a criar uma nova planilha para cada coleção aninhada.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**O que isso faz:**  
Quando o processador encontra uma coleção dentro de outra coleção (o array `Items`), ele cria uma nova planilha chamada `OrderDetails` e a preenche com as linhas relacionadas. Isso mantém a planilha mestre organizada e reflete um layout típico de relatório mestre‑detalhe.

---

## Etapa 6: Processar a planilha usando a fonte de dados

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

O método `Process` substitui cada Smart Marker pelo valor correspondente em `orderData`. Ele também expande linhas conforme necessário, de modo que você não precise pré‑alocar espaço no modelo.

---

## Etapa 7: Salvar a pasta de trabalho preenchida

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Resultado:**  
- `masterDetail.xlsx` contém uma planilha mestre com os IDs dos pedidos.  
- Uma nova planilha `OrderDetails` contém os nomes dos itens para cada pedido.  
- Toda a formatação (fontes, bordas, larguras de coluna) do modelo é preservada.

Abra o arquivo no Excel para verificar se os dados correspondem ao objeto de origem.

---

## Código-fonte completo (pronto para copiar‑colar)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Saída esperada no Excel**

| **Orders** (planilha mestre) |
|---|
| Id |
| 1 |
| 2 |

Planilha *OrderDetails*:

| **Items** |
|---|
| Name |
| A |
| B |
| C |

As linhas são adicionadas automaticamente para corresponder ao número de itens por pedido.

---

## Variações comuns e casos de borda

| Situação | Como adaptar o código |
|----------|-----------------------|
| **Múltiplos níveis de detalhe** (ex.: Orders → Items → SubItems) | Adicione outra propriedade de coleção (`SubItems`) e defina `DetailSheetNewName` com um valor diferente para cada nível. O Aspose.Cells criará planilhas adicionais automaticamente. |
| **Nomeação de planilha personalizada por registro mestre** | Use `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` e inclua um campo `SheetName` na coleção mestre. |
| **Conjuntos de dados grandes (10 000+ linhas)** | Chame `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` antes de carregar o modelo para reduzir o consumo de memória. |
| **Modelo sem planilha de detalhe** (relatório plano) | Omitir `DetailSheetNewName`; o processador gravará os dados aninhados diretamente na planilha mestre, expandindo linhas conforme necessário. |
| **Execução em ASP.NET Core** | Substitua `Console.WriteLine` por logging (`ILogger`) e use `Path.Combine` para resolver caminhos de arquivos relativos ao `wwwroot`. |

---

## Dicas para geração confiável de Excel

* **Mantenha os marcadores em uma linha separada** – Smart Markers expandem linhas abaixo do marcador; posicioná‑los na linha de cabeçalho preserva a formatação.  
* **Evite mesclar células dentro da região de dados** – Células mescladas podem causar deslocamentos inesperados de linhas durante a expansão.  
* **Teste primeiro com um conjunto de dados mínimo**; depois que o layout funcionar, escale para dados reais.  
* **Trave a versão** – Registre a versão do Aspose.Cells que você usou (`Aspose.Cells 23.12`) para evitar quebras ao atualizar.  

---

## Conclusão

Agora você sabe como **gerar Excel a partir de um modelo** em C# usando Aspose.Cells Smart Markers, e pode facilmente estender o mesmo padrão para **gerar relatório Excel C#** em qualquer cenário mestre‑detalhe. A abordagem separa o layout (o modelo) dos dados (o objeto C#), proporcionando um mecanismo de relatório mantível e reutilizável.

Em seguida, explore estes tópicos relacionados:

* **Estilizando células programaticamente** – aprenda a aplicar formatação condicional após os dados serem preenchidos.  
* **Exportando para PDF** – o Aspose.Cells pode converter a pasta de trabalho gerada em PDF com uma única chamada.  
* **Integração com ASP.NET Core** – transmita o arquivo gerado diretamente ao navegador sem gravá‑lo em disco.

Experimente o código, modifique o modelo para combinar com a identidade visual da sua empresa e deixe os relatórios Excel gerados se tornarem parte central das suas aplicações .NET. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to generate Excel report by merging an Excel template with Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}