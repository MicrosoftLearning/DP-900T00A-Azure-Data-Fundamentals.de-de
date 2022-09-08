---
lab:
  title: "Erkunden der Grundlagen der Datenvisualisierung mit Power\_BI"
  module: Explore fundamentals of data visualization
---

# <a name="explore-fundamentals-of-data-visualization-with-power-bi"></a>Erkunden der Grundlagen der Datenvisualisierung mit Power BI

In dieser Übung verwenden Sie Microsoft Power BI Desktop, um ein Datenmodell und einen Bericht mit interaktiven Datenvisualisierungen zu erstellen.

Dieses Lab dauert ungefähr **20** Minuten.

## <a name="before-you-start"></a>Vorbereitung

Sie benötigen ein [Azure-Abonnement](https://azure.microsoft.com/free), in dem Sie Administratorzugriff besitzen.

### <a name="install-power-bi-desktop"></a>Installieren von Power BI Desktop

Wenn Microsoft Power BI Desktop noch nicht auf Ihrem Windows-Computer installiert ist, können Sie es kostenlos herunterladen und installieren.

1. Laden Sie das Installationsprogramm für Power BI Desktop von [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true) herunter.
1. When the file has downloaded, open it, and use the setup wizard to install Power BI Desktop on your computer. This insatllation may take a few minutes.

## <a name="import-data"></a>Daten importieren

1. Open Power BI Desktop. The application interface should look similar to this:

    ![Screenshot: Power BI Desktop-Startbildschirm](images/power-bi-start.png)

    Jetzt sind Sie bereit, die Daten für Ihren Bericht zu importieren.

1. Wählen Sie auf dem Begrüßungsbildschirm von Power BI Desktop die Option **Daten abrufen** und anschließend in der Liste der Datenquellen die Option **Web** und dann **Verbinden** aus.

    ![Screenshot: Auswahl der Webdatenquelle in Power BI](images/web-source.png)

1. Geben Sie im Dialogfeld **Aus dem Web** die folgende URL ein, und wählen Sie dann **OK** aus:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. Wählen Sie im Dialogfeld „Auf Webinhalt zugreifen“ die Option **Verbinden** aus.

1. Verify that the URL opens a dataset containing customer data, as shown below. Then select <bpt id="p1">**</bpt>Load<ept id="p1">**</ept> to load the data into the data model for your report.

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

## <a name="explore-a-data-model"></a>Erkunden eines Datenmodells

Die drei Importierten Datentabellen wurden in ein Datenmodell geladen, das Sie nun erkunden und optimieren werden.

1. In Power BI Desktop, on the left-side edge, select the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> tab, and then arrange the tables in the model so you can see them. You can hide the panes on the right side by using the <bpt id="p1">**</bpt><ph id="ph1">&gt;&gt;</ph><ept id="p1">**</ept> icons:

    ![Screenshot: Registerkarte „Modell“ in Power BI](images/model-tab.png)

1. Wählen Sie in der Tabelle **Orders** (Bestellungen) das Feld **Revenue** (Umsatz) aus, und legen Sie dann im Bereich **Eigenschaften** die Eigenschaft **Format** auf **Währung** fest:

    ![Screenshot: Festlegen des Umsatzformats in Power BI auf „Währung“](images/revenue-currency.png)

    Durch diesen Schritt wird sichergestellt, dass die Umsatzwerte in den Berichtsvisualisierungen in der entsprechenden Währung angezeigt werden.

1. In the products table, right-click the <bpt id="p1">**</bpt>Category<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Create hierarchy<ept id="p3">**</ept>. This step creates a hierarchy named <bpt id="p1">**</bpt>Category Hierarchy<ept id="p1">**</ept>. You may need to expand or scroll in the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> table to see this - you can also see it in the <bpt id="p2">**</bpt>Fields<ept id="p2">**</ept> pane:

    ![Screenshot: Hinzufügen der Kategoriehierarchie in Power BI](images/category-hierarchy.png)

1. In the products table, right-click the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Add to hierarchy<ept id="p3">**</ept><ph id="ph2"> &gt; </ph><bpt id="p4">**</bpt>Category Hierarchy<ept id="p4">**</ept>. This adds the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field to the hierarchy you created previously.
1. In the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, right-click <bpt id="p2">**</bpt>Category Hierarchy<ept id="p2">**</ept> (or open its <bpt id="p3">**</bpt>...<ept id="p3">**</ept> menu) and select <bpt id="p4">**</bpt>Rename<ept id="p4">**</ept>. Then rename the hierarchy to <bpt id="p1">**</bpt>Categorized Product<ept id="p1">**</ept>.

    ![Screenshot: Umbenennen der Hierarchie in Power BI](images/rename-hierarchy.png)

1. Wählen Sie am linken Rand die Registerkarte **Daten** und dann im Bereich **Felder** die Tabelle **Customers** (Kunden) aus.
1. Wählen Sie die Spaltenüberschrift **City** (Stadt) aus, und legen Sie die Eigenschaft **Datenkategorie** auf **City** (Stadt) fest:

    ![Screenshot: Festlegen einer Datenkategorie in Power BI](images/data-category.png)

    Durch diesen Schritt wird sichergestellt, dass die Werte in dieser Spalte als Städtenamen interpretiert werden, was nützlich sein kann, wenn Sie Kartenvisualisierungen verwenden möchten.

## <a name="create-a-report"></a>Erstellen eines Berichts

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Options and Settings<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Options<ept id="p1">**</ept>, and in the <bpt id="p2">**</bpt>Security<ept id="p2">**</ept> section, ensure that <bpt id="p3">**</bpt>Use Map and Filled Map visuals<ept id="p3">**</ept> is enabled and select <bpt id="p4">**</bpt>OK<ept id="p4">**</ept>.

    ![Screenshot: Festlegen der Eigenschaft der Visuals „Karte verwenden“ und „Flächenkartogramm“ in PowerBI](images/set-options.png)

    Durch diese Einstellung wird sichergestellt, dass Sie Kartenvisualisierungen in Berichte aufnehmen können.

1. Wählen Sie auf der linken Seite die Registerkarte **Bericht** aus, um die Benutzeroberfläche für den Berichtsentwurf anzuzeigen.

    ![Screenshot: Registerkarte „Bericht“ in Power BI](images/report-tab.png)

1. In the ribbon, above the report design surface, select <bpt id="p1">**</bpt>Text Box<ept id="p1">**</ept> and add a text box containing the text <bpt id="p2">**</bpt>Sales Report<ept id="p2">**</ept> to the report. Format the text to make it bold with a font size of 32.

    ![Screenshot: Hinzufügen eines Textfelds in Power BI](images/text-box.png)

1. Wenn die Datei heruntergeladen wurde, öffnen Sie sie, und verwenden Sie den Setup-Assistenten, um Power BI Desktop auf Ihrem Computer zu installieren.

    ![Screenshot: Hinzufügen einer Tabelle mit kategorisierten Produkten zu einem Bericht in Power BI](images/categorized-products-table.png)

1. Diese Installation kann einige Minuten dauern.

    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Data<ept id="p2">**</ept> tab and change the decimal places if you wish.

    ![Screenshot: Tabelle kategorisierter Produkte mit Umsatz in einem Bericht](images/revenue-column.png)

1. With the table still selected, in the <bpt id="p1">**</bpt>Visualizations<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Stacked column chart<ept id="p2">**</ept> visualization. The table is changed to a column chart showing revenue by category.

    ![Screenshot: Gestapeltes Säulendiagramm kategorisierter Produkte mit Umsatz in einem Bericht](images/stacked-column-chart.png)

1. Öffnen Sie Power BI Desktop.

    ![Screenshot: Säulendiagramm mit Detailinformationen zu Produkten innerhalb einer Kategorie](images/drill-down.png)

1. Die Anwendungsschnittstelle sollte in etwa wie folgt aussehen:
1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Quantity<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>orders<ept id="p3">**</ept> table and the <bpt id="p4">**</bpt>Category<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>products<ept id="p5">**</ept> table. This step results in another column chart showing sales quantity by product category.
1. Wählen Sie bei ausgewähltem neuen Säulendiagramm im Bereich **Visualisierungen** die Option **Kreisdiagramm** aus, ändern Sie dann die Größe des Diagramms, und positionieren Sie es neben dem Säulendiagramm für den Umsatz nach Kategorie.

    ![Screenshot: Kreisdiagramm, das die Umsatzmenge nach Kategorie anzeigt](images/category-pie-chart.png)

1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>City<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>customers<ept id="p3">**</ept> table and then select the <bpt id="p4">**</bpt>Revenue<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>orders<ept id="p5">**</ept> table. This results in a map showing sales revenue by city. Rearrange and resize the visualizations as needed:

    ![Screenshot: Karte mit dem Umsatz nach Stadt](images/revenue-map.png)

1. In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.

    ![Screenshot: Karte mit Umsatz nach Stadt, wobei die Daten für die ausgewählte Stadt hervorgehoben sind](images/selected-data.png)

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Save<ept id="p2">**</ept>. Then save the file with an appropriate .pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

Wenn Sie über ein Abonnement des [Power BI-Diensts](https://www.powerbi.com/?azure-portal=true) verfügen, können Sie sich bei Ihrem Konto anmelden und den Bericht in einem Power BI-Arbeitsbereich veröffentlichen. 
