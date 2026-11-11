---
category: general
date: 2026-10-26
description: Aprenda a usar WRAPCOLS em C# para dividir um intervalo em colunas, aplicar
  WRAPROWS nas linhas e salvar a pasta de trabalho como XLSX programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: pt
lastmod: 2026-10-26
og_description: Como usar WRAPCOLS em C# para dividir dados em colunas, usar WRAPROWS
  para linhas e salvar a planilha como XLSX. Siga o guia completo passo a passo.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Como usar WRAPCOLS em C# – dividir intervalos e salvar como XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como usar WRAPCOLS em C# e salvar a pasta de trabalho como XLSX
url: /pt/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar WRAPCOLS em C# e salvar a pasta de trabalho como XLSX

Se você precisa **how to use WRAPCOLS** para reorganizar dados em um arquivo Excel, este guia mostra uma solução completa e executável. Você verá um **excel wrapcols example**, aprenderá como **split range into rows** com WRAPROWS e terminará com **save workbook as XLSX** — tudo feito **programmatically**.

Trabalhar com Excel a partir de C# geralmente significa criar uma pasta de trabalho, aplicar fórmulas e persistir o arquivo. O código abaixo usa a biblioteca Aspose.Cells, que permite manipular arquivos Excel sem precisar do Microsoft Office instalado. Ao final deste tutorial, você será capaz de **create excel workbook programmatically**, dividir dados tanto horizontalmente quanto verticalmente e gerar um arquivo `.xlsx` limpo pronto para processamento posterior.

## Pré-requisitos

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+)
* Uma referência ao pacote NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Familiaridade básica com C# e fórmulas do Excel

## Etapa 1: Como usar WRAPCOLS para dividir um intervalo em colunas

A função **WRAPCOLS** recebe um intervalo unidimensional e distribui seus valores pelas colunas especificadas. Neste exemplo, começamos com valores em `A1:A10` e pedimos ao WRAPCOLS para criar três colunas.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Resultado:** As células `C1:E4` agora contêm os dez itens originais organizados em três colunas (a última coluna contém os itens restantes).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## Etapa 2: Dividir intervalo em linhas com WRAPROWS

Enquanto **WRAPCOLS** funciona horizontalmente, **WRAPROWS** faz o oposto: distribui um intervalo por um número especificado de linhas. Aqui, pegamos valores de `B1:B10` e os organizamos em duas linhas a partir de `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Resultado:** A fórmula preenche as células `F1:K2` com os dez valores distribuídos em duas linhas.

## Etapa 3: Salvar pasta de trabalho como XLSX

Depois de aplicar as fórmulas, a etapa final é persistir o arquivo. A operação **save workbook as xlsx** grava a pasta de trabalho em memória no disco no formato OpenXML moderno.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Como o arquivo salvo se parece

Ao abrir `wrapcols_wraprows_output.xlsx` no Excel, você verá:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

e

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Valor 1 | Valor 3 | Valor 5 | Valor 7 | Valor 9 | |
| Valor 2 | Valor 4 | Valor 6 | Valor 8 | Valor 10 | |

As fórmulas permanecem nas células, de modo que quaisquer alterações posteriores nos intervalos de origem são refletidas automaticamente.

## Etapa 4: Variações comuns e casos extremos

### Alterando o número de colunas ou linhas

* **Mais colunas:** Aumente o segundo argumento de `WRAPCOLS`.  
  Exemplo: `=WRAPCOLS(A1:A10,5)` cria cinco colunas, deixando células vazias onde os dados acabam.
* **Contagem de colunas dinâmica:** Use uma referência de célula em vez de um número fixo.  
  `=WRAPCOLS(A1:A10, G1)` onde `G1` contém a contagem de colunas desejada.

### Lidando com células vazias ou não numéricas

WRAPCOLS e WRAPROWS ignoram células vazias por padrão, mas preservam a ordem dos valores não vazios. Se precisar preservar os vazios, envolva o intervalo de origem com as funções `IFERROR` ou `TEXT` antes de aplicar WRAPCOLS.

### Salvando em outros formatos

Embora este tutorial se concentre em **save workbook as xlsx**, Aspose.Cells suporta vários formatos (`.xls`, `.csv`, `.pdf`, etc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Dicas profissionais e armadilhas

* **Dica profissional:** Defina `Workbook.Settings.CalcEngineEnabled = true` se você planeja avaliar as fórmulas imediatamente após salvar.
* **Cuidado com:** Grandes intervalos de origem podem gerar áreas de spill muito grandes, o que pode impactar o desempenho. Limite o tamanho do intervalo ou divida a operação em várias planilhas.
* **Segurança de thread:** Os objetos Aspose.Cells **não** são seguros para uso em múltiplas threads. Crie uma instância separada de `Workbook` por thread se você estiver processando arquivos em paralelo.

## Conclusão

Agora você sabe **how to use WRAPCOLS** para dividir um intervalo vertical em várias colunas, como **split range into rows** com WRAPROWS e como **save workbook as XLSX** após realizar essas transformações. Seguindo os passos acima, você pode **create excel workbook programmatically**, aplicar fórmulas spill poderosas e gerar arquivos Excel prontos para compartilhamento sem intervenção manual.

### O que vem a seguir?

* Explore **conditional formatting** para destacar os dados spill.
* Combine **WRAPCOLS** com **SORT** ou **FILTER** para dashboards dinâmicos.
* Use a **charting API** do Aspose.Cells para visualizar os dados reorganizados diretamente do código.

Feliz codificação, e aproveite automatizar seus fluxos de trabalho Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [como usar wrapcols em C# – Guia completo com Excel WRAPROWS & Recalcular Fórmulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Como usar WRAPCOLS em C# – Redimensionar um Array para uma Matriz no Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Como usar WRAPCOLS – Guia completo para automação Excel em C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}