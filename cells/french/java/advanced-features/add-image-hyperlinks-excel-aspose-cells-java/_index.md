---
date: '2026-09-02'
description: Apprenez à créer des classeurs Excel contenant des images cliquables
  avec Aspose.Cells for Java, en ajoutant des hyperlinks aux images pour des feuilles
  de calcul interactives.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Apprenez à créer des classeurs Excel contenant des images cliquables
  avec Aspose.Cells for Java, en ajoutant des hyperlinks, des screen tips, et en optimisant
  les performances en quelques lignes de code.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Créer une image cliquable dans Excel avec Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Créer une image cliquable dans Excel avec Aspose.Cells for Java
url: /fr/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une image Excel cliquable avec Aspose.Cells for Java

## Introduction

Si vous souhaitez **créer des classeurs Excel avec image cliquable** qui permettent aux utilisateurs d'accéder à des sites web, des documents ou d'autres ressources d'un simple clic, vous êtes au bon endroit. Dans ce tutoriel, nous verrons comment Aspose.Cells for Java vous permet d'**ajouter des objets image Excel avec hyperlien**, de configurer les infobulles et de garder vos feuilles de calcul à la fois belles et fonctionnelles.

### Ce que vous apprendrez
- Initialisation d'un classeur Aspose.Cells en Java.  
- Insertion d'une image et transformation en hyperlien cliquable.  
- Méthodes clés telles que `addHyperlink`, `setPlacement` et `setScreenTip`.  
- Bonnes pratiques pour les performances et la licence.

## Réponses rapides
- **Quelle bibliothèque est requise ?** Aspose.Cells for Java.  
- **Puis-je utiliser des fichiers .xlsx ?** Oui – l'API fonctionne avec les .xls et .xlsx.  
- **Ai-je besoin d'une licence ?** Un essai fonctionne pour l'évaluation ; une licence permanente est requise pour la production.  
- **Combien de lignes de code ?** Environ 20 lignes pour ajouter une image cliquable.  
- **Est‑il thread‑safe ?** Les objets Workbook ne sont pas thread‑safe ; créez des instances séparées par thread.  
- **Puis-je ajouter une infobulle Excel ?** Oui – utilisez `Hyperlink.setScreenTip()` pour afficher un texte d'aide au survol.

## Comment créer une image Excel cliquable avec Aspose.Cells for Java

Vous créez un classeur Excel avec image cliquable en chargeant ou en créant un `Workbook`, en insérant un objet `Picture`, en attachant un `Hyperlink` à cette image, en définissant éventuellement une infobulle, puis en enregistrant le fichier. L'API gère tout le XML Excel de bas niveau, vous n'avez donc besoin que de quelques lignes simples de code Java.

### Prérequis
- **Aspose.Cells for Java** (v25.3 ou ultérieure).  
- **JDK 8+** installé.  
- Un IDE (IntelliJ IDEA, Eclipse ou NetBeans) ainsi que Maven ou Gradle pour la gestion des dépendances.  

### Bibliothèques requises
Add Aspose.Cells to your project:

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

