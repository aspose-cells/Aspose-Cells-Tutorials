---
category: general
date: 2026-10-01
description: Converter data de era japonesa para um DateTime gregoriano usando Aspose.Cells
  em C#. Aprenda como converter o calendário japonês rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: pt
lastmod: 2026-10-01
og_description: Converter data de era japonesa para um DateTime gregoriano em C#.
  Este tutorial explica como converter o calendário japonês com precisão usando o
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Converter data da era japonesa para o calendário gregoriano em C# – guia
  passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Como converter data da era japonesa para o calendário gregoriano em C#
url: /pt/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter data de era japonesa para o calendário gregoriano em C#

Se você precisa **converter datas de era japonesa** para datas gregorianas em C#, este guia mostra exatamente como fazer. Seja processando dados legados, lendo entrada do usuário ou gerando relatórios, a biblioteca Aspose.Cells torna a conversão simples. Além disso, você descobrirá a melhor forma de **como converter calendário japonês** ao trabalhar com planilhas.

O tutorial cobre cada passo — desde a criação de uma pasta de trabalho até a obtenção de um valor `DateTime` — para que você possa copiar‑colar um programa completo e executável. Nenhuma documentação externa é necessária; basta seguir o código e as explicações abaixo.

## Pré-requisitos

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.6+)
* Uma licença para **Aspose.Cells** (a versão de avaliação gratuita funciona para testes)
* Um ambiente de desenvolvimento como Visual Studio 2022 ou VS Code
* Familiaridade básica com aplicativos de console C#

## Converter data de era japonesa com Aspose.Cells

O núcleo da conversão está em algumas chamadas simples de API. Aspose.Cells interpreta automaticamente strings de era japonesa (por exemplo, “Reiwa 2/04/01”) e expõe o resultado como um objeto `DateTime` assim que a planilha é recalculada.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Por que cada passo importa

| Passo | Propósito | Como ajuda na conversão |
|------|---------|-----------------------------|
| **Create workbook** | Fornece um contêiner que entende fórmulas do Excel e sistemas de datas. | O mecanismo interno de datas da biblioteca é ativado somente dentro de uma pasta de trabalho. |
| **Insert era string** | Fornece o texto bruto do calendário japonês que você deseja traduzir. | Aspose.Cells reconhece nomes de eras como *Reiwa*, *Heisei*, *Showa*, etc. |
| **Set style** | Força a célula a ser tratada como célula de valor e não como string literal. | Sem um estilo, o método `Calculate` pode ignorar a célula, deixando o texto inalterado. |
| **Calculate** | Aciona a análise da string de era e a conversão para o número de data serial interno. | A biblioteca converte “Reiwa 2/04/01” → número serial → `DateTime` gregoriano. |
| **Read `DateTimeValue`** | Retorna o objeto .NET `DateTime` convertido. | Agora você tem um `DateTime` padrão que pode usar em qualquer API .NET. |

## Como converter calendário japonês em outros cenários

A mesma abordagem funciona para qualquer nome de era japonesa suportado pelo Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Tratamento de strings inválidas ou ambíguas

* **Invalid era name** – Aspose.Cells lança uma `FormatException`. Envolva a conversão em `try/catch` para fornecer uma mensagem de erro amigável.
* **Missing year/month/day** – A biblioteca espera um padrão completo “Era Ano/Mês/Dia”. Se você receber dados parciais, adicione as partes ausentes ou rejeite a entrada imediatamente.
* **Different locale settings** – A conversão **não** depende da cultura da thread atual; ela sempre usa o mapa de eras japonesas incorporado ao Aspose.Cells. Isso torna o método seguro para processamento no lado do servidor.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Dicas práticas e armadilhas comuns

* **Always call `SetStyle`** before `Calculate`. Pular esta etapa é uma fonte frequente de bugs porque a célula permanece como um contêiner de texto simples.
* **Reuse the same workbook** se você precisar converter muitas datas. Criar uma nova pasta de trabalho para cada conversão adiciona sobrecarga desnecessária.
* **Batch conversion** – Preencha uma coluna com strings de era, chame `worksheet.Calculate()` uma vez e, em seguida, leia toda a coluna de `DateTimeValue`s. Isso é muito mais eficiente do que recalcular célula por célula.
* **Version compatibility** – A lógica de conversão de era foi introduzida no Aspose.Cells 22.9. Certifique‑se de estar nessa versão ou posterior; versões mais antigas tratam a string como texto simples.

## Exemplo completo funcional (aplicativo console)

A seguir está um programa autônomo que você pode compilar e executar imediatamente. Ele demonstra tanto a conversão Reiwa quanto a Heisei, tratando erros de forma elegante.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Saída esperada no console**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Executar este programa confirma que a biblioteca converte corretamente strings de **convert japanese era date** e relata graciosamente valores não suportados.

## Conclusão

Agora você sabe como **convert Japanese era date** strings para objetos `DateTime` gregorianos padrão usando Aspose.Cells em C#. O processo resume‑se a inserir o texto da era, aplicar um estilo, recalcular a planilha e ler `DateTimeValue`. Seguindo os passos acima, você também pode responder à questão mais ampla de **how to convert Japanese calendar** em lote, tratar erros e otimizar o desempenho.

### Próximos passos

* Explore **formatting options** para gravar a data gregoriana de volta na planilha com um formato numérico personalizado.
* Combine esta conversão com **data import pipelines** (por exemplo, lendo arquivos CSV que contêm datas de era).
* Revise outros recursos do Aspose.Cells, como **date arithmetic** e **regional settings**, para cenários de calendário mais complexos.

Boa codificação, e sinta‑se à vontade para adaptar o exemplo ao seu próprio fluxo de processamento de dados!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Analisar data de era japonesa em C# com Aspose.Cells – Guia completo](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Habilitar análise de era japonesa em C# com Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Como criar pasta de trabalho e converter string para data em C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}