---
title: Ler o tempo de criação dos comentários encadeados na planilha
linktitle: Ler o tempo de criação dos comentários encadeados na planilha
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a ler o tempo de criação de comentários encadeados no Excel usando Aspose.Cells para .NET. Guia passo a passo com exemplos de código incluídos.
weight: 21
url: /pt/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ler o tempo de criação dos comentários encadeados na planilha

## Introdução
Ao trabalhar com arquivos do Excel, gerenciar comentários pode ser um aspecto crucial da colaboração e feedback de dados. Se você estiver usando o Aspose.Cells para .NET, você o achará incrivelmente poderoso para lidar com várias funcionalidades do Excel, incluindo comentários encadeados. Neste tutorial, vamos nos concentrar em como ler o tempo de criação de comentários encadeados em uma planilha. Seja você um desenvolvedor experiente ou apenas iniciante, este guia o guiará pelo processo passo a passo.
## Pré-requisitos
Antes de mergulharmos no código, vamos garantir que você tenha tudo o que precisa para começar:
1. Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada. Você pode baixá-la do[Site Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: uma instalação funcional do Visual Studio ou qualquer outro IDE .NET onde você pode escrever e executar seu código C#.
3. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
4.  Arquivo Excel: Tenha um arquivo Excel pronto com alguns comentários encadeados. Para este exemplo, usaremos um arquivo chamado`ThreadedCommentsSample.xlsx`.
Agora que cobrimos nossos pré-requisitos, vamos importar os pacotes necessários.
## Pacotes de importação
Para começar a usar o Aspose.Cells, você precisa importar os namespaces necessários. Veja como fazer isso:
### Importe o namespace Aspose.Cells
Abra seu projeto C# no Visual Studio e adicione a seguinte diretiva using no topo do seu arquivo de código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Este namespace permite que você acesse todas as classes e métodos fornecidos pela biblioteca Aspose.Cells.
Agora que definimos o cenário, vamos dividir o processo de leitura do tempo de criação dos comentários encadeados em etapas gerenciáveis.
## Etapa 1: Defina o diretório de origem
Primeiro, você precisa especificar o diretório onde seu arquivo Excel está localizado. Isso é crucial porque o programa precisa saber onde procurar o arquivo.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"`com o caminho real para o seu arquivo Excel. Isso pode ser algo como`"C:\\Documents\\"`.
## Etapa 2: Carregue a pasta de trabalho
Em seguida, você carregará a pasta de trabalho do Excel que contém os comentários encadeados. Veja como fazer isso:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
 Esta linha de código cria um novo`Workbook` objeto carregando o arquivo Excel especificado. Se o arquivo não for encontrado, uma exceção será lançada, então garanta que o caminho esteja correto.
## Etapa 3: Acesse a planilha
Depois que a pasta de trabalho for carregada, o próximo passo é acessar a planilha específica que contém os comentários. No nosso caso, acessaremos a primeira planilha:
```csharp
// Acesse a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```
Esta linha recupera a primeira planilha (índice 0) da pasta de trabalho. Se seus comentários estiverem localizados em uma planilha diferente, ajuste o índice de acordo.
## Etapa 4: Obtenha comentários encadeados
Agora, é hora de recuperar os comentários encadeados de uma célula específica. Neste exemplo, obteremos comentários da célula A1:
```csharp
// Obter comentários encadeados
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
Esta linha busca todos os comentários encadeados associados à célula A1. Se não houver comentários, a coleção estará vazia.
## Etapa 5: iterar pelos comentários
Com os comentários encadeados recuperados, agora podemos percorrê-los e exibir os detalhes, incluindo o horário de criação:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
 Este loop percorre cada comentário no`threadedComments` coleção e imprime o texto do comentário, o nome do autor e a hora em que o comentário foi criado.
## Etapa 6: Mensagem de confirmação
Por fim, após executar a lógica de leitura de comentários, é sempre uma boa ideia fornecer uma mensagem de confirmação. Isso ajuda na depuração e garante que o código foi executado com sucesso:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Conclusão
Parabéns! Você aprendeu com sucesso como ler o tempo de criação de comentários encadeados em uma planilha do Excel usando o Aspose.Cells para .NET. Essa funcionalidade pode ser incrivelmente útil para rastrear feedback e colaboração em seus documentos do Excel. Com apenas algumas linhas de código, você pode extrair informações valiosas que podem aprimorar seus processos de análise de dados e relatórios.
## Perguntas frequentes
### O que é Aspose.Cells para .NET?
Aspose.Cells para .NET é uma biblioteca poderosa que permite aos desenvolvedores criar, manipular e converter arquivos do Excel em aplicativos .NET.
### Como posso baixar o Aspose.Cells para .NET?
 Você pode baixá-lo do[Site Aspose](https://releases.aspose.com/cells/net/).
### Existe um teste gratuito disponível?
 Sim, você pode experimentar o Aspose.Cells gratuitamente visitando o[página de teste grátis](https://releases.aspose.com/).
### Posso acessar comentários de outras células?
Absolutamente! Você pode modificar a referência da célula no`GetThreadedComments` método para acessar comentários de qualquer célula.
### Onde posso obter suporte para o Aspose.Cells?
 Para obter suporte, você pode visitar o[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
