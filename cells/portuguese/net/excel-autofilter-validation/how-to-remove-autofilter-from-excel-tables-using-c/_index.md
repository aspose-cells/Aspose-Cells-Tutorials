---
category: general
date: 2026-10-07
description: Aprenda como remover o autofiltro de tabelas do Excel com C#. Este guia
  também mostra como ocultar as setas de filtro no Excel e desativar o filtro de tabelas
  do Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- excel table hide filter
- hide filter arrows excel
- disable excel table filter
language: pt
lastmod: 2026-10-07
og_description: Remova o autofiltro de tabelas do Excel em C# para limpar suas planilhas.
  Siga este tutorial completo para ocultar as setas de filtro no Excel, desativar
  o filtro de tabelas do Excel e salvar uma pasta de trabalho limpa.
og_image_alt: Screenshot of an Excel worksheet after the autofilter UI has been removed
og_title: Remova o autofiltro de tabelas do Excel em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to remove autofilter from Excel tables with C#. This guide
    also shows how to hide filter arrows Excel and disable Excel table filter.
  headline: How to remove autofilter from Excel tables using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Como remover o autofiltro de tabelas do Excel usando C#
url: /pt/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como remover o autofiltro de tabelas do Excel usando C#

Se você precisa **remover o autofiltro do Excel**, este guia mostra como fazer isso programaticamente com C#. Você aprenderá como ocultar as setas de filtro no Excel e desativar o filtro da tabela para que a planilha fique limpa.

O tutorial percorre cada passo necessário — desde a instalação da biblioteca até a gravação da pasta de trabalho final. Ao final, você poderá abrir o arquivo salvo e ver que os ícones de dropdown do filtro desapareceram, a tabela se comporta como um intervalo normal e nenhum elemento de UI distrai o usuário. Não é necessário ter experiência prévia com a API Aspose.Cells, mas é preciso ter conhecimentos básicos de C#.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior instalado  
* Um ambiente de desenvolvimento como Visual Studio 2022 ou VS Code  
* O pacote **Aspose.Cells for .NET** do NuGet (o exemplo de código usa esta biblioteca)  
* Um arquivo Excel que contenha uma tabela com filtro ativo (por exemplo, `TableWithFilter.xlsx`)

Você pode instalar o Aspose.Cells via .NET CLI:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Use a versão estável mais recente do pacote para aproveitar correções de bugs recentes e melhorias de desempenho.

## Etapa 1 – remover autofiltro do Excel: carregar a pasta de trabalho

A primeira operação é carregar a pasta de trabalho que contém a tabela que você deseja modificar. Carregar o arquivo cria uma representação em memória que pode ser manipulada.

```csharp
using Aspose.Cells;

string sourcePath = @"C:\Data\TableWithFilter.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Por que esta etapa importa*: Sem carregar a pasta de trabalho, você não tem acesso à planilha, à tabela (`ListObject`) ou às suas configurações de filtro. A classe `Workbook` abstrai todo o arquivo Excel, tornando as ações subsequentes simples.

## Etapa 2 – localizar a planilha que contém a tabela

A maioria das pastas de trabalho tem uma planilha padrão chamada “Sheet1”. Você também pode direcionar uma planilha pelo índice ou nome. Aqui usamos a primeira planilha.

```csharp
Worksheet worksheet = workbook.Worksheets[0];   // index‑based access
// Alternative: Worksheet worksheet = workbook.Worksheets["Sales"]; // by name
```

*Por que esta etapa importa*: As tabelas estão vinculadas a uma planilha específica. Acessar a planilha correta garante que você modifique o `ListObject` desejado.

## Etapa 3 – obter o ListObject (tabela do Excel) que você quer alterar

Uma tabela no Excel é representada por um `ListObject`. Você pode obtê‑la pelo nome da tabela, que pode ser visto na aba “Table Design” do Excel.

```csharp
// Replace "SalesTable" with the actual table name in your workbook
ListObject salesTable = worksheet.ListObjects["SalesTable"];
```

Se não souber o nome da tabela, pode enumerar todas as tabelas da planilha:

```csharp
foreach (ListObject tbl in worksheet.ListObjects)
{
    Console.WriteLine($"Found table: {tbl.Name}");
}
```

*Por que esta etapa importa*: A propriedade `AutoFilter` está no `ListObject`. Selecionar a tabela correta assegura que você remova a UI de filtro certa.

## Etapa 4 – ocultar as setas de filtro do Excel limpando a UI do AutoFilter

A operação principal é definir a propriedade `AutoFilter` como `null`. Isso remove as setas de dropdown do filtro da linha de cabeçalho da tabela.

```csharp
salesTable.AutoFilter = null;   // removes the filter UI
```

> **Observação:** Definir `AutoFilter` como `null` equivale ao comando “Clear Filter” na UI do Excel, mas também elimina as setas visuais. Isso atende ao requisito de **excel table hide filter** e **disable Excel table filter**.

### Alternativa: desativar o filtro para todas as tabelas da pasta de trabalho

Se sua pasta de trabalho contém várias tabelas e você deseja uma solução abrangente, itere sobre cada `ListObject`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (ListObject tbl in ws.ListObjects)
    {
        tbl.AutoFilter = null;
    }
}
```

