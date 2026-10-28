---
category: general
date: 2026-09-24
description: Exportar intervalo do Excel como imagem em C# usando Aspose.Cells – guia
  passo a passo para salvar uma área da planilha como PNG ou JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: pt
lastmod: 2026-09-24
og_description: Exporte intervalo do Excel como imagem em C# com Aspose.Cells. Aprenda
  a converter qualquer área da planilha, incluindo tabelas dinâmicas, para PNG ou
  JPEG em minutos.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Exportar intervalo do Excel como imagem com C# – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Como exportar intervalo do Excel como imagem com C# e Aspose.Cells
url: /pt/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar intervalo do Excel como imagem com C# e Aspose.Cells

Se você precisa **exportar intervalo do Excel como imagem** em uma aplicação .NET, este guia mostra uma solução completa, pronta‑para‑executar. Seja publicando um painel, incorporando uma tabela dinâmica em uma página web ou gerando uma miniatura de relatório, você pode transformar qualquer área da planilha em PNG (ou JPEG) com apenas algumas linhas de código C#.

Neste tutorial você aprenderá a:

* Carregar uma pasta de trabalho existente (`Workbook` class)  
* Definir o intervalo exato de células que deseja capturar (`PrintArea`)  
* Configurar opções de exportação de imagem (`ImageOrPrintOptions`)  
* Salvar a imagem resultante no disco  

Todos os pré‑requisitos, casos de borda e armadilhas comuns são abordados para que você possa adaptar o código aos seus próprios projetos sem surpresas.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

| Requisito | Motivo |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Fornece as APIs `Workbook`, `Worksheet` e `ImageOrPrintOptions` usadas no exemplo. |
| **.NET 6.0 ou posterior** | O exemplo tem como alvo o .NET 6, mas qualquer versão do .NET Core/Framework que suporte Aspose.Cells funciona. |
| **Um arquivo Excel válido** (por exemplo, `input.xlsx`) | A pasta de trabalho que você deseja converter. |
| **Permissão de escrita na pasta de saída** | Necessário para que `Save` seja bem‑sucedido. |

Você pode instalar o Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Exportar intervalo do Excel como imagem – visão geral do processo

A operação consiste em três fases lógicas:

1. **Load** a pasta de trabalho do disco.  
2. **Define** a área de células que se tornará a imagem (a *área de impressão*).  
3. **Export** a área usando `ImageOrPrintOptions` e grave o arquivo.

A seguir, cada fase é detalhada em uma etapa dedicada com código‑fonte completo e explicação.

## Etapa 1: Carregar a pasta de trabalho

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Por que isso importa:**  
`Workbook` é o ponto de entrada para todas as operações do Excel. Carregar o arquivo uma única vez mantém o uso de memória baixo e permite acessar qualquer planilha posteriormente.

## Etapa 2: Acessar a planilha de destino

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Dica:** Se precisar de uma planilha específica pelo nome, substitua o índice por `workbook.Worksheets["SheetName"]`. Isso evita erros quando o layout da pasta de trabalho mudar.

## Etapa 3: Definir o intervalo que você deseja exportar

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Por que definir `PrintArea`?**  
Aspose.Cells renderiza a *área de impressão* ao criar uma imagem. Ao restringi‑la ao intervalo exato, você evita espaços em branco extras e melhora o desempenho.

### Alternativa: Exportar a planilha inteira

Se quiser a planilha completa, simplesmente omita a atribuição de `PrintArea`. O Aspose.Cells usará o intervalo usado da planilha por padrão.

## Etapa 4: Configurar opções de exportação de imagem

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Explicação das propriedades principais:**

* `ImageFormat` – Determina o tipo de arquivo (`Png`, `Jpeg`, `Bmp`, etc.). PNG é ideal para gráficos e texto porque preserva bordas nítidas.  
* `HorizontalResolution` / `VerticalResolution` – Controlam a densidade de pixels. Para miniaturas web, 96 DPI é suficiente; para gráficos prontos para impressão, 300 DPI é recomendado.  
* `PageOrientation` – Ajuda quando o intervalo selecionado é mais largo que alto.

## Etapa 5: Exportar o intervalo para um arquivo de imagem

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**O que acontece nos bastidores:**  
Quando `PrintArea` está definido, o Aspose.Cells gera uma imagem temporária representando aquela área. O objeto `Pictures[0]` é então salvo usando as opções fornecidas.

### Lidando com planilhas sem imagens

Se a planilha ainda não contiver uma imagem (por exemplo, um arquivo recém‑criado), você pode criar uma sobre‑voo:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Exemplo completo e executável

Juntando tudo, aqui está um aplicativo console autocontido que você pode copiar, colar e executar:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Saída esperada:**  
Um arquivo chamado `range.png` aparece em `YOUR_DIRECTORY`. Ao abri‑lo, você verá as células exatas de **A1 a G20** renderizadas como uma imagem PNG nítida.

## Variações comuns e tratamento de casos de borda

| Cenário | Ajuste |
|----------|------------|
| **Exportar para JPEG** | Altere `ImageFormat = ImageFormat.Jpeg` e, opcionalmente, defina `Quality = 90` (intervalo 0‑100). |
| **Múltiplos intervalos** | Chame `sheet.Pictures.Add` para cada intervalo e salve cada imagem com um nome de arquivo distinto. |
| **Planilhas grandes** | Aumente `HorizontalResolution`/`VerticalResolution` apenas para o intervalo necessário para evitar picos de memória. |
| **Nenhuma imagem gerada** | Verifique se `PrintArea` está formatado corretamente (`"A1:G20"`). Um endereço inválido resulta em uma coleção `Pictures` vazia. |
| **Salvando em um stream** | Use `pic.Save(Stream, imgOptions)` quando precisar da imagem em memória (por exemplo, para uma resposta ASP.NET). |

## Dicas profissionais para exportação de imagem confiável

* **Validar a área de impressão** – Use o parsing de `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) para construir intervalos programaticamente e evitar erros de digitação.  
* **Liberar recursos** – Envolva `Workbook` em um bloco `using` se estiver processando muitos arquivos para liberar recursos nativos rapidamente.  
* **Processamento em lote** – Ao exportar dezenas de intervalos, reutilize uma única instância de `ImageOrPrintOptions` para reduzir a sobrecarga de alocação de objetos.  
* **Segurança de thread** – Os objetos Aspose.Cells **não** são seguros para uso em múltiplas threads. Crie um `Workbook` separado por thread ou sincronize o acesso.

## Conclusão

Agora você tem um método completo e pronto para produção para **exportar intervalo do Excel como imagem** usando C# e Aspose.Cells. As etapas — carregar a pasta de trabalho, definir a área de impressão, configurar `ImageOrPrintOptions` e salvar a imagem — cobrem tanto o “como” quanto o “por quê”, garantindo que você possa adaptar o código a tabelas dinâmicas, gráficos ou qualquer bloco de células personalizado.

Em seguida, você pode explorar:

* **Exportar intervalo do Excel como imagem** em outros formatos (SVG, BMP) – outra palavra‑chave secundária para experimentar.  
* **Incorporar o PNG em um PDF** usando Aspose.PDF para geração de relatórios de ponta a ponta.  
* **Automatizar exportações em lote** em várias pastas de trabalho com um simples loop de console.

Sinta‑se à vontade para experimentar diferentes resoluções, orientações e diretórios de saída. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Exportar Células do Excel para Imagem Usando Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Exportar Pasta de Trabalho do Excel como Imagem Usando Aspose.Cells para Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Como Exportar uma Planilha do Excel para PNG Usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}