---
category: general
date: 2026-06-21
description: Importe JSON para Excel rapidamente e aprenda como converter JSON para
  XLSX, gerar Excel a partir de JSON e exportar JSON para planilha em alguns passos
  fáceis.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: pt
og_description: Importe JSON para Excel sem esforço. Este guia mostra como converter
  JSON para XLSX, gerar Excel a partir de JSON e exportar JSON para planilha usando
  C#.
og_title: Importar JSON para Excel com Aspose.Cells – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Importar JSON para Excel com Aspose.Cells – Guia Completo de Programação
url: /pt/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar JSON para Excel – Guia Completo de Programação

Já se perguntou **como importar JSON para Excel** sem escrever um analisador personalizado? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando precisam transformar um payload JSON em uma planilha organizada para relatórios ou tarefas de análise de dados. A boa notícia? Com Aspose.Cells você pode **converter JSON para XLSX** em apenas algumas linhas, e todo o processo é rápido e seguro em termos de tipos.

Neste tutorial vamos percorrer cada passo necessário para **gerar Excel a partir de JSON**, salvar o resultado como um arquivo `.xlsx` e ainda explorar algumas variações úteis — como exportar JSON para uma planilha que se atualiza automaticamente quando você altera os dados de origem. Ao final, você terá um snippet reutilizável que pode ser inserido em qualquer projeto .NET.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

- .NET 6.0 ou superior (o código também funciona no .NET Framework)
- Uma licença válida do Aspose.Cells for .NET ou uma chave de avaliação temporária
- Visual Studio 2022 (ou qualquer IDE C# de sua preferência)
- Familiaridade básica com estruturas JSON e sintaxe C#

Nenhum pacote NuGet extra além do **Aspose.Cells** é necessário, o que mantém a configuração leve.

## Etapa 1: Instalar Aspose.Cells e Configurar o Projeto

Primeiro de tudo, adicione a biblioteca Aspose.Cells ao seu projeto. Abra o Package Manager Console e execute:

```powershell
Install-Package Aspose.Cells
```

Se estiver usando a CLI do .NET, o equivalente é:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Após a instalação, adicione seu arquivo de licença (`Aspose.Cells.lic`) à raiz do projeto e carregue‑o na inicialização:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Agora você está pronto para começar a **importar JSON para Excel**.

## Etapa 2: Preparar o Payload JSON

Para demonstração, usaremos um array simples de objetos pessoa. Em um cenário real você pode ler essa string de um arquivo, de uma resposta de API ou de um banco de dados.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Observe que o JSON é um array plano — exatamente o formato que funciona melhor com os smart markers do Aspose.Cells.

## Etapa 3: Configurar as Opções de Carregamento do JSON

Aspose.Cells permite tratar todo o array JSON como uma *única* fonte de dados. Isso é crucial quando você quer que as linhas se expandam automaticamente dentro da planilha.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Definir `ArrayAsSingle = true` indica à biblioteca **gerar um smart marker que se repete para cada elemento** do array, que é o coração do fluxo de **converter JSON para XLSX**.

## Etapa 4: Criar o Workbook e Importar o JSON

Agora criamos uma nova instância de `Workbook` e importamos o JSON usando um smart marker chamado `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

Nos bastidores, Aspose.Cells analisa o JSON, mapeia cada propriedade (`Name`, `Age`) para uma coluna e prepara um placeholder que será expandido posteriormente em linhas.

## Etapa 5: Inserir o Smart Marker na Planilha

Um smart marker tem a forma `{{People}}`. Quando o workbook é salvo, Aspose.Cells substitui esse marcador por uma tabela que contém todos os dados do array JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Você pode mover o marcador para qualquer lugar — o canto superior esquerdo é uma escolha comum porque dá à tabela espaço para crescer para baixo e para a direita.

## Etapa 6: Salvar o Workbook como Arquivo XLSX

Finalmente, grave o workbook no disco. É aqui que **salvamos JSON como Excel** e obtemos um verdadeiro arquivo `.xlsx` que pode ser aberto no Excel, Google Sheets ou qualquer outro aplicativo de planilhas.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Ao abrir `JsonSingleCell.xlsx`, você verá algo como:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

Esse é o resultado da **geração de Excel a partir de JSON** em ação.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Saída Esperada

Executar o programa imprime:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

Abrir o arquivo mostra uma tabela de duas linhas com os cabeçalhos **Name** e **Age**, correspondendo exatamente ao array JSON original.

## Variações Avançadas

### 1. Importar Múltiplos Arrays JSON em Planilhas Diferentes

Se você tem vários arrays — por exemplo `"Employees"` e `"Departments"` — pode importar cada um em sua própria planilha:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Agora você **exportou JSON para planilha** com várias abas, cada uma refletindo um conjunto de dados distinto.

### 2. Estilizar a Tabela Gerada

Você pode aplicar um estilo depois que os dados forem expandidos:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Esse pequeno ajuste faz a linha de cabeçalho se destacar, o que é útil para dashboards de relatórios.

### 3. Usar um Arquivo JSON em vez de uma String

Se seu JSON está armazenado em disco, basta lê‑lo primeiro:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

O restante dos passos permanece exatamente o mesmo, então você pode **salvar JSON como Excel** a partir de qualquer fonte.

## Armadilhas Comuns & Como Evitá‑las

- **`ArrayAsSingle` ausente** – Esquecer essa flag fará com que cada objeto seja tratado como uma fonte de dados separada, resultando em células vazias. Sempre defina-a quando seu JSON for um array de nível superior.
- **Nome do Smart Marker Incorreto** – O marcador (`{{People}}`) deve coincidir com o `DataSourceName` que você passou (`"People"`). Um erro de digitação deixará o placeholder sem substituição.
- **Licença Não Carregada** – No modo de avaliação, o arquivo de saída contém uma marca d'água. Carregue sua licença logo no início para manter o workbook limpo.
- **Permissões de Caminho de Arquivo** – Tentar salvar em uma pasta protegida lança uma exceção. Use `Environment.CurrentDirectory` ou um caminho gravável pelo usuário.

## Testando o Resultado Programaticamente

Se quiser verificar que a exportação foi bem‑sucedida sem abrir o Excel, você pode ler a primeira célula de volta:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

Uma verificação rápida no console como essa confirma que **converter JSON para XLSX** funcionou como esperado.

## Conclusão

Acabamos de cobrir tudo que você precisa para **importar JSON para Excel** usando Aspose.Cells: desde a instalação da biblioteca, preparação do JSON, configuração dos smart markers, até o **salvar JSON como Excel**. Seja para **converter JSON para XLSX**, **gerar Excel a partir de JSON**, ou **exportar JSON para planilha** para análises, o padrão permanece o mesmo — os smart markers fazem o trabalho pesado.

Sinta‑se à vontade para experimentar estilos, múltiplas planilhas ou até atualizações dinâmicas re‑importando JSON em tempo de execução. O próximo passo lógico é integrar esse código a uma API web que sirva relatórios Excel sob demanda — basta substituir a linha de gravação de arquivo por um stream retornado ao cliente.

Tem dúvidas sobre casos de borda, como objetos JSON aninhados ou conjuntos de dados grandes? Deixe um comentário abaixo, e feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Efficiently Import JSON to Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}