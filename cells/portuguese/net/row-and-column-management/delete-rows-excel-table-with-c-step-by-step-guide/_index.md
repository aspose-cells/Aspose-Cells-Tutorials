---
category: general
date: 2026-02-28
description: Excluir linhas de tabela do Excel em C# rapidamente. Aprenda como adicionar
  intervalo nomeado no Excel, acessar a planilha pelo nome e evitar erros de nomes
  duplicados.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: pt
og_description: Excluir linhas de tabela do Excel usando C#. Este tutorial também
  mostra como adicionar intervalos nomeados no Excel e acessar a planilha pelo nome.
og_title: Excluir linhas da tabela do Excel com C# – Guia completo
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Excluir Linhas de Tabela do Excel com C# – Guia Passo a Passo
url: /pt/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir Linhas de Tabela do Excel com C# – Tutorial de Programação Completo

Já precisou **excluir linhas de tabela do Excel** de uma pasta de trabalho, mas não tinha certeza de qual chamada de API usar? Você não está sozinho — a maioria dos desenvolvedores encontra o mesmo obstáculo na primeira vez que tenta reduzir uma tabela programaticamente.  

Neste guia vamos percorrer um exemplo completo e executável que não só remove linhas de uma tabela do Excel, mas também mostra **como adicionar nome definido** (também conhecido como *named range*), como **acessar a planilha por nome**, e por que adicionar um nome duplicado em outra planilha gera uma `InvalidOperationException`.  

Ao final do artigo você será capaz de:

* Obter uma planilha usando o nome da sua aba.  
* Excluir com segurança linhas de dados da primeira tabela nessa planilha.  
* Criar um nome definido que aponta para um endereço específico.  
* Entender as armadilhas de nomes duplicados entre planilhas.

Nenhuma documentação externa necessária — tudo o que você precisa está aqui.

---

## O que Você Precisa

* **DevExpress Spreadsheet** (ou qualquer biblioteca que exponha os objetos `Workbook`, `Worksheet`, `ListObject` e `Names`).  
* Um projeto .NET direcionado a **.NET 6** ou superior (o código também compila com .NET Framework 4.8).  
* Familiaridade básica com C# — se você sabe escrever um loop `foreach`, está pronto para começar.

> **Dica de especialista:** Se você estiver usando a edição Community gratuita do DevExpress, as APIs usadas abaixo são idênticas à versão comercial.

---

## Etapa 1 – Acessar Planilha por Nome

A primeira coisa que você precisa fazer é localizar a planilha que contém a tabela que deseja modificar.  
A maioria dos desenvolvedores recorre a `Worksheets[0]` por hábito, mas isso acopla seu código à ordem das planilhas e quebra assim que alguém renomeia uma aba.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Por que isso importa:* Ao usar o **nome** da planilha em vez do seu índice, você evita edições acidentais na planilha errada quando a pasta de trabalho é alterada.  

Se o nome fornecido não existir, a biblioteca lança uma `KeyNotFoundException`, que você pode capturar para apresentar uma mensagem de erro amigável.

---

## Etapa 2 – Excluir Linhas de Tabela do Excel (Modo Seguro)

Agora que você tem a planilha correta, vamos remover as linhas de dados da primeira tabela.  
Um erro comum é chamar `DeleteRows(1, rowCount‑1)`. Desde o **DevExpress 22.2** essa sobrecarga está **proibida** e gera uma `InvalidOperationException`. A biblioteca espera que você exclua linhas **dentro do intervalo de dados da tabela**, não na linha de cabeçalho.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **E se a tabela estiver vazia?** A verificação `if` impede uma chamada com `rowCount = 0`, que caso contrário levantaria uma exceção.

### Visão Geral Visual  

![exemplo de exclusão de linhas de tabela do excel](image.png "Captura de tela mostrando linhas sendo removidas de uma tabela do Excel")  

*Texto alternativo: exemplo de exclusão de linhas de tabela do excel em código C#*

---

## Etapa 3 – Como Adicionar Nome Definido (Criar um Named Range)

Depois de limpar a tabela, talvez você queira referenciar um intervalo específico mais tarde — por exemplo, para um gráfico ou uma lista de validação de dados. É aí que **add named range excel** entra em ação.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

O método `Names.Add` recebe dois parâmetros: o identificador e o endereço no estilo A1.  
Como usamos **acessar planilha por nome** anteriormente, a string de endereço pode referenciar com segurança qualquer planilha sem se preocupar com mudanças de índice.

---

## Etapa 4 – Named Range em Outra Planilha – Evite Erros de Nome Duplicado

Você pode pensar que pode reutilizar o mesmo identificador em outra planilha, assim:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Infelizmente, o escopo de nomes do Excel é **para todo o workbook**, não por planilha. A chamada acima dispara uma `InvalidOperationException` com a mensagem *“A name with the same identifier already exists.”*  

### Como Contornar

1. **Escolha um nome único** (`MyTable_Sheet2`).  
2. **Exclua o nome existente** antes de adicioná‑lo novamente (apenas se realmente quiser substituí‑lo).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Exemplo Completo e Executável

Juntando tudo, aqui está um aplicativo console autônomo que você pode inserir no Visual Studio e executar contra um arquivo de exemplo `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Resultado esperado**

* Todas as linhas de dados da primeira tabela na **Sheet1** desaparecem, restando apenas a linha de cabeçalho.  
* O nome **MyTable** agora aponta para `Sheet1!$A$1:$C$5`.  
* Um segundo nome **MyTable_Sheet2** referencia com segurança um intervalo na **Sheet2** sem gerar exceção.

---

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| *E se a pasta de trabalho tiver várias tabelas?* | Obtenha o `ListObject` correto pelo índice (`worksheet.ListObjects[1]`) ou pelo nome (`worksheet.ListObjects["MyTable"]`). |
| *Posso excluir linhas de uma tabela que se estende por várias planilhas?* | Não — tabelas ficam confinadas a uma única planilha. Você deve repetir a lógica de exclusão para cada planilha. |
| *Existe uma forma de excluir apenas um subconjunto de linhas?* | Sim — use `table.DeleteRows(startRow, count)` onde `startRow` é baseado em zero dentro da área de dados da tabela. |
| *Os nomes definidos permanecem após salvar?* | Absolutamente. Depois de chamar `SaveDocument`, os nomes passam a fazer parte do XML da pasta de trabalho. |
| *Como listar todos os nomes definidos na pasta de trabalho?* | Itere `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusão

Cobrirmos **excluir linhas de tabela do Excel** usando C#, demonstramos **add named range excel**, e mostramos a maneira correta de **acessar planilha por nome** evitando a temida exceção de nome duplicado.  

A solução completa está no trecho de código acima — copie, cole e execute em seus próprios arquivos. A partir daqui você pode expandir a lógica para lidar com múltiplas tabelas, cálculos de intervalos dinâmicos ou até integrar com uma interface de usuário.

**Próximos passos** que você pode explorar:

* Use **named range em outra planilha** para alimentar séries de gráficos.  
* Combine a lógica de exclusão com **ExcelDataReader** para importar dados antes de limpá‑los.  
* Automatize atualizações em massa em dezenas de pastas de trabalho usando um simples loop `foreach (var file in Directory.GetFiles(...))`.

Tem mais perguntas sobre automação do Excel em C#? Deixe um comentário e vamos continuar a conversa. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}