---
category: general
date: 2026-10-26
description: Crie uma pasta de trabalho do Excel programaticamente em C# usando marcadores
  inteligentes do Aspose.Cells e dados JSON. Siga um guia passo a passo com código
  completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- Aspose.Cells smart markers
- C# Excel automation
- JSON data binding
- process smart markers
language: pt
lastmod: 2026-10-26
og_description: Crie uma pasta de trabalho Excel programaticamente em C# usando marcadores
  inteligentes do Aspose.Cells e dados JSON. Este tutorial fornece um exemplo completo
  e executável.
og_image_alt: Generated Excel workbook showing employee list created programmatically
og_title: Criar pasta de trabalho do Excel programaticamente em C# – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Create Excel workbook programmatically in C# using Aspose.Cells smart
    markers and JSON data. Follow a step‑by‑step guide with complete code.
  headline: How to create Excel workbook programmatically with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Como criar uma pasta de trabalho do Excel programaticamente com C#
url: /pt/net/smart-markers-dynamic-data/how-to-create-excel-workbook-programmatically-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel programaticamente com C#

Se você precisa **criar uma pasta de trabalho Excel programaticamente**, este tutorial mostra uma solução completa usando marcadores inteligentes do Aspose.Cells e um objeto de dados no estilo JSON. Você verá como inserir um marcador, vincular um array JSON, processar os marcadores e salvar o resultado — tudo em um único aplicativo console C# executável.

Criar arquivos Excel programaticamente elimina a entrada manual de dados e permite relatórios automatizados, exportação de dados e integração com outros sistemas. O exemplo abaixo demonstra **automação Excel em C#** que pode ser adaptado a qualquer fonte de dados, seja um banco de dados, serviço web ou coleção em memória.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou superior (o código também funciona com .NET Framework 4.7+).
* Visual Studio 2022 ou qualquer IDE que suporte projetos C#.
* Uma licença válida do Aspose.Cells for .NET (ou uma licença temporária gratuita para avaliação).  
  Instale o pacote NuGet:

```bash
dotnet add package Aspose.Cells
```

## Etapa 1: Configurar o projeto console

Crie um novo aplicativo console e adicione as diretivas `using` necessárias.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The full workflow is implemented in the RunDemo method.
            RunDemo();
        }

        private static void RunDemo()
        {
            // Steps 2‑5 are called from here.
        }
    }
}
```

*Por que esta etapa?*  
Uma estrutura de projeto limpa mantém a demonstração isolada e facilita a integração do código em soluções maiores posteriormente.

## Etapa 2: Criar uma nova pasta de trabalho e inserir um marcador inteligente

Dentro de `RunDemo`, instancie uma pasta de trabalho, acesse a primeira planilha e coloque um marcador inteligente que será substituído por um array JSON.

```csharp
private static void RunDemo()
{
    // Create a new workbook with one worksheet.
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.Worksheets[0];

    // Insert a smart marker. The marker syntax ${Collection:ArrayAsSingle}
    // tells Aspose.Cells to expand the collection into a single column.
    worksheet.Cells[0, 0].PutValue("${Employees:ArrayAsSingle}");
}
```

*Por que esta etapa?*  
Marcadores inteligentes do Aspose.Cells atuam como marcadores de posição que a biblioteca substitui pelos dados em tempo de execução. Usar `${Employees:ArrayAsSingle}` indica ao motor que escreva cada nome de funcionário em uma linha separada a partir da célula **A1**.

## Etapa 3: Preparar o objeto de dados no estilo JSON

Crie um objeto anônimo que imita uma carga JSON. O nome da propriedade deve corresponder ao nome do marcador (`Employees`).

```csharp
    // Prepare data that matches the smart marker.
    var employeeData = new
    {
        Employees = new[] { "John", "Jane", "Bob" }
    };
```

*Por que esta etapa?*  
Marcadores inteligentes funcionam com qualquer objeto .NET que possa ser serializado para JSON. Ao usar um tipo anônimo, você evita classes de modelo extras enquanto demonstra **vinculação de dados JSON**.

## Etapa 4: Processar os marcadores inteligentes

Passe o objeto de dados para `ProcessSmartMarkers`. O método varre a pasta de trabalho, substitui o marcador e expande as linhas automaticamente.

```csharp
    // Replace the marker with actual data.
    workbook.ProcessSmartMarkers(employeeData);
