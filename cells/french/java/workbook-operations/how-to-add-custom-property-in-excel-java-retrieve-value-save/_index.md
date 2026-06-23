---
category: general
date: 2026-06-18
description: Comment ajouter une propriété personnalisée dans Excel en Java. Apprenez
  à récupérer la valeur d’une propriété personnalisée et à enregistrer le classeur
  au format XLSB avec un exemple complet et exécutable.
draft: false
keywords:
- how to add custom property
- retrieve custom property value
- save workbook as xlsb
- create custom property in excel
language: fr
og_description: Comment ajouter une propriété personnalisée dans Excel en utilisant
  Java. Ce guide vous montre comment récupérer la valeur de la propriété personnalisée
  et enregistrer le classeur au format XLSB.
og_title: Comment ajouter une propriété personnalisée dans Excel (Java) – Étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add custom property in Excel using Java. Learn to retrieve custom
    property value and save workbook as XLSB with a complete, runnable example.
  headline: How to Add Custom Property in Excel (Java) – Retrieve Value & Save as
    XLSB
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Comment ajouter une propriété personnalisée dans Excel (Java) – Récupérer la
  valeur et enregistrer en XLSB
url: /fr/java/workbook-operations/how-to-add-custom-property-in-excel-java-retrieve-value-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter une propriété personnalisée dans Excel (Java) – Récupérer la valeur & enregistrer en XLSB

Comment ajouter une propriété personnalisée dans Excel à l’aide de Java est un besoin fréquent lorsque vous souhaitez étiqueter les feuilles de calcul avec des métadonnées. Dans ce tutoriel, nous récupérerons également la valeur de la propriété personnalisée et **enregistrerons le classeur au format XLSB**, afin que vous disposiez d’une solution complète, de bout en bout, que vous pouvez intégrer à n’importe quel projet.

Imaginez que vous construisez un moteur de reporting qui génère des dizaines de feuilles de calcul chaque nuit. Vous aimeriez intégrer un « ProjectId » ou « ReportVersion » directement dans le fichier afin que les systèmes en aval puissent les filtrer ou les auditer plus tard. C’est exactement ce que les propriétés personnalisées vous offrent — de petites pièces de données stockées à l’intérieur du classeur sans encombrer les cellules visibles.

Nous couvrirons :

* La création d’une propriété personnalisée dans Excel (exemple « ProjectId »).  
* La récupération de la valeur de cette propriété personnalisée pour vérifier son bon fonctionnement.  
* L’enregistrement du classeur modifié en tant que fichier **XLSB**, qui est le format binaire permettant de réduire la taille du fichier et d’accélérer les temps de chargement.  

**Prérequis**

* Java 17 ou version supérieure.  
* Aspose.Cells for Java (la bibliothèque qui vous permet de manipuler des fichiers Excel sans Microsoft Office).  
* Une licence valide d’Aspose.Cells — l’évaluation gratuite fonctionne pour cette démonstration, mais une licence supprime le filigrane d’évaluation.  

Si vous n’avez jamais utilisé Aspose.Cells auparavant, ne vous inquiétez pas. L’API est simple, et le code ci‑dessous est prêt à être exécuté après avoir ajouté le JAR à votre classpath.

![comment ajouter une propriété personnalisée dans Excel avec Java](image-url-placeholder "Comment ajouter une propriété personnalisée dans Excel avec Java")

---

## Comment ajouter une propriété personnalisée – Étape 1

Tout d’abord, nous devons charger un classeur existant (ou en créer un nouveau) puis y attacher une propriété personnalisée à la première feuille de calcul. La propriété n’est qu’une paire clé/valeur stockée dans la collection `CustomProperties` de la feuille.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook from a file (you can also create a new workbook)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        // This is the core of how to add custom property in Excel.
        sheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the value of the custom property we just added
        // (We'll also show you how to retrieve custom property value later.)
        Object projectIdValue = sheet.getCustomProperties().get("ProjectId").getValue();

        // Step 5: Display the retrieved value on the console
        System.out.println("ProjectId = " + projectIdValue);

        // Step 6: Save the modified workbook to a new file in XLSB format
        // This demonstrates how to save workbook as XLSB.
        workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
    }
}
```

**Pourquoi cela fonctionne**

* `Workbook` est le point d’entrée pour tout fichier Excel — pensez‑y comme le conteneur de toutes les feuilles, styles et métadonnées.  
* `Worksheet.getCustomProperties()` renvoie une collection qui se comporte comme un dictionnaire ; appeler `.add(name, value)` crée la propriété si elle n’existe pas.  
* La valeur de la propriété peut être de n’importe quel type primitif (int, double, String, boolean) — Aspose.Cells gère la conversion pour vous.  

L’exécution du programme affiche :

```
ProjectId = 12345
```

Vous avez maintenant **ajouté une propriété personnalisée** et confirmé qu’elle existe.

---

## Récupérer la valeur d’une propriété personnalisée

Vous vous demandez peut‑être : « Et si je dois lire la propriété plus tard, peut‑être dans un autre module ? » La même collection `CustomProperties` vous permet de récupérer la valeur par son nom. Le fragment ci‑dessous montre comment **récupérer la valeur d’une propriété personnalisée** sans la recréer.

```java
// Assume workbook is already loaded and sheet points to the correct worksheet
CustomPropertyCollection props = sheet.getCustomProperties();

