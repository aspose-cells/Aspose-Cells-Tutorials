---
"date": "2025-04-05"
"description": "Découvrez comment ajouter et personnaliser des filigranes dans des feuilles Excel avec Aspose.Cells pour .NET. Ce guide couvre la configuration, la mise en œuvre et les fonctionnalités de sécurité."
"title": "Comment ajouter des filigranes dans Excel à l'aide d'Aspose.Cells .NET ? Un guide complet"
"url": "/fr/net/headers-footers/excel-watermark-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Comment ajouter des filigranes dans Excel avec Aspose.Cells .NET

Dans le monde numérique d'aujourd'hui, la protection de vos données sensibles est cruciale lors du partage de documents tels que des feuilles de calcul. L'ajout de filigranes, un indice visuel subtil mais puissant, peut indiquer la confidentialité ou la propriété. Ce guide complet vous explique comment utiliser Aspose.Cells pour .NET pour ajouter et personnaliser des effets de filigrane dans des feuilles Excel.

## Ce que vous apprendrez
- Configuration d'Aspose.Cells pour .NET dans votre environnement de développement.
- Ajout d'un filigrane à une feuille Excel avec C#.
- Personnalisation de l'apparence des filigranes, y compris les paramètres de couleur et de transparence.
- Verrouillage des formes dans Excel pour empêcher les modifications non autorisées.
- Applications pratiques pour améliorer la sécurité des documents.

Explorons comment vous pouvez implémenter ces fonctionnalités dans vos projets.

## Prérequis
Avant de commencer, assurez-vous d’avoir :
- **Visual Studio** installé sur votre machine (toute version à partir de 2017).
- Connaissances de base du développement C# et .NET.
- Une compréhension générale de la manipulation de fichiers Excel à l'aide d'API.

De plus, installez Aspose.Cells pour .NET via la console du gestionnaire de packages NuGet ou la CLI .NET :

**Gestionnaire de packages NuGet**
```bash
PM> Install-Package Aspose.Cells
```

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

