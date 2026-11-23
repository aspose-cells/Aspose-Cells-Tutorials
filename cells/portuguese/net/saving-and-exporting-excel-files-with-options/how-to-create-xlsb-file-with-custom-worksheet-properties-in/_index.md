---
category: general
date: 2026-11-22
description: Crie um arquivo xlsb em C# e aprenda como adicionar propriedades a uma
  planilha do Excel; salve a pasta de trabalho como xlsb usando Aspose.Cells para
  armazenamento binário rápido.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create xlsb file
- how to add properties
- excel worksheet custom properties
- custom worksheet properties
- save workbook as xlsb
language: pt
lastmod: 2026-11-22
og_description: Criar arquivo xlsb em C# usando Aspose.Cells. Este tutorial mostra
  como adicionar propriedades a uma planilha do Excel e salvar a pasta de trabalho
  como xlsb para armazenamento binário rápido.
og_image_alt: Screenshot of an Excel workbook saved as .xlsb with custom worksheet
  properties displayed in the file explorer
og_title: Criar arquivo xlsb com propriedades personalizadas – Guia C#
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  headline: How to create xlsb file with custom worksheet properties in C#
  type: TechArticle
- description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  name: How to create xlsb file with custom worksheet properties in C#
  steps:
  - name: Open your preferred IDE (Visual Studio, Rider, or VS Code).
    text: Open your preferred IDE (Visual Studio, Rider, or VS Code).
  - name: 'Create a new console project:'
    text: 'Create a new console project:'
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: Open the file.
    text: Open the file.
  - name: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
    text: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
  - name: You will see the `Department` and `Reviewed` entries.
    text: You will see the `Department` and `Reviewed` entries.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar um arquivo xlsb com propriedades de planilha personalizadas em C#
url: /pt/net/saving-and-exporting-excel-files-with-options/how-to-create-xlsb-file-with-custom-worksheet-properties-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar um arquivo xlsb com propriedades de planilha personalizadas em C#

Se você precisa **criar um arquivo xlsb** programaticamente, este guia fornece uma solução completa. Você verá exatamente **como adicionar propriedades** a uma planilha Excel e então **salvar a pasta de trabalho como xlsb** com Aspose.Cells. As etapas funcionam com .NET 6 ou superior e não exigem instalação manual do Excel.

O tutorial aborda a configuração do projeto, criação da pasta de trabalho, adição de propriedades personalizadas à planilha, salvamento do arquivo no formato binário do Excel e verificação do resultado. Ao final, você poderá gerar uma pasta de trabalho *.xlsb* compacta que contém metadados como departamento ou status de revisão.

## Criar arquivo xlsb – visão geral

Criar um arquivo *.xlsb* difere do formato clássico *.xlsx* apenas na etapa final de salvamento. A estrutura da pasta de trabalho, as planilhas e os dados das células são idênticos; o formato binário reduz o tamanho do arquivo e acelera a abertura no Excel. O exemplo de código abaixo demonstra todo o ciclo de vida, de uma pasta de trabalho vazia até um arquivo *.xlsb* salvo que contém **excel worksheet custom properties**.

## Configurar Aspose.Cells no seu projeto C#

1. Abra sua IDE preferida (Visual Studio, Rider ou VS Code).  
2. Crie um novo projeto de console:

   ```bash
   dotnet new console -n XlsbDemo
   cd XlsbDemo
   ```

3. Adicione o pacote NuGet Aspose.Cells:

   ```bash
   dotnet add package Aspose.Cells
   ```

   O pacote fornece as classes `Workbook`, `Worksheet` e `CustomPropertyCollection` necessárias para este tutorial.

## Como adicionar propriedades a uma planilha Excel

Propriedades personalizadas de planilha permitem armazenar metadados arbitrários ao lado da aba. Elas são úteis para processamento posterior, trilhas de auditoria ou dicas de UI. O código a seguir cria uma pasta de trabalho, acessa a primeira planilha e adiciona duas propriedades: uma string `Department` e um booleano `Reviewed`.

```csharp
using Aspose.Cells;

class XlsbCustomPropsDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();                 // workbook is the container for all sheets
        Worksheet worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Add custom properties to the worksheet
        // These are *excel worksheet custom properties* that travel with the sheet.
        worksheet.CustomProperties.Add("Department", "Finance");
        worksheet.CustomProperties.Add("Reviewed", true);

        // Step 3: Save the workbook in binary Excel format (.xlsb)
        // The file will contain the custom properties defined above.
        workbook.Save("CustomProps.xlsb");
    }
}
```