// Check if the property exists to avoid NullPointerException
if (props.contains("ProjectId")) {
    Object value = props.get("ProjectId").getValue();
    System.out.println("Retrieved ProjectId = " + value);
} else {
    System.out.println("ProjectId property not found.");
}
```

**Points clés**

* `contains` est une précaution — dans le code réel, il faut toujours vérifier l’existence avant de lire.  
* L’`Object` retourné peut être casté au type attendu si vous avez besoin d’opérations arithmétiques (par ex., `(int) value`).  

Ce petit schéma résout la plupart des scénarios d’audit où vous devez extraire des métadonnées d’un classeur généré il y a plusieurs semaines.

---

## Enregistrer le classeur au format XLSB

Pourquoi choisir le XLSB plutôt que le plus répandu XLSX ? Les fichiers binaires XLSB sont généralement **30‑40 % plus petits** et s’ouvrent plus rapidement, surtout pour de gros ensembles de données. Aspose.Cells rend l’enregistrement dans ce format très simple, comme le montre la **Étape 6** du premier bloc de code.

Si vous devez conserver le classeur en mémoire (par exemple pour l’envoyer via un service web), vous pouvez écrire dans un `ByteArrayOutputStream` à la place :

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
workbook.save(baos, SaveFormat.XLSB);
byte[] xlsbBytes = baos.toByteArray();
// Now you can attach xlsbBytes to an email, upload to S3, etc.
```

L’énumération `SaveFormat.XLSB` garantit le format binaire, et le même appel fonctionne pour n’importe quel classeur, que vous veniez d’ajouter une propriété personnalisée ou d’effectuer des calculs intensifs.

---

## Créer une propriété personnalisée dans Excel – Exemple complet de bout en bout

Voici un programme complet, autonome, qui réunit **comment ajouter une propriété personnalisée**, **récupérer la valeur d’une propriété personnalisée**, et **enregistrer le classeur au format XLSB**. Copiez‑collez-le simplement dans votre IDE, ajustez les chemins de fichiers, et exécutez‑le immédiatement.

```java
import com.aspose.cells.*;

public class ExcelCustomPropertyExample {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load an existing XLSB workbook (or create a new one)
            Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

            // 2️⃣ Grab the first worksheet – you could loop through all sheets if needed
            Worksheet sheet = workbook.getWorksheets().get(0);

            // 3️⃣ Create a custom property called "ProjectId"
            // This is the essential step for how to add custom property.
            sheet.getCustomProperties().add("ProjectId", 12345);
            System.out.println("Custom property 'ProjectId' added.");

            // 4️⃣ Retrieve the property to prove it works – demonstrates retrieve custom property value
            CustomPropertyCollection props = sheet.getCustomProperties();
            if (props.contains("ProjectId")) {
                Object val = props.get("ProjectId").getValue();
                System.out.println("Retrieved ProjectId = " + val);
            }

            // 5️⃣ Optionally, add another property (string type) to show flexibility
            sheet.getCustomProperties().add("ReportVersion", "v2.1");
            System.out.println("Added ReportVersion property.");

            // 6️⃣ Save the workbook as an XLSB file – this is the save workbook as XLSB step.
            workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
            System.out.println("Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb");

        } catch (Exception e) {
            // Real‑world code should log the exception; here we just print stack trace.
            e.printStackTrace();
        }
    }
}
```

**Sortie console attendue**

```
Custom property 'ProjectId' added.
Retrieved ProjectId = 12345
Added ReportVersion property.
Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb
```

Ouvrez `customOut.xlsb` dans Excel, allez dans **Fichier → Infos → Propriétés → Propriétés avancées → Personnalisées**, et vous verrez à la fois `ProjectId` et `ReportVersion` listés — preuve que **créer une propriété personnalisée dans Excel** a bien fonctionné.

---

## Pièges courants & Astuces professionnelles

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| Oublier d’appeler `workbook.save(...)` | Le classeur reste en mémoire et aucune modification n’est écrite sur le disque. | Toujours appeler `workbook.save("chemin/fichier.xlsb")` après avoir ajouté ou modifié des propriétés. |
| Utiliser un type non pris en charge pour la valeur | Certaines valeurs (ex. objets complexes) ne sont pas sérialisables en tant que propriété personnalisée. | Limitez‑vous aux types primitifs (int, double, String, boolean) ou convertissez‑les en chaîne avant l’ajout. |
| Ignorer la vérification d’existence | Une tentative de lecture d’une propriété inexistante lève une exception. | Utilisez `if (worksheet.getCustomProperties().contains("NomPropriete")) { … }`. |
| Oublier la licence Aspose.Cells | En mode d’évaluation, un filigrane apparaît dans le fichier généré. | Appliquez votre licence avant d’exécuter le code (`License license = new License(); license.setLicense("Aspose.Cells.lic");`). |

---

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Gestion des propriétés personnalisées d’un classeur Excel avec Aspose.Cells .NET](/cells/english/net/workbook-operations/excel-workbook-property-management-aspose-cells-net/)
- [Comment exporter les propriétés personnalisées d’Excel vers PDF avec Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [Comment accéder aux propriétés personnalisées d’un document Excel avec Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}