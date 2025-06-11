---
"description": "Aprenda a desagrupar linhas e colunas no Excel usando o Aspose.Cells para .NET com este guia completo. Simplifique a manipulação de dados no Excel."
"linktitle": "Desagrupar linhas e colunas no Excel com Aspose.Cells"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Desagrupar linhas e colunas no Excel com Aspose.Cells"
"url": "/pt/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Desagrupar linhas e colunas no Excel com Aspose.Cells

## Introdução
Ao lidar com arquivos do Excel, você pode se deparar com situações em que precisa desagrupar linhas e colunas. Seja para limpar uma planilha ou reformatar dados para melhor apresentação, o Aspose.Cells para .NET é uma ferramenta fantástica que simplifica o processo. Neste tutorial, guiarei você pelas etapas para desagrupar linhas e colunas no Excel usando o Aspose.Cells. Ao final, você terá uma sólida compreensão de como trabalhar com arquivos do Excel programaticamente.
## Pré-requisitos
Antes de mergulhar no código, vamos garantir que você tenha tudo configurado. Aqui está o que você precisa:
1. Visual Studio: Você deve ter uma versão funcional do Visual Studio instalada em sua máquina. Se ainda não a tiver, você pode baixá-la em [Site do Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells para .NET: Você precisará baixar a biblioteca Aspose.Cells. Você pode obtê-la em [Página de lançamentos da Aspose](https://releases.aspose.com/cells/net/)Certifique-se de ter as licenças necessárias, que podem ser adquiridas ou obtidas por meio de um [licença temporária](https://purchase.aspose.com/temporary-license/).
3. Conhecimento básico de C#: uma compreensão fundamental da programação em C# ajudará você a acompanhar mais facilmente.
Depois que tudo estiver pronto, podemos passar para a parte divertida: o código!
## Pacotes de importação
Para começar, você precisa importar os pacotes necessários para o seu projeto C#. Veja como fazer:
1. Abra seu projeto no Visual Studio.
2. Adicione uma referência à biblioteca Aspose.Cells. Você pode fazer isso clicando com o botão direito do mouse nas referências do seu projeto e selecionando Adicionar Referência. Navegue até o local onde você salvou a DLL Aspose.Cells.
3. No início do seu arquivo C#, adicione as seguintes diretivas using:
```csharp
using System.IO;
using Aspose.Cells;
```
Agora que tudo está configurado, vamos seguir as etapas para desagrupar linhas e colunas na sua planilha do Excel. 
## Etapa 1: definir o diretório de documentos
Primeiro, você precisa especificar o diretório onde seu arquivo Excel está localizado. Você pode configurá-lo da seguinte forma:
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```
Substituir `"Your Document Directory"` com o caminho real no seu computador onde o arquivo Excel foi salvo. 
## Etapa 2: Criar um fluxo de arquivos
Em seguida, você precisa criar um fluxo de arquivos para abrir o arquivo do Excel. Veja como fazer isso:
```csharp
// Criando um fluxo de arquivo contendo o arquivo Excel a ser aberto
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Aqui, você está abrindo o arquivo chamado `book1.xls`. Certifique-se de que esse arquivo existe no diretório especificado, caso contrário, você encontrará um erro de arquivo não encontrado.
## Etapa 3: Instanciar um objeto de pasta de trabalho
Agora, vamos carregar o arquivo do Excel em um objeto Workbook. Isso permite que você manipule a pasta de trabalho programaticamente:
```csharp
// Instanciando um objeto Workbook
// Abrindo o arquivo Excel através do fluxo de arquivos
Workbook workbook = new Workbook(fstream);
```
Com esta linha de código, você carregou com sucesso o arquivo do Excel na memória e está pronto para trabalhar com ele.
## Etapa 4: Acesse a planilha
Depois de ter a pasta de trabalho, o próximo passo é acessar a planilha específica onde você deseja desagrupar linhas e colunas. Veja como fazer isso:
```csharp
// Acessando a primeira planilha no arquivo Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Neste caso, estamos acessando a primeira planilha. Se seus dados estiverem em uma planilha diferente, você pode alterar o índice conforme necessário.
## Etapa 5: Desagrupar linhas
Agora vem a parte emocionante! Vamos desagrupar as seis primeiras linhas (da linha 0 à linha 5). Use o seguinte código:
```csharp
// Desagrupando as seis primeiras linhas (de 0 a 5)
worksheet.Cells.UngroupRows(0, 5);
```
Este método remove qualquer agrupamento aplicado às linhas especificadas. É simples assim!
## Etapa 6: Desagrupar colunas
Assim como as linhas, você também pode desagrupar colunas. Veja como desagrupar as três primeiras colunas (da coluna 0 para a coluna 2):
```csharp
// Desagrupando as três primeiras colunas (de 0 a 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Etapa 7: Salve o arquivo Excel modificado
Depois de desagrupar as linhas e colunas, o próximo passo é salvar as alterações em um arquivo do Excel. Você pode fazer isso usando o `Save` método:
```csharp
// Salvando o arquivo Excel modificado
workbook.Save(dataDir + "output.xls");
```
Neste exemplo, estamos salvando o arquivo modificado como `output.xls`. Você pode alterar o nome do arquivo para o que preferir.
## Etapa 8: Feche o fluxo de arquivos
Por fim, para liberar recursos, você deve fechar o fluxo de arquivos:
```csharp
// Fechando o fluxo de arquivos para liberar todos os recursos
fstream.Close();
```
Esta é uma boa prática para garantir que seu aplicativo não retenha os identificadores de arquivo por mais tempo do que o necessário.
## Conclusão
E pronto! Você aprendeu com sucesso a desagrupar linhas e colunas em um arquivo do Excel usando o Aspose.Cells para .NET. Com apenas algumas linhas de código, você pode fazer alterações significativas em seus arquivos do Excel programaticamente. Seja automatizando relatórios ou preparando dados para análise, dominar essas técnicas pode economizar muito tempo.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para trabalhar com arquivos do Excel em aplicativos .NET, permitindo fácil manipulação, conversão e criação de planilhas.
### Posso desagrupar linhas e colunas no Excel usando outras bibliotecas?
Sim, existem outras bibliotecas disponíveis para manipulação do Excel no .NET, mas o Aspose.Cells oferece recursos abrangentes e facilidade de uso.
### Existe uma maneira de desfazer alterações depois de salvar?
Depois de salvar um arquivo do Excel, o estado anterior não pode ser restaurado, a menos que você tenha um backup do arquivo original.
### Como obtenho suporte para o Aspose.Cells?
Você pode encontrar suporte visitando o [Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9), onde você pode fazer perguntas e encontrar soluções.
### Posso usar o Aspose.Cells sem uma licença?
Sim, você pode usar o Aspose.Cells gratuitamente com certas limitações e pode começar com um [licença temporária](https://purchase.aspose.com/temporary-license/) para funcionalidade completa.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}