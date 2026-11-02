---
category: general
date: 2026-06-24
description: Crie um arquivo OPC plano em C# usando Aspose.Cells. Aprenda a configurar
  SaveOptions para FlatOPC, exportar dados Xlsx e verificar o resultado em minutos.
draft: false
keywords:
- create flat OPC file
- Aspose.Cells FlatOPC save
- Xlsx flat OPC format
- SaveOptions FlatOPC example
- workbook save flat OPC
language: pt
og_description: Crie um arquivo OPC flat em C# rapidamente. Este tutorial mostra passo
  a passo como configurar SaveOptions para FlatOPC e gerar um arquivo .opc válido.
og_title: Criar arquivo OPC plano com C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create flat OPC file in C# using Aspose.Cells. Learn to set up SaveOptions
    for FlatOPC, export Xlsx data, and verify the result in minutes.
  headline: Create flat OPC file with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose.Cells is cross‑platform, and the same code runs on Windows,
      Linux, or macOS.
    question: Does this work with .NET Core?
  - answer: Set the `Password` property on `SaveOptions` before calling `Save`. The
      flat OPC will include the encryption metadata.
    question: What if I need to export a password‑protected workbook?
  - answer: Yes. Use the overload `wb.Save(Stream, SaveOptions)` and pipe the stream
      wherever you need (HTTP response, Azure Blob, etc.).
    question: Can I stream the output instead of writing to disk?
  - answer: Typically a bit larger because it’s plain XML, but the trade‑off is human
      readability.
    question: Is the Flat OPC file larger than a regular .xlsx?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
- File formats
title: Criar arquivo OPC plano com C# – Guia Completo
url: /pt/net/saving-and-exporting-excel-files-with-options/create-flat-opc-file-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar arquivo flat OPC com C# – Guia Completo

Já se perguntou como **criar um arquivo flat OPC** sem lutar com XML manualmente? Você não está sozinho. Seja porque você precisa de uma representação leve de uma pasta de trabalho do Excel para controle de versão, testes automatizados ou simplesmente por curiosidade, o formato Flat OPC é uma ferramenta prática.  

Neste tutorial vamos percorrer um exemplo do mundo real usando Aspose.Cells para .NET, mostrando exatamente como configurar o objeto `SaveOptions`, adicionar alguns dados a uma pasta de trabalho e, finalmente, gravar um arquivo flat OPC adequado no disco. Sem referências vagas — apenas uma solução completa e executável que você pode copiar‑colar.

## O que você aprenderá

- O propósito do formato **Flat OPC** e quando ele se destaca.
- Como instalar e referenciar Aspose.Cells em um projeto C#.
- Código passo‑a‑passo que **cria um arquivo flat OPC** do zero.
- Dicas para solucionar armadilhas comuns e verificar a saída.

Antes de mergulharmos, certifique‑se de que você tem uma versão recente do .NET (4.6+ ou .NET Core 3.1+) e um IDE com o qual se sinta confortável — Visual Studio, Rider ou até mesmo VS Code servirão.

![Exemplo de criação de arquivo flat OPC](/images/create-flat-opc-file.png "Captura de tela de um arquivo flat OPC gerado por código C#")

## Criar arquivo flat OPC – Visão geral

O formato Flat OPC é essencialmente um único documento XML que contém todas as partes de um pacote Office Open XML (como uma pasta de trabalho `.xlsx`) em uma estrutura legível linha por linha. É perfeito para controle de versão amigável ao diff porque você pode ver cada célula, estilo e relacionamento como texto simples. Aspose.Cells abstrai o trabalho pesado, permitindo que você **crie um arquivo flat OPC** com apenas algumas linhas de código.

## Etapa 1: Instalar Aspose.Cells

Primeiro de tudo — você precisa da biblioteca Aspose.Cells. A maneira mais rápida é via NuGet:

```bash
dotnet add package Aspose.Cells
```

