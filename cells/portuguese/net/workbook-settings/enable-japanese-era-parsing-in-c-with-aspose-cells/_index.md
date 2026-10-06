---
category: general
date: 2026-05-30
description: Habilite a análise de eras japonesas em C# usando Aspose.Cells. Aprenda
  a definir a cultura da pasta de trabalho, analisar datas de eras e lidar com o calendário
  japonês em planilhas do Excel.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: pt
og_description: Habilite a análise de eras japonesas em C# com Aspose.Cells. Este
  guia mostra como definir a cultura da pasta de trabalho, habilitar o suporte a eras
  e trabalhar com datas japonesas.
og_title: Ativar a Análise de Era Japonesa em C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Habilitar a análise da era japonesa em C# com Aspose.Cells
url: /pt/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Habilitar a Análise de Era Japonesa em C# com Aspose.Cells

Já precisou **habilitar a análise de era japonesa** ao gerar arquivos Excel para um cliente do Japão? Você não está sozinho—muitos desenvolvedores se deparam com dificuldades quando o calendário japonês legado (令和, 平成, etc.) aparece nos dados. A boa notícia é que o Aspose.Cells torna muito fácil reconhecer essas datas de era e convertê‑las em valores gregorianos padrão.

Neste tutorial vamos percorrer os passos exatos para **habilitar a análise de era japonesa** usando Aspose.Cells, definir a cultura da pasta de trabalho para japonês e inserir uma data formatada por era em uma célula. Ao final, você terá um trecho de código C# executável que analisa “令和3年5月1日” e o converte para o objeto de data `2021‑05‑01`. Não é necessário consultar documentação externa—basta copiar, colar e executar.

## Pré‑requisitos

- .NET 6.0 ou superior (o código funciona com .NET Core, .NET Framework e .NET 5+)
- Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`)
- Conhecimento básico de C#—se você sabe escrever um `Console.WriteLine`, está pronto
- Uma IDE de sua escolha (Visual Studio, VS Code, Rider…)

> **Dica de especialista:** Mantenha sua versão do Aspose.Cells atualizada; a versão 24.10+ inclui as definições mais recentes de eras japonesas.

## Por que Habilitar a Análise de Era Japonesa?

Os calendários japoneses utilizam eras vinculadas aos reinados imperiais. Para a maioria das aplicações modernas você desejará armazenar datas no formato gregoriano familiar, mas os dados de origem podem ainda chegar como “令和3年5月1日”. Se você ignorar **habilitar a análise de era japonesa**, a string será tratada como texto simples, quebrando cálculos, ordenação e gráficos. Ao ativar o suporte a eras, o Aspose.Cells converte automaticamente essas strings em valores `DateTime` corretos, preservando tanto a legibilidade para usuários japoneses quanto a correção numérica para o processamento posterior.

## Etapa 1: Definir a Cultura da Pasta de Trabalho para Japonês

A primeira coisa a fazer é informar ao Aspose.Cells que a localidade padrão da pasta de trabalho é japonesa (`ja-JP`). Isso garante que qualquer análise dependente de cultura (incluindo nomes de eras) siga as regras japonesas.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Por que isso importa:** O objeto `CultureInfo` controla formatos numéricos, separadores de data e, mais importante para nós, o sistema de calendário usado ao analisar strings.

## Etapa 2: Habilitar a Análise de Era Japonesa

Agora que a cultura está definida, você precisa ativar a opção que indica ao Aspose.Cells para reconhecer datas de era. Este é o núcleo de **habilitar a análise de era japonesa**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Armadilha comum:** Esquecer essa flag faz com que “令和3年5月1日” permaneça como uma string literal. Com ela ativada, o Aspose.Cells mapeia a era para o ano gregoriano correto automaticamente.

## Etapa 3: Inserir uma Data Formatada por Era em uma Célula

Com a cultura e o suporte a eras prontos, inserir uma string de era japonesa é simples. A biblioteca a analisará e armazenará um verdadeiro valor `DateTime`.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Saída Esperada

- **Célula A1** no `JapaneseEraDemo.xlsx` gerado exibirá **2021‑05‑01** (ou o formato de data japonês localizado se você abrir no Excel com a localidade japonesa).
- O valor subjacente é um verdadeiro `DateTime`, portanto pode ser usado com segurança em fórmulas, tabelas dinâmicas ou cálculos adicionais em C#.

## Etapa 4: Verificar a Data Analisada Programaticamente (Opcional)

Se quiser confirmar que a análise foi bem‑sucedida antes de salvar, você pode ler a célula novamente:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Esta pequena verificação é útil em testes unitários ou ao processar arquivos Excel fornecidos por usuários.

## Casos Limites & Variações

| Cenário | O que Fazer |
|----------|------------|
| **Múltiplas eras em uma única pasta de trabalho** | Mantenha `UseJapaneseEra = true`; o Aspose.Cells reconhecerá todas as eras suportadas (令和, 平成, 昭和, 大正, 明治). |
| **Strings gregorianas e de era misturadas** | O analisador distingue automaticamente; strings gregorianas permanecem inalteradas. |
| **Requisitos de calendário personalizados** | Ainda é possível definir `Workbook.Settings.Calendar` para uma instância específica de `Calendar` se precisar de mais controle. |
| **Versões mais antigas do .NET** | O mesmo código funciona no .NET Framework 4.6+; apenas certifique‑se de que o construtor `System.Globalization.CultureInfo` está disponível. |

## Dicas Práticas para Projetos Reais

- **Cache o CultureInfo** se estiver criando muitas pastas de trabalho em um loop; construí‑lo repetidamente gera sobrecarga.
- **Valide a entrada** antes de chamar `PutValue`; strings de era malformadas lançarão uma exceção.
- **Desative a análise de era** (`UseJapaneseEra = false`) quando tiver certeza de que os dados nunca contêm datas de era—isso pode melhorar levemente o desempenho.
- **Use `Workbook.SaveOptions`** para controlar o formato de saída (XLSX, XLS, CSV) mantendo a data analisada.

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Execute o programa, abra o arquivo gerado e você verá **2021‑05‑01** na célula A1—prova de que conseguimos **habilitar a análise de era japonesa** com sucesso.

## Conclusão

Acabamos de demonstrar como **habilitar a análise de era japonesa** em C# usando Aspose.Cells, definir a cultura da pasta de trabalho e converter perfeitamente datas de era como “令和3年5月1日” em valores gregorianos padrão. Os passos são mínimos, o código é autocontido e o resultado funciona perfeitamente no Excel.

Pronto para o próximo desafio? Experimente combinar **definir a cultura da pasta de trabalho** com formatação numérica para iene japonês, ou gerar um relatório de múltiplas planilhas que mescla datas gregorianas e de era. Agora você tem a base para lidar com quaisquer peculiaridades do calendário japonês em seus projetos de automação Excel .NET.

---

*Se este guia foi útil, considere dar uma estrela ao repositório Aspose.Cells no GitHub ou compartilhar suas próprias dicas nos comentários. Boa codificação!*

## O Que Você Deve Aprender a Seguir?

- [Load Excel Workbooks with Culture-Specific Dates using Aspose.Cells for .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Load Workbook Culture Specific Dates Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}