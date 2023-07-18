---
lab:
  title: "Erkunden der Grundlagen der Datenvisualisierung mit Power\_BI"
  module: Explore fundamentals of data visualization
---

# Erkunden der Grundlagen der Datenvisualisierung mit Power BI

In dieser Übung verwenden Sie Microsoft Power BI Desktop, um ein Datenmodell und einen Bericht mit interaktiven Datenvisualisierungen zu erstellen.

Dieses Lab dauert ungefähr **20** Minuten.

## Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

### Installieren von Power BI Desktop

Wenn Microsoft Power BI Desktop noch nicht auf Ihrem Windows-Computer installiert ist, können Sie es kostenlos herunterladen und installieren.

1. Laden Sie das Installationsprogramm für Power BI Desktop von [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true) herunter.
1. Wenn die Datei heruntergeladen wurde, öffnen Sie sie, und verwenden Sie den Setup-Assistenten, um Power BI Desktop auf Ihrem Computer zu installieren. Diese Installation kann einige Minuten dauern.

## Daten importieren

1. Öffnen Sie Power BI Desktop. Die Anwendungsschnittstelle sollte in etwa wie folgt aussehen:

    ![Screenshot: Power BI Desktop-Startbildschirm](images/power-bi-start.png)

    Jetzt sind Sie bereit, die Daten für Ihren Bericht zu importieren.

1. Wählen Sie auf dem Begrüßungsbildschirm von Power BI Desktop die Option **Daten abrufen** und anschließend in der Liste der Datenquellen die Option **Web** und dann **Verbinden** aus.

    ![Screenshot: Auswahl der Webdatenquelle in Power BI](images/web-source.png)

1. Geben Sie im Dialogfeld **Aus dem Web** die folgende URL ein, und wählen Sie dann **OK** aus:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. Wählen Sie im Dialogfeld „Auf Webinhalt zugreifen“ die Option **Verbinden** aus.

1. Überprüfen Sie, ob die URL ein Dataset mit Kundendaten öffnet, wie unten dargestellt. Wählen Sie dann **Laden** aus, um die Daten in das Datenmodell für Ihren Bericht zu laden.

    ![Screenshot: Dataset mit Kundendaten, die in Power BI angezeigt werden](images/customers.png)

1. Wählen Sie im Hauptfenster von Power BI Desktop im Menü „Daten“ die Option **Daten abrufen** und dann die Option **Web** aus:

    ![Screenshot: Menü „Daten abrufen“ in Power BI](images/get-data.png)

1. Geben Sie im Dialogfeld **Aus dem Web** die folgende URL ein, und wählen Sie dann **OK** aus:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. Wählen Sie im Dialogfeld die Option **Laden** aus, um die Produktdaten in dieser Datei in das Datenmodell zu laden.

1. Wiederholen Sie die vorherigen drei Schritte, um ein drittes Dataset mit Bestelldaten aus der folgenden URL zu importieren:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## Erkunden eines Datenmodells

Die drei Importierten Datentabellen wurden in ein Datenmodell geladen, das Sie nun erkunden und optimieren werden.

1. Wählen Sie in Power BI Desktop am linken Rand die Registerkarte **Modell** aus, und ordnen Sie die Tabellen im Modell so an, dass sie sichtbar sind. Sie können die Bereiche auf der rechten Seite mithilfe der **>>** -Symbole ausblenden:

    ![Screenshot: Registerkarte „Modell“ in Power BI](images/model-tab.png)

1. Wählen Sie in der Tabelle **Orders** (Bestellungen) das Feld **Revenue** (Umsatz) aus, und legen Sie dann im Bereich **Eigenschaften** die Eigenschaft **Format** auf **Währung** fest:

    ![Screenshot: Festlegen des Umsatzformats in Power BI auf „Währung“](images/revenue-currency.png)

    Durch diesen Schritt wird sichergestellt, dass die Umsatzwerte in den Berichtsvisualisierungen in der entsprechenden Währung angezeigt werden.

1. Klicken Sie in der Tabelle der Produkte mit der rechten Maustaste auf das Feld **Kategorie** (oder öffnen Sie dessen Menü **&vellip;** ), und wählen Sie **Hierarchie erstellen** aus. Dieser Schritt erstellt eine Hierarchie namens **Kategoriehierarchie**. Möglicherweise müssen Sie die Ansicht in der Tabelle **products** erweitern oder scrollen, um diese Hierarchie zu sehen. Sie wird auch im Bereich **Felder** angezeigt:

    ![Screenshot: Hinzufügen der Kategoriehierarchie in Power BI](images/category-hierarchy.png)