### Acquisition de licence
Pour utiliser Aspose.Cells pour .NET, vous pouvez commencer avec une licence d'essai gratuite pour explorer ses capacités :
1. **Essai gratuit :** Visitez le [Page de licence temporaire Aspose](https://purchase.aspose.com/temporary-license/) et demander une licence temporaire.
2. **Achat:** Pour une utilisation à long terme, achetez une licence via [Page d'achat d'Aspose](https://purchase.aspose.com/buy).

### Configuration de base
Une fois que vous avez acquis Aspose.Cells via NuGet ou la CLI, initialisez-le dans votre projet C# :
```csharp
using Aspose.Cells;
```

## Configuration d'Aspose.Cells pour .NET
Voici un bref aperçu de la configuration et de l'initialisation d'Aspose.Cells :
1. **Installer** Aspose.Cells à l'aide de la console du gestionnaire de packages ou de la CLI .NET comme indiqué ci-dessus.
2. **Initialiser:** Commencez par créer un `Workbook` objet, représentant un fichier Excel.

```csharp
Workbook workbook = new Workbook();
```
3. **Demander une licence :** Si vous disposez d'une licence, appliquez-la pour débloquer toutes les fonctionnalités.

## Guide de mise en œuvre

### Fonctionnalité 1 : Ajouter un filigrane à une feuille Excel
#### Aperçu
L'ajout d'un filigrane consiste à créer des effets de texte qui se superposent subtilement à vos données, signalant le statut du document comme « CONFIDENTIEL ».

#### Mise en œuvre étape par étape
##### Créer un classeur et une feuille de travail
```csharp
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

##### Ajouter un effet de texte en filigrane
Créez la forme d'effet de texte avec des attributs spécifiques tels que le style de police, la taille, la position et l'apparence.

```csharp
Shape wordart = sheet.Shapes.AddTextEffect(
    MsoPresetTextEffect.TextEffect1,
    "CONFIDENTIAL", 
    "Arial Black",
    50,   // Taille de la police
    false, // Est en italique
    true, // Est audacieux
    18,   // Position gauche
    8,    // Position supérieure
    1,    // Largeur
    1,    // Hauteur
    130,  // Angle de rotation
    800   // Facteur d'échelle
);
```

##### Personnaliser l'apparence
Définissez la couleur du dégradé et la transparence pour un look soigné.
```csharp
FillFormat wordArtFormat = wordart.Fill;
wordArtFormat.SetOneColorGradient(Color.Red, 0.2, GradientStyleType.Horizontal, 2); 
wordArtFormat.Transparency = 0.9; // Rendez-le légèrement transparent

wordart.HasLine = false; // Supprimez la ligne de bordure pour une apparence plus nette
```

##### Enregistrez votre classeur
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

### Fonctionnalité 2 : Verrouiller les aspects de forme dans une feuille Excel
#### Aperçu
Le verrouillage des formes empêche les utilisateurs non autorisés de modifier le filigrane ou d'autres formes, garantissant ainsi l'intégrité du document.

#### Mise en œuvre étape par étape
##### Verrouiller diverses propriétés du filigrane
Sécurisez votre filigrane en verrouillant ses aspects.
```csharp
wordart.IsLocked = true;
wordart.SetLockedProperty(ShapeLockType.Selection, true);
wordart.SetLockedProperty(ShapeLockType.ShapeType, true);
wordart.SetLockedProperty(ShapeLockType.Move, true);
wordart.SetLockedProperty(ShapeLockType.Resize, true);
wordart.SetLockedProperty(ShapeLockType.Text, true);
```

##### Enregistrer les modifications
Assurez-vous que les modifications sont enregistrées dans votre classeur.
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

## Applications pratiques
1. **Rapports confidentiels :** Utilisez des filigranes pour les rapports internes contenant des informations sensibles.
2. **Avis de droits d'auteur :** Intégrer des avis de droits d’auteur dans les modèles distribués aux clients.
3. **Contrôle de version :** Indiquez les versions brouillon ou finales des documents avec le texte en filigrane correspondant.

## Considérations relatives aux performances
- **Optimiser les ressources :** Minimisez l’utilisation des ressources en chargeant uniquement les feuilles de calcul et les formes nécessaires.
- **Gestion de la mémoire :** Éliminer les objets de manière appropriée en utilisant `Dispose()` méthodes, le cas échéant, garantissant une gestion efficace de la mémoire dans les applications .NET.

## Conclusion
En maîtrisant l'utilisation d'Aspose.Cells pour .NET pour ajouter des filigranes et verrouiller des formes dans des feuilles Excel, vous renforcez la sécurité de vos documents et communiquez des informations essentielles en un clin d'œil. Ce guide vous a donné les compétences nécessaires pour mettre en œuvre efficacement ces fonctionnalités.

### Prochaines étapes
Explorez d'autres options de personnalisation dans le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) ou essayez d'intégrer ces fonctionnalités dans des systèmes plus vastes nécessitant une gestion de documents robuste.

## Section FAQ
1. **Comment puis-je modifier le texte du filigrane ?**
   - Modifier le deuxième paramètre de `AddTextEffect()` méthode avec le texte souhaité.
2. **Puis-je utiliser différentes polices pour mon filigrane ?**
   - Oui, spécifiez n'importe quelle police en modifiant le troisième paramètre dans `AddTextEffect()`.
3. **Que faire si mon fichier Excel est volumineux et que le chargement est lent ?**
   - Envisagez d’optimiser votre code pour charger uniquement les parties nécessaires du classeur ou d’utiliser les options de réglage des performances disponibles dans Aspose.Cells.
4. **Est-il possible de supprimer un filigrane ultérieurement ?**
   - Oui, vous pouvez supprimer des formes de la collection de feuilles de calcul dans laquelle elles résident.
5. **Comment appliquer cette solution dans le traitement par lots ?**
   - Parcourez plusieurs classeurs en appliquant une logique similaire dans des boucles ou des tâches asynchrones pour plus d'efficacité.

## Ressources
- [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Télécharger Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Acheter une licence](https://purchase.aspose.com/buy)
- [Obtenez un essai gratuit](https://releases.aspose.com/cells/net/)
- [Demander une licence temporaire](https://purchase.aspose.com/temporary-license/)
- [Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9)

Maintenant que vous avez les connaissances, il est temps de mettre ces techniques en pratique et de sécuriser efficacement vos documents Excel !


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}