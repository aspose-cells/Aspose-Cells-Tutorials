---
category: general
date: 2026-02-09
description: Limpe a interface de filtro no Excel com C# removendo o botão AutoFilter.
  Aprenda como ocultar o botão de filtro, exibir a linha de cabeçalho e manter suas
  planilhas organizadas.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: pt
og_description: Limpar interface de filtro no Excel usando C#. Este guia mostra como
  ocultar o botão de filtro, exibir a linha de cabeçalho e manter as planilhas limpas.
og_title: Limpar a interface de filtro no Excel com C# – Remover o botão AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Limpar interface de filtro no Excel com C# – Remover botão AutoFilter
url: /pt/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interface de filtro limpa no Excel com C# – Remover o botão AutoFilter

Já precisou **limpar a interface de filtro** em uma planilha Excel, mas não sabia qual linha de código realmente oculta aquela pequena seta suspensa? Você não está sozinho. O botão de filtro pode ser incômodo quando você entrega um relatório para usuários finais que nunca precisam mudar a visualização.  

Neste tutorial vamos percorrer um exemplo completo e executável que **remove o botão AutoFilter** de uma tabela, garante que a linha de cabeçalho permaneça visível e ainda aborda como *ocultar o botão de filtro* de forma permanente. Ao final, você saberá exatamente **como remover o AutoFilter** em C# e por que cada passo é importante.

## O que você vai precisar

- .NET 6+ (ou .NET Framework 4.7.2+) – qualquer runtime recente funciona.
- O pacote NuGet **EPPlus** (versão 6.x ou superior) – ele fornece `ExcelWorksheet`, `ExcelTable`, etc.
- Um arquivo Excel simples com uma tabela chamada **SalesTable** (sinta-se à vontade para criar uma em poucos cliques).

É só isso. Sem interop COM, sem DLLs extras, apenas algumas instruções `using` e algumas linhas de código.

## Interface de filtro limpa: Removendo o botão AutoFilter

O cerne da solução está em três pequenas instruções. Vamos detalhá‑las para que você entenda *por que* são necessárias, não apenas *o que* fazem.

### Etapa 1 – Obter uma referência à tabela

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Por que isso importa: o EPPlus trabalha com **tabelas** (`ExcelTable`), não com intervalos brutos. Ao obter o objeto da tabela, ganhamos acesso à propriedade `AutoFilter`, que controla o elemento de UI que você vê na planilha. Se você tentar manipular a planilha diretamente, afetará apenas os valores, não o botão de filtro.

### Etapa 2 – Remover a linha do botão AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Definir `AutoFilter` como `null` indica ao EPPlus que deve excluir a linha de filtro subjacente. Esta é a operação de *limpar a interface de filtro* que a maioria dos desenvolvedores procura quando perguntam “**como remover autofilter**”. É uma abordagem limpa, de uma única linha, que funciona em qualquer versão do Excel suportada pelo EPPlus.

### Etapa 3 – Manter a linha de cabeçalho visível

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Ao remover a UI de filtro, o Excel pode, às vezes, ocultar a linha de cabeçalho se a flag `ShowHeader` da tabela estiver falsa. Definindo‑a explicitamente como `true` garantimos que os títulos das colunas permaneçam na tela – um detalhe sutil, mas importante, para um relatório final bem apresentado.

### Exemplo completo e executável

A seguir, um aplicativo console mínimo que abre uma pasta de trabalho existente, executa as três etapas e salva o resultado. Copie‑e‑cole, pressione **F5** e veja o botão de filtro desaparecer.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Resultado esperado:** Abra *SalesReport_NoFilter.xlsx* – as setas de filtro desapareceram, mas os cabeçalhos das colunas permanecem. Chega de “clique‑para‑filtrar” poluindo a UI.

> **Dica de especialista:** Se você tem **várias tabelas** e deseja ocultar o botão de filtro em todas elas, percorra `worksheet.Tables` e aplique as mesmas três linhas dentro do loop.

## Como remover o AutoFilter no Excel usando C# – um mergulho mais profundo

Você pode se perguntar: “E se a pasta de trabalho já tiver um filtro aplicado? Definir `AutoFilter = null` também limpa as linhas filtradas?” A resposta é **sim**. O EPPlus limpa tanto a UI quanto os critérios de filtro subjacentes, deixando os dados na ordem original.  

Se você quiser apenas *ocultar* o botão, mas manter o filtro ativo, pode definir a propriedade `AutoFilter` para um **novo filtro vazio**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Essa variação é útil quando você deseja *ocultar o botão de filtro* para um visual mais limpo, mas ainda permitir que usuários avançados ativem filtros via VBA ou pela faixa de opções.

### Caso especial: Tabelas sem linha de cabeçalho

Alguns relatórios legados usam intervalos simples em vez de tabelas. Nesse cenário, o EPPlus não expõe um objeto `ExcelTable`, então o código acima lançará uma exceção. A solução alternativa é **converter o intervalo em uma tabela** primeiro:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Agora você *removeu autofilter excel* estilo UI mesmo em um intervalo que começou sem uma tabela formal.

## Mostrar a linha de cabeçalho após ocultar o botão de filtro – por que isso importa

Uma reclamação comum é que, depois de ocultar a UI de filtro, a linha de cabeçalho às vezes desaparece, especialmente quando a pasta de trabalho foi criada originalmente com “Ocultar Cabeçalho” ativado. Definindo explicitamente `salesTable.ShowHeader = true;` evitamos essa surpresa.  

Se precisar **ocultar o botão de filtro** mas manter o cabeçalho oculto (talvez ao gerar um dump bruto de dados), basta definir `salesTable.ShowHeader = false;` após limpar o filtro. O código é simétrico, o que facilita alternar com base em uma flag de configuração.

## Ocultar o botão de filtro – dicas práticas e armadilhas

- **Compatibilidade de versão:** EPPlus 6+ funciona apenas com arquivos `.xlsx`. Se você estiver lidando com o formato antigo `.xls`, precisará de outra biblioteca (por exemplo, NPOI) porque a API de *limpar a interface de filtro* não está disponível.
- **Desempenho:** Carregar uma pasta de trabalho enorme só para ocultar um botão pode ser lento. Considere usar `ExcelPackage.Load(stream, true)` para abrir em modo **somente‑leitura**, aplicar a alteração e, em seguida, salvar.
- **Testes:** Sempre valide o arquivo de saída manualmente na primeira vez. Testes automatizados de UI podem verificar se as setas de filtro realmente desapareceram (`worksheet.Tables[0].AutoFilter == null`).
- **Licenciamento:** O EPPlus mudou para uma licença dupla na versão 5. Para projetos comerciais, você precisará de uma licença paga ou mudar para uma biblioteca alternativa.

## Arquivo fonte completo para copiar‑e‑colar

A seguir está o arquivo exato que você pode inserir em um novo projeto console. Sem dependências ocultas, tudo está contido.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Execute `dotnet add package EPPlus --version 6.0.8` (ou a versão mais recente) antes de compilar, e você terá uma planilha limpa pronta para distribuição.

## Conclusão

Acabamos de **mostrar como remover o AutoFilter** e **limpar a interface de filtro** em uma pasta de trabalho Excel usando C#. O núcleo de três linhas (`AutoFilter = null;`, `ShowHeader = true;`) faz o trabalho pesado, enquanto a estrutura ao redor torna a solução

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}