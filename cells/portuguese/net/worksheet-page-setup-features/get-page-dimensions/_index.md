---
title: Obter dimensões de página da planilha
linktitle: Obter dimensões de página da planilha
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como obter dimensões de página em uma planilha do Excel com Aspose.Cells para .NET. Um guia passo a passo para personalizar tamanhos de papel A2, A3, A4 e Letter.
weight: 13
url: /pt/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter dimensões de página da planilha

## Introdução
Se você estiver trabalhando com arquivos do Excel programaticamente usando o Aspose.Cells para .NET, pode haver momentos em que você precise acessar e definir as dimensões de página de uma planilha. Saber as dimensões pode ajudar com layouts, impressão e personalização de planilhas do Excel para propósitos específicos. Neste artigo, exploraremos como recuperar e exibir várias dimensões de página no Excel usando o Aspose.Cells para .NET. Passaremos por um tutorial passo a passo para garantir que você tenha todos os detalhes para começar com confiança.
## Pré-requisitos
Antes de começar, vamos garantir que você tenha tudo o que precisa para seguir este tutorial.
1.  Aspose.Cells para .NET: Certifique-se de ter o Aspose.Cells para .NET instalado. Você pode[baixe a biblioteca aqui](https://releases.aspose.com/cells/net/) ou instale-o via NuGet no seu projeto .NET.
2. Ambiente .NET: Um ambiente de desenvolvimento .NET compatível (por exemplo, Visual Studio).
3.  Configuração de licença: Para a funcionalidade completa do Aspose.Cells, aplique uma licença. Você pode[solicite uma licença temporária gratuita](https://purchase.aspose.com/temporary-license/) para fins de avaliação.
Comece com a versão de avaliação gratuita do Aspose.Cells se estiver avaliando-o pela primeira vez.
## Pacotes de importação
Antes de começarmos o código, você precisará importar o namespace Aspose.Cells para seu projeto para acessar todas as classes e métodos necessários.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Vamos dividir o processo em etapas fáceis. Aqui, acessaremos diferentes tamanhos de papel, aplicaremos a uma planilha e imprimiremos as dimensões de cada um.
## Etapa 1: Criar uma instância de pasta de trabalho
 O primeiro passo é criar uma instância do`Workbook` classe. Este objeto atuará como nossa pasta de trabalho principal contendo planilhas que podemos manipular.
```csharp
Workbook book = new Workbook();
```
 Pense em`Workbook` como o contêiner principal para seu arquivo Excel. Precisamos dele para acessar e controlar planilhas individuais.
## Etapa 2: Acesse a primeira planilha
 Em seguida, vamos acessar a primeira planilha na pasta de trabalho. Por padrão, uma nova pasta de trabalho vem com uma planilha, então podemos referenciá-la diretamente usando um índice de`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 O`Worksheets` coleção em`Workbook` nos permite acessar cada planilha por índice. Aqui, pegamos a primeira planilha para começar a definir as dimensões da página.
## Etapa 3: Defina o tamanho do papel como A2 e exiba as dimensões
Agora que temos acesso à nossa planilha, vamos definir o tamanho do papel para A2. Definir o tamanho do papel é útil para formatar a página antes de imprimi-la ou exportá-la. Depois de definir o tamanho do papel, imprimiremos as dimensões da página em polegadas.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Aqui, mudamos o`PaperSize` propriedade para`PaperA2` . Depois de definir o tamanho,`PageSetup.PaperWidth` e`PageSetup.PaperHeight` recuperar a largura e a altura da folha em polegadas. Isso nos dá uma visão geral rápida das dimensões da página.
## Etapa 4: Defina o tamanho do papel como A3 e as dimensões da tela
Seguindo os mesmos passos acima, vamos ajustar as dimensões da página para o tamanho A3. Essa mudança é útil para impressões um pouco maiores ou para encaixar mais conteúdo em uma página.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
O tamanho A3 é o dobro do tamanho do A4, o que o torna uma boa escolha para tabelas grandes ou gráficos detalhados. Alterar o tamanho do papel ajuda a adaptar o layout da planilha de acordo.
## Etapa 5: Defina o tamanho do papel como A4 e as dimensões da tela
Agora, vamos definir o tamanho do papel para A4. Este é o tamanho de página mais comumente usado para imprimir documentos. Exibiremos as dimensões atualizadas depois.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Se o seu alvo for um formato de documento padrão, A4 é normalmente o tamanho mais adequado. Saber as dimensões pode ajudar a ajustar o layout do conteúdo para evitar problemas de impressão.
## Etapa 6: Defina o tamanho do papel como Carta e as dimensões de exibição
Por fim, definiremos o tamanho do papel para o formato Letter, que é comumente usado na América do Norte. Vamos imprimir as dimensões uma última vez.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
O tamanho Carta é amplamente usado para documentos na América do Norte, portanto, definir esse tamanho ajuda na colaboração com equipes ou clientes baseados naquele país.
## Conclusão
Neste tutorial, nós explicamos como definir e recuperar dimensões de página para diferentes tamanhos de papel usando o Aspose.Cells para .NET. Ao configurar tamanhos de página como A2, A3, A4 e Letter, você pode formatar planilhas do Excel para atender a necessidades específicas de impressão e layout. Esse controle sobre as dimensões da página é especialmente valioso para relatórios e apresentações profissionais, pois garante que seu conteúdo se encaixe perfeitamente em cada tamanho de página.
## Perguntas frequentes
### Como posso alterar a orientação da página no Aspose.Cells?  
 Você pode alterar a orientação usando o`PageSetup.Orientation` propriedade, definindo-a para`PageOrientationType.Portrait` ou`PageOrientationType.Landscape`.
### Posso definir dimensões de página personalizadas no Aspose.Cells?  
 Sim, você pode definir dimensões de página personalizadas ajustando as margens e as opções de escala em`PageSetup` para mais controle.
### Qual é o tamanho de papel padrão no Aspose.Cells?  
O tamanho de papel padrão é tipicamente A4. No entanto, isso pode depender de configurações regionais e pode ser ajustado conforme necessário.
### É possível visualizar layouts de página no Aspose.Cells?  
Embora o Aspose.Cells não ofereça uma visualização gráfica, você pode configurar layouts programaticamente e usar visualizações de impressão no Excel.
### Como instalo o Aspose.Cells para .NET?  
 Você pode instalar o Aspose.Cells usando o Gerenciador de Pacotes NuGet no Visual Studio ou baixar a DLL do[Página de download do Aspose.Cells](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
