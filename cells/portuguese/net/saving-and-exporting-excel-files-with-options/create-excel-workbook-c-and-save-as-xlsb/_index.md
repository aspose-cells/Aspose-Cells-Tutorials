---
category: general
date: 2026-11-25
description: Criar pasta de trabalho do Excel em C# e salvar como XLSB enquanto define
  propriedade personalizada da planilha para metadados do relatório.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- save workbook as xlsb
- set worksheet custom property
- Aspose.Cells Excel export
- C# Excel automation
language: pt
lastmod: 2026-11-25
og_description: Crie uma pasta de trabalho Excel em C# e salve como XLSB. Este guia
  mostra como definir uma propriedade personalizada da planilha para que seus relatórios
  mantenham as informações do proprietário.
og_image_alt: Screenshot of a C# program creating an Excel workbook and saving it
  as XLSB
og_title: Criar pasta de trabalho Excel em C# – salvar como XLSB com propriedades
  personalizadas
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  headline: Create Excel workbook C# and save as XLSB
  type: TechArticle
- description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  name: Create Excel workbook C# and save as XLSB
  steps:
  - name: '**Create a new workbook** – the in‑memory representation of an Excel file.'
    text: '**Create a new workbook** – the in‑memory representation of an Excel file.'
  - name: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
    text: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
  - name: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
    text: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
  type: HowTo
tags:
- excel
- csharp
- xlsb
- custom-properties
title: Criar pasta de trabalho Excel em C# e salvar como XLSB
url: /pt/net/saving-and-exporting-excel-files-with-options/create-excel-workbook-c-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel C# e salvar como XLSB

Se você precisa **create Excel workbook C#** para uma rotina de relatórios, provavelmente também quer que o arquivo mantenha metadados extras, como o proprietário do relatório. Este tutorial mostra como **set worksheet custom property** e então **save workbook as XLSB** em um fluxo de trabalho único e reproduzível.

Você terminará com um arquivo XLSB codificado em binário que abre no Excel, preserva a propriedade personalizada e está pronto para distribuição. Nenhum script externo é necessário — apenas a biblioteca Aspose.Cells for .NET e algumas linhas de C#.

## Pré-requisitos

* .NET 6.0 (ou posterior) instalado – Aspose.Cells suporta .NET Standard 2.0+.
* Uma licença válida do Aspose.Cells (ou uma chave de avaliação gratuita).  
* Visual Studio 2022 ou qualquer IDE C# que você prefira.

Add the NuGet package:

```bash
dotnet add package Aspose.Cells
```

> **Dica:** Use o teste gratuito do **Aspose.Cells** para evitar erros de licenciamento em tempo de execução durante os testes.

## Visão geral da criação de pasta de trabalho Excel C# – overview

O processo consiste em três ações atômicas:

1. **Create a new workbook** – a representação em memória de um arquivo Excel.
2. **Set worksheet custom property** – anexa metadados de chave/valor à primeira planilha.
3. **Save workbook as XLSB** – grava o arquivo no formato binário XLSB, que mantém a propriedade personalizada intacta.

Cada passo é ilustrado com código completo e executável.

