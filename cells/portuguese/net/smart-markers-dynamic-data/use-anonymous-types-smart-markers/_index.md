---
title: Use tipos anônimos com marcadores inteligentes Aspose.Cells
linktitle: Use tipos anônimos com marcadores inteligentes Aspose.Cells
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a usar tipos anônimos com marcadores inteligentes no Aspose.Cells para geração dinâmica de relatórios do Excel no .NET. Siga nosso guia fácil.
weight: 17
url: /pt/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Use tipos anônimos com marcadores inteligentes Aspose.Cells

## Introdução
Quando se trata de gerar relatórios dinâmicos do Excel em aplicativos .NET, o Aspose.Cells se destaca como uma ferramenta poderosa. Um de seus melhores recursos é a capacidade de trabalhar com marcadores inteligentes e tipos anônimos. Se você é novo neste conceito, não se preocupe! Este guia detalhará tudo o que você precisa saber, desde pré-requisitos até exemplos práticos, tudo isso mantendo-o envolvente e fácil de seguir.
## Pré-requisitos
Antes de mergulharmos no código, vamos garantir que você tenha tudo o que precisa para executar sem problemas os exemplos neste tutorial.
### 1. Ambiente .NET
Certifique-se de ter um ambiente .NET funcional configurado em sua máquina local. Você pode usar o Visual Studio ou qualquer outro IDE de sua escolha.
### 2. Biblioteca Aspose.Cells
 Você precisará da biblioteca Aspose.Cells. Se você ainda não baixou, você pode encontrá-la facilmente[aqui](https://releases.aspose.com/cells/net/) . Você também pode experimentar com uma avaliação gratuita disponível em[este link](https://releases.aspose.com/).
### 3. Conhecimento básico de C#
Uma compreensão fundamental da programação em C# ajudará você a navegar pelo tutorial mais facilmente. Se termos como classes, objetos e propriedades são familiares para você, você está pronto para começar!
## Pacotes de importação
Para usar a biblioteca Aspose.Cells no seu projeto, você deve importar os namespaces relacionados. Adicione as seguintes diretivas using no topo do seu arquivo C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Esses namespaces darão acesso a todas as classes e métodos necessários que serão discutidos mais tarde.
Agora, vamos ao cerne do tutorial! Você verá como criar um arquivo Excel com marcadores inteligentes usando uma classe personalizada. Não se preocupe; vamos dividir tudo em etapas gerenciáveis!
## Etapa 1: Crie uma classe personalizada
Primeiro, precisamos de uma classe simples para representar os dados que queremos adicionar ao nosso arquivo Excel. Esta classe conterá informações sobre uma pessoa.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
 Aqui, estamos definindo uma classe chamada`Person` com duas propriedades,`Name` e`Age`. O construtor inicializa essas propriedades. 
## Etapa 2: Configurar o Workbook Designer
 Em seguida, vamos criar uma instância do`WorkbookDesigner`classe, que usaremos para projetar nosso arquivo Excel com marcadores inteligentes.
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Instanciar o objeto designer da pasta de trabalho.
WorkbookDesigner report = new WorkbookDesigner();
```
 Substituir`"Your Document Directory"` com o caminho real do arquivo onde você deseja salvar o arquivo Excel. O`WorkbookDesigner` class é o coração desta operação, onde você define seu modelo.
## Etapa 3: Adicionar marcadores às células
Agora, precisamos adicionar marcadores inteligentes à planilha. Esses marcadores serão marcadores de posição para os dados que inseriremos mais tarde.
```csharp
// Obtenha a primeira planilha na pasta de trabalho.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Insira alguns marcadores nas células.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Designamos a primeira planilha e definimos valores para as células de cabeçalho. Os marcadores inteligentes são prefixados com`&=` que informa ao Aspose que esses são espaços reservados para dados a serem inseridos posteriormente.
## Etapa 4: Crie uma lista de pessoas
 Agora vamos criar uma lista de pessoas usando nosso`Person` classe que usaremos para preencher os marcadores inteligentes.
```csharp
// Instancie a coleção de listas com base na classe personalizada.
IList<Person> list = new List<Person>();
// Forneça valores para os marcadores usando o objeto de classe personalizado.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Criamos uma lista e adicionamos instâncias de`Person`para ele. Esta lista serve como nossa fonte de dados ao preencher o modelo do Excel.
## Etapa 5: Definir fonte de dados e marcadores de processo
 Depois de termos nossa lista pronta, precisamos defini-la como a fonte de dados para nosso`WorkbookDesigner` instância e então processar os marcadores.
```csharp
// Defina a fonte de dados.
report.SetDataSource("MyProduct", list);
// Processe os marcadores.
report.Process(false);
```
 O`SetDataSource` método vincula nossa lista previamente definida aos marcadores. O`Process` O método substitui os marcadores inteligentes na pasta de trabalho pelos valores reais dos nossos objetos.
## Etapa 6: Salve o arquivo Excel
Por fim, salvaremos a pasta de trabalho modificada no diretório designado.
```csharp
// Salve o arquivo Excel.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Esta linha salva a pasta de trabalho no caminho de arquivo especificado. Você pode abrir este arquivo usando o Excel para ver os dados inseridos.
## Conclusão
E aí está! Você criou com sucesso um arquivo Excel usando marcadores inteligentes em Aspose.Cells com sua própria classe personalizada. Este método não só torna seu gerenciamento de dados mais dinâmico, mas também mantém seu código limpo e organizado.
Então, quer você esteja gerando relatórios para análise, rastreando informações ou qualquer outra tarefa relacionada a dados, os marcadores inteligentes são seus aliados para tornar os relatórios do Excel mais gerenciáveis e flexíveis!
## Perguntas frequentes
### O que são marcadores inteligentes no Aspose.Cells?
Marcadores inteligentes são marcadores de posição especiais no seu documento do Excel que permitem inserir dados dinamicamente durante o tempo de execução.
### Posso usar tipos anônimos para marcadores inteligentes?
Sim! Marcadores inteligentes podem ser usados com qualquer tipo de objeto, incluindo tipos anônimos, desde que correspondam à estrutura de dados esperada.
### O Aspose.Cells é gratuito?
Aspose.Cells é um produto pago, mas você pode começar com uma avaliação gratuita para explorar seus recursos.
### Quais formatos de arquivo o Aspose.Cells suporta?
Ele suporta uma ampla variedade de formatos de arquivo, incluindo XLS, XLSX, CSV e muito mais.
### Onde posso encontrar mais informações sobre o Aspose.Cells?
 Para mais detalhes, confira o[documentação](https://reference.aspose.com/cells/net/) ou visite o[fórum de suporte](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
