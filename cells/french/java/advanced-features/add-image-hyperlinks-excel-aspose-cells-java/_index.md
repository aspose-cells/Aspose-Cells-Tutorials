---
date: '2026-02-16'
description: Apprenez à créer des images cliquables dans Excel avec Aspose.Cells pour
  Java, en ajoutant des hyperliens aux images pour des feuilles de calcul interactives.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Créer un fichier Excel avec image cliquable à l'aide d'Aspose.Cells pour Java
url: /fr/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec image cliquable à l'aide d'Aspose.Cells pour Java

## Introduction

Si vous souhaitez **créer des classeurs Excel avec image cliquable** qui permettent aux utilisateurs d'accéder à des sites web, des documents ou d'autres ressources d'un simple clic, vous êtes au bon endroit. Dans ce tutoriel, nous verrons comment Aspose.Cells pour Java vous permet **d'ajouter des images Excel avec hyperlien**, de configurer des info-bulles, et de garder vos feuilles de calcul à la fois belles et fonctionnelles.

### Ce que vous allez apprendre
- Initialiser un classeur Aspose.Cells en Java.  
- Insérer une image et la transformer en hyperlien cliquable.  
- Méthodes clés telles que `addHyperlink`, `setPlacement` et `setScreenTip`.  
- Bonnes pratiques pour les performances et la licence.

## Réponses rapides
- **Quelle bibliothèque est requise ?** Aspose.Cells for Java.  
- **Puis-je utiliser des fichiers .xlsx ?** Oui – l'API fonctionne avec les formats .xls et .xlsx.  
- **Ai‑je besoin d'une licence ?** Un essai fonctionne pour l'évaluation ; une licence permanente est requise pour la production.  
- **Combien de lignes de code ?** Environ 20 lignes pour ajouter une image cliquable.  
- **Est‑ce thread‑safe ?** Les objets Workbook ne sont pas thread‑safe ; créez des instances séparées par thread.  
- **Puis‑je ajouter une info‑bulle Excel ?** Oui – utilisez `Hyperlink.setScreenTip()` pour afficher un texte d'aide au survol.

## Comment créer un classeur Excel avec image cliquable à l'aide d'Aspose.Cells pour Java

### Prérequis
Avant de commencer, assurez‑vous d'avoir :

- **Aspose.Cells for Java** (v25.3 ou ultérieure).  
- **JDK 8+** installé.  
- Un IDE (IntelliJ IDEA, Eclipse ou NetBeans) et Maven ou Gradle pour la gestion des dépendances.  

### Bibliothèques requises
Ajoutez Aspose.Cells à votre projet :

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Obtention de licence
Aspose.Cells est commercial, mais vous pouvez commencer avec un essai gratuit ou demander une licence temporaire :

