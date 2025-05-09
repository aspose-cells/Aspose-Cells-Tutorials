---
"description": "Aprenda a adicionar imagens facilmente a gráficos do Excel usando o Aspose.Cells para .NET. Aprimore seus gráficos e apresentações em apenas alguns passos simples."
"linktitle": "Adicionar imagem ao gráfico"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar imagem ao gráfico"
"url": "/pt/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar imagem ao gráfico

## Introdução

Cansado de gráficos sem graça e sem um toque pessoal? Quer aprender a incrementar seus visuais do Excel adicionando imagens? Bem, você está com sorte! Neste tutorial, vamos mergulhar no mundo do Aspose.Cells para .NET e aprender como adicionar imagens a gráficos no Excel. Então, pegue sua xícara de café favorita e vamos começar!

## Pré-requisitos

Antes de começarmos a trabalhar nos detalhes da codificação, existem alguns pré-requisitos que você precisa ter para seguir adiante sem problemas:

- Visual Studio: É aqui que você escreverá e executará seu código .NET. Certifique-se de tê-lo instalado.
- Aspose.Cells para .NET: Você precisará desta biblioteca para trabalhar com arquivos do Excel. Você pode [baixe aqui](https://releases.aspose.com/cells/net/).
- Noções básicas de C#: embora eu o oriente pelo código, ter uma noção dos conceitos básicos de C# deixará as coisas mais claras.

### Etapas de instalação

1. Instalar o Aspose.Cells: Você pode adicionar o Aspose.Cells ao seu projeto do Visual Studio por meio do Gerenciador de Pacotes NuGet. Para isso, acesse Ferramentas > Gerenciador de Pacotes NuGet > Gerenciar Pacotes NuGet para Solution e pesquise por "Aspose.Cells". Clique em Instalar.
2. Configurando seu projeto: crie um novo projeto de aplicativo de console C# no Visual Studio.

## Pacotes de importação

Depois de configurar tudo, o próximo passo é importar os pacotes necessários para o seu projeto. Veja como fazer:

### Importe os namespaces necessários

No início do seu arquivo de código C#, você precisará importar os seguintes namespaces:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Isso diz ao seu programa: "Ei! Vou usar esses recursos legais do Aspose.Cells."

Agora que definimos nossos pré-requisitos, vamos dividir o processo em etapas menores. 

## Etapa 1: Defina seus diretórios

Antes de mais nada, precisamos configurar os caminhos para nossos arquivos de entrada e saída. Esta etapa é crucial porque precisamos saber onde encontrar nosso arquivo Excel existente e onde salvar o arquivo modificado.

```csharp
//Diretório de origem
string sourceDir = "Your Document Directory/";

//Diretório de saída
string outputDir = "Your Output Directory/";
```

Substituir `Your Document Directory` e `Your Output Directory` com caminhos reais no seu computador. 

## Etapa 2: Carregar a pasta de trabalho existente

Agora, vamos carregar o arquivo Excel existente onde queremos adicionar nossa imagem ao gráfico.

```csharp
// Abra o arquivo existente.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Este código abre a pasta de trabalho, deixando-a pronta para edição.

## Etapa 3: preparar o fluxo de imagens

Antes de adicionar a imagem, precisamos ler a imagem que queremos inserir no gráfico. 

```csharp
// Obter um arquivo de imagem para o fluxo.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Certifique-se de que a imagem foi salva no diretório especificado.

## Etapa 4: Direcione o gráfico

Agora, vamos especificar a qual gráfico adicionaremos a imagem. Neste exemplo, usaremos como alvo o primeiro gráfico da primeira planilha.

```csharp
// Pegue o gráfico do designer na segunda folha.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Você pode acessar qualquer planilha alterando o índice adequadamente.

## Etapa 5: adicione a imagem ao gráfico

Com o gráfico selecionado, é hora de adicionar a imagem! 

```csharp
// Adicione uma nova imagem ao gráfico.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Aqui, `50` e `50` são as coordenadas X e Y onde a imagem será colocada e `200` é a largura e a altura da imagem.

## Etapa 6: personalize o formato de linha da imagem

Quer dar um toque especial à sua foto? Você pode personalizar a borda! Veja como fazer:

```csharp
// Obtenha o tipo de formato de linha da imagem.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Defina o estilo do traço.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Defina a espessura da linha.
lineformat.Weight = 4;    
```

Este trecho permite que você escolha a aparência e a espessura da borda. Escolha qualquer estilo que combine com sua apresentação!

## Etapa 7: Salve a pasta de trabalho modificada

Depois de todo esse trabalho duro, vamos salvar suas modificações executando a seguinte linha de código:

```csharp
// Salve o arquivo Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Agora sua imagem foi integrada com sucesso ao gráfico e seu arquivo de saída está pronto para visualização!

## Etapa 8: Indique o sucesso

Por fim, você pode adicionar uma mensagem simples para confirmar que sua operação foi bem-sucedida:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusão

Neste tutorial, exploramos como dar um toque de personalidade aos seus gráficos do Excel adicionando imagens usando o Aspose.Cells para .NET. Com apenas alguns passos simples, você pode transformar suas apresentações comuns em memoráveis. Então, o que você está esperando? Experimente e deixe seus gráficos brilharem!

## Perguntas frequentes

### Posso adicionar várias imagens a um único gráfico?
Sim! Você pode ligar para o `AddPictureInChart` método várias vezes para adicionar quantas fotos desejar.

### Quais formatos de imagem o Aspose.Cells suporta?
O Aspose.Cells suporta uma variedade de formatos de imagem, incluindo PNG, JPEG, BMP e GIF.

### Posso personalizar a posição da imagem?
Certamente! As coordenadas X e Y no `AddPictureInChart` método permite posicionamento preciso.

### O Aspose.Cells é gratuito?
O Aspose.Cells oferece um teste gratuito, mas para obter todos os recursos, é necessária uma licença. Você pode encontrar os preços [aqui](https://purchase.aspose.com/buy).

### Onde posso encontrar mais exemplos?
Confira o [Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para exemplos e funcionalidades mais detalhados.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}