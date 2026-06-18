---
date: '2026-05-28'
description: Apprenez à configurer le single page view PDF, modifier les viewer preferences,
  éditer les bookmarks et configurer les PDF settings en utilisant Aspose.PDF for
  Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Single page view PDF en Java – Modifier la mise en page et les signets
url: /fr/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Vue page unique PDF en Java – Modifier la mise en page et éditer les signets

## Introduction
Lorsque les lecteurs ouvrent un PDF volumineux, la mise en page par défaut du visualiseur peut défiler de façon continue, rendant difficile la concentration sur une seule page. En configurant le paramètre **single page view pdf**, vous forcez le visualiseur à afficher une page à la fois, ce qui est idéal pour les rapports, les e‑books et les catalogues. Dans ce tutoriel, vous apprendrez également à modifier les signets PDF existants, à définir des destinations de signets lors de la création d’un document, et à ajuster d’autres préférences du visualiseur à l’aide d’Aspose.PDF pour Java. À la fin, vous disposerez d’un contrôle complet sur la navigation, la précision des signets et la mise en page à l’écran.

**Ce que vous apprendrez**
- Comment modifier les signets PDF existants afin qu’ils pointent vers le début d’une page.  
- Comment définir les destinations des signets lors de la création d’un PDF.  
- Comment changer les préférences du visualiseur, comme la mise en page à page unique.  
- Conseils pratiques pour charger un document PDF en Java et optimiser les performances.

### Réponses rapides
- **Quelle est la méthode principale pour activer la vue page unique PDF ?** Appelez `PdfContentEditor.changeViewerPreference()` avec `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Les destinations des signets peuvent‑elles être modifiées après la génération d’un PDF ?** Oui – chargez le document, récupérez le plan, et assignez un nouveau `ExplicitDestination`.  
- **Ai‑je besoin d’une licence pour ces fonctionnalités ?** Un essai gratuit suffit pour l’évaluation ; une licence complète supprime toutes les limitations.  
- **Quelle dépendance Maven est requise ?** `com.aspose:aspose-pdf:25.3` (ou version ultérieure).  
- **Cette fonctionnalité est‑elle compatible avec Java 11 et supérieur ?** Absolument – Aspose.PDF prend en charge Java 8+.

## Qu’est‑ce que « modifier la mise en page PDF » ?
Modifier la mise en page PDF contrôle la façon dont les pages sont affichées dans un visualiseur : page unique, continue, affichage double page, etc. Activer **single page view pdf** améliore la lisibilité des documents longs et garantit que chaque page est présentée isolément, ce qui est particulièrement utile sur les appareils mobiles et les tablettes.

## Pourquoi modifier les signets PDF et définir des destinations de signets ?
Les signets fonctionnent comme une table des matières dynamique. Des destinations précises permettent aux lecteurs de sauter directement à la section souhaitée, éliminant le défilement supplémentaire et réduisant la frustration. Cela conduit à une navigation plus fluide et à une plus grande satisfaction pour les manuels techniques, les catalogues de produits et les livres numériques.

## Prérequis
- **Bibliothèques et dépendances** : Aspose.PDF for Java v25.3 ou ultérieure.  
- **Environnement** : JDK 8 ou plus récent, outil de construction Maven ou Gradle.  
- **Connaissances** : programmation Java de base et familiarité avec les concepts PDF.

## Configuration d’Aspose.PDF pour Java
### Installation Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Installation Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Acquisition de licence** : Commencez avec un essai gratuit ou demandez une licence temporaire pour un accès complet aux fonctionnalités. Envisagez d’acheter une licence permanente pour une utilisation en production.

### Initialisation de base
La classe `Document` est l’objet central d’Aspose.PDF qui représente un fichier PDF en mémoire. Après avoir créé une instance, toutes les opérations de lecture/écriture passent par cet objet.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Guide d’implémentation
### Comment modifier la mise en page PDF en Java
**Vue d’ensemble** : Ajustez les préférences du visualiseur pour afficher les pages comme vous le souhaitez.

#### Initialisation de PdfContentEditor
`PdfContentEditor` est une classe utilitaire qui vous permet de modifier les paramètres du visualiseur sans réécrire l’ensemble du document.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Modification des préférences du visualiseur
Pour activer **single page view pdf**, invoquez `changeViewerPreference()` avec la valeur d’énumération appropriée. Cette appel met à jour le dictionnaire interne des préférences du visualiseur du PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Enregistrement du document mis à jour
Après avoir modifié les préférences, appelez `save()` pour écrire les changements sur le disque.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Comment modifier les signets PDF
**Réponse** : Pour modifier les signets existants, chargez le PDF avec `Document`, récupérez sa collection de plan, localisez le `OutlineItem` souhaité, et assignez un nouveau `ExplicitDestination` qui pointe vers la bonne page et les bonnes coordonnées. Après la mise à jour de chaque signet, enregistrez le document pour persister les changements. Cela garantit que les utilisateurs sont dirigés précisément vers les sections prévues sans défilement supplémentaire.

#### Accès aux signets
`OutlineItemCollection` représente l’arbre hiérarchique des signets. Récupérez‑le depuis l’objet `Document` pour travailler avec les entrées individuelles.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Définir une nouvelle destination
Un `ExplicitDestination` définit la page exacte et l’emplacement qu’un signet doit atteindre. Assignez‑le à la propriété `Destination` de l’élément de plan.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Enregistrement des modifications
Persistez l’arbre de signets mis à jour en appelant `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Comment définir la destination d’un signet lors de la création d’un PDF
**Réponse** : Lors de la génération d’un PDF, vous pouvez créer des signets à la volée en instanciant des objets `OutlineItem`, en définissant leurs titres, et en définissant un `ExplicitDestination` qui cible une page spécifique et un mode de visualisation. Ajoutez chaque signet à la collection de plan du document avant d’enregistrer, afin que le fichier résultant contienne un arbre de navigation prêt à l’emploi.

