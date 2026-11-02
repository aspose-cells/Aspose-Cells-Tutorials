---
category: general
date: 2026-08-11
description: Criar arquivo Excel programaticamente em C# usando Aspose.Cells. Analisar
  uma data de era japonesa, escrevê‑la em uma célula e salvar a pasta de trabalho.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: pt
lastmod: 2026-08-11
og_description: Crie um arquivo Excel programaticamente em C# usando Aspose.Cells.
  Aprenda a analisar uma data de era japonesa com o formato personalizado DateTime.ParseExact,
  escrever a data em uma célula do Excel e salvar a pasta de trabalho de forma eficiente.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Criar arquivo Excel programaticamente em C# – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Criar arquivo Excel programaticamente em C# – tutorial
url: /pt/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar arquivo Excel programaticamente em C# – tutorial

Se você precisa **criar arquivo Excel programaticamente**, pode fazê‑lo em algumas linhas de código C#. Este guia mostra como gerar uma pasta de trabalho Excel com Aspose.Cells, analisar uma data de era japonesa usando um **DateTime.ParseExact com formato personalizado**, gravar essa data em uma célula da planilha e, finalmente, **salvar o arquivo Excel em estilo C#**. Ao final, você terá um arquivo *.xlsx* pronto para uso que contém uma data gregoriana convertida corretamente.

Você aprenderá a:

* Inicializar uma pasta de trabalho sem modelo.  
* Converter uma string baseada em era, como `"R3/04/01"`, para um `DateTime`.  
* Inserir o valor `DateTime` em uma célula específica (`A1`).  
* Persistir a pasta de trabalho no disco com uma única chamada `Save`.

Nenhuma biblioteca adicional além do Aspose.Cells e da biblioteca de classes base do .NET é necessária.

---

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* **.NET 6.0** ou superior instalado (o código também funciona com .NET Framework 4.6+).  
* Uma licença válida do **Aspose.Cells** ou uma cópia de avaliação gratuita.  
* Familiaridade básica com a sintaxe C# e Visual Studio (ou qualquer IDE de sua preferência).

---

## Criar arquivo Excel programaticamente – inicializar pasta de trabalho

O primeiro passo é criar um objeto de pasta de trabalho vazio. Aspose.Cells fornece a classe `Workbook` que representa um arquivo Excel inteiro na memória.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Por que isso importa:**  
Criar a pasta de trabalho programaticamente elimina a necessidade de um arquivo de modelo físico, o que mantém a pegada de implantação pequena e permite gerar arquivos sob demanda para relatórios, faturas ou exportações de dados.

---

## Usar DateTime.ParseExact com formato personalizado para datas de era japonesa

Strings de data que contêm símbolos de era japonesa (por exemplo, `"R"` para Reiwa) não podem ser analisadas com o `DateTime.Parse` padrão. É necessário fornecer um **formato personalizado** e uma cultura japonesa que reconheça o designador de era.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Por que isso importa:**  
`DateTime.ParseExact` garante que a entrada corresponda ao padrão que você especifica, evitando ambiguidades dependentes de localidade. O padrão `"ggy/MM/dd"` indica ao .NET que o primeiro caractere é uma era (`g`), seguido por um ano de dois dígitos (`yy`), mês e dia. Usar `japaneseCulture` assegura que os símbolos de era sejam interpretados corretamente, produzindo um `DateTime` gregoriano (`2021‑04‑01` no exemplo).

---

## Gravar data em célula Excel com Aspose.Cells

Agora que você tem uma instância `DateTime`, pode colocá‑la em qualquer célula da planilha. Aspose.Cells formata automaticamente a célula de acordo com o estilo de data padrão da pasta de trabalho.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Por que isso importa:**  
Usar `PutValue` permite que Aspose.Cells infera o tipo da célula (data, número, texto) a partir do tipo .NET que você fornece. Essa abordagem é mais segura do que gravar uma string formatada, pois o Excel mantém a semântica da data — permitindo que você classifique, filtre ou execute cálculos na coluna posteriormente.

---

## Como salvar arquivo Excel C# – finalizando a pasta de trabalho

O último passo é persistir a pasta de trabalho em memória em um arquivo físico. Aspose.Cells suporta muitos formatos; aqui usamos o formato moderno `.xlsx`.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Por que isso importa:**  
Chamar `Save` com `SaveFormat.Xlsx` grava um arquivo Office Open XML compatível com padrões que pode ser aberto no Excel, LibreOffice ou qualquer visualizador que suporte o formato. O método também cuida de toda a compressão e empacotamento subjacentes, de modo que você não precisa gerenciar streams zip manualmente.

---

## Resultado esperado

Ao executar o programa:

| Célula | Valor (exibição) | Tipo subjacente |
|--------|------------------|-----------------|
| A1     | 4/1/2021         | Data (DateTime) |

O arquivo `JapaneseEra.xlsx` conterá uma única planilha chamada **Sheet1** com a data gregoriana `2021‑04‑01` na célula **A1**. O Excel tratará a célula como data, permitindo cálculos adicionais como `=A1+30` para adicionar 30 dias.

---

## Variações comuns e casos de borda

| Situação | Solução |
|----------|---------|
| **Era diferente** (por exemplo, Heisei `H30/12/31`) | Altere a string de entrada; o mesmo padrão `"ggy/MM/dd"` funciona porque o `CultureInfo` japonês conhece todas as eras. |
| **Ano de quatro dígitos** (por exemplo, `"R2023/04/01`) | Use `"ggyyyy/MM/dd"` como a string de formato. |
| **Símbolo de era ausente** | Forneça um formato de fallback como `"yyyy/MM/dd"` e tente `DateTime.TryParseExact` com múltiplos padrões. |
| **Data inválida** (por exemplo, `"R3/13/01`) | Envolva `ParseExact` em um bloco `try/catch` ou use `DateTime.TryParseExact` para lidar com falhas de análise de forma elegante. |

**Dica profissional:** Sempre valide o `DateTime` analisado antes de gravá‑lo na planilha, especialmente quando os dados de origem vêm de entrada do usuário ou arquivos externos.

---

## Recapitulação

* Você **criou arquivo Excel programaticamente** usando Aspose.Cells.  
* Você analisou uma string de era japonesa com **DateTime.ParseExact formato personalizado**.  
* Você **gravou a data em célula Excel** usando `PutValue`.  
* Você aprendeu **como salvar arquivo Excel C#** com uma única chamada `Save`.

Esses quatro passos formam um padrão reutilizável para qualquer cenário em que você precise importar datas culturalmente específicas em relatórios Excel.

---

## Próximos passos

* Explore **estilização de células** (fontes, cores, bordas) para deixar seus relatórios mais polidos.  
* Use **Workbook.Save** com outros formatos (`Csv`, `Pdf`) para exportar dados para diferentes públicos.  
* Combine esta técnica com **inserção em massa de dados** (`Cells.ImportDataTable`) para importações em grande escala.  

Sinta‑se à vontade para experimentar diferentes símbolos de era, formatos numéricos personalizados ou múltiplas planilhas. A mesma lógica central — criar, analisar, gravar, salvar — se aplica a todas as tarefas de automação Excel em C#.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como criar e salvar uma pasta de trabalho Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Como salvar páginas específicas de um arquivo Excel como PDF usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Como criar e salvar uma pasta de trabalho Excel como SVG usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}