---
title: Adicionar um botão à planilha no Excel
linktitle: Adicionar um botão à planilha no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar um botão a uma planilha do Excel usando Aspose.Cells for .NET com este tutorial passo a passo. Aprimore planilhas do Excel com botões interativos.
weight: 12
url: /pt/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar um botão à planilha no Excel

## Introdução
As planilhas do Excel são versáteis e comumente usadas para gerenciar dados, mas às vezes precisam de interatividade adicional. Uma das melhores maneiras de aprimorar a experiência do usuário é adicionando botões a uma planilha. Esses botões podem disparar macros ou navegar os usuários para links úteis. Se você é um desenvolvedor .NET trabalhando com arquivos do Excel, o Aspose.Cells for .NET fornece uma maneira fácil de manipular pastas de trabalho do Excel programaticamente, incluindo a adição de botões.
Neste tutorial, vamos orientá-lo no processo de adicionar um botão a uma planilha no Excel usando o Aspose.Cells for .NET. Abordaremos todos os detalhes, desde a configuração dos pré-requisitos até as instruções passo a passo. Vamos mergulhar!
## Pré-requisitos
Antes de poder seguir este tutorial, certifique-se de ter as seguintes ferramentas e pacotes instalados:
-  Biblioteca Aspose.Cells para .NET: Você pode baixá-la em[aqui](https://releases.aspose.com/cells/net/).
- Ambiente de desenvolvimento .NET: certifique-se de ter um ambiente .NET funcional, como o Visual Studio, instalado.
- Noções básicas de programação em C#: você deve estar familiarizado com os conceitos básicos de programação em C#.
-  Licença: Você precisará de uma licença válida. Se você não tiver uma, você pode obter uma[teste gratuito](https://releases.aspose.com/) ou solicitar um[licença temporária](https://purchase.aspose.com/temporary-license/).
Vamos prosseguir com a importação dos pacotes necessários.
## Pacotes de importação
Antes de começar a codificar, você precisará importar os pacotes necessários para seu projeto .NET. Aqui está um trecho de código simples para ajudar você a importar Aspose.Cells para seu projeto:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Agora que importamos os pacotes necessários, vamos dividir o exemplo em um guia passo a passo detalhado.
## Etapa 1: Configurar a pasta de trabalho e a planilha
Nesta primeira etapa, criaremos uma nova pasta de trabalho do Excel e obteremos uma referência para a primeira planilha.
```csharp
// Defina o caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Crie uma nova pasta de trabalho.
Workbook workbook = new Workbook();
// Obtenha a primeira planilha na pasta de trabalho.
Worksheet sheet = workbook.Worksheets[0];
```

-  Criação da pasta de trabalho: Começamos criando uma nova`Workbook` objeto, que representa um arquivo Excel.
-  Referência da planilha: A`Worksheets[0]` O comando recupera a primeira planilha na pasta de trabalho, que iremos modificar.
Esta etapa define a base criando um arquivo Excel em branco com uma única planilha.
## Etapa 2: Adicionar um botão à planilha
Em seguida, adicionaremos um botão à planilha. É aqui que a mágica acontece!
```csharp
// Adicione um novo botão à planilha.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- Método AddButton: Este método adiciona um botão em um local especificado na planilha. Os parâmetros definem a posição do botão (linha, coluna, deslocamento x, deslocamento y) e o tamanho (altura, largura).
- Linha e coluna: o botão é colocado na linha 2 e na coluna 0, sem deslocamento adicional.
- Tamanho: A altura do botão é definida como 28 e a largura como 80.
Esta etapa adiciona com sucesso um botão à planilha, mas ainda não terminamos — vamos personalizá-lo.
## Etapa 3: Definir propriedades do botão
Agora é hora de personalizar a aparência do botão definindo seu texto, fonte e posicionamento.
```csharp
// Defina a legenda do botão.
button.Text = "Aspose";
// Defina o Tipo de Posicionamento, a maneira como o Botão é anexado às células.
button.Placement = PlacementType.FreeFloating;
```

- Texto: Definimos a legenda do botão como “Aspose”.
-  Posicionamento: definimos como o botão é posicionado em relação às células da planilha.`FreeFloating` permite que o botão se mova independentemente das células.
Esta etapa personaliza a legenda e o posicionamento do botão.
## Etapa 4: personalize a fonte do botão
Vamos dar um toque especial ao botão personalizando as propriedades da fonte.
```csharp
// Defina o nome da fonte.
button.Font.Name = "Tahoma";
// Defina a sequência de caracteres da legenda em negrito.
button.Font.IsBold = true;
// Defina a cor como azul.
button.Font.Color = Color.Blue;
```

- Nome da fonte: Mudamos a fonte para "Tahoma", que é uma fonte limpa e moderna.
- Negrito: colocamos o texto do botão em negrito para dar ênfase.
- Cor: A cor da fonte é definida como azul, fazendo com que o texto do botão se destaque.
Esta etapa melhora a aparência do botão, garantindo que ele seja funcional e visualmente atraente.
## Etapa 5: adicione um hiperlink ao botão
Você pode tornar o botão ainda mais útil adicionando um hiperlink.
```csharp
// Defina o hiperlink para o botão.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink: Usamos esse método para adicionar um hyperlink clicável ao botão. Quando clicado, o botão navegará para o site Aspose.
Esta etapa adiciona interatividade ao botão, tornando-o funcional além da mera estética.
## Etapa 6: Salve o arquivo Excel
Depois que tudo estiver configurado, não se esqueça de salvar suas alterações!
```csharp
// Salva o arquivo.
workbook.Save(dataDir + "book1.out.xls");
```

-  Método de salvamento: Usamos o`Save` método para gravar a pasta de trabalho modificada em um novo arquivo. O arquivo será salvo no diretório especificado.
Parabéns! Você adicionou um botão totalmente personalizado a uma planilha do Excel.
## Conclusão
Adicionar botões às planilhas do Excel pode melhorar muito a funcionalidade das suas planilhas, tornando-as mais interativas e fáceis de usar. Com o Aspose.Cells para .NET, você pode conseguir isso com apenas algumas linhas de código, como mostramos neste tutorial.
Aspose.Cells para .NET é uma biblioteca poderosa que fornece infinitas possibilidades para manipulação do Excel. Não importa se você está automatizando tarefas ou adicionando novos recursos às suas planilhas, esta biblioteca é sua solução preferida.
 Se você ainda não fez isso,[baixe a biblioteca Aspose.Cells para .NET](https://releases.aspose.com/cells/net/) e comece a aprimorar seus arquivos do Excel.
## Perguntas frequentes
### Posso usar outras formas além de botões no Aspose.Cells para .NET?
Sim, o Aspose.Cells permite que você adicione várias formas, incluindo caixas de seleção, botões de opção e muito mais.
### Posso acionar uma macro a partir de um botão adicionado por meio do Aspose.Cells?
Sim, você pode vincular o botão a uma macro, embora precise manipular o código da macro separadamente no Excel.
### Como posso fazer o botão redimensionar automaticamente com as células?
 Use o`PlacementType.Move` propriedade para permitir que o botão seja redimensionado com as células.
### É possível adicionar vários botões em uma única planilha?
 Claro! Você pode adicionar quantos botões precisar chamando o`AddButton` método várias vezes.
### Posso personalizar ainda mais a aparência do botão?
Sim, você pode modificar muitas propriedades, incluindo a cor de fundo, o estilo da borda e muito mais.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
