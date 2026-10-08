---
category: general
date: 2026-03-21
description: Como exportar dados do Excel com nomes de colunas, preservar o formato
  numérico e ler linhas específicas usando Aspose.Cells em C#. Aprenda a ler a planilha
  do Excel e exportar linhas específicas de forma eficiente.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: pt
og_description: Como exportar dados do Excel com nomes de colunas, preservar o formato
  numérico e ler linhas específicas usando Aspose.Cells. Um exemplo completo e executável
  para desenvolvedores C#.
og_title: Como Exportar Dados do Excel em C# – Guia Completo de Programação
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Como Exportar Dados do Excel em C# – Guia Passo a Passo
url: /pt/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Dados do Excel em C# – Guia Completo de Programação

Já se perguntou **como exportar excel** dados sem perder a formatação original? Talvez você tenha tentado um rápido copiar‑colar e acabou com datas aparecendo como “44728” ou cabeçalhos de coluna ausentes. Isso é frustrante, não é? Neste tutorial você verá uma maneira limpa, de ponta a ponta, de ler uma planilha Excel, preservar o formato numérico, exportar com nomes de coluna e até selecionar apenas as linhas que você precisa.

Usaremos a biblioteca Aspose.Cells porque ela oferece controle detalhado sobre as opções de exportação. Ao final deste guia você terá um trecho reutilizável que pode ser inserido em qualquer projeto .NET, e entenderá por que cada opção é importante. Nenhuma documentação externa necessária — tudo o que você precisa está aqui.

---

## O que Você Vai Aprender

- **Read Excel worksheet** na memória com Aspose.Cells.
- **Export specific rows** (por exemplo, linhas 0‑49) mantendo os nomes das colunas.
- **Preserve number format** para que moedas, datas e percentuais permaneçam intactos.
- Como **export with column names** e incluir comentários de célula se precisar.
- Um exemplo completo, pronto‑para‑executar em C#, além de dicas para armadilhas comuns.

### Pré-requisitos

- .NET 6.0 ou posterior (o código funciona também com .NET Framework 4.6+).
- Aspose.Cells para .NET instalado via NuGet (`Install-Package Aspose.Cells`).
- Um arquivo Excel (`input.xlsx`) colocado em uma pasta que você possa referenciar.

> **Dica profissional:** Se você estiver em um pipeline CI, considere obter o pacote NuGet de um feed privado para evitar surpresas de licenciamento.

---

## Etapa 1 – Instalar Aspose.Cells e Adicionar Namespaces

Primeiro, certifique‑se de que o pacote Aspose.Cells está no seu projeto. Abra o Package Manager Console e execute:

```powershell
Install-Package Aspose.Cells
```

Em seguida, adicione as diretivas `using` necessárias no topo do seu arquivo C#:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Essas importações dão acesso a `Workbook`, `Worksheet`, `ExportTableOptions` e `DataTable` — os componentes principais para **reading an Excel worksheet** e exportar dados.

---

## Etapa 2 – Carregar a Pasta de Trabalho (Read the Excel File)

Agora realmente **read the Excel worksheet**. O construtor `Workbook` recebe um caminho para o arquivo, e o Aspose.Cells lidará tanto com formatos `.xlsx` quanto com os mais antigos `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Por que isso importa:** Carregar a pasta de trabalho uma vez e reutilizar o mesmo objeto `Worksheet` é muito mais eficiente do que abrir o arquivo repetidamente, especialmente para planilhas grandes.

---

## Etapa 3 – Configurar Opções de Exportação (Preserve Number Format & Column Names)

É aqui que dizemos ao Aspose.Cells *como* exportar. A classe `ExportTableOptions` nos permite ajustar finamente a saída. Ativaremos três flags:

1. `ExportAsString = true` – força cada célula a se tornar uma string, o que garante que os números mantenham sua representação visual.
2. `IncludeCellComments = true` – copia quaisquer comentários anexados às células (útil para documentação).
3. `PreserveNumberFormat = true` – mantém o formato numérico original (símbolos de moeda, padrões de data, etc.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Caso extremo:** Se você definir `ExportAsString` como `false` mas ainda quiser manter os formatos numéricos, pode acabar com valores numéricos brutos (por exemplo, 44728 para uma data). Manter ambas as flags ativadas evita essa surpresa.

---

## Etapa 4 – Obter a Primeira Worksheet (Read Excel Worksheet)

A maioria dos arquivos simples tem os dados que você precisa na primeira planilha, então a buscaremos por índice. Se precisar de outra planilha, basta substituir `0` pelo índice zero‑based apropriado ou usar `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Por que é útil:** Acessar diretamente o objeto worksheet lhe dá controle total sobre sua coleção `Cells`, o que é essencial para **export specific rows** mais adiante.

