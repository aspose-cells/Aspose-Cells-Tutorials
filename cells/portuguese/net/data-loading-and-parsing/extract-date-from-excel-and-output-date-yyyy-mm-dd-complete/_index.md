---
category: general
date: 2026-03-18
description: Extrair data do Excel e exibir a data no formato ISO yyyy‑mm‑dd. Aprenda
  a ler datas da era japonesa, convertê‑las e exibir datas ISO em C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: pt
og_description: Extrair data do Excel e gerar data no formato yyyy‑mm‑dd em ISO. Tutorial
  passo a passo em C# com código completo e explicações.
og_title: Extrair data do Excel – Exibir data no formato yyyy‑MM‑dd em C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Extrair data do Excel e exibir data yyyy‑mm‑dd – Guia completo de C#
url: /pt/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair data do Excel – Como gerar data yyyy‑mm‑dd no formato ISO

Já precisou **extrair data do Excel** mas não sabia como lidar com datas do calendário japonês ou obter uma string limpa `yyyy‑mm‑dd`? Você não está sozinho. Em muitos projetos de migração de dados a planilha de origem armazena datas usando o calendário do Imperador japonês, e o sistema downstream espera uma data compatível com ISO como `2024-04-01`.  

Neste guia vamos percorrer uma solução completa e executável que lê uma célula, interpreta a era japonesa e **gera a data yyyy‑mm‑dd**. Ao final, você saberá exatamente como **exibir data no formato ISO** em qualquer aplicativo .NET, e terá um trecho de código reutilizável para inserir em seu próprio projeto.

## O que você vai precisar

- **.NET 6+** (ou .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – a biblioteca que nos permite definir um calendário personalizado ao carregar uma planilha.  
- Um arquivo Excel (`japan-date.xlsx`) que contém uma data armazenada em uma célula com era japonesa (por exemplo `令和3年4月1日`).  
- Uma IDE de sua preferência – Visual Studio, Rider ou até VS Code servem.

Nenhum pacote NuGet adicional é necessário além do Aspose.Cells, e o código funciona no Windows, Linux ou macOS.

## Etapa 1: Configurar o projeto e instalar o Aspose.Cells

Primeiro, crie um aplicativo console:

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Dica profissional:** Se você estiver em um servidor de CI, fixe a versão do pacote (`Aspose.Cells 23.12`) para garantir builds reproduzíveis.

## Etapa 2: Carregar a planilha com o calendário do Imperador japonês

A chave para **extrair data do Excel** quando a origem usa um calendário não gregoriano é informar ao Aspose.Cells qual calendário aplicar ao carregar. Fazemos isso com `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Por que isso importa:** Sem o calendário personalizado, o Aspose.Cells trataria a célula como uma simples string, e você perderia a informação da era. Ao atribuir `JapaneseEmperorCalendar`, a biblioteca converte automaticamente `令和3年4月1日` para `2021‑04‑01` nos bastidores.

## Etapa 3: Recuperar a data de uma célula específica

Agora que a planilha sabe como interpretar a era, podemos ler a célula como um `DateTime`. Vamos supor que a data esteja na primeira planilha, célula **A1** (linha 0, coluna 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Se a célula estiver vazia ou contiver um valor que não seja data, `GetDateTime()` lançará uma exceção. Uma abordagem defensiva fica assim:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Caso de borda:** Alguns arquivos Excel antigos armazenam datas como números (datas seriais). O Aspose.Cells lida com isso automaticamente, mas ainda assim você deve verificar o tipo da célula se esperar conteúdo misto.

## Etapa 4: Gerar data yyyy‑mm‑dd (ISO) e verificar

Com o `DateTime` em mãos, formatá‑lo como **output date yyyy‑mm‑dd** é uma linha única:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Executando o programa contra um arquivo que contém `令和3年4月1日` será impresso:

```
Extracted date (ISO): 2021-04-01
```

Essa é a **display date iso format** exata que muitas APIs exigem.

## Exemplo completo funcional

Juntando todas as peças, aqui está o programa completo, pronto para copiar e colar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Observação:** Substitua `YOUR_DIRECTORY` pela pasta real que contém `japan-date.xlsx`. O código funciona com qualquer planilha e qualquer célula – basta ajustar os índices.

## Manipulando outros calendários (Opcional)

Se precisar **extrair data do Excel** que usa o calendário budista tailandês ou o calendário hebraico, basta trocar a instância do calendário:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

O restante da lógica permanece inalterado, o que demonstra a flexibilidade da abordagem.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| `GetDateTime()` lança `InvalidCastException` | A célula não é uma data (talvez uma string) | Verifique `Cell.Type` antes de chamar, ou use `DateTime.TryParse` em `Cell.StringValue`. |
| Ano incorreto após a conversão | Planilha carregada sem definir `Calendar` | Sempre crie `LoadOptions` com o calendário apropriado **antes** de abrir o arquivo. |
| Saída ISO mostra parte de tempo (`2021-04-01 00:00:00`) | Usou `ToString()` sem especificar formato | Use o especificador de formato `"yyyy-MM-dd"` para forçar **output date yyyy‑mm‑dd**. |
| Arquivo não encontrado | Caminho relativo aponta para a pasta errada | Use `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` ou forneça um caminho absoluto. |

## Dicas avançadas para código pronto para produção

1. **Cacheie a planilha** se precisar ler muitas datas do mesmo arquivo – abrir uma planilha é relativamente custoso.  
2. **Encapsule a lógica de extração** em um método reutilizável:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Registre a string original da era** (`cell.StringValue`) junto com a saída ISO para auditoria.  
4. **Teste unitário** do método com alguns arquivos Excel codificados contendo diferentes eras (Heisei, Reiwa) para garantir a correção.

## Visão geral visual

Abaixo está um diagrama rápido ilustrando o fluxo de dados — da célula Excel à string ISO.  

![Extract date from Excel example showing Excel → LoadOptions → DateTime → ISO string]  

*Texto alternativo: diagrama “extract date from excel” exibindo o pipeline de conversão.*

## Conclusão

Cobrimos tudo o que você precisa para **extrair data do Excel**, lidar com valores de era japonesa e **gerar data yyyy‑mm‑dd** de modo que esteja em conformidade com o **display date iso format** que APIs modernas adoram. A solução é autocontida, funciona com qualquer versão do .NET que suporte Aspose.Cells e pode ser estendida a outros calendários com uma única linha de alteração.

Tem outro calendário em mente? Ou talvez esteja extraindo datas de várias colunas? Sinta‑se à vontade para ajustar o helper `ExtractIsoDate` ou deixar um comentário abaixo. Boa codificação, e que suas datas estejam sempre perfeitamente sincronizadas com o ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}