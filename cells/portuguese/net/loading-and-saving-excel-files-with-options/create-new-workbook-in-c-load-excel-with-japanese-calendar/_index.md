---
category: general
date: 2026-02-26
description: Crie uma nova pasta de trabalho em C# e aprenda a carregar arquivos Excel,
  definir o calendário para japonês e extrair datas do Excel sem esforço.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: pt
og_description: Crie uma nova planilha em C# e aprenda rapidamente como carregar o
  Excel, definir um calendário japonês e extrair datas de arquivos Excel.
og_title: Criar nova pasta de trabalho em C# – Carregar Excel com calendário japonês
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Criar nova pasta de trabalho em C# – Carregar Excel com calendário japonês
url: /pt/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

workbook instance with Japanese calendar settings" should be translated.

But need to keep the URL unchanged.

Also the table content: translate.

Let's produce.

Be careful with bullet points.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho em C# – Carregar Excel com Calendário Japonês

Já precisou **criar nova pasta de trabalho** em C# mas não sabia como fazer o Excel respeitar o calendário japonês? Você não está sozinho. Em muitos cenários corporativos você receberá planilhas que armazenam datas no sistema de eras japonesas, e extrair essas datas corretamente pode parecer decifrar uma linguagem secreta.

A verdade é que você pode **criar nova pasta de trabalho**, instruir o carregador a interpretar datas usando o calendário japonês e então **extrair data do excel** com apenas algumas linhas de código. Neste guia vamos percorrer *como carregar excel*, *como definir calendário* para datas japonesas e, por fim, *ler datas japonesas* de uma célula. Sem enrolação — apenas um exemplo completo e executável que você pode copiar‑colar no seu projeto.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)
- A biblioteca **Aspose.Cells** (versão de avaliação ou licenciada). Instale via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Um arquivo Excel (`JapanDates.xlsx`) que contém datas de era japonesa na célula A1.

É só isso. Se você tem esses itens, podemos começar agora.

---

## Criar Nova Pasta de Trabalho e Definir Calendário Japonês

O primeiro passo é **criar nova pasta de trabalho** e configurar o `LoadOptions` para que o analisador saiba qual calendário usar.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Dica:** A propriedade `LoadOptions.Calendar` aceita vários enums (`Gregorian`, `Japanese`, `Hijri`, etc.). Escolher o correto garante que a biblioteca traduza o texto da era (ex.: “令和3年”) para um `DateTime` do .NET.

![create new workbook example screenshot](image-url.png "Captura de tela mostrando uma nova instância de workbook com configurações de calendário japonês"){: .align-center alt="captura de tela do exemplo de criação de nova pasta de trabalho"}

### Por que isso funciona

- **Criação da Workbook**: `new Workbook()` fornece uma tela limpa — sem planilhas ocultas, sem dados padrão.
- **LoadOptions**: Ao atribuir `CalendarType.Japanese` *antes* de chamar `Load`, o analisador trata quaisquer strings baseadas em era como datas, e não como texto simples.
- **GetDateTime()**: Após o carregamento, `cellA1.GetDateTime()` devolve um verdadeiro objeto `DateTime`, permitindo realizar operações aritméticas, formatação ou inserções em banco de dados sem etapas extras de conversão.

---

## Como Carregar Arquivo Excel Corretamente

Você pode se perguntar: “Existe uma forma especial de **como carregar excel** ao lidar com calendários não gregorianos?” A resposta é sim — sempre defina o `LoadOptions` *antes* de invocar `Load`. Se você carregar primeiro e depois mudar o calendário, as datas já terão sido analisadas incorretamente.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

O trecho acima demonstra uma armadilha comum. A ordem correta (conforme mostrada na seção anterior) garante que o motor interprete as células *como datas* desde o início.

---

## Como Definir Calendário para Datas Japonesas

Se precisar trocar de calendário dinamicamente — por exemplo, processando um lote de arquivos que usam diferentes sistemas de era — você pode reutilizar o mesmo objeto `Workbook` com um novo `LoadOptions` a cada vez.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Chamar `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` produz o mesmo resultado do nosso exemplo principal, enquanto `CalendarType.Gregorian` trataria a mesma célula como uma string simples (ou lançaria uma exceção se o formato for irreconhecível).

---

## Extrair Data do Excel – Lendo Datas Japonesas

Agora que a workbook está carregada com o calendário adequado, extrair a data é simples. O método `Cell.GetDateTime()` devolve um `DateTime` que respeita a conversão de era.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Casos de Borda & Cenários “E Se”

| Situação                                 | O Que Fazer                                                                                              |
|------------------------------------------|----------------------------------------------------------------------------------------------------------|
| A célula contém **texto** em vez de data | Chame `cell.GetString()` primeiro, valide com `DateTime.TryParse`, ou imponha validação de dados no Excel. |
| Várias planilhas precisam ser processadas | Percorra `workbook.Worksheets` e aplique a mesma lógica de extração em cada planilha.                     |
| Datas são armazenadas como **números** (serial do Excel) | `cell.GetDateTime()` ainda funciona porque o Aspose.Cells converte automaticamente números seriais.      |
| O arquivo está **protegido por senha**  | Defina `LoadOptions.Password = "yourPwd"` antes de chamar `Load`.                                      |

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um aplicativo console. Ele inclui tratamento de erros e demonstra todas as quatro palavras‑chave secundárias em contexto.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Saída esperada** (supondo que A1 contenha “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Se a célula contiver uma data gregoriana como “2021‑05‑12”, o mesmo código ainda funciona porque a biblioteca recua graciosamente para a interpretação gregoriana.

---

## Conclusão

Agora você sabe como **criar nova pasta de trabalho**, **como carregar excel** corretamente, definir o **como definir calendário** apropriado e, finalmente, **extrair data do excel** enquanto **lê datas japonesas** sem necessidade de parsing manual. O ponto principal é que o calendário deve ser definido *antes* do carregamento; uma vez que a workbook está em memória, as datas já foram materializadas como objetos `DateTime` adequados.

### O que vem a seguir?

- **Processamento em lote**: Percorra uma pasta de arquivos, chamando `LoadWithCalendar` para cada um.
- **Exportar para outros formatos**: Use `workbook.Save("output.csv")` após a conversão.
- **Localização**: Combine `CultureInfo` com `DateTime.ToString` para exibir datas no idioma preferido do usuário.

Sinta-se à vontade para experimentar — troque `CalendarType.Japanese` por `CalendarType.Hijri` ou `CalendarType.Gregorian` e veja o mesmo código se adaptar automaticamente. Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação do Aspose.Cells para aprofundar nos detalhes da API.

Boa codificação, e aproveite transformar aquelas misteriosas datas de era japonesa em valores .NET `DateTime` limpos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}