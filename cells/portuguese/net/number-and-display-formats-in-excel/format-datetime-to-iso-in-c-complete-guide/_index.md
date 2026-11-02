---
category: general
date: 2026-03-22
description: Aprenda a formatar datetime para ISO ao extrair a data do Excel e exibir
  a data ISO usando Aspose.Cells em C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: pt
og_description: Formatar data e hora para ISO ficou fácil. Este guia mostra como extrair
  a data do Excel e exibir a data ISO com Aspose.Cells.
og_title: formatar DateTime para ISO em C# – Tutorial passo a passo
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formatar DateTime para ISO em C# – Guia Completo
url: /pt/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatar datetime para ISO em C# – Guia Completo

Já precisou **formatar datetime para iso** mas a fonte está dentro de uma planilha Excel? Talvez a célula contenha uma era japonesa como “令和3年5月1日” e você esteja se perguntando como transformar isso em uma string limpa `2021‑05‑01`. Você não está sozinho. Neste tutorial vamos **extrair data do excel**, analisar a era japonesa e então **exibir data iso** no console — tudo com algumas linhas de C# e Aspose.Cells.

Vamos percorrer tudo o que você precisa: o pacote NuGet necessário, o código exato que você pode copiar‑colar, por que cada linha importa e algumas dicas de casos extremos. Ao final você terá um snippet reutilizável que formata datetime para iso não importa quão excêntrica seja a data original no Excel.

## O que você precisará

- .NET 6.0 ou superior (o código também compila no .NET Framework 4.6+)
- Visual Studio 2022 (ou qualquer editor de sua preferência)
- **Aspose.Cells for .NET** pacote NuGet – `Install-Package Aspose.Cells`
- Um arquivo Excel (ou uma nova workbook) que contenha uma data no formato de era japonesa

É isso. Nenhuma biblioteca extra, sem interop COM, apenas um único método bem documentado.

## Etapa 1: Criar uma Workbook e gravar uma data em era japonesa  

Primeiro, precisamos de uma workbook para trabalhar. Se você já tem um arquivo Excel, pode carregá‑lo com `new Workbook("path")`. Para este exemplo criaremos uma nova workbook na memória e inseriremos uma string de era japonesa na célula **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Por que fazemos isso:** Aspose.Cells trata os valores das células como strings por padrão. Ao inserir o texto bruto da era simulamos um cenário real onde um cliente japonês inseriu datas em seu calendário nativo.

## Etapa 2: Habilitar a análise de era japonesa e extrair a data  

Aspose.Cells pode traduzir automaticamente strings de era japonesa em objetos .NET `DateTime` — desde que você indique isso. A flag `DateTimeParseOptions.EnableJapaneseEra` faz o trabalho pesado.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Dica profissional:** Se você esquecer a opção `EnableJapaneseEra`, a biblioteca retornará a string original e a conversão subsequente falhará. Sempre verifique `parsed.Type` se estiver lidando com conteúdo misto.

## Etapa 3: Converter o DateTime analisado para ISO 8601  

Agora que temos um `DateTime` adequado, transformá‑lo em uma string formatada em ISO é muito simples. O padrão `"yyyy-MM-dd"` está em conformidade com a parte de data do ISO 8601, que é o que a maioria das APIs espera.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Executar o programa imprime:

```
ISO date: 2021-05-01
```

Esse é o **exibir data iso** que você procurava.

## Exemplo completo e executável  

A seguir está o bloco de código completo que você pode copiar direto para um projeto de console. Sem dependências ocultas, sem configuração extra.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Saída esperada:** `ISO date: 2021-05-01`

## Análise passo a passo (Por que cada parte importa)

| Etapa | O que acontece | Por que é importante |
|------|----------------|----------------------|
| **Create workbook** | Inicializa um contêiner Excel em memória. | Fornece um sandbox para testar sem tocar no sistema de arquivos. |
| **PutValue** | Armazena a string bruta da era japonesa em **A1**. | Simula a entrada real de dados; garante que o analisador veja o texto exato. |
| **GetValue with `EnableJapaneseEra`** | Converte a string da era em um .NET `DateTime`. | Lida com a conversão de calendário automaticamente — sem necessidade de tabelas de consulta manuais. |
| **`ToString("yyyy-MM-dd")`** | Formata o `DateTime` para ISO 8601. | Garante uma string de data invariável à cultura, ordenável e aceita por APIs REST, bancos de dados, etc. |
| **Console.WriteLine** | Exibe a data ISO final. | Confirma que todo o pipeline funciona de ponta a ponta. |

## Lidando com variações comuns  

### 1. Diferentes localizações de célula  

Se sua data está em **B2** ou em um intervalo nomeado, basta substituir `"A1"` pelo endereço apropriado:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Múltiplas datas em uma coluna  

Quando precisar **extrair data do excel** para muitas linhas, faça um loop pelo intervalo usado:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Alternativa para datas sem era  

Se uma célula já contém uma string de data padrão, o analisador ainda funciona, mas você pode querer uma rede de segurança:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

A flag `TryParse` impede exceções e devolve o valor original se a conversão falhar.

### 4. Componente de tempo  

Caso precise também da parte de horário, use `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Isso gera um timestamp ISO 8601 completo (`2021-05-01T00:00:00`).

## Ilustração visual  

![exemplo de formatação datetime para iso](image.png "Um exemplo de formatação datetime para iso em C#")

*Texto alternativo:* *exemplo de formatação datetime para iso mostrando a saída do console*

## Perguntas Frequentes  

- **Posso usar isso com arquivos .xls?**  
  Sim. Aspose.Cells suporta `.xls`, `.xlsx`, `.csv` e muitos outros formatos nativamente.

- **E se a workbook estiver protegida por senha?**  
  Carregue-a com `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **O formato ISO depende da localidade?**  
  Não. O padrão `"yyyy-MM-dd"` é invariável à cultura, garantindo a mesma string em qualquer máquina.

- **Isso funciona no .NET Core?**  
  Absolutamente — Aspose.Cells é compatível com .NET Standard 2.0.

## Conclusão  

Cobremos como **formatar datetime para iso** ao **extrair data do excel**, analisar strings de era japonesa e finalmente **exibir data iso** no console. Os passos principais — criar uma workbook, gravar ou carregar o texto da era, habilitar a análise de era japonesa e formatar com `ToString("yyyy-MM-dd")` — são tudo que você precisa na maioria dos cenários.

A seguir, você pode querer:

- Gravar as datas ISO de volta em outra coluna para processamento posterior.
- Exportar a workbook transformada para CSV para importação em massa.
- Combinar essa lógica com uma API web que aceita uploads de Excel e devolve datas ISO codificadas em JSON.

Sinta‑se à vontade para experimentar diferentes formatos de data, fusos horários ou até calendários personalizados. A flexibilidade do Aspose.Cells significa que raramente você encontrará um obstáculo.

Happy coding, and may all your dates be perfectly ISO‑compliant!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}