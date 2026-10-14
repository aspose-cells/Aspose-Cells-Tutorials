---
category: general
date: 2026-10-13
description: Crie uma pasta de trabalho Excel em C# e escreva a data no Excel usando
  Aspose.Cells. Aprenda a salvar o arquivo Excel como xlsx e a adicionar a data à
  planilha com o código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: pt
lastmod: 2026-10-13
og_description: Crie uma pasta de trabalho Excel em C# e escreva a data no Excel.
  Siga este guia completo para salvar o arquivo Excel como xlsx e adicionar a data
  à planilha com Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Criar pasta de trabalho Excel e adicionar data à planilha – passo a passo
  em C#
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar pasta de trabalho do Excel e adicionar data à planilha em C#
url: /pt/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel e adicionar data à planilha em C#

Se você precisa **criar pasta de trabalho Excel** programaticamente, este guia mostra como **escrever data no Excel** e **salvar arquivo Excel** como uma pasta de trabalho *.xlsx*. Você verá um exemplo completo e executável que analisa uma string de era imperial japonesa e armazena o `DateTime` resultante na célula A1.

Trabalhar com Excel a partir de C# geralmente requer três etapas: instanciar a pasta de trabalho, colocar dados em uma planilha e, finalmente, persistir o arquivo. Este tutorial cobre cada etapa, explica por que o código foi escrito dessa forma e destaca armadilhas comuns, como análise dependente de cultura e permissões de sistema de arquivos. Ao final, você poderá **adicionar data à planilha**, **salvar pasta de trabalho como xlsx** e adaptar o padrão para qualquer tipo de dado.

> **Pré-requisito** – O exemplo usa a biblioteca **Aspose.Cells for .NET** (versão 23.10 ou posterior). Instale-a via NuGet:

```bash
dotnet add package Aspose.Cells
```

Você também precisa de um SDK .NET 6+ e de um diretório gravável para o arquivo de saída.

---

## Criar pasta de trabalho Excel e configurar planilha

A primeira etapa é instanciar uma pasta de trabalho vazia e obter sua planilha padrão. O Aspose.Cells cria automaticamente uma pasta de trabalho com uma planilha chamada “Sheet1”.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Por que isso importa** – `Workbook` é o ponto de entrada para todas as operações do Excel. Ao criá‑la sem parâmetros, você obtém uma pasta de trabalho limpa que pode, posteriormente, **salvar arquivo Excel** em qualquer formato que escolher.

---

## Analisar data imperial japonesa

Datas imperiais japonesas usam um símbolo de era (por exemplo, “R” para Reiwa) seguido por um ano de dois dígitos. O método .NET `DateTime.ParseExact` pode lidar com esse formato quando você fornece um objeto `DateTimeParseOptions` personalizado que indica ao analisador usar o calendário do Imperador japonês.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Explicação** –  
* `gg` lê o designador de era (`R` para Reiwa).  
* `yy` lê o ano de dois dígitos dentro dessa era.  
* `MM/dd` lê mês e dia.  

Se você omitir `parseOptions`, o analisador assume o calendário gregoriano e lança um `FormatException`. Esse é um caso de borda comum ao lidar com calendários não gregorianos.

---

## Escrever data na planilha

Agora que você tem um valor `DateTime`, pode colocá‑lo em uma célula. O Aspose.Cells formata automaticamente a célula com base no tipo do valor.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Por que definir um estilo?** – Sem um estilo, o Excel pode exibir a data usando o formato padrão do sistema, o que pode ser confuso para usuários em outras localidades. Definir explicitamente `"yyyy-mm-dd"` garante uma aparência consistente.

---

## Salvar arquivo Excel como xlsx

Por fim, persista a pasta de trabalho no disco. O método `Save` determina o formato de saída a partir da extensão do arquivo, portanto usar “.xlsx” aciona automaticamente o formato Office Open XML.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Dica** – Se o diretório de destino não existir ou você não tiver permissão de gravação, `Save` lança um `IOException`. Sempre verifique o caminho antes de chamar `Save`.

---

## Exemplo completo executável

Abaixo está o programa completo que você pode copiar, colar e executar. Ele inclui todas as diretivas `using`, tratamento de erros e comentários que esclarecem cada operação.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Resultado esperado**

Ao abrir `JapaneseDate.xlsx`, a célula A1 contém a data **2021‑04‑01** (o equivalente gregoriano de Reiwa 3 / 04 / 01) exibida no formato `yyyy‑mm‑dd`.

![Pasta de trabalho Excel com data na célula A1](excel-date-screenshot.png){alt="Captura de tela de uma pasta de trabalho Excel mostrando uma data imperial japonesa na célula A1"}

---

## Perguntas comuns e casos de borda

| Pergunta | Resposta |
|----------|----------|
| *E se a era mudar (por exemplo, Heisei para Reiwa)?* | O calendário `JapaneseEmperor` mapeia automaticamente os símbolos de era (`H`, `R`, etc.) para o intervalo gregoriano correto, portanto você só precisa atualizar a string de entrada. |
| *Posso escrever várias datas em uma coluna?* | Sim. Percorra seus dados e chame `sheet.Cells[row, column].PutValue(dateValue)` para cada linha. |
| *E se eu precisar de um formato de data diferente?* | Altere `dateStyle.Custom` para qualquer string de formato de data do Excel, como `"dd-mmm-yyyy"` ou `"mm/dd/yyyy"`. |
| *Existe uma maneira de proteger a planilha após escrever a data?* | Use `sheet.Protect(ProtectOptions.All, "password")` antes de salvar. |
| *Como lidar com fusos horários?* | `DateTime` armazena hora UTC ou local. Converta usando `DateTime.SpecifyKind` ou `TimeZoneInfo.ConvertTime` antes de chamar `PutValue`. |

---

## Conclusão

Agora você sabe como **criar pasta de trabalho Excel**, **escrever data no Excel**, **adicionar data à planilha** e **salvar pasta de trabalho como xlsx** usando Aspose.Cells em C#. O exemplo completo demonstra a análise de uma string de calendário imperial japonês, a aplicação de um estilo consistente e o tratamento de questões de sistema de arquivos.  

A partir daqui, você pode


## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código totalmente funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook – Wrap Columns and Save as XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}