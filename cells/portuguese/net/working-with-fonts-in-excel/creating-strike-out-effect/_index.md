---
title: Criando efeito de riscado no texto no Excel
linktitle: Criando efeito de riscado no texto no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como aplicar um efeito de tachado no texto no Excel com o Aspose.Cells para .NET neste tutorial detalhado passo a passo.
weight: 15
url: /pt/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criando efeito de riscado no texto no Excel

## Introdução
Quando se trata do Excel, os elementos visuais são tão importantes quanto os dados em si. Quer você esteja destacando alterações importantes ou marcando itens que não são mais relevantes, o efeito de tachado no texto é uma maneira clássica de gerenciar a representação visual em planilhas. Neste guia, nós o guiaremos pelo processo de implementação de um efeito de tachado no texto no Excel usando o Aspose.Cells para .NET. Este tutorial não cobrirá apenas os pré-requisitos necessários, mas também fornecerá uma abordagem passo a passo para garantir que você possa replicar esse efeito com facilidade.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos atendidos:
1. Ambiente de desenvolvimento: Você deve ter um ambiente de desenvolvimento .NET configurado. Pode ser o Visual Studio ou qualquer outro IDE que você prefira que suporte desenvolvimento .NET.
2. Aspose.Cells para .NET: Certifique-se de ter o Aspose.Cells instalado em seu projeto. Você pode baixá-lo no seguinte link:[Baixar Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: Uma compreensão fundamental da programação em C# é útil, pois os exemplos serão codificados em C#.
4. .NET Framework: certifique-se de que seu projeto esteja direcionado a uma versão compatível do .NET Framework, geralmente .NET Core ou .NET Framework 4.5 e superior.
## Pacotes de importação
Antes de escrever qualquer código, você precisa importar os namespaces necessários do Aspose.Cells. Isso é crucial para acessar vários recursos fornecidos pela biblioteca. Veja como você pode importar os namespaces necessários:
```csharp
using System.IO;
using Aspose.Cells;
```
Com essas importações, você terá acesso às classes Workbook, Worksheet e Style que serão usadas neste tutorial.
Agora que definimos o cenário, vamos dividir o processo em etapas gerenciáveis. Cada etapa será acompanhada por instruções claras para guiá-lo na criação de um efeito de tachado no texto no Excel.
## Etapa 1: Defina o diretório do documento
Comece definindo o caminho onde seus documentos do Excel serão armazenados. Este será o local para salvar seus arquivos de saída.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho do diretório real onde você quer salvar seu arquivo Excel. Isso configura o diretório para sua saída.
## Etapa 2: Crie o diretório
Em seguida, você precisa garantir que o diretório especificado na etapa anterior exista. Se não existir, você pode criá-lo programaticamente.
```csharp
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este código verifica se o diretório existe e o cria, caso contrário. Isso ajuda a evitar erros quando você tenta salvar seu arquivo mais tarde.
## Etapa 3: Instanciar um objeto de pasta de trabalho
Agora, é hora de criar um novo objeto Workbook. Esta é a base do seu arquivo Excel onde você adicionará dados e aplicará formatos.
```csharp
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
```
 O`Workbook` class representa um arquivo Excel. Ao criar uma instância desta classe, você está essencialmente criando um novo documento Excel.
## Etapa 4: Adicionar uma nova planilha
Cada pasta de trabalho pode conter várias planilhas. Vamos em frente e criar uma nova planilha na sua pasta de trabalho.
```csharp
// Adicionar uma nova planilha ao objeto Excel
int i = workbook.Worksheets.Add();
```
 O`Add` método do`Worksheets` collection adiciona uma nova planilha à pasta de trabalho e retorna seu índice. 
## Etapa 5: Obtenha a referência da nova planilha
Depois de criar a planilha, você precisa referenciá-la para operações futuras.
```csharp
// Obtendo a referência da planilha recém-adicionada passando seu índice de planilha
Worksheet worksheet = workbook.Worksheets[i];
```
Aqui, você está buscando a planilha recém-criada usando seu índice (`i`). Isso lhe dá acesso para manipular a planilha.
## Etapa 6: Acesse uma célula
 Você vai querer acessar uma célula específica na sua planilha onde você aplicará o formato strikeout. Neste exemplo, estamos usando célula`A1`.
```csharp
// Acessando a célula "A1" da planilha
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 No Excel, as células são referenciadas por seus identificadores de coluna e linha (por exemplo, "A1"). Estamos obtendo uma referência à célula`A1` para posterior manipulação.
## Etapa 7: Adicionar valor à célula
 Em seguida, vamos inserir algum texto na célula. Vamos escrever “Hello Aspose!” na célula`A1`.
```csharp
// Adicionando algum valor à célula "A1"
cell.PutValue("Hello Aspose!");
```
 O`PutValue` O método é usado para atribuir um valor de string à célula. Você pode modificar essa string para qualquer coisa que você queira que seja exibida.
## Etapa 8: Obtenha o estilo da célula
Agora que temos texto em nossa célula, é hora de acessar o estilo da célula para aplicar a formatação desejada, incluindo o efeito de tachado.
```csharp
// Obtendo o estilo da célula
Style style = cell.GetStyle();
```
 O`GetStyle` O método recupera o estilo atual da célula, permitindo que você modifique propriedades como tipo de fonte, tamanho e efeitos.
## Etapa 9: Defina o efeito Strikeout
Vamos aplicar o efeito strikeout ao texto na célula. Modificaremos o estilo da fonte da célula.
```csharp
// ExStart:DefinirStrikeout
// Definindo o efeito de riscado na fonte
style.Font.IsStrikeout = true;
// ExEnd:DefinirStrikeout
```
 Ao definir`IsStrikeout` para verdadeiro, você está instruindo o Excel a riscar visualmente o texto na célula selecionada - como se estivesse marcando visualmente algo em uma lista.
## Etapa 10: aplique o estilo à célula
Depois de modificar o estilo, você precisa aplicá-lo novamente à célula para refletir as alterações.
```csharp
// Aplicando o estilo à célula
cell.SetStyle(style);
```
 O`SetStyle` O método atualiza a célula com o novo estilo, que agora inclui a formatação tachado.
## Etapa 11: Salve o arquivo Excel
 Finalmente, é hora de salvar sua pasta de trabalho no diretório especificado. Neste exemplo, estamos salvando o arquivo com o nome`book1.out.xls`.
```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 O`Save`método grava a pasta de trabalho no disco no formato Excel 97-2003. Você pode especificar formatos diferentes, se necessário.
## Conclusão
Criar um efeito de strikeout em texto no Excel usando Aspose.Cells para .NET é um processo direto quando você o divide passo a passo. Ao seguir este guia, você agora tem as habilidades para aprimorar suas planilhas com dicas visuais, tornando seus dados não apenas informativos, mas também visualmente envolventes.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para gerenciar arquivos do Excel em aplicativos .NET, permitindo que você crie, manipule e converta documentos do Excel programaticamente.
### Posso usar o Aspose.Cells gratuitamente?
 Sim, você pode usá-lo gratuitamente durante um período de teste. Um teste gratuito está disponível em[Aspose.Cells Teste grátis](https://releases.aspose.com/).
### Como faço para comprar o Aspose.Cells?
 Você pode comprar uma licença para Aspose.Cells através do site deles[Compre Aspose.Cells](https://purchase.aspose.com/buy).
### Há exemplos disponíveis para usar o Aspose.Cells?
 Sim, você pode encontrar muitos exemplos e trechos de código no[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/).
### Onde posso obter suporte para o Aspose.Cells?
 Você pode obter suporte e ajuda da comunidade[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