![Create Excel workbook C# screenshot](excel_workbook.png)

## Etapa 1: Inicializar uma nova pasta de trabalho

```csharp
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();          // creates a default workbook with one worksheet
            Worksheet worksheet = workbook.Worksheets[0]; // reference to the first worksheet
```

**Why this matters** – `Workbook` é o ponto de entrada para todas as operações do Excel. Quando você o instancia sem parâmetros, o Aspose.Cells cria uma pasta de trabalho limpa com uma única planilha, o que é perfeito para geração programática.

## Etapa 2: Definir propriedade personalizada da planilha

```csharp
            // Step 2: Add a custom property to the worksheet (e.g., the report owner)
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
```

*`set worksheet custom property`* é a chamada exata que armazena a chave **ReportOwner** com o valor **Alice** dentro da coleção de propriedades personalizadas da planilha. O Excel pode ler essa propriedade posteriormente via **File → Info → Properties → Advanced Properties**.

> **Pergunta comum:** *E se eu precisar de várias propriedades?*  
> Basta chamar `Add` repetidamente com nomes diferentes, por exemplo, `worksheet.CustomProperties.Add("Department", "Finance");`.

## Etapa 3: Salvar pasta de trabalho como XLSB

```csharp
            // Step 3: Save the workbook in XLSB format – the custom property is preserved
            string outputPath = @"YOUR_DIRECTORY\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);
        }
    }
}
```

A linha **save workbook as xlsb** grava o arquivo usando o formato binário XLSB. Comparado ao clássico XLSX, o XLSB carrega mais rápido para grandes conjuntos de dados e mantém as propriedades personalizadas sem etapas adicionais.

### Resultado esperado

Após executar o programa:

* `custom_props.xlsb` aparece em `YOUR_DIRECTORY`.
* Abrir o arquivo no Excel mostra uma única planilha sem dados visíveis (apenas adicionamos metadados).
* Navegue até **File → Info → Properties → Advanced Properties → Custom** – você verá **ReportOwner = Alice**.

## Verificando a propriedade personalizada programaticamente (optional)

Se você quiser confirmar que a propriedade sobreviveu ao ciclo, pode recarregar o arquivo:

```csharp
            // Verify the property after loading
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            System.Console.WriteLine($"Report owner: {owner}"); // should print "Alice"
```

Executar este trecho imprime:

```
Report owner: Alice
```

## Casos de borda e boas práticas

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Large workbooks (>10 000 rows)         | Use **XLSB** porque sua compressão binária reduz a pegada de memória.          |
| Need to preserve culture‑specific data| Defina `Workbook.Settings.CultureInfo` antes de adicionar valores.                     |
| Multiple worksheets need the same property| Itere sobre `workbook.Worksheets` e adicione a propriedade a cada planilha.        |
| Running on Linux/macOS                 | Garanta que a compilação Aspose.Cells .NET Standard esteja referenciada; sem APIs exclusivas do Windows. |

> **Atenção:** Salvar em um diretório sem permissão de gravação lançará `UnauthorizedAccessException`. Sempre valide o caminho ou use `Path.GetTempPath()` para arquivos temporários.

## Exemplo completo e executável

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create Excel workbook C#
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Set worksheet custom property
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
            worksheet.CustomProperties.Add("ReportDate", DateTime.Today.ToShortDateString());

            // 3️⃣ Save workbook as XLSB
            string outputPath = @"C:\Temp\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // Optional verification
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            Console.WriteLine($"Report owner verified: {owner}");
        }
    }
}
```

Copie o código para um novo projeto de console, substitua `C:\Temp\` por uma pasta que você possua, e execute. O console exibirá `Report owner verified: Alice`, provando que **create Excel workbook C#**, **set worksheet custom property**, e **save workbook as xlsb** funcionaram em conjunto.

## Conclusão

Agora você sabe como **create Excel workbook C#**, anexar uma **worksheet custom property**, e **save workbook as XLSB** em um padrão limpo e pronto para produção. Essa abordagem é ideal para pipelines de relatórios automatizados, serviços de exportação de dados ou qualquer cenário onde metadados precisam acompanhar o arquivo Excel.

Em seguida, você pode explorar:

* Adicionar tabelas de dados e estilizar (`Cells`, objetos `Style`).
* Exportar para outros formatos como **XLSX** ou **CSV** preservando as propriedades.
* Usar **Aspose.Cells** para ler propriedades personalizadas de pastas de trabalho existentes.

Sinta-se à vontade para experimentar diferentes nomes de propriedades, múltiplas planilhas ou grandes conjuntos de dados. O mesmo padrão de três etapas escala de um arquivo simples de uma planilha para soluções de relatórios em nível empresarial. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel C# – Adicionar Propriedade Personalizada e Salvar XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [Criar Pasta de Trabalho Excel – Adicionar Propriedades Personalizadas e Salvar como XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Como criar pasta de trabalho Excel C# com formatação personalizada e salvar como XLSX](/cells/english/net/excel-formatting-and-styling/how-to-create-excel-workbook-c-with-custom-formatting-and-sa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}