---
title: Utiliser des types anonymes avec des marqueurs intelligents Aspose.Cells
linktitle: Utiliser des types anonymes avec des marqueurs intelligents Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment utiliser des types anonymes avec des marqueurs intelligents dans Aspose.Cells pour générer des rapports Excel dynamiques dans .NET. Suivez notre guide simple.
weight: 17
url: /fr/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utiliser des types anonymes avec des marqueurs intelligents Aspose.Cells

## Introduction
Aspose.Cells est un outil puissant pour générer des rapports Excel dynamiques dans des applications .NET. L'une de ses meilleures fonctionnalités est la possibilité de travailler avec des marqueurs intelligents et des types anonymes. Si vous êtes novice dans ce domaine, ne vous inquiétez pas ! Ce guide vous expliquera tout ce que vous devez savoir, des prérequis aux exemples pratiques, tout en restant engageant et facile à suivre.
## Prérequis
Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour exécuter correctement les exemples de ce didacticiel.
### 1. Environnement .NET
Assurez-vous que vous disposez d'un environnement .NET fonctionnel configuré sur votre machine locale. Vous pouvez utiliser Visual Studio ou tout autre IDE de votre choix.
### 2. Bibliothèque Aspose.Cells
 Vous aurez besoin de la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore téléchargée, vous pouvez facilement la trouver[ici](https://releases.aspose.com/cells/net/) . Vous pouvez également l'essayer avec un essai gratuit disponible sur[ce lien](https://releases.aspose.com/).
### 3. Connaissances de base de C#
Une compréhension fondamentale de la programmation C# vous aidera à parcourir le didacticiel plus facilement. Si des termes tels que classes, objets et propriétés vous sont familiers, vous êtes prêt !
## Paquets d'importation
Pour utiliser la bibliothèque Aspose.Cells dans votre projet, vous devez importer les espaces de noms associés. Ajoutez les directives using suivantes en haut de votre fichier C# :
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Ces espaces de noms vous donneront accès à toutes les classes et méthodes nécessaires qui seront abordées plus tard.
Passons maintenant au cœur du tutoriel ! Vous verrez comment créer un fichier Excel avec des marqueurs intelligents à l'aide d'une classe personnalisée. Ne vous inquiétez pas, nous allons tout décomposer en étapes faciles à gérer !
## Étape 1 : Créer une classe personnalisée
Tout d’abord, nous avons besoin d’une classe simple pour représenter les données que nous voulons ajouter à notre fichier Excel. Cette classe contiendra des informations sur une personne.
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
 Ici, nous définissons une classe appelée`Person` avec deux propriétés,`Name` et`Age`. Le constructeur initialise ces propriétés. 
## Étape 2 : Configurer le concepteur de classeurs
 Ensuite, créons une instance de`WorkbookDesigner`classe, que nous utiliserons pour concevoir notre fichier Excel avec des marqueurs intelligents.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Instanciez l’objet concepteur de classeur.
WorkbookDesigner report = new WorkbookDesigner();
```
 Remplacer`"Your Document Directory"` avec votre chemin de fichier réel où vous souhaitez enregistrer le fichier Excel.`WorkbookDesigner` la classe est le cœur de cette opération, où vous définissez votre modèle.
## Étape 3 : ajouter des marqueurs aux cellules
Nous devons maintenant ajouter des marqueurs intelligents à la feuille de calcul. Ces marqueurs serviront d'espaces réservés aux données que nous saisirons plus tard.
```csharp
// Prenez la première feuille de travail du classeur.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Entrez des marqueurs dans les cellules.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Nous désignons la première feuille de calcul et définissons les valeurs des cellules d'en-tête. Les marqueurs intelligents sont préfixés par`&=` qui indique à Aspose qu'il s'agit d'espaces réservés pour les données à insérer ultérieurement.
## Étape 4 : Créer une liste de personnes
 Créons maintenant une liste de personnes utilisant notre`Person` classe que nous utiliserons pour remplir les marqueurs intelligents.
```csharp
// Instanciez la collection de listes en fonction de la classe personnalisée.
IList<Person> list = new List<Person>();
// Fournissez des valeurs pour les marqueurs à l’aide de l’objet de classe personnalisé.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Nous créons une liste et ajoutons des instances de`Person`à cela. Cette liste sert de source de données lors du remplissage du modèle Excel.
## Étape 5 : définir la source de données et les marqueurs de processus
 Une fois notre liste prête, nous devons la définir comme source de données pour notre`WorkbookDesigner` instance et ensuite traiter les marqueurs.
```csharp
// Définir la source de données.
report.SetDataSource("MyProduct", list);
// Traiter les marqueurs.
report.Process(false);
```
 Le`SetDataSource` La méthode relie notre liste précédemment définie aux marqueurs.`Process` La méthode remplace les marqueurs intelligents du classeur par les valeurs réelles de nos objets.
## Étape 6 : Enregistrez le fichier Excel
Enfin, nous enregistrerons le classeur modifié dans notre répertoire désigné.
```csharp
// Enregistrez le fichier Excel.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Cette ligne enregistre le classeur dans le chemin de fichier spécifié. Vous pouvez ouvrir ce fichier avec Excel pour voir les données insérées.
## Conclusion
Et voilà ! Vous avez réussi à créer un fichier Excel à l'aide de marqueurs intelligents dans Aspose.Cells avec votre propre classe personnalisée. Cette méthode rend non seulement votre gestion des données plus dynamique, mais maintient également votre code propre et organisé.
Ainsi, que vous génériez des rapports à des fins d'analyse, de suivi d'informations ou toute autre tâche liée aux données, les marqueurs intelligents sont votre allié pour rendre les rapports Excel plus gérables et flexibles !
## FAQ
### Que sont les marqueurs intelligents dans Aspose.Cells ?
Les marqueurs intelligents sont des espaces réservés spéciaux dans votre document Excel qui vous permettent d'insérer dynamiquement des données pendant l'exécution.
### Puis-je utiliser des types anonymes pour les marqueurs intelligents ?
Oui ! Les marqueurs intelligents peuvent être utilisés avec n'importe quel type d'objet, y compris les types anonymes, à condition qu'ils correspondent à la structure de données attendue.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
Aspose.Cells est un produit payant, mais vous pouvez commencer par un essai gratuit pour explorer ses fonctionnalités.
### Quels formats de fichiers Aspose.Cells prend-il en charge ?
Il prend en charge une large gamme de formats de fichiers, notamment XLS, XLSX, CSV, etc.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
 Pour plus de détails, consultez le[documentation](https://reference.aspose.com/cells/net/) ou visitez le[Forum de soutien](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
