---
category: general
date: 2026-10-26
description: Aprenda a importar DataTable para uma planilha Excel com C# e Aspose.Cells,
  preservando estilos e cabeçalhos em apenas algumas linhas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: pt
lastmod: 2026-10-26
og_description: Como importar DataTable em uma planilha Excel usando C# e Aspose.Cells.
  Siga este guia completo para preservar estilos, cabeçalhos e formatação.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Como importar DataTable para uma planilha Excel – guia passo a passo em
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Como importar DataTable para uma planilha do Excel usando C#
url: /pt/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como importar DataTable para uma planilha Excel usando C#

Se você precisa **como importar datatable** para uma planilha Excel, este guia mostra os passos exatos em C#. Seja construindo um mecanismo de relatórios ou exportando dados de grade, você verá como manter os cabeçalhos das colunas e os estilos das células intactos com Aspose.Cells. A solução funciona com .NET 6+ e requer apenas algumas linhas de código.

Importar um DataTable é uma tarefa comum ao trabalhar com planilhas, mas os desenvolvedores frequentemente esquecem de habilitar a transferência de estilo ou de passar a bandeira de cabeçalho corretamente. Neste tutorial você aprenderá a configurar **ImportTableOptions**, ativar **ImportDataTableStyle** e chamar `ImportDataTable` com segurança. Ao final, você terá um método pronto‑para‑executar que pode ser inserido em qualquer projeto C#.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6 SDK ou posterior instalado.
* Uma cópia licenciada do **Aspose.Cells for .NET** (a versão de avaliação gratuita serve para testes).
* Familiaridade básica com `DataTable` e conceitos de Excel.
* Uma IDE como Visual Studio 2022 (qualquer editor que suporte C# funciona).

Nenhum pacote NuGet adicional é necessário além do `Aspose.Cells`.

## Etapa 1: Recuperar os dados de origem em um DataTable

A primeira coisa que você faz ao responder **como importar datatable** é ter os dados prontos. Na maioria dos cenários reais, o `DataTable` vem de uma consulta ao banco de dados, de um analisador CSV ou de uma coleção em memória. Aqui está um exemplo mínimo que cria uma tabela com algumas linhas:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Por que isso importa*: Ao construir o `DataTable` primeiro, você controla a ordem das colunas, os tipos de dados e os nomes dos cabeçalhos — tudo isso é preservado quando você posteriormente importa a tabela para uma planilha Excel.

## Etapa 2: Criar `ImportTableOptions` e habilitar a importação de estilo

Quando você responde **como importar datatable**, a próxima decisão é se deseja o estilo visual (fontes, cores, bordas) que já pode estar definido no `DataTable` de origem. Aspose.Cells fornece a classe `ImportTableOptions` para controle granular. Definir `ImportDataTableStyle = true` copia as informações de estilo para a planilha de destino.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Por que isso importa*: Sem habilitar `ImportDataTableStyle`, as células importadas usariam o estilo padrão da planilha, perdendo qualquer formatação personalizada que você tenha aplicado ao `DataTable`. Essa bandeira é essencial para uma exportação polida.

## Etapa 3: Importar o DataTable para a planilha, incluindo cabeçalhos

Agora você tem tudo que precisa para responder **como importar datatable** para um arquivo Excel. Você cria uma workbook, escolhe uma worksheet e chama `ImportDataTable`. O segundo argumento do método (`true`) indica ao Aspose.Cells que escreva os cabeçalhos das colunas na primeira linha.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Executar `ExportDataTableToExcel("Employees.xlsx")` produz um arquivo `Employees.xlsx` onde a primeira linha contém **Id**, **Name** e **Department**, e cada célula mantém o estilo definido no `DataTable` original.

### Exemplo completo e executável

Abaixo está um programa de console completo e autocontido que demonstra **como importar datatable** e salva o resultado no diretório atual. Copie‑e‑cole em um novo projeto de console e execute.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Saída esperada**  
Ao abrir `Employees.xlsx`, você verá:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Todas as células mantêm o estilo padrão do DataTable (fonte, alinhamento). Se você aplicou estilos personalizados ao `DataTable` antes da importação, esses estilos aparecem identicamente na planilha porque `ImportDataTableStyle` está definido como `true`.

## Armadilhas comuns e dicas de boas práticas

| Problema | Por que acontece | Como evitar |
|----------|------------------|--------------|
| **Cabeçalhos ausentes** | Passar `false` como segundo argumento para `ImportDataTable` ignora os nomes das colunas. | Sempre use `true` quando precisar dos cabeçalhos, ou escreva‑os manualmente antes da importação. |
| **Estilo não transferido** | Esquecer de habilitar `ImportDataTableStyle`. | Defina `ImportDataTableStyle = true` em `ImportTableOptions`. |
| **Tabelas grandes causam lentidão** | Importar milhões de linhas sem paginação. | Importar em lotes ou usar a sobrecarga de `ImportDataTable` com `startRow` para transmitir os dados. |
| **Referência de planilha incorreta** | Usar `workbook.Worksheets[1]` quando existe apenas uma planilha. | Use `workbook.Worksheets[0]` ou crie uma nova planilha com `workbook.Worksheets.Add()`. |
| **Expiração da licença** | Versão de avaliação do Aspose.Cells exibe marca d'água após 30 dias. | Aplique uma licença válida com `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Dica de especialista**: Se precisar aplicar um tema personalizado após a importação, chame `ws.Cells.ApplyStyle(style)` onde `style` é um objeto `Style` que você configura uma vez e reutiliza em todas as linhas.

## Expandindo a solução

Agora que você sabe **como importar datatable**, pode explorar cenários relacionados:

* **Importar várias tabelas** – repita a importação em diferentes worksheets.
* **Formatação condicional** – após a importação, adicione regras com `ws.Cells.ApplyConditionalFormatting`.
* **Exportar para CSV** – use `workbook.Save("file.csv", SaveFormat.Csv)` se for necessário um formato de texto simples.
* **Ler de volta para um DataTable** – use `ws.Cells.ExportDataTable` para verificar a integridade da ida‑e‑volta.

Todas essas extensões se baseiam no padrão central demonstrado acima: recuperar os dados, configurar as opções de importação e chamar um único método do Aspose.Cells.

## Conclusão

Você agora tem uma resposta completa e pronta para produção sobre **como importar datatable** para uma planilha Excel usando C#. O tutorial abordou a recuperação dos dados de origem, a configuração de `ImportTableOptions` com `ImportDataTableStyle` e a execução da importação com `ImportDataTable`. Seguindo o exemplo de código, você preservará cabeçalhos e estilos automaticamente, podendo adaptar o padrão para conjuntos de dados maiores, múltiplas planilhas ou necessidades adicionais de formatação.

Pronto para automatizar seu fluxo de relatórios? Experimente substituir o `DataTable` de exemplo por uma consulta real ao banco de dados, experimente estilos de célula personalizados e integre o método na sua camada de serviço existente. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}