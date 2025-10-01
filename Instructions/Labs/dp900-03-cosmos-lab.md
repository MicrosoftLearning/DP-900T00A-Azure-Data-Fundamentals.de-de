---
lab:
  title: Einführung in Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# Einführung in Azure Cosmos DB

In dieser Übung erfahren Sie, wie Sie ein Azure Cosmos DB-Konto bereitstellen, eine Beispieldatenbank und einen Container erstellen, JSON-Elemente hinzufügen und anzeigen sowie SQL-ähnliche Abfragen ausführen, um Daten abzurufen. Sie sammeln praktische Erfahrung im Azure-Portal und lernen, wie Cosmos DB eine flexible, nicht relationale Datenspeicherung und Abfrage unterstützt.

Dieses Lab dauert ungefähr **15** Minuten.

## Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## Erstellen eines Cosmos DB-Kontos

Damit Sie Cosmos DB verwenden können, müssen Sie in Ihrem Azure-Abonnement ein Cosmos DB-Konto bereitstellen. In dieser Übung stellen Sie ein Cosmos DB-Konto bereit, für das Azure Cosmos DB for NoSQL verwendet wird.

1. Wählen Sie oben links im Azure-Portal **+ Erstellen einer Ressource** und suchen Sie nach `Azure Cosmos DB`.  Wählen Sie in den Ergebnissen **Azure Cosmos DB** und dann **Erstellen** aus.

    ![Screenshot: Azure-Portal mit Cosmos DB auf dem Marketplace](images/cosmosdb-marketplace.png)

1. Wählen Sie in der **Azure Cosmos DB für NoSQL**-Kachel **Erstellen** aus.

    ![Screenshot: Azure-Portal mit Cosmos DB-Erstellungsoption](images/cosmosdb-nosql-create.png)
   
    > _**Tipp**: Das Konto ist die oberste Ebene für Ihre Cosmos DB-Ressourcen. Wenn Sie Azure Cosmos DB for NoSQL auswählen, können Sie JSON-Daten mit einer einfachen SQL-ähnlichen Abfragesprache speichern und abfragen._

1. Geben Sie die folgenden Details ein, und wählen Sie **Überprüfen und erstellen** aus:
   
    - **Workloadtyp**: Lernen
    - **Abonnement**: Wenn Sie eine Sandbox verwenden, wählen Sie die Option *Concierge-Abonnement* aus. Wenn Sie Ihr eigenes Azure-Abonnement verwenden, wählen Sie dieses aus.
    - **Ressourcengruppe**: Wenn Sie eine Sandbox verwenden, wählen Sie die vorhandene Ressourcengruppe aus (mit einem ähnlichen Namen wie *learn-xxxx....* ). Erstellen Sie andernfalls eine neue Ressourcengruppe mit einem Namen Ihrer Wahl.
    - **Kontoname**: Geben Sie einen eindeutigen Namen ein.
    - **Verfügbarkeitszonen**: Deaktivieren
    - **Speicherort**: Wählen Sie einen beliebigen empfohlenen Speicherort aus.
    - **Kapazitätsmodus**: bereitgestellter Durchsatz
    - **Rabatt für Free-Tarif anwenden**: Wählen Sie „Anwenden“ aus, falls verfügbar.
    - **Beschränken des gesamten Kontodurchsatzes**: nicht ausgewählt
  
    > _**Warum diese Auswahlmöglichkeiten?**_
    >
    > _Wir setzen den **Workloadtyp** auf „Lernen“, da dieser anfängerfreundliche Voreinstellungen bietet, die die Einrichtung erleichtern und die Kosten niedrig halten. Ihr **Kontoname** muss für den gesamten Dienst eindeutig sein, da er Teil der URL Ihres Diensts wird. Wir wählen einen **Standort** in Ihrer Nähe, damit Ihre Tests schneller laufen; welche Standorte Ihnen angezeigt werden, hängt von Ihrem Abonnement und der Aktivierung bestimmter Verfügbarkeitszonen ab. Für **Kapazitätsmodus**verwenden wir den bereitgestellten Durchsatz, sodass die Leistung während dieser kurzen Übung vorhersehbar bleibt, obwohl „serverlos“ auch in Ordnung ist, wenn sie es nur gelegentlich benötigen. Wenn der **Free-Tarif** verfügbar ist, verwenden wir ihn, damit Sie üben können, ohne dass Gebühren berechnet werden. Schließlich lassen wir die Einstellung **Beschränken des gesamten Kontodurchsatzes** ausgeschaltet, damit während Ihrer Arbeit nichts unerwartet verlangsamt wird._

1. Wählen Sie nach dem Überprüfen der Konfiguration **Erstellen** aus.

    > _**Tipp**: Azure Portal schätzt, wie lange es dauert, um diese Instanz von CosmosDB bereitzustellen. Die geschätzte Erstellungszeit wird anhand des von Ihnen ausgewählten Speicherorts berechnet._

1. Warten Sie, bis die Bereitstellung abgeschlossen ist. Wechseln Sie dann zur bereitgestellten Ressource.

## Erstellen einer Beispieldatenbank

