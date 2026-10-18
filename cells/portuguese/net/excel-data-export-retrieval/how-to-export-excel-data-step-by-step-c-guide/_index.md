---
category: general
date: 2026-03-29
description: Aprenda como exportar tabelas do Excel para texto simples, gravar strings
  em arquivo e converter tabelas do Excel para CSV ou TXT usando C#. Inclui código
  completo e dicas.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: pt
og_description: Como exportar tabelas do Excel para arquivos de texto em C#. Obtenha
  a solução completa, o código e as melhores práticas para converter tabelas do Excel
  e salvar arquivos TXT.
og_title: Como Exportar Dados do Excel – Tutorial Completo de C#
tags:
- C#
- Excel
- File I/O
title: Como Exportar Dados do Excel – Guia C# Passo a Passo
url: /pt/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Dados do Excel – Guia Completo em C#

Já se perguntou **como exportar dados do Excel** sem abrir a planilha manualmente? Talvez você precise despejar uma tabela em um arquivo de texto simples para um sistema legado, ou queira uma exportação rápida em CSV para pipelines de análise de dados. Neste tutorial vamos percorrer uma solução prática, de ponta a ponta, que **escreve uma string em arquivo** e mostra exatamente como **converter tabela do Excel** em um formato de texto delimitado usando C#.

Cobriremos tudo, desde o carregamento da pasta de trabalho, a escolha da tabela correta, a configuração das opções de exportação e, finalmente, a gravação do resultado como um arquivo `.txt`. Ao final, você será capaz de **exportar tabela como CSV** (ou qualquer delimitador que escolher) e verá alguns truques úteis para **salvar arquivo txt C#** em projetos. Nenhuma ferramenta externa necessária — apenas alguns pacotes NuGet e um pouco de código.

---

## O Que Você Precisa

- **.NET 6.0+** (ou .NET Framework 4.7.2 se preferir o clássico)
- Pacote NuGet **Syncfusion.XlsIO** (a classe `ExportTableOptions` está aqui)
- Um IDE básico de C# (Visual Studio, VS Code, Rider — qualquer um serve)
- Uma pasta de trabalho Excel que contenha ao menos uma tabela (usaremos `ws.Tables[0]` no exemplo)

> Dica de especialista: Se ainda não tem a biblioteca Syncfusion, execute  
> `dotnet add package Syncfusion.XlsIO.Net.Core` no terminal.

---

## Etapa 1 – Abrir a Pasta de Trabalho e Capturar a Primeira Tabela  

A primeira coisa é carregar o arquivo Excel e obter uma referência à planilha que contém a tabela. Esta etapa é crucial porque a operação **convert excel table** funciona em um objeto `ITable`, não em intervalos de células brutas.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Por que isso importa:* Abrir a pasta de trabalho com `using` garante que todos os recursos não gerenciados sejam liberados, evitando problemas de bloqueio de arquivo mais tarde quando você tentar **write string to file**.

---

## Etapa 2 – Configurar Opções de Exportação (Texto Simples, Sem Cabeçalhos, Delimitador ponto‑e‑vírgula)  

Agora informamos à Syncfusion como queremos que a tabela seja serializada. O `ExportTableOptions` permite alternar a inclusão de cabeçalhos, escolher um delimitador e decidir se queremos obter uma string ou um array de bytes.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Por que isso importa:* Definir `IncludeHeaders = false` costuma atender às expectativas de sistemas downstream que já conhecem a ordem das colunas. Alterar o delimitador é como você **exporta tabela como CSV** com um separador personalizado.

---

## Etapa 3 – Exportar a Tabela para uma String  

Com as opções prontas, chamamos `ExportToString`. Este método extrai toda a tabela (incluindo todas as linhas) e devolve uma única string pronta para ser gravada em arquivo.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Por que isso importa:* A chamada `ExportToString` faz o trabalho pesado de converter a grade do Excel em um formato delimitado. Ela respeita o `Delimiter` que você definiu, então você obtém um resultado **export table as csv** limpo sem processamento extra.

---

## Etapa 4 – Gravar o Texto Exportado em um Arquivo  

Finalmente, persistimos a string no disco. `File.WriteAllText` é a maneira mais simples de **save txt file C#**; ele cria o arquivo automaticamente se ele não existir e o sobrescreve caso exista.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Por que isso importa:* Ao gravar a string diretamente, você evita uma etapa extra de conversão. O arquivo agora contém linhas como `Value1;Value2;Value3`, pronto para qualquer analisador downstream.

---

## Exemplo Completo (Todas as Etapas em Um Só Lugar)  

A seguir está o programa completo, pronto para copiar‑colar, que combina tudo o que discutimos. Inclui tratamento de erros e comentários para clareza.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Saída esperada** (o conteúdo de `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Cada linha corresponde a uma linha da tabela Excel original, com valores separados por ponto‑e‑vírgula. Se você mudar `Delimiter = ","` obterá um arquivo CSV clássico.

---

## Perguntas Frequentes & Casos de Borda  

### E se Minha Pasta de Trabalho Tiver Múltiplas Tabelas?  
Você pode simplesmente mudar `ws.Tables[0]` para o índice apropriado, ou percorrer `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Como Incluir Cabeçalhos de Coluna?  
Defina `IncludeHeaders = true` em `ExportTableOptions`. Isso é útil quando o sistema downstream espera uma linha de cabeçalho.

### Posso Exportar para uma Pasta Diferente Dinamicamente?  
Claro. Use `Path.Combine` com `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` ou qualquer caminho fornecido pelo usuário para tornar a solução mais flexível.

### E Quanto a Arquivos Grandes?  
Para tabelas massivas, considere transmitir a saída ao invés de carregar a string inteira na memória:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Isso Funciona no .NET Core?  
Sim — Syncfusion.XlsIO suporta .NET 5/6/7. Basta referenciar o pacote NuGet adequado e está tudo pronto.

---

## Dicas Profissionais para Exportações Confiáveis  

- **Valide o caminho do arquivo** antes de gravar. Um diretório inexistente lançará `DirectoryNotFoundException`.  
- **Use `ExportAsString`** apenas quando a tabela couber confortavelmente na memória; caso contrário, utilize `ExportToStream` para conjuntos de dados enormes.  
- **Fique atento à cultura**: se seus dados contêm vírgulas como separadores decimais, escolha um delimitador ponto‑e‑vírgula (`;`) ou tab (`\t`) para evitar erros de análise CSV.  
- **Bloqueio de versão**: a Syncfusion ocasionalmente altera assinaturas de API. Fixe a versão do NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) para manter sua build reprodutível.

---

## Conclusão  

Neste guia demonstramos **como exportar tabelas do Excel** para arquivos de texto simples usando C#. Ao carregar a pasta de trabalho, configurar `ExportTableOptions`, exportar a tabela para uma string e, finalmente, **escrever a string em arquivo**, você agora possui um padrão robusto para **convert excel table**, **export table as csv** e tarefas de **save txt file C#**.  

Sinta-se à vontade para experimentar — troque o delimitador, inclua cabeçalhos ou percorra múltiplas tabelas. A mesma abordagem serve para gerar relatórios CSV, alimentar parsers legados ou simplesmente arquivar o conteúdo de planilhas como arquivos de texto leves.

Tem mais cenários que gostaria de abordar? Talvez precise **write string to file** de forma assíncrona, ou queira compactar a saída em tempo real. Confira nossos próximos tutoriais sobre *asynchronous file I/O in C#* e *zipping files with .NET* para manter o ritmo.

Boa codificação! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}