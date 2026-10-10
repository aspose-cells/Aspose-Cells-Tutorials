---
category: general
date: 2026-10-10
description: Aprenda a salvar Excel como texto em C# usando Aspose.Cells. Este guia
  aborda converter Excel para txt, exportar XLSX para txt e criar txt a partir do
  Excel com código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: pt
lastmod: 2026-10-10
og_description: Salve o Excel como texto usando Aspose.Cells para .NET. Siga este
  guia para converter Excel em txt, exportar XLSX para txt e criar txt a partir do
  Excel com código de exemplo.
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: Salvar Excel como texto em C# – tutorial completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: Como salvar Excel como texto com Aspose.Cells – guia passo a passo
url: /pt/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar Excel como texto com Aspose.Cells – guia passo a passo

Se você precisa **salvar Excel como texto** rapidamente, este tutorial mostra exatamente como fazer isso em C# com Aspose.Cells. Você verá como **converter Excel para txt**, controlar a precisão numérica e lidar com casos de borda comuns — tudo em um único exemplo executável.

Nas seções a seguir, você aprenderá o fluxo de trabalho completo, desde a instalação da biblioteca até a verificação do arquivo de saída. Nenhuma documentação externa é necessária; tudo o que você precisa está incluído aqui.

## O que você alcançará

* Carregar qualquer workbook `.xlsx` do disco.  
* Configurar `TxtSaveOptions` para limitar o número de dígitos significativos.  
* **Exportar XLSX para txt** com uma única chamada `Save`.  
* Entender como solucionar problemas de formatação ao **criar txt a partir do Excel**.

### Pré-requisitos

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7.2+).  
* Familiaridade básica com C# e Visual Studio (ou qualquer IDE .NET).  
* Uma licença ativa do Aspose.Cells for .NET ou uma chave de avaliação gratuita.  
* O arquivo Excel que você deseja converter (`input.xlsx` nos exemplos).

> **Dica profissional:** Se você pretende executar isso em um servidor, armazene o arquivo de licença em um local seguro e carregue‑o uma única vez na inicialização da aplicação.

## Etapa 1: Configurar o ambiente de desenvolvimento

1. Crie um novo projeto de console:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. Adicione o pacote NuGet Aspose.Cells:

   ```bash
   dotnet add package Aspose.Cells
   ```

   Isso traz a versão estável mais recente (em 2026‑10‑10 é 23.9).

3. (Opcional) Se você tem um arquivo de licença, coloque `Aspose.Cells.lic` na raiz do projeto e adicione o seguinte código no início de `Program.cs`:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   Carregar a licença remove as marcas d'água de avaliação e desabilita limites de tamanho.

## Etapa 2: Carregar o workbook Excel

A primeira linha funcional cria uma instância `Workbook` que representa o arquivo Excel completo.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**Por que isso importa:** `Workbook` abstrai planilhas, células, fórmulas e formatação. Ao carregar o arquivo uma única vez, você mantém a conversão rápida e eficiente em memória.

## Etapa 3: Configurar TxtSaveOptions para controle preciso de dígitos

Ao **converter Excel para txt**, valores numéricos podem conter muitas casas decimais. `TxtSaveOptions` permite limitar a saída a um número específico de dígitos significativos, o que costuma ser exigido por sistemas downstream que esperam texto de largura fixa.

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**Explicação:**  
* `SignificantDigits` elimina ruído de ponto flutuante enquanto preserva precisão suficiente para a maioria dos cálculos de negócios.  
* `Separator` tem padrão de espaço; definir como `\t` (tab) torna o arquivo resultante mais fácil de importar para bancos de dados ou planilhas.  
* `ExportActiveWorksheetOnly` impede a exportação acidental de planilhas ocultas, o que poderia inflar o arquivo de texto.

## Etapa 4: Exportar XLSX para txt com as opções configuradas

Agora você tem tudo que precisa para **salvar Excel como texto**. O método `Save` grava a representação em texto simples no caminho de destino.

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

O `output.txt` gerado conterá linhas de valores separados por tabulação, cada célula renderizada como texto simples de acordo com as opções definidas.

### Programa completo executável

Juntando as peças, aqui está um aplicativo console completo e autônomo:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**Saída esperada** (console):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**Amostra do `output.txt` resultante** (primeiras três linhas):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

Os números são arredondados para cinco dígitos significativos, e as colunas são separadas por tabulações.

## Etapa 5: Verificar a saída e lidar com casos de borda

### Verificar programaticamente

Você pode ler o arquivo gerado de volta para a memória para confirmar que a exportação foi bem‑sucedida:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### Casos de borda comuns

| Situação                              | O que observar                                 | Correção recomendada |
|----------------------------------------|---------------------------------------------------|-----------------|
| Células contêm fórmulas                | O valor exportado é o **resultado calculado**, não o texto da fórmula. | Garanta que o workbook esteja totalmente calculado (`workbook.CalculateFormula();`) antes de salvar. |
| Datas aparecem como números seriais         | O Excel armazena datas como números; elas podem aparecer como `44745`. | Defina `txtOptions.ConvertDateTime = true;` para forçar um formato de data legível. |
| Planilhas grandes (>10 000 linhas)        | O consumo de memória pode disparar.                     | Use `txtOptions.ExportAllSheets = false;` e processe as planilhas individualmente. |
| Caracteres Unicode (por exemplo, emojis)      | A codificação padrão é UTF‑8; sistemas mais antigos podem esperar ANSI. | Defina `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` se necessário. |

Ao antecipar esses cenários, você pode **criar txt a partir do Excel** de forma confiável em diferentes conjuntos de dados.

## Conclusão

Agora você sabe como **salvar Excel como texto** usando Aspose.Cells para .NET, desde o carregamento do workbook até a configuração de `TxtSaveOptions` e, finalmente, **exportar XLSX para txt**. O exemplo demonstra todo o caminho do código, explica o raciocínio por trás de cada configuração e cobre armadilhas típicas ao **converter Excel para txt**.

### O que vem a seguir?

* Tente exportar para CSV (`CsvSaveOptions`) para arquivos compatíveis com Excel separados por vírgulas.  
* Explore a classe `PdfSaveOptions` para **exportar Excel para PDF** em uma única linha.  
* Combine várias planilhas em um único arquivo de texto iterando sobre `workbook.Worksheets`.  

Sinta-se à vontade para experimentar as opções — alterando o separador, a precisão ou a seleção de planilhas — para adequar ao seu fluxo de trabalho específico.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Salvar Excel como Arquivo de Texto com Separador Personalizado usando Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Salvar Excel como txt – Guia Completo em C# para Exportar Números com Dígitos Significativos](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [Como Salvar Arquivos Excel em Múltiplos Formatos Usando Aspose.Cells .NET (Guia 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}