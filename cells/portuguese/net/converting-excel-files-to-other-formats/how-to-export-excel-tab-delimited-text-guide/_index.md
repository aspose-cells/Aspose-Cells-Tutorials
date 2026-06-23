---
category: general
date: 2026-02-26
description: como exportar excel para um arquivo txt delimitado por tabulação usando
  C#. Aprenda a exportar excel como tab, converter excel para txt e exportar excel
  com delimitador em três passos fáceis.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: pt
og_description: como exportar excel para um arquivo txt delimitado por tabulação usando
  C#. este tutorial mostra exportar excel como tabulação, converter excel para txt
  e exportar excel com delimitador.
og_title: como exportar excel – Guia de Texto Delimitado por Tabulação
tags:
- csharp
- excel
- file-conversion
title: Como exportar Excel – Guia de Texto Delimitado por Tabulação
url: /pt/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

etc. Keep them.

Translate paragraphs, bullet points, etc.

Let's produce final output.

Check for any URLs: none besides maybe none.

We need to translate "how to export excel – Complete C# Tutorial" title. Keep "excel" lower case? Keep as is.

Translate "Ever wondered **how to export excel** data into a plain‑text file without losing formatting?" etc.

Make sure to keep bold formatting.

Also keep the note about "Pro tip". Keep "Pro tip" maybe translate "Dica profissional"? But keep formatting. Could translate "Pro tip" to "Dica profissional". Keep bold.

All code block placeholders remain.

Let's craft translation.

Be careful with "ASP.NET"? Not present.

Make sure to keep "ExportTable" etc.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to export excel – Complete C# Tutorial

Já se perguntou **como exportar excel** para um arquivo de texto simples sem perder a formatação? Talvez você precise de um TSV (valores separados por tabulação) rápido para um pipeline de dados, ou esteja alimentando um sistema legado que só lê `.txt`. Seja como for, você não está sozinho — desenvolvedores frequentemente esbarram nessa barreira ao mover dados de planilhas.

A boa notícia? Em apenas três passos simples você pode **exportar excel como tab**‑delimitado, **converter excel para txt**, e ainda escolher um delimitador personalizado caso mude de ideia depois. Abaixo você verá um exemplo C# totalmente executável, por que cada linha importa, e algumas dicas para evitar armadilhas comuns.

> **Dica profissional:** Esta abordagem funciona com a popular biblioteca Aspose.Cells, mas os conceitos se aplicam a qualquer API .NET para Excel que ofereça um método estilo `ExportTable`.

## What You’ll Need

- **.NET 6+** (ou .NET Framework 4.6+). O código compila em qualquer runtime recente.
- **Aspose.Cells for .NET** (versão de avaliação ou licenciada). Instale via NuGet: `dotnet add package Aspose.Cells`.
- Um workbook de entrada chamado `input.xlsx` colocado em uma pasta que você controla.
- Um pouquinho de curiosidade — não é necessário conhecimento profundo dos internals do Excel.

Se já tem tudo isso, vamos direto à solução.

## Step 1 – Load the Workbook You Want to Export

Primeiro criamos um objeto `Workbook` que aponta para o arquivo fonte. Esse objeto representa todo o arquivo Excel, incluindo todas as planilhas, intervalos nomeados e formatações.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Por que isso importa:*  
Carregar o workbook lhe dá acesso à coleção de planilhas (`workbook.Worksheets`). Sem esse objeto você não pode endereçar células, intervalos ou configurações de exportação.  

> **Nota:** Se seu arquivo está em um compartilhamento de rede, preceda com `\\` ou use um caminho UNC — Aspose.Cells lida com isso tranquilamente.

## Step 2 – Configure Export Options (String Values & Tab Delimiter)

Agora informamos à biblioteca como queremos que os dados sejam gravados. Definindo `ExportAsString = true` forçamos que cada célula seja tratada como string simples, eliminando formatos numéricos dependentes de localidade. A parte `Delimiter = "\t"` é o coração do **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Por que isso importa:*  
Se você pular `ExportAsString`, uma célula contendo `12345` pode virar `12,345` em algumas localidades, quebrando analisadores posteriores. O delimitador pode ser trocado por vírgulas, pipes ou qualquer outro caractere caso você decida **exportar excel com delimitador** diferente de tabulação.

