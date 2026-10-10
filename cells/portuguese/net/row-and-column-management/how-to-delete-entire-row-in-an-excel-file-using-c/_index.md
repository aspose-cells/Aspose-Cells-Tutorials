---
category: general
date: 2026-10-10
description: Aprenda como excluir uma linha inteira em uma pasta de trabalho do Excel
  com C#. Este guia passo a passo também aborda como excluir linha por índice e remover
  linha por índice usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: pt
lastmod: 2026-10-10
og_description: Excluir linha inteira em uma pasta de trabalho do Excel usando C#.
  Siga este guia para aprender como excluir uma linha por índice, remover uma linha
  por índice e salvar o arquivo com segurança.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Excluir linha inteira no Excel com C# – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Como excluir linha inteira em um arquivo Excel usando C#
url: /pt/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir linha inteira em um arquivo Excel usando C#

Se você precisa **excluir linha inteira** em uma pasta de trabalho Excel, este guia mostra exatamente como fazer isso com C#. Seja limpando dados importados ou construindo uma ferramenta de relatórios, os passos abaixo permitem remover uma linha pelo seu índice e salvar o resultado sem perder outros dados.

Você também verá como a mesma abordagem responde à pergunta **how to delete row** por índice, como **remove row by index**, e por que isso funciona em cenários de **delete row excel** em C#.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.6+)
* A biblioteca **Aspose.Cells for .NET** (disponível via NuGet: `Install-Package Aspose.Cells`)
* Familiaridade básica com projetos de console ou desktop em C#

Nenhum componente adicional de interop do Excel ou COM é necessário, o que mantém a solução leve e segura para execução no lado do servidor.

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo aplicativo de console (ou adicione o código a um projeto existente) e inclua as diretivas `using` necessárias:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Por que isso importa*: Importar `Aspose.Cells` fornece acesso a `Workbook`, `Worksheet` e ao método `DeleteRows` que realiza a remoção real da linha.

## Etapa 2: Carregar a pasta de trabalho e selecionar a planilha

Você deve carregar o arquivo de origem (`input.xlsx`) e obter a planilha que deseja modificar. A primeira planilha é acessada com o índice `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Dica**: Se precisar trabalhar com uma planilha específica, substitua o índice pelo nome da planilha: `workbook.Worksheets["Data"]`.

## Etapa 3: Excluir a linha inteira pelo seu índice baseado em zero

Aspose.Cells usa indexação baseada em zero, portanto a primeira linha é `0`. Para excluir a linha 5 (a sexta linha visual), chame `DeleteRows` com `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Explicação*:

* `ws.Cells[5, 0]` aponta para a primeira célula da linha que você deseja excluir.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` indica ao Aspose.Cells para remover **1** linha, e a flag `DeleteEntireRow` garante que **a linha inteira** desapareça, deslocando as linhas abaixo para cima.

### Como excluir linha por índice em outros cenários

* **Excluir várias linhas consecutivas** – altere o primeiro argumento para o número de linhas que deseja apagar:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Excluir a última linha** – use `ws.Cells.MaxDataRow` para obter o índice da linha mais baixa preenchida:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Esses trechos respondem ao requisito de **remove row by index** mantendo o código fácil de ler.

## Etapa 4: Salvar a pasta de trabalho com a linha removida

Após a exclusão, grave a pasta de trabalho modificada de volta ao disco. Você pode sobrescrever o arquivo original ou criar um novo.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Se precisar manter o arquivo original inalterado, basta mudar o caminho de saída. O método `Save` suporta vários formatos (`.xls`, `.csv`, `.pdf`, etc.) – basta alterar a extensão do arquivo.

## Exemplo completo em funcionamento

Juntando tudo, aqui está um programa completo, pronto‑para‑executar:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Saída esperada**: Após executar o programa, `output.xlsx` conterá todas as linhas originais, exceto a que começava na linha visual 6. Todos os dados abaixo da linha removida são deslocados para cima automaticamente, preservando fórmulas e formatação.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Índice fora do intervalo** | Tentando excluir um índice de linha que não existe (por exemplo, `ws.Cells[1000,0]` em uma planilha com 200 linhas) | Use `ws.Cells.MaxDataRow` para verificar o maior índice válido antes de chamar `DeleteRows`. |
| **Exclusão parcial de linha** | Omitir `DeleteOptions.DeleteEntireRow` resulta apenas na limpeza do conteúdo das células | Sempre passe `DeleteOptions.DeleteEntireRow` quando precisar remover a linha inteira. |
| **Alterações inesperadas em fórmulas** | Excluir linhas que fazem parte de um intervalo de fórmula pode quebrar referências | Reavalie as fórmulas após a exclusão (`workbook.CalculateFormula()`) se sua pasta de trabalho depender de intervalos dinâmicos. |
| **Salvar em um local somente‑leitura** | A chamada `Save` lança uma exceção se a pasta estiver protegida | Garanta que o diretório de destino seja gravável ou execute o programa com permissões adequadas. |

Abordar essas questões torna a solução robusta para uso em produção e satisfaz as consultas **delete row excel** e **delete row c#**.

## Avançado: Excluindo linhas com base em uma condição

Às vezes você precisa remover linhas que atendem a um determinado critério (por exemplo, linhas onde a coluna A está vazia). O loop a seguir demonstra uma forma segura de percorrer de baixo para cima e excluir linhas correspondentes:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Percorrer de baixo para cima evita o problema de deslocamento de índices que ocorre ao excluir linhas enquanto itera de forma crescente.

## Conclusão

Agora você sabe como **delete entire row** em uma pasta de trabalho Excel usando C#. O guia abordou:

* Carregar uma pasta de trabalho e selecionar uma planilha  
* Usar `DeleteRows` com `DeleteOptions.DeleteEntireRow` para **how to delete row** por índice  
* Salvar o arquivo modificado com segurança  
* Tratamento de casos extremos, dicas de desempenho e um exemplo de exclusão condicional  

Com esse conhecimento você pode implementar com confiança a funcionalidade de **remove row by index**, automatizar a limpeza de dados e integrar a manipulação de Excel em qualquer aplicação C#.  

**Próximos passos**: explore outros recursos do Aspose.Cells, como inserir linhas, copiar intervalos ou converter a pasta de trabalho para PDF — todos baseados nos mesmos objetos `Workbook` e `Worksheet` que você acabou de dominar. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Excluir uma Linha Excel Usando Aspose.Cells .NET: Um Guia Abrangente](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Proteger a Linha de Cabeçalho no Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Gerenciamento Eficiente de Linhas no Excel usando Aspose.Cells para Java: Inserir e Excluir Linhas](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}