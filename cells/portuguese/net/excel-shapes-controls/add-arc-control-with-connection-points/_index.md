---
title: Adicionar controle de arco com pontos de conexão
linktitle: Adicionar controle de arco com pontos de conexão
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra como adicionar controles de arco com pontos de conexão usando o Aspose.Cells para .NET neste guia detalhado.
weight: 27
url: /pt/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar controle de arco com pontos de conexão

## Introdução
Quando se trata de criar relatórios do Excel visualmente envolventes, as ilustrações desempenham um papel vital. Não importa se você está elaborando um relatório financeiro ou uma análise de projeto, usar formas como arcos pode adicionar profundidade e clareza à sua apresentação de dados. Hoje, estamos nos aprofundando em como utilizar o Aspose.Cells para .NET para adicionar controles de arco com pontos de conexão em suas planilhas do Excel. Então, se você já se perguntou como apimentar suas planilhas ou fazer seus dados cantarem, continue lendo!
## Pré-requisitos
Antes de pularmos para a emoção da codificação, vamos garantir que você esteja tudo pronto. Aqui está o que você precisa:
1. .NET Framework: Certifique-se de ter uma versão compatível instalada. O Aspose.Cells funciona com várias versões, incluindo .NET Core.
2.  Aspose.Cells para .NET: Você precisará baixar e instalar a biblioteca Aspose.Cells. Você pode obtê-la facilmente do[link para download](https://releases.aspose.com/cells/net/).
3. Um bom IDE: o Visual Studio, o fiel companheiro de qualquer desenvolvedor .NET, ajudará a otimizar sua experiência de codificação.
4. Conhecimento básico de C#: se você conhece bem C#, vai achar este tutorial tranquilo.
5. Acesso ao seu diretório de documentos: saiba onde você salvará seus arquivos do Excel. É essencial para organizar sua saída de forma eficiente.
## Pacotes de importação
O próximo passo é garantir que você tenha os pacotes certos importados para seu projeto. O Aspose.Cells para .NET tem várias funcionalidades, então vamos manter tudo simples. Aqui está o que você precisa incluir:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Esses namespaces darão acesso a todos os recursos de desenho e funcionalidades de gerenciamento de células que você usará ao longo deste guia.
## Etapa 1: configure seu diretório de documentos
Primeiro as coisas mais importantes — vamos colocar em prática um diretório onde você salvará esses novos arquivos brilhantes do Excel. Veja como fazemos isso:
```csharp
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este pedaço de código verifica se a pasta especificada existe. Se não, ele cria uma. Simples, certo? É sempre bom ter um lugar específico para seus arquivos para evitar desordem.
## Etapa 2: Instanciar uma pasta de trabalho
Agora que temos nosso diretório pronto, vamos criar uma nova pasta de trabalho do Excel.
```csharp
Workbook excelbook = new Workbook();
```
 Ao chamar o`Workbook` construtor, você está basicamente dizendo: “Ei, vamos começar um novo arquivo do Excel!” Esta será a tela para todas as suas formas e dados.
## Etapa 3: Adicionando a primeira forma de arco
É aqui que a diversão começa! Vamos adicionar nossa primeira forma de arco.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Esta linha de código adiciona uma forma de arco à primeira planilha. Os parâmetros especificam as coordenadas do arco e os ângulos que definem sua curvatura. 
## Etapa 4: personalize a aparência do arco
Um arco em branco é como uma tela sem tinta: precisa de um pouco de talento!
### Definir cor de preenchimento do arco
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Isso faz com que o arco fique azul sólido. Você pode mudar a cor para qualquer matiz que desejar, trocando`Color.Blue` para outra cor.
### Definir posicionamento do arco
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Definir o posicionamento como "FreeFloating" permite que o arco se mova independentemente dos limites das células, dando a você flexibilidade no posicionamento.
### Ajustar espessura e estilo da linha
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aqui, você define o peso e o estilo da linha, tornando-a mais proeminente e visualmente atraente.
## Etapa 5: Adicionando outra forma de arco
Por que parar em um? Vamos adicionar outra forma de arco para enriquecer nosso visual do Excel.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Assim como o primeiro arco, este é adicionado em uma posição diferente — é aqui que a mágica do design acontece!
## Etapa 6: Personalize o segundo arco
Vamos dar um pouco de personalidade ao nosso segundo arco também!
### Alterar cor da linha do arco
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Estamos mantendo a consistência com uma cor azul, mas você sempre pode misturar e combinar para ver o que combina melhor com seu design!
### Definir propriedades semelhantes ao primeiro arco
Certifique-se de replicar essas escolhas estéticas:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aqui, você está simplesmente garantindo que o segundo arco corresponda ao primeiro, criando uma aparência coesa em toda a planilha.
## Etapa 7: Salve sua pasta de trabalho
Nenhuma obra-prima está completa sem ser salva, certo? Hora de escrever seus arcos em um arquivo Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Esta linha salva os arcos recém-criados em um arquivo Excel chamado "book1.out.xls" no diretório designado.
## Conclusão
Parabéns! Você acabou de dominar o básico sobre como adicionar controles de arco com pontos de conexão em suas planilhas do Excel usando o Aspose.Cells para .NET. Essa funcionalidade não apenas embeleza suas planilhas, mas também pode tornar dados complexos mais fáceis de digerir. Seja você um desenvolvedor experiente ou apenas iniciante, esses elementos visuais podem transformar seus relatórios de insossos em grandiosos.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET que permite aos desenvolvedores criar e manipular arquivos do Excel programaticamente.
### Posso usar o Aspose.Cells gratuitamente?
 Sim! Você pode experimentar uma avaliação gratuita. Visite[este link](https://releases.aspose.com/) para começar.
### Como adiciono outras formas além de arcos?
Você pode usar diferentes classes disponíveis no namespace Aspose.Cells.Drawing para adicionar várias formas, como retângulos, círculos e muito mais.
### Que tipo de arquivo posso criar com o Aspose.Cells?
Você pode criar e manipular vários formatos do Excel, incluindo XLS, XLSX, CSV e muito mais.
### Há suporte técnico disponível para o Aspose.Cells?
 Claro! Você pode acessar o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9) para obter assistência.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
