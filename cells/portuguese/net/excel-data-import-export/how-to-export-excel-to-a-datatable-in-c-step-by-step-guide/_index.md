---
category: general
date: 2026-03-18
description: Como exportar dados do Excel para um DataTable em C# com código que manipula
  células específicas, converte Excel para DataTable e formata números. Aprenda a
  exportar células específicas e muito mais.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: pt
og_description: Como exportar dados do Excel para um DataTable em C#. Este tutorial
  mostra como exportar células específicas, converter Excel para DataTable e formatar
  números com facilidade.
og_title: Como Exportar Excel para um DataTable em C# – Guia Completo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Como Exportar Excel para um DataTable em C# – Guia Passo a Passo
url: /pt/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Excel para um DataTable em C# – Guia Passo a Passo

Já se perguntou **como exportar Excel** para um `DataTable` sem perder a formatação? Você não está sozinho—desenvolvedores precisam constantemente extrair uma parte de uma planilha para a memória para relatórios, validações ou operações de inserção em massa. A boa notícia? Com algumas linhas de C# você pode exportar um intervalo preciso (por exemplo *A1:F11*), forçar que cada célula seja tratada como string e ainda aplicar um formato numérico personalizado.

Neste tutorial vamos cobrir tudo o que você precisa saber: desde o carregamento da pasta de trabalho, configuração de **exportar células específicas**, conversão do intervalo para um `DataTable` e tratamento de casos de borda como linhas vazias ou números dependentes de localidade. Ao final, você terá um método reutilizável que funciona com cenários **excel to datatable c#** em código de produção.

> **Pré‑requisitos** – Você precisará da biblioteca Aspose.Cells for .NET (ou qualquer API similar que ofereça `ExportDataTable`). O exemplo assume .NET 6+, mas os conceitos se aplicam a versões anteriores também.

---

## O que Você Vai Aprender

- Como **converter Excel para DataTable** usando Aspose.Cells.  
- Exportar um intervalo personalizado (`excel range to datatable`) tratando todos os valores como strings.  
- Aplicar um formato numérico de duas casas decimais (`#,#00.00`) durante a exportação.  
- Armadilhas comuns (linhas nulas, colunas ocultas) e como evitá‑las.  
- Um exemplo de código pronto‑para‑copiar e totalmente executável.

---

## Pré‑requisitos e Configuração

Antes de mergulharmos no código, certifique‑se de que você tem:

1. **Aspose.Cells for .NET** instalado via NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Um arquivo Excel (`input.xlsx`) colocado em uma pasta que você possa referenciar, por exemplo `YOUR_DIRECTORY/input.xlsx`.  
3. Um projeto que tenha como alvo .NET 6 ou superior (as instruções `using` mostradas abaixo funcionam imediatamente).

> **Dica de especialista:** Se você estiver usando outra biblioteca (ex.: EPPlus ou ClosedXML), o conceito permanece o mesmo—carregue a pasta de trabalho, selecione um intervalo e chame um método que retorne um `DataTable`.

---

## Etapa 1: Carregar a Pasta de Trabalho e Obter a Primeira Planilha

A primeira coisa que você precisa é um objeto `Workbook` que represente seu arquivo Excel. Depois de obtê‑lo, você pode acessar qualquer planilha por índice ou nome.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Por que isso importa:** Carregar a pasta de trabalho logo no início permite inspecionar sua estrutura (planilhas ocultas, proteção) antes de decidir quais células exportar. Se o arquivo for grande, considere usar `LoadOptions` para transmitir apenas as partes necessárias.

---

## Etapa 2: Configurar Opções de Exportação – Tratar Todos os Valores como Strings

Quando você exporta dados para processamento posterior (ex.: inserção em massa no SQL), costuma querer uma **representação de string consistente**. Isso evita erros de incompatibilidade de tipos mais tarde.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explicação:**  
- `ExportAsString = true` indica ao Aspose.Cells que ignore o tipo nativo da célula e retorne o texto formatado.  
- `NumberFormat = "#,##0.00"` garante que números como `1234.5` se tornem `"1,234.50"`—útil para relatórios financeiros.

Se precisar dos tipos de dados originais, basta definir `ExportAsString` como `false` e fazer a conversão manualmente.

