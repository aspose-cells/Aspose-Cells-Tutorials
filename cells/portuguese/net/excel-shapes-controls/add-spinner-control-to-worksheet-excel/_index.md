---
title: Adicionar controle Spinner à planilha no Excel
linktitle: Adicionar controle Spinner à planilha no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar um controle Spinner a uma planilha do Excel usando o Aspose.Cells para .NET neste tutorial passo a passo.
weight: 23
url: /pt/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar controle Spinner à planilha no Excel

## Introdução
Se você está mergulhando no mundo da automação do Excel usando .NET, provavelmente já se deparou com a necessidade de controles mais interativos em suas planilhas. Um desses controles é o Spinner, que permite aos usuários incrementar ou decrementar um valor facilmente. Neste tutorial, exploraremos como adicionar um controle Spinner a uma planilha do Excel usando Aspose.Cells para .NET. Vamos dividi-lo em etapas digeríveis para que você possa acompanhar perfeitamente. 
## Pré-requisitos
Antes de começarmos o código, vamos garantir que você tenha tudo configurado para uma experiência tranquila:
1.  Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells. Se você ainda não a instalou, você pode obter a versão mais recente do[link para download](https://releases.aspose.com/cells/net/).
2. Visual Studio: você deve ter uma instalação funcional do Visual Studio ou qualquer outro IDE .NET de sua preferência.
3. Conhecimento básico de C#: Familiaridade com programação em C# ajudará você a entender os trechos de código facilmente. Se você está apenas começando, não se preocupe! Eu vou te guiar por cada parte.
## Pacotes de importação
Para usar Aspose.Cells no seu projeto, você precisa importar os namespaces necessários. Veja como você pode configurar seu ambiente:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Esses namespaces permitem que você acesse as principais funcionalidades do Aspose.Cells, incluindo manipulação de pastas de trabalho e recursos de desenho para formas como o Spinner.
Agora que cobrimos os pré-requisitos e importamos os pacotes necessários, vamos mergulhar no guia passo a passo. Cada passo é projetado para ser claro e conciso para que você possa implementá-lo facilmente.
## Etapa 1: configure seu diretório de projeto
Antes de começar a codificar, é uma boa prática organizar seus arquivos. Vamos criar um diretório para nossos arquivos Excel.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Aqui, especificamos um caminho para nosso diretório de documentos. Se o diretório não existir, nós o criamos. Isso garante que todos os nossos arquivos gerados tenham um home designado.
## Etapa 2: Crie uma nova pasta de trabalho
Agora é hora de criar uma pasta de trabalho do Excel onde adicionaremos nosso controle Spinner.
```csharp
// Instanciar uma nova pasta de trabalho.
Workbook excelbook = new Workbook();
```
 O`Workbook` class representa um arquivo Excel. Ao instanciá-lo, criamos uma nova pasta de trabalho pronta para modificações.
## Etapa 3: Acesse a primeira planilha
Adicionaremos nosso Spinner à primeira planilha da pasta de trabalho.
```csharp
// Obtenha a primeira planilha.
Worksheet worksheet = excelbook.Worksheets[0];
```
Esta linha acessa a primeira planilha (índice 0) da nossa pasta de trabalho. Você pode ter várias planilhas, mas para este exemplo, vamos manter a simplicidade.
## Etapa 4: Trabalhar com células
Em seguida, vamos trabalhar com as células em nossa planilha. Definiremos alguns valores e estilos.
```csharp
// Obtenha as células da planilha.
Cells cells = worksheet.Cells;
// Insira um valor de string na célula A1.
cells["A1"].PutValue("Select Value:");
// Defina a cor da fonte da célula.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Defina a fonte do texto como negrito.
cells["A1"].GetStyle().Font.IsBold = true;
// Insira o valor na célula A2.
cells["A2"].PutValue(0);
```
Aqui, estamos preenchendo a célula A1 com um prompt, aplicando uma cor vermelha e deixando o texto em negrito. Também definimos a célula A2 para um valor inicial de 0, que será vinculado ao nosso Spinner.
## Etapa 5: estilize a célula A2
Em seguida, vamos aplicar alguns estilos à célula A2 para torná-la mais atraente visualmente.
```csharp
// Defina a cor do sombreamento como preto com fundo sólido.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Defina a cor da fonte da célula.
cells["A2"].GetStyle().Font.Color = Color.White;
// Defina a fonte do texto como negrito.
cells["A2"].GetStyle().Font.IsBold = true;
```
Estamos adicionando um fundo preto com um padrão sólido à célula A2 e definindo a cor da fonte como branca. Esse contraste fará com que ela se destaque na planilha.
## Etapa 6: adicione o controle Spinner
Agora, estamos prontos para adicionar o controle Spinner à nossa planilha.
```csharp
// Adicione um controle giratório.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Esta linha adiciona um controle Spinner à planilha. Os parâmetros especificam a posição e o tamanho do Spinner (linha, coluna, largura, altura).
## Etapa 7: Configurar as propriedades do Spinner
Vamos personalizar o comportamento do Spinner para atender às nossas necessidades.
```csharp
// Defina o tipo de posicionamento do spinner.
spinner.Placement = PlacementType.FreeFloating;
// Defina a célula vinculada para o controle.
spinner.LinkedCell = "A2";
// Defina o valor máximo.
spinner.Max = 10;
//Defina o valor mínimo.
spinner.Min = 0;
// Defina a alteração de incremento para o controle.
spinner.IncrementalChange = 2;
// Defina o sombreamento 3D.
spinner.Shadow = true;
```
Aqui, definimos as propriedades do Spinner. Nós o vinculamos à célula A2, permitindo que ele controle o valor exibido ali. Os valores mínimo e máximo definem o intervalo em que o Spinner pode trabalhar, enquanto a alteração incremental define o quanto o valor muda a cada clique. Adicionar sombreamento 3D dá a ele uma aparência polida.
## Etapa 8: Salve o arquivo Excel
Por fim, vamos salvar nossa pasta de trabalho do Excel com o Spinner incluído.
```csharp
// Salve o arquivo Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Este comando salva a pasta de trabalho no diretório especificado. Você pode alterar o nome do arquivo conforme necessário.
## Conclusão
aí está! Você adicionou com sucesso um controle Spinner a uma planilha do Excel usando o Aspose.Cells para .NET. Este elemento interativo aprimora a experiência do usuário ao permitir ajustes rápidos nos valores. Não importa se você está criando uma ferramenta de relatório dinâmico ou um formulário de entrada de dados, o controle Spinner pode ser uma adição valiosa. 
## Perguntas frequentes
### O que é um controle Spinner no Excel?
Um controle Spinner permite que os usuários aumentem ou diminuam um valor numérico facilmente, fornecendo uma maneira intuitiva de fazer seleções.
### Posso personalizar a aparência do Spinner?
Sim, você pode modificar o tamanho, a posição e até mesmo o sombreamento 3D para uma aparência mais refinada.
### Preciso de uma licença para usar o Aspose.Cells?
 O Aspose.Cells oferece um teste gratuito, mas uma licença paga é necessária para uso em produção. Confira o[opções de compra](https://purchase.aspose.com/buy).
### Como posso obter ajuda com o Aspose.Cells?
 Para obter suporte, visite o[Fórum Aspose](https://forum.aspose.com/c/cells/9) onde você pode fazer perguntas e encontrar respostas.
### É possível adicionar vários Spinners à mesma planilha?
Claro! Você pode adicionar quantos Spinners forem necessários seguindo os mesmos passos para cada controle.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
