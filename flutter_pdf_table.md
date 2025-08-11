# Sample make pdf and write table data

```dart
import 'package:pdf/pdf.dart';
import 'package:pdf/widgets.dart' as pw;
import 'dart:io';

void createPdfWithTable() async {
  final pdf = pw.Document();

  pdf.addPage(
    pw.Page(
      build: (context) {
        return pw.Center(
          child: pw.Table.fromTextArray(
            headers: ['Name', 'Age', 'City'],
            data: [
              ['Alice', '25', 'New York'],
              ['Bob', '30', 'Chicago'],
              ['Charlie', '22', 'San Francisco'],
            ],
          ),
        );
      },
    ),
  );

  final file = File('table_example.pdf');
  await file.writeAsBytes(await pdf.save());
}

```
