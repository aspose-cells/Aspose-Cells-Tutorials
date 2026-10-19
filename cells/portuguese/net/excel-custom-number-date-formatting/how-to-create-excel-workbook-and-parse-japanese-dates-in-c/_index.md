---
category: general
date: 2026-10-10
description: Criar uma pasta de trabalho Excel em C# e definir o valor da célula com
  uma data de era japonesa, depois aplicar formato personalizado e ler a célula de
  data usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: pt
lastmod: 2026-10-10
og_description: Crie uma pasta de trabalho Excel em C# e analise datas de era japonesa.
  Aprenda a definir o valor da célula, aplicar formato personalizado e ler a célula
  de data com Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Criar pasta de trabalho do Excel em C# – guia completo de análise de datas
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como criar uma pasta de trabalho do Excel e analisar datas japonesas em C#
url: /pt/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar Excel workbook e analisar datas japonesas em C#

Se você precisar **create Excel workbook** do zero, este guia mostra exatamente como fazer. Você aprenderá a **set cell value** com uma string de data de era japonesa, **apply custom format** que entende a era, e finalmente **read date cell** para obter um .NET `DateTime`. O exemplo completo funciona com a versão mais recente do Aspose.Cells para .NET, então você pode copiar‑colar o código em qualquer projeto C#.

Trabalhar com datas que incluem eras japonesas pode ser complicado porque o analisador padrão do Excel não reconhece os símbolos de era. Ao usar um formato numérico personalizado (`[ja-JP-Era]`) você indica ao Excel como interpretar a string, permitindo uma **excel date parsing** confiável. As etapas abaixo cobrem todo o fluxo de trabalho, desde a criação da pasta de trabalho até a extração da data.

## Pré-requisitos

- .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.7+)
- Aspose.Cells for .NET (pacote NuGet `Aspose.Cells`)
- Familiaridade básica com C# e Visual Studio ou qualquer IDE de sua escolha

## Etapa 1: Create Excel workbook and add a worksheet

A primeira operação é **create Excel workbook** na memória. Aspose.Cells cria uma planilha padrão automaticamente, mas você pode adicionar mais se necessário.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Criar a pasta de trabalho aloca as estruturas internas que mais tarde armazenam células, estilos e fórmulas. Nenhum arquivo é gravado neste ponto, o que mantém a operação rápida e testável.

## Etapa 2: Set cell value with a Japanese era date string

Em seguida, **set cell value** para a representação de era japonesa `"R5-04-01"` (Reiwa 5, 1 de abril). A string segue o padrão `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Usar `PutValue` armazena o texto bruto. O Excel o tratará como string até que um formato numérico indique o contrário. Essa abordagem funciona para qualquer representação de calendário personalizado, não apenas eras japonesas.

## Etapa 3: Apply a custom number format that understands the Japanese era

Agora **apply custom format** para que o Excel possa traduzir a string de era em uma data serial real. O formato `[ja-JP-Era]yyyy/MM/dd` indica ao mecanismo interpretar o caractere de era inicial (`R` para Reiwa) e calcular a data gregoriana.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

O formato personalizado é armazenado no objeto de estilo da célula. Aspose.Cells respeita esse formato tanto durante a renderização quanto na conversão de valores, permitindo uma **excel date parsing** confiável mais adiante no pipeline.

## Etapa 4: Retrieve the parsed DateTime value from the cell

Finalmente, **read date cell** para obter um .NET `DateTime`. A propriedade `DateTimeValue` retorna o valor convertido com base no formato personalizado aplicado anteriormente.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Quando o programa é executado, o console exibe:

```
Parsed Gregorian date: 2023-04-01
```

A saída confirma que a string de era japonesa `"R5-04-01"` foi interpretada corretamente como 1 de abril de 2023.

## Exemplo completo e executável

Juntando as peças, obtém‑se um programa autônomo que você pode compilar e executar imediatamente.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Executar o programa cria `JapaneseEraDate.xlsx` com a célula A1 exibindo `2023/04/01` enquanto o console mostra a mesma data gregoriana. O arquivo pode ser aberto no Excel para ver o valor formatado.

## Por que esta abordagem funciona

- **create excel workbook** – Instanciar `Workbook` constrói toda a estrutura de arquivo Excel na memória sem tocar no disco.
- **set cell value** – `PutValue` armazena texto bruto, o que é necessário antes de aplicar um formato específico de cultura.
- **apply custom format** – O token `[ja-JP-Era]` preenche a lacuna entre a notação de era e o sistema interno de datas serial do Excel.
- **read date cell** – `DateTimeValue` usa automaticamente o estilo da célula para realizar a conversão, fornecendo um `DateTime` nativo.
- **excel date parsing** – Ao delegar a análise ao estilo da célula, você evita manipulação manual de strings, reduzindo erros e melhorando o suporte a localizações.

## Casos de borda e dicas práticas

- **Different eras** – Use `S` para Showa, `H` para Heisei, `R` para Reiwa. A mesma string de formato funciona para todas as eras.
- **Invalid strings** – Se a célula contiver uma data de era malformada, `DateTimeValue` retorna `DateTime.MinValue`. Verifique `dateCell.IsDate` antes de ler.
- **Multiple cells** – Aplique o formato personalizado a todo um intervalo (`range.ApplyStyle(style)`) quando precisar analisar muitas datas.
- **Performance** – Definir o estilo uma vez por coluna é mais rápido que por célula em planilhas grandes.
- **Saving options** – Aspose.Cells pode gerar XLSX, XLS, CSV ou PDF. Escolha o formato que corresponde ao processamento subsequente.

## Perguntas frequentes

**Posso usar a cultura .NET incorporada em vez de um formato personalizado?**  
A classe .NET `CultureInfo` não entende símbolos de era japonesa da mesma forma que o Excel. Usar um formato numérico personalizado é o método mais confiável para **excel date parsing** de strings de era.

**E se eu precisar gravar a data de volta no Excel no formato de era?**  
Defina o valor da célula como um `DateTime` e aplique o mesmo formato personalizado. O Excel exibirá a era automaticamente.

**Isso funciona em versões mais antigas do Excel?**  
O token `[ja-JP-Era]` é suportado pelo Excel 2010 e posteriores. Aspose.Cells emula o comportamento, portanto a pasta de trabalho é exibida corretamente mesmo quando aberta em versões mais antigas do Excel que não possuem suporte nativo a eras.

## Conclusão

Agora você sabe como **create Excel workbook**, **set cell value** com uma string de era japonesa, **apply custom format**, e **read date cell** para obter um `DateTime`. Esse padrão fornece uma **excel date parsing** robusta sem manipulação manual de strings, tornando seu código de automação C# conciso e confiável.

Em seguida, explore tópicos relacionados como **formatting multiple date columns**, **working with other cultural calendars**, ou **exporting the workbook to PDF**. Cada extensão se baseia nos mesmos princípios abordados aqui, permitindo que você adapte a solução a uma ampla variedade de cenários de localização. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}