---
category: general
date: 2026-06-21
description: Como usar o Excel para mala direta com C#. Aprenda a adicionar a tag
  de abertura à célula, criar modelos e gerar arquivos mesclados em minutos.
draft: false
keywords:
- how to use excel for mail merge
- add opening tag to cell
- excel mail merge c#
- c# asp.net mail merge
- generate excel templates programmatically
language: pt
og_description: Como usar o Excel para mala direta? Este guia mostra como adicionar
  a tag de abertura à célula, criar um modelo e executar a mesclagem usando C#.
og_title: Como usar o Excel para mala direta – Tutorial passo a passo em C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use Excel for mail merge with C#. Learn to add opening tag to
    cell, build templates, and generate merged files in minutes.
  headline: How to Use Excel for Mail Merge – Complete C# Guide
  type: TechArticle
tags:
- Excel
- Mail Merge
- C#
- Aspose.Cells
title: Como usar o Excel para mala direta – Guia completo em C#
url: /pt/net/templates-reporting/how-to-use-excel-for-mail-merge-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar o Excel para Mala Direta – Guia Completo em C#

Já se perguntou **como usar o Excel para mala direta** sem abrir o Excel manualmente a cada vez? Você não está sozinho. Em muitos painéis corporativos precisamos espalhar dados em uma planilha pré‑formatada e, em seguida, enviar o resultado para um cliente ou um sistema de relatórios. A boa notícia? Com algumas linhas de C# você pode transformar uma pasta de trabalho vazia em um modelo de mala‑direta completo e deixar o motor fazer o trabalho pesado.

Neste tutorial vamos percorrer exatamente **como usar o Excel para mala direta** usando a biblioteca Aspose.Cells. Também abordaremos a etapa frequentemente negligenciada de **add opening tag to cell**, que é a chave para aninhar coleções como Departamentos → Funcionários. Ao final, você terá um projeto pronto‑para‑executar que gera `output.xlsx` a partir de um arquivo `template.xlsx`.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 SDK ou superior (o código funciona em .NET Core e .NET Framework)
- Visual Studio 2022 ou qualquer editor de sua preferência
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Uma pasta chamada `YOUR_DIRECTORY` (ou altere os caminhos no código)

Nenhuma outra dependência é necessária, e o exemplo funciona no Windows, Linux ou macOS.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Criar um novo aplicativo de console é muito fácil:

```bash
dotnet new console -n ExcelMailMergeDemo
cd ExcelMailMergeDemo
dotnet add package Aspose.Cells
```

Agora abra `Program.cs` e adicione as instruções `using` necessárias:

```csharp
using System;
using Aspose.Cells;
```

> **Dica profissional:** Se você estiver usando o Visual Studio, o IDE sugerirá a adição do `using` automaticamente quando você digitar `Workbook`.

## Etapa 2: Carregar a Pasta de Trabalho que Contém o Modelo

A primeira coisa que você precisa fazer ao **add opening tag to cell** é ter uma pasta de trabalho carregada na memória. Essa pasta de trabalho se tornará, mais tarde, o modelo para o motor de mala‑direta.

```csharp
// Step 1: Load the workbook that will contain the template
Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");
```

Se `template.xlsx` ainda não existir, o Aspose.Cells criará uma nova pasta de trabalho vazia para você. Isso é útil para experimentos rápidos.

## Etapa 3: Acessar a Planilha de Destino

A maioria dos modelos vive na primeira planilha, mas você pode direcionar qualquer índice. Aqui pegamos a primeira planilha:

```csharp
// Step 2: Access the first worksheet where the template will be placed
Worksheet ws = workbook.Worksheets[0];
```

Lembre‑se de que as planilhas são indexadas a partir de zero, então `[0]` é a primeira aba que você vê no Excel.

## Etapa 4: **Add Opening Tag to Cell** – Iniciar a Coleção Pai

As tags de mala‑direta seguem a sintaxe Mustache/Handlebars (`{{#Collection}}`). Para dizer ao motor que uma coleção de departamentos está prestes a começar, escrevemos a tag de abertura em uma célula:

```csharp
// Step 3: Insert the opening tag for the parent collection (Departments)
ws.Cells["A1"].PutValue("{{#Departments}}");
```

Por que colocá‑la em `A1`? Porque queremos que a tag seja a primeira coisa que o motor leia. Você poderia escolher qualquer célula, mas manter as tags no topo facilita a leitura do modelo.

## Etapa 5: Inserir um Marcador de Posicionamento para o Nome do Departamento

Agora precisamos de um local onde o nome de cada departamento aparecerá durante a mesclagem:

```csharp
// Step 4: Add a placeholder for the department name
ws.Cells["A2"].PutValue("Dept: {{Name}}");
```

O token `{{Name}}` será substituído pela propriedade `Name` de cada objeto `Department` que você passar ao motor.

## Etapa 6: **Add Opening Tag to Cell** – Iniciar a Coleção Aninhada

Departamentos geralmente têm muitos funcionários. Para iterar sobre eles, abrimos uma coleção aninhada logo após o nome do departamento:

```csharp
// Step 5: Mark the start of the nested collection (Employees) inside each department
ws.Cells["A3"].PutValue("{{#Employees}}");
```

Observe que novamente estamos **add opening tag to cell**—desta vez a tag é `{{#Employees}}`. O aninhamento funciona porque o motor mantém uma pilha de tags abertas.

## Etapa 7: Inserir Marcadores de Posicionamento para os Detalhes do Funcionário

Cada funcionário normalmente tem nome e sobrenome. Vamos adicionar uma única linha que será repetida para cada funcionário:

```csharp
// Step 6: Insert placeholders for employee details
ws.Cells["A4"].PutValue("{{FirstName}} {{LastName}}");
```

