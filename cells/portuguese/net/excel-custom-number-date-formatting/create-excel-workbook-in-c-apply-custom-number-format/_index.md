---
category: general
date: 2026-05-23
description: Criar uma pasta de trabalho do Excel em C# e aprender como aplicar formato
  numérico personalizado, definir o estilo da célula programaticamente, formatar a
  célula em notação científica e, em seguida, salvar a pasta de trabalho como xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: pt
og_description: Crie uma pasta de trabalho Excel em C# rapidamente. Aprenda a aplicar
  formato numérico personalizado, estilizar células programaticamente, formatar notação
  científica e salvar em xlsx.
og_title: Criar Pasta de Trabalho Excel em C# – Aplicar Formato de Número Personalizado
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Criar Pasta de Trabalho do Excel em C# – Aplicar Formato Numérico Personalizado
url: /pt/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel em C# – Aplicar Formato Numérico Personalizado

Criar uma pasta de trabalho Excel em C# é mais fácil do que você imagina. Neste guia, vamos mostrar como aplicar um formato numérico personalizado, formatar uma célula em notação científica, definir o estilo da célula programaticamente e, finalmente, salvar a pasta de trabalho em um arquivo xlsx.

Se você já ficou encarando uma planilha em branco e se perguntou como automatizar tudo — desde preencher dados até fazer os números aparecerem exatamente como você precisa — este tutorial é para você. Ao final, você terá um arquivo Excel totalmente funcional que pode abrir em qualquer programa de planilhas, e entenderá **por que** cada passo é importante, não apenas **como** digitar o código.

## O que você vai precisar

- **.NET 6+** (ou qualquer .NET Framework recente que suporte a biblioteca)  
- **Aspose.Cells for .NET** (ou outra API que exponha as classes `Workbook`, `Cell` e `CellFormat`)  
- Um nível razoável de experiência em C# — se você consegue escrever um `Console.WriteLine`, está pronto para prosseguir.  

Nenhum arquivo de configuração extra, sem interop COM, e certamente sem necessidade de instalação manual do Excel.

---

## Criar Pasta de Trabalho Excel – Inicializar o Objeto Workbook

A primeira coisa que precisamos fazer é criar uma pasta de trabalho vazia. Pense na classe `Workbook` como a tela em branco onde você pintará linhas, colunas e estilos.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

É isso — uma linha e você tem um novo arquivo Excel na memória. O construtor `Workbook` cria a coleção padrão de planilhas, permitindo que você comece a adicionar dados imediatamente.

> **Dica profissional:** Se precisar de várias planilhas, você pode chamar `workbook.Worksheets.Add()` antes de começar a preencher as células.

![Exemplo de criação de pasta de trabalho Excel](image-placeholder.png "Captura de tela da criação de pasta de trabalho Excel")

*Texto alternativo da imagem: exemplo de criação de pasta de trabalho Excel mostrando uma planilha Excel em branco na IDE.*

## Aplicar Formato Numérico Personalizado a uma Célula

Agora que a pasta de trabalho existe, vamos inserir um número na célula **A1** e aplicar um formato personalizado. Formatos numéricos personalizados permitem controlar como os números são exibidos — moeda, porcentagens, datas ou, no nosso caso, notação científica.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Por que obter o estilo primeiro? Porque o objeto `Cell` armazena um objeto **Style** que contém fontes, bordas, alinhamento e formatação numérica tudo em um só lugar. Ao editar a propriedade `Custom` informamos ao Excel: “exiba este valor usando notação científica com duas casas decimais.”

> **Pergunta comum:** *Posso usar um formato interno em vez de um personalizado?*  
> Sim — defina `style.Number = 10` para um formato científico interno, mas a string personalizada oferece controle preciso sobre as casas decimais.

## Definir Estilo da Célula Programaticamente (Além do Formato Numérico)

Frequentemente você desejará mais do que apenas um formato numérico. Vamos adicionar uma fonte em negrito e um fundo cinza claro para que a célula se destaque.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Observe que reutilizamos o mesmo objeto `style` que ajustamos anteriormente. Essa é a vantagem de **definir estilo da célula programaticamente** — você obtém o estilo uma única vez, modifica as propriedades necessárias e grava novamente. Não há necessidade de recriar objetos ou perder o formato numérico que já foi definido.

## Formatar Célula em Notação Científica (Tratamento de Casos Limite)

Se você está lidando com números muito grandes ou muito pequenos, a notação científica é uma mão na roda. O formato personalizado que usamos (`0.00E+00`) garante duas casas decimais após o ponto e força o sinal de mais para o expoente. Aqui está uma rápida verificação de sanidade:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Ao abrir o arquivo resultante, B2 aparecerá como `1.23E-05`, confirmando que a diretiva **formatar célula em notação científica** funciona tanto para números grandes quanto pequenos.

## Salvar Pasta de Trabalho em XLSX

Toda a diversão termina quando você realmente grava o arquivo no disco. O método `Save` cuida do trabalho pesado, convertendo a representação em memória em um pacote `.xlsx` adequado.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Essa linha cumpre o objetivo de **salvar pasta de trabalho em xlsx**. Se o diretório não existir, `Save` lançará uma exceção — portanto, assegure-se de que a pasta seja criada previamente ou envolva a chamada em um bloco try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Agora você tem um arquivo Excel pronto para ser compartilhado, com um número científico bem formatado, estilo em negrito e fundo cinza claro.

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para copiar e colar, que une todas as partes. Ele compila como um aplicativo de console, mas você pode inserir a lógica em qualquer projeto C#.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Resultado esperado:** Abra `CustomFormatted.xlsx` e você verá:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Ambas as células estão em negrito, têm preenchimento cinza claro e exibem números em notação científica com duas casas decimais.

---

## Conclusão

Acabamos de **criar pasta de trabalho excel** do zero, **aplicar formato numérico personalizado**, **formatar célula em notação científica**, **definir estilo da célula programaticamente**, e **salvar pasta de trabalho em xlsx** — tudo em algumas linhas de C#. A abordagem escala: basta percorrer as linhas, clonar o objeto `style`, e você terá um relatório totalmente estilizado em segundos.

### O que vem a seguir?

- **Formatação dinâmica:** Alterar formatos com base na magnitude do valor (ex.: moeda vs. porcentagem).  
- **Múltiplas planilhas:** Use `workbook.Worksheets.Add("Summary")` para criar painéis.  
- **Estilização avançada:** Bordas, formatação condicional e validação de dados

## Tutoriais Relacionados

- [Como criar e salvar uma pasta de trabalho Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Criar e salvar pasta de trabalho Excel Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Criar e salvar pasta de trabalho Excel em PDF Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}