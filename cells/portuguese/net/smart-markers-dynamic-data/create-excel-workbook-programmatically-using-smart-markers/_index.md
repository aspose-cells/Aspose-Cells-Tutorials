---
category: general
date: 2026-09-24
description: Crie programaticamente uma pasta de trabalho do Excel e aprenda a criar
  várias planilhas de detalhes; em seguida, salve a pasta de trabalho como arquivo
  xlsx com um exemplo claro em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: pt
lastmod: 2026-09-24
og_description: Crie uma pasta de trabalho do Excel programaticamente, veja como criar
  várias planilhas de detalhes e salvar a pasta de trabalho como arquivo xlsx em um
  único exemplo executável.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Criar planilha Excel programaticamente – guia completo de C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Criar pasta de trabalho do Excel programaticamente usando Smart Markers
url: /pt/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel programaticamente usando Smart Markers

Se você precisa **criar pasta de trabalho Excel programaticamente**, este guia mostra exatamente como fazer isso com Aspose.Cells .NET. Você também descobrirá **como criar várias planilhas de detalhe** a partir de uma única fonte de dados e, finalmente, **salvar a pasta de trabalho como arquivo xlsx** sem nenhuma etapa manual.  

A solução é autônoma: percorremos cada linha de código, explicamos por que cada configuração importa e abordamos armadilhas comuns, como nomes de planilhas duplicados. Ao final, você terá um aplicativo de console pronto‑para‑executar que produz uma pasta de trabalho com uma planilha mestre e um conjunto de planilhas de detalhe.

## O que você precisará

