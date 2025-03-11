---
title: Obter lista de fontes usadas na planilha
linktitle: Obter lista de fontes usadas na planilha
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como buscar e listar fontes de planilhas do Excel usando o Aspose.Cells para .NET com este tutorial fácil de seguir.
weight: 10
url: /pt/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter lista de fontes usadas na planilha

## Introdução
Já se viu rolando por uma planilha do Excel, pensando sobre as fontes usadas em suas várias células? Talvez você tenha encontrado um documento antigo e adoraria saber quais escolhas de tipografia foram feitas? Bem, você está com sorte! Com o Aspose.Cells para .NET, é como ter uma caixa de ferramentas que permite que você peneire e descubra aqueles segredos de fontes escondidos em suas planilhas. Neste guia, mostraremos como recuperar facilmente uma lista de todas as fontes usadas em um arquivo do Excel. Aperte o cinto e vamos mergulhar no mundo das planilhas!
## Pré-requisitos
Antes de pularmos para o código, há algumas coisas que você precisa para começar. Não se preocupe, é bem simples. Aqui está uma lista de verificação do que você precisa:
1. Visual Studio: Certifique-se de ter uma versão do Visual Studio instalada em sua máquina. É aqui que escreveremos nosso código.
2. Aspose.Cells para .NET: Você precisa ter a biblioteca Aspose.Cells disponível. Se você ainda não baixou, você pode obtê-la do[site](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: Um pouco de compreensão de programação em C# certamente ajudará você a navegar pelo código facilmente.
4. Um arquivo Excel de exemplo: Você precisará de um arquivo Excel de exemplo, como "sampleGetFonts.xlsx," para trabalhar. É aqui que aplicaremos nossa exploração de fontes.
Depois de ter tudo organizado, você estará pronto para começar a codificar!
## Pacotes de importação
Para começar, vamos importar os namespaces necessários. No .NET, importar pacotes é como convidar os convidados certos para sua festa — sem eles, as coisas simplesmente não funcionam bem.
Veja como importar Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Com essa linha simples, estamos convidando a funcionalidade principal do Aspose.Cells para o nosso projeto. Agora, vamos prosseguir para carregar a pasta de trabalho.
## Etapa 1: Defina o diretório de documentos
Primeiro as coisas mais importantes — antes de mergulharmos no código, você precisa definir o caminho para o diretório do seu documento. É aqui que seu arquivo Excel fica. 
```csharp
string dataDir = "Your Document Directory";
```
Você substituirá “Your Document Directory” pelo caminho real onde seu arquivo Excel está localizado. Pense nisso como dizer ao programa, “Ei, aqui é onde eu escondi meu arquivo Excel; vá dar uma olhada!”
## Etapa 2: Carregue a pasta de trabalho de origem
 É hora de carregar o arquivo Excel. Criaremos uma nova instância do`Workbook` classe e passe o caminho do arquivo. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 O que está acontecendo aqui? Estamos basicamente abrindo a porta para nossa planilha. O`Workbook` A classe nos permite interagir com o conteúdo do arquivo Excel. 
## Etapa 3: Obtenha todas as fontes
 Agora vem o momento mágico — vamos realmente recuperar as fontes! O`GetFonts()` O método é o nosso bilhete dourado.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Aqui, estamos pedindo à pasta de trabalho para revelar todas as fontes usadas nela.`fnts` a matriz guardará nossos tesouros.
## Etapa 4: Imprima as fontes
Por fim, vamos pegar essas fontes e imprimi-las. Isso nos ajudará a verificar o que encontramos.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Este loop percorre cada fonte em nosso`fnts` array, enviando-os para o console um por um. É como exibir todas as escolhas legais de tipografia que você tem no seu arquivo Excel!
## Conclusão
E aí está! Com apenas algumas linhas de código, você recuperou e imprimiu com sucesso a lista de fontes usadas em sua planilha do Excel usando o Aspose.Cells para .NET. Não se trata apenas de fontes; trata-se de entender as sutilezas de seus documentos, aprimorar suas apresentações e dominar a arte da tipografia em suas planilhas. Seja você um desenvolvedor ou alguém que simplesmente adora mexer no Excel, este pequeno trecho pode mudar o jogo. 
## Perguntas frequentes
### Preciso instalar o Aspose.Cells separadamente?
Sim, você precisa baixar e referenciar a biblioteca em seu projeto. 
### Posso usar o Aspose.Cells para outros formatos?
Absolutamente! Aspose.Cells funciona com vários formatos do Excel, como XLSX, XLS e CSV.
### Existe um teste gratuito disponível?
 Sim, você pode obter uma avaliação gratuita do[link para download](https://releases.aspose.com/).
### Como posso obter suporte técnico?
 Se precisar de ajuda, o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9) é um ótimo recurso.
### O Aspose.Cells é compatível com o .NET Core?
Sim, o Aspose.Cells também é compatível com projetos .NET Core.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