Você pode adicionar mais colunas (por exemplo, `{{Title}}`, `{{Salary}}`) sem mudar a lógica; basta colocá‑las em células adjacentes.

## Etapa 8: Fechar as Coleções Aninhada e Pai

Toda tag de abertura precisa de uma contraparte de fechamento. Primeiro fechamos a coleção `Employees` e, em seguida, a coleção `Departments`:

```csharp
// Step 7: Close the nested collection and then the parent collection
ws.Cells["A5"].PutValue("{{/Employees}}");
ws.Cells["A6"].PutValue("{{/Departments}}");
```

Se você esquecer uma tag de fechamento, a mesclagem lançará uma exceção—algo que abordaremos na seção “Problemas Comuns”.

## Etapa 9: Salvar o Modelo Pronto para a Mesclagem

Neste ponto a pasta de trabalho contém um modelo totalmente formado. Salve‑o para que o processador de mala‑direta possa utilizá‑lo mais tarde:

```csharp
// Step 8: Save the workbook with the template ready for mail‑merge processing
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Agora você tem `output.xlsx` contendo apenas as tags. Em um cenário de produção, você manteria esse arquivo separado e o usaria como um modelo reutilizável.

## Etapa 10: Executar a Mala Direta (Opcional, mas Recomendado)

Se quiser ver todo o pipeline em ação, crie um modelo de dados simples e invoque a mesclagem:

```csharp
// Define data models
public class Department
{
    public string Name { get; set; }
    public Employee[] Employees { get; set; }
}

public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

// Build sample data
var data = new[]
{
    new Department
    {
        Name = "Sales",
        Employees = new[]
        {
            new Employee { FirstName = "Alice", LastName = "Anderson" },
            new Employee { FirstName = "Bob", LastName = "Brown" }
        }
    },
    new Department
    {
        Name = "Engineering",
        Employees = new[]
        {
            new Employee { FirstName = "Charlie", LastName = "Clark" },
            new Employee { FirstName = "Dana", LastName = "Doe" }
        }
    }
};

// Load the template we just saved
Workbook template = new Workbook("YOUR_DIRECTORY/output.xlsx");

// Perform the mail merge
template.Worksheets[0].MailMerge.ExecuteTemplate(data);

// Save the merged result
template.Save("YOUR_DIRECTORY/merged_result.xlsx");
```

Executar este trecho produz `merged_result.xlsx` onde cada departamento e seus funcionários aparecem na ordem definida pelo array de dados.

### Saída Esperada

| A (mesclado) |
|--------------|
| Dept: Sales |
| Alice Anderson |
| Bob Brown |
| Dept: Engineering |
| Charlie Clark |
| Dana Doe |

Se você abrir o arquivo no Excel verá exatamente o que as tags descrevem.

## Problemas Comuns & Casos de Borda

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| **Tag de fechamento ausente** (`{{/Employees}}` ou `{{/Departments}}`) | O motor espera uma pilha de tags balanceada. | Verifique duas vezes se cada `{{#…}}` tem um `{{/…}}` correspondente. |
| **Tag colocada em célula mesclada** | Células mescladas podem confundir o analisador porque o endereço da célula subjacente muda. | Mantenha as tags em células simples, não mescladas (A1‑A6 no nosso exemplo). |
| **Conjuntos de dados grandes** | Renderizar milhares de linhas pode atingir limites de memória. | Use `MailMerge.ExecuteTemplate` com `SaveOptions` que transmitem os dados para o disco. |
| **Layout de planilha diferente** | Se seu modelo usar uma ordem de planilhas diferente, o código ainda aponta para `[0]`. | Recupere a planilha pelo nome: `workbook.Worksheets["Template"]`. |
| **Caracteres especiais nos dados** | Caracteres como `{` ou `}` dentro dos dados quebram a sintaxe das tags. | Escape‑os ou use uma sintaxe de placeholder diferente (`[[FirstName]]`). |

## Dicas para uma Experiência Tranquila

- **Dica profissional:** Mantenha todas as tags na coluna **A** e deixe o restante das colunas conter conteúdo estático (cabeçalhos, fórmulas, formatação). Essa separação facilita a manutenção do modelo.
- **Fique atento a:** Se precisar de seções condicionais (`{{#if …}}`), o Aspose.Cells oferece suporte a tags condicionais básicas, mas elas também devem ser **add opening tag to cell** da mesma forma.
- **Verificação de versão:** O código acima usa Aspose.Cells 23.9.0. Versões mais recentes podem introduzir pequenas alterações na API, portanto, sempre consulte as notas de lançamento.

## Visão Geral Visual

![Exemplo de modelo de mala‑direta no Excel mostrando como usar o Excel para mala direta](/images/excel-mail-merge-template.png){: .center alt="exemplo de modelo de como usar o Excel para mala direta"}

A captura de tela (texto alternativo inclui a palavra‑chave principal) mostra a colocação exata das tags nas células A1‑A6.

## Conclusão

Aí está – um exemplo completo e executável que demonstra **como usar o Excel para mala direta** do início ao fim, e mostra exatamente como **add opening tag to cell** para

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código totalmente funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Acessar uma Célula do Excel por Nome Usando Aspose.Cells for .NET: Um Guia Passo a Passo](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)
- [Como Adicionar Bordas a Células do Excel Usando Aspose.Cells for .NET: Um Guia Passo a Passo](/cells/english/net/formatting/add-borders-excel-cells-aspose-cells-dotnet/)
- [Como Adicionar Quebras de Página no Excel Usando Aspose.Cells for .NET – Um Guia Abrangente](/cells/english/net/headers-footers/aspose-cells-net-add-page-breaks-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}