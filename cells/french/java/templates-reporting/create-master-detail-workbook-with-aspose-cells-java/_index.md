---
category: general
date: 2026-06-08
description: Créer un classeur maître‑détail en Java avec Aspose.Cells Smart Marker.
  Apprenez étape par étape comment lier les données maîtres à une feuille de détail
  et exporter Excel.
draft: false
keywords:
- create master detail workbook
- Aspose.Cells Smart Marker
- Java Excel export
- master‑detail relationship
- Smart Marker data source
language: fr
og_description: Créez un classeur maître‑détail en Java en utilisant Aspose.Cells
  Smart Marker. Suivez ce guide complet pour lier les données maîtres à une feuille
  de détail et générer des fichiers Excel.
og_title: Créer un classeur maître‑détail avec Aspose.Cells (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create master detail workbook in Java using Aspose.Cells Smart Marker.
    Learn step‑by‑step how to bind master data to a detail sheet and export Excel.
  headline: Create master detail workbook with Aspose.Cells (Java)
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
title: Créer un classeur maître‑détail avec Aspose.Cells (Java)
url: /fr/java/templates-reporting/create-master-detail-workbook-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur maître‑détail avec Aspose.Cells (Java)

Si vous devez **créer un classeur maître‑détail** en Java, vous êtes au bon endroit. Que vous construisiez un tableau de bord commercial, un générateur de factures, ou tout outil de reporting nécessitant une vue maître‑détail, ce guide vous accompagnera à travers tout le processus—sans fioritures, juste du code solide et exécutable.

Dans ce tutoriel, nous utiliserons **Aspose.Cells Smart Marker**, une fonctionnalité puissante qui vous permet d’insérer des espaces réservés de données directement dans un modèle Excel. À la fin, vous comprendrez comment configurer la relation maître‑détail, lier une liste de POJO comme source de données, et exporter un fichier .xlsx propre prêt à être consommé en aval.

## Ce que vous allez apprendre

- Comment initialiser un classeur et ajouter une feuille de détail.  
- Comment insérer un Smart Marker qui lie les lignes maîtres à la feuille de détail.  
- Comment fournir une liste d'objets `Order` comme source de données du Smart Marker.  
- Comment recalculer les formules qui dépendent des données insérées.  
- Comment enregistrer le fichier final avec la relation maître‑détail intacte.  

**Prérequis :** Java 17 (ou plus récent), Maven ou Gradle, et une licence valide d’Aspose.Cells pour Java (l’essai gratuit fonctionne pour les tests). Si vous n’avez jamais utilisé Aspose.Cells auparavant, ne vous inquiétez pas—ce guide suppose uniquement des connaissances de base en Java.

---

![Créer un diagramme de classeur maître‑détail](create_master_detail_workbook.png "Diagramme montrant le flux du classeur maître‑détail")

## Créer un classeur maître‑détail – Étape 1 : Initialiser le classeur

La première chose dont nous avons besoin est une nouvelle instance de `Workbook`. Considérez le classeur comme la toile sur laquelle vivront les feuilles maître et détail.

```java
import com.aspose.cells.*;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and add the master and detail worksheets
        Workbook workbook = new Workbook();                 // empty workbook with a default sheet
        Worksheet masterSheet = workbook.getWorksheets().get(0); // the first sheet becomes the master
        Worksheet detailSheet = workbook.getWorksheets().add("Details"); // add a detail sheet
```

*Pourquoi c’est important :* Aspose.Cells crée toujours une feuille par défaut, nous la réutilisons donc comme maître. Ajouter une feuille de détail nommée (`"Details"`) rend la référence du Smart Marker ultérieure plus claire et garde le fichier ordonné.

> **Astuce :** Si vous avez déjà un fichier modèle, remplacez `new Workbook()` par `new Workbook("template.xlsx")`. Le reste des étapes reste identique.

## Insérer un Smart Marker – Étape 2 : Lier les lignes maîtres à la feuille de détail

Les Smart Markers sont des espaces réservés que Aspose.Cells remplace par des données à l’exécution. La syntaxe `${DataSource,DetailSheet=SheetName}` indique au moteur quelles données extraire et où placer les lignes de détail.

```java
        // Step 2: Insert the Smart Marker that links the master data to the detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");
```

*Pourquoi c’est important :* Placer le marqueur en `A2` signifie que la ligne maître commencera juste en dessous de la ligne d’en-tête (généralement `A1`). La partie `DetailSheet=Details` crée automatiquement une **relation maître‑détail**—chaque ligne maître génère un bloc de lignes dans la feuille `Details`.

> **Question fréquente :** *Puis-je placer le marqueur dans une colonne différente ?* Absolument. Il suffit d’ajuster la référence de cellule (`B2`, `C2`, etc.) et de vous assurer que la mise en page de votre modèle correspond.

## Fournir la source de données – Étape 3 : Lier les POJO au Smart Marker

Nous alimentons maintenant le Smart Marker avec de vraies données. Dans cet exemple, nous utilisons une liste de POJO `Order` renvoyée par une classe d’assistance `DataFactory`.

```java
        // Step 3: Provide the data source for the Smart Marker (a list of Order objects)
        List<Order> orders = DataFactory.getOrders();   // your POJO list
        workbook.getSmartMarkers().setDataSource("Orders", orders);
```

*Pourquoi c’est important :* La clé `"Orders"` doit correspondre au nom utilisé à l’intérieur du placeholder `${...}`. Aspose.Cells parcourra la liste, créant une ligne maître pour chaque `Order` et extrayant les données enfants associées (le cas échéant) dans la feuille de détail.

> **Cas particulier :** Si votre liste est vide, le Smart Marker laissera simplement la zone maître vide—aucune exception n’est levée. Cependant, vous pourriez vouloir vérifier `orders.isEmpty()` au préalable pour décider s’il faut générer un fichier ou non.

## Recalculer les formules – Étape 4 : Maintenir les calculs à jour

Souvent, les feuilles maître‑détail contiennent des formules qui additionnent des quantités, calculent des totaux ou appliquent des taxes. Après que le Smart Marker a injecté les données, nous devons recalculer ces formules.

```java
        // Step 4: Recalculate any formulas that may depend on the inserted data
        workbook.calculateFormula();
```

*Pourquoi c’est important :* Sans cet appel, les cellules qui référencent les nouvelles lignes insérées afficheraient encore les anciennes valeurs (ou #DIV/0!). `calculateFormula()` parcourt l’ensemble du classeur, garantissant que chaque cellule dépendante reflète les nouvelles données.

> **Note de performance :** Pour les classeurs volumineux, vous pouvez limiter le recalcul à une feuille spécifique en utilisant `worksheet.calculateFormula()`. Dans la plupart des scénarios maître‑détail, l’appel sur le classeur complet convient.

## Enregistrer le fichier – Étape 5 : Exporter le classeur maître‑détail

Enfin, écrivez le classeur sur le disque. Vous pouvez choisir n’importe quel format supporté (`.xlsx`, `.xls`, `.csv`, etc.)—ici nous restons avec le moderne `.xlsx`.

```java
        // Step 5: Save the workbook with the master‑detail relationship applied
        workbook.save("output/master-detail.xlsx"); // adjust path as needed
    }
}
```

*Pourquoi c’est important :* Le fichier enregistré contient maintenant deux feuilles : **Sheet1** (le maître) et **Details** (le détail). L’ouvrir dans Excel affichera une vue maître‑détail bien formatée, avec toutes les formules que vous avez recalculées.

> **Pièges :** Si vous oubliez d’appeler `calculateFormula()` avant d’enregistrer, Excel recalculera à l’ouverture, ce qui peut être plus lent et produire des résultats différents si le classeur contient des fonctions volatiles.

---

## Code source complet (exécutable)

En assemblant toutes les pièces, voici le programme complet que vous pouvez copier‑coller dans votre IDE :

```java
import com.aspose.cells.*;
import java.util.List;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize workbook and worksheets
        Workbook workbook = new Workbook();
        Worksheet masterSheet = workbook.getWorksheets().get(0);
        Worksheet detailSheet = workbook.getWorksheets().add("Details");

        // Optional: Add headers to master sheet
        masterSheet.getCells().get("A1").putValue("Order ID");
        masterSheet.getCells().get("B1").putValue("Customer");
        masterSheet.getCells().get("C1").putValue("Total");

        // Step 2: Insert Smart Marker linking to detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");

        // Step 3: Supply data source (list of Order POJOs)
        List<Order> orders = DataFactory.getOrders(); // assume this returns a populated list
        workbook.getSmartMarkers().setDataSource("Orders", orders);

        // Step 4: Recalculate formulas (if any)
        workbook.calculateFormula();

        // Step 5: Save the resulting workbook
        workbook.save("output/master-detail.xlsx");
    }
}
```

**Sortie attendue :** Ouvrez `master-detail.xlsx` et vous verrez :

- **Sheet1** (maître) répertoriant chaque ID de commande, le nom du client et le total.  
- **Details** (détail) contenant les lignes appartenant à chaque commande (par ex., articles de ligne).  
- Toutes les formules de total ou de taxe correctement renseignées.

---

## Variantes fréquemment posées

| Question | Réponse |
|----------|--------|
| *Puis-je utiliser un modèle au lieu d’un classeur vierge ?* | Oui. Chargez‑le avec `new Workbook("template.xlsx")` et placez le Smart Marker dans la cellule appropriée. |
| *Et si mes données de détail se trouvent dans une liste séparée ?* | Vous pouvez imbriquer des Smart Markers : `${Orders.Details,DetailSheet=Details}` où `Details` est une propriété de chaque `Order` renvoyant une liste d’articles. |
| *Comment styliser les lignes de détail ?* | Appliquez un style à la première ligne de détail dans le modèle ; Aspose.Cells dupliquera ce style pour chaque ligne générée. |
| *Existe‑t‑il un moyen de masquer la feuille de détail jusqu’à ce qu’une ligne maître soit développée ?* | Pas directement via les Smart Markers, mais vous pouvez définir la propriété `Visible` de la feuille à `false` et la basculer avec VBA après l’ouverture. |

## Conclusion

Vous savez maintenant **comment créer un classeur maître‑détail** en Java en utilisant Aspose.Cells Smart Marker. De l’initialisation du classeur, l’insertion du Smart Marker, la liaison d’une liste de POJO, le recalcul des formules, jusqu’à l’enregistrement final du fichier—chaque étape a été expliquée avec le *pourquoi* qui la sous-tend, afin que vous puissiez adapter le modèle à vos propres projets.

Ensuite, essayez d’étendre cet exemple :

- Ajoutez une mise en forme conditionnelle pour mettre en évidence les commandes de grande valeur.  
- Exportez le classeur au format PDF avec `workbook.save("report.pdf", SaveFormat.PDF)`.  
- Combinez plusieurs sections maître‑détail dans un même fichier en utilisant différents noms de Smart Marker.  

Les concepts de **master‑

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec Aspose.Cells en Java : guide étape par étape](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Manipulation de fichiers Excel maîtres avec Aspose.Cells pour Java \| Guide des opérations de classeur](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java \| Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}