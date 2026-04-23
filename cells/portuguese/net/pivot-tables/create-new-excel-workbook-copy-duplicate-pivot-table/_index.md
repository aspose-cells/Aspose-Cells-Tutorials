---
category: general
date: 2026-02-09
description: Crie uma nova pasta de trabalho do Excel e aprenda a copiar tabelas dinâmicas
  sem esforço. Este guia mostra como duplicar a tabela dinâmica e salvar a pasta de
  trabalho como nova.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: pt
og_description: Crie uma nova pasta de trabalho Excel em C# e copie uma tabela dinâmica
  instantaneamente. Aprenda como duplicar a tabela dinâmica e salvar a pasta de trabalho
  como nova com um exemplo de código completo.
og_title: Criar Nova Pasta de Trabalho do Excel – Cópia de Tabela Dinâmica Passo a
  Passo
tags:
- excel
- csharp
- aspose.cells
- automation
title: Criar Nova Pasta de Trabalho do Excel – Copiar e Duplicar Tabela Dinâmica
url: /pt/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho Excel – Copiar & Duplicar Tabela Dinâmica

Já precisou **criar nova pasta de trabalho Excel** que mantenha uma tabela dinâmica complexa de um arquivo existente? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao automatizar pipelines de relatórios. A boa notícia é que, com algumas linhas de C# e a biblioteca Aspose.Cells, você pode **como copiar pivot** rapidamente, **duplicar tabela dinâmica**, e **salvar pasta de trabalho como nova** sem abrir o Excel manualmente.

Neste guia percorreremos todo o processo, desde o carregamento da pasta de trabalho fonte até a gravação da versão duplicada. Ao final, você terá um trecho pronto‑para‑executar que pode ser inserido em qualquer projeto .NET. Sem enrolação, apenas uma solução prática que você pode testar hoje.

## O Que Este Tutorial Cobre

* **Pré‑requisitos** – .NET 6+ (ou .NET Framework 4.6+), Visual Studio e o pacote NuGet Aspose.Cells para .NET.
* Código passo a passo que **cria nova pasta de trabalho Excel**, copia a tabela dinâmica e grava o resultado no disco.
* Explicações de **por que** cada linha importa, não apenas **o que** ela faz.
* Dicas para lidar com casos extremos, como planilhas ocultas ou intervalos de dados grandes.
* Uma visão rápida de **como copiar planilha** caso você precise da planilha inteira em vez de apenas da tabela dinâmica.

Pronto? Vamos mergulhar.

![ilustração de criar nova pasta de trabalho excel](image.png "Diagrama mostrando pasta de trabalho fonte, cópia da tabela dinâmica e pasta de trabalho de destino")

## Etapa 1: Configurar o Projeto e Instalar Aspose.Cells

Antes de podermos **criar nova pasta de trabalho Excel**, precisamos de um projeto que faça referência à biblioteca correta.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Por que isso importa:* Aspose.Cells funciona totalmente na memória, então você nunca precisa iniciar o Excel no servidor. Ele também preserva as informações de cache da tabela dinâmica, essenciais para uma verdadeira **duplicar tabela dinâmica**.

> **Dica de especialista:** Se você estiver mirando .NET Core, certifique‑se de que o identificador de runtime (RID) do seu projeto corresponda à plataforma onde será implantado; caso contrário, você pode encontrar erros ao carregar bibliotecas nativas.

## Etapa 2: Carregar a Pasta de Trabalho Fonte que Contém a Tabela Dinâmica

Agora vamos **como copiar pivot** de um arquivo existente. A pasta de trabalho fonte pode estar em qualquer lugar no disco, em um stream ou até mesmo em um array de bytes.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Por que escolhemos um intervalo:* Uma tabela dinâmica vive dentro de um intervalo de células regular, mas também possui dados de cache ocultos associados à planilha. Ao copiar o intervalo **incluindo a tabela dinâmica**, Aspose.Cells garante que o cache viaje junto, proporcionando a você uma **duplicar tabela dinâmica** funcional no arquivo de destino.

