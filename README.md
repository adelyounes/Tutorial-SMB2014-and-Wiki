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

 -Adding a Table:

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.layout.VBox;
import javafx.scene.text.Font;
import javafx.stage.Stage;
 
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

Par exemple, supposons que les contacts dans le carnet d'adresses ont deux comptes de messagerie. Ensuite, vous avez besoin de deux colonnes pour afficher les adresses primaire et le secondaire email.

le code:
TableColumn firstEmailCol = new TableColumn("Primary");
TableColumn secondEmailCol = new TableColumn("Secondary");

emailCol.getColumns().addAll(firstEmailCol, secondEmailCol);


-Définition du modèle de données 
Lorsque vous créez une table dans une application JavaFX, il est recommandé de mettre en œuvre une classe qui définit le modèle de données et fournit des méthodes et des champs de travailler davantage avec la table. 

public static class Person {
    private final SimpleStringProperty firstName;
    private final SimpleStringProperty lastName;
    private final SimpleStringProperty email;
 
    private Person(String fName, String lName, String email) {
        this.firstName = new SimpleStringProperty(fName);
        this.lastName = new SimpleStringProperty(lName);
        this.email = new SimpleStringProperty(email);
    }
 
    public String getFirstName() {
        return firstName.get();
    }
    public void setFirstName(String fName) {
        firstName.set(fName);
    }
        
    public String getLastName() {
        return lastName.get();
    }
    public void setLastName(String fName) {
        lastName.set(fName);
    }
    
    public String getEmail() {
        return email.get();
    }
    public void setEmail(String fName) {
        email.set(fName);
    }
        
}
-Le nom, prénom, e-mail et les propriétés de chaîne sont créés pour permettre le référencement d'un élément de données en particulier. 

En outre, les méthodes get et set sont prévus pour chaque élément de données. Ainsi, par exemple, la méthode getFirstName renvoie la valeur de la propriété prenom, et la méthode de setFirstName spécifie une valeur pour cette propriété. 

Lorsque le modèle de données est décrite dans la classe de la personne, vous pouvez créer un tableau ObservableList et définir le nombre de lignes de données que vous souhaitez montrer à votre table.

final ObservableList<Person> data = FXCollections.observableArrayList(
    new Person("Jacob", "Smith", "jacob.smith@example.com"),
    new Person("Isabella", "Johnson", "isabella.johnson@example.com"),
    new Person("Ethan", "Williams", "ethan.williams@example.com"),
    new Person("Emma", "Jones", "emma.jones@example.com"),
    new Person("Michael", "Brown", "michael.brown@example.com")
);

-L'étape suivante consiste à associer les données avec les colonnes de la table. Vous pouvez le faire à travers les propriétés définies pour chaque donnée élémentaire

-firstNameCol.setCellValueFactory(
    new PropertyValueFactory<Person,String>("firstName")
);
lastNameCol.setCellValueFactory(
    new PropertyValueFactory<Person,String>("lastName")
);
emailCol.setCellValueFactory(
    new PropertyValueFactory<Person,String>("email")
);
-Procédé setCellValueFactory spécifie une fabrique de cellules pour chaque colonne. Les usines de cellules sont mises en œuvre à l'aide de la classe PropertyValueFactory, qui utilise le nom, prénom, et les propriétés électroniques des colonnes de la table comme des références aux méthodes correspondantes de la classe de la personne. 

Lorsque le modèle de données est définie, et les données sont ajoutées et associée avec les colonnes, on peut ajouter les données de la table en utilisant la méthode de la classe des TableView setItems: table.setItems (données). 

Parce que l'objet de ObservableList permet le suivi de toutes les modifications apportées à ses éléments, le contenu TableView met à jour automatiquement à chaque modification de données.

import javafx.application.Application;
import javafx.beans.property.SimpleStringProperty;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.geometry.Insets;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.TextField;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.layout.VBox;
import javafx.scene.text.Font;
import javafx.stage.Stage;
 
public class TableViewSample extends Application {
 
    private TableView<Person> table = new TableView<Person>();
    private final ObservableList<Person> data =
        FXCollections.observableArrayList(
            new Person("Jacob", "Smith", "jacob.smith@example.com"),
            new Person("Isabella", "Johnson", "isabella.johnson@example.com"),
            new Person("Ethan", "Williams", "ethan.williams@example.com"),
            new Person("Emma", "Jones", "emma.jones@example.com"),
            new Person("Michael", "Brown", "michael.brown@example.com")
        );
   
