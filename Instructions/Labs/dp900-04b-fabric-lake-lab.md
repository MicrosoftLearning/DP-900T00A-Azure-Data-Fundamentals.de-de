---
lab:
  title: Erkunden von Datenanalysen in Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Erkunden von Datenanalysen in Microsoft Fabric

In dieser Übung erkunden Sie die Datenerfassung und -analyse in einem Microsoft Fabric-Lakehouse.

Dieses Lab dauert ungefähr **25** Minuten.

> **Hinweis:** Sie benötigen eine Microsoft Fabric-Lizenz, um diese Übung durchführen zu können. Weitere Informationen zum Aktivieren einer kostenlosen Fabric-Testlizenz finden Sie unter [Erste Schritte mit Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Dazu benötigen Sie ein *Schul-* , *Geschäfts-* oder Unikonto von Microsoft. Wenn Sie über kein Microsoft-Konto verfügen, können Sie sich [für eine kostenlose Testversion von Microsoft Office 365 E3 oder höher registrieren](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

*Bei der ersten Verwendung von Microsoft Fabric-Funktionen können Prompts mit Tipps erscheinen. Schließen Sie diese.*

## Erstellen eines Arbeitsbereichs

Erstellen Sie vor dem Arbeiten mit Daten in Fabric einen Arbeitsbereich mit aktivierter Fabric-Testversion.

1. Melden Sie sich bei [Microsoft Fabric](https://app.fabric.microsoft.com) unter `https://app.fabric.microsoft.com` an.
1. Wechseln Sie in der Menüleiste unten links zur Erfahrung **Datentechnik**.

    ![Screenshot: Menü zum Wechseln der Benutzeroberfläche.](./images/fabric-switcher.png)

1. Wählen Sie auf der Menüleiste auf der linken Seite **Arbeitsbereiche** aus (Symbol ähnelt &#128455;).
1. Erstellen Sie einen neuen Arbeitsbereich mit einem Namen Ihrer Wahl, und wählen Sie im Bereich **Erweitert** einen Lizenzierungsmodus mit Fabric-Kapazitäten aus (*Testversion*, *Premium* oder *Fabric*).
1. Wenn Ihr neuer Arbeitsbereich geöffnet wird, sollte er leer sein.

    ![Screenshot: Leerer Arbeitsbereich in Power BI](./images/new-workspace.png)

## Erstellen eines Lakehouse

Da Sie nun einen Arbeitsbereich besitzen, ist es an der Zeit, ein Data Lakehouse für Ihre Datendateien zu erstellen.

1. Erstellen Sie auf der Startseite des Arbeitsbereichs ein neues **Lakehouse** mit einem Namen Ihrer Wahl.

    Nach etwa einer Minute wird ein neues Lakehouse erstellt:

    ![Screenshot: Neues Lakehouse](./images/new-lakehouse.png)

1. Sehen Sie sich das neue Lakehouse an, und beachten Sie, dass Sie im Bereich **Lakehouse-Explorer** auf der linken Seite Tabellen und Dateien im Lakehouse durchsuchen können:
    - Der Ordner **Tables** enthält Tabellen, die Sie mithilfe von SQL abfragen können. Die Tabellen in einem Microsoft Fabric-Lakehouse basieren auf dem *Delta-Lake*-Open-Source-Dateiformat, das üblicherweise in Apache Spark verwendet wird.
    - Der Ordner **Files** enthält Datendateien im OneLake-Speicher für das Lakehouse, die nicht verwalteten Deltatabellen zugeordnet sind. Sie können auch *Verknüpfungen* in diesem Ordner erstellen, um auf extern gespeicherte Daten zu verweisen.

    Derzeit sind keine Tabellen oder Dateien im Lakehouse vorhanden.

## Einlesen von Daten

Eine einfache Möglichkeit zum Erfassen von Daten ist das Verwenden der Aktivität **Daten kopieren** in einer Pipeline, um die Daten aus einer Quelle zu extrahieren und in eine Datei im Lakehouse zu kopieren.

1. Wählen Sie auf der Seite **Start** für Ihr Lakehouse im Menü **Daten abrufen** die Option **Neue Datenpipeline** aus, und erstellen Sie eine neue Datenpipeline mit dem Namen **Ingest Data**.
1. Wählen Sie im Assistenten **Daten kopieren** auf der Seite **Datenquelle auswählen** die Option **Beispieldaten** und wählen Sie dann den Beispieldatensatz **NYC Taxi - Green**.

    ![Screenshot: Die Seite „Datenquelle auswählen“](./images/choose-data-source.png)

1. Auf der Seite **Mit Datenquelle verbinden** können Sie die Tabellen in der Datenquelle anzeigen. Es sollte eine Tabelle geben, die Details zu den Taxifahrten in New York City enthält. Wählen Sie dann **Weiter** aus, um zur Seite **Datenziel auswählen** zu gelangen.
1. Wählen Sie auf der Seite **Datenziel auswählen** Ihr vorhandenes Lakehouse aus. Wählen Sie **Weiter**aus.
1. Legen Sie die folgenden Datenzieloptionen fest, und wählen Sie dann **Weiter** aus:
    - **Stammordner**: Tabellen
    - **Einstellungen laden**: In neue Tabelle laden
    - **Zieltabellenname**: taxi_rides *(Möglicherweise müssen Sie warten, bis die Vorschau der Spaltenzuordnungen angezeigt wird, bevor Sie dies ändern können)*
    - **Spaltenzuordnungen**: *Standardzuordnungen unverändert übernehmen*
    - **Partition aktivieren**: *Nicht ausgewählt*
1. Stellen Sie sicher, dass auf der Seite **Überprüfen + speichern** die Option **Datenübertragung sofort starten** ausgewählt ist, und wählen **Sie dann Speichern + ausführen** aus.

    Eine neue Pipeline wird wie folgt mit der Aktivität **Daten kopieren** erstellt:

    ![Screenshot: Eine Pipeline mit der Aktivität „Daten kopieren“](./images/copy-data-pipeline.png)

    Wenn die Pipeline gestartet wird, können Sie ihren Status im Bereich **Ausgabe** unter dem Pipeline-Designer überwachen. Verwenden Sie das Symbol **&#8635;** (*Aktualisieren*), um den Status zu aktualisieren, und warten Sie, bis der Vorgang abgeschlossen ist (was 10 Minuten oder länger dauern kann).

1. Wählen Sie in der Hubmenüleiste auf der linken Seite Ihr Lakehouse aus.
1. Wählen Sie auf der **Startseite** im Bereich **Lakehouse-Explorer** im Menü **...** für den Knoten **Tabellen** die Option **Aktualisieren** aus und erweitern Sie dann **Tabellen**, um zu überprüfen, ob die Tabelle **taxi_rides** erstellt worden ist.

    > **Hinweis**: Wenn die neue Tabelle als *unbekannt* aufgeführt ist, verwenden Sie die Menüoption **Aktualisieren**, um die Ansicht zu aktualisieren.

1. Wählen Sie die Tabelle **taxi_rides**, um ihren Inhalt anzuzeigen.

    ![Screenshot der taxi_rides-Tabelle.](./images/dimProduct.png)

## Abfragen von Daten in einem Lakehouse

Nachdem Sie nun Daten in einer Tabelle im Lakehouse erfasst haben, können Sie diese mithilfe von SQL abfragen.

1. Wechseln Sie oben rechts auf der Lakehouse-Seite von der Ansicht **Lakehouse** zum **SQL-Analyse-Endpunkt** für Ihr Lakehouse.

1. Wählen Sie auf der Symbolleiste **Neue SQL-Abfrage** aus. Geben Sie dann den folgenden SQL-Code in den Abfrage-Editor ein:

    ```sql
    SELECT  DATENAME(dw,lpepPickupDatetime) AS Day,
            AVG(tripDistance) As AvgDistance
    FROM taxi_rides
    GROUP BY DATENAME(dw,lpepPickupDatetime)
    ```

1. Klicken Sie auf die Schaltfläche **&#9655; Ausführen**, um die Abfrage auszuführen und die Ergebnisse zu überprüfen, die die durchschnittliche Fahrtstrecke für jeden Wochentag enthalten sollten.

    ![Screenshot: SQL-Abfrage.](./images/sql-query.png)

## Visualisieren von Daten in einem Lakehouse

In Microsoft Fabric-Lakehouses sind alle Tabellen in einem semantischen Datenmodell organisiert, das Sie zum Erstellen von Visualisierungen und Berichten verwenden können.

1. Wählen Sie unten links auf der Seite unter dem Bereich **Explorer** die Registerkarte **Modell**, um das Datenmodell für die Tabellen im Lakehouse zu sehen (dazu gehören sowohl die Systemtabellen als auch die Tabelle **taxi_rides**).
1. Wählen Sie in der Symbolleiste **Neuer Bericht**, um einen neuen Bericht auf der Grundlage von **taxi_rides** zu erstellen.
1. Im Berichts-Designer:
    1. Erweitern Sie im Bereich **Daten** die Tabelle **taxi_rides** und wählen Sie die Felder **lpepPickupDatetime** und **passengerCount**.
    1. Wählen Sie im Bereich **Visualisierungen** die Visualisierung **Liniendiagramm**. Stellen Sie dann sicher, dass die **X-Achse** das Feld **lpepPickupDatetime** und die **Y**-Achse die **Summe von passengerCount** enthält.

        ![Screenshot eines Power BI-Berichts](./images/fabric-report.png)

    > **Tipp**: Sie können die **>>** -Symbole verwenden, um die Bereiche des Berichts-Designers auszublenden und den Bericht übersichtlicher zu gestalten.

1. Wählen Sie im Menü **Datei** die Option **Speichern**, um den Bericht als **Taxi-Fahrten-Bericht** in Ihrem Fabric-Arbeitsbereich zu speichern.

    Sie finden den Bericht auf der Seite für Ihren Arbeitsbereich im Microsoft Fabric-Portal.

## Bereinigen von Ressourcen

Wenn Sie die Untersuchung von Microsoft Fabric abgeschlossen haben, können Sie den Arbeitsbereich löschen, den Sie für diese Übung erstellt haben.

1. Wählen Sie auf der Leiste auf der linken Seite das Symbol für Ihren Arbeitsbereich aus, um alle darin enthaltenen Elemente anzuzeigen.
2. Wählen Sie im Menü **...** auf der Symbolleiste die **Arbeitsbereichseinstellungen** aus.
3. Wählen Sie im Abschnitt **Andere** die Option **Diesen Arbeitsbereich entfernen** aus.
