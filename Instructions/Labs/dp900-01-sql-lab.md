---
lab:
  title: Einführung in Azure SQL-Datenbank
  module: Explore relational data in Azure
---

# <a name="explore-azure-sql-database"></a>Einführung in Azure SQL-Datenbank

In dieser Übung stellen Sie eine Azure SQL-Datenbankressource in Ihrem Azure-Abonnement bereit und verwenden dann SQL, um die Tabellen in einer relationalen Datenbank abzufragen.

Dieses Lab dauert ungefähr **15** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## <a name="provision-an-azure-sql-database-resource"></a>Bereitstellen einer Azure SQL-Datenbankressource

1. In the <bpt id="p1">[</bpt>Azure portal<ept id="p1">](https://portal.azure.com?azure-portal=true)</ept>, select <bpt id="p2">**</bpt>&amp;#65291; Create a resource<ept id="p2">**</ept> from the upper left-hand corner and search for <bpt id="p3">*</bpt>Azure SQL<ept id="p3">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure SQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Überprüfen Sie die verfügbaren Azure SQL-Optionen. Vergewissern Sie sich, dass auf der Kachel **SQL-Datenbanken** die Option **Einzeldatenbank** ausgewählt ist, und klicken Sie auf **Erstellen**.

    ![Screenshot: Azure-Portal mit der Seite „Azure SQL“](images//azure-sql-portal.png)

1. Geben Sie auf der Seite **SQL-Datenbank erstellen** die folgenden Werte ein:
    - **Abonnement**: Wählen Sie Ihr Azure-Abonnement.
    - **Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe mit einem Namen Ihrer Wahl.
    - **Datenbankname**: *AdventureWorks*
    - <bpt id="p1">**</bpt>Server<ept id="p1">**</ept>:  Select <bpt id="p2">**</bpt>Create new<ept id="p2">**</ept> and create a new server with a unique name in any available location. Use <bpt id="p1">**</bpt>SQL authentication<ept id="p1">**</ept> and specify your name as the server admin login and a suitably complex password (remember the password - you'll need it later!)
    - **Möchten Sie einen Pool für elastische SQL-Datenbanken verwenden?**: *Nein*
    - **Compute + Speicher**: Lassen Sie den Wert unverändert.
    - **Redundanz für Sicherungsspeicher**: *Lokal redundanter Sicherungsspeicher*

1. On the <bpt id="p1">**</bpt>Create SQL Database<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Next :Networking &gt;<ept id="p2">**</ept>, and on the <bpt id="p3">**</bpt>Networking<ept id="p3">**</ept> page, in the <bpt id="p4">**</bpt>Network connectivity<ept id="p4">**</ept> section, select <bpt id="p5">**</bpt>Public endpoint<ept id="p5">**</ept>. Then select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> for both options in the <bpt id="p2">**</bpt>Firewall rules<ept id="p2">**</ept> section to allow access to your database server from Azure services and your current client IP address.

1. Klicken Sie auf **Weiter: Sicherheit >** , und legen Sie für **Microsoft Defender für SQL aktivieren** die Option **Nicht jetzt** fest.

1. Klicken Sie auf **Weiter: Zusätzliche Einstellungen >** . Legen Sie auf der Registerkarte **Zusätzliche Einstellungen** für **Vorhandene Daten verwenden** die Option **Beispiel** fest. Dadurch wird eine Beispieldatenbank erstellt, die Sie sich später ansehen können.

1. Klicken Sie zum Erstellen Ihrer Instanz von Azure SQL-Datenbank auf **Überprüfen + erstellen** und dann auf **Erstellen**.

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![Screenshot: Azure-Portal mit der Seite „SQL-Datenbank“](images//sql-database-portal.png)

1. Klicken Sie im linken Bereich auf **Abfrage-Editor (Vorschau)**. Melden Sie sich mit dem Administratornamen und dem Kennwort an, die Sie für Ihren Server angegeben haben.
    
    *Wird eine Fehlermeldung mit dem Hinweis angezeigt, dass die Client-IP-Adresse nicht zulässig ist, klicken Sie auf den Link **Liste zugelassener IP-Adressen...** am Ende der Nachricht, um den Zugriff zu gewähren. Versuchen Sie dann erneut, sich anzumelden. (Sie haben zwar zuvor die Client-IP-Adresse Ihres Computers den Firewallregeln hinzugefügt, doch je nach Netzwerkkonfiguration stellt der Abfrage-Editor möglicherweise eine Verbindung von einer anderen Adresse aus her.)*
    
    Der Abfrage-Editor sieht folgendermaßen aus:
    
    ![Screenshot: Azure-Portal mit dem Abfrage-Editor](images//query-editor.png)

1. Erweitern Sie den Ordner **Tabellen**, um die Tabellen in der Datenbank anzuzeigen.

1. Geben Sie im Bereich **Abfrage 1** den folgenden SQL-Code ein:

    ```sql
    SELECT * FROM SalesLT.Product;
    ```

1. Klicken Sie oberhalb der Abfrage auf **&#9655; Ausführen**, um die Abfrage auszuführen und die Ergebnisse anzuzeigen. Diese sollten wie nachstehend gezeigt sämtliche Spalten aller Zeilen der Tabelle **SalesLT.Product** enthalten:

    ![Screenshot: Azure-Portal mit dem Abfrage-Editor und den Abfrageergebnissen](images//sql-query-results.png)

1. Ersetzen Sie die SELECT-Anweisung durch den folgenden Code, und klicken Sie dann auf **&#9655; Ausführen**, um die neue Abfrage auszuführen und die Ergebnisse anzuzeigen (diese enthalten nur die Spalten **ProductID**, **Name**, **ListPrice** und **ProductCategoryID**):

    ```sql
    SELECT ProductID, Name, ListPrice, ProductCategoryID
    FROM SalesLT.Product;
    ```

1. Führen Sie nun die folgende Abfrage aus, die mithilfe von JOIN den Kategorienamen aus der Tabelle **SalesLT.ProductCategory** abruft:

    ```sql
    SELECT p.ProductID, p.Name AS ProductName,
            c.Name AS Category, p.ListPrice
    FROM SalesLT.Product AS p
    JOIN [SalesLT].[ProductCategory] AS c
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

1. Schließen Sie den Bereich des Abfrage-Editors, und verwerfen Sie Ihre Bearbeitungen.

> **Tipp**: Wenn Sie die Erkundung von Azure SQL-Datenbank abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen.
