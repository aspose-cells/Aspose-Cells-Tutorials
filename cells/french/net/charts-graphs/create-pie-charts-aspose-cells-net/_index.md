---
"date": "2025-04-05"
"description": "Apprenez à créer des graphiques à secteurs dynamiques avec des lignes de repère avec Aspose.Cells pour .NET. Suivez ce guide pour améliorer vos compétences en visualisation de données."
"title": "Création de graphiques à secteurs avec lignes de repère dans Aspose.Cells .NET - Un guide complet"
"url": "/fr/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Création de graphiques à secteurs avec lignes de repère à l'aide d'Aspose.Cells .NET

## Introduction
Améliorez la visualisation de vos données en créant des graphiques à secteurs plus informatifs avec Aspose.Cells pour .NET. Ce guide étape par étape vous explique comment ajouter des lignes de repère aux segments de votre graphique à secteurs, facilitant ainsi l'identification rapide des catégories de données correspondantes. En suivant ce tutoriel, vos visualisations seront à la fois attrayantes et hautement fonctionnelles.

**Ce que vous apprendrez :**
- Configuration d'Aspose.Cells pour .NET dans votre environnement
- Création de graphiques à secteurs à lignes de repère personnalisées à l'aide de C#
- Enregistrer le graphique sous forme d'image ou dans un classeur Excel

Assurez-vous d’avoir tout prêt pour suivre efficacement.

## Prérequis
Avant de commencer, assurez-vous de remplir ces conditions préalables :

- **Bibliothèques et versions**: Installez Aspose.Cells pour .NET. Assurez-vous que votre projet est configuré avec la dernière version.
- **Configuration de l'environnement**:Ce guide suppose un environnement .NET compatible pour Aspose.Cells.
- **Prérequis en matière de connaissances**:Une connaissance de base de la programmation C# et des opérations Excel est bénéfique.

## Configuration d'Aspose.Cells pour .NET
Pour commencer, installez Aspose.Cells dans votre projet via :

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**Gestionnaire de paquets**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Obtenez une licence pour toutes les fonctionnalités en sélectionnant parmi les options suivantes :
- **Essai gratuit**: Commencez votre essai gratuit sur le [Page de téléchargement d'Aspose](https://releases.aspose.com/cells/net/).
- **Permis temporaire**: Obtenir un permis temporaire [ici](https://purchase.aspose.com/temporary-license/).
- **Achat**: Pour bénéficier de toutes les fonctionnalités, achetez une licence [ici](https://purchase.aspose.com/buy).

Initialisez Aspose.Cells dans votre projet en créant une instance de `Workbook` classe.

## Guide de mise en œuvre

### Création du classeur et de la feuille de travail
1. **Initialiser le classeur**
   Créer un nouveau classeur au format XLSX :
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Accéder à la première feuille de travail**
   Utilisez la première feuille de calcul pour saisir les données :
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Ajout de données pour un graphique à secteurs**
   Remplissez votre feuille de calcul avec des catégories et des valeurs :
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Ajoutez les noms de catégories restants...
   worksheet.Cells["B1"].PutValue(10.4);
   // Ajoutez les valeurs correspondantes...
   ```

### Ajout d'un graphique à secteurs à la feuille de calcul
1. **Créer le graphique à secteurs**
   Générez un graphique à secteurs et ajoutez-le à la collection de graphiques de votre feuille de calcul :
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Configurer les données des séries et des catégories**
   Lier les données pour les séries et les catégories :
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Personnaliser les étiquettes de données**
   Désactiver l'affichage de la légende, définir des étiquettes de données pour afficher les noms de catégorie et les pourcentages :
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Mise en œuvre des lignes directrices
1. **Activer les lignes de repère**
   Activer les lignes de repère pour des connexions visuelles plus claires :
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Ajuster la position des étiquettes de données**
   Assurez la visibilité en ajustant les positions des étiquettes :
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Enregistrer le graphique et le classeur
1. **Enregistrer en tant qu'image**
   Rendre le graphique dans un fichier image :
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Enregistrer le classeur**
   Enregistrez le classeur pour afficher le graphique dans Excel :
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Applications pratiques
- **Rapports financiers**:Représenter clairement les allocations budgétaires.
- **Analyse marketing**:Visualisez efficacement les données de part de marché dans des présentations ou des rapports.
- **Analyse des ventes**:Affichez facilement la répartition des ventes entre différentes régions/produits.

Les possibilités d’intégration incluent l’exportation de ces visualisations vers des applications Web ou leur intégration dans des outils de reporting automatisés.

## Considérations relatives aux performances
Lorsque vous utilisez Aspose.Cells, tenez compte des éléments suivants pour des performances optimales :
- Réduisez les grands ensembles de données chargés en mémoire à la fois.
- Utilisez des boucles efficaces et évitez les calculs inutiles à l'intérieur des boucles.
- Nettoyez régulièrement les ressources telles que les objets du classeur pour éviter les fuites de mémoire.

## Conclusion
Vous avez appris à créer des graphiques à secteurs avec des lignes de repère à l'aide d'Aspose.Cells pour .NET. Cette fonctionnalité améliore la clarté de vos visualisations de données, les rendant plus accessibles et plus percutantes. 

**Prochaines étapes :**
Explorez d’autres personnalisations dans l’apparence des graphiques ou expérimentez d’autres types de graphiques disponibles dans Aspose.Cells.

## Section FAQ
1. **Qu'est-ce qu'une ligne de repère dans un graphique à secteurs ?**
   Les lignes de repère relient les étiquettes de données à leurs segments respectifs, améliorant ainsi la lisibilité.

2. **Puis-je utiliser Aspose.Cells gratuitement ?**
   Oui, vous pouvez commencer avec un essai gratuit, mais les fonctionnalités complètes nécessitent une licence.

3. **Est-il possible d'exporter des graphiques sous forme d'images ?**
   Absolument ! Utilisez `ImageOrPrintOptions` pour enregistrer votre graphique dans des formats d'image tels que PNG ou JPEG.

4. **Comment ajuster manuellement les positions des étiquettes de données ?**
   Modifiez les coordonnées X et Y des étiquettes de données dans la boucle de points de série.

5. **Aspose.Cells peut-il s'intégrer à d'autres systèmes ?**
   Oui, il peut être utilisé conjointement avec des bases de données, des services Web et bien plus encore pour des solutions de reporting automatisées.

## Ressources
- [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Télécharger Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Licence d'achat](https://purchase.aspose.com/buy)
- [Essai gratuit](https://releases.aspose.com/cells/net/)
- [Permis temporaire](https://purchase.aspose.com/temporary-license/)
- [Forum d'assistance](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}