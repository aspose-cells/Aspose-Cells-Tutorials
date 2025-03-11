---
title: Definir hora de criação de PDF no .NET
linktitle: Definir hora de criação de PDF no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como definir o tempo de criação de PDF no .NET usando Aspose.Cells. Siga nosso guia passo a passo para conversão perfeita de Excel para PDF.
weight: 11
url: /pt/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir hora de criação de PDF no .NET

## Introdução
Na era digital de hoje, a capacidade de converter documentos em diferentes formatos é crucial para muitas aplicações. Uma necessidade comum é converter planilhas do Excel em arquivos PDF. Isso não só preserva a formatação, mas também torna o compartilhamento e a impressão muito mais fáceis. Se você é um desenvolvedor trabalhando com .NET, Aspose.Cells é uma biblioteca fantástica que simplifica esse processo. Neste tutorial, vamos nos aprofundar em como definir o tempo de criação do PDF ao converter um arquivo Excel para PDF usando Aspose.Cells para .NET.
## Pré-requisitos
Antes de entrarmos nos detalhes do código, vamos garantir que você tenha tudo o que precisa para começar.
### O que você precisa
1. Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. Este será seu ambiente de desenvolvimento.
2.  Aspose.Cells para .NET: Baixe a biblioteca Aspose.Cells do[site](https://releases.aspose.com/cells/net/). Você também pode começar com um teste gratuito para testar suas funcionalidades.
3. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
4.  Arquivo Excel: Tenha um arquivo Excel pronto para conversão. Para este exemplo, usaremos um arquivo chamado`Book1.xlsx`.
Agora que você tem os pré-requisitos resolvidos, vamos para a parte divertida: importar os pacotes necessários e escrever o código!
## Pacotes de importação
Para começar, você precisa importar os namespaces necessários no seu arquivo C#. Isso é crucial, pois permite que você acesse as classes e métodos fornecidos pela biblioteca Aspose.Cells.
### Abra seu projeto C#
Abra o Visual Studio e crie um novo projeto ou abra um existente onde você deseja implementar o recurso de conversão de PDF.
### Adicionar referência Aspose.Cells
Você pode adicionar a biblioteca Aspose.Cells ao seu projeto clicando com o botão direito do mouse no seu projeto no Solution Explorer, selecionando “Manage NuGet Packages” e pesquisando por “Aspose.Cells”. Instale o pacote.
### Importar namespaces
No topo do seu arquivo C#, inclua os seguintes namespaces:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Esses namespaces darão acesso à classe Workbook e outras funcionalidades essenciais.

Agora que importamos nossos pacotes, vamos detalhar o processo de conversão de um arquivo Excel em PDF e, ao mesmo tempo, definir o horário de criação.
## Etapa 1: Defina o diretório do documento
Primeiro, você precisa especificar o diretório onde seus documentos estão armazenados. É aqui que seu arquivo Excel está localizado e onde o PDF de saída será salvo.
```csharp
string dataDir = "Your Document Directory"; // Especifique seu diretório de documentos
```
 Substituir`"Your Document Directory"` com o caminho real onde seu`Book1.xlsx` arquivo está localizado. Este caminho ajudará o aplicativo a localizar o arquivo para processamento.
## Etapa 2: Carregue o arquivo Excel
 Em seguida, você carregará o arquivo Excel em um`Workbook` objeto. É aqui que o Aspose.Cells brilha, pois permite que você trabalhe com arquivos do Excel sem esforço.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Caminho para o seu arquivo Excel
Workbook workbook = new Workbook(inputPath); // Carregue o arquivo Excel
```
 O`Workbook` class é usada para carregar e manipular arquivos do Excel. Ao passar o caminho de entrada, você está dizendo ao aplicativo com qual arquivo trabalhar.
## Etapa 3: Criar PdfSaveOptions
 Agora, é hora de criar uma instância de`PdfSaveOptions`. Esta classe permite que você especifique várias opções para salvar sua pasta de trabalho como PDF, incluindo o horário de criação.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Criar instância PdfSaveOptions
options.CreatedTime = DateTime.Now; // Defina a hora de criação para agora
```
 Ao definir`options.CreatedTime` para`DateTime.Now`, você garante que o PDF refletirá a data e a hora atuais em que foi criado.
## Etapa 4: Salve a pasta de trabalho como PDF
Por fim, você salvará a pasta de trabalho como um arquivo PDF usando as opções que acabou de definir.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Salvar como PDF
```
 Esta linha de código pega a pasta de trabalho e a salva em formato PDF no local especificado. O`options` O parâmetro é passado para incluir o horário de criação nos metadados do PDF.

## Conclusão
E aí está! Você converteu com sucesso um arquivo Excel para um PDF usando o Aspose.Cells para .NET, completo com um carimbo de data/hora de criação. Esse recurso pode ser incrivelmente útil quando você precisa manter o controle das versões do documento ou quando deseja fornecer aos destinatários informações sobre quando o documento foi criado.
 Se você deseja explorar mais recursos do Aspose.Cells, não hesite em conferir o[documentação](https://reference.aspose.com/cells/net/).
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel.
### Posso usar o Aspose.Cells gratuitamente?
 Sim, você pode começar com um teste gratuito disponível no[Site Aspose](https://releases.aspose.com/).
### Como defino outras propriedades do PDF?
 Você pode definir várias propriedades de PDF usando o`PdfSaveOptions` classe, como tamanho de página, compactação e muito mais.
### É possível converter vários arquivos do Excel de uma só vez?
Sim, você pode percorrer uma lista de arquivos e aplicar o mesmo processo de conversão a cada um.
### Onde posso obter suporte para o Aspose.Cells?
 Você pode obter suporte da comunidade Aspose em seu[fórum de suporte](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
