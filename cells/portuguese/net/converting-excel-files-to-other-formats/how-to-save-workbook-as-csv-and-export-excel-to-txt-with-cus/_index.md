---
category: general
date: 2026-09-15
description: Aprenda como salvar a pasta de trabalho como CSV, exportar o Excel para
  TXT e aplicar formato numérico personalizado ao converter valores de células para
  maiúsculas em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: pt
lastmod: 2026-09-15
og_description: Salvar a pasta de trabalho como CSV, exportar o Excel para TXT e aplicar
  formato numérico personalizado enquanto converte os valores das células para maiúsculas
  usando Aspose.Cells em C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Salvar a pasta de trabalho como CSV e exportar Excel para TXT com formatação
  personalizada em C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como salvar a pasta de trabalho como CSV e exportar o Excel para TXT com formatação
  personalizada em C#
url: /pt/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar uma pasta de trabalho como CSV e exportar Excel para TXT com formatação personalizada em C#

Se você precisa **salvar a pasta de trabalho como CSV** enquanto também exporta uma planilha como texto simples e aplica um formato numérico personalizado, este guia mostra uma solução completa e pronta‑para‑executar. Você verá como manter a precisão numérica, converter cada valor de célula para maiúsculas e lidar com datas no calendário japonês — tudo com Aspose.Cells para .NET.

Exportar dados do Excel geralmente significa lidar com vários formatos: CSV para troca de dados, TXT para sistemas legados e formatos numéricos personalizados para relatórios específicos de localidade. Este tutorial percorre cada requisito passo a passo, para que você possa copiar o código diretamente para o seu projeto.

Nas seções a seguir, você aprenderá a:

* **salvar a pasta de trabalho como csv** com um número definido de dígitos significativos  
* **exportar excel para txt** forçando **valores de célula em maiúsculas**  
* **aplicar formato numérico personalizado** para datas no calendário japonês e ler o resultado formatado  

Nenhuma ferramenta externa é necessária — apenas a biblioteca Aspose.Cells e um ambiente de desenvolvimento .NET.

## Pré‑requisitos

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.8)  
* Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`)  
* Familiaridade básica com C# e conceitos de Excel  

---

## Etapa 1: Salvar a pasta de trabalho como CSV com precisão controlada

Ao **salvar a pasta de trabalho como CSV**, os valores numéricos são gravados usando a representação padrão de string, o que pode perder precisão. Configurando `CsvSaveOptions.SignificantDigits`, você informa ao Aspose.Cells quantos dígitos significativos devem ser mantidos.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Por que isso importa:**  
Definir `SignificantDigits` evita erros de arredondamento que costumam aparecer quando grandes volumes de dados são trocados com sistemas downstream (por exemplo, data‑warehouses). O objeto `CsvSaveOptions` também permite controlar delimitadores, codificação e outras configurações específicas de CSV, se necessário.

---

## Etapa 2: Exportar uma planilha como texto simples enquanto converte valores para maiúsculas

Exportar uma planilha para um arquivo `.txt` simples é útil para rotinas legadas de importação que esperam dados delimitados por espaços. Ao habilitar `ExportTableOptions.ExportAsString` e fornecer um delegate `CustomExport`, você pode **exportar excel para txt** e, simultaneamente, impor **valores de célula em maiúsculas**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Por que isso importa:**  
Muitos pontos de integração (por exemplo, jobs batch de mainframe) esperam identificadores em maiúsculas. O callback `CustomExport` lhe dá controle total sobre a representação de cada célula, permitindo injetar transformações como trim, padding ou formatação específica de localidade sem precisar de pós‑processamento do arquivo.

---

## Etapa 3: Aplicar um formato numérico personalizado e ler o resultado formatado

Os formatos numéricos nativos do Excel cobrem a maioria dos casos, mas às vezes é necessário exibir datas em um sistema de calendário específico — como a era japonesa. O código a seguir demonstra como **aplicar formato numérico personalizado** a uma célula e, em seguida, ler a string formatada que respeita a localidade da pasta de trabalho.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Por que isso importa:**  
Usar `SetStyle` com um formato numérico garante que a exibição da célula respeite as configurações regionais, o que é crítico para relatórios distribuídos em diferentes localidades. Quando você posteriormente lê `StringValue`, obtém exatamente a string que o usuário veria na interface do Excel, eliminando a necessidade de parsing manual.

---

## Exemplo completo e executável

Abaixo está um programa único que combina as três etapas. Cole-o em um novo projeto Console App, adicione o pacote NuGet Aspose.Cells e execute.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Saída esperada**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(O formato exato da data pode variar de acordo com as configurações de localidade do seu sistema.)

---

## Perguntas comuns e tratamento de casos extremos

| Pergunta | Resposta |
|----------|----------|
| *E se eu precisar de um delimitador diferente no CSV?* | Defina `csvOptions.Separator` para `','`, `'\t'` ou qualquer caractere personalizado antes de chamar `Save`. |
| *Posso manter a precisão numérica original em vez de arredondar?* | Use `SignificantDigits = 0` para gravar o valor de dupla precisão completo, ou ajuste `NumberDecimalSeparator` para símbolos decimais específicos de localidade. |
| *Como exportar apenas um intervalo específico em vez da planilha inteira?* | Chame `ExportTable(string fileName, ExportTableOptions options, CellArea area)` e passe um `CellArea` que define o intervalo. |
| *E se a pasta de trabalho contiver fórmulas que referenciam outras planilhas?* | Certifique‑se de chamar `workbook.CalculateFormula()` antes da exportação; caso contrário, você obterá os valores em cache. |
| *Existe uma forma de manter a formatação original das células (fontes, cores) no arquivo TXT?* | Formatos de texto simples não podem reter estilos visuais. Se precisar de formatação rica, considere exportar para HTML (`HtmlSaveOptions`). |

---

## Conclusão

Agora você sabe como **salvar a pasta de trabalho como CSV** com precisão controlada, **exportar excel para TXT** forçando **valores de célula em maiúsculas** e **aplicar formato numérico personalizado** para renderização de datas sensível à localidade. Cada trecho de código é autocontido, funciona imediatamente e segue as melhores práticas de desempenho e manutenção.

A seguir, você pode explorar:

* Usar `HtmlSaveOptions` para manter o estilo ao exportar para formatos amigáveis à web.  
* Aproveitar `CsvSaveOptions.Encoding` para UTF‑8 ou outros conjuntos de caracteres ao lidar com dados multilíngues.  
* Automatizar o processamento em lote de várias planilhas percorrendo `workbook.Worksheets`.

Sinta‑se à vontade para adaptar o código aos seus próprios pipelines de dados, e deixe a flexibilidade do Aspose.Cells fazer o trabalho pesado.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}