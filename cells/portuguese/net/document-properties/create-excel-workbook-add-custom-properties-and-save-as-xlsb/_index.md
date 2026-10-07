---
category: general
date: 2026-03-22
description: Criar pasta de trabalho do Excel, adicionar propriedades personalizadas,
  definir o nome da planilha e salvar como arquivo binário XLSB usando C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: pt
og_description: Criar uma pasta de trabalho do Excel, adicionar propriedades personalizadas,
  definir o nome da planilha e salvar como arquivo binário XLSB usando C#.
og_title: Criar Pasta de Trabalho do Excel – Adicionar Propriedades Personalizadas
  e Salvar como XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar Pasta de Trabalho do Excel – Adicionar Propriedades Personalizadas e
  Salvar como XLSB
url: /pt/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel – Adicionar Propriedades Personalizadas e Salvar como XLSB

Já precisou **criar uma pasta de trabalho Excel** programaticamente, mas também manter alguns metadados anexados? Talvez você esteja construindo um mecanismo de relatórios que marca cada arquivo com um ID de relatório, nome do autor ou número da versão. Nesse caso, aprender a **adicionar propriedades personalizadas** enquanto **define o nome da planilha** e, finalmente, **salva como XLSB** economizará muito trabalho manual de pós‑processamento.

Neste tutorial, percorreremos um exemplo completo e executável que mostra exatamente como **escrever um arquivo Excel binário** usando C#. Você verá por que o formato XLSB é a escolha certa para transportar propriedades personalizadas, como evitar as armadilhas mais comuns e o que fazer se precisar oferecer suporte a versões mais antigas do Excel.

---

## O que Você Precisa

- **.NET 6+** (ou .NET Framework 4.6+). O código funciona em qualquer runtime recente.
- **Aspose.Cells for .NET** (versão de avaliação ou licenciada). Ele fornece as classes `Workbook`, `Worksheet` e `CustomProperties` usadas abaixo.
- Uma IDE com a qual você se sinta confortável – Visual Studio, Rider ou até mesmo VS Code serve.
- Permissão de gravação em uma pasta onde o arquivo gerado será salvo.

Nenhuma outra biblioteca de terceiros é necessária.

---

## Etapa 1: Instalar Aspose.Cells

Para começar, adicione o pacote NuGet Aspose.Cells ao seu projeto:

```bash
dotnet add package Aspose.Cells
```

> **Dica profissional:** Se você estiver em um servidor de CI, armazene a chave de licença em uma variável de ambiente e carregue‑a em tempo de execução – isso impede que a marca d'água de “avaliação” apareça no seu output.

---

## Etapa 2: Criar Pasta de Trabalho Excel – Visão Geral

A primeira ação real é **criar a pasta de trabalho Excel**. Esse objeto representa todo o arquivo na memória e fornece acesso a planilhas, estilos e propriedades personalizadas.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Por que instanciar um `Workbook` novo em vez de carregar um modelo? Uma pasta de trabalho em branco garante que não haja estilos ocultos ou propriedades personalizadas residuais, o que é especialmente importante quando você pretende **escrever um arquivo Excel binário** para sistemas downstream que esperam um ponto de partida limpo.

---

## Etapa 3: Definir Nome da Planilha (e Por Que Isso Importa)

As planilhas do Excel têm, por padrão, nomes como “Sheet1”, “Sheet2”, etc. Dar à planilha um nome significativo facilita o processamento downstream — como Power Query ou macros VBA — tornando a leitura muito mais simples.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Se você tentar atribuir um nome duplicado, o Aspose.Cells lançará uma `ArgumentException`. Para ficar seguro, você pode verificar `Worksheets.Exists("Data")` antes de renomear.

---

## Etapa 4: Adicionar Propriedades Personalizadas

As propriedades personalizadas são armazenadas no XML interno da pasta de trabalho e viajam com o arquivo independentemente do formato. Elas são perfeitas para incorporar coisas como `ReportId` ou `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Por que usar propriedades personalizadas?**  
> • Elas são acessíveis via o painel “Arquivo → Informações → Propriedades” do Excel.  
> • O código que consome a pasta de trabalho pode lê‑las sem precisar analisar o conteúdo das células.  
> • Elas sobrevivem a conversões de formato (XLSX ↔ XLSB) porque fazem parte dos metadados do arquivo.

Você também pode armazenar datas, booleanos ou até blobs binários, mas mantenha a carga útil pequena — o Excel não é um banco de dados.

---

## Etapa 5: Salvar como XLSB (Escrever Arquivo Excel Binário)

O formato XLSB armazena os dados em uma estrutura binária, o que torna o arquivo menor e mais rápido de abrir. Mais importante para este tutorial, **as propriedades personalizadas são incorporadas ao fluxo binário**, garantindo que viajem junto com o arquivo.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Resultado Esperado

Depois de executar o programa, você encontrará `WithCustomProps.xlsb` na sua área de trabalho. Abra-o no Excel, vá em **Arquivo → Informações → Propriedades**, e verá `ReportId` e `GeneratedBy` listados em *Personalizado*.

---

## Etapa 6: Casos de Borda & Perguntas Frequentes

### E se a pasta de destino for somente‑leitura?

Envolva a chamada `Save` em um bloco `try/catch` e faça fallback para um local gravável pelo usuário, como `%TEMP%`. Isso impede que a aplicação trave por erros de permissão.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Posso **salvar como XLSX** e ainda manter as propriedades personalizadas?

Sim — basta mudar `SaveFormat.Xlsb` para `SaveFormat.Xlsx`. As propriedades são armazenadas na mesma parte XML, portanto sobrevivem à troca de formato. Contudo, arquivos XLSX são maiores porque são XML compactado, enquanto XLSB oferece melhor desempenho para grandes volumes de dados.

### Como leio as propriedades personalizadas depois?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Este trecho imprime cada propriedade personalizada, facilitando a verificação da procedência do arquivo por serviços downstream.

---

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Nenhuma parte está faltando — tudo, desde as instruções `using` até o `Console.WriteLine` final, está incluído.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Execute o programa, abra o arquivo resultante e verifique as propriedades personalizadas. Esse é o fluxo completo de **criar pasta de trabalho Excel**, **adicionar propriedades personalizadas**, **definir nome da planilha** e **salvar como XLSB** em uma sequência organizada.

---

## Conclusão

Agora você sabe exatamente como **criar uma pasta de trabalho Excel**, dar à sua planilha um **nome de planilha claro**, incorporar metadados úteis com **adicionar propriedades personalizadas** e, finalmente, **salvar como XLSB** para produzir um arquivo Excel compacto e binário. Esse fluxo de trabalho é confiável, funciona em várias versões do .NET e escala bem, seja gerando um relatório ou mil.

Qual o próximo passo? Experimente adicionar uma tabela de dados à planilha “Data”, teste diferentes tipos de propriedade (datas, booleanos) ou altere a saída para **salvar como xlsb** em conjuntos de dados massivos. Você também pode explorar a proteção da pasta de trabalho com senha — o Aspose.Cells faz isso em uma única linha.

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo, ou compartilhar como você estendeu esse padrão em seus próprios projetos. Boa codificação!  

---  

![Create Excel workbook screenshot](image.png){alt="Criar pasta de trabalho Excel com propriedades personalizadas"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}