    public static void main(String[] args) {
        launch(args);
    }
 
    @Override
    public void start(Stage stage) {
        Scene scene = new Scene(new Group());
        stage.setTitle("Table View Sample");
        stage.setWidth(450);
        stage.setHeight(500);
 
        final Label label = new Label("Address Book");
        label.setFont(new Font("Arial", 20));
 
        table.setEditable(true);
 
        TableColumn firstNameCol = new TableColumn("First Name");
        firstNameCol.setMinWidth(100);
        firstNameCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("firstName"));
 
        TableColumn lastNameCol = new TableColumn("Last Name");
        lastNameCol.setMinWidth(100);
        lastNameCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("lastName"));
 
        TableColumn emailCol = new TableColumn("Email");
        emailCol.setMinWidth(200);
        emailCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("email"));
 
        table.setItems(data);
        table.getColumns().addAll(firstNameCol, lastNameCol, emailCol);
 
        final VBox vbox = new VBox();
        vbox.setSpacing(5);
        vbox.setPadding(new Insets(10, 0, 0, 10));
        vbox.getChildren().addAll(label, table);
 
        ((Group) scene.getRoot()).getChildren().addAll(vbox);
 
        stage.setScene(scene);
        stage.show();
    }
 
    public static class Person {
 
        private final SimpleStringProperty firstName;
        private final SimpleStringProperty lastName;
        private final SimpleStringProperty email;
 
        private Person(String fName, String lName, String email) {
            this.firstName = new SimpleStringProperty(fName);
            this.lastName = new SimpleStringProperty(lName);
            this.email = new SimpleStringProperty(email);
        }
 
        public String getFirstName() {
            return firstName.get();
        }
 
        public void setFirstName(String fName) {
            firstName.set(fName);
        }
 
        public String getLastName() {
            return lastName.get();
        }
 
        public void setLastName(String fName) {
            lastName.set(fName);
        }
 
        public String getEmail() {
            return email.get();
        }
 
        public void setEmail(String fName) {
            email.set(fName);
        }
    }
}
Vous pouvez utiliser les champs de texte pour saisir de nouvelles valeurs dans le Prénom, Nom, et des colonnes de messagerie. Le contrôle de zone de texte permet à votre application pour recevoir une entrée de texte à partir d'un utilisateur.

final TextField addFirstName = new TextField();
addFirstName.setPromptText("First Name");
addFirstName.setMaxWidth(firstNameCol.getPrefWidth());
final TextField addLastName = new TextField();
addLastName.setMaxWidth(lastNameCol.getPrefWidth());
addLastName.setPromptText("Last Name");
final TextField addEmail = new TextField();
addEmail.setMaxWidth(emailCol.getPrefWidth());
addEmail.setPromptText("Email");
 
final Button addButton = new Button("Add");
addButton.setOnAction(new EventHandler<ActionEvent>() {
    @Override public void handle(ActionEvent e) {
        data.add(new Person(
            addFirstName.getText(),
            addLastName.getText(),
            addEmail.getText()
        ));
        addFirstName.clear();
        addLastName.clear();
        addEmail.clear();
    }
});

Quand un utilisateur clique sur le bouton Ajouter, les valeurs saisies dans les champs de texte sont inclus dans un constructeur personne et ajoutés à la liste des données observables. Ainsi, la nouvelle entrée des informations de contact apparaît dans la table.

import javafx.application.Application;
import javafx.beans.property.SimpleStringProperty;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.TextField;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.scene.text.Font;
import javafx.stage.Stage;
 
public class FileChooserSample extends Application {
 
    private TableView<Person> table = new TableView<Person>();
    private final ObservableList<Person> data =
            FXCollections.observableArrayList(
            new Person("Jacob", "Smith", "jacob.smith@example.com"),
            new Person("Isabella", "Johnson", "isabella.johnson@example.com"),
            new Person("Ethan", "Williams", "ethan.williams@example.com"),
            new Person("Emma", "Jones", "emma.jones@example.com"),
            new Person("Michael", "Brown", "michael.brown@example.com"));
    final HBox hb = new HBox();
 
    public static void main(String[] args) {
        launch(args);
    }
 
