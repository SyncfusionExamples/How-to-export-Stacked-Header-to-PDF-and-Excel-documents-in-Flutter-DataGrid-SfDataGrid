# How to export DataGrid content with a Stacked Header to PDF and Excel documents in Flutter DataGrid (SfDataGrid)?

In this article, you can learn about how to export DataGrid content with a Stacked Header to PDF and Excel documents in the [Flutter DataGrid](https://help.syncfusion.com/flutter/datagrid/getting-started).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the required properties. To ensure proper export of the [StackedHeaderRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderRow-class.html) to Excel or PDF, it is crucial to define the corresponding text within the [StackedHeaderCell.text](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderCell/text.html) property. As widgets cannot be exported to Excel or PDF, setting this property is essential to provide the appropriate text during the export process of the SfDataGrid to Excel or PDF.

```dart
  Future<void> exportDataGridToPDF() async {
    final sf_pdf.PdfDocument document = key.currentState!.exportToPdfDocument();
    final List<int> bytes = document.saveSync();
    await helper.saveAndLaunchFile(bytes, 'DataGrid.pdf');
    document.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: Column(
        children: [
          Container(
            margin: const EdgeInsets.symmetric(vertical: 10),
            width: 250,
            child: ElevatedButton.icon(
                icon: const Icon(Icons.print),
                onPressed: () => exportDataGridToPDF(),
                label: const Text('Export to PDF')),
          ),
          Expanded(
            child: SfDataGrid(
              key: key,
              source: employeeDataSource,
              stackedHeaderRows: [
                StackedHeaderRow(
                  cells: [
                    StackedHeaderCell(
                      text: 'Employee Details', // Text used when exporting
                      columnNames: ['id', 'name', 'designation', 'salary'],
                      child: const Center(child: Text('Employee Details')),
                    ),
                  ],
                ),
              ],
              columns: getColumns,
            ),
          ),
        ],
      ),
    );
  }
```

You can download the example from [GitHub](https://github.com/SyncfusionExamples/How-to-export-Stacked-Header-to-PDF-and-Excel-documents-in-Flutter-DataGrid-SfDataGrid)