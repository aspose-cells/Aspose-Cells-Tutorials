---
title: Especificar fonte do Extremo Oriente e Latina no Excel
linktitle: Especificar fonte do Extremo Oriente e Latina no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a especificar fontes do Extremo Oriente e Latinas no Excel usando o Aspose.Cells para .NET neste tutorial abrangente e fácil de seguir.
weight: 17
url: /pt/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificar fonte do Extremo Oriente e Latina no Excel

## Introdução
Você está procurando aprimorar seus relatórios ou documentos do Excel com requisitos de fonte específicos? Quer você esteja lidando com vários idiomas ou simplesmente buscando uma estética única em suas planilhas, entender como especificar fontes do Extremo Oriente e Latinas no Excel é uma habilidade crucial. Para sua sorte, temos uma solução! Neste tutorial, exploramos como usar o Aspose.Cells para .NET para implementar esse recurso perfeitamente. Vamos mergulhar!
## Pré-requisitos
Antes de começarmos, há algumas coisas que você precisa configurar antes de começar a usar o Aspose.Cells:
### .NET Framework ou .NET Core
Certifique-se de ter o .NET Framework ou .NET Core instalado na sua máquina. Esta biblioteca funciona bem com ambos.
### Instalação do Aspose.Cells
 Você precisará baixar a biblioteca Aspose.Cells. Você pode[baixe aqui](https://releases.aspose.com/cells/net/) . Se você não estiver familiarizado com a instalação de pacotes NuGet, siga[este guia](https://www.nuget.org/).
### Ambiente de Desenvolvimento Integrado (IDE)
Ter um IDE como o Visual Studio ou o JetBrains Rider pode simplificar a codificação, a depuração e a execução do seu projeto.
### Conhecimento básico de C#
A familiaridade com a programação em C# será muito benéfica para seguir este tutorial.
## Pacotes de importação
Antes de podermos trabalhar com Aspose.Cells, precisamos importar os pacotes necessários para o nosso projeto. Veja como você pode fazer isso:
### Criar um novo projeto
1. Abra seu IDE e crie um novo projeto de aplicativo de console.
2.  Dê ao seu projeto um nome descritivo, como`FontSpecifyingApp`.
### Adicionar pacote Aspose.Cells NuGet
1. Clique com o botão direito do mouse no seu projeto no Solution Explorer.
2.  Selecione`Manage NuGet Packages...`.
3.  Procurar`Aspose.Cells` e instale-o.
Ao final dessas etapas, você terá tudo pronto para começar a codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Com a configuração feita, é hora de arregaçar as mangas e começar a codificar. Especificamente, criaremos uma nova pasta de trabalho do Excel e especificaremos as fontes Far East e Latin para caixas de texto. Veja como fazer isso passo a passo:
## Etapa 1: Configurar o diretório de saída
Começamos especificando onde queremos salvar nosso arquivo Excel. Isso é crucial porque queremos garantir que nosso arquivo de saída seja armazenado em um local de fácil acesso.
```csharp
// Diretório de saída
string outputDir = "Your Document Directory";
```
## Etapa 2: Crie uma pasta de trabalho vazia
Agora que configuramos nosso diretório, vamos criar uma nova pasta de trabalho onde adicionaremos nosso conteúdo. Isso é semelhante a começar com uma tela nova antes de pintar.
```csharp
// Crie uma pasta de trabalho vazia.
Workbook wb = new Workbook();
```
## Etapa 3: Acesse a primeira planilha
Em seguida, queremos trabalhar com uma planilha do nosso livro de exercícios. Pense em uma planilha como uma página do seu livro onde toda a mágica acontece.
```csharp
// Acesse a primeira planilha.
Worksheet ws = wb.Worksheets[0];
```
## Etapa 4: Adicionar uma caixa de texto
Agora, adicionaremos uma caixa de texto à nossa planilha. É aqui que digitaremos nosso texto. Imagine isso como criar uma caixa de texto dentro de um slide de uma apresentação.
```csharp
// Adicione uma caixa de texto dentro da planilha.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Etapa 5: Defina o texto da caixa de texto
Vamos digitar algum texto. Neste exemplo, vamos inserir caracteres japoneses para demonstrar a fonte Far East. É tão simples quanto escrever em uma caixa de texto no seu computador!
```csharp
// Defina o texto da caixa de texto.
tb.Text = "こんにちは世界"; //Isso significa "Olá, Mundo" em japonês.
```
## Etapa 6: Especifique as fontes
Agora vem a parte emocionante! Vamos definir as fontes Latina e Extremo Oriente para o texto. Isso é semelhante a escolher a fonte perfeita para um convite de casamento chique!
```csharp
// Especifique o nome do Extremo Oriente e do latim da fonte.
tb.TextOptions.LatinName = "Comic Sans MS"; // Esta é a fonte latina que escolhemos.
tb.TextOptions.FarEastName = "KaiTi"; // Esta é a fonte Far East que desejamos.
```
## Etapa 7: Salve o arquivo de saída do Excel
Por fim, vamos salvar nossa pasta de trabalho! Este passo encerra nossa tarefa e garante que todo o trabalho duro que fizemos seja salvo corretamente. 
```csharp
// Salve o arquivo de saída do Excel.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Etapa 8: Mensagem de confirmação
Para nos informar que tudo foi executado com sucesso, imprimiremos uma mensagem de confirmação no console:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Conclusão
E aí está! Você especificou com sucesso fontes Far East e Latin em uma pasta de trabalho do Excel usando Aspose.Cells para .NET. Essa habilidade não só dá aos seus documentos um toque profissional, mas também enriquece a experiência de leitura para usuários em diferentes idiomas.
Sinta-se à vontade para experimentar diferentes fontes e estilos para encontrar uma combinação que se encaixe em suas necessidades específicas. Boa codificação!
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET para criar e gerenciar planilhas do Excel sem precisar ter o Microsoft Excel instalado em sua máquina. 
### Posso usar o Aspose.Cells para aplicativos web?
Sim! O Aspose.Cells pode ser usado tanto para aplicativos de desktop quanto para aplicativos web criados com .NET.
### Existe uma versão gratuita do Aspose.Cells?
 Sim, o Aspose oferece um teste gratuito. Você pode[baixe aqui](https://releases.aspose.com/).
### Como obtenho suporte para o Aspose.Cells?
 Você pode pedir suporte e encontrar recursos valiosos no[Fóruns Aspose](https://forum.aspose.com/c/cells/9).
### Onde posso comprar o Aspose.Cells?
 Você pode comprar Aspose.Cells diretamente do[Site Aspose](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
