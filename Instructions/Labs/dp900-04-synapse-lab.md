---
lab:
  title: Erkunden von Datenanalysen in Azure mit Azure Synapse Analytics
  module: Explore fundamentals of large-scale data warehousing
---

# Erkunden von Datenanalysen in Azure mit Azure Synapse Analytics

In dieser Übung stellen Sie einen Azure Synapse Analytics-Arbeitsbereich in Ihrem Azure-Abonnement bereit und verwenden ihn zum Erfassen und Abfragen von Daten.

Dieses Lab dauert ungefähr **30** Minuten.

## Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## Bereitstellen eines Azure Synapse Analytics-Arbeitsbereichs

Damit Sie Azure Synapse Analytics verwenden können, müssen Sie eine Azure Synapse Analytics-Arbeitsbereichsressource in Ihrem Azure-Abonnement bereitstellen.

1. Öffnen Sie das Azure-Portal unter [https://portal.azure.com](https://portal.azure.com?azure-portal=true), und melden Sie sich mit den Anmeldeinformationen für Ihr Azure-Abonnement an.

    > **Tipp**: Stellen Sie sicher, dass Sie sich im Verzeichnis mit Ihrem Abonnement befinden. Dies wird oben rechts unter Ihrer Benutzer-ID angegeben. Falls nicht, klicken Sie auf das Benutzersymbol, und wechseln Sie das Verzeichnis.

2. Verwenden Sie das Symbol **&#65291; Ressource erstellen** auf der **Startseite** des Azure-Portals, um eine neue Ressource zu erstellen.
3. Suchen Sie nach *Azure Synapse Analytics*, und erstellen Sie eine neue **Azure Synapse Analytics-Ressource** mit den folgenden Einstellungen:
    - **Abonnement:** *Geben Sie Ihr Azure-Abonnement an.*
        - **Ressourcengruppe**: *Erstellen Sie eine neue Ressourcengruppe mit einem geeigneten Namen wie „synapse-rg“.*
        - **Verwaltete Ressourcengruppe**: *Geben Sie einen geeigneten Namen ein, z. B. „synapse-managed-rg“.*
    - **Arbeitsbereichsname**: *Geben Sie einen eindeutigen Arbeitsbereichsnamen ein, z. B. „synapse-ws-<Ihr_Name>“* .
    - **Region:***Wählen Sie eine der folgenden Regionen aus:*
        - Australien (Osten)
        - USA (Mitte)
        - USA (Ost) 2
        - Nordeuropa
        - USA Süd Mitte
        - Asien, Südosten
        - UK, Süden
        - Europa, Westen
        - USA (Westen)
        - USA, Westen 2
    - **Data Lake Storage Gen 2 auswählen**: Aus Abonnement
        - **Kontoname**: *Erstellen Sie ein neues Konto mit einem eindeutigen Namen, z. B. „datalake<Ihr_Name>“.*
        - **Dateisystemname**: *Erstellen Sie ein neues Dateisystem mit einem eindeutigen Namen, z. B. „fs<Ihr_Name>“.*

    > **Hinweis**: Ein Synapse Analytics-Arbeitsbereich erfordert zwei Ressourcengruppen in Ihrem Azure-Abonnement: eine für Ressourcen, die Sie explizit erstellen, und eine andere für verwaltete Ressourcen, die vom Dienst verwendet werden. Außerdem ist ein Data Lake-Speicherkonto erforderlich, in dem Daten, Skripts und andere Artefakte gespeichert werden.

4. Wenn Sie diese Details eingegeben haben, klicken Sie auf **Überprüfen + Erstellen** und dann auf **Erstellen**, um den Arbeitsbereich zu erstellen.
5. Warten Sie, bis der Arbeitsbereich erstellt wurde. Dies kann etwa fünf Minuten dauern.
6. Wenn die Bereitstellung abgeschlossen ist, wechseln Sie zur erstellten Ressourcengruppe, und überprüfen Sie, ob sie Ihren Synapse Analytics-Arbeitsbereich und ein Data Lake-Speicherkonto enthält.
7. Wählen Sie Ihren Synapse-Arbeitsbereich aus, und klicken Sie auf der Seite **Übersicht** der Karte **Synapse Studio öffnen** auf die Option **Öffnen**, um Synapse Studio auf einer neuen Browserregisterkarte zu öffnen. Synapse Studio ist eine webbasierte Schnittstelle, die Sie zum Arbeiten mit Ihrem Synapse Analytics-Arbeitsbereich verwenden können.
8. Verwenden Sie auf der linken Seite von Synapse Studio das Symbol **&rsaquo;&rsaquo;**, um das Menü zu erweitern. Dadurch werden die verschiedenen Seiten in Synapse Studio angezeigt, die Sie zum Verwalten von Ressourcen und zum Ausführen von Datenanalyseaufgaben verwenden, wie im Folgenden gezeigt:

    ![Abbildung des erweiterten Synapse Studio-Menüs zum Verwalten von Ressourcen und Ausführen von Datenanalyseaufgaben](images/synapse-studio.png)

## Erfassen von Daten

Eine der wichtigsten Aufgaben, die Sie mit Azure Synapse Analytics ausführen können, ist das Definieren von *Pipelines*, die Daten aus einer Vielzahl von Quellen zur Analyse in Ihren Arbeitsbereich übertragen (und bei Bedarf transformieren).

1. Wählen Sie in Synapse Studio auf der **Startseite** die Option **Erfassen** aus, um das Tool **Daten kopieren** zu öffnen.
2. Stellen Sie im Tool „Daten kopieren “im Schritt **Eigenschaften** sicher, dass die Optionen **Integrierte Kopieraufgabe** und **Jetzt einmal ausführen** ausgewählt sind, und klicken Sie auf **Weiter >**.
3. Wählen Sie im Schritt **Quelle** im Teilschritt **Dataset** die folgenden Einstellungen aus:
    - **Quelltyp**: Alle
    - **Verbindung**: *Erstellen Sie eine neue Verbindung, und wählen Sie im Bereich **Neue Verbindung** auf der Registerkarte **Generisches Protokoll** die Option **HTTP** aus. Erstellen Sie dann mithilfe der folgenden Einstellungen eine Verbindung zu einer Datendatei:*
        - **Name**: AdventureWorks-Produkte
        - **Beschreibung**: Produktliste über HTTP
        - **Verbindung über Integration Runtime herstellen**: AutoResolveIntegrationRuntime
        - **Basis-URL**: `https://raw.githubusercontent.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/master/Azure-Synapse/products.csv`
        - **Überprüfung des Serverzertifikats**: Aktivieren
        - **Authentifizierungstyp**: Anonym
4. Stellen Sie nach dem Erstellen der Verbindung sicher, dass im Teilschritt **Quelle/Dataset** die folgenden Einstellungen ausgewählt sind, und klicken Sie dann auf **Weiter >**:
    - **Relative URL**: *Nicht ausfüllen*
    - **Anforderungsmethode:** GET
    - **Zusätzliche Kopfzeilen**: *Nicht ausfüllen*
    - **Binärkopie**: <u>Nicht</u> ausgewählt
    - **Anforderungstimeout**: *Nicht ausfüllen*
    - **Maximal zulässige Anzahl paralleler Verbindungen**: *Nicht ausfüllen*
5. Wählen Sie im Schritt **Quelle** im Teilschritt **Konfiguration** die Option **Vorschaudaten** aus, um eine Vorschau der von Ihrer Pipeline erfassten Produktdaten anzuzeigen, und schließen Sie dann die Vorschau.
6. Stellen Sie nach dem Anzeigen der Datenvorschau sicher, dass im Teilschritt **Quelle/Konfiguration** die folgenden Einstellungen ausgewählt sind, und klicken Sie dann auf **Weiter >**:
    - **Dateiformat**: DelimitedText
    - **Spaltentrennzeichen**: Komma (,)
    - **Zeilen-Trennzeichen**: Zeilenvorschub (\n)
    - **Erste Zeile ist Überschrift**: Ausgewählt
    - **Komprimierungstyp**: Keiner
7. Wählen Sie im Schritt **Ziel** im Teilschritt **Dataset** die folgenden Einstellungen aus:
    - **Zieltyp**: Azure Data Lake Storage Gen 2
    - **Verbindung**: *Wählen Sie die vorhandene Verbindung mit Ihrem Data Lake-Speicher aus (diese wurde bei der Erstellung des Arbeitsbereichs für Sie erstellt).*
8. Stellen Sie nach Auswahl der Verbindung sicher, dass im Schritt **Ziel/Dataset** die folgenden Einstellungen ausgewählt sind, und klicken Sie dann auf **Weiter >** :
    - **Ordnerpfad**: *Navigieren Sie zum Ihrem Dateisystemordner.*
    - **Dateiname**: products.csv
    - **Kopierverhalten**: Keins
    - **Maximal zulässige Anzahl paralleler Verbindungen**: *Nicht ausfüllen*
    - **Blockgröße (MB)**: *Nicht ausfüllen*
9. Stellen Sie im Schritt **Ziel** im Teilschritt **Konfiguration** sicher, dass die folgenden Eigenschaften ausgewählt sind. Klicken Sie anschließend auf **Weiter >**.
    - **Dateiformat**: DelimitedText
    - **Spaltentrennzeichen**: Komma (,)
    - **Zeilen-Trennzeichen**: Zeilenvorschub (\n)
    - **Header zu Datei hinzufügen**: Ausgewählt
    - **Komprimierungstyp**: Keiner
    - **Maximale Zeilenanzahl pro Datei**: *Nicht ausfüllen*
    - **Dateinamenpräfix**: *Nicht ausfüllen*
10. Konfigurieren Sie im Schritt **Einstellungen** die folgenden Einstellungen, und klicken Sie dann auf **Weiter >**.
    - **Aufgabenname**: Kopieren von Produkten
    - **Aufgabenbeschreibung**: Kopieren von Produktdaten
    - **Fehlertoleranz **: *Nicht ausfüllen*
    - **Protokollierung aktivieren**: <u>Nicht</u> ausgewählt
    - **Staging aktivieren**: <u>Nicht</u> ausgewählt
11. Lesen Sie im Schritt **Überprüfen und fertig stellen** im Teilschritt **Überprüfen** die Zusammenfassung, und klicken Sie dann auf **Weiter >**.
12. Warten Sie im Teilschritt **Bereitstellung**, bis die Pipeline bereitgestellt wurde, und klicken Sie dann auf **Fertig stellen**.
13. Wählen Sie in Synapse Studio die Seite **Überwachen** aus, und warten Sie, bis auf der Registerkarte **Pipelineausführung** die Pipeline **Produkte kopieren** mit dem Status **Erfolgreich** ausgeführt wurde. (Über die Schaltfläche **&#8635; Aktualisieren** auf der Seite „Pipelineausführung“ können Sie den Status aktualisieren.)
14. Wählen Sie auf der Seite **Daten** die Registerkarte **Verknüpft** aus, und erweitern Sie die Hierarchie **Azure Data Lake Storage Gen 2**, bis der Dateispeicher für Ihren Synapse-Arbeitsbereich angezeigt wird. Wählen Sie dann den Dateispeicher aus, um zu überprüfen, ob eine Datei mit dem Namen **products.csv** an diesen Speicherort kopiert wurde, wie hier gezeigt:

    ![Abbildung von Synapse Studio mit erweiterter Azure Data Lake Storage Gen 2-Hierarchie mit dem Dateispeicher für Ihren Synapse-Arbeitsbereich](images/synapse-storage.png)

## Verwenden eines SQL-Pools zum Analysieren von Daten

Nachdem Sie nun einige Daten in Ihrem Arbeitsbereich erfasst haben, können Sie Synapse Analytics verwenden, um die Daten abzufragen und zu analysieren. Eine der gängigsten Methoden zum Abfragen von Daten ist die Verwendung von SQL. In Synapse Analytics können Sie zum Ausführen von SQL-Code einen *SQL-Pool* verwenden.

1. Klicken Sie in Synapse Studio mit der rechten Maustaste auf die **products.csv**-Datei im Dateispeicher Ihres Synapse-Arbeitsbereichs, zeigen Sie auf **Neues SQL-Skript**, und wählen Sie **Die ersten 100 Zeilen auswählen** aus.
2. Überprüfen Sie im geöffneten Bereich **SQL-Skript 1** den generierten SQL Code, der in etwa wie der folgende lauten sollte:

    ```SQL
    -- This is auto-generated code
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0'
        ) AS [result]
    ```

    Dieser Code öffnet ein Rowset aus der importierten Textdatei und ruft die ersten 100 Datenzeilen ab.

3. Vergewissern Sie sich, dass in der Liste **Verbinden mit** die Option **Integriert** ausgewählt ist. Dies entspricht dem integrierten SQL-Pool, der mit Ihrem Arbeitsbereich erstellt wurde.
4. Verwenden Sie die Symbolleistenschaltfläche **&#9655; Ausführen**, um den SQL-Code auszuführen, und überprüfen Sie die Ergebnisse, die in etwa wie folgt aussehen sollten:

    | C1 | c2 | c3 | c4 |
    | -- | -- | -- | -- |
    | ProductID | ProductName | Category | ListPrice |
    | 771 | Mountain-100 Silver, 38 | Mountainbikes | 3399.9900 |
    | 772 | Mountain-100 Silver, 42 | Mountainbikes | 3399.9900 |
    | ... | ... | ... | ... |

5. Beachten Sie, dass die Ergebnisse aus vier Spalten mit den Namen C1, C2, C3 und C4 bestehen und dass die erste Zeile in den Ergebnissen die Namen der Datenfelder enthält. Um dieses Problem zu beheben, fügen Sie der OPENROWSET-Funktion wie hier gezeigt einen Parameter HEADER_ROW = TRUE hinzu (ersetzen Sie dabei *datalakexx* und *fsxx* durch die Namen Ihres Data Lake-Speicherkontos und -Dateisystems), und führen Sie dann die Abfrage erneut aus:

    ```SQL
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    ```

    Die Ergebnisse sehen nun wie folgt aus:

    | ProductID | ProductName | Category | ListPrice |
    | -- | -- | -- | -- |
    | 771 | Mountain-100 Silver, 38 | Mountainbikes | 3399.9900 |
    | 772 | Mountain-100 Silver, 42 | Mountainbikes | 3399.9900 |
    | ... | ... | ... | ... |

6. Ändern Sie die Abfrage wie folgt (ersetzen Sie *datalakexx* und *fsxx* durch die Namen Ihres Data Lake-Speicherkontos und Dateisystems):

    ```SQL
    SELECT
        Category, COUNT(*) AS ProductCount
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    GROUP BY Category;
    ```

7. Führen Sie die geänderte Abfrage aus, die ein Resultset zurückgeben sollte, das die folgende Produktanzahl in den jeweiligen Kategorien enthält:

    | Category | ProductCount |
    | -- | -- |
    | Trägershorts | 3 |
    | Fahrradträger | 1 |
    | ... | ... |

8. Ändern Sie im Bereich **Eigenschaften** den **Namen** für **SQL-Skript 1** in **Produkte nach Kategorie zählen**. Klicken Sie dann auf der Symbolleiste auf **Veröffentlichen**, um das Skript zu speichern.

9. Schließen Sie den Skriptbereich **Produkte nach Kategorie zählen**.

10. Wählen Sie in Synapse Studio die Seite **Entwickeln** aus. Wie Sie sehen, ist hier Ihr veröffentlichtes SQL-Skript **Produkte nach Kategorie zählen** gespeichert.

11. Wählen Sie das SQL-Skript **Produkte nach Kategorie zählen** aus, um es erneut zu öffnen. Vergewissern Sie sicher, dass das Skript mit dem **integrierten** SQL-Pool verbunden ist, und führen Sie es aus, um die Produktanzahl abzurufen.

12. Wählen Sie im **Ergebnisbereich** die **Diagrammansicht** aus, und nehmen Sie folgende Einstellungen für das Diagramm vor:
    - **Diagrammtyp**: Spalte
    - **Kategoriespalte**: Kategorie
    - **Legendenspalten (Reihen)**: ProductCount
    - **Legendenposition**: Unten zentriert
    - **Legendenbeschriftung (Reihen)**: *Nicht ausfüllen*
    - **Mindestwert für Legende (Reihe)**: *Nicht ausfüllen*
    - **Höchstwert für Legende (Reihen)**: *Nicht ausfüllen*
    - **Kategoriebezeichnung**: *Nicht ausfüllen*

    Das resultierende Diagramm sollte in etwa wie folgt aussehen:

    ![Abbildung der Diagrammansicht „Produktanzahl“](images/column-chart.png)

## Verwenden eines Spark-Pools zum Analysieren von Daten

Während SQL eine gängige Sprache zum Abfragen strukturierter Datasets ist, finden viele Datenanalysten Sprachen wie Python nützlich, um Daten zu untersuchen und für die Analyse vorzubereiten. In Azure Synapse Analytics können Sie Python-Code (und anderen Code) in einem *Spark-Pool* ausführen, der eine auf Apache Spark basierende verteilte Datenverarbeitungsengine verwendet.

1. Wählen Sie in Synapse Studio die Seite **Verwalten** aus.
2. Wählen Sie die Registerkarte **Apache Spark-Pools** aus, und verwenden Sie dann das Symbol **&#65291; Neu**, um einen neuen Spark-Pool mit den folgenden Einstellungen zu erstellen:
    - **Name des Apache Spark-Pools**: Spark
    - **Knotengrößenfamilie**: Arbeitsspeicheroptimiert
    - **Knotengröße**: Klein (4 virtuelle Kerne/32 GB)
    - **Autoskalierung**: Aktiviert
    - **Anzahl der Knoten**: 3----3
3. Überprüfen und erstellen Sie den Spark-Pool, und warten Sie, bis er bereitgestellt ist (dies kann einige Minuten dauern).
4. Wenn der Spark-Pool bereitgestellt wurde, navigieren Sie in Synapse Studio auf der Seite **Daten** zum Dateisystem für Ihren Synapse-Arbeitsbereich. Klicken Sie dann mit der rechten Maustaste auf die Datei ** products.csv**, zeigen Sie auf **Neues Notebook**, und wählen Sie **In DataFrame laden** aus.
5. Wählen Sie im daraufhin angezeigten Bereich **Notebook 1** in der Liste **Anfügen an** den **Spark-Pool** aus, den Sie zuvor erstellt haben, und stellen Sie sicher, dass die **Sprache** auf **PySpark (Python)** festgelegt ist.
6. Überprüfen Sie den Code in der ersten (und einzigen) Zelle des Notebooks, die wie folgt aussehen sollte:

    ```Python
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    ##, header=True
    )
    display(df.limit(10))
    ```

7.  Wählen Sie **&#9655; Ausführen** links neben der Codezelle aus, um diese auszuführen, und warten Sie auf die Ergebnisse. Wenn Sie eine Zelle zum ersten Mal in einem Notebook ausführen, wird der Spark-Pool gestartet. Es kann also etwa eine Minute dauern, bis Ergebnisse zurückgegeben werden.

    > **Hinweis**: Wenn ein Fehler auftritt, weil der Python-Kernel noch nicht verfügbar ist, führen Sie die Zelle erneut aus.

8. Letztlich sollten die Ergebnisse unterhalb der Zelle angezeigt werden und in etwa wie folgt aussehen:

    | _c0_ | _c1_ | _c2_ | _c3_ |
    | -- | -- | -- | -- |
    | ProductID | ProductName | Category | ListPrice |
    | 771 | Mountain-100 Silver, 38 | Mountainbikes | 3399.9900 |
    | 772 | Mountain-100 Silver, 42 | Mountainbikes | 3399.9900 |
    | ... | ... | ... | ... |

9. Aufheben der Auskommentierung der Zeile *,header=True* (da die products.csv-Datei die Spaltenüberschriften in der ersten Zeile enthält), sodass Ihr Code wie folgt aussieht:

    ```Python
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    , header=True
    )
    display(df.limit(10))
    ```

10. Führen Sie die Zelle erneut aus, und überprüfen Sie, ob die Ergebnisse wie folgt aussehen:

    | ProductID | ProductName | Category | ListPrice |
    | -- | -- | -- | -- |
    | 771 | Mountain-100 Silver, 38 | Mountainbikes | 3399.9900 |
    | 772 | Mountain-100 Silver, 42 | Mountainbikes | 3399.9900 |
    | ... | ... | ... | ... |

    Beachten Sie, dass das erneute Ausführen der Zelle weniger Zeit in Anspruch nimmt, da der Spark-Pool bereits gestartet wurde.

11. Verwenden Sie unter den Ergebnissen das Symbol **&#65291; Code**, um dem Notebook eine neue Codezelle hinzuzufügen.
12. Fügen Sie in der neuen leeren Codezelle den folgenden Code hinzu:

    ```Python
    df_counts = df.groupBy(df.Category).count()
    display(df_counts)
    ```

13. Führen Sie die neue Codezelle aus, indem Sie links davon auf **&#9655; Ausführen** klicken, und überprüfen Sie die Ergebnisse, die in etwa wie folgt aussehen sollten:

    | Category | count |
    | -- | -- |
    | Lenkköpfe | 3 |
    | Räder | 14 |
    | ... | ... |

14. Wählen Sie in der Ergebnisausgabe für die Zelle die **Diagrammansicht** aus. Das resultierende Diagramm sollte in etwa wie folgt aussehen:

    ![Abbildung der Diagrammansicht „Kategorieanzahl“](images/bar-chart.png)

15. Schließen Sie den Bereich **Notebook 1**, und verwerfen Sie Ihre Änderungen.

## Löschen von Azure-Ressourcen

Wenn Sie der Erkundung von Azure Synapse Analytics fertig sind, löschen Sie die erstellten Ressourcen, um unnötige Azure-Kosten zu vermeiden.

1. Schließen Sie die Synapse Studio-Registerkarte im Browser, und kehren Sie zum Azure-Portal zurück.
2. Wählen Sie auf der **Startseite** des Azure-Portals die Option **Ressource erstellen** aus.
3. Wählen Sie die Ressourcengruppe für Ihren Synapse Analytics-Arbeitsbereich (nicht die verwaltete Ressourcengruppe) aus, und überprüfen Sie, ob sie den Synapse-Arbeitsbereich, das Speicherkonto und den Spark-Pool für Ihren Arbeitsbereich enthält.
4. Wählen Sie oben auf der Seite **Übersicht** für Ihre Ressourcengruppe die Option **Ressourcengruppe löschen** aus.
5. Geben Sie den Namen der Ressourcengruppe ein, um zu bestätigen, dass Sie sie löschen möchten, und wählen Sie **Löschen** aus.

    Nach ein paar Minuten werden Ihr Azure Synapse-Arbeitsbereich und der ihm zugeordnete verwaltete Arbeitsbereich gelöscht.
