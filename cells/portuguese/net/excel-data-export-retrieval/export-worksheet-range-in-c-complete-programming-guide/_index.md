---
category: general
date: 2026-05-04
description: Exportar intervalo da planilha usando C# com formatação personalizada.
  Aprenda como exportar um intervalo do Excel e como personalizar a exportação de
  células em alguns passos fáceis.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: pt
og_description: Exportar intervalo de planilha com C#. Este guia mostra como exportar
  intervalos do Excel e personalizar a exportação de células de forma rápida e confiável.
og_title: Exportar intervalo de planilha em C# – Guia completo de programação
tags:
- C#
- Excel
- Data Export
title: Exportar intervalo de planilha em C# – Guia completo de programação
url: /pt/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar intervalo de planilha em C# – Guia de Programação Completo

Já precisou **exportar intervalo de planilha** mas a saída padrão não era o que você queria? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao tentar extrair um bloco de células para um arquivo CSV ou JSON. A boa notícia? Com algumas linhas de C# você pode não apenas **exportar intervalo do Excel** mas também **personalizar a exportação de células** para corresponder a qualquer formato de destino.

Neste tutorial, percorreremos um cenário real: pegar as células *A1:D10* de uma pasta de trabalho Excel, transformar cada valor em uma string entre colchetes e gravar o resultado em um arquivo. Ao final, você saberá exatamente **como exportar intervalo de planilha** com controle total sobre a representação de cada célula, além de algumas dicas para casos extremos que você pode encontrar mais tarde.

## O que você precisará

- .NET 6 ou posterior (o código também funciona com .NET Framework 4.7+)  
- O pacote NuGet **GemBox.Spreadsheet** (ou qualquer biblioteca que ofereça `ExportTableOptions`; a API mostrada é da GemBox)  
- Um entendimento básico da sintaxe C# – nada sofisticado, apenas as declarações `using` habituais e a criação de objetos  

Se você tem isso, está pronto para mergulhar.

## Etapa 1: Configurar as Opções de Exportação – Ponto de Controle Principal  

A primeira coisa que você faz é criar uma instância de `ExportTableOptions` e instruí‑la a tratar cada célula como string. Esta é a base para **como exportar intervalo do Excel** mantendo o tipo de dado consistente.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Por que forçar a exportação como string?*  
Quando você personalizar cada célula mais tarde, inserirá colchetes e possivelmente outros símbolos. Manter tudo como string evita surpresas de conversão de tipo (por exemplo, datas se transformando em números seriais).

## Etapa 2: Conectar ao Evento CellExport – Personalizando Cada Célula  

Agora vem a parte divertida: **como personalizar a exportação de célula**. O GemBox dispara um evento `CellExport` para cada célula que está prestes a ser escrita. Ao tratá‑lo, você pode envolver o valor em colchetes, prefixar um texto ou até mesmo pular uma célula completamente.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Dica de especialista:* Se você quiser modificar apenas células numéricas, verifique `e.Value.GetType()` antes de aplicar os colchetes. Essa pequena verificação pode evitar que você altere acidentalmente o texto do cabeçalho.

## Etapa 3: Exportar o Intervalo Desejado – A Ação Principal  

Com as opções prontas, você chama `ExportTable`. O método recebe a pasta de trabalho que você carregou, o endereço do intervalo desejado e as opções que você acabou de configurar.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

A sobrecarga que usamos grava diretamente em um arquivo (CSV por padrão). Se preferir uma string em memória, troque o último argumento por um `StringWriter` e leia o resultado depois.

### Exemplo Completo Funcional

Abaixo está um aplicativo de console autônomo que você pode colar em um novo projeto e executar imediatamente (basta substituir os caminhos dos arquivos).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Saída esperada (trecho CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Cada célula de *A1* a *D10* agora está envolvida em colchetes quadrados, exatamente como definimos no manipulador `CellExport`.

## Lidando com Casos Limite Comuns  

### 1. Células Vazias  
Se uma célula estiver vazia, `e.Value` será `null`. Tentar formatá‑la com interpolação de string lança uma exceção. Proteja‑se contra isso:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Intervalos Grandes  
Exportar milhões de linhas pode atingir limites de memória. Nesse cenário, faça streaming da saída em vez de carregar toda a pasta de trabalho na memória:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Delimitadores Diferentes  
CSV não é o único formato que você pode precisar. Altere o delimitador ajustando `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Perguntas Frequentes  

**Q: Isso funciona com arquivos .xlsx criados pelo Excel 365?**  
Absolutamente. O GemBox lê o formato OpenXML moderno sem configuração extra.

**Q: Posso exportar vários intervalos não contíguos de uma vez?**  
Não diretamente por uma única chamada `ExportTable`. Percorra cada string de intervalo (`"A1:D10"`, `"F1:H5"` etc.) e concatene as saídas você mesmo.

**Q: E se eu precisar aplicar formatações diferentes por coluna?**  
Dentro do manipulador `CellExport` você tem acesso a `e.ColumnIndex`. Use uma instrução `switch` para aplicar lógica específica por coluna.

## Conclusão  

Cobremos **como exportar intervalo de planilha** com controle total sobre a aparência de cada célula, demonstramos **como exportar intervalo do Excel** usando `ExportTableOptions` e mostramos **como personalizar a exportação de célula** via o evento `CellExport`. A solução completa está em algumas dezenas de linhas de C#, mas é flexível o suficiente para cenários de produção.

Próximos passos? Experimente substituir o envoltório de colchetes por um formato compatível com JSON, ou experimente lógica condicional que pula linhas ocultas. Você também pode explorar a exportação direta para um `MemoryStream` para respostas de web‑API—sem necessidade de arquivos temporários.

Se você acompanhou, agora tem um padrão sólido e reutilizável para exportar qualquer intervalo de planilha exatamente da maneira que precisar. Boa codificação, e sinta‑se à vontade para deixar um comentário se encontrar algum problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}