---

## Etapa 3: Exportar um Intervalo Específico (A1:F11) para um DataTable

Agora vem o núcleo de **exportar células específicas**. O método `ExportDataTable` recebe índices de linha/coluna de início e fim (baseados em zero) além de uma bandeira para inclusão de cabeçalho.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**O que você obtém:** Um `DataTable` com 11 linhas (incluindo o cabeçalho) e 6 colunas (`A`‑`F`). Todos os valores são strings formatadas de acordo com `exportOptions`.

---

## Etapa 4: Verificar o Resultado – Imprimir no Console

É sempre uma boa prática validar a saída antes de passar a tabela para outro componente.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Você deverá ver algo como:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Observe como as colunas numéricas exibem duas casas decimais, exatamente como especificamos.

---

## Exemplo Completo Funcional (Pronto para Copiar e Colar)

A seguir está o programa completo que une tudo. Cole em um novo projeto de console, ajuste o caminho do arquivo e execute—nenhuma configuração adicional é necessária.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Principais aprendizados do código:**  

- O objeto `ExportTableOptions` é reutilizável; você pode passá‑lo para múltiplas chamadas `ExportDataTable` se precisar exportar vários intervalos.  
- A indexação começa em **0**, portanto `A1` corresponde a `(0,0)`.  
- Definir `includeColumnNames` como `true` usa automaticamente a primeira linha como cabeçalhos de coluna—ideal para operações posteriores com `DataTable`.

---

## Tratamento de Casos de Borda & Perguntas Frequentes

### E se a planilha tiver linhas ou colunas ocultas?

O Aspose.Cells respeita a visibilidade por padrão. Se precisar exportar dados ocultos, defina `exportOptions.ExportHiddenRows = true` e `ExportHiddenColumns = true`.

### Meu arquivo Excel contém fórmulas—receberei os valores calculados?

Sim. Por padrão, `ExportDataTable` retorna o **valor exibido** (o resultado da fórmula). Se quiser o texto bruto da fórmula, defina `exportOptions.ExportFormulas = true`.

### Como pular linhas completamente vazias?

Após a exportação, você pode limpar o `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Posso exportar um intervalo não contíguo (ex.: A1:B5 e D1:E5)?

O Aspose.Cells não suporta intervalos disjuntos em uma única chamada. Em vez disso, exporte cada bloco separadamente e depois mescle os `DataTable`s resultantes manualmente.

---

## Dicas de Performance

- **Reutilize `ExportTableOptions`** para múltiplas exportações; criar uma nova instância a cada vez gera um overhead insignificante, mas polui o código.  
- **Transmita arquivos grandes** usando `LoadOptions` para evitar carregar a pasta de trabalho inteira na memória.  
- **Evite `DataTable`** se precisar apenas de uma exportação rápida para CSV—`ExportDataTable` é conveniente, mas não é a opção mais eficiente em memória para planilhas massivas.

---

## Conclusão

Percorremos **como exportar Excel** para um `DataTable` controlando a formatação, lidando com intervalos de células específicos e garantindo que cada valor chegue como string. O exemplo completo demonstra uma abordagem limpa e pronta para produção que você pode adaptar para **convert excel to datatable**, **export specific cells** ou qualquer cenário **excel range to datatable** que encontrar.

Sinta‑se à vontade para experimentar: altere o intervalo, alterne `ExportAsString` ou direcione o `DataTable` diretamente ao Entity Framework para inserções em massa. O céu é o limite quando você tem essa base sólida.

### Próximos Passos & Tópicos Relacionados

- **Importar DataTable de volta para Excel** – aprenda a operação inversa com `ImportDataTable`.  
- **Inserção em massa de um DataTable no SQL Server** – use `SqlBulkCopy` para carregamentos ultrarrápidos.  
- **Trabalhar com EPPlus ou ClosedXML** – veja como a mesma tarefa se apresenta com bibliotecas alternativas.  
- **Formatação de células na exportação** – explore mais o `ExportTableOptions` para formatos de data, configurações de cultura personalizadas e muito mais.

Tem perguntas ou um caso de uso diferente? Deixe um comentário e vamos manter a conversa rolando. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}