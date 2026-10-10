---
category: general
date: 2026-10-10
description: Aprenda a processar modelo de Excel em C# enquanto nomeia planilhas automaticamente.
  Guia passo a passo com código SmartMarkerProcessor e melhores práticas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: pt
lastmod: 2026-10-10
og_description: Processar modelo Excel em C# e nomear automaticamente as planilhas
  com SmartMarkerProcessor. Siga este tutorial detalhado para gerar pastas de trabalho
  dinâmicas.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Processar modelo Excel e nomear planilhas automaticamente em C# – guia completo
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Como processar um modelo de Excel e nomear planilhas automaticamente em C#
url: /pt/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como processar modelo Excel e nomear planilhas automaticamente em C#

Se você precisa **processar modelo Excel** em uma aplicação .NET, este guia mostra uma maneira confiável de gerar pastas de trabalho e **nomear planilhas automaticamente**. Usando o `SmartMarkerProcessor` do GroupDocs.Parser, você pode vincular dados a um modelo, criar planilhas de detalhe dinamicamente e manter a pasta de trabalho organizada sem renomeação manual.

Você concluirá o tutorial com um exemplo totalmente executável que lê um modelo, aplica uma fonte de dados e produz planilhas nomeadas `Detail`, `Detail_1`, `Detail_2`, … Todos os namespaces necessários, etapas de configuração e armadilhas comuns são abordados, para que você possa copiar o código para seu próprio projeto com confiança.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código funciona com .NET Core e .NET Framework)
* Uma referência ao pacote NuGet **GroupDocs.Parser** (versão 23.5 ou mais recente)
* Um modelo Excel (`Template.xlsx`) que contém tags SmartMarker como `{{Table}}` para dados mestre‑detalhe
* Um modelo de dados simples (por exemplo, um `DataTable` ou uma lista de objetos) que corresponde às marcas no modelo

Se algum desses itens estiver faltando, instale o pacote NuGet com:

```bash
dotnet add package GroupDocs.Parser
```

## Visão geral da solução

A solução segue três fases lógicas:

1. **Criar uma instância de `SmartMarkerProcessor`** – este objeto controla todo o mecanismo de modelagem.
2. **Configurar o processador para nomear planilhas de detalhe automaticamente** – a opção `DetailSheetNewName` define o nome base e a biblioteca adiciona sufixos incrementais.
3. **Executar `Process`** – o método lê o modelo, mescla a fonte de dados e grava o resultado em uma nova pasta de trabalho.

Cada fase é explicada abaixo, junto com o código exato que você precisa.

## Etapa 1: Criar uma instância de SmartMarkerProcessor

O processador é o ponto de entrada para todas as operações SmartMarker. Ele não requer argumentos no construtor, mas você pode passar um objeto `SmartMarkerOptions` personalizado mais tarde, se precisar de configurações avançadas.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Por que isso importa*: Instanciar o processador uma vez por operação mantém o uso de memória baixo e permite reutilizar o mesmo objeto para múltiplos modelos, se necessário.

## Etapa 2: Configurar nomeação automática de planilhas

Quando uma tabela mestre‑detalhe se expande em planilhas separadas, a biblioteca cria novas planilhas automaticamente. Definindo `DetailSheetNewName`, você controla o nome base que o mecanismo usa. A biblioteca adiciona um sublinhado e um número incremental para cada planilha adicional.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*Dicas*:

* Escolha um nome base que não entre em conflito com nomes de planilhas existentes no modelo.
* O esquema de nomenclatura funciona para qualquer número de linhas de detalhe; a biblioteca deixa de adicionar sufixos quando a última planilha é criada.
* Se precisar de um padrão de nomeação diferente (por exemplo, prefixo em vez de sufixo), você pode manipular `processor.Options.DetailSheetNewName` antes de cada chamada.

## Etapa 3: Processar a planilha com uma fonte de dados

O método `Process` aceita três argumentos:

* **A planilha de origem** (`Worksheet` object) – você a obtém carregando o arquivo de modelo.
* **O fluxo de destino** – onde a pasta de trabalho processada será gravada.
* **A fonte de dados** – qualquer objeto que implemente `IDataSource` (por exemplo, `DataTable`, `IEnumerable<T>`).

A seguir, um exemplo completo que carrega `Template.xlsx`, vincula um `DataTable` e salva o resultado em `Result.xlsx`.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Explicação das linhas principais*:

