---
lab:
  title: Einführung in Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>Einführung in Azure Cosmos DB

In dieser Übung stellen Sie eine Azure Cosmos DB-Datenbank in Ihrem Azure-Abonnement bereit und erkunden die verschiedenen Möglichkeiten, es zum Speichern nicht rationaler Daten zu verwenden.

Dieses Lab dauert ungefähr **15** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## <a name="create-a-cosmos-db-account"></a>Erstellen eines Cosmos DB-Kontos

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Wählen Sie auf der Kachel **Core (SQL) – empfohlen** die Option **Erstellen** aus.
1. Geben Sie die folgenden Details ein, und wählen Sie **Überprüfen und erstellen** aus:
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Ressourcengruppe**: Wenn Sie eine Sandbox verwenden, wählen Sie die vorhandene Ressourcengruppe aus (mit einem ähnlichen Namen wie *learn-xxxx....* ). Erstellen Sie andernfalls eine neue Ressourcengruppe mit einem Namen Ihrer Wahl.
    - **Kontoname**: Geben Sie einen eindeutigen Namen ein.
    - **Speicherort**: Wählen Sie einen beliebigen empfohlenen Speicherort aus.
    - **Kapazitätsmodus**: bereitgestellter Durchsatz
    - **Rabatt für Free-Tarif anwenden**: Wählen Sie „Anwenden“ aus, falls verfügbar.
    - **Beschränken des gesamten Kontodurchsatzes**: nicht ausgewählt
1. Wählen Sie nach dem Überprüfen der Konfiguration **Erstellen** aus.
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>Erstellen einer Beispieldatenbank

*Schließen Sie während dieses Vorgangs alle Tipps, die im Portal angezeigt werden*.

1. Wählen Sie auf der Seite für Ihr neues Cosmos DB-Konto im Bereich links die Option **Data Explorer** aus.
1. Wählen Sie auf der Seite **Data Explorer** die Option **Schnellstart** aus.
1. Überprüfen Sie auf der Registerkarte **Neuer Container** die vorausgefüllten Einstellungen für die Beispieldatenbank, und klicken Sie auf **OK**.
1. Beobachten Sie den Status im Bereich am unteren Bildschirmrand, bis die Datenbank **SampleDB** und der zugehörige Container **SampleContainer** erstellt wurden (dies kann etwa eine Minute dauern).

## <a name="view-and-create-items"></a>Anzeigen und Erstellen von Elementen

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
1. Wählen Sie eines der Elemente in der Liste aus, um eine JSON-Darstellung der Elementdaten anzuzeigen.
1. Wählen Sie oben auf der Seite **Neues Element aus**, um ein neues leeres Element zu erstellen.
1. Ändern Sie den JSON-Code für das neue Element wie folgt, und wählen Sie dann **Speichern** aus.

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. Nach dem Speichern des neuen Elements werden zusätzliche Metadateneigenschaften automatisch hinzugefügt.

## <a name="query-the-database"></a>Abfragen der Datenbank

1. Wählen Sie auf der Seite **Data Explorer** das Symbol **Neue SQL-Abfrage** aus.
1. Überprüfen Sie im SQL-Abfrage-Editor die Standardabfrage (`SELECT * FROM c`), und verwenden Sie die Schaltfläche `SELECT * FROM c`, um sie auszuführen.
1. Überprüfen Sie die Ergebnisse, zu denen die vollständige JSON-Darstellung aller Elemente gehört.
1. Ändern Sie die Abfrage wie folgt:

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. Verwenden Sie die Schaltfläche **Abfrage ausführen**, um die überarbeitete Abfrage auszuführen und die Ergebnisse zu überprüfen. Diese enthalten JSON-Entitäten für alle Elemente mit einem Feld **address**, das den Text „Any St.“ enthält.
1. Schließen Sie SQL-Abfrage-Editor, und verwerfen Sie Ihre Änderungen.

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> **Tipp**: Wenn Sie die Erkundung von Azure Cosmos DB abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen.