```

*Por que esta etapa?*  
`ProcessSmartMarkers` é o núcleo da funcionalidade **process smart markers**. Ele analisa o marcador, mapeia a propriedade `Employees` para o array JSON e grava cada elemento na planilha.

## Etapa 5: Salvar a pasta de trabalho preenchida

Por fim, escreva a pasta de trabalho em um arquivo. Ajuste o caminho conforme necessário para o seu ambiente.

```csharp
    // Save the result to disk.
    string outputPath = @"YOUR_DIRECTORY/JsonSingle.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

*Por que esta etapa?*  
Salvar a pasta de trabalho gera um arquivo padrão `.xlsx` que pode ser aberto no Microsoft Excel, Google Sheets ou qualquer visualizador compatível.

## Programa completo e executável

Juntando todas as etapas, aqui está o arquivo‑fonte completo que você pode copiar para `Program.cs` e executar.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            RunDemo();
        }

        private static void RunDemo()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert a smart marker that will be replaced by a JSON array.
            worksheet.Cells[0, 0].PutValue("${Employees:ArrayAsSingle}");

            // 3️⃣ Prepare the JSON‑style data object.
            var employeeData = new
            {
                Employees = new[] { "John", "Jane", "Bob" }
            };

            // 4️⃣ Process the smart markers using the data object.
            workbook.ProcessSmartMarkers(employeeData);

            // 5️⃣ Save the populated workbook.
            string outputPath = @"YOUR_DIRECTORY/JsonSingle.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Saída esperada

Após executar o programa, abra `JsonSingle.xlsx`. A primeira coluna (A) conterá:

| A      |
|--------|
| John   |
| Jane   |
| Bob    |

A pasta de trabalho é criada **programaticamente**, e os dados foram inseridos via **marcadores inteligentes** sem qualquer manipulação manual de células.

![Generated Excel workbook showing employee list created programmatically](excel-workbook.png){.align-center width=600 alt="Pasta de Excel gerada mostrando a lista de funcionários criada programaticamente"}

*Descrição da imagem (texto alternativo):* *Pasta de Excel gerada mostrando a lista de funcionários criada programaticamente.*

## Variações comuns e casos de borda

| Situação | Como adaptar o código |
|-----------|----------------------|
| **Múltiplas colunas** – você precisa escrever uma tabela com nome, idade e departamento. | Use `${Employees:Array}` com uma coleção de objetos que possuam essas propriedades e coloque o marcador na célula superior‑esquerda da tabela. |
| **Conjuntos de dados grandes** – mais de 10 000 linhas. | Chame `workbook.CalculateFormula()` após o processamento para garantir que quaisquer fórmulas sejam recalculadas de forma eficiente. |
| **Formato de arquivo personalizado** – você quer um CSV em vez de XLSX. | Substitua `workbook.Save(outputPath, SaveFormat.Csv);` onde `SaveFormat` é um enum do Aspose.Cells. |
| **Sem licença** – você está usando a versão de avaliação. | A biblioteca adiciona uma marca d'água; obtenha uma licença para removê‑la em produção. |
| **Nome de arquivo dinâmico** – o caminho de saída depende da data atual. | Use `string outputPath = $"Reports/Employees_{DateTime.Now:yyyyMMdd}.xlsx";`. |

### Dicas avançadas

* **Reutilizar a pasta de trabalho** – se você gerar muitos relatórios em um loop, mantenha uma única instância `Workbook` e limpe suas planilhas com `workbook.Worksheets.Clear();` antes de cada iteração.
* **Desempenho** – desative o cálculo automático durante a inserção em massa de dados: `workbook.Settings.CalculateFormulaOnOpen = false;`.
* **Segurança de threads** – cada thread deve trabalhar com sua própria instância `Workbook`; objetos Aspose.Cells não são thread‑safe.

## Conclusão

Agora você sabe como **criar uma pasta de trabalho Excel programaticamente** usando C#, marcadores inteligentes do Aspose.Cells e um objeto de dados no estilo JSON. O tutorial cobriu cada passo, desde a configuração do projeto até a gravação do arquivo final, explicou a importância de cada operação e forneceu variações para cenários mais complexos.

Em seguida, explore tópicos relacionados como **automação Excel em C# com fórmulas**, **exportação para PDF** ou **uso de tabelas de dados para formatação avançada**. Cada um desses se baseia na mesma fundação de marcadores inteligentes e ajuda a entregar soluções de relatório totalmente automatizadas.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar pasta de trabalho Excel programaticamente usando Marcadores Inteligentes](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/)
- [Criar Pasta de Trabalho Excel a partir de JSON – Guia Completo do Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Como Criar Pasta de Trabalho com Marcadores Inteligentes – Guia Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}