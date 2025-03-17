---
lab:
  title: Erkunden von Echtzeitanalysen in Microsoft Fabric
  module: Explore real-time analytics in Microsoft Fabric
---

# Erkunden von Echtzeitanalysen in Microsoft Fabric

Microsoft Fabric bietet Echtzeitintelligenz. Sie können damit analytische Lösungen für Echtzeit-Datenströme erstellen. In dieser Übung verwenden Sie die Real-Time Intelligence-Funktionen von Microsoft Fabric, um einen Echtzeit-Datenstrom eines Taxiunternehmens aufzunehmen, zu analysieren und zu visualisieren.

Dieses Lab dauert ungefähr **30** Minuten.

> **Hinweis**: Sie benötigen einen [Microsoft Fabric-Tenant](https://learn.microsoft.com/fabric/get-started/fabric-trial), um diese Übung durchzuführen.

## Erstellen eines Arbeitsbereichs

Bevor Sie mit Daten in Fabric arbeiten, müssen Sie einen Arbeitsbereich mit aktivierter Fabric-Kapazität erstellen.

1. Navigieren Sie in einem Browser unter `https://app.fabric.microsoft.com/home?experience=fabric` zur [Microsoft Fabric-Startseite](https://app.fabric.microsoft.com/home?experience=fabric) und melden Sie sich mit Ihren Fabric-Anmeldeinformationen an.
1. Wählen Sie auf der Menüleiste auf der linken Seite **Arbeitsbereiche** aus (Symbol ähnelt &#128455;).
1. Erstellen Sie einen neuen Arbeitsbereich mit einem Namen Ihrer Wahl, und wählen Sie einen Lizenzierungsmodus mit Fabric-Kapazitäten aus (*Testversion*, *Premium* oder *Fabric*).
1. Wenn Ihr neuer Arbeitsbereich geöffnet wird, sollte er leer sein.

    ![Screenshot eines leeren Arbeitsbereichs in Fabric](./images/new-workspace.png)

## Erstellen eines Ereignisstreams

Jetzt können Sie Echtzeitdaten aus einer Streamingquelle suchen und erfassen. Sie beginnen im Fabric Echtzeit-Hub.

> **Tipp**: Wenn Sie den Echtzeit-Hub zum ersten Mal verwenden, werden möglicherweise einige *Tipps für die ersten Schritte* angezeigt. Sie können dies schließen.

1. Wählen Sie in der Menüleiste auf der linken Seite den **Echtzeit-Hub** aus.

    Der Echtzeit-Hub bietet eine einfache Möglichkeit, Quellen von Streaming-Daten zu finden und zu verwalten.

    ![Screenshot des Echtzeit-Hubs in Fabric.](./images/real-time-hub.png)

1. Wählen Sie im Echtzeit-Hub im Abschnitt **Verbinden mit** die Option **Datenquellen** aus.
1. Suchen Sie die Beispieldatenquelle **Gelbes Taxi** und wählen Sie **Verbinden**. Benennen Sie dann im **Verbindungs**-Assistenten die Quelle als `taxi`, und bearbeiten Sie den Standard-Eventstreamnamen, um ihn in `taxi-data` zu ändern. Der Standard-Stream, der mit diesen Daten verbunden ist, wird automatisch *taxi-data-stream* genannt:

    ![Screenshot eines neuen Eventstreams.](./images/name-eventstream.png)

1. Wählen Sie **Weiter** aus; warten Sie, bis der Quell- und Eventstream erstellt wurde, und wählen Sie dann **Eventstream öffnen** aus. Der Eventstream zeigt die **Taxi**-Quelle und den **taxi-data-stream** auf der Entwurfsfläche an:

   ![Screenshot des Eventstream-Canvas.](./images/new-taxi-stream.png)

## Erstellen eines Eventhouses

Der Eventstream erfasst die Echtzeit-Bestandsdaten, macht aber derzeit nichts damit. Erstellen wir ein Eventhouse, in dem die erfassten Daten in einer Tabelle gespeichert werden können.

1. Wählen Sie in der Menüleiste auf der linken Seite **Erstellen** aus. Wählen Sie auf der Seite *Neu* unter dem Abschnitt *Real-Time-Inteligence* die Option **Eventhouse** aus. Wählen Sie einen eindeutigen Namen Ihrer Wahl aus.

    >**Hinweis**: Wenn die Option **Erstellen** nicht an die Seitenleiste angeheftet ist, müssen Sie zuerst die Ellipses-Option (**…**) auswählen.

    Schließen Sie alle Tipps oder Aufforderungen, die angezeigt werden, bis Sie Ihr neues leeres Eventhouse sehen.

    ![Screenshot eines neuen Eventhouse](./images/create-eventhouse.png)

1. Beachten Sie im linken Bereich, dass Ihr Eventhouse eine KQL-Datenbank mit demselben Namen wie das Eventhouse enthält. Sie können in dieser Datenbank Tabellen für Ihre Echtzeitdaten anlegen oder bei Bedarf weitere Datenbanken erstellen.
1. Wählen Sie die Datenbank aus und beachten Sie, dass es ein zugehöriges *Queryset* gibt. Diese Datei enthält einige KQL-Beispielabfragen, die Sie verwenden können, um mit der Abfrage der Tabellen in Ihrer Datenbank zu beginnen.

    Allerdings gibt es derzeit keine Tabellen zum Abfragen. Dieses Problem lässt sich beheben, indem Daten aus dem Eventstream in einer neuen Tabelle gespeichert werden.

1. Wählen Sie auf der Hauptseite Ihrer KQL-Datenbank **Daten abrufen**.
1. Wählen Sie als Datenquelle **Eventstream** > **Vorhandener Eventstream**.
1. Erstellen Sie im Bereich **Zieltabelle auswählen oder erstellen** eine neue Tabelle mit dem Namen `taxi`. Wählen Sie dann im Bereich **Datenquelle konfigurieren** Ihren Arbeitsbereich und den **taxi-data**-Eventstream aus und benennen Sie die Verbindung `taxi-table`.

   ![Screenshot der Konfiguration zum Laden einer Tabelle aus einem Eventstream.](./images/configure-destination.png)

1. Verwenden Sie die Schaltfläche **Weiter**, um die Schritte zum Überprüfen der Daten auszuführen und die Konfiguration dann abzuschließen. Schließen Sie dann das Konfigurationsfenster, um Ihr Eventhouse mit der Bestandstabelle anzuzeigen.

   ![Screenshot von und Eventhouse mit einer Tabelle.](./images/eventhouse-with-table.png)

    Die Verbindung zwischen dem Datenstrom und der Tabelle wurde erstellt. Überprüfen wir dies im Eventstream.

1. Wählen Sie in der Menüleiste auf der linken Seite den **Echtzeit**-Hub aus und zeigen Sie dann die Seite **Meine Datenströme** an. Wählen Sie im Menü **…** für den **taxi-data-stream**-Stream die Option **Eventstream öffnen**.

    Der Eventstream zeigt nun ein Ziel für den Datenstrom an:

   ![Screenshot eines Eventstreams mit einem Ziel.](./images/eventstream-destination.png)

    > **Tipp**: Wählen Sie das Ziel im Entwurfsbereich aus, und wenn darunter keine Datenvorschau angezeigt wird, wählen Sie **Aktualisieren** aus.

    In dieser Übung haben Sie einen sehr einfachen Eventstream erstellt, der Echtzeitdaten erfasst und diese in eine Tabelle lädt. In einer echten Lösung würden Sie in der Regel Transformationen hinzufügen, um die Daten über Zeitfenster zu aggregieren (z. B. um den Durchschnittspreis jeder Aktie über Fünf-Minuten-Zeiträume zu erfassen).

    Lassen Sie uns nun untersuchen, wie Sie die erfassten Daten abfragen und analysieren können.

## Abfragen der erfassten Daten

Der Eventstream erfasst die Taxitarifdaten in Echtzeit und lädt sie in eine Tabelle in Ihrer KQL-Datenbank. Sie können diese Tabelle abfragen, um die erfassten Daten zu sehen.

1. Wählen Sie in der Menüleiste auf der linken Seite Ihre Eventhouse-Datenbank aus.
1. Wählen Sie das *Queryset* für Ihre Datenbank.
1. Ändern Sie im Abfragebereich die erste Beispielabfrage wie hier gezeigt:

    ```kql
    taxi
    | take 100
    ```

1. Wählen Sie den Abfragecode aus und führen Sie ihn aus, um 100 Datenzeilen aus der Tabelle anzuzeigen.

    ![Screenshot einer KQL-Abfrage.](./images/kql-stock-query.png)

1. Überprüfen Sie die Ergebnisse und ändern Sie dann die Abfrage, um die Anzahl der Taxifahrten pro Stunde anzuzeigen:

    ```kql
    taxi
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. Markieren Sie die geänderte Abfrage und führen Sie sie aus, um die Ergebnisse zu sehen.
1. Warten Sie ein paar Sekunden und führen Sie es erneut aus. Beachten Sie, dass sich die Anzahl der Abholungen ändert, wenn neue Daten aus dem Echtzeit-Stream zur Tabelle hinzugefügt werden.

## Bereinigen von Ressourcen

In dieser Übung haben Sie ein Eventhouse erstellt, Echtzeitdaten mithilfe eines Eventstreams erfasst, die erfassten Daten in einer KQL-Datenbanktabelle abgefragt, ein Echtzeit-Dashboard zur Visualisierung der Echtzeitdaten erstellt und eine Warnung mithilfe von Activator konfiguriert.

Wenn Sie die Erkundung von Real-Time Intelligence in Fabric abgeschlossen haben, können Sie den für diese Übung erstellten Arbeitsbereich löschen.

1. Wählen Sie auf der Leiste auf der linken Seite das Symbol für Ihren Arbeitsbereich aus.
2. Wählen Sie in der Symbolleiste **Arbeitsbereichseinstellungen** aus.
3. Wählen Sie im Abschnitt **Allgemein** die Option **Diesen Arbeitsbereich entfernen** aus.