1. Klicken Sie in der Produkttabelle mit der rechten Maustaste auf das Feld **ProductName** (oder öffnen Sie das zugehörige Menü **&vellip;** ), und wählen Sie **Zu Hierarchie hinzufügen** > **Kategoriehierarchie** aus. Dadurch wird das Feld **ProductName** (Produktname) zur zuvor erstellten Hierarchie hinzugefügt.
1. Klicken Sie im Bereich **Felder** mit der rechten Maustaste auf **Kategoriehierarchie** (oder öffnen Sie das Menü **...**), und wählen Sie **Umbenennen** aus. Benennen Sie die Hierarchie in **Kategorisiertes Produkt** um.

    ![Screenshot: Umbenennen der Hierarchie in Power BI](images/rename-hierarchy.png)

1. Wählen Sie am linken Rand die Registerkarte **Datenansicht** und dann im Bereich **Daten** die Tabelle **Customers** (Kunden) aus.
1. Wählen Sie die Spaltenüberschrift **City** (Stadt) aus, und legen Sie die Eigenschaft **Datenkategorie** auf **City** (Stadt) fest:

    ![Screenshot: Festlegen einer Datenkategorie in Power BI](images/data-category.png)

    Durch diesen Schritt wird sichergestellt, dass die Werte in dieser Spalte als Städtenamen interpretiert werden, was nützlich sein kann, wenn Sie Kartenvisualisierungen verwenden möchten.

## Erstellen eines Berichts

Jetzt sind Sie fast so weit, einen Bericht zu erstellen. Zunächst müssen Sie einige Einstellungen überprüfen, um sicherzustellen, dass alle Visualisierungen aktiviert sind.

1. Wählen Sie im Menü **Datei** die Option **Optionen und Einstellungen** aus. Wählen Sie dann **Optionen** aus, und vergewissern Sie sich im Abschnitt **Sicherheit**, dass die Option **Verwenden von Kartenvisuals und Flächenkartogrammen** aktiviert ist, und wählen Sie **OK** aus.

    ![Screenshot: Festlegen der Eigenschaft der Visuals „Karte verwenden“ und „Flächenkartogramm“ in PowerBI](images/set-options.png)

    Durch diese Einstellung wird sichergestellt, dass Sie Kartenvisualisierungen in Berichte aufnehmen können.

1. Wählen Sie auf der linken Seite die Registerkarte **Berichtansicht** aus, um die Benutzeroberfläche für den Berichtsentwurf anzuzeigen.

    ![Screenshot: Registerkarte „Bericht“ in Power BI](images/report-tab.png)

1. Wählen Sie im Menüband oberhalb der Berichtsentwurfsoberfläche **Textfeld** aus, und fügen Sie dem Bericht ein Textfeld mit dem Text **Sales Report** (Umsatzbericht) hinzu. Formatieren Sie den Text so, dass er fett angezeigt wird und einen Schriftgrad von 32 hat.

    ![Screenshot: Hinzufügen eines Textfelds in Power BI](images/text-box.png)

1. Wählen Sie einen leeren Bereich im Bericht aus, um die Auswahl des Textfelds aufzuheben. Erweitern Sie dann im Bereich **Daten** das Feld **Products** (Produkte), und wählen Sie das Feld **Categorized Products** (Kategorisierte Produkte) aus. Durch diesen Schritt wird dem Bericht eine Tabelle hinzufügt.

    ![Screenshot: Hinzufügen einer Tabelle mit kategorisierten Produkten zu einem Bericht in Power BI](images/categorized-products-table.png)

