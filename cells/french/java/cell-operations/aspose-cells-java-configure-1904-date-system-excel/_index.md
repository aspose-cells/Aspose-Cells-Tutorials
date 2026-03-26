---
date: '2026-02-22'
description: Apprenez comment modifier le système de dates d’Excel en 1904 avec Aspose.Cells
  pour Java, définir le format de date Excel et convertir efficacement le système
  1904 d’Excel.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Modifier le système de dates Excel en 1904 avec Aspose.Cells Java
url: /fr/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifier le système de dates Excel en 1904 avec Aspose.Cells Java

Gérer des données historiques dans Excel peut être difficile car Excel prend en charge deux systèmes de dates différents. **Dans ce tutoriel, vous apprendrez comment modifier le système de dates Excel au format 1904 en utilisant Aspose.Cells pour Java**, ce qui rend la gestion des dates héritées simple. Nous parcourrons l'initialisation d'un classeur, l'activation du système de dates 1904 et la persistance du changement.

## Réponses rapides
- **Que fait le système de dates 1904 ?** Il commence à compter les jours à partir du 1 janvier 1904, décalant toutes les dates de 1462 jours par rapport au système par défaut 1900.  
- **Pourquoi utiliser Aspose.Cells pour changer le système de dates ?** Il fournit une API simple qui fonctionne sans Excel installé et prend en charge les gros fichiers.  
- **Quelles versions de Java sont prises en charge ?** JDK 8 ou supérieur.  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence supprime les limites d'utilisation.  
- **Puis-je reconvertir au système 1900 plus tard ?** Oui, il suffit de définir `setDate1904(false)`.

## Qu'est-ce que le système de dates 1904 dans Excel ?
Le système de dates 1904 était à l'origine utilisé par les premières versions Macintosh d'Excel. Il compte les jours à partir du 1 janvier 1904, ce qui est utile pour la compatibilité avec les feuilles de calcul anciennes et certains modèles financiers.

## Pourquoi modifier le système de dates Excel avec Aspose.Cells ?
- **Compatibilité multiplateforme** – fonctionne sous Windows, Linux et macOS.  
- **Aucune installation d'Excel requise** – idéal pour le traitement côté serveur.  
- **Haute performance** – gère de grands classeurs avec une surcharge mémoire minimale.  

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur.  
- Maven ou Gradle pour la gestion des dépendances.  
- Connaissances de base en programmation Java.  

## Configuration d'Aspose.Cells pour Java

### Maven
Ajoutez la dépendance suivante à votre fichier `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Incluez cette ligne dans votre fichier `build.gradle` :

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Acquisition de licence
Aspose propose un essai gratuit, une licence temporaire et des licences commerciales complètes. Vous pouvez commencer avec l'[essai gratuit](https://releases.aspose.com/cells/java/) ou obtenir une licence temporaire depuis la [page de licence temporaire](https://purchase.aspose.com/temporary-license/).

## Modifier le système de dates Excel avec Aspose.Cells Java

Voici le guide étape par étape qui **modifie réellement le système de dates Excel**. Chaque étape comprend une brève explication suivie du code exact dont vous avez besoin.

### Étape 1 : Initialiser et charger le classeur
Tout d'abord, créez une instance `Workbook` qui pointe vers votre fichier Excel existant.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Étape 2 : Activer le système de dates 1904
Utilisez les paramètres du classeur pour changer le système de dates.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Astuce :** Vous pouvez également appeler `setDate1904(false)` plus tard si vous devez revenir en arrière.

### Étape 3 : Enregistrer le classeur modifié
Enfin, écrivez les modifications dans un nouveau fichier (ou écrasez l'original).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Note :** Le code ci‑dessus utilise le nom de classe `tWorkbook` tel qu'il a été fourni à l'origine. Assurez‑vous que cette faute de frappe correspond aux conventions de nommage de votre projet ou corrigez‑la en `Workbook` si nécessaire.

## Définir la date Excel par programme (mot‑clé secondaire)
Si vous devez ajuster les valeurs de cellules individuelles après avoir changé le système, vous pouvez utiliser `Cells.get(i, j).putValue(Date)` où la date sera interprétée selon le système de dates actif.

## Convertir le système Excel 1904 en 1900 (mot‑clé secondaire)
Pour revenir en arrière, appelez simplement :

```java
workbook.getSettings().setDate1904(false);
```

Puis enregistrez à nouveau le classeur.

## Applications pratiques
1. **Archivage des données** – Conserver les horodatages hérités lors de la migration d'anciennes feuilles de calcul basées sur Mac.  
2. **Rapports multiplateformes** – Générer des rapports qui peuvent être ouverts à la fois sous Windows et macOS sans discordances de dates.  
3. **Modélisation financière** – Aligner les calculs de dates avec les modèles financiers hérités qui attendent le système 1904.  

## Considérations de performance
- Limitez les opérations sur le classeur dans une session unique afin de maintenir une faible utilisation de la mémoire.  
- Utilisez le réglage du ramasse‑miettes de Java pour les fichiers très volumineux.  

## Questions fréquemment posées

**Q : Quelle est la différence entre les systèmes de dates 1900 et 1904 ?**  
R : Le système 1900 commence le 1 janvier 1900, tandis que le système 1904 commence le 1 janvier 1904, décalant toutes les dates de 1462 jours.

**Q : Puis‑je changer le système de dates d'un classeur actuellement ouvert dans Excel ?**  
R : Oui, mais vous devez d'abord fermer le fichier dans Excel ; sinon l'opération d'enregistrement échouera.

**Q : Ai‑je besoin d'une licence pour utiliser `setDate1904` ?**  
R : La méthode fonctionne dans l'essai gratuit, mais une licence complète supprime les limitations d'évaluation.

**Q : Est‑il possible de changer le système de dates pour une seule feuille de calcul ?**  
R : Non, le système de dates est un paramètre au niveau du classeur ; il s'applique à toutes les feuilles.

**Q : Comment vérifier que le système de dates a été modifié ?**  
R : Ouvrez le fichier enregistré dans Excel, allez dans **Fichier → Options → Avancé**, et cochez la case **"Utiliser le système de dates 1904"**.

## Conclusion
Vous savez maintenant comment **modifier le système de dates Excel** en 1904 en utilisant Aspose.Cells pour Java, comment définir les formats de dates Excel, et comment revenir en arrière si nécessaire. Intégrez ces extraits dans vos pipelines de traitement de données pour garantir la compatibilité des dates sur toutes les plateformes.

---

**Dernière mise à jour :** 2026-02-22  
**Testé avec :** Aspose.Cells 25.3 for Java  
**Auteur :** Aspose  

**Ressources**
- **Documentation :** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Téléchargement :** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Acheter une licence :** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Essai gratuit :** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licence temporaire :** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Forum de support :** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}