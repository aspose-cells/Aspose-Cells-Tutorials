---
category: general
date: 2026-10-13
description: Aprenda como salvar Excel como TXT com Aspose.Cells. Este guia aborda
  exportar Excel para TXT, escrever valor em uma célula e definir dígitos significativos
  em apenas alguns passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: pt
lastmod: 2026-10-13
og_description: Salvar Excel como TXT com Aspose.Cells. Aprenda como exportar Excel
  para TXT, escrever valor em uma célula e definir dígitos significativos em apenas
  algumas linhas de código C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Salvar Excel como TXT – guia passo a passo para desenvolvedores .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Como salvar Excel como TXT usando Aspose.Cells em C#
url: /pt/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar Excel como TXT usando Aspose.Cells em C#

Se você precisa **salvar Excel como TXT** rapidamente, este tutorial mostra o processo completo em menos de cinco minutos. Você verá como exportar Excel para TXT, escrever valor em célula e definir dígitos significativos para que o arquivo de texto contenha exatamente os dados esperados.

Exportar uma planilha como TXT é útil quando sistemas downstream aceitam apenas entrada em texto simples, quando você precisa gerar logs ou quando deseja um despejo legível por humanos dos cálculos. O exemplo abaixo funciona com Aspose.Cells v25.10 ou posterior e roda em qualquer runtime .NET 6+.

## Pré-requisitos

* Uma cópia licenciada do **Aspose.Cells for .NET** (a versão de avaliação gratuita serve para testes).
* .NET 6 SDK ou posterior instalado.
* Uma IDE como Visual Studio 2022, VS Code ou Rider.
* Conhecimento básico de C# — não é necessário experiência avançada em automação do Excel.

Você pode instalar o pacote NuGet Aspose.Cells com:

```bash
dotnet add package Aspose.Cells
```

## Etapa 1: Criar uma workbook e acessar sua primeira planilha (save excel as txt)

A primeira coisa que você faz quando quer **save Excel as TXT** é criar um objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** A classe `Workbook` é o ponto de entrada para todas as operações de planilha. Ao iniciar com uma workbook nova, você evita formatações ocultas que poderiam afetar a saída em texto simples.

## Etapa 2: Escrever um número de alta‑precisão em uma célula (write value to cell)

Agora você precisa **write value to cell** A1. O método `PutValue` detecta automaticamente o tipo de dado e o armazena como um valor numérico.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** Se mais tarde precisar escrever strings, datas ou fórmulas, o mesmo método `PutValue` funciona — basta passar o tipo .NET apropriado.

## Etapa 3: Configurar as opções de exportação para manter apenas a precisão necessária (set significant digits)

Ao exportar para um arquivo TXT, costuma‑se limitar o número de dígitos para manter o tamanho do arquivo pequeno ou para atender a uma especificação downstream. A classe `TxtSaveOptions` fornece a propriedade `SignificantDigits` para esse propósito.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Why you should set significant digits:** Sem essa configuração, o Aspose.Cells grava o valor de dupla precisão completo, o que pode gerar strings longas como `12345.6789012345`. Definir `SignificantDigits = 6` reduz a saída para `12345.7`, atendendo à maioria dos requisitos de relatório.

## Etapa 4: Exportar a workbook como um arquivo TXT (export excel to txt)

Finalmente, você **export Excel to TXT** chamando `Workbook.Save` com as opções configuradas anteriormente.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Quando o código termina, `LimitedDigits.txt` contém:

```
12345.7
```

> **Result verification:** Abra o arquivo em qualquer editor de texto (Notepad, VS Code) para confirmar que apenas seis dígitos significativos estão presentes e que não há vírgulas extras ou delimitadores de tabulação.

## Exemplo completo e executável

Abaixo está um aplicativo de console autocontido que você pode copiar, colar e executar imediatamente.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explicação de cada bloco**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Importa o namespace Aspose.Cells necessário para `Workbook`, `Worksheet` e `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instancia uma workbook Excel vazia na memória. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 with a double‑precision number. |
| `TxtSaveOptions` | Configura o comportamento **set significant digits** para a exportação TXT. |
| `workbook.Save(..., txtOptions);` | Executa a operação **export excel to txt**, criando o arquivo de texto simples. |

## Casos de borda e dicas adicionais

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | Use `txtOptions.Encoding = Encoding.UTF8` se precisar de suporte Unicode, e considere transmitir o arquivo com `Workbook.Save(Stream, txtOptions)` para evitar alto consumo de memória. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` também expõe `Separator` — defina‑o como `','` para produzir saída no estilo CSV mantendo o formato TXT. |
| **Preserving formulas** | Defina `txtOptions.ExportFormulas = true` para gravar o texto da fórmula em vez do valor calculado. |
| **Locale‑specific decimal separators** | Ajuste `txtOptions.DecimalSeparator` para `','` em localidades europeias. |
| **Multiple worksheets** | Percorra `workbook.Worksheets` e chame `Save` para cada uma, adicionando o nome da planilha ao nome do arquivo. |

## Perguntas frequentes

**Q: O `SignificantDigits` arredonda ou trunca?**  
A: Ele arredonda para o valor mais próximo com base no número especificado de dígitos significativos, garantindo que a saída seja matematicamente precisa nessa precisão.

**Q: Posso exportar diretamente para um memory stream?**  
A: Sim. Substitua o caminho do arquivo por uma instância `MemoryStream`: `workbook.Save(stream, txtOptions);`. Isso é útil para APIs web que precisam retornar o conteúdo TXT sem tocar no sistema de arquivos.

**Q: E se eu precisar manter a formatação original (por exemplo, datas)?**  
A: Use `txtOptions.ExportFormattedValues = true`. Isso força o Aspose.Cells a gravar o texto exibido na célula em vez do valor bruto.

## Conclusão

Agora você sabe como **save Excel as TXT** com controle total sobre precisão, formatação e local de saída. Seguindo as quatro etapas — criar uma workbook, **write value to cell**, **set significant digits** e **export Excel to TXT** — você pode integrar a exportação em texto simples em qualquer aplicação .NET.

Em seguida, explore tópicos relacionados como **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV** ou **use Aspose.Cells to generate JSON reports**. Cada um desses se baseia nos mesmos conceitos centrais demonstrados aqui, oferecendo um conjunto de ferramentas versátil para intercâmbio de dados entre plataformas.

Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}