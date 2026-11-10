---
category: general
date: 2026-10-01
description: Aprenda como adicionar propriedades personalizadas a uma pasta de trabalho
  do Excel usando Aspose.Cells. Este guia também mostra como adicionar o ID do projeto
  e ler propriedades personalizadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: pt
lastmod: 2026-10-01
og_description: Adicione propriedades personalizadas a uma pasta de trabalho do Excel
  com Aspose.Cells. Siga este tutorial completo para adicionar um ID de projeto, definir
  informações do revisor e ler propriedades personalizadas programaticamente.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Adicionar propriedades personalizadas à pasta de trabalho do Excel – guia
  passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como adicionar propriedades personalizadas a uma pasta de trabalho do Excel
url: /pt/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como adicionar propriedades personalizadas a uma pasta de trabalho do Excel

Se você precisar **adicionar propriedades personalizadas** a uma pasta de trabalho do Excel, este guia mostra exatamente como fazer isso com Aspose.Cells para .NET. Você também aprenderá como adicionar um ID de projeto, definir o nome de um revisor e, posteriormente, **ler propriedades personalizadas** do arquivo.

Trabalhar com metadados personalizados permite incorporar informações específicas de negócios diretamente na planilha, facilitando o rastreamento de propriedade, versão ou qualquer outro contexto sem manter um banco de dados separado. As etapas abaixo cobrem o fluxo de trabalho completo de ponta a ponta, desde a criação da pasta de trabalho até a persistência das novas propriedades.

## Pré-requisitos

* .NET 6.0 ou posterior instalado  
* Uma licença válida do Aspose.Cells para .NET (ou um teste gratuito)  
* Visual Studio 2022 (ou qualquer IDE C#)  

Nenhum pacote NuGet adicional é necessário além de `Aspose.Cells`.

## Etapa 1: Configurar o projeto e importar namespaces

Crie uma nova aplicação console e adicione a referência ao Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

O namespace `Aspose.Cells` contém as classes `Workbook`, `Worksheet` e `CustomPropertyCollection` que usaremos.

## Etapa 2: Carregar uma pasta de trabalho existente (ou criar uma nova)

Você pode começar com um arquivo `.xlsb` existente ou gerar uma nova pasta de trabalho. O exemplo abaixo carrega um arquivo chamado **Data.xlsb** localizado em uma pasta chamada `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Se o arquivo não existir, substitua o código por `new Workbook();` para criar uma pasta de trabalho em branco.

## Etapa 3: Adicionar propriedades personalizadas à primeira planilha

A operação principal é **adicionar propriedades personalizadas** a uma planilha. O Aspose.Cells armazena propriedades personalizadas em uma coleção que se comporta como um dicionário.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Usamos `CustomProperties.Add` em vez de `CustomProperties["Name"] = value` porque o método `Add` cria a entrada se ela não existir e garante que o tipo de dado correto seja armazenado. Essa abordagem evita incompatibilidades de tipo acidentais que podem causar erros em tempo de execução ao ler os valores posteriormente.

## Etapa 4: Salvar a pasta de trabalho com as novas propriedades

Depois de inserir os metadados, persista as alterações em um novo arquivo para que o original permaneça intacto.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Neste ponto o arquivo Excel contém os metadados personalizados que você definiu. Você pode verificar as propriedades usando as etapas na seção seguinte.

## Etapa 5: Ler propriedades personalizadas de uma pasta de trabalho

Ler **propriedades personalizadas do Excel** segue o mesmo padrão de coleção. Este trecho demonstra como recuperar os valores que acabamos de armazenar.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

O indexador `CustomPropertyCollection` retorna um objeto `CustomProperty`; acessar sua propriedade `Value` fornece os dados armazenados em seu tipo original. Verificar se é `null` antes de converter evita `NullReferenceException` caso uma propriedade esteja ausente.

### Saída esperada no console

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

O carimbo de data/hora refletirá o momento exato em que você chamou `Add` na etapa 3.

## Dica profissional: Atualizando uma propriedade personalizada existente

Se você precisar **adicionar informações personalizadas** mais tarde (por exemplo, alterar o revisor), use o setter `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Esse padrão garante que a propriedade seja atualizada ou criada, o que é útil em fluxos de trabalho iterativos, como a geração automática de relatórios.

## Etapa 6: Verificar as propriedades no Excel (opcional)

Você também pode visualizar as propriedades personalizadas diretamente no Excel:

1. Abra o arquivo `DataWithProps.xlsb` salvo no Microsoft Excel.  
2. Vá em **Arquivo → Informações → Propriedades → Propriedades avançadas**.  
3. Selecione a aba **Personalizado**.  

Você verá as entradas `ProjectId`, `Reviewer` e `CreatedOn` listadas com seus respectivos valores.

## Exemplo completo em funcionamento

Abaixo está o programa completo e autocontido que combina todos os trechos anteriores. Copie‑o para `Program.cs` e execute; o console exibirá os valores recuperados.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Executar este programa produz a saída do console mostrada anteriormente e cria `DataWithProps.xlsb` contendo os metadados incorporados.

## Perguntas comuns e casos extremos

| Pergunta | Resposta |
|---|---|
| **Posso armazenar tipos não‑primitivos?** | O Aspose.Cells suporta `string`, `int`, `double`, `DateTime` e `bool`. Para objetos complexos, serialize‑os para JSON ou XML primeiro e armazene a string. |
| **E se a pasta de trabalho estiver protegida por senha?** | Abra a pasta de trabalho com uma senha (`new Workbook(path, password)`) antes de acessar `CustomProperties`. As propriedades ainda ficam acessíveis após a descriptografia. |
| **As propriedades personalizadas sobrevivem à conversão de formato?** | Ao salvar em um formato diferente (por exemplo, `.xlsx`), o Aspose.Cells preserva as propriedades personalizadas, desde que o formato de destino as suporte. |
| **Como excluir uma propriedade personalizada?** | Use `worksheet.CustomProperties.Remove("PropertyName");`. Isso remove a entrada da coleção. |

## Próximos passos

Agora que você sabe **adicionar propriedades personalizadas**, pode explorar tópicos relacionados, como:

* **excel custom properties** para versionamento de documentos  
* **read custom properties** de várias planilhas em uma única pasta de trabalho  
* Usando **Aspose.Cells** para criar tabelas dinâmicas que referenciam metadados personalizados  
* Exportar a pasta de trabalho para PDF mantendo as propriedades personalizadas  

Experimente diferentes tipos de dados, combine propriedades personalizadas com comentários de células ou integre os metadados em um sistema maior de gerenciamento de documentos.

---

**Pronto para automatizar seus relatórios em Excel?** Adicione o código acima ao seu projeto, ajuste os nomes das propriedades para atender às necessidades do seu negócio, e você terá uma planilha auto‑descritiva pronta para o processamento subsequente.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel – Adicionar Propriedades Personalizadas e Salvar como XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Como Acessar Propriedades de Documento Personalizadas no Excel Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Domine Propriedades Personalizadas do Excel Usando Aspose.Cells .NET para Gerenciamento de Dados Aprimorado](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}