**Por que essas linhas são importantes**

- `Workbook()` constrói uma representação em memória de um arquivo Excel.  
- `worksheet.CustomProperties.Add` armazena pares chave‑valor que o Excel pode ler via a caixa de diálogo *Custom Properties*.  
- `workbook.Save` com a extensão `.xlsb` aciona o caminho **save workbook as xlsb**, usando automaticamente o formato binário.

Você pode adicionar qualquer número de propriedades; a coleção aceita strings, números, datas e booleanos. Se precisar lê‑las depois, use `worksheet.CustomProperties["Department"]`.

## Salvar a pasta de trabalho como xlsb

O método `Save` determina o formato do arquivo a partir da extensão. Fornecer `"CustomProps.xlsb"` instrui o Aspose.Cells a gravar a pasta de trabalho binária. Esta etapa é o único lugar onde **save workbook as xlsb** aparece no código, mas o efeito é visível em todo o tamanho do arquivo e na velocidade de abertura.

Se preferir controlar o formato explicitamente, use o objeto `SaveOptions`:

```csharp
// Alternative: specify the save format with SaveOptions
var options = new XlsbSaveOptions(SaveFormat.Xlsb);
workbook.Save("CustomPropsExplicit.xlsb", options);
```

Ambas as abordagens produzem um arquivo *.xlsb* válido que contém as **custom worksheet properties** que você definiu.

## Verificar propriedades personalizadas da planilha

Depois que o programa for executado, abra o `CustomProps.xlsb` gerado no Excel:

1. Abra o arquivo.  
2. Clique com o botão direito na aba da planilha e escolha **View Code** → **Properties** (ou use a caixa de diálogo *File → Info → Properties*).  
3. Você verá as entradas `Department` e `Reviewed`.

A presença dessas entradas confirma que as **excel worksheet custom properties** foram incorporadas corretamente.

### Saída esperada

Executar o programa cria dois arquivos na pasta do projeto:

- `CustomProps.xlsb` – a pasta de trabalho binária com propriedades personalizadas.  
- `CustomPropsExplicit.xlsb` – conteúdo idêntico, salvo via `XlsbSaveOptions`.

Ambos os arquivos abrem no Excel sem avisos e exibem os metadados personalizados ao serem inspecionados.

## Armadilhas comuns e dicas de boas práticas

- **Não misture extensões de arquivo.** Usar `.xlsx` enquanto passa `XlsbSaveOptions` resulta em um arquivo corrompido. Sempre combine a extensão ao formato escolhido.  
- **Nomes de propriedades diferenciam maiúsculas de minúsculas** na coleção. Acesse‑as com a chave exata usada ao adicioná‑las.  
- **Grandes pastas de trabalho se beneficiam do formato binário** porque o tamanho do arquivo pode reduzir em até 50 % comparado ao `.xlsx`. Isso é especialmente verdadeiro quando a pasta contém muitas fórmulas ou estilos.  
- **Segurança de threads:** instâncias de `Workbook` não são thread‑safe. Crie uma instância separada por thread se gerar vários arquivos simultaneamente.  

## Próximos passos

Agora que você pode **criar um arquivo xlsb** com **custom worksheet properties**, pode explorar:

- Adicionar **excel worksheet custom properties** a várias planilhas na mesma pasta de trabalho.  
- Usar **how to add properties** para linhas ou células via a coleção `Cell.CustomProperties`.  
- Exportar a pasta de trabalho para PDF ou HTML preservando os metadados.  
- Automatizar o processo em uma API web que devolve um stream *.xlsb* diretamente ao cliente.

Essas extensões permitem construir pipelines robustos de automação Excel que aproveitam a velocidade do formato binário e a flexibilidade dos metadados personalizados.

---

*Você aprendeu como criar uma pasta de trabalho *.xlsb* em C#, adicionar propriedades personalizadas de planilha e salvar o arquivo usando Aspose.Cells. Aplique os padrões acima aos seus próprios relatórios orientados a dados, dashboards ou serviços de troca de dados.*

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [How to Save XLSB and Add Custom Document Properties in C#](/cells/english/net/document-properties/how-to-save-xlsb-and-add-custom-document-properties-in-c/)
- [How to Save XLSB with Custom Properties in C# – Step‑by‑Step Guide](/cells/english/net/document-properties/how-to-save-xlsb-with-custom-properties-in-c-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}