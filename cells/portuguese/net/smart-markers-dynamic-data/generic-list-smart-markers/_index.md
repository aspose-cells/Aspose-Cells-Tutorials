---
title: Use a lista genérica em marcadores inteligentes Aspose.Cells
linktitle: Use a lista genérica em marcadores inteligentes Aspose.Cells
second_title: API de processamento do Aspose.Cells .NET Excel
description: Domine o Aspose.Cells para .NET com Listas Genéricas e Marcadores Inteligentes para criar relatórios dinâmicos do Excel sem esforço. Guia fácil para desenvolvedores.
weight: 20
url: /pt/net/smart-markers-dynamic-data/generic-list-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Use a lista genérica em marcadores inteligentes Aspose.Cells

## Introdução
Criar relatórios dinâmicos e aplicativos orientados a dados é uma habilidade essencial no cenário tecnológico atual. Se você trabalha com arquivos .NET e Excel, provavelmente já ouviu falar do Aspose.Cells, uma biblioteca poderosa projetada especificamente para manipular planilhas do Excel programaticamente. Este guia abrangente o guiará pela utilização de Listas Genéricas com Marcadores Inteligentes no Aspose.Cells, fornecendo uma abordagem passo a passo para otimizar o tratamento de dados em seus aplicativos.
## Pré-requisitos
Antes de mergulhar no código, vamos rever rapidamente o que você precisa:
### Conhecimento básico de C#
Você deve ter um entendimento básico de C# e como trabalhar com classes e objetos. Se você é animado com programação orientada a objetos, você já está no caminho certo.
### Aspose.Cells para .NET instalado
 Certifique-se de ter o Aspose.Cells instalado no seu projeto .NET. Você pode baixar a biblioteca do[Site Aspose](https://releases.aspose.com/cells/net/). 
### Ambiente do Visual Studio
Ter o Visual Studio instalado na sua máquina é crucial. É o ambiente de desenvolvimento mais comum onde você escreverá seu código C#.
### Um arquivo de modelo
Para este tutorial, usaremos um modelo simples do Excel que você pode configurar com antecedência. Você só precisará de uma pasta de trabalho em branco para a demonstração.
## Pacotes de importação
Agora que temos o essencial no lugar, vamos começar importando os pacotes necessários. Uma boa regra prática é incluir o seguinte namespace:
```csharp
using System.IO;
using Aspose.Cells;
using System;
using System.Drawing;
using System.Collections.Generic;
```
Esses namespaces fornecerão as funcionalidades necessárias para trabalhar com arquivos do Excel e estilizar células.
## Etapa 1: Defina suas classes
Primeiro as coisas mais importantes! Precisamos definir nosso`Person` e`Teacher` aulas. Veja como:
### Defina a classe Pessoa
 O`Person` a classe terá atributos básicos como nome e idade.
```csharp
public class Person
{
    int _age;
    string _name;
    
    public int Age
    {
        get { return _age; }
        set { _age = value; }
    }
    
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
    
    public Person(string name, int age)
    {
        _age = age;
        _name = name;
    }
}
```
### Defina a classe do professor
 O próximo é o`Teacher` classe, que herda da`Person` classe. Esta classe encapsulará ainda mais uma lista de alunos.
```csharp
public class Teacher : Person
{
    private IList<Person> m_students;
    public IList<Person> Students
    {
        get { return m_students; }
        set { m_students = value; }
    }
    
    public Teacher(string name, int age) : base(name, age)
    {
        m_students = new List<Person>();
    }
}
```
## Etapa 2: inicializar a pasta de trabalho e criar um designer
Agora que temos nossas classes prontas, é hora de inicializar nossa pasta de trabalho:
```csharp
string dataDir = "Your Document Directory"; // Especifique seu diretório de documentos
Workbook workbook = new Workbook(); // Nova instância da pasta de trabalho
Worksheet worksheet = workbook.Worksheets[0];
```
## Etapa 3: Configurar marcadores inteligentes na planilha
Vamos configurar marcadores inteligentes na planilha do Excel, indicando onde nossos valores dinâmicos serão colocados.
```csharp
worksheet.Cells["A1"].PutValue("Teacher Name");
worksheet.Cells["A2"].PutValue("&=Teacher.Name");
worksheet.Cells["B1"].PutValue("Teacher Age");
worksheet.Cells["B2"].PutValue("&=Teacher.Age");
worksheet.Cells["C1"].PutValue("Student Name");
worksheet.Cells["C2"].PutValue("&=Teacher.Students.Name");
worksheet.Cells["D1"].PutValue("Student Age");
worksheet.Cells["D2"].PutValue("&=Teacher.Students.Age");
```
## Etapa 4: aplique estilo para aprimorar a apresentação
Qualquer bom relatório deve ser visualmente atraente! Vamos aplicar algum estilo aos nossos cabeçalhos:
```csharp
Range range = worksheet.Cells.CreateRange("A1:D1");
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
StyleFlag flag = new StyleFlag();
flag.All = true;
range.ApplyStyle(style, flag);
```
## Etapa 5: Crie as instâncias do professor e do aluno
 Agora, vamos criar instâncias do nosso`Teacher` e`Person` classes e preenchê-las com dados:
```csharp
System.Collections.Generic.List<Teacher> list = new System.Collections.Generic.List<Teacher>();
// Crie o primeiro objeto professor
Teacher h1 = new Teacher("Mark John", 30);
h1.Students = new List<Person>
{
    new Person("Chen Zhao", 14),
    new Person("Jamima Winfrey", 18),
    new Person("Reham Smith", 15)
};
//Crie o segundo objeto professor
Teacher h2 = new Teacher("Masood Shankar", 40);
h2.Students = new List<Person>
{
    new Person("Karishma Jathool", 16),
    new Person("Angela Rose", 13),
    new Person("Hina Khanna", 15)
};
// Adicionar à lista
list.Add(h1);
list.Add(h2);
```
## Etapa 6: Defina a fonte de dados para o designer
Agora precisamos vincular nossos dados com a planilha que preparamos. 
```csharp
WorkbookDesigner designer = new WorkbookDesigner();
designer.Workbook = workbook;
designer.SetDataSource("Teacher", list);
```
## Etapa 7: Processe os marcadores
O próximo passo é processar todos os marcadores inteligentes que colocamos anteriormente:
```csharp
designer.Process();
```
## Etapa 8: Ajustar automaticamente as colunas e salvar a pasta de trabalho
Para garantir que tudo pareça profissional, vamos ajustar automaticamente as colunas e salvar nossa pasta de trabalho:
```csharp
worksheet.AutoFitColumns();
designer.Workbook.Save(dataDir + "output.xlsx"); // Salvar no diretório especificado
```
## Conclusão
E aí está! Você acabou de criar uma planilha do Excel dinamicamente, aproveitando o poder das Listas Genéricas e Marcadores Inteligentes com o Aspose.Cells para .NET. Essa habilidade permitirá que você crie relatórios complexos facilmente e incorpore funcionalidades orientadas a dados em seus aplicativos. Quer você esteja gerando relatórios escolares, análises de negócios ou qualquer conteúdo dinâmico, as técnicas neste guia ajudarão a simplificar seu fluxo de trabalho significativamente.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET para criar e gerenciar arquivos do Excel sem precisar instalar o Microsoft Excel.
### Posso usar o Aspose.Cells para outros formatos de arquivo?
Sim! O Aspose oferece bibliotecas para PDF, Word e outros formatos, tornando-o versátil para gerenciamento de documentos.
### Preciso de uma licença para usar o Aspose.Cells?
 Você pode começar com um teste gratuito em[aqui](https://releases.aspose.com/), mas uma licença paga é necessária para uso em produção.
### O que são marcadores inteligentes?
Marcadores inteligentes são marcadores de posição em modelos do Excel que são substituídos por dados reais quando processados pelo Aspose.Cells.
### Aspose.Cells é adequado para grandes conjuntos de dados?
Absolutamente! O Aspose.Cells é otimizado para desempenho, tornando-o capaz de manipular grandes conjuntos de dados de forma eficiente.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
