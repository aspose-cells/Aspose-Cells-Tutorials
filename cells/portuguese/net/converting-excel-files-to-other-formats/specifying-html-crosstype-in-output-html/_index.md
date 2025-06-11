---
"description": "Aprenda a especificar HTML CrossType no Aspose.Cells para .NET. Siga nosso tutorial passo a passo para converter arquivos do Excel para HTML com precisão."
"linktitle": "Especificando HTML CrossType na saída HTML programaticamente no .NET"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Especificando HTML CrossType na saída HTML programaticamente no .NET"
"url": "/pt/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Especificando HTML CrossType na saída HTML programaticamente no .NET

## Introdução
Ao converter arquivos do Excel para HTML em aplicativos .NET, você pode precisar especificar como as referências cruzadas são tratadas na saída. A classe HtmlSaveOptions no Aspose.Cells para .NET fornece várias configurações para controlar o processo de conversão, e uma dessas opções é o HtmlCrossType. Neste tutorial, mostraremos como especificar programaticamente o tipo cruzado HTML ao exportar arquivos do Excel para o formato HTML. 
## Pré-requisitos
Antes de mergulhar no código, certifique-se de ter o seguinte:
- Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada em seu projeto. Você pode baixá-la do site [Site Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: uma instalação funcional do Visual Studio ou qualquer outro ambiente de desenvolvimento .NET.
- Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os exemplos.
- Arquivo Excel de exemplo: Tenha um arquivo Excel de exemplo pronto para trabalhar. Para este exemplo, usaremos `sampleHtmlCrossStringType.xlsx`.
## Pacotes de importação
Para começar, você precisará importar os namespaces Aspose.Cells necessários. Veja como fazer isso:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Vamos detalhar isso passo a passo, para que fique mais fácil para você acompanhar e implementar essa funcionalidade em seus próprios projetos.
## Etapa 1: Defina seus diretórios de origem e saída
Primeiro, você precisa definir os diretórios para o seu arquivo Excel de origem e onde deseja salvar o arquivo HTML de saída.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
## Etapa 2: Carregue o arquivo Excel de exemplo
Em seguida, carregue seu arquivo Excel de amostra em um `Workbook` objeto. É aqui que toda a magia começa.
```csharp
// Carregue o arquivo Excel de exemplo
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Aqui, substitua `"Your Document Directory"` com o caminho real onde o arquivo do Excel está localizado. Esta linha lê o arquivo do Excel na memória para que você possa manipulá-lo.
## Etapa 3: especifique as opções de salvamento de HTML
Agora, criaremos uma instância de `HtmlSaveOptions`, que permite configurar como o arquivo Excel será convertido em HTML.
```csharp
// Especificar tipo de cruzamento HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
Nesta etapa, definimos o `HtmlCrossStringType` para `HtmlCrossType.Default`, que é uma das opções disponíveis para lidar com referências cruzadas no HTML de saída.
## Etapa 4: Altere o tipo de cruz conforme necessário
Você pode especificar diferentes tipos para `HtmlCrossStringType` com base nas suas necessidades. Aqui estão as várias opções que você pode usar:
- `HtmlCrossType.Default`: O tipo de cruz padrão.
- `HtmlCrossType.MSExport`: Exporta o HTML com comportamento semelhante ao MS Excel.
- `HtmlCrossType.Cross`: Cria referências cruzadas.
- `HtmlCrossType.FitToCell`Ajusta as referências cruzadas às dimensões da célula.
Você pode modificar o `HtmlCrossStringType` assim:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpout;
// ou 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Etapa 5: Salve o arquivo HTML de saída
Depois de configurar suas opções, é hora de salvar o arquivo HTML convertido. Use o `Save` método em seu `Workbook` objeto:
```csharp
// Saída HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Aqui, estamos nomeando o arquivo de saída com base no `HtmlCrossStringType` definimos. Dessa forma, você pode identificar facilmente qual tipo de cruz foi usado na conversão.
## Etapa 6: Confirmar a execução bem-sucedida
Por fim, é sempre uma boa prática confirmar se sua operação foi bem-sucedida. Você pode imprimir uma mensagem no console:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Isso permitirá que você saiba que o processo foi concluído sem erros.
## Conclusão
pronto! Você especificou com sucesso o tipo cruzado HTML para sua exportação do Excel em .NET usando Aspose.Cells. Essa funcionalidade é particularmente útil quando você precisa manter formatações ou referências específicas na sua saída HTML, garantindo que os documentos convertidos atendam aos seus requisitos.
## Perguntas frequentes
### O que é HtmlCrossType em Aspose.Cells?  
HtmlCrossType define como as referências cruzadas no arquivo Excel são tratadas durante a conversão para HTML. Você pode escolher opções como Padrão, MSExport, Cruzado e Ajustar à Célula.
### Posso usar o Aspose.Cells gratuitamente?  
O Aspose.Cells oferece uma versão de teste gratuita. Você pode baixá-la em [site](https://releases.aspose.com/).
### Como instalo o Aspose.Cells no meu projeto .NET?  
Você pode instalar o Aspose.Cells por meio do Gerenciador de Pacotes NuGet no Visual Studio executando o comando: `Install-Package Aspose.Cells`.
### Onde posso encontrar a documentação do Aspose.Cells?  
Você pode encontrar documentação completa em Aspose.Cells [aqui](https://reference.aspose.com/cells/net/).
### que devo fazer se encontrar um erro ao salvar o arquivo HTML?  
Certifique-se de que os caminhos dos diretórios estejam corretos e que você tenha permissões de gravação para o diretório de saída. Se o problema persistir, consulte o fórum de suporte do Aspose para obter ajuda.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}