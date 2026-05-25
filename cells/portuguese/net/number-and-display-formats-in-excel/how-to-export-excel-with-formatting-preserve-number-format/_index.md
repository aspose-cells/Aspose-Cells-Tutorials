---
category: general
date: 2026-03-22
description: Como exportar Excel com formatação e preservar o formato de número. Aprenda
  a converter intervalo do Excel, obter o resultado da fórmula e exportar Excel com
  formatação usando Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: pt
og_description: Como exportar Excel com formatação e preservar o formato numérico.
  Guia passo a passo para converter intervalo do Excel, obter o resultado da fórmula
  e exportar Excel com formatação em C#.
og_title: Como Exportar Excel com Formatação – Preservar Formato de Número
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como Exportar o Excel com Formatação – Preservar o Formato de Número
url: /pt/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Excel com Formatação – Preservar Formato de Número

Já se perguntou **como exportar Excel** mantendo a aparência de cada célula exatamente como você a vê na planilha? Talvez você precise enviar um relatório para um cliente, alimentar um controle de grade, ou apenas armazenar os valores em um banco de dados. O ponto crítico costuma ser a perda da formatação numérica ou as fórmulas se transformarem em strings brutas.  

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar em C# que **preserva o formato de número**, **converte um intervalo do Excel** para um `DataTable`, **obtém o resultado da fórmula**, e finalmente **exporta Excel com formatação** usando Aspose.Cells. Ao final você terá um único método que pode ser inserido em qualquer projeto e chamado com uma referência à planilha.

> **Pré‑visualização rápida:** o código cria uma pasta de trabalho, grava um valor e uma fórmula, instrui o Aspose.Cells a exportar as células como strings formatadas e imprime `123.456 | 246.912` – exatamente o que você esperaria ver no Excel.

---

## O que Você Precisa

- **Aspose.Cells for .NET** (a versão de avaliação gratuita funciona bem para aprendizado)
- .NET 6.0 ou superior (a API é a mesma no .NET Framework)
- Um ambiente básico de desenvolvimento C# (Visual Studio, VS Code, Rider… você escolhe)

Nenhum pacote NuGet extra além do Aspose.Cells é necessário. Se ainda não o instalou, execute:

```bash
dotnet add package Aspose.Cells
```

---

## Etapa 1 – Criar uma Pasta de Trabalho e Gravar Valores (incluindo uma fórmula)

Primeiro criamos uma nova pasta de trabalho e inserimos um valor numérico em **A1**. Em seguida adicionamos uma fórmula simples em **B1** que multiplica a primeira célula por dois. Isso prepara o cenário para demonstrar **obter resultado da fórmula** mais adiante.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Por que isso importa:**  
- `PutValue` armazena o número bruto, enquanto `PutFormula` armazena o cálculo.  
- Aspose.Cells mantém a fórmula **ativa**, de modo que quando pedirmos o valor da célula obteremos realmente `246.912`, e não a string `"=A1*2"`.

---

## Etapa 2 – Instruir o Aspose.Cells a Exportar Valores como Strings Formatadas

Se você simplesmente chamar `ExportDataTable` com as configurações padrão, as células numéricas serão retornadas como seus valores subjacentes `double`. Isso remove separadores de milhar, símbolos de moeda ou casas decimais personalizadas que você possa ter definido. A classe `ExportTableOptions` nos permite **preservar o formato de número** e **exportar como string**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Ponto chave:** `ExportNumberFormat = true` é a bandeira que faz a **preservação do formato de número** funcionar. Sem ela você veria `"123.456"` e `"246.912"` como números brutos, o que pode parecer aceitável no código, mas não quando você cola os dados em uma UI que espera a mesma formatação do Excel.

---

## Etapa 3 – Imprimir os Dados Exportados (Verificação)

Agora que temos um `DataTable` cheio de strings formatadas, vamos despejar o conteúdo no console. Isso também demonstra que conseguimos **obter o resultado da fórmula** sem avaliar a fórmula manualmente.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Executar o programa imprime:

```
123.456 | 246.912
```

Observe como a segunda coluna mostra o **resultado da fórmula**, não o texto da fórmula. Isso é exatamente o que você precisa ao **exportar Excel com formatação** para processamento posterior.

---

## Etapa 4 – Convertendo Intervalos Maiores do Excel (Opcional)

O exemplo acima trata de um pequeno recorte `A1:B1`, mas cenários reais frequentemente exigem exportar tabelas inteiras. O mesmo método funciona para qualquer bloco retangular – basta ajustar os argumentos `firstRow`, `firstColumn`, `totalRows` e `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Dica de especialista:** Se sua planilha já possui uma linha de cabeçalho, defina `includeColumnNames` como `true`. O Aspose.Cells usará a primeira linha do intervalo como nomes de coluna, o que é útil quando você posteriormente vincular o `DataTable` a uma grade de UI.

---

## Etapa 5 – Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| **Números perdem vírgulas ou símbolos de moeda** | `ExportAsString` está `false` ou `ExportNumberFormat` foi omitido | Defina ambos `ExportAsString = true` **e** `ExportNumberFormat = true`. |
| **Células de fórmula retornam o texto da fórmula** | Você não chamou `CalculateFormula` antes da exportação (necessário apenas se a pasta de trabalho não estiver configurada para auto‑calcular) | Ative o auto‑cálculo (`workbook.CalculateFormula()`) ou confie em `ExportAsString`, que força a avaliação. |
| **Cabeçalhos aparecem como linhas de dados** | `includeColumnNames` definido como `false` enquanto seu intervalo inclui uma linha de cabeçalho | Defina `includeColumnNames = true` para tratar a primeira linha como nomes de coluna. |
| **Intervalos grandes causam pressão de memória** | Exportar a planilha inteira de uma vez carrega tudo na memória | Exporte em blocos (por exemplo, 500 linhas por vez) e mescle os `DataTable`s se necessário. |

---

## Etapa 6 – Exemplo Completo (Pronto para Copiar‑Colar)

Abaixo está o programa inteiro, desde as declarações `using` até o `Main`. Cole em um aplicativo console e pressione **F5** – você verá a saída formatada instantaneamente.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Saída esperada**

```
123.456 | 246.912

Press any key to exit...
```

Esse é todo o fluxo de **como exportar Excel**, com formatação intacta, resultados de fórmula avaliados e um `DataTable` limpo pronto para qualquer consumidor .NET.

---

## Conclusão

Cobremos tudo o que você precisa saber sobre **como exportar Excel** mantendo o **formato de número**, **convertendo um intervalo do Excel** para um `DataTable`, e **obtendo resultados de fórmula** sem parsing extra. A chave está na configuração `ExportTableOptions` – uma vez que você define `ExportAsString` e `ExportNumberFormat` como `true`, o Aspose.Cells faz o trabalho pesado por você.

A partir daqui você pode:

- Inserir o `DataTable` em um `DataGrid` WPF ou em uma view ASP.NET MVC.  
- Gravar a tabela em um arquivo CSV mantendo a representação visual exata.  
- Estender a abordagem para múltiplas planilhas ou intervalos dinâmicos.

Sinta‑se à vontade para experimentar diferentes formatos (moeda, porcentagem) e blocos de dados maiores. Se encontrar alguma particularidade, volte à tabela de **armadilhas comuns** – ela cobre os contratempos mais frequentes ao **exportar Excel com formatação**.

Bom código, e que suas planilhas exportadas estejam sempre tão polidas quanto as originais!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}