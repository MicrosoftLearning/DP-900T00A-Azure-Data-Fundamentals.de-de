---
lab:
  title: Einführung in Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# Einführung in Azure Cosmos DB

In dieser Übung stellen Sie eine Azure Cosmos DB-Datenbank in Ihrem Azure-Abonnement bereit und erkunden die verschiedenen Möglichkeiten, es zum Speichern nicht rationaler Daten zu verwenden.

Dieses Lab dauert ungefähr **15** Minuten.

## Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## Erstellen eines Cosmos DB-Kontos

Damit Sie Cosmos DB verwenden können, müssen Sie in Ihrem Azure-Abonnement ein Cosmos DB-Konto bereitstellen. In dieser Übung stellen Sie ein Cosmos DB-Konto bereit, für das Azure Cosmos DB for NoSQL verwendet wird.

1. Wählen Sie oben links im Azure-Portal **+ Erstellen einer Ressource** und suchen Sie nach `Azure Cosmos DB`.  Wählen Sie in den Ergebnissen **Azure Cosmos DB** und dann **Erstellen** aus.
1. Wählen Sie in der **Azure Cosmos DB für NoSQL**-Kachel **Erstellen** aus.
1. Geben Sie die folgenden Details ein, und wählen Sie **Überprüfen und erstellen** aus:
    - **Workloadtyp**: Lernen
    - **Abonnement**: Wenn Sie eine Sandbox verwenden, wählen Sie die Option *Concierge-Abonnement* aus. Wenn Sie Ihr eigenes Azure-Abonnement verwenden, wählen Sie dieses aus.
    - **Ressourcengruppe**: Wenn Sie eine Sandbox verwenden, wählen Sie die vorhandene Ressourcengruppe aus (mit einem ähnlichen Namen wie *learn-xxxx....* ). Erstellen Sie andernfalls eine neue Ressourcengruppe mit einem Namen Ihrer Wahl.
    - **Kontoname**: Geben Sie einen eindeutigen Namen ein.
    - **Speicherort**: Wählen Sie einen beliebigen empfohlenen Speicherort aus.
    - **Kapazitätsmodus**: bereitgestellter Durchsatz
    - **Rabatt für Free-Tarif anwenden**: Wählen Sie „Anwenden“ aus, falls verfügbar.
    - **Beschränken des gesamten Kontodurchsatzes**: nicht ausgewählt
1. Wählen Sie nach dem Überprüfen der Konfiguration **Erstellen** aus.
1. Warten Sie, bis die Bereitstellung abgeschlossen ist. Wechseln Sie dann zur bereitgestellten Ressource.

## Erstellen einer Beispieldatenbank

*Schließen Sie während dieses Vorgangs alle Tipps, die im Portal angezeigt werden*.

1. Wählen Sie auf der Seite für Ihr neues Cosmos DB-Konto im Bereich links die Option **Data Explorer** aus.
1. Wählen Sie auf der Seite **Data Explorer** die Option **Schnellstart** aus.
1. Überprüfen Sie auf der Registerkarte **Neuer Container** die vorausgefüllten Einstellungen für die Beispieldatenbank, und klicken Sie auf **OK**.
1. Beobachten Sie den Status im Bereich am unteren Bildschirmrand, bis die Datenbank **SampleDB** und der zugehörige Container **SampleContainer** erstellt wurden (dies kann etwa eine Minute dauern).

## Anzeigen und Erstellen von Elementen

1. Erweitern Sie auf der Seite „Data Explorer“ die Datenbank **SampleDB** und den Container **SampleContainer**, und wählen Sie **Elemente** aus, um eine Liste der Elemente im Container anzuzeigen. Die Elemente repräsentieren Produktdaten mit jeweils einer eindeutigen ID und anderen Eigenschaften.
1. Wählen Sie eines der Elemente in der Liste aus, um eine JSON-Darstellung der Elementdaten anzuzeigen.
1. Wählen Sie oben auf der Seite **Neues Element aus**, um ein neues leeres Element zu erstellen.
1. Ändern Sie den JSON-Code für das neue Element wie folgt, und wählen Sie dann **Speichern** aus.

    ```json
   {
       "name": "Road Helmet,45",
       "id": "123456789",
       "categoryID": "123456789",
       "SKU": "AB-1234-56",
       "description": "The product called \"Road Helmet,45\" ",
       "price": 48.74
   }
    ```

1. Nach dem Speichern des neuen Elements werden zusätzliche Metadateneigenschaften automatisch hinzugefügt.

## Abfragen der Datenbank

1. Wählen Sie auf der Seite **Data Explorer** das Symbol **Neue SQL-Abfrage** aus.
1. Überprüfen Sie im SQL-Abfrage-Editor die Standardabfrage (`SELECT * FROM c`), und verwenden Sie die Schaltfläche `SELECT * FROM c`, um sie auszuführen.
1. Überprüfen Sie die Ergebnisse, zu denen die vollständige JSON-Darstellung aller Elemente gehört.
1. Ändern Sie die Abfrage wie folgt:

    ```sql
   SELECT *
   FROM c
   WHERE CONTAINS(c.name,"Helmet")
    ```

1. Verwenden Sie die Schaltfläche **Abfrage ausführen**, um die überarbeitete Abfrage auszuführen und die Ergebnisse zu überprüfen. Diese enthalten JSON-Entitäten für alle Elemente mit einem Feld **Name**, das den Text „Helmet“ enthält.
1. Schließen Sie SQL-Abfrage-Editor, und verwerfen Sie Ihre Änderungen.

    Nun wissen Sie, wie Sie JSON-Entitäten in einer Cosmos DB-Datenbank mithilfe der Data Explorer-Schnittstelle im Azure-Portal erstellen und abfragen können. In einem realen Szenario würde ein Anwendungsentwickler eines der vielen programmiersprachenspezifischen Software Development Kits (SDKs) verwenden, um die NoSQL-API aufzurufen und mit Daten in der Datenbank zu arbeiten.

> **Tipp**: Wenn Sie die Erkundung von Azure Cosmos DB abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen.
