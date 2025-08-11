# Create pdf and write table data there

```dart
import 'package:open_file/open_file.dart';
import 'package:path_provider/path_provider.dart';
import 'package:pdf/pdf.dart';
import 'package:pdf/widgets.dart' as pw;
```
```dart
 void createPdfWithTable() async {
    final pdf = pw.Document();

    pdf.addPage(
      pw.Page(
        build: (context) {
          return pw.Center(
            child: pw.TableHelper.fromTextArray(
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

    final outputDir = await getApplicationDocumentsDirectory();

    // Construct the full file path
    final filePath = '${outputDir.path}/table_example.pdf';

    final file = File(filePath);
    await file.writeAsBytes(await pdf.save());

    print('PDF saved at $filePath');
    final result = await OpenFile.open(filePath);
    print('Open file result: ${result.message}');
  }
```
