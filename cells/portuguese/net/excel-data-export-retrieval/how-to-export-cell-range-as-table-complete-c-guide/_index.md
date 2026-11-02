---
category: general
date: 2026-07-13
description: Como exportar intervalo de células como tabela usando C# e ExportTableOptions.
  Aprenda passo a passo a configuração da planilha, formatação e exportação da tabela.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: pt
lastmod: 2026-07-13
og_description: Como exportar um intervalo de células como tabela em C# com ExportTableOptions.
  Siga este guia para formatar células, criar uma pasta de trabalho e exportar uma
  tabela sem esforço.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Como Exportar Intervalo de Células como Tabela – Guia Completo em C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Como Exportar Intervalo de Células como Tabela – Guia Completo de C#
url: /pt/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Intervalo de Células como Tabela – Guia Completo em C#

Já se perguntou **como exportar intervalo de células como tabela** sem perder a cabeça com peculiaridades de formatação? Você não está sozinho. Seja alimentando dados em um pipeline de relatórios ou apenas precisando de um despejo rápido no estilo CSV, dominar o processo de exportação pode economizar horas de cópia‑e‑cola manual.

Neste tutorial vamos percorrer passo a passo como pegar uma célula numérica, aplicar notação científica e exportá‑la como tabela usando **ExportTableOptions**. Ao final você terá um trecho de código executável, entenderá o *porquê* de cada chamada e saberá como ajustar o código para intervalos maiores ou formatos diferentes.

## Pré‑requisitos

- .NET 6 ou superior (a API funciona da mesma forma no .NET Framework 4.7+)
- Aspose.Cells for .NET instalado (`Install-Package Aspose.Cells`)
- Noções básicas de sintaxe C#; não é necessário conhecimento profundo do Excel

Tem tudo isso? Ótimo—vamos começar.

## Passo 1: Configurar Opções de Exportação – Como Exportar Intervalo de Células como Tabela

A primeira coisa que você precisa é uma instância de **ExportTableOptions** que indique à biblioteca como tratar o conteúdo das células. Sem isso, a exportação usa valores numéricos brutos, o que pode quebrar consumidores posteriores que esperam texto.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Por que isso importa:**  
- `ExportAsString = true` força a biblioteca a gravar o texto exibido na célula, não o double subjacente.  
- `CustomFormat` permite impor uma **exportação em notação científica**, útil ao lidar com números muito grandes ou muito pequenos.

> **Dica profissional:** Se precisar de um formato de data ou moeda, substitua `"0.00E+00"` por `"yyyy‑MM‑dd"` ou `"$#,##0.00"` respectivamente.

## Passo 2: Criar um Workbook e Obter a Primeira Worksheet – Manipulação de Workbook e Worksheet

Um **Workbook** representa o arquivo Excel completo, enquanto uma **Worksheet** é uma única aba. Para uma exportação simples, usaremos a primeira planilha, que está sempre presente no índice 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Por que isso importa:**  
Criar um `Workbook` novo garante um ponto de partida limpo—sem estilos ocultos ou dados residuais que possam atrapalhar. Acessar `Worksheets[0]` é a forma mais rápida de obter a planilha ativa sem se preocupar com nomes de abas.

## Passo 3: Preencher a Célula de Destino – Formatação de Valor da Célula C#

Agora inserimos um valor numérico na célula **A1** (linha 0, coluna 0). O valor escolhido tem muitas casas decimais deliberadamente, para que você veja a notação científica em ação.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Por que isso importa:**  
Chamar `PutValue` infere automaticamente o tipo de dado da célula. Como exportaremos como string, o double bruto será convertido usando o formato definido anteriormente, resultando em um tidy `"1.23E+04"`.

## Passo 4: Exportar o Intervalo de Células Definido como Tabela – Exportando o Intervalo de Células como Tabela

Com as opções e os dados prontos, o passo final é instruir o Aspose.Cells a gravar o intervalo. O método `ExportTable` espera a linha/coluna inicial, o tamanho do intervalo e o objeto de opções que criamos.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Por que isso importa:**  
- `totalRows = 1` e `totalColumns = 1` limitam a exportação a uma única célula, mas você pode expandir esses números para cobrir blocos maiores (ex.: `5, 3` para um intervalo de 5 linhas × 3 colunas).  
- O método grava os dados em uma estrutura de tabela interna que pode ser salva como CSV, HTML ou até mesmo transmitida diretamente a um cliente.

### Salvando o Resultado (Opcional)

Se quiser persistir a tabela exportada no disco, pode gravá‑la em um arquivo CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Executar o código acima gerará um arquivo contendo:

```
1.23E+04
```

## Casos de Borda & Variações Comuns

| Situação | O que Alterar | Razão |
|-----------|----------------|--------|
| **Exportando várias linhas** | Ajuste `totalRows` e faça loop sobre as linhas, se necessário | Permite exportação em lote sem invocar `ExportTable` repetidamente |
| **Preservando fórmulas** | Defina `ExportAsString = false` | Mantém a fórmula original em vez do valor exibido |
| **Delimitadores diferentes** | Use a sobrecarga `ExportTableToCSV(..., ',', ...)` | Troca de valores separados por vírgula para tabulação ou pipe |
| **Planilhas grandes** | Transmita a exportação para evitar `OutOfMemoryException` | Funciona bem para >10 000 linhas |

## Exemplo Completo Funcionando

Abaixo está o programa completo, pronto para copiar e colar. Ele compila em qualquer projeto console .NET que referencia Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Saída esperada:**  
Um arquivo chamado `ExportedTable.csv` contendo uma única linha:

```
1.23E+04
```

Se você abrir o CSV em um editor de texto verá a notação científica aplicada exatamente como definida.

## Conclusão

Cobremos **como exportar intervalo de células como tabela** do início ao fim: configurando `ExportTableOptions`, criando um `Workbook`, inserindo dados e, finalmente, invocando `ExportTable`. Ao entender cada peça, você pode escalar a abordagem para intervalos maiores, formatos diferentes ou até integrá‑la a uma API web que sirva dados derivados do Excel em tempo real.

Olhando adiante, você pode querer explorar:

- **ExportTableToHTML** para pré‑visualizações web  
- **ExportTableToDataTable** para alimentar diretamente pipelines ADO.NET  
- Formatos **personalizados avançados** para datas, moedas ou percentuais  

Experimente essas opções e transforme uma simples exportação de célula em um motor versátil de entrega de dados. Tem dúvidas ou um caso de uso curioso? Deixe um comentário abaixo—bom código!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui código completo e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}