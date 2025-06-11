---
"description": "Aprenda a adicionar arcos a planilhas do Excel usando o Aspose.Cells para .NET. Siga nosso guia passo a passo para aprimorar o design das suas planilhas."
"linktitle": "Adicionar arco à planilha no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar arco à planilha no Excel"
"url": "/pt/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar arco à planilha no Excel

## Introdução
Criar planilhas do Excel visualmente atraentes é crucial para a apresentação de dados, e a biblioteca Aspose.Cells oferece aos desenvolvedores ferramentas robustas para realizar essa tarefa. Um recurso interessante que você pode querer incorporar aos seus documentos do Excel é a capacidade de adicionar formas, como arcos. Neste tutorial, mostraremos passo a passo como adicionar arcos a uma planilha do Excel usando o Aspose.Cells para .NET. Ao final deste artigo, você não apenas aprenderá como adicionar arcos, mas também obterá insights sobre o gerenciamento de formas em geral.
## Pré-requisitos
Antes de nos aprofundarmos nas complexidades da adição de arcos à sua planilha, é essencial garantir que você tenha alguns itens em mãos. Aqui estão os pré-requisitos necessários para começar:
1. Visual Studio: Você precisará ter o Visual Studio instalado no seu computador, pois usaremos C# como linguagem de programação.
2. .NET Framework: Certifique-se de ter o .NET Framework ou o .NET Core instalado. O Aspose.Cells suporta ambos.
3. Aspose.Cells para .NET: Você precisa ter a biblioteca Aspose.Cells. Você pode baixá-la do site [Downloads do Aspose.Cells](https://releases.aspose.com/cells/net/) página.
4. Noções básicas de C#: a familiaridade com C# ajudará você a acompanhar os trechos de código sem muita complicação.
## Pacotes de importação
Para começar a trabalhar com Aspose.Cells no seu projeto, você precisa importar os pacotes necessários. Veja como fazer:
### Criar um novo projeto
- Abra o Visual Studio.
- Selecione "Criar um novo projeto".
- Selecione um modelo que funcione com .NET (como Console Application).
  
### Adicionar referências Aspose.Cells
- Clique com o botão direito do mouse no seu projeto no Solution Explorer.
- Selecione "Gerenciar pacotes NuGet".
- Procure por “Aspose.Cells” e instale-o.
Agora você está pronto para começar a codificar a adição do arco.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Aqui está uma análise passo a passo do código que demonstra como adicionar arcos a uma planilha no Excel.
## Etapa 1: Configurando o diretório
primeiro passo é criar um diretório onde você salvará seu arquivo Excel. Isso facilita o gerenciamento dos arquivos de saída.
```csharp
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Neste trecho de código, especificamos o caminho para o diretório do documento. Também verificamos se o diretório existe; caso contrário, o criamos. Isso estabelece a base para nossa saída.
## Etapa 2: Instanciar uma pasta de trabalho
Em seguida, vamos criar uma nova instância de pasta de trabalho.
```csharp
// Instanciar uma nova pasta de trabalho.
Workbook excelbook = new Workbook();
```
Esta linha cria uma nova pasta de trabalho do Excel. Pense nela como uma tela em branco onde podemos adicionar formas, dados e muito mais.
## Etapa 3: adicione a primeira forma de arco
Agora, vamos adicionar nossa primeira forma de arco à planilha.
```csharp
// Adicione uma forma de arco.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Aqui, estamos adicionando um arco à primeira planilha. Os parâmetros definem a posição e o tamanho do arco: `(left, top, width, height, startAngle, endAngle)`. É como traçar um segmento de um círculo!
## Etapa 4: personalize o primeiro arco
Depois de adicionar o arco, você pode querer personalizar sua aparência.
```csharp
// Defina a cor da forma de preenchimento
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Defina o posicionamento do arco.
arc1.Placement = PlacementType.FreeFloating;           
// Defina a espessura da linha.
arc1.Line.Weight = 1;      
// Defina o estilo do traço do arco.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Nesta seção, estamos personalizando o arco. Definimos o tipo de preenchimento como cor sólida (azul neste caso), definimos como ele será posicionado, definimos a espessura da linha e escolhemos um estilo de traço. Basicamente, estamos decorando nosso arco para torná-lo visualmente atraente!
## Etapa 5: adicione uma segunda forma de arco
Vamos adicionar outra forma de arco para fornecer mais contexto.
```csharp
// Adicione outra forma de arco.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Semelhante ao primeiro arco, estamos adicionando um segundo arco na mesma planilha. As coordenadas aqui estão um pouco deslocadas para posicioná-lo de forma diferente.
## Etapa 6: personalize o segundo arco
Assim como fizemos no primeiro arco, personalizaremos o segundo também.
```csharp
// Defina a cor da linha
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Defina o posicionamento do arco.
arc2.Placement = PlacementType.FreeFloating;          
// Defina a espessura da linha.
arc2.Line.Weight = 1;           
// Defina o estilo do traço do arco.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aqui, damos ao segundo arco o mesmo estilo do primeiro. Você pode alterar a cor ou o estilo conforme desejar, para fins de exclusividade ou temática.
## Etapa 7: Salve a pasta de trabalho
Por fim, é hora de salvar sua pasta de trabalho recém-criada com os arcos.
```csharp
// Salve o arquivo Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Esta linha funciona como clicar no botão de salvar. Estamos salvando nosso trabalho no local especificado com um nome de arquivo específico. Certifique-se de verificar seu diretório para ver sua obra-prima em formato Excel!
## Conclusão
Neste tutorial, exploramos o processo de adicionar formas de arco a uma planilha do Excel usando o Aspose.Cells para .NET. Por meio de um guia passo a passo simples, você aprendeu a criar uma nova pasta de trabalho, adicionar arcos, personalizar sua aparência e salvar seu documento. Esse recurso não apenas aprimora o apelo visual de suas planilhas, como também torna suas apresentações de dados mais informativas. Seja criando gráficos, relatórios ou apenas experimentando, usar formas como arcos pode adicionar um toque criativo aos seus projetos.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa que permite aos desenvolvedores criar, manipular e converter arquivos do Excel programaticamente, sem a necessidade do Microsoft Excel.
### Preciso instalar o Microsoft Excel para usar o Aspose.Cells?
Não, o Aspose.Cells é completamente independente e não requer a instalação do Microsoft Excel.
### Posso testar o Aspose.Cells gratuitamente?
Sim, você pode experimentar o Aspose.Cells usando seus [Teste grátis](https://releases.aspose.com/).
### Quais linguagens de programação o Aspose.Cells suporta?
O Aspose.Cells oferece suporte a várias linguagens, incluindo C#, VB.NET e muito mais.
### Onde posso obter suporte para o Aspose.Cells?
Você pode obter suporte através do [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}