## Step 3 – Export a Specific Range to a Text File

Por fim, escolhemos o intervalo que nos interessa (`A1:D10` neste exemplo) e o gravamos em `out.txt`. O método `ExportTable` faz todo o trabalho pesado: lê as células, aplica as opções e grava o resultado no disco.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Depois que isso for executado, você encontrará `out.txt` com conteúdo semelhante a:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Cada coluna está separada por uma **tabulação**, pronta para `awk`, `PowerShell` ou qualquer ferramenta compatível com CSV que respeite tabs.

### Quick Verification

Abra o arquivo gerado em um editor de texto simples (Notepad, VS Code) e confirme:

1. As colunas alinham quando você habilita “Mostrar espaços em branco”.
2. Não aparecem aspas ou vírgulas extras.
3. Todas as células numéricas aparecem exatamente como no Excel (graças ao `ExportAsString`).

Se algo parecer errado, verifique se o workbook fonte não está ocultando linhas/colunas e se você referenciou o índice da planilha correto.

## Common Variations & Edge Cases

### Exporting an Entire Worksheet

Se quiser **exportar excel range** que cubra a planilha inteira, pode usar `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Using a Different Delimiter

Trocar a tabulação por pipe (`|`) é tão simples quanto mudar uma linha:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Isso satisfaz o cenário **export excel with delimiter** sem reescrever nenhum outro código.

### Handling Large Files (> 100 MB)

Para workbooks massivos, faça o streaming da exportação para evitar carregar tudo na memória:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Converting Multiple Sheets in One Pass

Se precisar **converter excel para txt** de várias planilhas, itere sobre elas:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Cada planilha gera seu próprio arquivo TSV — útil para jobs em lote.

## Full Working Example (Copy‑Paste Ready)

Abaixo está o programa completo, pronto para compilar. Basta substituir os caminhos de arquivo pelos seus.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Saída esperada:** Um arquivo chamado `out.txt` onde cada coluna está separada por um caractere de tabulação, e cada valor de célula aparece exatamente como no Excel.

## Frequently Asked Questions

- **Isso funciona com arquivos .xls?**  
  Sim. Aspose.Cells detecta o formato automaticamente, então você pode apontar `Workbook` para um `.xls` antigo e o mesmo código funciona.

- **E se meus dados contiverem tabs?**  
  Tabs dentro de uma célula serão preservadas, o que pode quebrar analisadores TSV. Nesse caso, considere mudar para um delimitador pipe (`|`) atualizando `exportOptions.Delimiter`.

- **Posso exportar fórmulas ao invés de valores?**  
  Defina `exportOptions.ExportAsString = false` e use a sobrecarga de `ExportTableOptions` que inclui `ExportFormula = true`. A saída conterá o texto bruto da fórmula.

- **Existe como pular linhas ocultas?**  
  Sim. Defina `exportOptions.ExportHiddenRows = false` (o padrão é `true`). Linhas ocultas serão omitidas do arquivo final.

## Conclusion

Agora você tem uma receita sólida e pronta para produção de **como exportar excel** como arquivo de texto delimitado por tabulação, como **exportar excel como tab**, e como **converter excel para txt** com controle total sobre delimitadores e seleção de intervalos. Ao aproveitar o método `ExportTable` da Aspose.Cells você evita a construção manual de CSV, preserva a fidelidade dos dados e mantém seu código limpo.

Pronto para o próximo desafio? Experimente:

- Exportar diretamente para um `MemoryStream` para APIs web.  
- Adicionar dinamicamente uma linha de cabeçalho baseada no conteúdo da primeira linha.  
- Integrar esta rotina em uma Azure Function que monitora um bucket de storage para novos uploads de Excel.

Teste, ajuste o delimitador e deixe os dados fluírem onde precisar. Happy coding!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}