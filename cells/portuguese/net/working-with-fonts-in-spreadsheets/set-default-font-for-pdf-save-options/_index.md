---
"description": "Aprenda a definir fontes padrão para opções de salvamento de PDF usando o Aspose.Cells para .NET, garantindo que seus documentos tenham uma aparência perfeita sempre."
"linktitle": "Definir fonte padrão para opções de salvamento de PDF"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Definir fonte padrão para opções de salvamento de PDF"
"url": "/pt/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Definir fonte padrão para opções de salvamento de PDF

## Introdução
Quando se trata de gerar relatórios, faturas ou qualquer outro documento em formato PDF, garantir que o conteúdo tenha a aparência ideal é fundamental. As fontes desempenham um papel vital na manutenção do apelo visual e da legibilidade dos seus documentos. No entanto, o que acontece quando a fonte usada no arquivo Excel não está disponível no sistema em que você está gerando o PDF? É aí que o Aspose.Cells para .NET entra em cena. Esta poderosa biblioteca permite que você defina fontes padrão para as opções de salvamento de PDF, garantindo que seus documentos tenham uma aparência profissional e consistente, independentemente de onde sejam abertos.
## Pré-requisitos
Antes de começar, certifique-se de ter o seguinte:
1. Visual Studio: você precisará de um ambiente de desenvolvimento como o Visual Studio para escrever e executar seu código.
2. Aspose.Cells para .NET: Você pode baixar a versão mais recente em [este link](https://releases.aspose.com/cells/net/). Como alternativa, você pode instalá-lo por meio do Gerenciador de Pacotes NuGet no Visual Studio.
3. Conhecimento básico de C#: entender os conceitos básicos de C# ajudará você a acompanhar os exemplos de código.
4. Arquivo de exemplo do Excel: Tenha um arquivo de exemplo do Excel pronto para teste. Você pode criar um com várias fontes e estilos para ver como o Aspose.Cells lida com fontes ausentes.
## Pacotes de importação
Antes de usar o Aspose.Cells no seu projeto, você precisa importar os pacotes necessários. Veja como fazer isso:
1. Abra seu projeto: inicie o Visual Studio e abra seu projeto existente ou crie um novo.
2. Adicionar referências: clique com o botão direito do mouse no seu projeto no Solution Explorer e selecione "Gerenciar pacotes NuGet".
3. Instalar Aspose.Cells: Procure por "Aspose.Cells" e clique no botão "Instalar".
4. Adicione diretivas de uso: no início do seu arquivo C#, inclua os seguintes namespaces:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Etapa 1: Configure seus diretórios
Antes de trabalhar com arquivos, é importante definir os diretórios de origem e saída. Isso facilitará a localização do arquivo Excel de entrada e o salvamento dos arquivos de saída gerados.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
Substituir `"Your Document Directory"` com o caminho real para seus diretórios.
## Etapa 2: Abra o arquivo do Excel
Agora que configuramos nossos diretórios, vamos abrir o arquivo Excel com o qual você deseja trabalhar. O `Workbook` A classe em Aspose.Cells é usada para carregar o documento Excel.
```csharp
// Abra um arquivo Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Certifique-se de substituir o nome do arquivo pelo seu nome de arquivo real.
## Etapa 3: Configurar opções de renderização de imagem
Em seguida, precisamos configurar as opções de renderização para converter nossa planilha do Excel para o formato de imagem. Criaremos uma instância de `ImageOrPrintOptions`, especificando o tipo de imagem e a fonte padrão.
```csharp
// Renderização para formato de arquivo PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
Neste trecho de código, definimos o `CheckWorkbookDefaultFont` propriedade para `false`o que significa que se alguma fonte estiver faltando, a fonte padrão especificada (“Times New Roman”) será usada.
## Etapa 4: renderizar a planilha como uma imagem
Agora, vamos renderizar a primeira planilha da pasta de trabalho como uma imagem PNG. Usaremos o `SheetRender` classe para realizar isso.
```csharp
// Renderize a primeira planilha em uma imagem
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Etapa 5: alterar o tipo de imagem e renderizar para TIFF
Se você quiser renderizar a mesma folha em um formato de imagem diferente, como TIFF, você pode simplesmente alterar o `ImageType` propriedade e repita o processo de renderização.
```csharp
// Definir para formato TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Etapa 6: Configurar opções de salvamento de PDF
A seguir, vamos configurar as opções de salvamento do PDF. Criaremos uma instância de `PdfSaveOptions`, defina a fonte padrão e especifique que queremos verificar se há fontes ausentes.
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
## Etapa 8: Confirmar a execução
Por fim, é uma boa prática informar ao usuário que o processo foi concluído com sucesso. Você pode fazer isso usando uma mensagem simples no console.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusão
O Aspose.Cells oferece uma maneira flexível e robusta de lidar com manipulações de arquivos do Excel, facilitando a criação de documentos visualmente atraentes que mantêm a formatação. Seja trabalhando em relatórios, documentos financeiros ou qualquer outra forma de apresentação de dados, ter controle sobre a renderização de fontes pode melhorar significativamente a qualidade da sua saída.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET que permite aos desenvolvedores manipular arquivos do Excel sem a necessidade de instalar o Microsoft Excel. Ela suporta vários formatos de arquivo e oferece recursos avançados para trabalhar com planilhas.
### Como posso definir uma fonte padrão para meus arquivos do Excel?
Você pode definir uma fonte padrão usando o `PdfSaveOptions` class e especifique o nome da fonte desejada. Isso garante que, mesmo que uma fonte esteja faltando, seu documento usará a fonte padrão que você especificou.
### Posso converter arquivos do Excel para outros formatos além de PDF?
Com certeza! O Aspose.Cells permite converter arquivos do Excel para vários formatos, incluindo imagens (PNG, TIFF), HTML, CSV e muito mais.
### O Aspose.Cells é gratuito?
O Aspose.Cells é um produto comercial, mas você pode experimentá-lo gratuitamente com uma versão de teste limitada. Para obter a funcionalidade completa, você precisará adquirir uma licença.
### Onde posso encontrar suporte para o Aspose.Cells?
Você pode encontrar suporte para Aspose.Cells visitando o [Fórum Aspose](https://forum.aspose.com/c/cells/9), onde você pode fazer perguntas e compartilhar ideias com outros usuários e desenvolvedores.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}