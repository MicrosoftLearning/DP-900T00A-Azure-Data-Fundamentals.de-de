---
lab:
  title: Erkunden von Azure Stream Analytics
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-stream-analytics"></a>Erkunden von Azure Stream Analytics

In dieser Übung stellen Sie einen Azure Stream Analytics-Auftrag in Ihrem Azure-Abonnement bereit und verwenden ihn zum Verarbeiten eines Echtzeitdatenstroms.

Dieses Lab dauert ungefähr **15** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## <a name="create-azure-resources"></a>Erstellen von Azure-Ressourcen

1. Melden Sie sich bei Ihrem Azure-Abonnement im [Azure-Portal](https://portal.azure.com) mit den Anmeldeinformationen Ihres Azure-Abonnements an.

1. Use the <bpt id="p1">**</bpt>[<ph id="ph1">\&gt;</ph>_]<ept id="p1">**</ept> button to the right of the search bar at the top of the page to create a new Cloud Shell in the Azure portal, selecting a <bpt id="p2">***</bpt>Bash<ept id="p2">***</ept> environment and creating storage if prompted. The cloud shell provides a command line interface in a pane at the bottom of the Azure portal, as shown here:

    ![Azure-Portal mit einem Cloud Shell-Bereich](./images/cloud-shell.png)

1. Geben Sie in Azure Cloud Shell den folgenden Befehl ein, um die für diese Übung benötigten Dateien herunterzuladen.

    ```bash
    git clone https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals dp-900
    ```

1. Warten Sie, bis der Befehl abgeschlossen ist, und geben Sie dann den folgenden Befehl ein, um das aktuelle Verzeichnis in den Ordner zu ändern, der die Dateien für diese Übung enthält.

    ```bash
    cd dp-900/streaming
    ```

1. Geben Sie den folgenden Befehl ein, um ein Skript auszuführen, das die für diese Übung benötigten Azure-Ressourcen erstellt.

    ```bash
    bash setup.sh
    ```

    Warten Sie, während das Skript ausgeführt wird und die folgenden Aktionen durchführt:

    1. Installieren der Azure CLI-Erweiterungen, die zum Erstellen von Ressourcen benötigt werden (*Sie können alle Warnungen zu experimentellen Erweiterungen ignorieren*)
    1. Identifizieren der für diese Übung bereitgestellte Azure-Ressourcengruppe
    1. Erstellen einer *Azure IoT Hub*-Ressource zum Empfang eines Datenstreams von einem simulierten Gerät
    1. Erstellen eines *Azure-Speicherkontos*, das zur Speicherung der verarbeiteten Daten verwendet wird
    1. Erstellen eines *Azure Stream Analytics*-Auftrags, der die eingehenden Gerätedaten in Echtzeit verarbeitet und die Ergebnisse in das Speicherkonto schreibt

## <a name="explore-the-azure-resources"></a>Erkunden der Azure-Ressourcen

1. In the <bpt id="p1">[</bpt>Azure portal<ept id="p1">](https://portal.azure.com?azure-portal=true)</ept>, on the home page, select <bpt id="p2">**</bpt>Resource groups<ept id="p2">**</ept> to see the resource groups in your subscription. This should include the <bpt id="p1">**</bpt>learn*xxxxxxxxxxxxxxxxx...<ept id="p1">**</ept>* resource group identified by the setup script.
2. Wählen Sie die Ressourcengruppe **learn*xxxxxxxxxxxxxxxxx...** * aus, und überprüfen Sie die darin enthaltenen Ressourcen. Es sollten folgende Elemente vorhanden sein:
    - Ein *IoT-Hub* mit dem Namen **iothub*xxxxxxxxxxxxx***, der für den Empfang eingehender Gerätedaten verwendet wird.
    - Ein *Speicherkonto* mit dem Namen **store*xxxxxxxxxxxx***, in das die Ergebnisse der Datenverarbeitung geschrieben werden.
    - Ein *Stream Analytics-Auftrag* mit dem Namen **stream*xxxxxxxxxxxxx***, der zum Verarbeiten von Streamingdaten verwendet wird.

    Falls nicht alle drei Ressourcen aufgeführt sind, klicken Sie auf die Schaltfläche **&#8635; Aktualisieren**, bis sie angezeigt werden.

    > **Hinweis**: Wenn Sie die Learn-Sandbox verwenden, kann die Ressourcengruppe auch ein zweites *Speicherkonto* mit dem Namen **cloudshell*xxxxxxxx*** enthalten, das zum Speichern von Daten für die Azure Cloud Shell-Instanz verwendet wird, die Sie zum Ausführen des Setupskripts verwendet haben.

3. Wählen Sie den Stream Analytics-Auftrag **stream*xxxxxxxxxxxxx*** aus, und sehen Sie sich die Informationen auf der Seite **Übersicht** an. Beachten Sie dabei die folgenden Details:
    - The job has one <bpt id="p1">*</bpt>input<ept id="p1">*</ept> named <bpt id="p2">**</bpt>iotinput<ept id="p2">**</ept>, and one <bpt id="p3">*</bpt>output<ept id="p3">*</ept> named <bpt id="p4">**</bpt>bloboutput<ept id="p4">**</ept>. These reference the IoT Hub and Storage account created by the setup script.
    - Der Auftrag umfasst eine *Abfrage*, die Daten aus der Eingabe **iotinput** liest und sie aggregiert, indem sie alle 10 Sekunden die Anzahl der verarbeiteten Nachrichten zählt und die Ergebnisse in die Ausgabe **bloboutput** schreibt.

## <a name="use-the-resources-to-analyze-streaming-data"></a>Verwenden der Ressourcen zum Analysieren von Streamingdaten

1. Klicken Sie oben auf der Seite **Übersicht** für den Stream Analytics-Auftrag auf die Schaltfläche **&#9655; Starten**, und wählen Sie dann im Bereich **Auftrag starten** die Option **Starten** aus, um den Auftrag zu starten.
2. Warten Sie auf eine Benachrichtigung, dass der Streamingauftrag erfolgreich gestartet wurde.
3. Wechseln Sie zurück zu Azure Cloud Shell, und geben Sie den folgenden Befehl ein, um ein Gerät zu simulieren, das Daten an den IoT Hub sendet.

    ```
    bash iotdevice.sh
    ```

4. Warten Sie, bis die Simulation beginnt, was durch eine Ausgabe wie diese angezeigt wird:

    ```
    Device simulation in progress: 6%|#    | 7/120 [00:08<02:21, 1.26s/it]
    ```

5. Kehren Sie während der Ausführung der Simulation im Azure-Portal auf die Seite für die Ressourcengruppe **learn*xxxxxxxxxxxxxxxxx...** * zurück, und wählen Sie das Speicherkonto **store*xxxxxxxxxxxx*** aus.
6. Wählen Sie im Bereich auf der linken Seite des Blatts „Speicherkonto“ die Registerkarte **Container** aus.
7. Öffnen Sie den Container **data**.
8. Navigieren Sie im Container **Daten** durch die Ordnerhierarchie, die einen Ordner für das aktuelle Jahr mit Unterordnern für den Monat, den Tag und die Stunde enthält.
9. Wählen Sie im Ordner für die Stunde die erstellte Datei aus, die einen ähnlichen Namen haben sollte wie **0_xxxxxxxxxxxxxxxx.json**.
10. Wählen Sie auf der Seite für die Datei die Option **Bearbeiten** aus, und überprüfen Sie den Inhalt der Datei. Dieser sollte aus einem JSON-Datensatz für jeden 10-Sekunden-Zeitraum bestehen, der die Anzahl der von IoT-Geräten empfangenen Nachrichten anzeigt, etwa so:

    ```
    {"starttime":"2021-10-23T01:02:13.2221657Z","endtime":"2021-10-23T01:02:23.2221657Z","device":"iotdevice","messages":2}
    {"starttime":"2021-10-23T01:02:14.5366678Z","endtime":"2021-10-23T01:02:24.5366678Z","device":"iotdevice","messages":3}
    {"starttime":"2021-10-23T01:02:15.7413754Z","endtime":"2021-10-23T01:02:25.7413754Z","device":"iotdevice","messages":4}
    ...
    ```

11. Verwenden Sie die Schaltfläche **&#8635; Aktualisieren**, um die Datei zu aktualisieren. Beachten Sie, dass zusätzliche Ergebnisse in die Datei geschrieben werden, da der Stream Analytics-Auftrag die Gerätedaten in Echtzeit verarbeitet, während sie vom Gerät an den IoT-Hub gestreamt werden.
12. Kehren Sie zu Azure Cloud Shell zurück, und warten Sie, bis die Gerätesimulation abgeschlossen ist (sie sollte etwa 3 Minuten dauern).
13. Aktualisieren Sie zurück im Azure-Portal die Datei ein weiteres Mal, um alle während der Simulation erzeugten Ergebnisse anzuzeigen.
14. Kehren Sie zur Ressourcengruppe **learn*xxxxxxxxxxxxxxxxx...** * zurück, und öffnen Sie erneut den Stream Analytics-Auftrag **stream*xxxxxxxxxxxxx***.
15. Verwenden Sie die im oberen Bereich der Seite für den Stream Analytics-Auftrag angezeigte Schaltfläche **&#11036; Beenden**, um den Auftrag zu beenden. Bestätigen Sie den Vorgang, wenn Sie dazu aufgefordert werden.

> **Hinweis**: Wenn Sie die Erkundung der Streaminglösung abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen.