### Acquisition de licence
- Essai gratuit : Téléchargez depuis [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licence temporaire : Demandez via la [page Licence temporaire](https://purchase.aspose.com/temporary-license/).  
- Achat : Pour une utilisation à long terme, visitez [Aspose Purchase](https://purchase.aspose.com/buy).

### Initialisation de base
La classe `Workbook` représente un fichier Excel complet en mémoire. Vous l’instanciez, puis obtenez une référence à la première feuille de calcul. `Worksheet` représente une feuille unique au sein du classeur.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Implémentation étape par étape

### Étape 1 : préparer votre classeur
Nous commençons par créer un nouveau classeur et sélectionner la première feuille.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Étape 2 : insérer une étiquette et ajuster la taille de la cellule
Ajoutez une étiquette descriptive et donnez à la cellule suffisamment d'espace pour l'image.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Étape 3 : ajouter l'image
`Picture` représente un objet image placé sur une feuille de calcul.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Astuce* : Remplacez `"path/to/aspose-logo.jpg"` par le chemin réel de votre fichier image.

### Étape 4 : configurer le placement et ajouter l'hyperlien
`Hyperlink` définit un lien associé à une cellule, une forme ou une image, permettant la navigation lorsqu'on clique.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Étape 5 : définir une infobulle et enregistrer le classeur
Fournissez une infobulle utile et écrivez le classeur sur le disque.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Pourquoi ajouter un hyperlien à une image Excel ?

Intégrer une image cliquable vous permet de transformer des éléments de marque, des icônes ou des diagrammes en points de navigation directs, réduisant le nombre de clics nécessaires pour accéder au contenu associé. Cette approche améliore l'efficacité des utilisateurs dans les tableaux de bord marketing, les manuels techniques et les feuilles de calcul éducatives.

## Comment ajouter une infobulle Excel

Vous ajoutez une infobulle en appelant `hyperlink.setScreenTip("Votre astuce ici")` sur l'objet `Hyperlink` attaché à l'image. L'infobulle apparaît lorsque le curseur survole l'image, offrant aux utilisateurs des indications contextuelles sans encombrer la feuille.

## Conseils de dépannage
- **Erreurs de chemin d'image** – vérifiez à nouveau l'emplacement du fichier et assurez-vous que l'application dispose des permissions de lecture.  
- **Licence non appliquée** – si l'essai expire, les hyperliens peuvent cesser de fonctionner ; appliquez une licence valide avec `License.setLicense`.  
- **Hyperlien non cliquable** – vérifiez que le `PlacementType` de l'image est réglé sur `FREE_FLOATING`.

## Applications pratiques
Embedding clickable images is useful in many scenarios:

1. **Rapports marketing** – lier les logos de marque aux pages produit.  
2. **Documentation technique** – joindre des diagrammes qui ouvrent des schémas détaillés.  
3. **Feuilles de calcul éducatives** – transformer des icônes en raccourcis vers des vidéos complémentaires.  
4. **Tableaux de bord de projet** – faire en sorte que les icônes de statut ouvrent les suivi de tâches associés.

## Considérations de performance
- Gardez des tailles de fichiers image raisonnables ; les grandes images augmentent l'utilisation mémoire du classeur.  
- Libérez les objets inutilisés (`workbook.dispose()`) lors du traitement de nombreux fichiers dans une boucle.  
- Mettez à jour vers la dernière version d'Aspose.Cells pour des améliorations de performance et des corrections de bugs.

## Conclusion
Vous savez maintenant comment ajouter un hyperlien aux images dans Excel en utilisant Aspose.Cells for Java, vous permettant de **créer des classeurs Excel avec image cliquable** plus riches et interactifs. Expérimentez avec différentes URL, infobulles et placements d'images pour répondre à vos besoins de reporting. Ensuite, vous pourriez explorer l'ajout d'hyperliens aux formes ou l'automatisation de l'insertion massive d'images sur plusieurs feuilles.

## Questions fréquemment posées

**Q:** Quelle est la taille maximale d'image prise en charge par Aspose.Cells for Java ?  
**A:** Il n'y a pas de limite stricte, mais les très grandes images peuvent affecter les performances et augmenter la taille du fichier.

**Q:** Puis-je utiliser cette fonctionnalité avec des fichiers .xlsx ?  
**A:** Oui, l'API fonctionne avec les formats `.xls` et `.xlsx`.

**Q:** Comment dois‑je gérer les exceptions lors de l'ajout d'hyperliens ?  
**A:** Enveloppez le code dans un bloc try‑catch et consignez les détails de `Exception` pour diagnostiquer les problèmes de chemin ou de licence.

**Q:** Est‑il possible de supprimer un hyperlien d'une image après son ajout ?  
**A:** Oui – récupérez l'objet `Picture` et appelez `pic.getHyperlink().remove()` ou supprimez l'image de la collection.

**Q:** Pourquoi mon hyperlien pourrait‑il ne pas fonctionner comme prévu ?  
**A:** Les causes courantes incluent une chaîne URL incorrecte, l'absence du préfixe `http://`/`https://`, ou un essai non licencié qui désactive certaines fonctionnalités.

## Ressources supplémentaires
- **Documentation :** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Téléchargement :** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Achat et essai :** Visitez [Aspose Purchase](https://purchase.aspose.com/buy) ou [Temporary License Page](https://purchase.aspose.com/temporary-license/) pour les options de licence.  
- **Forum de support :** Pour obtenir de l'aide, consultez le [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Dernière mise à jour :** 2026-09-02  
**Testé avec :** Aspose.Cells for Java 25.3  
**Auteur :** Aspose

## Tutoriels associés

- [Comment créer des hyperliens dans Excel avec Aspose.Cells pour Java - Guide étape par étape](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Comment styliser les cellules Excel et ajouter des hyperliens avec Aspose.Cells pour Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Ajouter une image à un commentaire Excel avec Aspose.Cells pour Java : Guide complet](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}