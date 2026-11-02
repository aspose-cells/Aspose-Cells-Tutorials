---
category: general
date: 2026-10-07
description: Aprenda como o Aspose.Cells exclui linhas de uma tabela do Excel, remove
  linhas exceto o cabeçalho e lida com a exclusão de linhas de tabela protegida usando
  código C# limpo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: pt
lastmod: 2026-10-07
og_description: Aspose.Cells exclui linhas de uma tabela Excel preservando o cabeçalho.
  Este guia mostra a solução completa em C#, lidando com tabelas protegidas e casos
  de borda comuns.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells excluir linhas – remover todas as linhas exceto o cabeçalho
  em C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como usar Aspose.Cells para excluir linhas em uma tabela do Excel mantendo
  o cabeçalho
url: /pt/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar Aspose.Cells para excluir linhas em uma tabela do Excel mantendo o cabeçalho

Se você precisa **aspose cells delete rows** de uma tabela, mas manter a linha de cabeçalho, este guia mostra uma solução completa e executável. Você verá por que uma chamada direta a `ListObject.DeleteRows` falha quando a tabela está protegida e como contornar essa limitação sem comprometer a integridade dos dados.

O tutorial aborda:

* Carregar uma pasta de trabalho que contém uma tabela protegida.  
* Detectar e remover temporariamente a proteção da tabela.  
* Excluir todas as linhas de dados preservando o cabeçalho.  
* Restaurar o estado original da proteção.  

Ao final do artigo você poderá executar operações de **delete rows excel table** de forma confiável em qualquer projeto Aspose.Cells.

## Pré‑requisitos

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7.2+).  
* Aspose.Cells para .NET 23.9 ou mais recente.  
* Familiaridade básica com C# e tabelas do Excel (também conhecidas como ListObjects).  

Nenhum pacote NuGet adicional é necessário além do Aspose.Cells.

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo aplicativo de console ou adicione o código a seguir a um projeto existente. Importe os namespaces do Aspose.Cells para que o compilador possa resolver `Workbook`, `Worksheet` e `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*Por que esta etapa importa* – Importar os namespaces corretos evita erros de tipo ambíguos e torna o restante do código mais claro.

## Etapa 2: Carregar a pasta de trabalho e localizar a tabela alvo

Substitua `"YOUR_DIRECTORY/TableProtection.xlsx"` pelo caminho do seu arquivo Excel. O exemplo assume que a tabela que você deseja modificar se chama **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*Por que esta etapa importa* – Acessar o `ListObject` fornece um manipulador direto da tabela, que é necessário para qualquer operação de **excel table row deletion**.

## Etapa 3: Verificar se a tabela está protegida

Aspose.Cells bloqueia a exclusão parcial de tabelas quando a tabela está protegida. Tentar `ordersTable.DeleteRows` nesse estado lança uma exceção. Detecte o status de proteção primeiro.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*Por que esta etapa importa* – Conhecer o estado de proteção permite decidir se a proteção deve ser temporariamente removida, garantindo que a regra **protect excel table rows** seja respeitada após a operação.

## Etapa 4: Desproteger temporariamente a tabela (se necessário)

Se a tabela estiver protegida, use `Unprotect` com a senha (se houver). Para tabelas sem senha, basta chamar `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*Por que esta etapa importa* – Desproteger a tabela permite que Aspose.Cells execute **aspose cells delete rows** sem gerar exceção, ao mesmo tempo que possibilita restaurar a proteção posteriormente.

## Etapa 5: Excluir todas as linhas, exceto o cabeçalho

O cabeçalho ocupa a primeira linha da tabela (`RowCount` inclui o cabeçalho). Excluir a partir do índice 1 remove todas as linhas de dados.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*Por que esta etapa importa* – Este código realiza a funcionalidade central de **remove rows except header** enquanto evita a exceção que ocorre com exclusões parciais em tabelas protegidas.

## Etapa 6: Reaplicar a proteção (se ela estava originalmente definida)

Depois que as linhas forem removidas, restaure o estado original de proteção para que a pasta de trabalho se comporte exatamente como antes.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*Por que esta etapa importa* – Restaurar a proteção respeita o requisito **protect excel table rows** e mantém a pasta de trabalho segura para usuários posteriores.

## Etapa 7: Salvar a pasta de trabalho modificada

Escolha um novo nome de arquivo para evitar sobrescrever o original, a menos que a sobrescrita seja intencional.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*Por que esta etapa importa* – Salvar finaliza a operação de **excel table row deletion** e fornece um resultado tangível que você pode abrir no Excel para verificar.

## Exemplo completo em funcionamento

Juntando todas as etapas, obtém‑se um programa autocontido que pode ser copiado, colado e executado.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### Saída esperada

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

Abra `TableProtection_Modified.xlsx` no Excel. Você verá a tabela **Orders** com apenas a linha de cabeçalho restante; todas as linhas de dados foram removidas.

## Tratamento de variações comuns e casos de borda

| Situação | Ajuste recomendado | Motivo |
|-----------|-------------------|--------|
| A tabela usa senha | Passe a senha para `Unprotect` e `Protect` | Garante o mesmo nível de segurança após a operação |
| A tabela não tem linhas de dados | Pule a chamada `DeleteRows` | Evita um `ArgumentOutOfRangeException` |
| Várias tabelas precisam ser limpas | Percorra `worksheet.ListObjects` e aplique a mesma lógica | Escala o padrão **delete rows excel table** para toda a planilha |
| Você quer manter o cabeçalho e a primeira linha de dados | Altere para `DeleteRows(2, dataRows‑1)` | Inicia a exclusão após a segunda linha, preservando a primeira linha de dados |

Essas variações demonstram um tratamento robusto de **excel table row deletion** e reforçam por que a abordagem apresentada é a recomendada.

## Dicas avançadas

* **Processamento em lote** – Se precisar excluir linhas de muitas pastas de trabalho, encapsule a lógica em um método reutilizável que aceite parâmetros `Workbook` e `tableName`.
* **Desempenho** – Excluir linhas em uma única chamada (`DeleteRows`) é mais rápido do que remover linhas uma a uma, pois o Aspose.Cells atualiza as estruturas internas apenas uma vez.
* **Segurança** – Sempre trabalhe em uma cópia do arquivo original ou mantenha um backup antes de aplicar exclusões, especialmente quando **protect excel table rows** está envolvido.

## Conclusão

Agora você tem uma solução completa e pronta para produção de **aspose cells delete rows** enquanto preserva o cabeçalho de uma tabela do Excel. O guia abordou o carregamento da pasta de trabalho, o tratamento de tabelas protegidas, a execução da operação **remove rows except header** e a restauração da proteção. Aplique o mesmo padrão a qualquer cenário de **excel table row deletion** e adapte o código para atender a requisitos adicionais, como tabelas protegidas por senha ou processamento em lote.

---

*Próximos passos* – Explore tópicos relacionados, como **delete rows excel table** com filtros, mesclar células após a remoção de linhas ou usar Aspose.Cells para copiar tabelas entre pastas de trabalho. Cada um desses amplia os conceitos centrais demonstrados aqui e aprofunda seu domínio da automação Excel com Aspose.Cells.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}