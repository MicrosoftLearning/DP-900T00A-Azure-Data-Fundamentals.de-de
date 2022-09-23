---
lab:
  title: Erkunden des Azure Synapse-Daten-Explorers
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-synapse-data-explorer"></a>Erkunden des Azure Synapse-Daten-Explorers

In dieser Übung verwenden Sie den Azure Synapse Daten-Explorer, um Zeitreihendaten zu analysieren.

Dieses Lab dauert ungefähr **25** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## <a name="provision-a-synapse-analytics-workspace"></a>Bereitstellen eines Synapse Analytics-Arbeitsbereichs

> **Tipp**: Wenn Sie bereits über einen Azure Synapse-Arbeitsbereich verfügen, überspringen Sie diesen Abschnitt, und fahren Sie direkt mit dem Abschnitt **[Erstellen eines Daten-Explorer-Pools](#create-a-data-explorer-pool)** fort.

1. Öffnen Sie das Azure-Portal unter [https://portal.azure/com](https://portal.azure.com?azure-portal=true), und melden Sie sich mit den Anmeldeinformationen für Ihr Azure-Abonnement an.

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Ensure you are working in the directory containing your subscription - indicated at the top right under your user ID. If not, select the user icon and switch directory.

1. Verwenden Sie das Symbol **&#65291; Ressource erstellen** auf der **Startseite** des Azure-Portals, um eine neue Ressource zu erstellen.
1. Suchen Sie nach *Azure Synapse Analytics*, und erstellen Sie eine neue **Azure Synapse Analytics-Ressource** mit den folgenden Einstellungen:
    - **Abonnement:** *Geben Sie Ihr Azure-Abonnement an.*
        - **Ressourcengruppe**: *Erstellen Sie eine neue Ressourcengruppe mit einem geeigneten Namen wie „synapse-rg“.*
        - **Verwaltete Ressourcengruppe**: *Geben Sie einen geeigneten Namen ein, z. B. „synapse-managed-rg“.*
    - **Arbeitsbereichsname**: *Geben Sie einen eindeutigen Arbeitsbereichsnamen ein, z. B. „synapse-ws-<Ihr_Name>“.*
    - **Region**: *Wählen Sie eine beliebige verfügbare Region aus.*
    - **Data Lake Storage Gen 2 auswählen**: Aus Abonnement
        - **Kontoname**: *Erstellen Sie ein neues Konto mit einem eindeutigen Namen, z. B. „datalake<Ihr_Name>“.*
        - **Dateisystemname**: *Erstellen Sie ein neues Dateisystem mit einem eindeutigen Namen, z. B. „fs<Ihr_Name>“.*

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.

1. Wenn Sie diese Details eingegeben haben, klicken Sie auf **Überprüfen + Erstellen** und dann auf **Erstellen**, um den Arbeitsbereich zu erstellen.
1. Warten Sie, bis der Arbeitsbereich erstellt wurde. Dies kann etwa fünf Minuten dauern.
1. Wenn die Bereitstellung abgeschlossen ist, wechseln Sie zur erstellten Ressourcengruppe, und überprüfen Sie, ob sie Ihren Synapse Analytics-Arbeitsbereich und ein Data Lake-Speicherkonto enthält.
1. Wählen Sie Ihren Synapse-Arbeitsbereich aus, und klicken Sie auf der Seite **Übersicht** der Karte **Synapse Studio öffnen** auf die Option **Öffnen**, um Synapse Studio auf einer neuen Browserregisterkarte zu öffnen. Synapse Studio ist eine webbasierte Schnittstelle, die Sie zum Arbeiten mit Ihrem Synapse Analytics-Arbeitsbereich verwenden können.
1. Verwenden Sie im linken Bereich von Synapse Studio das Symbol **&rsaquo;&rsaquo;** , um das Menü zu erweitern. Dadurch werden die verschiedenen Seiten in Synapse Studio angezeigt, die Sie zur Verwaltung von Ressourcen und zur Durchführung von Datenanalyseaufgaben verwenden werden.

## <a name="create-a-data-explorer-pool"></a>Erstellen eines Data Explorer-Pools

1. Wählen Sie in Synapse Studio die Seite **Verwalten** aus.
1. Wählen Sie die Registerkarte **Daten-Explorer-Pools** aus, und verwenden Sie dann das Symbol **&#65291; Neu**, um einen neuen Pool mit den folgenden Einstellungen zu erstellen:
    - **Name des Daten-Explorer-Pools**: dxpool
    - **Workload**: Computeoptimiert
    - **Größe**: Sehr klein (2 Kerne)
1. Wählen Sie **Weiter: Zusätzliche Einstellungen >** aus, und aktivieren Sie die Einstellung **Streamingerfassung**. So kann der Daten-Explorer neue Daten aus einer Streamingquelle wie z. B. Azure Event Hubs erfassen.
1. Wählen Sie **Überprüfen und erstellen** aus, um den Daten-Explorer-Pool zu erstellen, und warten Sie dann, bis er bereitgestellt ist (was 15 Minuten oder länger dauern kann. Der Status ändert sich von *Wird erstellt* in *Online*).

## <a name="create-a-database-and-ingest-data"></a>Erstellen einer Datenbank und Erfassen von Daten

1. Wählen Sie in Synapse Studio die Seite **Daten** aus.
1. Stellen Sie sicher, dass die Registerkarte **Arbeitsbereich** ausgewählt ist, und wählen Sie bei Bedarf das Symbol **&#8635;** oben links auf der Seite aus, um die Ansicht zu aktualisieren, sodass **Daten-Explorer-Datenbanken** aufgelistet wird.
1. Erweitern Sie **Daten-Explorer-Datenbanken**, und überprüfen Sie, ob **dxpool** aufgeführt ist.
1. Verwenden Sie im Bereich **Daten** das Symbol **&#65291;** , um eine neue **Daten-Explorer Datenbank** mit dem Namen **iot-data** im **dxpool**-Pool zu erstellen.
1. Laden Sie beim Warten auf die Erstellung der Datenbank **devices.csv** von [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true) herunter, und speichern Sie die Datei in einem beliebigen Ordner auf Ihrem lokalen Computer.
1. Warten Sie ggf. in Synapse Studio, bis die Datenbank erstellt ist, und wählen Sie dann im Menü **...** für die neue **iot-data**-Datenbank die Option **In Azure Data Explorer öffnen** aus.
1. Wählen Sie auf der neuen Browserregisterkarte mit Azure Data Explorer auf der Registerkarte **Daten** die Option **Neue Daten erfassen** aus.
1. Wählen Sie auf der Seite **Ziel** die folgenden Einstellungen aus:
    - **Cluster**: *Der Daten-Explorer-Pool **dxpool** in Ihrem Azure Synapse-Arbeitsbereich*
    - **Datenbank**: iot-data
    - **Tabelle**: Erstellen Sie eine neue Tabelle mit dem Namen **devices**.
1. Wählen Sie **Weiter: Quelle** und auf der Seite **Quelle** die folgenden Optionen aus:
    - **Quelltyp**: Datei
    - **Dateien**: Laden Sie die **devices.csv**-Datei von Ihrem lokalen Computer hoch.
1. Wählen Sie **Weiter: Schema** aus, und stellen Sie auf der Seite **Schema** sicher, dass die folgenden Einstellungen korrekt sind:
    - **Komprimierungstyp**: Nicht komprimiert
    - **Datenformat**: CSV
    - **Ersten Datensatz ignorieren**: ausgewählt
    - **Zuordnung**: devices_mapping
1. Ensure the column data types have been correctly identified as <bpt id="p1">*</bpt>Time (datetime)<ept id="p1">*</ept>, <bpt id="p2">*</bpt>Device (string)<ept id="p2">*</ept>, and <bpt id="p3">*</bpt>Value (long)<ept id="p3">*</ept>). Then select <bpt id="p1">**</bpt>Next: Start Ingestion<ept id="p1">**</ept>.
1. Klicken Sie nach Abschluss der Erfassung auf **Schließen**.
1. Stellen Sie sicher, dass in Azure Data Explorer auf der Registerkarte **Abfrage** die Datenbank **iot-data** ausgewählt ist, und geben Sie dann im Abfragebereich die folgende Abfrage ein.

    ```kusto
    devices
    ```

1. Wählen Sie auf der Symbolleiste **&#9655; Ausführen** aus, um die Abfrage auszuführen, und überprüfen Sie die Ergebnisse, die in etwa wie folgt aussehen sollten:

    | Zeit | Sicherungsmedium | Wert |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    Wenn die Ergebnisse hiermit übereinstimmen, haben Sie die Tabelle **devices** erfolgreich aus den Daten in der Datei erstellt.

    > <bpt id="p1">**</bpt>Tip<ept id="p1">**</ept>: In this example, you imported a very small amount of batch data from a file, which is fine for the purposes of this exercise. In reality, you can use Data Explorer to analyze much larger volumes of data; and since you enabled stream ingestion, you could also have configured Data Explorer to ingest data into the table from a streaming source such as Azure Event Hubs.

## <a name="use-kusto-query-language-to-query-the-table-in-synapse-studio"></a>Verwenden der Kusto-Abfragesprache zum Abfragen der Tabelle in Synapse Studio

1. Schließen Sie die Azure Data Explorer-Browserregisterkarte, und kehren Sie zu der Registerkarte zurück, die Synapse Studio enthält.
1. On the <bpt id="p1">**</bpt>Data<ept id="p1">**</ept> page, expand the <bpt id="p2">**</bpt>iot-data<ept id="p2">**</ept> database and its <bpt id="p3">**</bpt>Tables<ept id="p3">**</ept> folder. Then in the <bpt id="p1">**</bpt>...<ept id="p1">**</ept> menu for the <bpt id="p2">**</bpt>devices<ept id="p2">**</ept> table, select <bpt id="p3">**</bpt>New KQL Script<ept id="p3">**</ept><ph id="ph1"> &gt; </ph><bpt id="p4">**</bpt>Take 1000 rows<ept id="p4">**</ept>.
1. Review the generated query and its results. The query should contain the following code:

    ```kusto
    devices
    | take 1000
    ```

    Die Ergebnisse der Abfrage enthalten die ersten 1.000 Datenzeilen.

1. Ändern Sie die Abfrage wie folgt:

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. Select <bpt id="p1">**</bpt>&amp;#9655; Run<ept id="p1">**</ept> to run the query. Then review the results, which should contain only the rows for the <bpt id="p1">*</bpt>Dev1<ept id="p1">*</ept> device.

1. Ändern Sie die Abfrage wie folgt:

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. Führen Sie die Abfrage aus, und überprüfen Sie die Ergebnisse, die nur die Zeilen für das *Dev1*-Gerät nach dem 7. Januar 2022 enthalten sollten.

1. Ändern Sie die Abfrage wie folgt:

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. Führen Sie die Abfrage aus, und überprüfen Sie die Ergebnisse, die den durchschnittlichen Gerätewert enthalten sollten, der zwischen dem 1. Januar und dem 7. Januar 2022 in aufsteigender Reihenfolge des Gerätenamens aufgezeichnet wurde.

1. Schließen Sie die KQL-Abfrageregisterkarte, und verwerfen Sie Ihre Änderungen.

## <a name="delete-azure-resources"></a>Löschen von Azure-Ressourcen

Nachdem Sie nun mit dem Erkunden von Azure Synapse Analytics fertig sind, löschen Sie die erstellten Ressourcen, um unnötige Azure-Kosten zu vermeiden.

1. Schließen Sie die Synapse Studio-Browserregisterkarte, ohne Änderungen zu speichern, und kehren Sie zum Azure-Portal zurück.
1. Wählen Sie auf der **Startseite** des Azure-Portals die Option **Ressource erstellen** aus.
1. Wählen Sie die Ressourcengruppe für Ihren Synapse Analytics-Arbeitsbereich (nicht die verwaltete Ressourcengruppe) aus, und vergewissern Sie sich, dass sie den Synapse-Arbeitsbereich, das Speicherkonto und den Daten-Explorer Pool für Ihren Arbeitsbereich enthält (wenn Sie die vorherige Übung abgeschlossen haben, enthält sie auch einen Spark-Pool).
1. Wählen Sie oben auf der Seite **Übersicht** für Ihre Ressourcengruppe die Option **Ressourcengruppe löschen** aus.
1. Geben Sie den Namen der Ressourcengruppe ein, um zu bestätigen, dass Sie sie löschen möchten, und wählen Sie **Löschen** aus.

    Nach ein paar Minuten werden Ihr Azure Synapse-Arbeitsbereich und der ihm zugeordnete verwaltete Arbeitsbereich gelöscht.
