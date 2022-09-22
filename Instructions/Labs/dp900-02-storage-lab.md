---
lab:
  title: Erkunden von Azure Storage
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-azure-storage"></a>Erkunden von Azure Storage

In dieser Übung stellen Sie ein Azure Storage-Konto in Ihrem Azure-Abonnement bereit und erkunden die verschiedenen Möglichkeiten, es zum Speichern von Daten zu verwenden.

Dieses Lab dauert ungefähr **15** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

## <a name="provision-an-azure-storage-account"></a>Bereitstellen eines Azure Storage-Kontos

Der erste Schritt bei der Verwendung von Azure Storage ist die Bereitstellung eines Azure Storage-Kontos in Ihrem Azure-Abonnement.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an, falls Sie dies noch nicht getan haben.
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Geben Sie auf der Seite **Erstellen eines Speicherkontos** die folgenden Werte ein:
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Ressourcengruppe**: Wenn Sie eine Sandbox verwenden, wählen Sie die vorhandene Ressourcengruppe aus (mit einem ähnlichen Namen wie *learn-xxxx....* ). Erstellen Sie andernfalls eine neue Ressourcengruppe mit einem Namen Ihrer Wahl.
    - **Speicherkontoname**: Geben Sie einen eindeutigen Namen für Ihr Speicherkonto mit Kleinbuchstaben und Zahlen ein.
    - **Region**: Wählen Sie einen beliebigen verfügbaren Standort aus.
    - **Leistung**: *Standard*
    - **Redundanz**: *Lokal redundanter Speicher (LRS)*

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. Fahren Sie mit den verbleibenden Seiten **Weiter >** fort, ohne die Standardeinstellungen zu ändern. Warten Sie dann auf der Seite **Überprüfen + erstellen**, bis Ihre Auswahl überprüft wurde, und wählen Sie **Erstellen** aus, um Ihr Azure Storage-Konto zu erstellen.
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>Erkunden von Blobspeicher

Nachdem Sie nun über ein Azure Storage-Konto verfügen, können Sie einen Container für Blobdaten erstellen.