- Essai gratuit : Téléchargez depuis [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licence temporaire : Demandez via la [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Achat : Pour une utilisation à long terme, visitez [Aspose Purchase](https://purchase.aspose.com/buy).

### Initialisation de base
Créez un classeur et récupérez la première feuille de calcul :

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Mise en œuvre étape par étape

### Étape 1 : Préparer votre classeur
Nous commençons par créer un nouveau classeur et sélectionner la première feuille.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Étape 2 : Insérer une étiquette et ajuster la taille de la cellule
Ajoutez une étiquette descriptive et donnez à la cellule suffisamment d'espace pour l'image.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Étape 3 : Ajouter l'image
Chargez le fichier image et placez‑le sur la feuille.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Astuce* : Remplacez `"path/to/aspose-logo.jpg"` par le chemin réel de votre fichier image.

### Étape 4 : Configurer le placement et ajouter l'hyperlien
Rendez l'image librement positionnable et attachez‑lui un hyperlien.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Étape 5 : Définir une info‑bulle et enregistrer le classeur
Fournissez une info‑bulle utile et écrivez le classeur sur le disque.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Pourquoi ajouter une image Excel avec hyperlien ?
Intégrer une image cliquable vous permet de transformer des éléments de marque, des icônes ou des diagrammes en points de navigation directs. Cela améliore l'expérience utilisateur dans les tableaux de bord marketing, les manuels techniques et les feuilles de travail éducatives en réduisant le nombre de clics nécessaires pour accéder au contenu associé.

## Comment ajouter une info‑bulle Excel
La méthode `setScreenTip` vous permet de définir le texte qui apparaît lorsque l'utilisateur place le curseur sur l'image. C’est idéal pour fournir du contexte, tel que « Voir les détails du produit » ou « Ouvrir la vidéo du tutoriel ».

## Conseils de dépannage
- **Erreurs de chemin d'image** – vérifiez le chemin du fichier et assurez‑vous que l'application dispose des permissions de lecture.  
- **Licence non appliquée** – si l'essai expire, les hyperliens peuvent cesser de fonctionner ; appliquez une licence valide avec `License.setLicense`.  
- **Hyperlien non cliquable** – assurez‑vous que le `PlacementType` de l'image est réglé sur `FREE_FLOATING`.

## Applications pratiques
Intégrer des images cliquables est utile dans de nombreux scénarios :

1. **Rapports marketing** – lier les logos de marque aux pages produit.  
2. **Documentation technique** – joindre des diagrammes qui ouvrent des schémas détaillés.  
3. **Fiches pédagogiques** – transformer des icônes en raccourcis vers des vidéos complémentaires.  
4. **Tableaux de bord de projet** – faire en sorte que les icônes d’état ouvrent les suivis de tâches associés.

## Considérations de performance
- Gardez les tailles de fichier image raisonnables ; les images volumineuses augmentent la consommation mémoire du classeur.  
- Libérez les objets inutilisés (`workbook.dispose()`) lors du traitement de nombreux fichiers dans une boucle.  
- Mettez à jour vers la dernière version d'Aspose.Cells pour bénéficier d'améliorations de performance et de corrections de bugs.

## Conclusion
Vous savez maintenant **comment ajouter un hyperlien** aux images dans Excel en utilisant Aspose.Cells pour Java, ce qui vous permet de **créer des classeurs Excel avec image cliquable** plus riches et interactifs. Expérimentez avec différentes URL, info‑bulles et placements d'images pour répondre à vos besoins de reporting. Ensuite, vous pourrez explorer l'ajout d'hyperliens aux formes ou automatiser l'insertion massive d'images sur plusieurs feuilles de calcul.

## Questions fréquentes

**Q :** Quelle est la taille maximale d'image prise en charge par Aspose.Cells pour Java ?  
**R :** Il n'existe pas de limite stricte, mais les images très volumineuses peuvent affecter les performances et augmenter la taille du fichier.

**Q :** Puis‑je utiliser cette fonctionnalité avec des fichiers .xlsx ?  
**R :** Oui, l'API fonctionne avec les formats `.xls` et `.xlsx`.

**Q :** Comment gérer les exceptions lors de l'ajout d'hyperliens ?  
**R :** Enveloppez le code dans un bloc `try‑catch` et consignez les détails de l'`Exception` pour diagnostiquer les problèmes de chemin ou de licence.

**Q :** Est‑il possible de supprimer un hyperlien d'une image après l'avoir ajouté ?  
**R :** Oui – récupérez l'objet `Picture` et appelez `pic.getHyperlink().remove()` ou supprimez l'image de la collection.

**Q :** Pourquoi mon hyperlien ne fonctionne‑t‑il pas comme prévu ?  
**R :** Les causes courantes incluent une chaîne URL incorrecte, l'absence du préfixe `http://`/`https://`, ou un essai non licencié qui désactive certaines fonctionnalités.

## Ressources supplémentaires
- **Documentation :** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Téléchargement :** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Achat et essai :** Visitez [Aspose Purchase](https://purchase.aspose.com/buy) ou [Temporary License Page](https://purchase.aspose.com/temporary-license/) pour les options de licence.  
- **Forum d'assistance :** Pour obtenir de l'aide, consultez le [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Dernière mise à jour :** 2026-02-16  
**Testé avec :** Aspose.Cells for Java 25.3  
**Auteur :** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}