* `new Worksheet(templateStream)` lê o arquivo Excel e cria uma representação em memória que o SmartMarker pode manipular.
* `DataTableSource` implementa `IDataSource`, permitindo que o processador enumere linhas e substitua marcas como `{{Employees.Name}}`.
* `processor.Process(ws, dataSource, resultStream)` mescla os dados e grava a pasta de trabalho final em `resultStream`. O método cria automaticamente planilhas de detalhe nomeadas `Detail`, `Detail_1`, etc., devido à opção definida na Etapa 2.
* Após o processamento, o resultado é salvo como `Result.xlsx`. Abra o arquivo no Excel para verificar que existem três planilhas de detalhe, cada uma contendo as linhas da tabela `Employees`.

## Verificar a saída

Abra `Result.xlsx` e verifique o seguinte:

| Nome da planilha | Conteúdo esperado |
|------------------|-------------------|
| Detail | Header row (`Name`, `Department`, `Salary`) and the first data row (`Alice`) |
| Detail_1 | Second data row (`Bob`) |
| Detail_2 | Third data row (`Charlie`) |

Se as planilhas aparecerem com o nome base correto e sufixos incrementais, o fluxo de **processar modelo Excel** foi bem‑sucedido e o recurso de **nomear planilhas automaticamente** funcionou como esperado.

## Tratamento de casos extremos

### Conjuntos de dados grandes

Quando a fonte de dados contém centenas de linhas, o processador cria uma planilha separada para cada linha por padrão. Para evitar que a pasta de trabalho exploda, você pode:

* **Agrupar linhas**: modifique o modelo para usar uma marca de tabela que se repita dentro de uma única planilha em vez de criar uma nova planilha por linha.
* **Limitar a criação de planilhas**: defina `processor.Options.MaxDetailSheets` para um número razoável (por exemplo, 50) e trate o excesso manualmente.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Conflitos com nomes de planilhas existentes

Se o modelo já contém uma planilha chamada `Detail`, o processador adiciona um sufixo numérico para evitar colisão (`Detail_0`, `Detail_1`, …). Para impor uma estratégia personalizada de resolução de conflitos, inspecione `Worksheet.Sheets` antes do processamento e renomeie quaisquer planilhas conflitantes.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Modelos não‑Excel

O mesmo `SmartMarkerProcessor` pode processar modelos Word, PowerPoint ou PDF. A única mudança é a classe que você instancia (`Document`, `Presentation`, etc.). O padrão de **processar modelo Excel** permanece idêntico, o que significa que você pode reutilizar o código com ajustes mínimos.

## Dicas profissionais para uso em produção

* **Reutilizar o processador**: Crie um singleton `SmartMarkerProcessor` se você processar muitos modelos em um serviço web. Isso reduz a sobrecarga de alocação.
* **Usar streams em vez de arquivos**: Em cenários de alto volume, mantenha tanto o modelo quanto o resultado em streams de memória para evitar I/O de disco.
* **Descartar objetos**: Todas as instâncias de `Worksheet`, `FileStream` e `MemoryStream` implementam `IDisposable`. Usar blocos `using`, como mostrado, garante a liberação correta dos recursos.
* **Registro de logs**: Habilite `processor.Options.Logging` para capturar informações detalhadas do processamento, o que ajuda a diagnosticar erros de modelo rapidamente.

## Exemplo completo executável

A seguir está o programa inteiro compilado em um único arquivo. Copie‑o para um projeto de console e execute‑o; a pasta de trabalho de saída aparecerá na pasta do projeto.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

Executar o programa imprime “Processing complete. Check Result.xlsx.” e cria um arquivo Excel que demonstra o fluxo de **processar modelo Excel** com **nomear planilhas automaticamente**.

## Conclusão

Agora você sabe como **processar modelo Excel** em C# enquanto permite que a biblioteca **nomeie planilhas automaticamente** com base em um nome base personalizado. O tutorial abordou criação do processador, configuração de opções, vinculação de dados e etapas de verificação, além do tratamento de casos extremos e dicas para produção. Aplique o mesmo padrão em projetos maiores, integre‑o em APIs web ou estenda‑o para outros formatos Office.

**Próximos passos** que você pode explorar:

* Use `processor.Options.DetailSheetNewName` com valores dinâmicos (por exemplo, incluir data ou ID do usuário).
* Combine múltiplas fontes de dados para gerar hierarquias mestre‑detalhe em várias planilhas.
* Experimente estilizar tags SmartMarker para controlar fontes, cores e formatos numéricos diretamente do modelo.

Feliz codificação e aproveite a automação simplificada do Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Excel a partir de Modelo – Guia passo a passo para desenvolvedores .NET](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [Como mesclar e renomear planilhas Excel usando Aspose.Cells para .NET: Guia passo a passo](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [Como vincular planilhas no Excel com SmartMarker – Guia passo a passo](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}