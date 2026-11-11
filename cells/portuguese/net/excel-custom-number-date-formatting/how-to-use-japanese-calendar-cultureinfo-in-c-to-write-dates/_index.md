---
category: general
date: 2026-10-26
description: Aprenda a usar o CultureInfo do calendário japonês em C# ao analisar
  datas de era e inseri‑las em uma planilha do Excel com NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: pt
lastmod: 2026-10-26
og_description: Use CultureInfo do calendário japonês em C# para analisar datas da
  era Reiwa e escrevê‑las em uma planilha Excel. Código completo e executável com
  explicações.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Usar CultureInfo do calendário japonês em C# – exemplo completo no Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Como usar CultureInfo do calendário japonês em C# para gravar datas no Excel
url: /pt/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar CultureInfo do calendário japonês em C# para gravar datas no Excel

Se você precisa **usar CultureInfo do calendário japonês** ao trabalhar com datas em C#, este guia mostra exatamente como fazer. Você aprenderá a analisar uma string de data que contém um nome de era japonesa (por exemplo, *Reiwa 2/5/1*) e então gravar o `DateTime` resultante na primeira célula de uma planilha Excel usando a biblioteca NPOI.

Analisar datas baseadas em eras sem o `CultureInfo` correto gera `FormatException` ou valores de mês/dia incorretos. Ao configurar o `CultureInfo` para o calendário japonês, você garante que o runtime .NET interprete a era corretamente e que o valor armazenado no Excel corresponda à notação japonesa original.

Neste tutorial você vai:

* Criar um objeto `CultureInfo` que usa o calendário japonês.
* Analisar uma string de data de era japonesa com `DateTime.Parse`.
* Inserir o `DateTime` analisado em uma célula de planilha NPOI.
* Ver o programa completo, executável, e a saída esperada.

> **Pré‑requisitos** – .NET 6.0+ (ou .NET Core 3.1+), o pacote **NPOI** NuGet e um entendimento básico de C# e manipulação de arquivos Excel.

---

## O que você precisará

| Item | Motivo |
|------|--------|
| **.NET SDK** (6.0 ou posterior) | Fornece o runtime e as bibliotecas para `CultureInfo`. |
| **NPOI** (pacote NuGet `NPOI`) | Permite criar e manipular arquivos Excel sem precisar do Office instalado. |
| **Visual Studio Code**, **Visual Studio**, ou qualquer IDE C# | Para compilar e executar o exemplo. |
| **String de data de era japonesa** (ex.: `"Reiwa 2/5/1"`) | Demonstra o uso do calendário japonês. |

---

## Etapa 1: Instalar o NPOI

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package NPOI --version 2.6.1
```

O pacote fornece os tipos `IWorkbook`, `ISheet` e `ICell` usados mais adiante.

---

## Etapa 2: Criar um CultureInfo que use o calendário japonês

O calendário japonês é um calendário baseado em eras. Você deve solicitar a variante *Japanese* da localidade `ja-JP` e definir explicitamente o calendário como `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Por que isso importa** – A cultura padrão `ja-JP` usa o calendário gregoriano. Reatribuir a propriedade `Calendar` garante que nomes de eras como *Reiwa* sejam reconhecidos durante a análise.

---

## Etapa 3: Analisar uma string de data de era japonesa

Agora que o `CultureInfo` está configurado, você pode analisar com segurança uma string que contém um nome de era.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Saída**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

O método `Parse` interpreta *Reiwa 2* como o ano gregoriano 2020, mês 5, dia 1.

### Caso limite: tratamento de eras inválidas

Se um usuário fornecer uma era não suportada (ex.: `"Heisei 31/4/30"` após o fim da era Heisei), `DateTime.Parse` lança uma `FormatException`. Envolva a chamada em um bloco try‑catch para fornecer uma mensagem de erro amigável:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Etapa 4: Gravar o DateTime analisado em uma planilha Excel

Com o objeto `DateTime` pronto, você pode armazená‑lo em uma célula Excel. O NPOI formata automaticamente valores `DateTime` como datas do Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Resultado** – Ao abrir *JapaneseEraDate.xlsx* a data **2020‑05‑01** aparece na célula A1.

### Por que usar o NPOI?

*Funciona em qualquer plataforma* (Windows, Linux, macOS) e **não** requer Microsoft Office. Isso torna a solução adequada para pipelines CI, contêineres Docker ou processamento no lado do servidor.

---

## Etapa 5: Programa completo e executável

Juntando tudo, aqui está uma aplicação console completa que demonstra todo o fluxo:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Como executar**

```bash
dotnet run
```

Após a execução, você encontrará `JapaneseEraDate.xlsx` na pasta do projeto com a data analisada corretamente.

---

## Armadilhas comuns e dicas de boas práticas

| Armadilha | Correção / Recomendação |
|-----------|--------------------------|
| Esquecer de definir `japaneseCulture.DateTimeFormat.Calendar` | Sempre atribua uma instância de `JapaneseCalendar`; caso contrário, o nome da era não será reconhecido. |
| Usar `DateTime.TryParse` sem o `CultureInfo` personalizado | Passe o mesmo `japaneseCulture` para `TryParse` para manter o comportamento consistente. |
| Esperar que o Excel exiba o nome da era | Os formatos de data internos do Excel são apenas gregorianos. Se precisar exibir a era, armazene a string original em uma coluna separada ou crie um formato de texto personalizado. |
| Não descartar o `FileStream` | Use um bloco `using` (como mostrado) para garantir que o manipulador de arquivo seja liberado rapidamente. |
| Misturar objetos `CultureInfo` entre threads | `CultureInfo` é thread‑safe para operações somente leitura, mas evite modificar sua propriedade `Calendar` após a configuração inicial. |

---

## Conclusão

Agora você sabe como **usar CultureInfo do calendário japonês** em C# para analisar datas de era japonesa com precisão e gravar o `DateTime` resultante em uma planilha Excel usando NPOI. O exemplo completo cobre configuração, análise, tratamento de erros e saída para Excel, proporcionando uma base sólida para qualquer cenário de relatórios internacionalizados ou troca de dados.

Em seguida, você pode explorar:

* **Formatar datas com texto personalizado** para manter o nome da era dentro do Excel.
* **Ler datas do Excel** usando `cell.DateCellValue` respeitando o calendário japonês.
* **Aplicar a mesma técnica** a outros calendários baseados em eras (ex.: calendário budista tailandês) trocando `JapaneseCalendar` pela subclasse `Calendar` apropriada.

Sinta‑se à vontade para experimentar diferentes strings de era, conjuntos de dados maiores ou integrar essa lógica em APIs ASP.NET Core que geram relatórios Excel on‑the‑fly. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel com Datas do Calendário Japonês – Guia Completo](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Analisar Datas de Era Japonesa no Excel – Guia Completo para Desenvolvedores C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Como criar pasta de trabalho Excel e analisar datas japonesas em C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}