---

## Etapa 5 – Exportar um Intervalo de Células (Export Specific Rows)

Agora o coração do tutorial: exportar linhas 0‑49 e colunas 0‑4 (ou seja, as primeiras 50 linhas e as primeiras cinco colunas) para um `DataTable`. Também pediremos ao Aspose.Cells que inclua os nomes das colunas como a primeira linha do `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### O Que Isso Faz

- **`startRow: 0`** – começa no topo da planilha.
- **`totalRows: 50`** – captura as primeiras 50 linhas (ou seja, **export specific rows**).
- **`totalColumns: 5`** – limita a exportação às primeiras cinco colunas.
- **`includeColumnNames: true`** – garante que os cabeçalhos de coluna do `DataTable` correspondam à linha de cabeçalho do Excel, atendendo ao requisito de **export with column names**.
- **`exportOptions`** – aplica as configurações da Etapa 3, de modo que seus valores numéricos permaneçam como “$1,234.56” em vez de “1234.56”.

---

## Etapa 6 – Verificar a Exportação (Como o Resultado Se Parece)

Vamos imprimir as primeiras linhas no console para que você veja que a formatação sobreviveu.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Saída esperada (exemplo):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Observe como as datas aparecem no formato `MM/dd/yyyy` e a moeda mantém o símbolo `$` — graças ao **preserve number format**.

---

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Correção |
|-------|----------------|-----|
| Dates turn into large numbers | `ExportAsString` left `false` | Keep `ExportAsString = true` or convert cells manually |
| Missing column headers | `includeColumnNames` set to `false` | Set it to `true` when you need **export with column names** |
| Comments disappear | `IncludeCellComments` not enabled | Turn on `IncludeCellComments` in `ExportTableOptions` |
| Exporting the wrong sheet | Using `Worksheets[0]` on a multi‑sheet file | Specify the sheet name: `workbook.Worksheets["Data"]` |
| Out‑of‑range exception | `totalRows` exceeds actual rows | Use `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bônus: Exportar a Planilha Inteira Enquanto Ainda Preserva Formatos

Se mais tarde decidir que precisa da planilha inteira, basta substituir `totalRows` e `totalColumns` pelas dimensões máximas da planilha:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Agora você tem uma rotina de **read excel worksheet** que funciona para qualquer tamanho, enquanto ainda **preserving number format** e **exporting with column names**.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um aplicativo console. Ele inclui todas as etapas, importações e uma simples impressão de verificação.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Salve isso como `Program.cs`, execute `dotnet run`, e você deverá ver a pré‑visualização formatada no seu terminal.

---

## Conclusão

Acabamos de percorrer **how to export excel** dados usando Aspose.Cells, cobrindo tudo desde o carregamento da pasta de trabalho até a preservação do formato numérico, exportação com nomes de coluna e limitação da exportação a linhas específicas. O código é autocontido, totalmente executável e inclui salvaguardas práticas para os casos extremos mais comuns.

Pronto para o próximo desafio? Tente exportar diretamente para um CSV mantendo ainda a formatação numérica original, ou envie o `DataTable` para um contexto Entity Framework Core para inserções em massa no banco de dados. Ambos os cenários se baseiam nos mesmos fundamentos que abordamos aqui.

Se você achou este guia útil

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}