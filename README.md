adelyounes
==========

smb214


 
---
Projet comprend les étapes suivantes:

Premiere: presenter et expliquer le JFX  et comprend le PLAN suivants:


- Java FX
- Langage de programmation de script 
- Data binding 
- Héritage et héritage mixin 
- Access modifiers 
- GUI avec Java FX 1 
-Langage de programmation de script




deuxièmement: Faire un tutorial basé sur le JFX:

Où puis-je dessine, je peux entrer les informations et modifié par l'introduction des boîtes, et je le lance à travers le développement de code dans le NetBeans, et ce code est dans le fichier nommé "TableViewSample.java ",Mais comment?
1- Ouvrir le netBeans
2-Creer un nouveau projet: file-New Project--choisir "JavaFX-JavaFX Application" et le nommer:"TableViewSample"
3-Copiez le code du fichier "TableViewSample.java" à cette projet.
4-Execute ce projet.

Une description de ce programme:
-Le fragment de code dans ce tutorial est crée une table vide avec trois colonnes et l'ajoute à la scène de l'application.
-Le contrôle de la table est créée par instanciation de la classe TableView. Dans ce tutorial , il est ajouté au conteneur de disposition VBox, cependant, vous pouvez l'ajouter directement à la scène de l'application. 

Exemple définit trois colonnes pour stocker les informations suivantes dans un carnet d'adresses: prénom d'un contact et prénom, et une adresse e-mail. Les colonnes sont créées en utilisant la classe TableColumn. 

La méthode de la classe TableView de getColumns ajoute les colonnes créées précédemment à la table. Dans vos applications, vous pouvez utiliser cette méthode pour ajouter et supprimer des colonnes.
et la premiere partie de code qui fait ca est:

 Adding a Table

-import javafx.application.Application;
-import javafx.geometry.Insets;
-import javafx.scene.Group;
-import javafx.scene.Scene;
-import javafx.scene.control.Label;
-import javafx.scene.control.TableColumn;
-import javafx.scene.control.TableView;
-import javafx.scene.layout.VBox;
-import javafx.scene.text.Font;
-import javafx.stage.Stage;
 
public class TableViewSample extends Application {
 
    private TableView table = new TableView();
    public static void main(String[] args) {
        launch(args);
    }
 
    @Override
    public void start(Stage stage) {
        Scene scene = new Scene(new Group());
        stage.setTitle("Table View Sample");
        stage.setWidth(300);
        stage.setHeight(500);
 
        final Label label = new Label("Address Book");
        label.setFont(new Font("Arial", 20));
 
        table.setEditable(true);
 
        TableColumn firstNameCol = new TableColumn("First Name");
        TableColumn lastNameCol = new TableColumn("Last Name");
        TableColumn emailCol = new TableColumn("Email");
        
        table.getColumns().addAll(firstNameCol, lastNameCol, emailCol);
 
        final VBox vbox = new VBox();
        vbox.setSpacing(5);
        vbox.setPadding(new Insets(10, 0, 0, 10));
        vbox.getChildren().addAll(label, table);
 
        ((Group) scene.getRoot()).getChildren().addAll(vbox);
 
        stage.setScene(scene);
        stage.show();
    }
}

-Vous pouvez gérer la visibilité des colonnes en appelant la méthode setVisible. Par exemple, si la logique de votre application nécessite cacher adresses e-mail de l'utilisateur, vous pouvez mettre en œuvre cette tâche comme suit: emailCol.setVisible (false). 

Lorsque la structure de vos données nécessite une représentation plus complexe, vous pouvez créer des colonnes imbriquées. 

Par exemple, supposons que les contacts dans le carnet d'adresses ont deux comptes de messagerie. Ensuite, vous avez besoin de deux colonnes pour afficher les adresses primaire et le secondaire email

le code:
TableColumn firstEmailCol = new TableColumn("Primary");
TableColumn secondEmailCol = new TableColumn("Secondary");

emailCol.getColumns().addAll(firstEmailCol, secondEmailCol);

