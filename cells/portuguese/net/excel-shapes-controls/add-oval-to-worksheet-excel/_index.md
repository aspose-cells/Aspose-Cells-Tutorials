---
"description": "Aprenda a adicionar uma oval a uma planilha do Excel usando o Aspose.Cells para .NET. Guia passo a passo com explicações detalhadas do código."
"linktitle": "Adicionar oval à planilha no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar oval à planilha no Excel"
"url": "/pt/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar oval à planilha no Excel

## Introdução
Criar arquivos Excel impressionantes e interativos pode envolver mais do que apenas números e fórmulas. Formas como ovais podem adicionar um apelo visual ou fornecer elementos funcionais às suas planilhas. Neste tutorial, exploraremos como usar o Aspose.Cells para .NET para adicionar ovais a uma planilha do Excel programaticamente. Seja para adicionar um toque especial ou funcionalidade, temos um guia passo a passo que explica tudo.
## Pré-requisitos
Antes de mergulhar no código, há algumas coisas que você precisa ter em mãos:
1. Biblioteca Aspose.Cells para .NET: Você pode baixá-la em [aqui](https://releases.aspose.com/cells/net/) ou instalá-lo usando o NuGet no Visual Studio.
2. Ambiente de desenvolvimento: AC# IDE como Visual Studio.
3. Noções básicas de C#: você deve estar familiarizado com conceitos básicos de codificação em C#.
Lembre-se também de configurar seu projeto instalando a biblioteca Aspose.Cells para .NET. Se você ainda não possui uma licença, pode solicitar uma. [licença temporária](https://purchase.aspose.com/temporary-license/) ou use o [teste gratuito](https://releases.aspose.com/) versão.
## Pacotes de importação
Antes de escrever qualquer código, certifique-se de incluir os namespaces necessários. Aqui está o trecho de código C# para garantir que você esteja usando as bibliotecas corretas:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Etapa 1: configure seu diretório
O primeiro passo para adicionar uma oval a uma planilha do Excel é especificar onde o arquivo será salvo. Vamos definir o caminho do diretório e garantir que ele exista antes de salvar nosso trabalho.

Criaremos um caminho de diretório e verificaremos se ele existe. Se a pasta não existir, ela será criada.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Esta etapa é crucial, pois garante que seu arquivo seja salvo em um local adequado e que você não tenha problemas com o caminho do arquivo mais tarde.
## Etapa 2: inicializar uma nova pasta de trabalho
Em seguida, precisamos criar uma nova pasta de trabalho na qual adicionaremos nossas formas ovais. A pasta de trabalho representa um arquivo do Excel, e podemos adicionar conteúdo ou formas a ela.

Nesta etapa, instanciamos um novo `Workbook` objeto que servirá como nosso contêiner de arquivos do Excel.
```csharp
// Instanciar uma nova pasta de trabalho.
Workbook excelbook = new Workbook();
```
## Etapa 3: adicione a primeira forma oval
Agora vem a parte divertida: adicionar uma forma oval à planilha. Essa forma oval pode representar um elemento visual, como um botão ou um destaque. Começaremos adicionando a primeira forma oval à primeira planilha da nossa pasta de trabalho.

Aqui, usamos o `Shapes.AddOval()` método para criar uma oval na planilha em uma linha e coluna específicas.
```csharp
// Adicione uma forma oval.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Os parâmetros internos `AddOval()` são os seguintes:
- Os dois primeiros números representam a linha e a coluna do canto superior esquerdo do oval.
- Os próximos dois números representam a altura e a largura do oval.
## Etapa 4: Defina o posicionamento e o estilo do oval
Uma vez criado o oval, podemos definir sua posição, espessura da linha e estilo do traço. `Placement` propriedade determina como o oval se comporta quando você redimensiona ou move células na planilha.

Deixamos o oval flutuando livremente e ajustamos sua aparência.
```csharp
// Defina o posicionamento do oval.
oval1.Placement = PlacementType.FreeFloating;
// Defina a espessura da linha.
oval1.Line.Weight = 1;
// Defina o estilo do traço do oval.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Isso permite que o oval se mova livremente na planilha, e sua espessura de linha e estilo são definidos para consistência visual.
## Etapa 5: adicione outra forma oval (círculo)
Por que parar em um? Nesta etapa, adicionaremos outra forma oval, desta vez criando um círculo perfeito, mantendo a altura e a largura iguais.

Criamos outro oval, colocamos em um local diferente e garantimos que ele tenha um formato circular definindo altura e largura iguais.
```csharp
// Adicione outra forma oval (círculo).
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Etapa 6: estilize o segundo oval
Assim como antes, ajustaremos o posicionamento, o peso e o estilo do traço deste segundo oval (ou círculo).

Aplicamos propriedades semelhantes ao segundo oval para combinar com o estilo do primeiro.
```csharp
// Defina o posicionamento do oval.
oval2.Placement = PlacementType.FreeFloating;
// Defina a espessura da linha.
oval2.Line.Weight = 1;
// Defina o estilo do traço do oval.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Etapa 7: Salve a pasta de trabalho
Por fim, precisamos salvar a pasta de trabalho com as ovais que acabamos de adicionar. Salvar o arquivo garante que todas as nossas alterações sejam armazenadas.

Salvamos a pasta de trabalho no caminho do diretório que definimos anteriormente.
```csharp
// Salve o arquivo Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
E pronto! Você adicionou ovais com sucesso à sua planilha do Excel e salvou o arquivo.
## Conclusão
Adicionar formas ovais a uma planilha do Excel usando o Aspose.Cells para .NET não é apenas simples, mas também uma maneira divertida de aprimorar suas planilhas com elementos visuais adicionais. Seja para fins de design ou para adicionar elementos clicáveis, as formas podem desempenhar um papel significativo na aparência e no funcionamento dos seus arquivos do Excel. Portanto, da próxima vez que estiver trabalhando em um projeto que exija planilhas interativas ou visualmente atraentes do Excel, você saberá exatamente como adicionar aquelas formas ovais perfeitas!
## Perguntas frequentes
### Posso adicionar outras formas, como retângulos ou linhas, usando o Aspose.Cells para .NET?
Sim, você pode adicionar várias formas como retângulos, linhas e setas usando o `Shapes` coleção em Aspose.Cells.
### É possível redimensionar os ovais depois de adicioná-los?
Com certeza! Você pode modificar as propriedades de altura e largura dos ovais depois de adicioná-los.
### Em quais formatos de arquivo posso salvar a pasta de trabalho além de XLS?
O Aspose.Cells suporta vários formatos como XLSX, CSV e PDF, entre outros.
### Posso modificar a cor do contorno do oval?
Sim, você pode alterar a cor da linha oval usando o `Line.Color` propriedade.
### É necessário ter uma licença para o Aspose.Cells?
Embora você possa experimentar o Aspose.Cells com uma avaliação gratuita, você precisará de um [licença](https://purchase.aspose.com/buy) para uso de longo prazo ou para acessar recursos avançados.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}