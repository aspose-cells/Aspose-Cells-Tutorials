---
"description": "Descubra como adicionar controles de arco com pontos de conexão usando o Aspose.Cells para .NET neste guia detalhado."
"linktitle": "Adicionar controle de arco com pontos de conexão"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar controle de arco com pontos de conexão"
"url": "/pt/net/excel-shapes-controls/add-arc-control-with-connection-points/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar controle de arco com pontos de conexão

## Introdução
Quando se trata de criar relatórios do Excel visualmente envolventes, as ilustrações desempenham um papel vital. Seja para elaborar um relatório financeiro ou um detalhamento de projeto, usar formas como arcos pode adicionar profundidade e clareza à sua apresentação de dados. Hoje, vamos nos aprofundar em como utilizar o Aspose.Cells para .NET para adicionar controles de arco com pontos de conexão em suas planilhas do Excel. Então, se você já se perguntou como incrementar suas planilhas ou dar vida aos seus dados, continue lendo!
## Pré-requisitos
Antes de entrarmos na emoção da programação, vamos garantir que você esteja com tudo pronto. Aqui está o que você precisa:
1. .NET Framework: Certifique-se de ter uma versão compatível instalada. O Aspose.Cells funciona com várias versões, incluindo o .NET Core.
2. Aspose.Cells para .NET: Você precisará baixar e instalar a biblioteca Aspose.Cells. Você pode obtê-la facilmente do [link para download](https://releases.aspose.com/cells/net/).
3. Um bom IDE: o Visual Studio, o fiel companheiro de qualquer desenvolvedor .NET, ajudará a otimizar sua experiência de codificação.
4. Conhecimento básico de C#: se você conhece bem C#, vai achar este tutorial tranquilo.
5. Acesso ao seu diretório de documentos: saiba onde você salvará seus arquivos do Excel. É essencial para organizar seus resultados com eficiência.
## Pacotes de importação
O próximo passo é garantir que você tenha os pacotes corretos importados para o seu projeto. O Aspose.Cells para .NET possui diversas funcionalidades, então vamos simplificar. Veja o que você precisa incluir:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Esses namespaces darão acesso a todos os recursos de desenho e funcionalidades de gerenciamento de células que você usará neste guia.
## Etapa 1: configure seu diretório de documentos
Vamos começar com o mais importante: vamos criar um diretório onde você salvará aqueles arquivos novos do Excel. Veja como fazemos:
```csharp
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este trecho de código verifica se a pasta especificada existe. Caso contrário, ele cria uma. Simples, não é? É sempre bom ter um lugar específico para seus arquivos para evitar bagunça.
## Etapa 2: Instanciar uma pasta de trabalho
Agora que temos nosso diretório pronto, vamos criar uma nova pasta de trabalho do Excel.
```csharp
Workbook excelbook = new Workbook();
```
Ao chamar o `Workbook` construtor, você está basicamente dizendo: "Ei, vamos começar um novo arquivo do Excel!" Esta será a tela para todas as suas formas e dados.
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
Isso torna o arco azul sólido. Você pode mudar a cor para qualquer matiz que desejar, trocando `Color.Blue` para outra cor.
### Definir posicionamento do arco
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Definir o posicionamento como "FreeFloating" permite que o arco se mova independentemente dos limites da célula, dando a você flexibilidade no posicionamento.
### Ajustar espessura e estilo da linha
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aqui, você define o peso e o estilo da linha, tornando-a mais proeminente e visualmente atraente.
## Etapa 5: Adicionando outra forma de arco
Por que parar em apenas um? Vamos adicionar outra forma de arco para enriquecer nosso visual do Excel.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Assim como o primeiro arco, este é adicionado em uma posição diferente — é aqui que a mágica do design acontece!
## Etapa 6: personalize o segundo arco
Vamos dar um pouco de personalidade ao nosso segundo arco também!
### Alterar cor da linha do arco
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Estamos mantendo a consistência na cor azul, mas você sempre pode misturar e combinar para ver o que combina melhor com seu design!
### Definir propriedades semelhantes ao primeiro arco
Certifique-se de replicar essas escolhas estéticas:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aqui, você está apenas garantindo que o segundo arco corresponda ao primeiro, criando uma aparência coesa em toda a planilha.
## Etapa 7: Salve sua pasta de trabalho
Nenhuma obra-prima está completa sem ser salva, certo? Hora de escrever seus arcos em um arquivo do Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Esta linha salva os arcos recém-criados em um arquivo Excel chamado "book1.out.xls" no diretório designado.
## Conclusão
Parabéns! Você acabou de dominar o básico para adicionar controles de arco com pontos de conexão em suas planilhas do Excel usando o Aspose.Cells para .NET. Essa funcionalidade não só embeleza suas planilhas, como também facilita a assimilação de dados complexos. Seja você um desenvolvedor experiente ou iniciante, esses elementos visuais podem transformar seus relatórios de simples em grandiosos.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET que permite aos desenvolvedores criar e manipular arquivos do Excel programaticamente.
### Posso usar o Aspose.Cells gratuitamente?
Sim! Você pode experimentar gratuitamente. Visite [este link](https://releases.aspose.com/) para começar.
### Como adiciono outras formas além de arcos?
Você pode usar diferentes classes disponíveis no namespace Aspose.Cells.Drawing para adicionar várias formas, como retângulos, círculos e muito mais.
### Que tipos de arquivos posso criar com o Aspose.Cells?
Você pode criar e manipular vários formatos do Excel, incluindo XLS, XLSX, CSV e muito mais.
### Há suporte técnico disponível para o Aspose.Cells?
Com certeza! Você pode acessar o [Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9) para assistência.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}