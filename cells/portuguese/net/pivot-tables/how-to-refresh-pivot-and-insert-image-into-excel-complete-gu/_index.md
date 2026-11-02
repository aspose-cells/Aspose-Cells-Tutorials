---
category: general
date: 2026-04-07
description: Aprenda a atualizar a tabela dinâmica, inserir imagem no Excel e salvar
  a pasta de trabalho do Excel com um espaço reservado para imagem em apenas alguns
  passos.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: pt
og_description: Como atualizar uma tabela dinâmica no Excel, inserir imagem no Excel
  e salvar a pasta de trabalho do Excel usando C# com um placeholder de imagem. Exemplo
  de código passo a passo.
og_title: Como atualizar a tabela dinâmica e inserir imagem no Excel – Guia Completo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como atualizar a tabela dinâmica e inserir imagem no Excel – Guia Completo
url: /pt/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como atualizar uma Tabela Dinâmica e inserir imagem no Excel – Guia Completo

Já se perguntou **como atualizar uma Tabela Dinâmica** quando os dados de origem mudam e, em seguida, inserir uma imagem nova do gráfico ou da tabela diretamente na mesma planilha? Você não está sozinho. Em muitos fluxos de relatório, os dados vivem em um banco de dados, a Tabela Dinâmica os traz, e o arquivo final do Excel precisa mostrar os números mais recentes como uma imagem — para que os usuários posteriores não possam editar acidentalmente a fonte.

Neste tutorial vamos percorrer exatamente isso: **como atualizar a Tabela Dinâmica**, **inserir imagem no Excel**, e finalmente **salvar a pasta de trabalho do Excel** usando um **marcador de posição de imagem**. Ao final, você terá um único programa C# executável que faz tudo isso, e entenderá por que cada linha é importante.

> **Dica profissional:** A abordagem funciona com Aspose.Cells 2024 ou posterior, o que significa que você não precisa do Excel instalado no servidor.

---

## O que você vai precisar

- **Aspose.Cells for .NET** (pacote NuGet `Aspose.Cells`).  
- .NET 6.0 SDK ou posterior (o código também compila com .NET 8).  
- Um arquivo Excel básico (`input.xlsx`) que já contenha uma Tabela Dinâmica e um marcador de posição de imagem (o primeiro objeto de imagem na planilha).  
- Um pouco de curiosidade sobre os modelos de objeto do Excel.

Sem interop COM extra, sem instalação do Office, apenas C# puro.

---

## Como atualizar a Tabela Dinâmica e capturar os dados mais recentes

A primeira coisa que você deve fazer é dizer ao Excel (ou melhor, ao Aspose.Cells) que a Tabela Dinâmica deve recalcular com base no intervalo de origem mais novo. Pular esta etapa deixa você com números desatualizados, o que anula todo o propósito da automação.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Por que isso importa:**  
Quando você chama `Refresh()`, o motor da Tabela Dinâmica reexecuta sua lógica de agregação. Se você exportar a Tabela Dinâmica como imagem depois, a foto exibirá os totais *atuais*, não os que estavam no arquivo na última vez que foi salvo.

---

## Inserir imagem no Excel usando um marcador de posição de imagem

Agora que a Tabela Dinâmica está atualizada, precisamos transformá‑la em uma imagem estática. Isso é útil quando você quer travar a visualização para distribuição ou incorporá‑la em um slide do PowerPoint mais tarde.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

O objeto `ImageOrPrintOptions` permite controlar resolução, fundo e formato. PNG é sem perdas e funciona muito bem para a maioria dos relatórios empresariais.

---

## Adicionar marcador de posição de imagem a uma planilha

A maioria dos modelos Excel já contém uma forma ou imagem que funciona como um “slot” para gráficos dinâmicos. Se você não tem um, basta inserir uma imagem em branco no Excel e salvar o modelo — o Aspose.Cells a exporá como `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**E se você tiver vários marcadores de posição?**  
Basta mudar o índice (`Pictures[1]`, `Pictures[2]`, …) ou percorrer `worksheet.Pictures` para encontrar um pelo nome.

---

## Salvar a pasta de trabalho do Excel após as modificações

Por fim, persistimos as alterações. A pasta de trabalho agora contém uma Tabela Dinâmica atualizada, um PNG recém‑gerado e o marcador de posição de imagem atualizado com essa imagem.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Ao abrir `output.xlsx` você verá o slot de imagem preenchido com a captura mais recente da Tabela Dinâmica. Nenhum passo manual necessário.

---

## Exemplo completo (Todas as etapas juntas)

Abaixo está o programa completo, pronto para copiar e colar. Ele inclui as declarações `using` necessárias, tratamento de erros e comentários que explicam cada linha não óbvia.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Resultado esperado:**  
Abra `output.xlsx`. O primeiro objeto de imagem agora mostra um PNG da Tabela Dinâmica atualizada. Se você mudar os dados de origem em `input.xlsx` e executar o programa novamente, a imagem será atualizada automaticamente — sem necessidade de copiar‑colar manual.

---

## Variações comuns e casos de borda

| Situação | O que mudar |
|-----------|----------------|
| **Múltiplas tabelas dinâmicas** | Percorra `sheet.PivotTables` e atualize cada uma, depois escolha a que você precisa para a imagem. |
| **Formato de imagem diferente** | Defina `ImageFormat = ImageFormat.Jpeg` (ou `Bmp`) em `ImageOrPrintOptions`. |
| **Seleção dinâmica de marcador** | Use `sheet.Pictures["MyPlaceholderName"]` em vez de um índice. |
| **Pastas de trabalho grandes** | Aumente `Workbook.Settings.CalculateFormulaEngine` para `EngineType.Fast` para atualizações mais rápidas. |
| **Execução em servidor sem interface** | Aspose.Cells funciona totalmente sem UI, portanto nenhuma configuração extra é necessária. |

---

## Perguntas Frequentes

**P: Isso funciona com pastas de trabalho habilitadas para macro (`.xlsm`)?**  
R: Sim. Aspose.Cells as trata como qualquer outra pasta de trabalho; as macros são preservadas, mas não são executadas durante a atualização.

**P: E se a Tabela Dinâmica usar uma fonte de dados externa?**  
R: Você deve garantir que a string de conexão seja válida na máquina onde o código está sendo executado. Use `pivotTable.CacheDefinition.ConnectionInfo` para ajustá‑la programaticamente.

**P: Posso colocar a imagem em um intervalo de células específico em vez de um marcador de posição?**  
R: Absolutamente. Use `sheet.Pictures.Add(row, column, pivotImg)` onde `row` e `column` são índices baseados em zero.

---

## Conclusão

Cobremos **como atualizar a Tabela Dinâmica**, **inserir imagem no Excel**, **adicionar marcador de posição de imagem** e, finalmente, **salvar a pasta de trabalho do Excel** — tudo em um trecho de C# bem organizado. Atualizando a Tabela Dinâmica primeiro, você garante que a imagem reflita os números mais recentes, e ao usar um marcador de posição mantém seus modelos limpos e reutilizáveis.

Próximos passos que você pode explorar:

- Exportar a mesma imagem para um relatório PDF (`PdfSaveOptions`).  
- Automatizar um lote de arquivos com diferentes dados de origem.  
- Usar Aspose.Slides para colar o PNG diretamente em um slide do PowerPoint.

Sinta‑se à vontade para experimentar — troque o PNG por JPEG, altere o DPI ou adicione várias imagens. A ideia central permanece a mesma: mantenha os dados atualizados, capture‑os como imagem e incorpore‑os onde precisar.

Boa codificação! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}