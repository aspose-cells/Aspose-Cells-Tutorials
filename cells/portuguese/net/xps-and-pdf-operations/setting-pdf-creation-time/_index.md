---
"description": "Aprenda a definir o horário de criação de um PDF no .NET usando o Aspose.Cells. Siga nosso guia passo a passo para uma conversão perfeita de Excel para PDF."
"linktitle": "Definindo o tempo de criação do PDF no .NET"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Definindo o tempo de criação do PDF no .NET"
"url": "/pt/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Definindo o tempo de criação do PDF no .NET

## Introdução
Na era digital atual, a capacidade de converter documentos em diferentes formatos é crucial para muitas aplicações. Uma necessidade comum é converter planilhas do Excel em arquivos PDF. Isso não apenas preserva a formatação, como também facilita muito o compartilhamento e a impressão. Se você é um desenvolvedor que trabalha com .NET, o Aspose.Cells é uma biblioteca fantástica que simplifica esse processo. Neste tutorial, veremos como definir o horário de criação do PDF ao converter um arquivo do Excel para PDF usando o Aspose.Cells para .NET.
## Pré-requisitos
Antes de começarmos com os detalhes do código, vamos garantir que você tenha tudo o que precisa para começar.
### O que você precisa
1. Visual Studio: Certifique-se de ter o Visual Studio instalado na sua máquina. Este será o seu ambiente de desenvolvimento.
2. Aspose.Cells para .NET: Baixe a biblioteca Aspose.Cells do [site](https://releases.aspose.com/cells/net/). Você também pode começar com um teste gratuito para testar suas funcionalidades.
3. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
4. Arquivo Excel: Tenha um arquivo Excel pronto para conversão. Para este exemplo, usaremos um arquivo chamado `Book1.xlsx`.
Agora que você já tem os pré-requisitos resolvidos, vamos para a parte divertida: importar os pacotes necessários e escrever o código!
## Pacotes de importação
Para começar, você precisa importar os namespaces necessários para o seu arquivo C#. Isso é crucial, pois permite acessar as classes e métodos fornecidos pela biblioteca Aspose.Cells.
### Abra seu projeto C#
Abra o Visual Studio e crie um novo projeto ou abra um existente onde você deseja implementar o recurso de conversão de PDF.
### Adicionar referência Aspose.Cells
Você pode adicionar a biblioteca Aspose.Cells ao seu projeto clicando com o botão direito do mouse no projeto no Solution Explorer, selecionando “Gerenciar pacotes NuGet” e pesquisando por “Aspose.Cells”. Instale o pacote.
### Importar namespaces
No início do seu arquivo C#, inclua os seguintes namespaces:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Esses namespaces darão acesso à classe Workbook e outras funcionalidades essenciais.

Agora que nossos pacotes foram importados, vamos detalhar o processo de conversão de um arquivo Excel em PDF e, ao mesmo tempo, definir o horário de criação.
## Etapa 1: definir o diretório de documentos
Primeiro, você precisa especificar o diretório onde seus documentos estão armazenados. É lá que seu arquivo Excel está localizado e onde o PDF de saída será salvo.
```csharp
string dataDir = "Your Document Directory"; // Especifique seu diretório de documentos
```
Substituir `"Your Document Directory"` com o caminho real onde seu `Book1.xlsx` o arquivo está localizado. Este caminho ajudará o aplicativo a localizar o arquivo para processamento.
## Etapa 2: Carregar o arquivo Excel
Em seguida, você carregará o arquivo Excel em um `Workbook` objeto. É aqui que o Aspose.Cells se destaca, pois permite que você trabalhe com arquivos do Excel sem esforço.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Caminho para o seu arquivo Excel
Workbook workbook = new Workbook(inputPath); // Carregar o arquivo Excel
```
O `Workbook` classe é usada para carregar e manipular arquivos do Excel. Ao passar o caminho de entrada, você informa ao aplicativo com qual arquivo trabalhar.
## Etapa 3: Criar PdfSaveOptions
Agora, é hora de criar uma instância de `PdfSaveOptions`. Esta classe permite que você especifique várias opções para salvar sua pasta de trabalho como PDF, incluindo o horário de criação.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Criar instância PdfSaveOptions
options.CreatedTime = DateTime.Now; // Defina a hora da criação para agora
```
Ao definir `options.CreatedTime` para `DateTime.Now`, você garante que o PDF refletirá a data e a hora atuais em que foi criado.
## Etapa 4: Salve a pasta de trabalho como PDF
Por fim, você salvará a pasta de trabalho como um arquivo PDF usando as opções que acabou de definir.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Salvar como PDF
```
Esta linha de código pega a pasta de trabalho e a salva em formato PDF no local especificado. `options` O parâmetro é passado para incluir o horário de criação nos metadados do PDF.

## Conclusão
pronto! Você converteu com sucesso um arquivo do Excel para PDF usando o Aspose.Cells para .NET, com carimbo de data/hora de criação. Esse recurso pode ser extremamente útil quando você precisa controlar as versões do documento ou quando deseja fornecer aos destinatários informações sobre quando o documento foi criado.
Se você deseja explorar mais recursos do Aspose.Cells, não hesite em conferir o [documentação](https://reference.aspose.com/cells/net/).
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel.
### Posso usar o Aspose.Cells gratuitamente?
Sim, você pode começar com um teste gratuito disponível no [Site Aspose](https://releases.aspose.com/).
### Como defino outras propriedades do PDF?
Você pode definir várias propriedades do PDF usando o `PdfSaveOptions` classe, como tamanho de página, compactação e muito mais.
### É possível converter vários arquivos do Excel de uma só vez?
Sim, você pode percorrer uma lista de arquivos e aplicar o mesmo processo de conversão a cada um.
### Onde posso obter suporte para o Aspose.Cells?
Você pode obter suporte da comunidade Aspose em seu [fórum de suporte](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}