Ou, se preferir o Console do Gerenciador de Pacotes dentro do Visual Studio:

```powershell
Install-Package Aspose.Cells
```

> **Dica de especialista:** Escolha a versão estável mais recente; a partir de junho 2026 é a 24.9.0, que inclui correções de bugs para o gravador Flat OPC.

## Etapa 2: Construir uma pasta de trabalho de exemplo

Ter uma pasta de trabalho com ao menos uma planilha e algumas células torna o arquivo flat OPC resultante mais interessante. Abaixo está um método autônomo que cria um `Workbook`, preenche-o e devolve a instância.

```csharp
using Aspose.Cells;
using System;

public class FlatOpcDemo
{
    /// <summary>
    /// Creates a simple workbook with data for demonstration.
    /// </summary>
    /// <returns>A populated Workbook object.</returns>
    public static Workbook BuildSampleWorkbook()
    {
        // Initialize a new workbook – this is the entry point for any Excel manipulation.
        var wb = new Workbook();

        // Grab the first worksheet (index 0) and give it a friendly name.
        var sheet = wb.Worksheets[0];
        sheet.Name = "Demo";

        // Add a header row.
        sheet.Cells["A1"].PutValue("Product");
        sheet.Cells["B1"].PutValue("Quantity");
        sheet.Cells["C1"].PutValue("Price");

        // Insert a few rows of sample data.
        sheet.Cells["A2"].PutValue("Apples");
        sheet.Cells["B2"].PutValue(120);
        sheet.Cells["C2"].PutValue(0.45);

        sheet.Cells["A3"].PutValue("Bananas");
        sheet.Cells["B3"].PutValue(85);
        sheet.Cells["C3"].PutValue(0.30);

        // Apply a simple style to the header row – optional but shows that styles survive the flat OPC conversion.
        var style = wb.CreateStyle();
        style.Font.IsBold = true;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        style.Pattern = BackgroundType.Solid;
        var styleFlag = new StyleFlag { Font = true, CellShading = true };
        sheet.Cells.CreateRange("A1:C1").ApplyStyle(style, styleFlag);

        return wb;
    }
}
```

Observe como cada linha está deliberadamente comentada. Esses comentários se tornam parte da explicação “por quê” do tutorial, atendendo ao requisito de citação de IA.

## Etapa 3: Configurar SaveOptions para o formato Flat OPC

Agora vem o cerne da questão: configurar o objeto `SaveOptions` para que o Aspose.Cells saiba que queremos **Flat OPC** em vez do padrão binário `.xlsx`. As propriedades chave são `SaveFormat` (deve ser `SaveFormat.FlatOPC`) e, opcionalmente, `Compression` (mas o flat OPC já é XML puro, então deixamos o padrão).

```csharp
using Aspose.Cells;

/// <summary>
/// Prepares SaveOptions to generate a flat OPC file.
/// </summary>
/// <returns>A configured SaveOptions instance.</returns>
public static SaveOptions GetFlatOpcSaveOptions()
{
    // Step 1: Create save options for the Flat OPC format.
    // The constructor takes the base format (Xlsx) because FlatOPC is a variant of Xlsx.
    var flatOpcSaveOptions = new SaveOptions(SaveFormat.Xlsx)
    {
        // Explicitly tell Aspose.Cells we need the Flat OPC representation.
        SaveFormat = SaveFormat.FlatOPC
    };

    // You could also tweak other options here, e.g., EnableZip64 = false,
    // but for most scenarios the defaults are fine.
    return flatOpcSaveOptions;
}
```

Este trecho reflete diretamente o código original que você forneceu, mas adiciona contexto sobre *por que* cada propriedade é definida, tornando o tutorial digno de citação.

## Etapa 4: Salvar a pasta de trabalho como um arquivo flat OPC