    @Override
    public void start(Stage stage) {
        Scene scene = new Scene(new Group());
        stage.setTitle("Table View Sample");
        stage.setWidth(450);
        stage.setHeight(550);
 
        final Label label = new Label("Address Book");
        label.setFont(new Font("Arial", 20));
 
        table.setEditable(true);
 
        TableColumn firstNameCol = new TableColumn("First Name");
        firstNameCol.setMinWidth(100);
        firstNameCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("firstName"));
 
        TableColumn lastNameCol = new TableColumn("Last Name");
        lastNameCol.setMinWidth(100);
        lastNameCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("lastName"));
 
        TableColumn emailCol = new TableColumn("Email");
        emailCol.setMinWidth(200);
        emailCol.setCellValueFactory(
                new PropertyValueFactory<Person, String>("email"));
 
        table.setItems(data);
        table.getColumns().addAll(firstNameCol, lastNameCol, emailCol);
 
        final TextField addFirstName = new TextField();
        addFirstName.setPromptText("First Name");
        addFirstName.setMaxWidth(firstNameCol.getPrefWidth());
        final TextField addLastName = new TextField();
        addLastName.setMaxWidth(lastNameCol.getPrefWidth());
        addLastName.setPromptText("Last Name");
        final TextField addEmail = new TextField();
        addEmail.setMaxWidth(emailCol.getPrefWidth());
        addEmail.setPromptText("Email");
 
        final Button addButton = new Button("Add");
        addButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent e) {
                data.add(new Person(
                        addFirstName.getText(),
                        addLastName.getText(),
                        addEmail.getText()));
                addFirstName.clear();
                addLastName.clear();
                addEmail.clear();
            }
        });
 
        hb.getChildren().addAll(addFirstName, addLastName, addEmail, addButton);
        hb.setSpacing(3);
 
        final VBox vbox = new VBox();
        vbox.setSpacing(5);
        vbox.setPadding(new Insets(10, 0, 0, 10));
        vbox.getChildren().addAll(label, table, hb);
 
        ((Group) scene.getRoot()).getChildren().addAll(vbox);
 
        stage.setScene(scene);
        stage.show();
    }
 
    public static class Person {
 
        private final SimpleStringProperty firstName;
        private final SimpleStringProperty lastName;
        private final SimpleStringProperty email;
 
        private Person(String fName, String lName, String email) {
            this.firstName = new SimpleStringProperty(fName);
            this.lastName = new SimpleStringProperty(lName);
            this.email = new SimpleStringProperty(email);
        }
 
        public String getFirstName() {
            return firstName.get();
        }
 
        public void setFirstName(String fName) {
            firstName.set(fName);
        }
 
        public String getLastName() {
            return lastName.get();
        }
 
        public void setLastName(String fName) {
            lastName.set(fName);
        }
 
        public String getEmail() {
            return email.get();
        }
 
        public void setEmail(String fName) {
            email.set(fName);
        }
    }
}

Modification des données dans le tableau:

-La classe TableView ne rend pas seulement des données tabulaires, mais il offre également des fonctionnalités pour le modifier. Utilisez la méthode setEditable pour permettre l'édition du contenu de la table. 

-Utilisez la méthode setCellFactory réimplémenter la cellule du tableau comme un champ de texte à l'aide de la classe TextFieldTableCell. La méthode de setOnEditCommit traite édition et attribue la valeur actualisée de la cellule correspondante de la table.

-firstNameCol.setCellFactory(TextFieldTableCell.forTableColumn());
firstNameCol.setOnEditCommit(
    new EventHandler<CellEditEvent<Person, String>>() {
        @Override
        public void handle(CellEditEvent<Person, String> t) {
            ((Person) t.getTableView().getItems().get(
                t.getTablePosition().getRow())
                ).setFirstName(t.getNewValue());
        }
    }
);

lastNameCol.setCellFactory(TextFieldTableCell.forTableColumn());
lastNameCol.setOnEditCommit(
    new EventHandler<CellEditEvent<Person, String>>() {
        @Override
        public void handle(CellEditEvent<Person, String> t) {
            ((Person) t.getTableView().getItems().get(
                t.getTablePosition().getRow())
                ).setLastName(t.getNewValue());
        }
    }
);

emailCol.setCellFactory(TextFieldTableCell.forTableColumn());
emailCol.setOnEditCommit(
    new EventHandler<CellEditEvent<Person, String>>() {
        @Override
        public void handle(CellEditEvent<Person, String> t) {
            ((Person) t.getTableView().getItems().get(
                t.getTablePosition().getRow())
                ).setEmail(t.getNewValue());
        }
    }
);.
