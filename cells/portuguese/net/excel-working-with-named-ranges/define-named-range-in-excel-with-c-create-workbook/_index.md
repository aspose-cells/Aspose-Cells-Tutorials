---
category: general
date: 2026-08-07
description: Defina um intervalo nomeado no Excel com C# e aprenda como adicionar
  uma tabela a uma planilha, depois salve a pasta de trabalho em um arquivo programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: pt
lastmod: 2026-08-07
og_description: Defina um intervalo nomeado no Excel com C# e veja como adicionar
  uma tabela, criar uma pasta de trabalho programaticamente e salvar a pasta de trabalho
  em um arquivo em um único fluxo.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Defina intervalo nomeado no Excel com C# – tutorial completo da pasta de
  trabalho
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Definir intervalo nomeado no Excel com C# – criar pasta de trabalho
url: /pt/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir intervalo nomeado no Excel com C# – criar pasta de trabalho

Se você precisar **definir intervalo nomeado no Excel** a partir de código C#, este tutorial mostra exatamente como fazer isso. Você também verá como **adicionar uma tabela a uma planilha**, criar a pasta de trabalho **programaticamente** e, finalmente, **salvar a pasta de trabalho em um arquivo** sem sair da IDE.

Trabalhar com arquivos Excel programaticamente economiza tempo, elimina erros manuais e permite pipelines de relatórios automatizados. Neste guia você irá:

* Criar uma nova pasta de trabalho Excel do zero.  
* Adicionar uma tabela que abrange um intervalo de células específico.  
* Definir um intervalo nomeado e lidar com conflitos de nomenclatura.  
* Persistir a pasta de trabalho no disco.

Todas as etapas utilizam a biblioteca **Aspose.Cells for .NET**, que funciona com .NET 6+ e .NET Framework 4.6+. Nenhuma interop COM adicional ou instalação do Office é necessária.

## Pré-requisitos

* .NET 6 SDK (ou .NET Framework 4.6+).  
* Visual Studio 2022 ou qualquer IDE compatível com C#.  
* Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Dica profissional:** Use a licença de avaliação gratuita durante os testes; substitua-a por uma licença de produção antes da implantação.

## Etapa 1: Criar pasta de trabalho Excel programaticamente

A primeira operação é instanciar um objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Por que isso importa*: Criar a pasta de trabalho no código lhe dá controle total sobre planilhas, estilos e dados antes que qualquer arquivo toque o disco.

## Etapa 2: Adicionar tabela à planilha

Uma tabela (também conhecida como ListObject) fornece filtragem, ordenação e estilo integrados. Aqui criamos uma tabela que cobre as células **A1:B5** e damos a ela o nome **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Por que isso importa*: Adicionar uma tabela cedo permite que você faça referência aos dados mais tarde com um **intervalo nomeado**, e a referência estruturada da tabela pode ser usada em fórmulas.

## Etapa 3: Definir intervalo nomeado no Excel – lidar com conflitos

Um **intervalo nomeado** é um identificador que aponta para uma célula ou intervalo, facilitando a leitura das fórmulas. Se um nome já existir (por exemplo, o nome da tabela **SalesData**), o Excel gera um conflito. O código abaixo demonstra como capturar essa exceção e continuar com segurança.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Por que isso importa*: Tratar colisões de nomes evita falhas em tempo de execução em tarefas automatizadas. O segundo intervalo nomeado **SalesTotal** demonstra a referência à coluna da tabela em uma fórmula.

## Etapa 4: Salvar pasta de trabalho em arquivo

Após todas as modificações, persista a pasta de trabalho no disco. O método `Save` suporta vários formatos; aqui usamos o padrão `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Por que isso importa*: Usar **salvar pasta de trabalho em arquivo** programaticamente habilita processamento em lote, geração de relatórios agendados e integração com APIs web.

## Código-fonte completo em uma visualização

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Resultado esperado

* Um arquivo Excel chamado **NameConflictHandled.xlsx** aparece em `C:\Temp`.  
* A Planilha 1 contém uma tabela formatada **SalesData** com linhas de produto‑unidade.  
* A célula **B6** mostra a soma da coluna **Units**, calculada via o intervalo nomeado **SalesTotal**.  
* O console imprime uma mensagem sobre o conflito de nomes (se houver) e confirma a localização do arquivo.

## Perguntas frequentes & casos limites

| Pergunta | Resposta |
|----------|----------|
| **Posso definir um intervalo nomeado que abranja várias planilhas?** | Sim. Use `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` e faça referência a ele a partir de qualquer planilha. |
| **E se eu precisar sobrescrever um arquivo existente?** | Chame `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **Como adiciono um intervalo nomeado sem conflito quando o nome já existe?** | Use `worksheet.Names.Remove("ExistingName")` antes de adicionar o novo, ou gere um identificador único (ex.: `Guid.NewGuid().ToString("N")`). |
| **Existe uma forma de aplicar um estilo à tabela automaticamente?** | Defina `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` após criar a tabela. |
| **Isso funciona no .NET Core?** | Aspose.Cells suporta .NET Core, .NET 5/6/7 e .NET Framework. Basta referenciar o mesmo pacote NuGet. |

## Conclusão

Agora você sabe como **definir intervalo nomeado no Excel** usando C#, **adicionar uma tabela a uma planilha** e **salvar a pasta de trabalho em arquivo** programaticamente. O exemplo completo demonstra a criação de uma pasta de trabalho Excel do zero, o tratamento de conflitos de nomes e a geração de um arquivo de relatório utilizável em um fluxo único e repetível.

Em seguida, explore tópicos relacionados como **adicionar gráficos a uma planilha**, **exportar para PDF** ou **ler pastas de trabalho existentes**. Cada um desses se baseia nos mesmos fundamentos abordados aqui, de modo que você estará pronto para expandir a solução para cenários de automação mais complexos. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar intervalo nomeado de células no Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [Como implementar fórmulas de intervalo nomeado em .NET usando Aspose.Cells para automação Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Como criar intervalos nomeados com escopo de pasta de trabalho no Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}