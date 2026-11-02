---
category: general
date: 2026-06-08
description: Excluir linhas de tabela do Word usando Aspose.Words. Aprenda como excluir
  linhas, excluir várias linhas do Word e dominar a edição de tabelas em minutos.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: pt
og_description: Excluir linhas de tabela do Word com Aspose.Words. Este tutorial mostra
  como excluir linhas, excluir várias linhas do Word e manter suas tabelas organizadas.
og_title: Excluir linhas da tabela do Word – Guia Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Excluir linhas da tabela do Word – Guia Completo de C#
url: /pt/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir linhas de tabela Word – Guia Completo em C#

Já precisou **delete rows word table** mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram esse obstáculo ao limpar relatórios gerados ou reduzir tabelas baseadas em dados. A boa notícia? Com algumas linhas de C# e Aspose.Words você pode remover facilmente linhas indesejadas, seja uma única linha ou um lote delas. Neste guia vamos percorrer *how to delete rows* e até cobrir o caso mais complicado de **delete multiple rows word** de uma só vez.

Vamos cobrir tudo o que você precisa saber: o código exato, por que cada passo importa, armadilhas comuns e um exemplo pronto‑para‑executar. Ao final, você será capaz de remover linhas de qualquer tabela Word sem quebrar a estrutura do documento. Sem enrolação, apenas técnicas práticas e testadas em batalha.

## Pré-requisitos

- **Aspose.Words for .NET** (versão 23.12 ou mais recente). Você pode obtê-lo no NuGet: `Install-Package Aspose.Words`.
- Um ambiente de desenvolvimento .NET (Visual Studio, Rider ou VS Code com a extensão C#).
- Um arquivo Word de entrada (`input.docx`) que contenha ao menos uma tabela com uma linha de cabeçalho.

É isso—nenhuma biblioteca extra, sem interop COM, apenas código gerenciado puro.

## Etapa 1: Carregar o documento Word

A primeira coisa que você faz é abrir o documento. Aspose.Words trata um arquivo Word como um objeto `Document`, que lhe dá acesso total a seções, corpos, tabelas e muito mais.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Por que isso importa:* Carregar o documento cria uma representação em memória, então quaisquer alterações que você faça são rápidas e não tocam o sistema de arquivos até que você salve explicitamente.

## Etapa 2: Obter a tabela alvo

Na maioria dos cenários você sabe qual tabela deseja editar—geralmente a primeira. Aspose.Words torna trivial obtê‑la via a propriedade `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

Se seu documento tem múltiplas tabelas, você pode percorrer `doc.GetChildNodes(NodeType.Table, true)` e escolher a correta com base no índice ou em um marcador personalizado.

## Etapa 3: Excluir linhas – única ou múltipla

### 3.1 Como excluir linhas (linha única)

Para remover uma única linha, chame `DeleteRows(startIndex, count)` onde `startIndex` é baseado em zero. Pular a linha de cabeçalho (índice 0) é comum:

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Delete multiple rows word – remoção em lote

Quando você precisa remover um intervalo—por exemplo, linhas 2‑6—você passa o índice inicial e o número de linhas a apagar. Este é o padrão **delete multiple rows word**:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Por que usar uma única chamada?* Excluir linhas uma a uma força a tabela a reindexar após cada remoção, o que pode gerar erros e ser mais lento. O método em lote mantém a estrutura interna da tabela consistente.

#### Caso de borda: Excluir além do tamanho da tabela

Se `startIndex + count` exceder a contagem real de linhas, Aspose.Words lança uma `ArgumentOutOfRangeException`. Uma proteção defensiva fica assim:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

Esse trecho garante que você nunca tente excluir mais linhas do que existem.

## Etapa 4: Salvar o documento modificado

Depois que as linhas são removidas, persistir as alterações é uma única linha:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

O método `Save` escolhe automaticamente o formato com base na extensão do arquivo, então você pode gerar PDF, HTML ou até ODT com um sufixo diferente.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto‑para‑executar:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Saída esperada

- `output.docx` contém a tabela original **sem** as linhas 2‑6.
- Todas as linhas restantes sobem, preservando a formatação das células e as larguras das colunas.
- A linha de cabeçalho permanece intacta, mantendo os títulos das colunas visíveis.

## Por que esta abordagem supera as alternativas

| Abordagem | Prós | Contras |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | Exclusão em lote de uma linha, preserva estilos, sem dependências COM | Requer uma biblioteca comercial (versão de avaliação gratuita disponível) |
| Office Interop | Funciona com o Word nativo | Necessita do Word instalado no servidor, lento, dores de cabeça com limpeza de COM |
| Open XML SDK | Gratuito, código aberto | Manipulação manual de XML; excluir linhas com segurança é trabalhoso |

Se você já está usando Aspose.Words para outras tarefas de documentos, permanecer com `DeleteRows` mantém sua base de código limpa e consistente.

## Dicas profissionais & armadilhas comuns

- **Pro tip:** Sempre mantenha a linha de cabeçalho (índice 0) intacta, a menos que você realmente queira removê‑la. Excluir o cabeçalho pode quebrar o processamento subsequente que espera nomes de colunas.
- **Watch out for merged cells.** Se uma linha contém uma célula mesclada verticalmente que se estende para a linha que você está excluindo, Aspose.Words ajustará automaticamente o intervalo de mesclagem, mas verifique o resultado visual.
- **Performance note:** Excluir muitas linhas de uma tabela enorme (milhares de linhas) ainda é rápido, mas se você estiver processando centenas de documentos em um loop, considere reutilizar o objeto `Document` sempre que possível para reduzir a sobrecarga de alocação.

## Perguntas frequentes

**Q: Posso excluir linhas com base no conteúdo da célula ao invés do índice?**  
A: Absolutamente. Percorra `table.Rows`, inspecione `row.Cells[i].GetText()` e colete os índices correspondentes. Em seguida, chame `DeleteRows` com o menor índice e a contagem total, ou exclua linhas em ordem reversa para evitar reindexação.

**Q: Isso funciona com arquivos .doc?**  
A: Sim. Aspose.Words suporta tanto `.doc` quanto `.docx`. Basta mudar a extensão do arquivo no construtor `Document` e na chamada `Save`.

**Q: E se a tabela estiver dentro de um cabeçalho/rodapé?**  
A: Recupere‑a via a coleção `doc.FirstSection.HeadersFooters`, então aplique a mesma lógica `DeleteRows`.

## Conclusão

Agora você tem uma solução sólida, de ponta a ponta, para **delete rows word table** usando C#. O exemplo mostra *how to delete rows* individualmente e como **delete multiple rows word** em uma única chamada eficiente. Com Aspose.Words você obtém uma API limpa, sem complicações COM, e controle total sobre documentos Word.

Pronto para o próximo desafio? Tente adicionar uma nova linha com totais calculados, ou exporte a tabela reduzida para CSV usando `Table.ToTxt`. O céu é o limite quando você domina a manipulação de tabelas.

Boa codificação, e que suas tabelas Word permaneçam organizadas!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Excluir Linhas no Excel Usando Aspose.Cells para Java | Guia & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Como Excluir Linhas em Branco no Excel Usando Aspose.Cells .NET para Limpeza de Dados](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Como Inserir e Excluir Linhas no Excel com Aspose.Cells para .NET&#58; Um Guia Abrangente](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}