#### Création et configuration du signet
`OutlineItem` représente une entrée de signet unique dans le plan PDF. Lors de la construction d’un PDF à partir de zéro, créez un nouveau `OutlineItem` et ajoutez‑le à la collection de plan du document.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Définition de la destination du signet
Utilisez `ExplicitDestination.createFitH(page, top)` pour positionner la vue en haut de la page cible.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Ajout et enregistrement du PDF
Enfin, ajoutez le signet au plan et enregistrez le document.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Applications pratiques
1. **Livres numériques** – Garantir que chaque signet de chapitre atterrit en haut de la page pour une expérience de lecture fluide.  
2. **Manuels techniques** – Une navigation précise aide les ingénieurs à trouver rapidement les sections, surtout dans les gros PDFs.  
3. **Catalogues de produits** – La mise en page à page unique rend la navigation dans les catalogues sur tablette plus intuitive.

## Considérations de performance
- **Optimisation des ressources** : Aspose.PDF peut traiter des PDFs jusqu’à 2 Go sans charger le fichier entier en mémoire, grâce à son architecture de streaming. Utilisez `Document.optimizeResources()` pour réduire davantage l’empreinte mémoire.  
- **Gestion de la mémoire Java** : Fermez explicitement les flux et laissez le ramasse‑miettes récupérer les objets après le traitement afin d’éviter les fuites de mémoire.

## Problèmes courants et solutions
- **Signets non mis à jour** : Vérifiez que vous modifiez le bon index du plan (`get_Item(1)` fait référence au premier signet de niveau supérieur).  
- **Préférence du visualiseur non appliquée** : Assurez‑vous d’appeler `editor.save()` après avoir modifié les préférences ; sinon les changements restent uniquement en mémoire.  
- **Exceptions de licence** : Une licence d’essai peut ajouter des filigranes ; obtenez une licence complète pour la production.

## Questions fréquemment posées
**Q : Quelle est la façon la plus simple de charger un document PDF en Java ?**  
R : Utilisez `new Document("path/to/file.pdf")` ; Aspose.PDF détecte automatiquement le format du fichier.  

**Q : Puis‑je changer la mise en page sans utiliser PdfContentEditor ?**  
R : Oui, vous pouvez définir les préférences du visualiseur directement sur l’objet `Document` via `pdfDocument.getViewerPreferences().setPageLayout(...)`.  

**Q : Le changement de la mise en page du visualiseur affecte‑t‑il l’impression ?**  
R : La mise en page du visualiseur n’influence que l’affichage à l’écran ; elle ne modifie pas la sortie imprimée.  

**Q : Existe‑t‑il des limites au nombre de signets que je peux créer ?**  
R : Aucun plafond explicite, mais des arbres de plan très volumineux peuvent impacter les performances ; il est recommandé de les garder organisés.  

**Q : Comment garantir que les destinations des signets sont précises après l’ajout ou la suppression de pages ?**  
R : Recalculez les destinations en utilisant les indices de page actuels après toute modification structurelle.

## Ressources
- **Documentation** : [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Téléchargement** : [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Acheter une licence Aspose.PDF** : [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Essai gratuit** : [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Demander une licence temporaire** : [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Dernière mise à jour :** 2026-05-28  
**Testé avec :** Aspose.PDF for Java v25.3  
**Auteur :** Aspose

## Tutoriels associés

- [Comment modifier les préférences du visualiseur PDF avec Aspose.PDF pour Java : guide complet](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Comment créer des signets PDF et gérer la navigation avec Aspose.PDF pour Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Tutoriels sur les signets PDF et la navigation pour Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}