---
category: general
date: 2026-07-03
description: Aprenda como exportar uma tabela do Excel para um arquivo .txt e salvar
  a tabela do Excel em um arquivo .txt usando C#. Exporte os dados do Excel como texto
  simples com um exemplo de código completo.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: pt
og_description: Como exportar tabela do Excel como texto simples. Este guia mostra
  como exportar dados do Excel como texto simples e salvar a tabela do Excel em um
  arquivo .txt com Aspose.Cells.
og_title: Como Exportar Tabela do Excel – Tutorial Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Como Exportar Tabela do Excel – Guia Completo Passo a Passo
url: /pt/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Tabela do Excel – Guia Completo Passo a Passo

Já se perguntou **como exportar tabela do Excel** sem carregar toda a pasta de trabalho na memória? Você não está sozinho. Em muitas tarefas de automação, o sistema downstream aceita apenas um arquivo simples `.txt`, então você precisa **salvar tabela do Excel em um arquivo .txt** de forma rápida e confiável.  

Neste tutorial vamos percorrer uma solução limpa em C# que **exporta dados do Excel como texto simples** usando Aspose.Cells. Ao final você terá um programa pronto‑para‑executar, entenderá por que cada linha importa e verá como ajustar a exportação para seus próprios casos de borda.

## O que você precisará

- **Aspose.Cells for .NET** (qualquer versão recente, por exemplo, 23.12).  
- .NET 6 SDK ou posterior – o código também compila com .NET Core.  
- Um arquivo de exemplo `input.xlsx` que contenha ao menos uma tabela do Excel.  
- Um editor de texto ou IDE (Visual Studio, VS Code, Rider… você escolhe).

Nenhum pacote NuGet extra além do Aspose.Cells é necessário, e tudo funciona no Windows, Linux ou macOS.

## Etapa 1: Configurar o Projeto e as Importações

Primeiro, crie um aplicativo console e traga os namespaces necessários para o escopo.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Dica de especialista:** Se você estiver usando a CLI do .NET, execute `dotnet new console -n ExcelTableExport` e depois `dotnet add package Aspose.Cells` antes de colar o código acima.

## Etapa 2: Carregar a Pasta de Trabalho e Obter a Primeira Planilha

O objeto workbook representa o arquivo Excel completo. Carregá‑lo uma única vez mantém o uso de memória baixo.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Por que escolhemos a primeira planilha? Em muitos relatórios gerados os dados ficam na primeira aba, mas você pode mudar o índice ou usar `wb.Worksheets["SheetName"]` para uma planilha nomeada.

## Etapa 3: Recuperar a Primeira Tabela Definida na Planilha

Tabelas do Excel (ListObjects) nos fornecem dados estruturados, tornando a exportação previsível.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Se sua pasta de trabalho contiver várias tabelas, basta iterar `ws.Tables` ou selecionar por `tbl.Name`.

## Etapa 4: Configurar Opções de Exportação – Exportar Cada Célula como String

Aspose.Cells permite controlar o formato de cada célula durante a exportação. Definir `ExportAsString` garante que números, datas e fórmulas se tornem texto simples.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Adicionando uma Ação de Exportação Personalizada para Remover Espaços em Branco

Frequentemente os dados de origem contêm espaços à esquerda ou à direita. Removê‑los deixa o arquivo `.txt` final mais limpo.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

A lambda recebe o objeto `Cell` e um `TextWriter`. Você também pode adicionar lógica condicional aqui — por exemplo, substituir vírgulas por ponto‑e‑vírgula para saída no estilo CSV.

## Etapa 5: Exportar a Tabela a partir da Célula A1 para um Arquivo de Texto

Agora realmente gravamos a tabela no disco. O método `ExportTable` percorre a tabela linha a linha, aplicando as opções que acabamos de definir.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**O que você verá:** Cada linha da tabela do Excel se torna uma linha em `Table.txt`. As colunas são separadas por um caractere de tabulação (`\t`) por padrão — perfeito para o parsing downstream.

### Exemplo de Saída Esperada

Assumindo que `input.xlsx` contenha uma tabela com três colunas (`ID`, `Name`, `Score`) e duas linhas de dados, `Table.txt` ficará assim:

```
1    Alice    85
2    Bob      92
```

Observe que os espaços são removidos e tudo está em texto simples — exatamente o que o requisito de **export excel data as plain text** pede.

## Lidando com Casos de Borda Comuns

| Situação | O que Fazer | Por quê |
|-----------|------------|-----|
| **Table has empty cells** | A lambda grava `cell.StringValue.Trim()` que devolve uma string vazia para células em branco. | Mantém o alinhamento das colunas sem adicionar caracteres indesejados. |
| **You need a custom delimiter** | Substitua `writer.Write(cell.StringValue.Trim());` por `writer.Write($"{cell.StringValue.Trim()},");` e remova o delimitador final após cada linha. | Alguns sistemas preferem vírgulas ou pipes em vez de tabs. |
| **Large worksheets ( > 100 k rows )** | Use `ExportTableOptions` com `ExportAsString = true` e faça o streaming do arquivo como mostrado; Aspose.Cells processa as linhas de forma streaming, evitando erros OOM. | Garante escalabilidade. |
| **Multiple tables in one sheet** | Percorra `ws.Tables` e chame `ExportTable` para cada uma, opcionalmente adicionando uma linha separadora entre as exportações. | Permite **save Excel table to .txt file** para cada tabela. |

## Exemplo Completo em Funcionamento

Abaixo está o programa completo que você pode copiar‑colar em `Program.cs`. Substitua `YOUR_DIRECTORY` por um caminho absoluto ou relativo que exista na sua máquina.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Execute o programa com `dotnet run`. Se tudo estiver configurado corretamente, você verá a mensagem de confirmação e um `Table.txt` recém‑criado contendo o **export excel data as plain text**.

## Bônus: Confirmação Visual (Opcional)

Se você quiser ver rapidamente uma captura de tela do arquivo resultante, pode abri‑lo em qualquer editor de texto. A seguir, uma imagem de placeholder mostrando o layout esperado.

![captura de tela de como exportar tabela do Excel](https://example.com/images/export-excel-table.png "como exportar tabela do Excel")

*Texto alternativo:* **como exportar tabela do Excel** – mostra a saída em texto puro de uma tabela do Excel exportada.

## Recapitulação & Próximos Passos

Cobrimos tudo o que você precisa saber **how to export Excel table** usando Aspose.Cells, desde o carregamento da pasta de trabalho até a remoção de espaços nas células e, finalmente, a gravação de um arquivo `.txt` limpo.  

- Agora você entende **save Excel table to .txt file** com lógica personalizada.  
- Pode adaptar a lambda para lidar com datas, números ou delimitadores personalizados.  
- Para projetos maiores, considere encapsular a lógica em um método ou classe reutilizável.

**O que vem a seguir?** Experimente exportar várias tabelas ou altere o formato de saída para CSV mudando o delimitador. Você também pode explorar **export excel data as plain text** diretamente para um stream de rede para integrações em tempo real.

Tem dúvidas ou encontrou algum problema? Deixe um comentário, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Exportar Arquivos Excel em .NET Usando Aspose.Cells: Um Guia Abrangente](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Como Exportar Linhas Visíveis do Excel Usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Como Combinar Planilhas Excel em um Único Arquivo de Texto Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}