---
title: Definir fonte padrão para opções de salvamento de PDF
linktitle: Definir fonte padrão para opções de salvamento de PDF
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a definir fontes padrão para opções de salvamento de PDF usando o Aspose.Cells para .NET, garantindo que seus documentos tenham uma aparência perfeita sempre.
weight: 11
url: /pt/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir fonte padrão para opções de salvamento de PDF

## Introdução
Quando se trata de gerar relatórios, faturas ou quaisquer outros documentos em formato PDF, garantir que seu conteúdo tenha a aparência correta é fundamental. As fontes desempenham um papel vital na manutenção do apelo visual e da legibilidade de seus documentos. No entanto, o que acontece quando a fonte que você usou em seu arquivo Excel não está disponível no sistema onde você está gerando seu PDF? É aí que o Aspose.Cells for .NET é útil. Esta biblioteca poderosa permite que você defina fontes padrão para suas opções de salvamento de PDF, garantindo que seus documentos tenham uma aparência profissional e consistente, não importa onde sejam abertos.
## Pré-requisitos
Antes de começar, certifique-se de ter o seguinte:
1. Visual Studio: você precisará de um ambiente de desenvolvimento como o Visual Studio para escrever e executar seu código.
2.  Aspose.Cells para .NET: Você pode baixar a versão mais recente em[este link](https://releases.aspose.com/cells/net/). Como alternativa, você pode instalá-lo por meio do Gerenciador de Pacotes NuGet no Visual Studio.
3. Conhecimento básico de C#: entender os conceitos básicos de C# ajudará você a acompanhar os exemplos de código.
4. Arquivo Excel de Exemplo: Tenha um arquivo Excel de exemplo pronto para teste. Você pode criar um com várias fontes e estilos para ver como o Aspose.Cells lida com fontes ausentes.
## Pacotes de importação
Antes de poder usar Aspose.Cells no seu projeto, você precisa importar os pacotes necessários. Veja como fazer isso:
1. Abra seu projeto: inicie o Visual Studio e abra seu projeto existente ou crie um novo.
2. Adicionar referências: clique com o botão direito do mouse no seu projeto no Solution Explorer e selecione "Gerenciar pacotes NuGet".
3. Instalar Aspose.Cells: Procure por "Aspose.Cells" e clique no botão "Instalar".
4. Adicione diretivas Using: No topo do seu arquivo C#, inclua os seguintes namespaces:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Etapa 1: configure seus diretórios
Antes de trabalhar com arquivos, é importante definir os diretórios de origem e saída. Isso tornará mais fácil localizar seu arquivo Excel de entrada e salvar os arquivos de saída gerados.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho real para seus diretórios.
## Etapa 2: Abra o arquivo Excel
 Agora que configuramos nossos diretórios, vamos abrir o arquivo Excel com o qual você deseja trabalhar. O`Workbook` A classe em Aspose.Cells é usada para carregar o documento Excel.
```csharp
// Abra um arquivo Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Certifique-se de substituir o nome do arquivo pelo nome real do arquivo.
## Etapa 3: Configurar opções de renderização de imagem
Em seguida, precisamos configurar as opções de renderização para converter nossa planilha do Excel em um formato de imagem. Criaremos uma instância de`ImageOrPrintOptions`, especificando o tipo de imagem e a fonte padrão.
```csharp
// Renderizando para formato de arquivo PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Neste trecho de código, definimos o`CheckWorkbookDefaultFont` propriedade para`false`, o que significa que se alguma fonte estiver faltando, a fonte padrão especificada (“Times New Roman”) será usada.
## Etapa 4: renderizar a planilha como uma imagem
 Agora, vamos renderizar a primeira planilha da pasta de trabalho como uma imagem PNG. Usaremos o`SheetRender` classe para realizar isso.
```csharp
// Renderizar a primeira planilha em uma imagem
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Etapa 5: Altere o tipo de imagem e renderize para TIFF
 Se você quiser renderizar a mesma folha em um formato de imagem diferente, como TIFF, você pode simplesmente alterar o`ImageType` propriedade e repita o processo de renderização.
```csharp
// Definir para formato TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Etapa 6: Configurar opções de salvamento de PDF
 A seguir, vamos configurar as opções de salvamento do PDF. Criaremos uma instância de`PdfSaveOptions`defina a fonte padrão e especifique que queremos verificar se há fontes ausentes.
```csharp
// Configurar opções de salvamento de PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Etapa 7: Salve a pasta de trabalho como PDF
Com as opções de salvamento configuradas, é hora de salvar nossa pasta de trabalho do Excel como um arquivo PDF. 
```csharp
// Salvar a pasta de trabalho em PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Etapa 8: Confirmar execução
Por fim, é uma boa prática informar ao usuário que o processo foi concluído com sucesso. Você pode fazer isso usando uma mensagem simples de console.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusão
O Aspose.Cells fornece uma maneira flexível e robusta de lidar com manipulações de arquivos do Excel, facilitando para os desenvolvedores criar documentos visualmente atraentes que mantêm sua formatação. Esteja você trabalhando em relatórios, documentos financeiros ou qualquer outra forma de apresentação de dados, ter controle sobre a renderização de fontes pode melhorar significativamente a qualidade da sua saída.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET poderosa que permite aos desenvolvedores manipular arquivos Excel sem precisar instalar o Microsoft Excel. Ela suporta vários formatos de arquivo e oferece recursos avançados para trabalhar com planilhas.
### Como posso definir uma fonte padrão para meus arquivos do Excel?
 Você pode definir uma fonte padrão usando o`PdfSaveOptions` class e especifique o nome da fonte desejada. Isso garante que, mesmo se uma fonte estiver faltando, seu documento usará a fonte padrão que você especificou.
### Posso converter arquivos do Excel para outros formatos além de PDF?
Absolutamente! O Aspose.Cells permite que você converta arquivos do Excel para vários formatos, incluindo imagens (PNG, TIFF), HTML, CSV e muito mais.
### O Aspose.Cells é gratuito?
Aspose.Cells é um produto comercial, mas você pode experimentá-lo gratuitamente com uma versão de teste limitada. Para funcionalidade completa, você precisará comprar uma licença.
### Onde posso encontrar suporte para o Aspose.Cells?
 Você pode encontrar suporte para Aspose.Cells visitando o[Fórum Aspose](https://forum.aspose.com/c/cells/9), onde você pode fazer perguntas e compartilhar ideias com outros usuários e desenvolvedores.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
