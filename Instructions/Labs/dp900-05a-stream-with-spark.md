---
lab:
  title: Erste Schritte mit Spark-Streaming in Azure Synapse Analytics
  module: Explore fundamentals of real-time analytics
---

# Erste Schritte mit Spark-Streaming in Azure Synapse Analytics

In dieser Übung verwenden Sie *strukturiertes Spark-Streaming* und *Deltatabellen* in Azure Synapse Analytics, um Streamingdaten zu verarbeiten.

Dieses Lab dauert ungefähr **15** Minuten.

## Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## Bereitstellen eines Synapse Analytics-Arbeitsbereichs

Um Synapse Analytics verwenden zu können, müssen Sie eine Synapse Analytics-Arbeitsbereichsressource in Ihrem Azure-Abonnement bereitstellen.

1. Öffnen Sie das [Azure Portal](https://portal.azure.com?azure-portal=true), und melden Sie sich mit den Anmeldeinformationen für Ihr Azure-Abonnement an.

    > **Hinweis**: Stellen Sie sicher, dass Sie sich im Verzeichnis mit Ihrem eigenen Abonnement befinden. Dies wird oben rechts unter Ihrer Benutzer-ID angegeben. Falls nicht, klicken Sie auf das Benutzersymbol, und wechseln Sie das Verzeichnis.

2. Verwenden Sie das Symbol **&#65291; Ressource erstellen** auf der **Startseite** des Azure-Portals, um eine neue Ressource zu erstellen.
3. Suchen Sie nach *Azure Synapse Analytics*, und erstellen Sie eine neue **Azure Synapse Analytics-Ressource** mit den folgenden Einstellungen:
    - **Abonnement:** *Geben Sie Ihr Azure-Abonnement an.*
        - **Ressourcengruppe**: *Erstellen Sie eine neue Ressourcengruppe mit einem geeigneten Namen wie „synapse-rg“.*
        - **Verwaltete Ressourcengruppe**: *Geben Sie einen geeigneten Namen ein, z. B. „synapse-managed-rg“.*
    - **Arbeitsbereichsname**: *Geben Sie einen eindeutigen Arbeitsbereichsnamen ein, z. B. „synapse-ws-<Ihr_Name>“.*
    - **Region**: *Wählen Sie eine beliebige verfügbare Region aus.*
    - **Data Lake Storage Gen 2 auswählen**: Aus Abonnement
        - **Kontoname**: *Erstellen Sie ein neues Konto mit einem eindeutigen Namen, z. B. „datalake<Ihr_Name>“.*
        - **Dateisystemname**: *Erstellen Sie ein neues Dateisystem mit einem eindeutigen Namen, z. B. „fs<Ihr_Name>“.*

    > **Hinweis**: Ein Synapse Analytics-Arbeitsbereich erfordert zwei Ressourcengruppen in Ihrem Azure-Abonnement: eine für Ressourcen, die Sie explizit erstellen, und eine andere für verwaltete Ressourcen, die vom Dienst verwendet werden. Außerdem ist ein Data Lake-Speicherkonto erforderlich, in dem Daten, Skripts und andere Artefakte gespeichert werden.

4. Wenn Sie diese Details eingegeben haben, klicken Sie auf **Überprüfen + Erstellen** und dann auf **Erstellen**, um den Arbeitsbereich zu erstellen.
5. Warten Sie, bis der Arbeitsbereich erstellt wurde. Dies kann etwa fünf Minuten dauern.
6. Wenn die Bereitstellung abgeschlossen ist, wechseln Sie zur erstellten Ressourcengruppe, und überprüfen Sie, ob sie Ihren Synapse Analytics-Arbeitsbereich und ein Data Lake-Speicherkonto enthält.
7. Wählen Sie Ihren Synapse-Arbeitsbereich aus, und klicken Sie auf der Seite **Übersicht** der Karte **Synapse Studio öffnen** auf die Option **Öffnen**, um Synapse Studio auf einer neuen Browserregisterkarte zu öffnen. Synapse Studio ist eine webbasierte Schnittstelle, die Sie zum Arbeiten mit Ihrem Synapse Analytics-Arbeitsbereich verwenden können.
8. Verwenden Sie im linken Bereich von Synapse Studio das Symbol **&rsaquo;&rsaquo;**, um das Menü zu erweitern. Dadurch werden die verschiedenen Seiten in Synapse Studio angezeigt, die Sie zur Verwaltung von Ressourcen und zur Durchführung von Datenanalyseaufgaben verwenden werden, wie im Folgenden gezeigt:

    ![Synapse Studio](images/synapse-studio.png)

## Erstellen eines Spark-Pools

Um Spark zum Verarbeiten von Streamingdaten zu nutzen, müssen Sie Ihrem Azure Synapse-Arbeitsbereich einen Spark-Pool hinzufügen.

1. Wählen Sie in Synapse Studio die Seite **Verwalten** aus.
2. Wählen Sie die Registerkarte **Apache Spark-Pools** aus, und verwenden Sie dann das Symbol **&#65291; Neu**, um einen neuen Spark-Pool mit den folgenden Einstellungen zu erstellen:
    - **Name des Apache Spark-Pools**: sparkpool
    - **Knotengrößenfamilie**: Arbeitsspeicheroptimiert
    - **Knotengröße**: Klein (4 virtuelle Kerne/32 GB)
    - **Autoskalierung**: Aktiviert
    - **Anzahl der Knoten**: 3----3
3. Überprüfen und erstellen Sie den Spark-Pool, und warten Sie, bis er bereitgestellt ist (dies kann einige Minuten dauern).

## Erkunden der Streamverarbeitung

Um die Streamverarbeitung mit Spark zu erkunden, verwenden Sie ein Notebook. Dieses enthält Python-Code und Hinweise, die Sie bei der Durchführung einiger grundlegender Aufgaben zur Streamverarbeitung mit strukturiertem Spark-Streaming und Deltatabellen unterstützen.

1. Laden Sie das Notebook [Structured Streaming and Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) auf Ihren lokalen Computer herunter. Hinweis: Wenn das Notebook als Textdatei in Ihrem Browser geöffnet wird, speichern Sie es in einem lokalen Ordner. Achten Sie hierbei darauf, dass Sie es als **Structured Streaming and Delta Tables.ipynb** und nicht als TXT-Datei speichern.
2. Wählen Sie in Synapse Studio die Seite **Entwickeln** aus.
3. Klicken Sie im Menü **&#65291;** auf die Option **&#8612; Importieren**, und wählen Sie die auf Ihrem lokalen Computer gespeicherte Datei **Structured Streaming and Delta Tables.ipynb** aus.
4. Befolgen Sie die Anweisungen im Notebook, um es mit Ihrem Spark-Pool zu verbinden und die darin enthaltenen Codezellen auszuführen, um verschiedene Möglichkeiten zur Verwendung von Spark für die Streamverarbeitung zu erkunden.

## Löschen von Azure-Ressourcen

> **Hinweis**: Wenn Sie andere Übungen abschließen möchten, in denen Azure Synapse Analytics verwendet wird, können Sie diesen Abschnitt überspringen. Führen Sie andernfalls die folgenden Schritte aus, um unnötige Azure-Kosten zu vermeiden.

1. Schließen Sie die Synapse Studio-Browserregisterkarte, ohne Änderungen zu speichern, und kehren Sie zum Azure-Portal zurück.
1. Wählen Sie auf der **Startseite** des Azure-Portals die Option **Ressource erstellen** aus.
1. Wählen Sie die Ressourcengruppe für Ihren Synapse Analytics-Arbeitsbereich (nicht die verwaltete Ressourcengruppe) aus, und vergewissern Sie sich, dass sie den Synapse-Arbeitsbereich, das Speicherkonto und den Daten-Explorer Pool für Ihren Arbeitsbereich enthält (wenn Sie die vorherige Übung abgeschlossen haben, enthält sie auch einen Spark-Pool).
1. Wählen Sie oben auf der Seite **Übersicht** für Ihre Ressourcengruppe die Option **Ressourcengruppe löschen** aus.
1. Geben Sie den Namen der Ressourcengruppe ein, um zu bestätigen, dass Sie sie löschen möchten, und wählen Sie **Löschen** aus.

    Nach ein paar Minuten werden Ihr Azure Synapse-Arbeitsbereich und der ihm zugeordnete verwaltete Arbeitsbereich gelöscht.