## Etapa 3: Criar uma Nova Pasta de Trabalho Excel para Receber os Dados Copiados

É aqui que realmente **cria nova pasta de trabalho Excel** que conterá a tabela dinâmica duplicada.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Por que uma pasta de trabalho nova?** Começar do zero garante que nenhuma formatação residual ou objetos ocultos interfiram na tabela dinâmica copiada. Também torna o arquivo resultante menor, o que é útil para anexos de e‑mail automatizados.

## Etapa 4: Copiar o Intervalo da Tabela Dinâmica para a Nova Pasta de Trabalho

Agora executamos a operação real de **como copiar pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Aquela única linha faz o trabalho pesado:

* Os valores das células, fórmulas e formatações são transferidos.
* O cache da tabela dinâmica é duplicado, de modo que a nova tabela permanece totalmente funcional.
* Quaisquer referências relativas dentro da tabela dinâmica são ajustadas automaticamente para a nova localização.

### Lidando com Casos Extremos

* **Planilhas ocultas:** Se a planilha fonte estiver oculta, a tabela dinâmica ainda será copiada corretamente, mas talvez você queira tornar a planilha de destino visível para o usuário:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Conjuntos de dados grandes:** Para intervalos maiores que alguns milhares de linhas, considere usar `CopyTo` com `CopyOptions` para transmitir a operação e reduzir a pressão de memória.

## Etapa 5: Salvar a Pasta de Trabalho de Destino como um Novo Arquivo

Por fim, **salvar pasta de trabalho como nova** e verificar o resultado.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Se você abrir `copied.xlsx` verá uma réplica exata da tabela dinâmica original, pronta para manipulação ou distribuição adicional.

### Opcional: Como Copiar Planilha em Vez de Apenas a Tabela Dinâmica

Às vezes você quer a planilha inteira, não só a tabela dinâmica. A mesma API torna isso trivial:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Isso atende à consulta **como copiar planilha** e pode ser útil quando você precisa preservar configurações adicionais ao nível da planilha.

## Exemplo Completo Funcional

Juntando tudo, aqui está um aplicativo console autônomo que você pode compilar e executar:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Saída esperada:** O console imprime uma mensagem de sucesso, e `copied.xlsx` aparece em `C:\Reports` com uma tabela dinâmica funcional idêntica à de `source.xlsx`.

## Perguntas Frequentes & Armadilhas

* **As fórmulas dentro da tabela dinâmica irão quebrar?** Não—como o cache da tabela dinâmica viaja com o intervalo, todos os campos calculados permanecem intactos.
* **E se a tabela dinâmica fonte usar conexões de dados externas?** Essas conexões *não* são copiadas. Você precisará recriá‑las na pasta de trabalho de destino ou converter a tabela dinâmica em uma tabela estática primeiro.
* **Posso copiar várias tabelas dinâmicas de uma vez?** Sim—basta definir um intervalo maior que englobe todas as tabelas, ou iterar sobre cada objeto `PivotTable` em `sourceSheet.PivotTables` e copiá‑las individualmente.
* **Preciso descartar os objetos `Workbook`?** Eles implementam `IDisposable`, portanto envolver em blocos `using` é uma boa prática, especialmente em serviços de alto volume.

## Conclusão

Agora você sabe **como criar nova pasta de trabalho Excel**, copiar uma tabela dinâmica, **duplicar tabela dinâmica**, e **salvar pasta de trabalho como nova** usando C# e Aspose.Cells. Os passos são simples: carregar, criar, copiar e salvar. Com o trecho opcional **como copiar planilha**, você também tem uma alternativa para duplicação completa da planilha.

Próximos passos, você pode explorar:

* Adicionar formatação personalizada à tabela dinâmica duplicada.
* Atualizar o cache da tabela dinâmica programaticamente após alterações nos dados.
* Exportar a pasta de trabalho para PDF ou CSV para sistemas downstream.

Teste, ajuste o intervalo e deixe a automação eliminar o trabalho manual do seu fluxo de relatórios. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}