---
category: general
date: 2026-06-27
description: Excluir várias linhas no Word usando C#. Aprenda como excluir linhas
  de tabelas, remover linhas de tabelas e editar tabelas de documentos Word de forma
  eficiente.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: pt
og_description: Exclua várias linhas no Word instantaneamente. Este tutorial mostra
  como excluir linhas de tabela, remover linhas de uma tabela do Word e dominar a
  edição de tabelas em documentos do Word.
og_title: Excluir várias linhas no Word – Edição de tabela passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Excluir várias linhas no Word – Guia completo para remover linhas de tabela
url: /pt/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir Várias Linhas Word – Guia Completo para Remover Linhas de Tabela

Já precisou **excluir várias linhas word** documentos mas não sabia qual chamada de API usar? Você não está sozinho — a maioria dos desenvolvedores encontra o mesmo obstáculo ao tentar reduzir uma tabela mantendo o cabeçalho intacto.  

Neste tutorial vamos percorrer uma solução concisa, de ponta a ponta, que mostra *como excluir linhas de tabela* programaticamente, *como remover linhas de tabela* com segurança, e por que a abordagem funciona para qualquer cenário de **excluir linhas de tabela do word** que você possa encontrar.

Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto C#, além de algumas dicas para tarefas mais amplas de **edição de tabelas em documentos word**.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)
- Aspose.Words for .NET instalado (`dotnet add package Aspose.Words`)
- Noções básicas de sintaxe C#
- Um arquivo `.docx` de entrada que contenha ao menos uma tabela com uma linha de cabeçalho

> **Dica de especialista:** Se ainda não tem uma licença, o Aspose.Words oferece um modo de avaliação gratuito que é perfeito para testes.

## Etapa 1: Configurar o Projeto e Carregar o Documento Word

Primeiro de tudo — crie um aplicativo console (ou integre a um serviço existente) e adicione as diretivas `using` necessárias. Em seguida, carregue o documento fonte.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Por que isso importa:**  
`Document` é o ponto de entrada para toda operação do Aspose.Words. Carregar o arquivo uma única vez mantém o uso de memória baixo e fornece um manipulador para todas as chamadas subsequentes de edição de tabelas.

## Etapa 2: Localizar a Primeira Tabela (ou Qualquer Tabela Necessária)

Se o seu documento contém várias tabelas, você pode escolher a que deseja pelo índice ou pesquisando por uma palavra‑chave. Para simplificar, vamos pegar a primeira tabela, que geralmente contém os dados que queremos reduzir.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Explicação:**  
`GetChild(NodeType.Table, 0, true)` percorre a árvore do documento em profundidade e devolve o primeiro nó `Table` encontrado. O cast `as Table` converte o nó com segurança, permitindo que trabalhemos com `Rows` posteriormente.

## Etapa 3: Excluir Várias Linhas Preservando o Cabeçalho

Agora chegamos ao ponto central: **excluir várias linhas word** documentos. Suponha que o cabeçalho esteja na linha 0 e você queira remover as duas linhas seguintes (índices 1 e 2). O método `DeleteRows` faz exatamente isso.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Como Excluir Linhas de Tabela – Variações

- **Excluir uma única linha:** `firstTable?.DeleteRows(rowIndex, 1);`
- **Excluir todas as linhas exceto o cabeçalho:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Excluir linhas com base em uma condição:** iterar `firstTable.Rows` e chamar `DeleteRows` quando uma célula corresponder ao seu critério.

Esses trechos respondem à pergunta comum **como remover linhas de tabela** de forma flexível.

## Etapa 4: Salvar o Documento Modificado

Depois que as linhas forem removidas, basta gravar o documento de volta ao disco. Você pode sobrescrever o arquivo original ou criar uma cópia nova.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**O que você verá:**  
Se a tabela original tinha, por exemplo, cinco linhas (cabeçalho + quatro linhas de dados), o `output.docx` salvo conterá agora apenas três linhas (cabeçalho + duas linhas de dados restantes). Abra o arquivo no Word para verificar que as linhas indesejadas desapareceram sem alterar nenhum outro conteúdo.

![exemplo de excluir várias linhas word](delete-multiple-rows-word.png)

*Texto alternativo da imagem: excluir várias linhas word – captura de tela antes e depois de uma tabela Word.*

## Exemplo Completo, Pronto‑para‑Executar

Juntando tudo, aqui está o programa completo que você pode copiar‑colar:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Execute o programa, abra `output.docx` e você verá o cabeçalho ainda presente enquanto as linhas escolhidas desapareceram. Isso é **excluir várias linhas word** em ação.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| **NullReferenceException** quando `firstTable` é `null` | O documento não tem tabelas ou o índice está errado | Sempre verifique `firstTable != null` antes de chamar `DeleteRows`. |
| **Linhas não são excluídas** | Uso do índice inicial errado (tabelas Word são baseadas em zero) | Lembre‑se que o cabeçalho é a linha 0; comece em 1 para mantê‑lo. |
| **Sobrescrever um arquivo somente‑leitura** | Permissões de arquivo impedem a sobrescrita | Salve em um caminho diferente ou ajuste os atributos do arquivo. |
| **Alterações inesperadas no layout** | Excluir linhas que contêm células mescladas pode corromper a tabela | Garanta que células mescladas sejam tratadas — desfaça a mesclagem primeiro ou exclua linhas inteiras com cuidado. |

## Expandindo a Solução – Mais Edição de Tabelas em Documentos Word

Se você tem interesse em **edição de tabelas em documentos word** mais abrangente, considere os próximos passos:

- **Inserir novas linhas:** `firstTable?.Rows.Add(new Row(doc));`
- **Atualizar texto da célula:** `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Aplicar estilos:** Use `CellFormat` ou `RowFormat` para definir sombreamento, bordas ou propriedades de fonte.
- **Exportar para PDF:** `doc.Save("output.pdf", SaveFormat.Pdf);`

Todas essas operações se baseiam no mesmo modelo de objetos que usamos para exclusão de linhas, mantendo seu código consistente.

## Conclusão

Acabamos de mostrar como **excluir várias linhas word** documentos com apenas algumas linhas de código C#. A abordagem cobre *como excluir linhas de tabela*, *como remover linhas de tabela* e o tema mais amplo de **edição de tabelas em documentos word**.  

Agora você tem um padrão sólido e reutilizável: carregar o documento, localizar a tabela, chamar `DeleteRows` com os índices corretos e salvar. A partir daqui, você pode ajustar o intervalo de linhas, percorrer várias tabelas ou combinar com outros recursos de edição para atender a qualquer tarefa de automação.

Pronto para avançar? Experimente automatizar a geração de faturas, limpar modelos de relatórios ou construir uma ferramenta de atualização em massa que processe dezenas de arquivos Word de uma só vez. O céu é o limite, e a API torna tudo indolor.

Se encontrar algum obstáculo, deixe um comentário abaixo — feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Delete Multiple Rows in Excel with Aspose.Cells .NET: A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Delete Multiple Rows in Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}