| Pré-requisito | Motivo |
|--------------|--------|
| .NET 6.0 SDK ou posterior | Fornece o runtime para o aplicativo de console C# |
| Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`) | Fornece as classes `Workbook`, `SmartMarkerProcessor` e `SmartMarkerOptions` |
| Uma fonte de dados simples (ex.: `DataTable` ou uma lista de objetos) | Fornece os valores que os Smart Markers expandirão |
| Visual Studio 2022 ou qualquer editor que suporte .NET | Facilita a compilação e execução do código |

> **Dica profissional:** Instale o pacote Aspose.Cells via CLI antes de começar:  
> `dotnet add package Aspose.Cells`

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo projeto de console e traga os namespaces necessários para o escopo.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Por que isso importa*: `Aspose.Cells` gerencia o ciclo de vida da pasta de trabalho, enquanto `Aspose.Cells.SmartMarkers` fornece o poderoso mecanismo Smart Marker que pode gerar várias planilhas a partir de um único modelo.

## Etapa 2: Criar a pasta de trabalho Excel programaticamente

A primeira ação concreta é instanciar um `Workbook`. Este objeto representa todo o arquivo Excel na memória.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Se preferir iniciar a partir de um modelo que já contém linhas de cabeçalho ou formatação, substitua `new Workbook()` por `new Workbook("Template.xlsx")`. O resto do processo funciona de forma idêntica.

## Etapa 3: Preparar um modelo Smart Marker

Smart Markers funcionam em conteúdos de célula que contêm marcadores de posição como `&=Employees.Name`. Para este tutorial, adicionaremos um modelo simples diretamente via código, mas você também pode editar a planilha manualmente no Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Por que isso importa*: O marcador de posição `&=Employees.Name` indica ao processador Smart Marker para iterar sobre a coleção `Employees`. Cada iteração criará uma nova planilha porque configuraremos o processador para criar uma **planilha de detalhe** para cada linha.

## Etapa 4: Construir uma fonte de dados que contenha várias linhas

Usaremos um `DataTable` como uma forma rápida de simular uma coleção de registros de funcionários.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Você pode substituir isso por qualquer `IEnumerable` (ex.: `List<Employee>`) – Smart Markers aceitam qualquer fonte de dados que implemente `IEnumerable`.

## Etapa 5: Configurar opções do Smart Marker – como criar várias planilhas de detalhe

Por padrão, Smart Markers gravam os dados de volta na mesma planilha. Para gerar **várias planilhas de detalhe**, você deve definir a propriedade `DetailSheetNewName`. Isso também demonstra **como criar várias planilhas de detalhe** sem conflitos de nomes.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Se a fonte de dados contiver nomes duplicados, o processador adiciona automaticamente um sufixo numérico (ex.: `Detail_1`, `Detail_2`). Isso evita erros em tempo de execução e garante que todas as planilhas de detalhe sejam salvas.

## Etapa 6: Processar os Smart Markers

Agora invocamos o processador, passando a fonte de dados e as opções que acabamos de definir.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Por que isso importa*: O processador lê o marcador de posição `&=Employees.Name`, itera sobre cada linha de `employees`, cria uma nova planilha chamada “Detail” e grava os dados da linha nessa planilha. A planilha original permanece como uma planilha de resumo ou mestre.

## Etapa 7: Salvar a pasta de trabalho como arquivo xlsx

Finalmente, persista a pasta de trabalho no disco usando o padrão **salvar pasta de trabalho como arquivo xlsx**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

O enum `SaveFormat.Xlsx` garante que o arquivo seja armazenado no formato moderno Office Open XML, que é compatível com Excel 2007+ e a maioria dos serviços de nuvem.

## Exemplo completo e executável

Copie o código a seguir para `Program.cs` de um projeto de console .NET e execute-o. O programa gerará `detail.xlsx` na pasta `output`, contendo uma planilha mestre e três planilhas de detalhe (uma por funcionário).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Saída esperada**

- `output/detail.xlsx` contém:
  - **Sheet1** – o modelo original com o cabeçalho “Employee Report”.
  - **Detail** – primeira planilha de detalhe com o registro de Alice.
  - **Detail_1** – segunda planilha de detalhe com o registro de Bob.
  - **Detail_2** – terceira planilha de detalhe com o registro de Carol.

Abra o arquivo no Excel e você verá cada funcionário em sua própria planilha, comprovando que conseguimos **criar várias planilhas de detalhe** e **salvar a pasta de trabalho como arquivo xlsx**.

## Perguntas comuns e tratamento de casos extremos

| Pergunta | Resposta |
|----------|----------|
| *E se eu precisar de um nome personalizado para cada planilha de detalhe?* | Defina `DetailSheetNewName = "Employee_"` e inclua uma coluna chamada `SheetName` na fonte de dados. O processador acrescentará o valor de `SheetName` ao nome base. |
| *Posso manter a planilha original como um resumo de todos os detalhes?* | Sim. A planilha mestre permanece intacta; você pode adicionar fórmulas que referenciam as planilhas de detalhe geradas. |
| *O que acontece quando a fonte de dados está vazia?* | Nenhuma planilha de detalhe é criada, mas a pasta de trabalho ainda é salva. Considere verificar `employees.Rows.Count` antes do processamento se precisar de tratamento especial. |
| *É possível usar um arquivo de modelo existente?* | Substitua `new Workbook()` por `new Workbook("Template.xlsx")`. Toda a lógica do Smart Marker funciona da mesma forma. |

## Conclusão

Agora você sabe **como criar pasta de trabalho Excel programaticamente**, como **criar várias planilhas de detalhe** usando Smart Markers e como **salvar a pasta de trabalho como arquivo xlsx** com Aspose.Cells. O exemplo completo pode ser adaptado para faturas, relatórios ou qualquer cenário onde seja necessário um output Excel mestre‑detalhe.

### Próximos passos

- Explore outros recursos do Smart Marker, como **marcadores de grupo** e **formatação condicional**.
- Substitua o `DataTable` por uma consulta real ao banco de dados para gerar relatórios em grande escala.
- Use `Workbook.Save("output.pdf", SaveFormat.Pdf)` para exportar os mesmos dados para PDF para distribuição.

Sinta-se à vontade para experimentar diferentes esquemas de nomenclatura, estilos ou planilhas adicionais — suas novas habilidades de geração programática de Excel estão prontas para uso em produção. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel C# – Adicionar Comentário e Salvar como XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Criar Nova Pasta de Trabalho em C# – Adicionar Fórmula e Salvar Arquivo Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Criar Pasta de Trabalho Excel C# – Inserir JSON e Salvar como XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}