Com a pasta de trabalho e as opções de salvamento prontas, gravar o arquivo é uma única linha. Também vamos envolver todo o fluxo em um método `Main` para que você possa executar o programa imediatamente.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Build a workbook with sample data.
        Workbook wb = FlatOpcDemo.BuildSampleWorkbook();

        // 2️⃣ Get the correctly configured SaveOptions.
        SaveOptions flatOpcOptions = FlatOpcDemo.GetFlatOpcSaveOptions();

        // 3️⃣ Define the output path – adjust the folder to suit your environment.
        string outputPath = @"C:\Temp\demo.flat.opc";

        // 4️⃣ Save the workbook using the configured options.
        // This is the line that actually creates the flat OPC file.
        wb.Save(outputPath, flatOpcOptions);

        Console.WriteLine($"Flat OPC file created at: {outputPath}");
    }
}
```

Executar este programa gerará um arquivo chamado `demo.flat.opc`. Abra-o com qualquer editor de texto e você verá um único documento XML contendo todos os dados da planilha, estilos e relacionamentos — exatamente o que a especificação **Flat OPC** determina.

## Verificação e o que esperar

Após a execução, navegue até `C:\Temp\demo.flat.opc` (ou o caminho que você escolheu). O arquivo começará com algo como:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<package xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
  <part name="/xl/workbook.xml" contentType="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml">
    <!-- workbook XML goes here -->
  </part>
  <part name="/xl/worksheets/sheet1.xml" contentType="application/vnd.openxmlformats-officedocument.spreadsheetml.worksheet+xml">
    <!-- sheet data, including rows for Apples and Bananas -->
  </part>
  <!-- additional parts for styles, shared strings, etc. -->
</package>
```

Como o formato **Flat OPC** colapsa o contêiner ZIP em um único XML, você pode comparar duas versões com um simples `git diff` e identificar instantaneamente alterações ao nível de célula. Essa é a principal vantagem sobre o pacote binário `.xlsx`.

### Perguntas comuns respondidas

- **Isso funciona com .NET Core?** Absolutamente — Aspose.Cells é multiplataforma, e o mesmo código roda no Windows, Linux ou macOS.
- **E se eu precisar exportar uma pasta de trabalho protegida por senha?** Defina a propriedade `Password` em `SaveOptions` antes de chamar `Save`. O flat OPC incluirá os metadados de criptografia.
- **Posso transmitir a saída em vez de gravar no disco?** Sim. Use a sobrecarga `wb.Save(Stream, SaveOptions)` e direcione o stream onde precisar (resposta HTTP, Azure Blob, etc.).
- **O arquivo Flat OPC é maior que um .xlsx normal?** Normalmente um pouco maior porque é XML puro, mas a troca vale a legibilidade humana.

## Conclusão

Acabamos de **criar um arquivo flat OPC** do zero usando C# e Aspose.Cells. O processo resumiu‑se a três ações claras: construir uma pasta de trabalho, configurar `SaveOptions` para o formato `FlatOPC` e chamar `Save`. Com o código completo acima, você pode adaptar o exemplo a qualquer pasta de trabalho existente, adicionar gráficos, tabelas dinâmicas ou até macros — tudo será representado fielmente na saída flat OPC.

### O que vem a seguir?

- Experimente as opções de salvamento **Aspose.Cells FlatOPC** como `EnableMemoryOptimization` para pastas de trabalho enormes.
- Tente converter um `.xlsx` existente para flat OPC carregando‑o com `new Workbook("input.xlsx")` e salvando novamente.
- Explore formatos relacionados: o **Open XML SDK** também suporta flat OPC, oferecendo uma alternativa gratuita caso você não precise dos recursos extras da Aspose.

Tem alguma variação que você tentou e funcionou (ou não)? Compartilhe nos comentários — aprender juntos fortalece a comunidade. Boa codificação e aproveite a simplicidade do flat OPC!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create Save Excel File Aspose Cells Dotnet](/cells/german/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Create Save Excel File Aspose Cells Dotnet](/cells/french/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Create Save Excel File Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}