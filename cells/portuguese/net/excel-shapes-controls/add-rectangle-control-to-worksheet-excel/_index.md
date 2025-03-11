---
title: Adicionar controle retângulo à planilha no Excel
linktitle: Adicionar controle retângulo à planilha no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar um controle retangular a uma planilha do Excel usando o Aspose.Cells para .NET com um guia detalhado passo a passo.
weight: 25
url: /pt/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar controle retângulo à planilha no Excel

## Introdução
Quando se trata de automatizar tarefas do Excel, o Aspose.Cells for .NET é uma ferramenta poderosa que pode ajudar você a atingir uma variedade de objetivos, um dos quais é adicionar formas como retângulos às suas planilhas. Neste guia, exploraremos como adicionar um controle de retângulo a uma planilha do Excel usando o Aspose.Cells for .NET. No final, você poderá criar, personalizar e salvar uma planilha com um controle de retângulo incorporado a ela.
Mas antes de começar, vamos falar sobre os pré-requisitos.
## Pré-requisitos
Para acompanhar este tutorial, certifique-se de ter os seguintes pré-requisitos:
1.  Biblioteca Aspose.Cells para .NET: Se você ainda não o fez,[baixar a biblioteca](https://releases.aspose.com/cells/net/) ou instale-o usando o NuGet no Visual Studio.
2. .NET Framework: você precisa ter o ambiente de desenvolvimento .NET configurado em sua máquina.
3. Conhecimento básico de C#: Embora o guiaremos passo a passo, é benéfica a familiaridade básica com C# e programação orientada a objetos.
4.  Licença: Usar Aspose.Cells no modo de avaliação funciona bem para tarefas básicas, mas para funcionalidade completa, considere obter um[licença temporária](https://purchase.aspose.com/temporary-license/)ou comprar um de[aqui](https://purchase.aspose.com/buy).
Agora, vamos mergulhar no código!
## Pacotes de importação
Para começar a usar o Aspose.Cells, certifique-se de ter importado os namespaces necessários para o seu projeto. Essas importações permitirão acesso a várias classes e métodos que você precisa para interagir com arquivos do Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Essas linhas garantem que seu projeto possa interagir com diretórios de arquivos (`System.IO`), pastas de trabalho do Excel (`Aspose.Cells`) e desenho de formas (`Aspose.Cells.Drawing`).
Agora, vamos dividir o processo em etapas simples para que você possa acompanhar e replicar facilmente em seus próprios projetos.
## Etapa 1: Configurando o caminho do diretório
A primeira coisa que você precisa fazer é definir o diretório onde seu arquivo Excel será salvo. Este passo garante que seu projeto saiba onde criar e armazenar o arquivo de saída.
### Definindo o diretório de dados
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```
 Aqui, você especifica o caminho do diretório onde o arquivo Excel será armazenado. Você pode substituir`"Your Document Directory"` com o caminho real na sua máquina, ou crie uma pasta dinamicamente se ela não existir.
### Verificando e criando o diretório
```csharp
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este bloco verifica se o diretório existe. Se não, ele cria um. Pense nisso como ter seu arquivo pronto antes de armazenar qualquer documento.
## Etapa 2: Instanciando uma nova pasta de trabalho
 Nesta etapa, você cria uma nova pasta de trabalho do Excel usando o`Aspose.Cells.Workbook` class. Isso servirá como contêiner para sua planilha e formas.
```csharp
// Instanciar uma nova pasta de trabalho.
Workbook excelbook = new Workbook();
```
 Ao chamar o`Workbook` construtor, agora você tem uma pasta de trabalho do Excel em branco pronta para personalização.
## Etapa 3: Adicionando um controle retângulo
É aqui que a mágica acontece. Você adicionará uma forma retangular à primeira planilha da sua pasta de trabalho.
```csharp
// Adicione um controle de retângulo.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Vamos analisar isso:
- `excelbook.Worksheets[0]`: Isso acessa a primeira planilha na sua pasta de trabalho.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Isso adiciona um formato retangular à planilha. Os parâmetros aqui definem a posição (linha e coluna), bem como a largura e a altura do retângulo.
## Etapa 4: Personalizando o retângulo
Apenas adicionar um retângulo não é o suficiente — você vai querer personalizá-lo. Nesta etapa, definiremos o posicionamento, a espessura da linha e o estilo do traço do retângulo.
### Definindo o posicionamento
```csharp
// Defina o posicionamento do retângulo.
rectangle.Placement = PlacementType.FreeFloating;
```
Isso especifica que o retângulo é flutuante livre, o que significa que ele não será limitado pelas dimensões da célula.
### Definindo a espessura da linha
```csharp
// Defina a espessura da linha.
rectangle.Line.Weight = 4;
```
Aqui, definimos a espessura da linha do retângulo para 4 pontos. Quanto maior o número, mais grossa a linha.
### Definindo o estilo do traço
```csharp
// Defina o estilo do traço do retângulo.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Esta linha define o estilo de traço da borda do retângulo como sólido. Você pode experimentar diferentes estilos como`Dash` ou`Dot` dependendo de suas necessidades.
## Etapa 5: Salvando a pasta de trabalho
Depois que o retângulo for adicionado e personalizado, a etapa final é salvar a pasta de trabalho no diretório especificado.
```csharp
// Salve o arquivo Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
 Isso salva a pasta de trabalho como um`.xls` arquivo na pasta que você definiu anteriormente. Você pode modificar o formato do arquivo alterando a extensão, como`.xlsx` se você preferir o formato mais recente do Excel.
## Conclusão
aí está! Adicionar um controle retangular a uma planilha do Excel usando o Aspose.Cells para .NET é um processo direto, uma vez que você o divide passo a passo. Se você precisa adicionar formas para apelo visual, destacar seções de seus dados ou personalizar seus relatórios, o Aspose.Cells oferece a flexibilidade para fazer isso programaticamente.
Este guia deve ter equipado você com todo o conhecimento necessário para começar a adicionar formas como retângulos às suas planilhas do Excel com Aspose.Cells. Agora é hora de experimentar e ver o que mais você pode conseguir com esta poderosa biblioteca!
## Perguntas frequentes
### Posso adicionar outras formas, como círculos ou linhas, usando o Aspose.Cells para .NET?  
Sim, o Aspose.Cells permite que você adicione uma variedade de formas, incluindo círculos, linhas, setas e muito mais.
### Que outras propriedades posso definir para o controle retângulo?  
Você pode personalizar a cor de preenchimento, a cor da linha, a transparência e até mesmo adicionar texto dentro do retângulo.
### O Aspose.Cells é compatível com o .NET Core?  
Sim, o Aspose.Cells suporta .NET Core, bem como .NET Framework e outras plataformas baseadas em .NET.
### Posso posicionar o retângulo em relação a uma célula específica?  
 Sim, você pode colocar o retângulo dentro de linhas e colunas específicas ou usar o`PlacementType` para controlar como ele é ancorado.
### Existe um teste gratuito disponível para o Aspose.Cells?  
 Sim, você pode obter um[teste gratuito](https://releases.aspose.com/) do site para testar os recursos da biblioteca antes de comprar.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
