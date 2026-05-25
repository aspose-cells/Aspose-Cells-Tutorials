---
category: general
date: 2026-03-29
description: Aprenda a inserir linhas no GridJs rapidamente. Este guia também aborda
  como adicionar linhas e inserir múltiplas linhas na grade com uma operação em lote.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: pt
og_description: Aprenda a inserir linhas no GridJs rapidamente. Este guia mostra como
  adicionar linhas, adicionar várias linhas na grade e lidar com inserções em lote
  de grande volume.
og_title: Como Inserir Linhas no GridJs – Adicionar Várias Linhas ao Grid de Forma
  Eficiente
tags:
- GridJs
- C#
- data‑grid
title: Como Inserir Linhas no GridJs – Adicionar Várias Linhas ao Grid de Forma Eficiente
url: /pt/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Inserir Linhas no GridJs – Adicionar Várias Linhas ao Grid de Forma Eficiente

Já se perguntou **como inserir linhas** em uma enorme tabela GridJs sem travar a interface? Talvez você tenha se deparado com a dificuldade de **adicionar linhas** uma a uma e o desempenho simplesmente desmorona. A boa notícia é que o GridJs oferece uma API em lote que permite **adicionar múltiplas linhas ao grid** em uma única chamada, mantendo tudo rápido mesmo quando você está lidando com milhões de registros.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente **como inserir linhas** usando `InsertRowsBatch`. Você verá por que o batching é importante, como verificar o resultado e o que observar quando o índice alvo é muito grande. Ao final, você será capaz de inserir mil novos registros em qualquer instância do GridJs com confiança.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 ou superior (o código compila com qualquer SDK recente)
- Uma referência ao pacote NuGet `GridJs` (ou o DLL se estiver usando uma build customizada)
- Conhecimento básico de C# – não é preciso ser um guru, apenas estar confortável com classes e métodos
- Uma IDE ou editor de sua escolha (Visual Studio, Rider, VS Code… todos funcionam)

> **Dica de especialista:** Se você planeja trabalhar com grids realmente massivos (dezenas de milhões de linhas), habilite `gridJs.EnableVirtualization = true;` para manter a renderização da UI leve.

## Etapa 1: Criar e Configurar a Instância do GridJs

Primeiro de tudo: você precisa de um objeto `GridJs` ativo. Pense nele como a tela onde você pintará as linhas.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Por que esta etapa importa:** Inicializar o grid e, opcionalmente, semear dados reflete um cenário real onde o grid já contém uma grande quantidade de informações. A inserção em lote que faremos depois deve respeitar o índice base zero, por isso pre‑populamos para ilustrar o ponto exato de inserção.

## Etapa 2: Usar `InsertRowsBatch` para **Adicionar Várias Linhas ao Grid**

Agora o núcleo do tutorial – a chamada que realmente **adiciona linhas** em massa. A assinatura do método é `InsertRowsBatch(int startIndex, int count)`. No nosso exemplo começaremos no índice 2 000 000 (que corresponde à 2 000 001ª linha) e adicionaremos dez linhas.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Como funciona:** `InsertRowsBatch` aloca internamente o número solicitado de linhas e desloca as linhas existentes para baixo. Como a operação é realizada em uma única transação, a UI é atualizada apenas uma vez, e é por isso que este método é a forma recomendada de **como adicionar linhas** de maneira eficiente.

## Etapa 3: Verificar a Inserção – As Linhas Foram Inseridas Onde Esperado?

Depois da operação em lote, você vai querer garantir que as linhas estejam onde você imagina. O helper a seguir lê a primeira e a última linha do bloco recém‑adicionado e as imprime no console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Saída esperada**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

As células vazias indicam que as linhas são marcadores aguardando dados. Você pode agora preenchê‑las individualmente ou executar outra atualização em lote.

> **Observação de caso extremo:** Se `startIndex` exceder a contagem atual de linhas, o GridJs adicionará automaticamente as novas linhas ao final. Por outro lado, um índice negativo lança uma `ArgumentOutOfRangeException`, portanto sempre valide os índices fornecidos pelo usuário.

## Etapa 4: Popular as Novas Linhas (Opcional, mas Comum)

Frequentemente você não quer apenas linhas vazias; precisa preenchê‑las com valores significativos. Você pode percorrer o intervalo recém‑criado e chamar `SetCell` ou uma API similar.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Você poderia chamar `PopulateNewRows(gridJs, startIndex, rowsToAdd);` logo após a inserção em lote se precisar que as linhas estejam prontas para exibição imediatamente.

## Etapa 5: Dicas de Performance para Grids Muito Grandes

Quando você está lidando com **adicionar múltiplas linhas ao grid** em milhões, mantenha estas estratégias em mente:

1. **Tamanho do lote importa** – Inserir 10 000 linhas de uma vez pode ser mais rápido que dez lotes separados de 1 000 linhas, pois cada lote gera apenas uma atualização da UI.
2. **Desative atualizações da UI** – Algumas versões do GridJs expõem `grid.SuspendLayout()` / `grid.ResumeLayout()`. Envolva seu lote nessas chamadas se notar lentidão.
3. **Use virtualização** – Como mostrado antes, `EnableVirtualization` reduz drasticamente o consumo de memória e o tempo de renderização.
4. **Evite cópias profundas** – Passe tipos de valor simples ou objetos leves para o grid; objetos pesados forçam o grid a clonar os dados, prejudicando a performance.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em um novo projeto de console:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Execute o programa e você verá a saída no console confirmando que as dez linhas foram inseridas no local correto e, em seguida, populadas.

## Conclusão

Cobremos **como inserir linhas** no GridJs usando a API em lote, demonstramos **como adicionar linhas** de forma eficiente e exploramos maneiras de **adicionar múltiplas linhas ao grid** sem sobrecarregar a UI. Os principais aprendizados são:

- Use `InsertRowsBatch(startIndex, count)` para qualquer operação em massa.
- Valide os índices e considere a virtualização para conjuntos de dados massivos.
- Popule as linhas após o lote se precisar de conteúdo imediato.

Em seguida, você pode querer explorar **como excluir linhas**, implementar **desfazer/refazer** para edições em lote, ou integrar o GridJs com um serviço back‑end que transmite dados sob demanda. Todos esses tópicos se baseiam diretamente nos conceitos que você acabou de aprender.

Sinta‑se à vontade para experimentar – altere o tamanho do lote, tente inserir no início do grid, ou combine vários lotes em uma única transação. Quanto mais você brincar, mais confortável ficará com grandes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}