*Schließen Sie während dieses Vorgangs alle Tipps, die im Portal angezeigt werden*.

1. Wählen Sie auf der Seite für Ihr neues Cosmos DB-Konto im Bereich links die Option **Data Explorer** aus.

    ![Screenshot: Data Explorer-Menü in Cosmos DB im Azure-Portal](images/cosmosdb-data-explorer.png)

1. Wählen Sie auf der Seite **Data Explorer** die Option **Schnellstart** aus.

    > _**Tipp**: Schnellstart erstellt eine Arbeitsdatenbank, einen Container und Beispieldaten, sodass Sie das Hinzufügen und Abfragen von Elementen üben können, ohne zuerst ein Schema zu entwerfen._

1. Überprüfen Sie auf der Registerkarte **Neuer Container** die vorausgefüllten Einstellungen für die Beispieldatenbank, und klicken Sie auf **OK**.

1. Beobachten Sie den Status im Bereich am unteren Bildschirmrand, bis die Datenbank **SampleDB** und der zugehörige Container **SampleContainer** erstellt wurden (dies kann etwa eine Minute dauern).

## Anzeigen und Erstellen von Elementen

1. Erweitern Sie auf der Seite „Data Explorer“ die Datenbank **SampleDB** und den Container **SampleContainer**, und wählen Sie **Elemente** aus, um eine Liste der Elemente im Container anzuzeigen. Die Elemente repräsentieren Produktdaten mit jeweils einer eindeutigen ID und anderen Eigenschaften.

    ![Screenshot: Data Explorer-Elemente in Comsos DB im Azure Portal](images/cosmosdb-items.png)

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

    ![Screenshot: Neues Data Explorer-Element in Comsos DB im Azure Portal](images/cosmosdb-new-item.png)

1. Nach dem Speichern des neuen Elements werden zusätzliche Metadateneigenschaften automatisch hinzugefügt.

    > _**Tipp**: Cosmos DB speichert Elemente als JSON (JavaScript Object Notation), sodass Sie Felder hinzufügen können, die ihrem Szenario ohne ein starres Schema entsprechen. Die `id` muss innerhalb des Containers eindeutig sein. Nach dem Speichern fügt Cosmos DB Systemeigenschaften (z. B. Zeitstempel und interne Bezeichner) hinzu, um Ihre Daten zu verwalten und zu optimieren:_
    > - *_rid – Die interne Ressourcen-ID, die von Cosmos DB verwendet wird, um das Element intern zu identifizieren.*
    > - *_self – Der vollständige Ressourcenlink für das Element.*
    > - *_etag – Das Entitätstag, das für Prüfungen optimistischer Parallelität verwendet wird.*
    > - *_ts – Der Unix-Zeitstempel (in Sekunden), als das Element zuletzt geändert wurde.*
    > - *_attachments – Ein Link zu den Anlagen des Dokuments (falls vorhanden).*

## Abfragen der Datenbank

1. Wählen Sie auf der Seite **Data Explorer** das Symbol **Neue SQL-Abfrage** aus.

    ![Screenshot: Neue Data Explorer-SQL-Abfrage in Comsos DB im Azure Portal](images/cosmosdb-new-sqlquery.png)

1. Überprüfen Sie im SQL-Abfrage-Editor die Standardabfrage (`SELECT * FROM c`), und verwenden Sie die Schaltfläche `SELECT * FROM c`, um sie auszuführen.

1. Überprüfen Sie die Ergebnisse, zu denen die vollständige JSON-Darstellung aller Elemente gehört.

1. Ändern Sie die Abfrage wie folgt:

    ```sql
   SELECT *
   FROM c
   WHERE CONTAINS(c.name,"Helmet")
    ```

    > _**Tipp**: Die NoSQL-API verwendet vertraute SQL-ähnliche Abfragen zum Durchsuchen von JSON-Dokumenten. `SELECT * FROM c` Listet alle Elemente auf und `CONTAINS` filtert nach Text innerhalb einer Eigenschaft. Das ist besonders für schnelle Suchvorgänge ohne zusätzliche Einstellungen nützlich._

1. Verwenden Sie die Schaltfläche **Abfrage ausführen**, um die überarbeitete Abfrage auszuführen und die Ergebnisse zu überprüfen. Diese enthalten JSON-Entitäten für alle Elemente mit einem Feld **Name**, das den Text „Helmet“ enthält.

    ![Screenshot: Data Explorer-SQL-Abfrage in Comsos DB im Azure Portal ausgeführt](images/cosmosdb-query.png)

1. Schließen Sie SQL-Abfrage-Editor, und verwerfen Sie Ihre Änderungen.

    Nun wissen Sie, wie Sie JSON-Entitäten in einer Cosmos DB-Datenbank mithilfe der Data Explorer-Schnittstelle im Azure-Portal erstellen und abfragen können. In einem realen Szenario würde ein Anwendungsentwickler eines der vielen programmiersprachenspezifischen Software Development Kits (SDKs) verwenden, um die NoSQL-API aufzurufen und mit Daten in der Datenbank zu arbeiten.

> _**Tipp**: Wenn Sie die Erkundung von Azure Cosmos DB abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen._
