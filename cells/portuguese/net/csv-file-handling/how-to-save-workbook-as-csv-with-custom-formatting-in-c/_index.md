---
category: general
date: 2026-10-20
description: Salvar a pasta de trabalho como CSV com dígitos decimais precisos, valores
  entre aspas e formato de data da era japonesa usando Aspose.Cells para .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: pt
lastmod: 2026-10-20
og_description: Salve a pasta de trabalho como CSV com controle total sobre decimais,
  aspas e datas da era japonesa. Siga este tutorial passo a passo em C# usando Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Salvar a pasta de trabalho como CSV – guia completo para desenvolvedores
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Como salvar a pasta de trabalho como CSV com formatação personalizada em C#
url: /pt/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar uma pasta de trabalho como CSV com formatação personalizada em C#

Se você precisa **salvar uma pasta de trabalho como CSV** controlando a precisão decimal, citando valores e lidando com datas do calendário japonês, este tutorial mostra como fazer isso com Aspose.Cells para .NET. Você aprenderá a **exportar Excel para CSV**, **definir o formato numérico do Excel** e **citar valores CSV** para que a saída atenda aos requisitos típicos de troca de dados.

O guia pressupõe que você tem um ambiente de desenvolvimento .NET (Visual Studio 2022 ou superior) e uma licença válida do Aspose.Cells. Nenhum pacote NuGet adicional é necessário além do `Aspose.Cells`.

## Pré-requisitos

- .NET 6.0 SDK ou superior  
- Aspose.Cells para .NET (instalado via NuGet: `Install-Package Aspose.Cells`)  
- Um arquivo Excel de exemplo (`Data.xlsx`) colocado em uma pasta que você possa referenciar a partir do código  

## Etapa 1: Carregar a pasta de trabalho de origem – a base para salvar a pasta de trabalho como CSV

Primeiro você cria uma instância `Workbook` que aponta para o arquivo Excel que deseja converter.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Por que esta etapa é importante*: O objeto `Workbook` contém todas as planilhas, estilos e fórmulas. Todas as operações subsequentes de CSV atuam sobre essa representação em memória.

## Etapa 2: Limitar a precisão decimal ao salvar a pasta de trabalho como CSV

Quando você precisa exatamente de quatro dígitos após o ponto decimal, configure `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Ponto chave*: `SignificantDigits` arredonda cada célula numérica para o número especificado de casas decimais antes de gravar o arquivo CSV. Isso evita ruído de ponto flutuante em sistemas downstream.

## Etapa 3: Exportar Excel para CSV com valores citados

Alguns analisadores downstream exigem que cada campo seja envolto em aspas duplas, especialmente quando os valores contêm vírgulas ou quebras de linha. A classe `ExportTableOptions` permite tratar cada célula como string e aplicar a citação personalizada.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Por que você deve citar valores*: Citar protege vírgulas, quebras de linha e espaços iniciais/finais de serem interpretados como delimitadores, o que é essencial para uma importação de dados confiável.

## Etapa 4: Definir o formato numérico do Excel para datas do calendário japonês

O Excel pode armazenar datas usando calendários específicos de eras. Para demonstrar, insira uma string de data no calendário japonês e aplique o formato numérico adequado.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Explicação*: A chamada `SetNumberFormat` indica ao Aspose.Cells que interprete a string usando o calendário japonês. Quando você chama `GetDateTime()`, a biblioteca converte automaticamente a notação da era para a data gregoriana.

## Etapa 5: Verificar os arquivos CSV gerados

Após executar o código, você deverá ver três arquivos em `YOUR_DIRECTORY`:

| Nome do arquivo            | Destaques |
|----------------------------|-----------|
| `Data_Sig4.csv`            | Números arredondados para 4 casas decimais |
| `TableExport.csv`          | Cada célula envolta em aspas duplas |
| `Data.xlsx` (inalterado)   | Demonstra o tratamento de datas do calendário japonês (visualizável no Excel) |

Abra `Data_Sig4.csv` em um editor de texto simples para confirmar a precisão, e abra `TableExport.csv` para ver os valores citados, por exemplo:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

A saída no console para a data da era será:

```
2021-04-01 00:00:00
```

## Armadilhas comuns e como evitá‑las

- **Separadores decimais dependentes de localidade**: `CsvSaveOptions` respeita a cultura atual. Se precisar de ponto (`.`) como separador independentemente da localidade, defina `csvOptions.Separator = ',';`.
- **Planilhas muito grandes**: Exportar uma pasta de trabalho com milhões de linhas pode consumir muita memória. Use `ExportTableOptions.StartRow` e `EndRow` para limitar o intervalo de exportação.
- **Caracteres especiais dentro de strings**: O escritor personalizado na Etapa 3 adiciona apenas aspas ao redor. Se uma célula já contiver aspas, duplique‑as (`""`) para manter a validade do CSV.

## Dica avançada: combinar opções para controle máximo

Você pode encadear `CsvSaveOptions` e `ExportTableOptions` primeiro convertendo a pasta de trabalho para um `MemoryStream` com um conjunto de opções e, em seguida, gravando o stream no disco com outro. Essa abordagem permite, por exemplo, aplicar tanto o arredondamento decimal **quanto** a citação em uma única passagem:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Conclusão

Agora você sabe como **salvar uma pasta de trabalho como CSV** com tratamento preciso de decimais, valores citados e formatação de data personalizada. A solução completa cobre o carregamento da pasta de trabalho, a configuração de `CsvSaveOptions`, o uso de `ExportTableOptions` para **citar valores CSV** e a aplicação de um **formato numérico do Excel** para datas do calendário japonês. A partir daqui, você pode explorar opções adicionais como separadores personalizados, diferentes codificações ou exportação seletiva de planilhas.

---

*Próximos passos*  
- Explore `CsvSaveOptions.Encoding` para gravar arquivos UTF‑8 BOM ou UTF‑16.  
- Use `ExportTableOptions.StartColumn` / `EndColumn` para exportar apenas um subconjunto de colunas.  
- Combine essas técnicas com o `DataFormatter` do Aspose.Cells para formatação numérica sensível à localidade.  

Happy coding!

## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Save Workbook as CSV – Complete Guide to Export Excel to CSV with Controlled](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Save workbook as CSV in C# – Export Excel to CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}