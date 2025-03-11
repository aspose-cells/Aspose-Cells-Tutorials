---
title: Especificando HTML CrossType na saída HTML programaticamente no .NET
linktitle: Especificando HTML CrossType na saída HTML programaticamente no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como especificar HTML CrossType em Aspose.Cells para .NET. Siga nosso tutorial passo a passo para converter arquivos Excel para HTML com precisão.
weight: 17
url: /pt/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificando HTML CrossType na saída HTML programaticamente no .NET

## Introdução
Quando se trata de converter arquivos do Excel para HTML em aplicativos .NET, você pode precisar especificar como as referências cruzadas são manipuladas na saída. A classe HtmlSaveOptions no Aspose.Cells para .NET fornece várias configurações para controlar o processo de conversão, e uma dessas opções é o HtmlCrossType. Neste tutorial, mostraremos como especificar programaticamente o tipo cruzado HTML ao exportar arquivos do Excel para o formato HTML. 
## Pré-requisitos
Antes de mergulhar no código, certifique-se de ter o seguinte:
-  Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada em seu projeto. Você pode baixá-la do[Site Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: uma instalação funcional do Visual Studio ou qualquer outro ambiente de desenvolvimento .NET.
- Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os exemplos.
-  Arquivo Excel de exemplo: Tenha um arquivo Excel de exemplo pronto para trabalhar. Para este exemplo, usaremos`sampleHtmlCrossStringType.xlsx`.
## Pacotes de importação
Para começar, você precisará importar os namespaces Aspose.Cells necessários. Veja como você pode fazer isso:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Vamos detalhar isso passo a passo, para que seja mais fácil para você acompanhar e implementar essa funcionalidade em seus próprios projetos.
## Etapa 1: Defina seus diretórios de origem e saída
Primeiro, você precisa definir os diretórios para seu arquivo Excel de origem e onde deseja salvar o arquivo HTML de saída.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
## Etapa 2: Carregue o arquivo Excel de amostra
 Em seguida, carregue seu arquivo Excel de amostra em um`Workbook` objeto. É aqui que toda a mágica começa.
```csharp
// Carregue o arquivo Excel de exemplo
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Aqui, substitua`"Your Document Directory"` com o caminho real onde seu arquivo Excel está localizado. Esta linha lê o arquivo Excel na memória para que você possa manipulá-lo.
## Etapa 3: especifique as opções de salvamento de HTML
 Agora, criaremos uma instância de`HtmlSaveOptions`, que permite configurar como o arquivo Excel será convertido em HTML.
```csharp
// Especificar tipo de cruz HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 Nesta etapa, definimos o`HtmlCrossStringType` para`HtmlCrossType.Default`, que é uma das opções disponíveis para lidar com referências cruzadas no HTML de saída.
## Etapa 4: Altere o tipo de cruz conforme necessário
 Você pode especificar diferentes tipos para`HtmlCrossStringType` com base em seus requisitos. Aqui estão as várias opções que você pode usar:
- `HtmlCrossType.Default`: O tipo de cruz padrão.
- `HtmlCrossType.MSExport`: Exporta o HTML com comportamento semelhante ao do MS Excel.
- `HtmlCrossType.Cross`: Cria referências cruzadas.
- `HtmlCrossType.FitToCell`: Ajusta as referências cruzadas às dimensões da célula.
 Você pode modificar o`HtmlCrossStringType` assim:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// ou
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// ou
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Etapa 5: Salve o arquivo HTML de saída
 Depois de configurar suas opções, é hora de salvar o arquivo HTML convertido. Use o`Save` método em seu`Workbook` objeto:
```csharp
// Saída Html
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Aqui, estamos nomeando o arquivo de saída com base no`HtmlCrossStringType` nós definimos. Dessa forma, você pode identificar facilmente qual tipo de cruz foi usado na conversão.
## Etapa 6: Confirme a execução bem-sucedida
Por fim, é sempre uma boa prática confirmar que sua operação foi bem-sucedida. Você pode imprimir uma mensagem no console:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Isso permitirá que você saiba que o processo foi concluído sem erros.
## Conclusão
aí está! Você especificou com sucesso o cross-type HTML para sua exportação do Excel em .NET usando Aspose.Cells. Essa funcionalidade é particularmente útil quando você precisa manter formatação ou referências específicas em sua saída HTML, garantindo que seus documentos convertidos atendam aos seus requisitos.
## Perguntas frequentes
### O que é HtmlCrossType em Aspose.Cells?  
HtmlCrossType define como referências cruzadas no arquivo Excel são manipuladas durante a conversão HTML. Você pode escolher opções como Default, MSExport, Cross e FitToCell.
### Posso usar o Aspose.Cells gratuitamente?  
 Aspose.Cells oferece uma versão de teste gratuita. Você pode baixá-la em seu[site](https://releases.aspose.com/).
### Como instalo o Aspose.Cells no meu projeto .NET?  
 Você pode instalar o Aspose.Cells por meio do Gerenciador de Pacotes NuGet no Visual Studio executando o comando:`Install-Package Aspose.Cells`.
### Onde posso encontrar a documentação do Aspose.Cells?  
 Você pode encontrar documentação abrangente em Aspose.Cells[aqui](https://reference.aspose.com/cells/net/).
### O que devo fazer se encontrar um erro ao salvar o arquivo HTML?  
Certifique-se de que os caminhos do diretório estejam corretos e que você tenha permissões de gravação para o diretório de saída. Se o problema persistir, verifique o fórum de suporte do Aspose para obter ajuda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