1. Laden Sie die JSON-Datei [product1.json](https://aka.ms/product1.json?azure-portal=true) von `https://aka.ms/product1.json` herunter, und speichern Sie sie auf Ihrem Computer (Sie können sie in einem beliebigen Ordner speichern. Später laden Sie sie in Blobspeicher hoch).

    *Wenn die JSON-Datei in Ihrem Browser angezeigt wird, speichern Sie die Seite als **product1.json**.*

1. Wählen Sie auf der Azure-Portalseite für Ihren Speichercontainer auf der linken Seite im Abschnitt **Datenspeicher** die Option **Container** aus.
1. Wählen Sie auf der Seite **Container** die Option **&#65291; Container** aus, und fügen Sie einen neuen Container namens **data** mit der öffentlichen Zugriffsebene **Privat (kein anonymer Zugriff)** hinzu.
1. Wenn der Container **data** erstellt wurde, überprüfen Sie, ob er auf der Seite **Container** aufgeführt ist.
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. Wählen Sie auf der Seite des Speicherbrowsers **Blobcontainer** aus, und überprüfen Sie, ob Ihr Container **data** aufgeführt ist.
1. Wählen Sie den Container **data** aus, und beachten Sie, dass er leer ist.
1. Wählen Sie **&#65291; Verzeichnis hinzufügen** aus, und lesen Sie die Informationen zu Ordnern, bevor Sie ein neues Verzeichnis namens **products** erstellen.
1. Überprüfen Sie im Speicher-Explorer, ob in der aktuellen Ansicht der Inhalt des soeben erstellten Ordners **products** angezeigt wird. Beachten Sie, dass die „Breadcrumbs“ oben auf der Seite den Pfad **Blobcontainer > data > products** widerspiegeln.
1. Wählen Sie in den Breadcrumbs **Daten** aus, um zum Container **data** zu wechseln, und beachten Sie, dass er <u>keinen</u> Ordner namens **products** enthält.

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. Verwenden Sie die Schaltfläche **&#10514; Hochladen**, um den Bereich **Blob hochladen** zu öffnen.
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. Schließen Sie den Bereich **Blob hochladen**, wenn er noch geöffnet ist, und überprüfen Sie, ob ein virtueller Ordner **product_data** im Container **data** erstellt wurde.
1. Wählen Sie den Ordner **product_data** aus, und vergewissern Sie sich, dass er das hochgeladene Blob **product1.json** enthält.
1. Wählen Sie auf der linken Seite im Abschnitt **Datenspeicher** die Option **Container** aus.
1. Öffnen Sie den Container **data**, und überprüfen Sie, ob der Ordner **product_data** aufgeführt ist, den Sie erstellt haben.
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. Verwenden Sie das Symbol **X** oben rechts auf der Seite **data**, um die Seite zu schließen und zur Seite **Container** zurückzukehren.

## <a name="explore-azure-data-lake-storage-gen2"></a>Erkunden von Azure Data Lake Storage Gen2

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. Laden Sie die JSON-Datei [product2.json](https://aka.ms/product2.json?azure-portal=true) von `https://aka.ms/product2.json` herunter, und speichern Sie sie auf Ihrem Computer in dem Ordner, in den Sie zuvor **product1.json** heruntergeladen haben. Sie laden sie später in Blob Storage hoch.
1. Scrollen Sie im Azure-Portal auf der Seite Ihres Speicherkontos links nach unten zum Abschnitt **Einstellungen**, und wählen Sie **Data Lake Gen2-Upgrade** aus.
1. Wählen Sie auf der Startseite des Azure-Portals links oben **&#65291; Ressource erstellen** aus, und suchen Sie nach *Speicherkonto*.
1. Wenn das Upgrade abgeschlossen ist, wählen Sie im Bereich auf der linken Seite im oberen Abschnitt **Speicherbrowser** aus, und navigieren Sie zurück zum Stamm Ihres Blobcontainers **data**, der weiterhin den Ordner **product_data** enthält.
1. Wählen Sie den Ordner **product_data** aus, und vergewissern Sie sich, dass er noch die Datei **product1.json** enthält, die Sie zuvor hochgeladen haben.
1. Verwenden Sie die Schaltfläche **&#10514; Hochladen**, um den Bereich **Blob hochladen** zu öffnen.
1. Wählen Sie dann auf der resultierenden Seite **Speicherkonto** die Option **Erstellen** aus.
1. Schließen Sie den Bereich **Blob hochladen**, wenn er noch geöffnet ist, und überprüfen Sie, ob ein Ordner **product_data** jetzt die Datei **product2.json** enthält.
1. Wählen Sie auf der linken Seite im Abschnitt **Datenspeicher** die Option **Container** aus.
1. Öffnen Sie den Container **data**, und überprüfen Sie, ob der Ordner **product_data** aufgeführt ist, den Sie erstellt haben.
1. Wählen Sie das Symbol **&#x2027;&#x2027;&#x2027;** am rechten Ende des Ordners aus, und beachten Sie, dass Sie Konfigurationsaufgaben wie das Umbenennen von Ordnern und das Festlegen von Berechtigungen auf Ordnerebene ausführen können, wenn der hierarchische Namespace aktiviert ist.
1. Verwenden Sie das Symbol **X** oben rechts auf der Seite **data**, um die Seite zu schließen und zur Seite **Container** zurückzukehren.

## <a name="explore-azure-files"></a>Erkunden von Azure Files

Azure Files bietet eine Möglichkeit, cloudbasierte Dateifreigaben zu erstellen.

1. Wählen Sie auf der Azure-Portalseite für Ihren Speichercontainer auf der linken Seite im Abschnitt **Datenspeicher** die Option **Dateifreigaben** aus.
1. Wählen Sie auf der Seite „Dateifreigaben“ die Option **&#65291; Dateifreigabe** aus, und fügen Sie mithilfe der Ebene **Transaktion optimiert** eine neue Dateifreigabe namens **files** hinzu.
1. Öffnen Sie ihre neue Freigabe **files** in den **Dateifreigaben**.
1. At the top of the page, select <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept>. Then in the <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept> pane, note that there are tabs for common operating systems (Windows, Linux, and macOS) that contain scripts you can run to connect to the shared folder from a client computer.
1. Schließen Sie den Bereich **Verbinden** und dann die Seite **files**, um zur Seite **Dateifreigaben** für Ihr Azure-Speicherkonto zurückzukehren.

## <a name="explore-azure-tables"></a>Erkunden von Azure Tables

Azure Tables bietet einen Schlüssel-Wert-Speicher für Anwendungen, die Datenwerte speichern müssen, aber nicht die vollständige Funktionalität und Struktur einer relationalen Datenbank benötigen.

1. Wählen Sie auf der Azure-Portalseite für Ihren Speichercontainer auf der linken Seite im Abschnitt **Datenspeicher** die Option **Tabellen** aus.
1. Wählen Sie auf der Seite **Tabellen** die Option **&#65291; Tabelle** aus, und erstellen Sie eine neue Tabelle mit dem Namen **products**.
1. Nachdem die Tabelle **products** erstellt wurde, wählen Sie im Bereich auf der linken Seite im oberen Abschnitt **Speicherbrowser** aus.
1. Wählen Sie im Speicher-Explorer **Tabellen** aus, und überprüfen Sie, ob die Tabelle **products** aufgeführt ist.
1. Wählen Sie die Tabelle **products** aus.
1. Wählen Sie auf der Seite **product** die Option **&#65291; Entität hinzufügen** aus.
1. Geben Sie im Bereich **Entität hinzufügen** die folgenden Schlüsselwerte ein:
    - **PartitionKey**: 1
    - **RowKey**: 1
1. Wählen Sie **Eigenschaft hinzufügen** aus, und erstellen Sie eine neue Eigenschaft mit den folgenden Werten:

    |Eigenschaftenname | type | Wert |
    | ------------ | ---- | ----- |
    | Name | String | Widget |

1. Fügen Sie eine zweite Eigenschaft mit den folgenden Werten hinzu:

    |Eigenschaftenname | type | Wert |
    | ------------ | ---- | ----- |
    | Preis | Double | 2,99 |

1. Wählen Sie **Einfügen** aus, um eine Zeile für die neue Entität in die Tabelle einzufügen.
1. Überprüfen Sie im Speicherbrowser, ob der Tabelle **products** eine Zeile hinzugefügt wurde, und ob eine Spalte **Zeitstempel** erstellt wurde, um anzugeben, wann die Zeile zuletzt geändert wurde.
1. Fügen Sie der Tabelle **products** eine weitere Entität mit den folgenden Eigenschaften hinzu:

    |Eigenschaftenname | type | Wert |
    | ------------ | ---- | ----- |
    | PartitionKey | String | 1 |
    | RowKey | String | 2 |
    | Name | String | Kniknak |
    | Preis | Double | 1.99 |
    | Eingestellt | Boolean | true |

1. Überprüfen Sie nach dem Einfügen der neuen Entität, ob eine Zeile mit dem eingestellten Produkt in der Tabelle angezeigt wird.

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> **Tipp**: Wenn Sie die Erkundung von Azure Storage abgeschlossen haben, können Sie die in dieser Übung erstellte Ressourcengruppe löschen.
