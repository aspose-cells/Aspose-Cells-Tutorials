---
"description": "Aprenda a adicionar uma caixa de combinação a uma planilha do Excel programaticamente usando o Aspose.Cells para .NET. Este guia passo a passo explica cada detalhe."
"linktitle": "Adicionar caixa de combinação à planilha no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Adicionar caixa de combinação à planilha no Excel"
"url": "/pt/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar caixa de combinação à planilha no Excel

## Introdução
Criar planilhas interativas do Excel pode aprimorar significativamente a experiência do usuário, especialmente quando você adiciona elementos de formulário, como caixas de combinação. As caixas de combinação permitem que os usuários selecionem opções de uma lista predefinida, adicionando facilidade e eficiência à entrada de dados. Com o Aspose.Cells para .NET, você pode criar caixas de combinação programadamente em planilhas do Excel sem precisar usar o Excel diretamente. Esta poderosa biblioteca permite que os desenvolvedores manipulem arquivos do Excel de diversas maneiras, incluindo a capacidade de automatizar controles de formulário.
Neste tutorial, mostraremos o processo de adição de uma caixa de combinação a uma planilha do Excel usando o Aspose.Cells para .NET. Se você deseja criar planilhas dinâmicas e fáceis de usar, este guia ajudará você a começar.
## Pré-requisitos
Antes de mergulharmos no código, vamos garantir que você tenha tudo o que precisa:
- Aspose.Cells para .NET: Baixe e instale a biblioteca Aspose.Cells para .NET do [página de download](https://releases.aspose.com/cells/net/).
- .NET Framework: Certifique-se de ter o .NET Framework instalado em sua máquina. Qualquer versão suportada pelo Aspose.Cells funcionará.
- Ambiente de desenvolvimento: use um IDE como o Visual Studio para gerenciar seu projeto e escrever código.
- Licença Aspose: Você pode trabalhar sem licença no modo de avaliação, mas para uma versão completa, você precisará aplicar uma licença. Obtenha uma [licença temporária](https://purchase.aspose.com/temporary-license/) se necessário.
## Pacotes de importação
Para começar, você precisa importar os namespaces necessários para o seu projeto. Veja o que você precisa:
```csharp
using System.IO;
using Aspose.Cells;
```
Eles são essenciais para interagir com arquivos do Excel e manipular elementos de formulário, como caixas de combinação na pasta de trabalho.
Vamos dividir o processo de adição de uma caixa de combinação em várias etapas simples para facilitar o entendimento.
## Etapa 1: Configurar o diretório de documentos
O primeiro passo é criar um diretório onde seus arquivos do Excel serão salvos. Você pode criar uma nova pasta, caso ela ainda não exista.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Crie um diretório se ele ainda não estiver presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Especifica o local onde o arquivo de saída será salvo.
- System.IO.Directory.Exists: Verifica se o diretório já existe.
- System.IO.Directory.CreateDirectory: Cria o diretório se ele estiver ausente.
## Etapa 2: Criar uma nova pasta de trabalho
Agora, crie uma nova pasta de trabalho do Excel onde você adicionará a caixa de combinação.

```csharp
// Crie uma nova pasta de trabalho.
Workbook workbook = new Workbook();
```

- Pasta de trabalho pasta de trabalho: Inicializa uma nova instância da classe Workbook, representando um arquivo do Excel.
## Etapa 3: Obtenha a planilha e as células
Em seguida, acesse a primeira planilha da pasta de trabalho e recupere o conjunto de células onde você irá inserir os dados.

```csharp
// Obtenha a primeira planilha.
Worksheet sheet = workbook.Worksheets[0];
// Obtenha a coleção de células da planilha.
Cells cells = sheet.Cells;
```

- Planilha: busca a primeira planilha da pasta de trabalho.
- Células células: Obtém o conjunto de células da planilha.
## Etapa 4: valores de entrada para caixa de combinação
Agora, precisamos inserir alguns valores nas células. Esses valores servirão como opções para a caixa de combinação.

```csharp
// Insira um valor.
cells["B3"].PutValue("Employee:");
// Coloque em negrito.
cells["B3"].GetStyle().Font.IsBold = true;
// Insira alguns valores que indiquem o intervalo de entrada para a caixa de combinação.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: Coloca o rótulo "Funcionário" na célula B3.
- Font.IsBold = true: Define o texto como negrito para destacá-lo.
- Intervalo de entrada: insira vários IDs de funcionários nas células A2 a A7. Eles aparecerão no menu suspenso da caixa de combinação.
## Etapa 5: adicione a caixa de combinação à planilha
O próximo passo é adicionar o controle de caixa de combinação à sua planilha. Esta caixa de combinação permitirá que os usuários escolham um dos IDs de funcionário que você inseriu anteriormente.

```csharp
// Adicione uma nova caixa de combinação.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Adiciona uma nova caixa de combinação à planilha. Os números (2, 0, 2, 0, 22, 100) representam a posição e as dimensões da caixa de combinação.
## Etapa 6: vincule a caixa de combinação a uma célula e defina o intervalo de entrada
Para tornar a caixa de combinação funcional, precisamos vinculá-la a uma célula específica e definir o intervalo de células de onde ela extrairá suas opções.

```csharp
// Defina a célula vinculada.
comboBox.LinkedCell = "A1";
// Defina o intervalo de entrada.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: vincula a seleção da caixa de combinação à célula A1. O valor selecionado na caixa de combinação aparecerá nesta célula.
- InputRange: define o intervalo de células (A2:A7) que contém os valores que preencherão as opções da caixa de combinação.
## Etapa 7: personalize a aparência da caixa de combinação
Você pode personalizar ainda mais a caixa de combinação especificando o número de linhas suspensas e habilitando o sombreamento 3D para melhor estética.

```csharp
// Defina o número de linhas de lista exibidas na parte de lista da caixa de combinação.
comboBox.DropDownLines = 5;
// Defina a caixa de combinação com sombreamento 3D.
comboBox.Shadow = true;
```

- DropDownLines: controla quantas opções ficarão visíveis na caixa de combinação suspensa ao mesmo tempo.
- Sombra: adiciona um efeito de sombreamento 3D à caixa de combinação.
## Etapa 8: Ajustar automaticamente as colunas e salvar a pasta de trabalho
Por fim, vamos ajustar automaticamente as colunas para um layout limpo e salvar a pasta de trabalho.

```csharp
// Colunas de ajuste automático
sheet.AutoFitColumns();
// Salva o arquivo.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: ajusta automaticamente as larguras das colunas para caber no conteúdo.
- Salvar: salva a pasta de trabalho como um arquivo Excel no diretório especificado.

## Conclusão
Adicionar uma caixa de combinação às suas planilhas do Excel usando o Aspose.Cells para .NET é um processo simples que melhora significativamente a flexibilidade na entrada de dados. Ao criar controles de formulário programaticamente, você pode criar planilhas interativas com facilidade. Este tutorial mostrou como adicionar uma caixa de combinação, vinculá-la a uma célula e configurar seu intervalo de entrada, tudo usando o Aspose.Cells.
O Aspose.Cells oferece uma ampla gama de recursos para manipulação de arquivos do Excel, tornando-o a escolha ideal para desenvolvedores que buscam automatizar tarefas em planilhas. Experimente com um [teste gratuito](https://releases.aspose.com/).
## Perguntas frequentes
### Posso usar o Aspose.Cells sem o Excel instalado?
Sim, o Aspose.Cells funciona independentemente do Excel e não requer que o Excel seja instalado.
### Como aplico uma licença no Aspose.Cells?
Você pode solicitar uma licença obtendo-a em [aqui](https://purchase.aspose.com/buy) e chamando `License.SetLicense()` no seu código.
### Quais formatos o Aspose.Cells suporta para salvar arquivos?
O Aspose.Cells suporta salvar arquivos em vários formatos, como XLSX, XLS, CSV, PDF e muito mais.
### Existe um limite para o número de caixas de combinação que posso adicionar?
Não, não há um limite estrito; você pode adicionar quantas caixas de combinação seu projeto exigir.
### Como obtenho suporte para o Aspose.Cells?
Você pode obter suporte do [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}