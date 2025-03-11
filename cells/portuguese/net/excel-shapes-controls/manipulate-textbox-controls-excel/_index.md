---
title: Manipular controles TextBox no Excel
linktitle: Manipular controles TextBox no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a manipular caixas de texto no Excel usando o Aspose.Cells para .NET com este tutorial passo a passo fácil de seguir.
weight: 15
url: /pt/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipular controles TextBox no Excel

## Introdução
Se você já trabalhou com o Excel, provavelmente já se deparou com aquelas pequenas caixas de texto que permitem adicionar texto flutuante a uma planilha. Mas e se você precisar manipular essas caixas de texto programaticamente? É aí que o Aspose.Cells for .NET é útil. Com ele, você pode acessar e modificar caixas de texto com facilidade, tornando-o perfeito para automatizar tarefas ou personalizar relatórios. Neste tutorial, mostraremos a você o processo de manipulação de caixas de texto no Excel usando o Aspose.Cells for .NET.
## Pré-requisitos
Antes de mergulhar no código propriamente dito, vamos nos certificar de que tudo esteja configurado corretamente:
1.  Aspose.Cells para .NET: Você precisa baixar a biblioteca Aspose.Cells para .NET. Você pode encontrar o link para download[aqui](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento .NET: qualquer IDE que suporte .NET, como o Visual Studio, funcionará.
3. Conhecimento básico de C#: Este tutorial pressupõe que você esteja familiarizado com a sintaxe básica do C# e com a estrutura das pastas de trabalho do Excel.
4.  Arquivo Excel: Um arquivo Excel existente com caixas de texto (usaremos`book1.xls`neste exemplo).
5.  Licença Aspose: Se você não estiver usando a versão de teste gratuita, será necessário[comprar](https://purchase.aspose.com/buy) uma licença ou obter uma[temporário](https://purchase.aspose.com/temporary-license/).
Agora, vamos mergulhar nos passos!
## Pacotes de importação
Antes de poder manipular pastas de trabalho e caixas de texto do Excel usando Aspose.Cells, você precisa importar os namespaces necessários. Aqui está o trecho de código que você usará no topo do seu arquivo C#:
```csharp
using System.IO;
using Aspose.Cells;
```
Esses pacotes dão acesso à manipulação de pastas de trabalho, acesso a planilhas e objetos de desenho (como caixas de texto).
Agora que configuramos tudo, vamos dividir o processo de manipulação de caixas de texto em etapas fáceis de seguir.
## Etapa 1: configure seu diretório de pasta de trabalho
 O primeiro passo é especificar onde seus arquivos do Excel estão localizados no seu sistema. Você precisará substituir o placeholder`Your Document Directory` com o caminho real para o seu arquivo. Este caminho é armazenado no`dataDir` variável para fácil referência em todo o código.
```csharp
string dataDir = "Your Document Directory";
```
Isso permite que seu programa saiba onde encontrar o arquivo Excel de entrada (`book1.xls`) e onde salvar o arquivo de saída.
## Etapa 2: Abra o arquivo Excel
Em seguida, você precisará carregar o arquivo Excel existente no objeto Aspose.Cells Workbook. Esta pasta de trabalho atua como o contêiner para seus dados do Excel, dando a você acesso às suas planilhas e a quaisquer objetos de desenho (como caixas de texto).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 O`Workbook` class do Aspose.Cells carregará o arquivo Excel especificado do seu diretório. Se o arquivo não existir no diretório especificado, ele lançará uma exceção, então certifique-se de que o caminho esteja correto.
## Etapa 3: Acesse a primeira planilha
Agora que você carregou a pasta de trabalho, você pode acessar suas planilhas. Neste exemplo, estamos acessando a primeira planilha na pasta de trabalho, que está armazenada no índice 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 O`Worksheets` propriedade dá acesso a todas as planilhas na pasta de trabalho. Aqui, estamos interessados apenas na primeira planilha, mas você pode trabalhar com qualquer planilha especificando o índice correto.
## Etapa 4: Obtenha o primeiro objeto TextBox
Caixas de texto em uma planilha do Excel são consideradas objetos de desenho. A classe Aspose.Cells.Drawing.TextBox fornece propriedades e métodos para manipulá-las. Para acessar a primeira caixa de texto na planilha, você simplesmente consulta o`TextBoxes` coleção por índice.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Isso recupera o primeiro objeto de caixa de texto do`TextBoxes` coleção. Se sua planilha não tiver uma caixa de texto nesse índice, ela lançará uma exceção, então sempre garanta que o índice seja válido.
## Etapa 5: recuperar texto da primeira caixa de texto
 Após acessar a caixa de texto, você pode extrair o texto que ela contém usando o`.Text` propriedade.
```csharp
string text0 = textbox0.Text;
```
 Isso irá capturar o texto da primeira caixa de texto para a`text0` string. Agora você pode exibi-la, manipulá-la ou processá-la em seu aplicativo.
## Etapa 6: Acesse o segundo objeto TextBox
Para manipular várias caixas de texto, podemos recuperar caixas adicionais da planilha. Aqui, acessaremos a segunda caixa de texto de forma semelhante à primeira:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Novamente, acessamos a segunda caixa de texto usando o índice 1 do`TextBoxes`coleção.
## Etapa 7: recuperar texto da segunda caixa de texto
Assim como na primeira caixa de texto, você pode recuperar o texto da segunda caixa de texto e armazená-lo em uma string:
```csharp
string text1 = textbox1.Text;
```
Isso capturará o texto atual da segunda caixa de texto.
## Etapa 8: Modifique o texto na segunda caixa de texto
 Agora, digamos que você queira modificar o texto dentro da segunda caixa de texto. Você pode fazer isso facilmente atribuindo uma nova string à`.Text` propriedade do objeto caixa de texto.
```csharp
textbox1.Text = "This is an alternative text";
```
Isso altera o texto dentro da segunda caixa de texto para o novo conteúdo. Você pode inserir qualquer texto aqui com base em suas necessidades.
## Etapa 9: Salve o arquivo Excel atualizado
 Finalmente, depois de modificar as caixas de texto, é hora de salvar suas alterações. Aspose.Cells permite que você salve a pasta de trabalho modificada usando o`.Save()` método. Você pode especificar um novo nome de arquivo ou substituir o arquivo existente.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Isso salvará o arquivo Excel modificado no seu caminho de saída designado. Agora, quando você abrir o arquivo Excel, verá as alterações que fez nas caixas de texto.
## Conclusão
E aí está! Você acabou de aprender como manipular caixas de texto no Excel usando o Aspose.Cells para .NET. Não importa se você está automatizando a geração de relatórios, personalizando planilhas do Excel ou criando conteúdo dinâmico, o Aspose.Cells facilita o controle de todos os aspectos dos seus arquivos do Excel programaticamente. Da extração e modificação de texto até salvar os arquivos atualizados, esta biblioteca é uma ferramenta poderosa para desenvolvedores que trabalham com o Excel em ambientes .NET.
## Perguntas frequentes
### Posso manipular outros objetos de desenho com Aspose.Cells além de caixas de texto?
Sim, o Aspose.Cells permite que você manipule outros objetos de desenho, como formas, gráficos e imagens.
### O que acontece se eu tentar acessar uma caixa de texto que não existe?
 Se o índice da caixa de texto estiver fora do intervalo, um`IndexOutOfRangeException` será jogado.
### Posso adicionar novas caixas de texto a uma planilha do Excel com o Aspose.Cells?
 Sim, o Aspose.Cells permite que você adicione novas caixas de texto usando o`AddTextBox` método.
### Preciso de uma licença para usar o Aspose.Cells?
 Sim, você precisará comprar uma licença, mas a Aspose também oferece uma[teste gratuito](https://releases.aspose.com/).
### Posso usar o Aspose.Cells com outras linguagens de programação além de C#?
Sim, o Aspose.Cells pode ser usado com qualquer linguagem suportada pelo .NET, como o VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
