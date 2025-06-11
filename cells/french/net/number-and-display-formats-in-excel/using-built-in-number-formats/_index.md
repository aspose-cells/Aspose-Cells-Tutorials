---
"description": "Automatisez la mise en forme des nombres dans Excel avec Aspose.Cells pour .NET. Apprenez à appliquer des formats de date, de pourcentage et de devise par programmation."
"linktitle": "Utilisation programmatique des formats numériques intégrés dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Utilisation programmatique des formats numériques intégrés dans Excel"
"url": "/fr/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Utilisation programmatique des formats numériques intégrés dans Excel

## Introduction
Dans ce tutoriel, nous vous expliquerons comment utiliser les formats numériques intégrés dans Excel avec Aspose.Cells pour .NET. Nous aborderons tous les aspects, de la configuration de votre environnement à l'application de différents formats tels que les dates, les pourcentages et les devises. Que vous soyez un expert ou que vous débutiez dans l'écosystème .NET, ce guide vous permettra de formater facilement des cellules Excel.
## Prérequis
Avant de vous lancer, assurez-vous d'avoir les éléments suivants :
- Bibliothèque Aspose.Cells pour .NET installée. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/cells/net/).
- Une connaissance pratique de C# et de la programmation .NET de base.
- Visual Studio ou tout autre IDE .NET installé sur votre machine.
- Une licence Aspose valide ou [permis temporaire](https://purchase.aspose.com/temporary-license/).
- .NET framework installé (version 4.0 ou supérieure).
  
S'il vous manque l'un des éléments ci-dessus, suivez les liens fournis pour tout configurer. Prêt ? Passons à la partie amusante !
## Importer des packages
Avant de commencer le didacticiel, assurez-vous d'importer les espaces de noms nécessaires pour travailler avec Aspose.Cells pour .NET :
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Une fois ces éléments importés, vous êtes prêt à manipuler des fichiers Excel par programmation. Passons maintenant au guide étape par étape !
## Étape 1 : Créez ou accédez à votre classeur Excel
À cette étape, vous allez créer un nouveau classeur. Imaginez l'ouverture d'un nouveau fichier Excel, sauf que vous le faites via du code !
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
Ici, nous instancions simplement un nouveau `Workbook` Objet. Il s'agit de votre fichier Excel, prêt à être manipulé. Vous pouvez également charger un fichier existant en indiquant son chemin d'accès.
## Étape 2 : Accéder à la feuille de travail
Les classeurs Excel peuvent contenir plusieurs feuilles de calcul. Dans cette étape, nous allons accéder à la première feuille de calcul de votre classeur :
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Nous accédons maintenant à la première feuille de calcul du classeur. Si vous devez manipuler d'autres feuilles, vous pouvez les référencer via leur index ou leur nom.
## Étape 3 : Ajouter des données aux cellules
Commençons par ajouter des données à des cellules spécifiques. Commençons par insérer la date système actuelle dans la cellule « A1 » :
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Cette ligne insère la date du jour dans la cellule A1. Plutôt pratique, non ? Imaginez faire cela manuellement pour des centaines de cellules : ce serait un cauchemar. Passons maintenant à la mise en forme !
## Étape 4 : Formater la date dans la cellule « A1 »
Ensuite, formatons cette date dans un format plus lisible, par exemple « 15-oct-24 ». C'est là qu'Aspose.Cells se démarque :
1. Récupérer le style de la cellule :
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Ici, nous récupérons le style de la cellule A1. Considérez cela comme une capture du « mode » de la cellule avant d'effectuer des modifications.
2. Définissez le format de la date :
```csharp
style.Number = 15;
```
Réglage de la `Number` La propriété 15 applique le format de date souhaité. Il s'agit d'un code de format numérique intégré permettant d'afficher les dates au format « j-mmm-aa ».
3. Appliquer le style à la cellule :
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Cette ligne applique les modifications de style à la cellule. Désormais, au lieu du format de date par défaut, vous verrez un format beaucoup plus convivial, comme « 15-oct-24 ».
## Étape 5 : Ajouter et formater un pourcentage dans la cellule « A2 »
Passons maintenant au formatage des pourcentages. Imaginez que vous souhaitiez insérer une valeur et l'afficher sous forme de pourcentage. Dans cette étape, nous allons ajouter une valeur numérique à la cellule « A2 » et la formater sous forme de pourcentage :
1. Insérer une valeur numérique :
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Cela insère le nombre 20 dans la cellule A2. Vous vous demandez peut-être : « Ce n'est qu'un simple nombre ; comment le transformer en pourcentage ? » Eh bien, nous allons y arriver.
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
Ici, nous ajoutons 2546 à la cellule A3. Nous allons ensuite formater ce nombre pour qu'il s'affiche comme une devise.
2. Récupérez le style et définissez le format de devise :
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formater comme devise
worksheet.Cells["A3"].SetStyle(style);
```
Réglage de la `Number` La propriété 6 applique le format monétaire. La valeur de la cellule A3 s'affichera désormais sous la forme « 2 546,00 », avec des virgules et deux décimales.
## Étape 7 : Enregistrez le fichier Excel
Maintenant que nous avons appliqué toute la magie du formatage, il est temps d'enregistrer le fichier :
```csharp
// Sauvegarde du fichier Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Cette ligne enregistre le fichier Excel au format Excel 97-2003. Vous pouvez modifier le `SaveFormat` pour répondre à vos besoins. Et voilà, vous avez créé et formaté un fichier Excel par programmation !
## Conclusion
Félicitations ! Vous avez appris à utiliser Aspose.Cells pour .NET pour appliquer des formats numériques intégrés aux cellules d'un fichier Excel. Des dates aux pourcentages en passant par les devises, nous avons abordé certains des besoins de mise en forme les plus courants pour le traitement des données Excel. Désormais, au lieu de formater manuellement les cellules, vous pouvez automatiser l'ensemble du processus, ce qui vous fait gagner du temps et réduit les erreurs.
## FAQ
### Puis-je appliquer des formats numériques personnalisés à l’aide d’Aspose.Cells pour .NET ?
Oui ! Outre les formats intégrés, Aspose.Cells prend également en charge les formats numériques personnalisés. Vous pouvez créer des formats très spécifiques grâce à l'outil `Custom` propriété dans le `Style` classe.
### Comment puis-je formater une cellule en tant que devise avec un symbole spécifique ?
Pour appliquer un symbole monétaire spécifique, vous pouvez utiliser un formatage personnalisé en définissant le `Style.Custom` propriété.
### Puis-je formater des lignes ou des colonnes entières ?
Absolument ! Vous pouvez appliquer des styles à des lignes ou des colonnes entières à l'aide de `Rows` ou `Columns` collections dans le `Worksheet` objet.
### Comment puis-je formater plusieurs cellules à la fois ?
Vous pouvez utiliser le `Range` objet permettant de sélectionner plusieurs cellules et d'appliquer des styles à toutes en même temps.
### Ai-je besoin d’installer Microsoft Excel pour utiliser Aspose.Cells ?
Non, Aspose.Cells fonctionne indépendamment de Microsoft Excel, vous n'avez donc pas besoin d'installer Excel sur votre machine.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}