## Etapa 5 – salvar a pasta de trabalho modificada

Depois de remover a UI do filtro, persista as alterações em um novo arquivo (ou sobrescreva o original, se preferir).

```csharp
string targetPath = @"C:\Data\TableNoFilter.xlsx";
workbook.Save(targetPath);
Console.WriteLine($"Workbook saved without autofilter at: {targetPath}");
```

*Por que esta etapa importa*: O Excel só reflete as mudanças quando o arquivo é salvo. O novo arquivo será aberto com uma tabela limpa que não mostra mais as setas de filtro.

## Resultado esperado

Abra `TableNoFilter.xlsx` no Excel. Você deverá ver:

* A linha de cabeçalho da tabela não exibe mais as setas de dropdown.  
* Nenhum critério de filtro está aplicado; todas as linhas ficam visíveis.  
* O restante da pasta de trabalho (fórmulas, formatação, gráficos) permanece inalterado.

## Casos de borda e armadilhas comuns

| Situação | Como lidar |
|-----------|------------|
| **Nome da tabela desconhecido** | Use a abordagem de enumeração mostrada na Etapa 3 para descobrir os nomes em tempo de execução. |
| **Múltiplas tabelas na mesma planilha** | Aplique o loop da alternativa na Etapa 4 para limpar os filtros de cada tabela. |
| **Formatos antigos do Excel (`.xls`)** | Aspose.Cells suporta tanto `.xlsx` quanto `.xls`. Carregue o arquivo da mesma forma; a API abstrai as diferenças de formato. |
| **Arquivo somente‑leitura ou bloqueado** | Garanta que o processo tenha permissão de gravação e que o arquivo não esteja aberto no Excel enquanto o código é executado. |
| **Precisa manter a lógica de filtro, mas ocultar as setas** | Em vez de definir `AutoFilter = null`, você pode manter o objeto de filtro e definir `ShowHideButtons = false` (disponível em versões mais recentes da biblioteca). |

## Exemplo completo e executável

Abaixo está um aplicativo console completo que você pode copiar, colar e executar. Ele demonstra cada passo, desde a configuração do projeto até a gravação da pasta de trabalho sem filtro.

```csharp
// Program.cs
using System;
using Aspose.Cells;

namespace ExcelFilterRemoval
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing the table
            string sourcePath = @"C:\Data\TableWithFilter.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Access the first worksheet (or specify by name)
            Worksheet worksheet = workbook.Worksheets[0];

            // 3. Retrieve the table you want to modify
            //    Replace "SalesTable" with your actual table name
            ListObject salesTable = worksheet.ListObjects["SalesTable"];

            // 4. Remove the AutoFilter UI from the table
            salesTable.AutoFilter = null;

            // 5. Save the workbook – the table now has no filter UI
            string targetPath = @"C:\Data\TableNoFilter.xlsx";
            workbook.Save(targetPath);

            Console.WriteLine($"Successfully removed autofilter and saved to {targetPath}");
        }
    }
}
```

Execute o programa com `dotnet run`. Quando terminar, abra o arquivo de saída para verificar que as setas de filtro desapareceram.

## Conclusão

Agora você sabe como **remover o autofiltro de tabelas do Excel** usando C#. O guia abordou carregar uma pasta de trabalho, localizar a tabela alvo, limpar a propriedade `AutoFilter` e salvar o resultado. Seguindo esses passos, você também alcança **excel table hide filter**, **hide filter arrows Excel** e **disable Excel table filter** em um único script repetível.

### O que explorar a seguir

* **Aplicar estilo personalizado** à tabela após remover a UI do filtro.  
* **Proteger a planilha** para impedir que usuários adicionem novos filtros.  
* **Combinar com exportação de dados** (por exemplo, gerar arquivos CSV) para processamento posterior.  

Sinta‑se à vontade para experimentar as abordagens alternativas mostradas na tabela de casos de borda. Se encontrar um cenário não coberto aqui, a documentação do Aspose.Cells oferece métodos adicionais para controle granular do comportamento das tabelas. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [hide filter arrows excel with C# – Complete Guide](/cells/english/net/excel-autofilter-validation/hide-filter-arrows-excel-with-c-complete-guide/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}