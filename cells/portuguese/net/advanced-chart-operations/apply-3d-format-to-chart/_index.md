---
title: Aplicar formato 3D ao gráfico
linktitle: Aplicar formato 3D ao gráfico
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra como criar gráficos 3D impressionantes no Excel usando Aspose.Cells para .NET. Siga nosso guia passo a passo simples.
weight: 10
url: /pt/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar formato 3D ao gráfico

## Introdução

Em uma era em que a visualização de dados é primordial, a maneira como apresentamos nossos dados vai além de gráficos e tabelas básicas. Com ferramentas como Aspose.Cells para .NET, você pode elevar suas apresentações de dados com gráficos 3D impressionantes que não apenas chamam a atenção, mas também transmitem informações de forma eficaz. Este guia o guiará pelas etapas para aplicar um formato 3D a um gráfico usando Aspose.Cells, transformando seus dados brutos em uma exibição envolvente.

## Pré-requisitos

Antes de nos aprofundarmos nos detalhes da aplicação de um formato 3D a um gráfico, vamos garantir que você tenha tudo o que precisa.

### Requisitos de software

- Visual Studio: certifique-se de ter o Visual Studio instalado para trabalhar com aplicativos .NET.
-  Aspose.Cells para .NET: Se ainda não o fez, baixe e instale o Aspose.Cells em[aqui](https://releases.aspose.com/cells/net/).

### Configuração do ambiente de codificação

1. Crie um novo projeto .NET: Abra o Visual Studio, selecione “Criar um novo projeto” e escolha um aplicativo de console.
2. Adicionar referência Aspose.Cells: por meio do Gerenciador de Pacotes NuGet, adicione Aspose.Cells pesquisando por ele ou por meio do Console do Gerenciador de Pacotes:

```bash
Install-Package Aspose.Cells
```

3. Configurar diretório de saída: designe um diretório de saída onde os arquivos gerados serão salvos. Isso pode ser tão simples quanto criar uma pasta na sua área de trabalho.

Agora que você está tudo pronto, é hora de começar a codificar e criar alguns gráficos 3D deslumbrantes!

## Pacotes de importação

Para começar, você precisa importar os namespaces necessários. Isso ajudará você a acessar as classes e métodos fornecidos pelo Aspose.Cells. Veja como fazer isso:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Esta seção dividirá o processo em etapas gerenciáveis, fornecendo a você uma compreensão clara de cada estágio.

## Etapa 1: inicialize sua pasta de trabalho

 Primeiro, você precisa criar uma instância do`Workbook` classe. Este objeto servirá como base para seu documento Excel.

```csharp
//Diretório de saída
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Pense nisso`Workbook` como uma tela em branco, pronta para ser preenchida com dados coloridos e visualizações impactantes.

## Etapa 2: renomeie a primeira planilha

Em seguida, vamos renomear a primeira planilha. Isso fornece clareza sobre com quais dados estamos trabalhando.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Os nomes devem ser intuitivos. Neste caso, estamos nomeando-o "DataSheet" para que saibamos onde nossos dados vivem.

## Etapa 3: Crie dados para o gráfico

Agora, adicionaremos alguns dados à nossa "Folha de Dados". Vamos preenchê-la com valores que nosso gráfico usará.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Assim como uma receita depende dos ingredientes, a eficácia do seu gráfico depende da qualidade e organização dos seus dados de entrada.

## Etapa 4: Configurar uma nova planilha de gráfico

Hora de criar uma nova planilha para o próprio gráfico. Isso ajuda a manter sua visualização de dados organizada.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Considere esta planilha como seu palco, onde o desempenho dos seus dados se desenvolve.

## Etapa 5: Adicionar um gráfico

Aqui, adicionaremos um gráfico de colunas à planilha recém-criada.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Estamos definindo um espaço para nosso gráfico e especificando qual tipo ele é. Pense nisso como selecionar o tipo de moldura para sua arte.

## Etapa 6: personalizar a aparência do gráfico

Agora, vamos personalizar a aparência do nosso gráfico definindo as cores de fundo. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Um fundo branco limpo geralmente faz com que as cores dos seus dados se destaquem, melhorando a visibilidade.

## Etapa 7: Adicionar séries de dados ao gráfico

É hora de alimentar nosso gráfico com os dados. Adicionaremos uma série de dados da nossa "DataSheet" para garantir que nosso gráfico reflita os dados que precisamos.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Isso é análogo a um chef preparando um prato com ingredientes específicos. Cada ponto de dados importa!

## Etapa 8: Acesse e formate a série de dados

Agora que nossos dados estão vinculados, vamos pegar as séries de dados e começar a aplicar alguns efeitos 3D.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Estamos nos preparando para adicionar um toque especial ao nosso prato — pense nisso como um tempero que realça o sabor geral.

## Etapa 9: aplique efeitos de chanfro 3D

Em seguida, adicionaremos um efeito de chanfro para dar alguma dimensão ao nosso gráfico.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Assim como um escultor molda uma pedra, estamos criando profundidade que dá vida ao nosso gráfico!

## Etapa 10: personalize o material da superfície e a iluminação

Vamos fazer nosso gráfico brilhar intensamente! Ajustaremos o material da superfície e as configurações de iluminação.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Iluminação e material adequados podem transformar um objeto plano em um visual cativante. Pense em um cenário de filme iluminado por especialistas para realçar cada cena.

## Etapa 11: retoques finais na aparência da série

Agora, vamos finalizar a aparência da nossa série de dados ajustando sua cor.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

A cor certa pode evocar certos sentimentos e reações: o marrom acrescenta um toque de elegância e sofisticação.

## Etapa 12: Salve sua pasta de trabalho

Finalmente, é hora de salvar sua obra-prima! Não esqueça de especificar o destino onde você quer armazená-la.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Salvar seu trabalho é como colocar sua arte em uma galeria; é um momento para valorizar e compartilhar.

## Conclusão

Parabéns! Você criou com sucesso um gráfico 3D visualmente atraente usando o Aspose.Cells para .NET. Seguindo essas etapas, você agora tem uma ferramenta poderosa para aprimorar suas apresentações de dados, tornando-as não apenas informativas, mas também visualmente cativantes. Ao refinar seus gráficos, lembre-se de que cada visualização é uma história — torne-a envolvente, clara e impactante!

## Perguntas frequentes

### O que é Aspose.Cells para .NET?
Aspose.Cells para .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular documentos do Excel programaticamente, incluindo a criação de gráficos e diagramas.

### Posso personalizar tipos de gráfico no Aspose.Cells?
Sim! O Aspose.Cells suporta vários tipos de gráficos como Coluna, Linha, Pizza e muitos outros, que podem ser facilmente personalizados.

### Existe um teste gratuito disponível para o Aspose.Cells?
 Absolutamente! Você pode baixar uma versão de teste gratuita em[aqui](https://releases.aspose.com/).

### Posso aplicar outros efeitos aos gráficos além dos formatos 3D?
Sim, você pode aplicar vários efeitos, como sombras, gradientes e estilos diferentes para aprimorar seus gráficos além do 3D.

### Onde posso encontrar suporte para o Aspose.Cells?
 Para obter suporte, você pode visitar o[Fórum Aspose](https://forum.aspose.com/c/cells/9) para assistência e ajuda da comunidade.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
