---
category: general
date: 2026-11-19
description: Como repetir a planilha ao preencher o Excel com dados de array. Aprenda
  a gerar várias planilhas e preencher a planilha a partir de uma lista em poucos
  passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: pt
lastmod: 2026-11-19
og_description: Como repetir planilha usando SmartMarkerProcessor. Siga este guia
  para preencher o Excel com dados de array, gerar várias planilhas e preencher a
  planilha a partir de uma lista.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Como repetir planilha no Excel – guia passo a passo
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Como repetir planilha no Excel com SmartMarkerProcessor
url: /pt/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como repetir planilha no Excel com SmartMarkerProcessor

Se você precisa **how to repeat worksheet** ao gerar relatórios Excel, este guia mostra uma solução completa e executável. Ao final do tutorial, você será capaz de **populate Excel with array** data, **generate multiple worksheets**, e **populate worksheet from list** usando a biblioteca SmartMarkerProcessor.

Repetir uma planilha é uma necessidade comum quando cada departamento, região ou período precisa de sua própria aba. O exemplo abaixo demonstra os passos exatos, explica por que cada configuração importa e cobre casos de borda como listas vazias ou nomes personalizados.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou posterior instalado
- Uma referência ao pacote NuGet **GroupDocs.Viewer** (ou equivalente) que contém `SmartMarkerProcessor`
- Um modelo de pasta de trabalho Excel (`.xlsx`) com um marcador como `${repeat:Dept}` colocado em uma linha que você deseja repetir
- Familiaridade básica com C# e LINQ (opcional, mas útil)

Nenhuma biblioteca de terceiros adicional é necessária.

## Passo 1: Crie a instância do SmartMarkerProcessor

O processador orquestra a substituição de marcadores e a duplicação de planilhas. Instanciá‑lo sem argumentos usa as opções padrão.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Criar o processador antecipadamente permite configurar opções globais antes que quaisquer dados sejam aplicados. Esta é a base para **how to repeat worksheet** corretamente.

## Passo 2: Habilitar repetição de planilha

Por padrão, o processador substitui marcadores apenas na planilha atual. Definir `RepeatWorksheet` como `true` indica ao mecanismo que clone a planilha inteira para cada item na coleção de dados.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Habilitar esta opção é a chave para **generate multiple worksheets** — o processador criará uma nova aba para cada elemento no array `Dept` e manterá a formatação original.

## Passo 3: Prepare a fonte de dados como um array ou lista

SmartMarkerProcessor funciona com qualquer enumerable, mas usar um array deixa a intenção clara quando você deseja **populate worksheet from list**. Aqui criamos um objeto anônimo que contém uma propriedade `Dept` contendo um array de strings.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Se você já tem um `List<string>` pode passá‑lo diretamente; o processador o tratará da mesma forma. A parte importante é que o nome da propriedade (`Dept`) corresponda ao marcador `${repeat:Dept}` no modelo.

## Passo 4: Carregue a planilha modelo

Assumindo que você tem um `ExcelPackage` (do EPPlus) ou um objeto `Workbook`, recupere a planilha que deseja repetir. A variável `ws` representa essa planilha.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Se preferir uma biblioteca diferente (por exemplo, ClosedXML), o mesmo princípio se aplica: obtenha um objeto de planilha que implemente a interface necessária.

## Passo 5: Processar a planilha com os dados

Agora aplique os dados ao modelo. O processador clona a planilha para cada departamento, substitui o marcador `${repeat:Dept}` pelo nome real do departamento e deixa o restante da planilha intacto.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Após a conclusão de `Process`, `ws` torna‑se a primeira de várias planilhas — uma por departamento. O nome da planilha original é preservado, enquanto as duplicatas recebem sufixos incrementais (ex.: “Sheet1 (1)”, “Sheet1 (2)”). Você pode renomeá‑las depois, se precisar de um esquema de nomes personalizado.

### Saída esperada

Quando você abrir a pasta de trabalho resultante, deverá ver:

- **Sheet1** – o modelo original (geralmente deixado em branco ou usado como mestre)
- **Sheet1 (1)** – preenchido com “HR”
- **Sheet1 (2)** – preenchido com “IT”
- **Sheet1 (3)** – preenchido com “Finance”

Cada aba contém o mesmo layout, mas com o nome do departamento substituído onde `${repeat:Dept}` aparecia.

## Tratamento de casos de borda

### Arrays vazios ou nulos

Se `Dept` for nulo ou vazio, o processador não criará planilhas adicionais. Para evitar uma pasta de trabalho completamente vazia, você pode adicionar uma proteção:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Nomes de planilha personalizados

O esquema de nomenclatura padrão pode não atender a todos os requisitos de relatório. Após o processamento, renomeie cada planilha usando um loop:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Preenchendo colunas adicionais

Se precisar **populate excel with array** valores além de um único marcador, estenda o objeto de dados:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Em seguida, ajuste os marcadores do modelo para `${repeat:Dept.Name}` e `${repeat:Dept.Headcount}`. O processador repetirá a linha para cada departamento e preencherá ambas as colunas.

## Exemplo completo em funcionamento

Abaixo está um aplicativo de console autônomo que demonstra todo o fluxo, desde o carregamento do modelo até a gravação da pasta de trabalho final.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explicação das seções principais**

- **Processor creation** – estabelece o mecanismo que interpretará os marcadores.
- **RepeatWorksheet option** – ativa o recurso principal que responde *how to repeat worksheet*.
- **Data source** – usa um array (`new[]`) para atender **populate excel with array**.
- **Template loading** – demonstra uma forma comum de obter um objeto de planilha.
- **Processing** – realiza a duplicação e inserção de dados em uma única chamada.
- **Renaming** – mostra como transformar os nomes genéricos “(1)”, “(2)” em títulos significativos, um requisito típico após **generate multiple worksheets**.

Executar este programa gera `Result.xlsx` com três abas específicas de departamentos, cada uma preenchida a partir do array.

## Armadilhas comuns e dicas profissionais

- **Marker spelling** – o marcador deve corresponder exatamente ao nome da propriedade (`${repeat:Dept}`). Um erro de digitação impede a repetição.
- **Worksheet index** – após o processamento, a planilha original permanece no índice 0; as planilhas geradas seguem sequencialmente. Indexação incorreta pode levar à renomeação da aba errada.
- **Large data sets** – gerar centenas de planilhas pode aumentar o tamanho do arquivo drasticamente. Considere dividir relatórios ou usar uma única planilha com seções agrupadas se o desempenho se tornar um problema.
- **Thread safety** – `SmartMarkerProcessor` não é seguro para threads. Crie uma instância separada por thread se você processar várias pastas de trabalho em paralelo.

## Conclusão

Agora você sabe **how to repeat worksheet** no Excel usando SmartMarkerProcessor, como **populate excel with array** dados, como **generate multiple worksheets**, e como **populate worksheet from list** de forma eficiente. O exemplo completo une todos os conceitos, e a etapa opcional de renomeação permite produzir nomes de abas limpos e amigáveis ao usuário.

Em seguida, você pode explorar:

- Usar **populate worksheet from list** com objetos complexos (coleções aninhadas)
- Aplicar formatação condicional após a duplicação da planilha
- Exportar a pasta de trabalho gerada para PDF ou CSV para consumo posterior

Sinta‑se à vontade para adaptar o código aos seus próprios cenários de relatório, e aproveite a automação de pastas de trabalho Excel com confiança!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Repetir Planilhas – Guia Completo para Automação Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Criar Planilha Por Item – Como Repetir Planilha em C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Como expandir array no Excel e preencher um modelo](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}