1. Mit weiterhin ausgewählter Tabelle erweitern Sie im Bereich **Daten** den Bereich **Orders** (Bestellungen), und wählen Sie **Revenue** (Umsatz) aus. Eine Spalte „Revenue“ (Umsatz) wird der Tabelle hinzugefügt. Möglicherweise müssen Sie die Größe der Tabelle erweitern, damit sie sichtbar wird.

    Der Umsatz wird in der Währung formatiert, die Sie im Modell angegeben haben. Allerdings haben Sie die Anzahl der Dezimalstellen nicht angegeben, sodass die Werte auch Bruchbeträge enthalten. Für die Visualisierungen, die Sie erstellen werden, spielt das keine Rolle, aber Sie können zur Registerkarte **Modell** oder **Daten** wechseln und bei Bedarf die Dezimalstellen ändern.

    ![Screenshot: Tabelle kategorisierter Produkte mit Umsatz in einem Bericht](images/revenue-column.png)

1. Wählen Sie bei ausgewählter Tabelle im Bereich **Visualisierungen** die Visualisierung **Gestapeltes Säulendiagramm** aus. Die Tabelle wird in ein Säulendiagramm geändert, in dem der Umsatz nach Kategorie angezeigt wird.

    ![Screenshot: Gestapeltes Säulendiagramm kategorisierter Produkte mit Umsatz in einem Bericht](images/stacked-column-chart.png)

1. Wählen Sie oberhalb des ausgewählten Säulendiagramms das Symbol **&#8595;** aus, um den Drilldown zu aktivieren. Wählen Sie in der Tabelle die zweite Spalte aus, um einen Drilldown auszuführen und den Umsatz für die einzelnen Produkte in dieser Kategorie anzuzeigen. Diese Funktion ist möglich, da Sie eine Hierarchie von Kategorien und Produkten definiert haben.

    ![Screenshot: Säulendiagramm mit Detailinformationen zu Produkten innerhalb einer Kategorie](images/drill-down.png)

1. Verwenden Sie das Symbol **&#x2191;** , um einen Drillup zur Kategorieebene durchzuführen. Wählen Sie dann das Symbol **(** &#8595; **)** aus, um das Drilldownfeature zu deaktivieren.
1. Wählen Sie einen leeren Bereich des Berichts aus, und wählen Sie dann im Bereich **Daten** das Feld **Menge** in der Tabelle **Orders** (Bestellungen) und das Feld **Category** in der Tabelle **Products** (Produkte) aus. Dieser Schritt führt zu einem weiteren Säulendiagramm, das die Umsatzmenge nach Produktkategorie zeigt.
1. Wählen Sie bei ausgewähltem neuen Säulendiagramm im Bereich **Visualisierungen** die Option **Kreisdiagramm** aus, ändern Sie dann die Größe des Diagramms, und positionieren Sie es neben dem Säulendiagramm für den Umsatz nach Kategorie.

    ![Screenshot: Kreisdiagramm, das die Umsatzmenge nach Kategorie anzeigt](images/category-pie-chart.png)

1. Wählen Sie einen leeren Bereich des Berichts aus, und wählen Sie dann im Bereich **Daten** das Feld **City** (Stadt) in der Tabelle **Customers** (Kunden) und das Feld **Revenue** (Umsatz) in der Tabelle **Orders** (Bestellungen) aus. Dies führt zu einer Karte mit dem Umsatz nach Stadt. Sie können die Visualisierungen nach Bedarf neu anordnen und ihre Größe anpassen:

    ![Screenshot: Karte mit dem Umsatz nach Stadt](images/revenue-map.png)

1. Beachten Sie, dass Sie auf der Karte ziehen, doppelklicken, ein Mausrad verwenden oder auf einem Touchscreen entsprechend Ausschnitte verkleinern und vergrößern können, um zu interagieren. Wählen Sie dann eine bestimmte Stadt aus, und beachten Sie, dass die anderen Visualisierungen im Bericht geändert werden, um die Daten für die ausgewählte Stadt hervorzuheben.

    ![Screenshot: Karte mit Umsatz nach Stadt, wobei die Daten für die ausgewählte Stadt hervorgehoben sind](images/selected-data.png)

1. Klicken Sie im Menü **Datei** auf **Speichern**. Speichern Sie dann die Datei unter einem geeigneten PBIX-Dateinamen. Sie können die Datei öffnen und die Datenmodellierung und -visualisierung in aller Ruhe weiter erkunden.

Wenn Sie über ein Abonnement des [Power BI-Diensts](https://www.powerbi.com/?azure-portal=true) verfügen, können Sie sich bei Ihrem Konto anmelden und den Bericht in einem Power BI-Arbeitsbereich veröffentlichen. 
