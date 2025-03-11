---
title: Utilisation des formats de nombres intégrés dans Excel par programmation
linktitle: Utilisation des formats de nombres intégrés dans Excel par programmation
second_title: API de traitement Excel Aspose.Cells .NET
description: Automatisez la mise en forme des nombres dans Excel à l'aide d'Aspose.Cells pour .NET. Découvrez comment appliquer des formats de date, de pourcentage et de devise par programmation.
weight: 10
url: /fr/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utilisation des formats de nombres intégrés dans Excel par programmation

## Introduction
Dans ce didacticiel, nous vous expliquerons comment utiliser les formats numériques intégrés dans Excel à l'aide d'Aspose.Cells pour .NET. Nous aborderons tous les aspects, de la configuration de votre environnement à l'application de différents formats tels que les dates, les pourcentages et les devises. Que vous soyez un professionnel chevronné ou que vous débutiez dans l'écosystème .NET, ce guide vous permettra de formater des cellules Excel en un clin d'œil.
## Prérequis
Avant de vous lancer, assurez-vous d'avoir les éléments suivants :
-  Bibliothèque Aspose.Cells pour .NET installée. Vous pouvez[téléchargez-le ici](https://releases.aspose.com/cells/net/).
- Une connaissance pratique de C# et de la programmation .NET de base.
- Visual Studio ou tout autre IDE .NET installé sur votre machine.
-  Une licence Aspose valide ou[permis temporaire](https://purchase.aspose.com/temporary-license/).
- .NET framework installé (version 4.0 ou supérieure).
  
Si l'un des éléments ci-dessus vous manque, suivez les liens fournis pour tout configurer. Prêt ? Passons à la partie amusante !
## Paquets d'importation
Avant de commencer le didacticiel, assurez-vous d'importer les espaces de noms nécessaires pour travailler avec Aspose.Cells pour .NET :
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Une fois que vous avez importé ces éléments, vous êtes prêt à manipuler les fichiers Excel par programmation. Passons maintenant au guide étape par étape !
## Étape 1 : Créez ou accédez à votre classeur Excel
Dans cette étape, vous allez créer un nouveau classeur. Considérez cela comme l'ouverture d'un nouveau fichier Excel, sauf que vous le faites via du code !
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
```
 Ici, nous instancions simplement un nouveau`Workbook` objet. Il s'agit de votre fichier Excel, prêt pour la manipulation des données. Vous pouvez également charger un fichier existant en fournissant son chemin.
## Étape 2 : Accéder à la feuille de travail
Les classeurs Excel peuvent contenir plusieurs feuilles de calcul. Dans cette étape, nous allons accéder à la première feuille de calcul de votre classeur :
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Nous accédons maintenant à la première feuille de calcul du classeur. Si vous devez manipuler des feuilles supplémentaires, vous pouvez les référencer à l'aide de leur index ou de leur nom.
## Étape 3 : ajouter des données aux cellules
Commençons par ajouter des données à des cellules spécifiques. Tout d'abord, nous allons insérer la date système actuelle dans la cellule « A1 » :
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Cette ligne insère la date actuelle dans la cellule A1. Plutôt sympa, non ? Imaginez que vous fassiez cela manuellement pour des centaines de cellules : ce serait un cauchemar. Passons maintenant au formatage !
## Étape 4 : Formater la date dans la cellule « A1 »
Ensuite, formatons cette date dans un format plus lisible, comme « 15-oct-24 ». C'est là qu'Aspose.Cells brille vraiment :
1. Récupérer le style de la cellule :
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Ici, nous récupérons le style de la cellule A1. Considérez cela comme une capture du « style » de la cellule avant d'effectuer des modifications.
2. Définissez le format de la date :
```csharp
style.Number = 15;
```
 Réglage de la`Number` La propriété 15 applique le format de date souhaité. Il s'agit d'un code de format de nombre intégré pour afficher les dates au format « j-mmm-aa ».
3. Appliquez le style à la cellule :
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Cette ligne applique les modifications de style à la cellule. Désormais, au lieu d'un format de date par défaut, vous verrez quelque chose de beaucoup plus convivial comme « 15-oct-24 ».
## Étape 5 : ajouter et formater un pourcentage dans la cellule « A2 »
Passons maintenant à la mise en forme des pourcentages. Imaginez que vous souhaitiez insérer une valeur et l'afficher sous forme de pourcentage. Dans cette étape, nous allons ajouter une valeur numérique à la cellule « A2 » et la formater sous forme de pourcentage :
1. Insérer une valeur numérique :
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Cela insère le nombre 20 dans la cellule A2. Vous vous demandez peut-être : « Ce n'est qu'un simple nombre, comment puis-je le transformer en pourcentage ? » Eh bien, nous sommes sur le point d'y arriver.
2. Récupérez le style et définissez le format de pourcentage :
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Format en pourcentage
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Ici, nous ajoutons 2546 à la cellule A3. Ensuite, nous allons formater ce nombre pour qu'il s'affiche comme une devise.
2. Récupérez le style et définissez le format de devise :
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formater comme devise
worksheet.Cells["A3"].SetStyle(style);
```
 Réglage de la`Number` La propriété 6 applique le format monétaire. La valeur dans la cellule A3 s'affichera désormais sous la forme « 2 546,00 », avec des virgules et deux décimales.
## Étape 7 : Enregistrer le fichier Excel
Maintenant que nous avons appliqué toute la magie du formatage, il est temps d'enregistrer le fichier :
```csharp
// Sauvegarde du fichier Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Cette ligne enregistre le fichier Excel au format Excel 97-2003. Vous pouvez modifier le`SaveFormat`pour répondre à vos besoins. Et comme ça, vous avez créé et formaté un fichier Excel par programmation !
## Conclusion
Félicitations ! Vous avez appris à utiliser Aspose.Cells pour .NET pour appliquer des formats numériques intégrés aux cellules d'un fichier Excel. Des dates aux pourcentages et aux devises, nous avons couvert certains des besoins de mise en forme les plus courants pour le traitement des données Excel. Désormais, au lieu de formater manuellement les cellules, vous pouvez automatiser l'ensemble du processus, ce qui vous fait gagner du temps et réduit les erreurs.
## FAQ
### Puis-je appliquer des formats numériques personnalisés à l’aide d’Aspose.Cells pour .NET ?
 Oui ! En plus des formats intégrés, Aspose.Cells prend également en charge les formats numériques personnalisés. Vous pouvez créer des formats très spécifiques à l'aide de`Custom` propriété dans le`Style` classe.
### Comment puis-je formater une cellule en tant que devise avec un symbole spécifique ?
 Pour appliquer un symbole monétaire spécifique, vous pouvez utiliser un formatage personnalisé en définissant le`Style.Custom` propriété.
### Puis-je formater des lignes ou des colonnes entières ?
 Absolument ! Vous pouvez appliquer des styles à des lignes ou des colonnes entières à l'aide de la`Rows` ou`Columns`collections dans le`Worksheet` objet.
### Comment puis-je formater plusieurs cellules à la fois ?
Vous pouvez utiliser le`Range` objet permettant de sélectionner plusieurs cellules et d'appliquer des styles à toutes en même temps.
### Dois-je installer Microsoft Excel pour utiliser Aspose.Cells ?
Non, Aspose.Cells fonctionne indépendamment de Microsoft Excel, vous n'avez donc pas besoin d'installer Excel sur votre machine.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
